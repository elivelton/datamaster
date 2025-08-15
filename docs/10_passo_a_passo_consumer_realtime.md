
# Criar o **Consumer Realtime** (AWS Lambda) – Passo a Passo

Este guia cria a função **Lambda `Consumer-Realtime`** que lê eventos do **Kinesis Data Stream (`broker`)**, avalia parâmetros meteorológicos e **dispara alertas via SNS** (e‑mail/SMS) quando os limiares forem atingidos.

---

## ✅ Pré‑requisitos
- Stream Kinesis **`broker`** criado.
- Função Lambda **`Producer`** funcionando (produz eventos no `broker`).
- **Tópico SNS** criado e com subscriptions confirmadas (e‑mail/SMS).
- **IAM Role `Consumer-Realtime`** criada com as políticas:
  - `AWSLambdaKinesisExecutionRole`
  - `AmazonSNSFullAccess`

> Você precisará do **ARN do tópico SNS** para configurar o código do Consumer.

---

## 1) Criar a função Lambda
1. Abra **AWS Lambda** → **Create function**.
2. **Author from scratch**.
3. **Function name**: `Consumer-Realtime`  
4. **Runtime**: `Python 3.12` (use esta versão para acompanhar o curso).
5. **Execution role** → **Use an existing role** → selecione **`Consumer-Realtime`**.
6. Clique em **Create function**.

---

## 2) Adicionar o código
1. Na aba **Code**, apague o arquivo de exemplo (`lambda_function.py` inicial).
2. **Cole o código do Consumer** (do material do curso).
3. **Substitua** no código a variável do **ARN do tópico SNS** pelo **ARN do seu tópico** (copie em **SNS → Topics → [seu tópico]**).
4. Clique em **Deploy** (obrigatório ao colar/editar código no editor).

> Dica: Nesta função **não** é usado `requests`; as imports padrão citadas no curso já existem no runtime do Lambda.

---

## 3) Configurar variáveis de ambiente
1. Vá em **Configuration → Environment variables** → **Edit** → **Add environment variable**.
2. **Crie as quatro variáveis** (exemplo de nomes e valores):
   | Name                          | Value |
   |-------------------------------|-------|
   | `PRECIPITATION_PROB_THRESHOLD`| `70`  |
   | `WIND_SPEED_THRESHOLD`        | `10`  |
   | `WIND_GUST_THRESHOLD`         | `0`   |
   | `RAIN_INTENSITY_THRESHOLD`    | `5`   |

   - Use **`0` em `WIND_GUST_THRESHOLD`** apenas para **facilitar o teste** (garante disparo). Em produção, ajuste para um valor realista.
3. **Save**.

> O código lê essas variáveis do ambiente e compara com os valores recebidos do stream (probabilidade de chuva, velocidade do vento, rajadas e intensidade de chuva). Se **qualquer** parâmetro ≥ limiar, o SNS é publicado.

---

## 4) Ligar o gatilho do Kinesis
1. **Configuration → Triggers** → **Add trigger**.
2. **Trigger**: `Kinesis`.
3. **Kinesis stream**: selecione **`broker`**.
4. Mantenha os demais padrões → **Add**.

Você verá no diagrama que a origem da Lambda passa a ser o **Kinesis**.

---

## 5) Testar de ponta a ponta
1. Abra a função **`Producer`**.
2. Clique em **Test** (evento `{}` vazio é suficiente).
3. O **Producer** envia dados ao **`broker`** → o **Consumer-Realtime** é acionado.
4. Se as condições forem atendidas (ex.: `WIND_GUST_THRESHOLD = 0`), você **receberá e‑mail/SMS** via SNS.

---

## 6) Verificar e Depurar
- **SNS**: confira se as subscriptions estão **Confirmed**.
- **CloudWatch Logs** (na função **Consumer-Realtime** → **Monitor → View logs in CloudWatch**):
  - Veja a execução, o parsing do registro (Base64 → UTF‑8 → JSON), os valores extraídos e a publicação no SNS.
- **Kinesis Stream (`broker`) → Monitoring**: métricas como **Incoming Records**/**Put Records**.

> Se não aparecerem pontos nas métricas logo de cara, **aguarde alguns segundos e atualize**. Há latência de atualização do painel.

---

## 7) (Opcional) Agendar o Producer
Para automatizar a geração de eventos, crie um **EventBridge Scheduler** (CloudWatch) que chame o **`Producer`** a cada 1–3 minutos. (Veja o guia específico de schedule.)

---

### ✅ Resultado
A função **`Consumer-Realtime`** está criada, ligada ao **Kinesis `broker`**, lê os eventos, compara com os **limiares** e **dispara alertas via SNS** quando necessário.
