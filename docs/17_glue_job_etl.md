
# Criar **Job ETL** no AWS Glue (de `raw` → `gold` em Parquet)

Este guia cria um **Job do AWS Glue** (Spark/Python) que lê dados **JSON** catalogados na camada **raw**, **achata** a estrutura e grava em **Parquet** particionado por **ano/mês/dia** na camada **gold**.

---

## ✅ Objetivo
- Ler tabelas do **Glue Data Catalog** (criadas pelo *crawler* da camada **raw**).
- **Flatten** (achatamento) do JSON para colunas tabulares.
- Gravar em **S3** em `s3://<seu-bucket>/gold/<YYYY>/<MM>/<DD>/` no formato **Parquet**.

---

## 📋 Pré‑requisitos
- **Crawler** da camada **raw** executado e **database** (ex.: `raw_db`) criado no **Data Catalog**.
- **Bucket S3** com a pasta **`gold/`**.
- **IAM Role** para Glue (ex.: `ETL-Role`) com:
  - `AWSGlueServiceRole`
  - `AmazonS3FullAccess`
  - `CloudWatchLogsFullAccess`

> Em produção, substitua *FullAccess* por permissões de **menor privilégio**.

---

## 1) Abrir o Glue Studio e criar o Job
1. No Console da AWS, procure **AWS Glue**.
2. Acesse **ETL Jobs** (Glue Studio).
3. Clique em **Create** → escolha **Script editor** ( Author with a script editor ).
4. **Type**: `Spark` (linguagem `Python`).
5. Selecione **Start fresh** para começar com script em branco.

---

## 2) Preparar o script
1. Cole o **script ETL** do curso no editor.
2. **Atualize os parâmetros** no topo do script (conforme o código do curso):
   - **Database** do catálogo (ex.: `raw_db`).
   - **OUTPUT_PATH**: S3 da camada **gold**.  
     - No S3, abra **`gold/`** → **Copy S3 URI** e cole no parâmetro (ex.: `s3://meu-bucket/gold/`).
3. O script deve:
   - Inicializar **Spark/GlueContext**.
   - Listar **tabelas** do `raw_db`.
   - Ler os **JSON** (DataSource do catálogo).
   - **Flatten** (transformar `struct`/JSON em colunas).
   - Extrair **ano/mês/dia** para particionamento.
   - Gravar em **Parquet** no **OUTPUT_PATH** com partições `year/month/day`.

> Observação: O *flatten* é a parte que transforma os campos aninhados (`struct`) em colunas tabulares.

---

## 3) Definir detalhes do Job
1. Em **Job details**:
   - **Name**: `weather-job` (ou outro nome do seu padrão).
   - **IAM role**: selecione **`ETL-Role`** (criada anteriormente).
2. (Opcional) Ajuste recursos (workers, Glue version) conforme sua conta e limites.

Clique em **Save** para salvar o script e as configurações.

---

## 4) Executar e acompanhar
1. Clique em **Run** para iniciar o Job.
2. Em **Runs**, acompanhe o status ( `Running` → `Succeeded` ).
3. Consulte **CloudWatch Logs** em caso de erros.

---

## 5) Validar saída no S3
1. Abra **Amazon S3** → seu bucket → **`gold/`**.
2. Verifique a criação de pastas **`YYYY/MM/DD/`**.
3. Confirme a presença de arquivos **`.parquet`**.
4. Baixe um Parquet (opcional) e valide o schema com alguma ferramenta/local.

---

## 6) Agendamento e incremental (opcionais)
- **Schedule no Glue**: defina uma periodicidade (ex.: 1x/dia ou a cada 6h) para rodar o Job em *batch*.
- **Job bookmark**: habilite para que o Glue **não reprocese** dados já carregados.
  - Requer um campo de referência (geralmente **data/hora**) no script.

---

## ✅ Resultado
O **Job ETL do Glue** lê a camada **raw**, achata o JSON e grava a camada **gold** em **Parquet** particionado por data, pronto para consultas (ex.: via **Athena**, Redshift, etc.).

> **Próximo passo**: rode um **crawler na pasta `gold/`** para catalogar as tabelas e consultar com o **Athena**.
