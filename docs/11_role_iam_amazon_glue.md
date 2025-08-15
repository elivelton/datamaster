# Passo a Passo: Criação da Role IAM para AWS Glue

## 1. Acessar o IAM
1. No Console da AWS, procure por **IAM** e abra o serviço.
2. No menu lateral, clique em **Roles**.
3. Clique no botão **Create role**.

## 2. Selecionar o tipo de entidade confiável (Trusted Entity)
1. Em **Trusted entity type**, selecione **AWS Service**.
2. Em **Use case**, procure e selecione **Glue**.
3. Clique em **Next**.

## 3. Adicionar permissões
Na etapa de permissões, adicione as seguintes **políticas gerenciadas**:

1. **AWSGlueServiceRole**  
   - Necessária para permitir que o Glue execute operações de ETL.
   
2. **AmazonS3FullAccess**  
   - Necessária para ler e gravar dados nos buckets S3.

3. **CloudWatchLogsFullAccess**  
   - Necessária para que o Glue registre logs de execução no CloudWatch.

Após selecionar as três políticas, clique em **Next**.

## 4. Configurar nome e revisar
1. Em **Role name**, digite:  
*(Seguindo a convenção definida no diagrama do projeto.)*

2. Opcionalmente, insira uma descrição.
3. Revise as permissões selecionadas:
- **AWSGlueServiceRole**
- **AmazonS3FullAccess**
- **CloudWatchLogsFullAccess**

4. Clique em **Create role**.

## 5. Resultado
- A role **ETL-Role** será criada e estará disponível para uso em jobs e crawlers do AWS Glue.
