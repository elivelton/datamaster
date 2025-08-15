
# Criar **Crawler** do AWS Glue para a camada **gold** (Parquet)

Este guia configura um **Glue Crawler** para varrer a pasta **`gold/`** do seu bucket S3, inferindo o esquema dos arquivos **Parquet** gerados pelo job de ETL e catalogando-os no **Glue Data Catalog**.

---

## ✅ Pré‑requisitos
- Job ETL do Glue já executado escrevendo em `s3://<seu-bucket>/gold/YYYY/MM/DD/...` (Parquet).
- Glue Crawler da camada **raw** já criado/executado (opcional, apenas contexto).

---

## 1) Abrir o AWS Glue e criar o Crawler
1. No Console da AWS, procure por **AWS Glue**.
2. No menu, clique em **Crawlers**.
3. Clique em **Create crawler**.
4. **Crawler name**: `gold-crawler` (ou outro nome do seu padrão).

> Observação: O Glue pode mostrar buckets internos gerados automaticamente (ex.: `aws-glue-assets-...`). **Ignore-os**. Você deve apontar para **o seu bucket** na pasta **`gold/`**.

---

## 2) Adicionar a fonte de dados (Data source)
1. Em **Data sources**, clique em **Add data source**.
2. **Source type**: selecione **Amazon S3**.
3. Em **Location** → **Browse**, navegue até **`s3://<seu-bucket>/gold/`** e selecione **a raiz da pasta `gold/`**.
4. Marque **Crawl all sub-folders** (fundamental para capturar as partições `YYYY/MM/DD`).
5. Clique em **Add** (para adicionar a fonte) e depois **Next**.

---

## 3) Permissões (IAM role do crawler)
1. Em **Choose an IAM role**, selecione **Create new IAM role** (ou crie uma específica para este crawler).
2. Aceite o nome sugerido ou defina um (ex.: `AWSGlueServiceRole-gold-crawler`).
3. Clique em **Next**.

---

## 4) Saída e agendamento
1. **Database** (Data Catalog): clique em **Add database** e crie **`weather`** (ou selecione o já existente).
2. Deixe **Table name prefix** em branco (opcional).
3. **Schedule**: selecione **On demand** (executaremos manualmente agora; você pode agendar depois).
4. Clique em **Next** → **Create crawler**.

---

## 5) Executar o crawler
1. Na lista de crawlers, selecione **`gold-crawler`**.
2. Clique em **Run**.
3. Aguarde até o **Status** mudar para **Ready / Succeeded** (pode levar alguns minutos).

---

## 6) Verificar o catálogo
1. Em **Databases**, abra **`weather`**.
2. Em **Tables**, verifique a(s) tabela(s) geradas para a camada **gold**.
3. Abra a tabela para conferir o **esquema inferido**:
   - Agora os dados devem estar **achatados** (flattened) em colunas tabulares, graças ao ETL (Parquet).
   - As partições `year/month/day` também devem aparecer.

---

## ✅ Resultado
- O **crawler da camada gold** está criado e o **Data Catalog** contém o **database `weather`** com as tabelas Parquet prontas para consulta.

> **Próximo passo**: consultar com o **Amazon Athena** (aponte para o database `weather` e rode consultas SQL sobre as tabelas catalogadas).
