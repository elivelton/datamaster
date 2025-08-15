
# Consultas no **Amazon Athena** (camada *gold*) – Passo a passo

Este guia mostra como **configurar o Athena** e **executar consultas SQL** sobre a tabela catalogada da camada **gold** (arquivos **Parquet** gerados pelo job do Glue).

---

## ✅ Pré‑requisitos
- **Glue Crawler (gold)** executado e **database** criado (ex.: `weather`) com tabela (ex.: `gold`).
- Dados **Parquet** em `s3://<seu-bucket>/gold/YYYY/MM/DD/...`.
- Permissões para usar **Athena**, **Glue Data Catalog** e **S3**.

---

## 1) Abrir o Athena
1. No Console da AWS, procure por **Amazon Athena** e abra o serviço.
2. (Opcional) Confirme o **Workgroup** (`primary`/`primary workgroup`) para o ambiente atual.

---

## 2) Configurar o local de resultados (obrigatório)
O Athena **exige** um local S3 para armazenar resultados e metadados de consultas.

1. Clique em **Settings** (engrenagem) → **Manage**.
2. Em **Query result location**, selecione um caminho **S3**.
   - Se ainda não tiver um bucket, crie em **S3** (ex.: `athena-queries-2025-<sufixo>`) e opcionalmente um prefixo `results/`.
   - Exemplo de valor: `s3://athena-queries-2025-abc/results/`
3. **Save** para aplicar.

> Se você tentar executar uma query sem esse caminho S3 configurado, o Athena exibirá um erro solicitando o **Query result location**.

---

## 3) Selecionar o *database* e a tabela
1. No painel esquerdo (catálogo), selecione o **Database** criado pelo crawler da **gold** (ex.: `weather`).
2. Expanda **Tables** e identifique sua tabela (ex.: `gold`).
3. (Opcional) Use **Preview table** para ver um SELECT automático gerado.

---

## 4) Primeira consulta
No editor do Athena, rode uma consulta simples (ajuste nomes de colunas conforme seu esquema):

```sql
SELECT time, cloud_base, cloud
FROM gold
LIMIT 10;
```

> Use o navegador de **tabelas/colunas** à esquerda para conferir os **nomes exatos** das colunas criadas pelo Glue (após o *flatten* no ETL).

---

## 5) Filtrar por partições (ano/mês/dia)
Como os Parquet foram gravados particionados, filtre por **partições** para reduzir custo e acelerar consultas:

```sql
SELECT *
FROM gold
WHERE year = '2024' AND month = '08' AND day = '06'
LIMIT 50;
```

---

## 6) Exemplos úteis
**Contagem total**  
```sql
SELECT COUNT(*) AS total_registros
FROM gold;
```

**Estatísticas de vento no dia**  
```sql
SELECT
  AVG(wind_speed)   AS avg_wind_speed,
  MAX(wind_gust)    AS max_wind_gust
FROM gold
WHERE year = '2024' AND month = '08' AND day = '06';
```

**Mais recentes por tempo (desc)**  
```sql
SELECT time, precipitation_probability, rain_intensity, wind_speed, wind_gust
FROM gold
ORDER BY time DESC
LIMIT 20;
```

> Dica: ajuste nomes de colunas (`precipitation_probability`, `rain_intensity`, etc.) conforme o **schema** inferido pelo crawler da **gold**.

---

## 7) Solução de problemas
- **Erro “You must specify a query result location to run this query.”**  
  → Configure o S3 em **Settings → Manage** e salve.

- **Não vejo partições novas**  
  → Re‑execute o **crawler da gold** para atualizar o catálogo **ou** rode:  
  ```sql
  MSCK REPAIR TABLE gold;
  ```

- **Permissão negada (AccessDenied)**  
  → Garanta que o **workgroup** do Athena e seu usuário/role tenham acesso ao **S3** dos resultados e ao **S3** de dados; o Glue Data Catalog também deve estar acessível.

- **Custo**  
  → O Athena cobra por **dados lidos**. Filtre por **partições** e mantenha **Parquet**/compressão para reduzir custo.

---

## ✅ Resultado
O **Athena** está configurado e você consegue **consultar** a tabela da camada **gold** (Parquet), explorando e analisando os dados por SQL.
