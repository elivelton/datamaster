
# Criar a função Lambda `lambda_consumer_batch` (Consumer Batch)

Este guia cria a função **Lambda** que consome eventos do **Kinesis Data Stream (`broker`)** e salva **dados brutos** no **Amazon S3**, **particionados por ano/mês/dia** no prefixo `raw/`.

---

## ✅ Objetivo
- Receber registros do Kinesis (produzidos pelo *Producer*).
- Decodificar payload (Base64 → UTF‑8 → JSON).
- Gravar o JSON **como está** (append‑only) em `s3://<bucket>/raw/<YYYY>/<MM>/<DD>/weather-data-<timestamp>.json`.

---

## 📋 Pré‑requisitos
- **Kinesis Data Stream** `broker` criado.
- **Bucket S3** criado com as pastas `raw/` e `gold/` (opcional para agora).
- **IAM Role** `Consumer-Batch` criada com as policies:
  - `AWSLambdaBasicExecutionRole`
  - `AmazonKinesisFullAccess`
  - `AmazonS3FullAccess`
- Função **`Producer`** disponível para gerar eventos de teste.

> 🔐 Em produção, substitua *FullAccess* por políticas **de menor privilégio** específicas para o stream e o bucket/prefixo.

---

## 1) Criar a função Lambda
1. Acesse **AWS Lambda** → **Create function**.
2. **Author from scratch**.
3. **Function name**: `lambda_consumer_batch`
4. **Runtime**: `Python 3.12`.
5. **Execution role** → **Use an existing role** → selecione **`Consumer-Batch`**.
6. Clique em **Create function**.

---

## 2) Adicionar o código
1. Na aba **Code**, apague o exemplo inicial.
2. **Cole o código** do *Consumer Batch* (do seu material do curso). O fluxo típico é:
   - Ler `event["Records"]`.
   - `base64.b64decode(...)` → `.decode("utf-8")` → `json.loads(...)`.
   - Montar chave S3: `raw/<YYYY>/<MM>/<DD>/weather-data-<ISO_TIMESTAMP>.json`.
   - `s3_client.put_object(Bucket=<BUCKET>, Key=<KEY>, Body=json.dumps(data))`.
3. Clique em **Deploy** (obrigatório ao colar/editar o código no editor).

> ℹ️ As dependências usadas são do runtime padrão (ex.: `boto3` já vem no AWS Lambda Python).

---

## 3) Variáveis de ambiente
1. Vá em **Configuration → Environment variables** → **Edit** → **Add environment variable**.
2. Crie a variável do nome do bucket:
   - **Key**: `BUCKET_NAME` *(ou **exatamente** o nome que o seu código espera; evite espaços em nomes de variáveis)*
   - **Value**: o nome do seu bucket (ex.: `weather-rt`).
3. **Save**.

> O código lerá o nome do bucket desta variável e gravará sempre sob o prefixo `raw/` com partição por data.

---

## 4) Conectar o gatilho do Kinesis
1. Acesse **Configuration → Triggers** → **Add trigger**.
2. **Trigger**: `Kinesis`.
3. **Kinesis stream**: selecione **`broker`**.
4. Demais opções: mantenha os **padrões**.
5. Clique em **Add**. O diagrama passará a mostrar o **Kinesis** como origem.

---

## 5) Testar de ponta a ponta
**Opção A – Producer manual**  
1. Abra a função **`Producer`** → **Test** (payload `{}`).
2. O Producer envia registros para `broker`, acionando `lambda_consumer_batch`.

**Opção B – Agendado (EventBridge)**  
1. Habilite o *schedule* que chama o **Producer** (1–3 min).

**Esperado no S3**  
- Em `s3://<bucket>/raw/<YYYY>/<MM>/<DD>/` devem surgir arquivos `weather-data-<timestamp>.json` (um por evento).

---

## 6) Validar no S3
1. Abra **S3 → seu bucket → raw/** e navegue por **ano/mês/dia**.
2. Baixe um arquivo e confira o JSON salvo **sem transformações**.

---

## 7) Dicas e solução de problemas
- **Nada chega ao S3**: verifique **CloudWatch Logs** da função para erros, a variável `BUCKET_NAME` e a **Role** anexada.
- **Permissão negada**: confirme políticas da role (`s3:PutObject`, `kinesis:GetRecords`, etc.).
- **Muitas execuções do Realtime**: desabilite temporariamente o *schedule* do Producer ou aumente os limiares do `Consumer-Realtime` para evitar envios de SNS durante seus testes.

---

## ✅ Resultado
A função **`lambda_consumer_batch`** está criada, assinando o **Kinesis `broker`** e persistindo **dados brutos particionados** no **S3** sob `raw/YYYY/MM/DD/`.
