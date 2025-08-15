
# Criar IAM Role `Consumer-Batch` para AWS Lambda

Este guia cria uma **IAM Role** para a função Lambda que atuará como **Consumer em batch**: ela lerá do **Kinesis Data Stream** e gravará arquivos no **Amazon S3**, além de registrar logs no **CloudWatch**.

---

## ✅ Pré‑requisitos
- Acesso ao **Console da AWS** com permissão para **IAM**.
- (Opcional) Stream **Kinesis** e bucket **S3** já planejados/criados.

---

## 1) Abrir o IAM e iniciar a criação
1. No Console da AWS, procure por **IAM**.
2. No menu esquerdo, clique em **Roles**.
3. Clique em **Create role**.

---

## 2) Definir a entidade confiável (Trusted entity)
1. **Trusted entity type**: selecione **AWS service**.
2. **Use case**: selecione **Lambda** (ou digite *Lambda* no buscador e escolha).
3. Clique em **Next**.

---

## 3) Anexar permissões (Policies)
Marque as **três** políticas abaixo:
- `AWSLambdaBasicExecutionRole`  *(logs no CloudWatch)*
- `AmazonKinesisFullAccess`      *(acesso ao Kinesis para leitura)*
- `AmazonS3FullAccess`           *(gravação/leitura no S3)*

> 🔒 **Boas práticas**: em produção, prefira políticas **de menor privilégio** (por exemplo, apenas `kinesis:DescribeStream`, `kinesis:GetShardIterator`, `kinesis:GetRecords` no stream necessário; e `s3:PutObject`, `s3:GetObject`, `s3:ListBucket` apenas no bucket/prefixo específico).

Clique em **Next**.

---

## 4) Nomear e revisar
1. **Role name**: `Consumer-Batch`
2. (Opcional) **Description**: “Role para Lambda Consumer em batch (Kinesis → S3)”.
3. Revise se as políticas listadas são:
   - `AWSLambdaBasicExecutionRole`
   - `AmazonKinesisFullAccess`
   - `AmazonS3FullAccess`
4. Clique em **Create role**.

---

## ✅ Resultado
A role **`Consumer-Batch`** foi criada e está pronta para ser associada à sua **função Lambda batch consumer**.

**Próximos passos**: crie/atualize a função Lambda que consumirá o stream e persistirá os dados no S3 usando esta role.
