
# Criar **Crawler** do AWS Glue para a camada **raw** (S3)

Este passo a passo cria um **Glue Crawler** que varre a pasta **`raw/`** do seu bucket S3, infere o esquema dos arquivos JSON e cadastra as tabelas no **Glue Data Catalog**.

---

## ✅ Pré‑requisitos
- Bucket S3 criado com a pasta **`raw/`** (ex.: `s3://meu-bucket/raw/AAAA/MM/DD/...`).
- (Opcional) Role IAM de ETL já criada para jobs do Glue. **Para o crawler**, criaremos uma role automática específica.

---

## 1) Abrir o AWS Glue e criar o Crawler
1. No Console da AWS, procure por **AWS Glue**.
2. No menu do Glue, acesse **Crawlers**.
3. Clique em **Create crawler**.
4. **Crawler name**: `raw-crawler` (ou um nome equivalente).

---

## 2) Configurar a fonte de dados (Data source)
1. Em **Data sources**, escolha **Add data source**.
2. **Source type**: selecione **Amazon S3**.
3. Em **Location**, clique em **Browse** e selecione **seu bucket** e a **pasta `raw/`**.
4. Marque **Crawl all sub-folders** *(importante para varrer `raw/AAAA/MM/DD/...`)*.
5. Clique em **Add** para adicionar a fonte. Depois **Next**.

---

## 3) Permissões (IAM role do crawler)
1. Na etapa **Choose an IAM role**, selecione **Create new IAM role**.
2. Aceite o nome sugerido (ou forneça um nome, ex.: `AWSGlueServiceRole-raw-crawler`).
   - O Glue criará e anexará as permissões necessárias automaticamente.
3. Clique em **Next**.

---

## 4) Banco de dados do Data Catalog
1. Em **Set output and scheduling**, na seção **Data target** → **Database**, clique em **Add database** (se ainda não existir).
2. **Database name**: `raw_db` (exemplo).
3. Salve o database e selecione-o na lista.
4. (Opcional) **Table name prefix**: deixe em branco.
5. **Schedule**: escolha **On demand** (executar manualmente quando quisermos).
6. Clique em **Next** e depois em **Create crawler**.

---

## 5) Executar o crawler
1. De volta à lista de crawlers, selecione **`raw-crawler`**.
2. Clique em **Run**.
3. Aguarde até o **Status** mudar para **Ready / Succeeded** (pode levar alguns minutos).

---

## 6) Verificar o catálogo
1. No menu do Glue, acesse **Databases** e confirme o **`raw_db`**.
2. Acesse **Tables** e verifique a(s) tabela(s) criada(s) para a pasta **`raw/`**.
3. Abra a tabela e confira o **esquema inferido**:
   - Colunas de **particionamento**: geralmente `year`, `month`, `day` *(strings)*.
   - Campos JSON aninhados podem aparecer como **`struct`** (por ex.: `data`, `location` com latitude/longitude).
   - Isso reflete a estrutura dos arquivos brutos.

> Observação: O esquema pode mostrar campos aninhados (JSON/`struct`). A **normalização/achatamento** para um formato tabular (ex.: **Parquet** na camada **gold**) será feita em **jobs de ETL do Glue**.

---

## ✅ Resultado
- O **Glue Crawler** para a camada **raw** está criado e o **Data Catalog** contém o **database `raw_db`** e tabela(s) correspondentes ao conteúdo de `raw/` no S3.
- Agora você pode criar um **Job do Glue** para transformar os dados brutos em dados **estruturados (Parquet)** na camada **gold**.
