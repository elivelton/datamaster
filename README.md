# datamaster
Repositorio para salvar os códigos e instruções para a capacitação do datamaster

## ✅ Pré-requisitos

- Conta AWS ativa
- Permissões para acessar o serviço **Amazon Kinesis**
- AWS CLI configurado (caso use a linha de comando)


# 01 -Kinesis Data Stream com Nome `broker` na AWS

Criar o Kinesis Data Stream com o nome `broker` 

1. Acesse o console:  
   [https://console.aws.amazon.com/kinesis](https://console.aws.amazon.com/kinesis)

2. No menu lateral, selecione **Data Streams**.

3. Clique em **Create data stream**.

4. Preencha o campo:
   - **Data stream name**: `broker`

5. Em **Number of shards**, deixe o valor padrão: `1`

6. Clique em **Create data stream**

7. Aguarde a criação do stream. Você será redirecionado para a página de detalhes do stream `broker`.

## 02 IAM Role producer_iam

### 1. Acesse o serviço IAM

1. Faça login no [Console da AWS](https://console.aws.amazon.com/)
2. No campo de busca superior, digite **IAM** e selecione o serviço.
3. No menu à esquerda, clique em **Roles**.

### 2. Criar uma nova Role

1. Clique em **Create role** (canto superior direito).

### 3. Escolher entidade confiável (Trusted Entity)

1. Em **Trusted entity type**, selecione: `AWS service`
2. Em **Use case**, selecione ou busque por: `Lambda`
3. Clique em **Next**

### 4. Adicionar permissões

1. Pesquise e selecione a política:  
   - `AWSLambdaBasicExecutionRole`

2. Em seguida, pesquise e selecione a política:  
   - `AmazonKinesisFullAccess`

> ⚠️ Essas políticas concedem permissões básicas para o Lambda funcionar e acesso completo ao Kinesis. Em produção, considere limitar o acesso com políticas customizadas.

### 5. Definir nome e descrição

1. Em **Role name**, digite: `producer_iam`
2. A descrição será preenchida automaticamente, mas pode ser ajustada se necessário.
3. Clique em **Next**

### 6. Tags (opcional)

- Nenhuma tag é necessária neste exemplo. Clique em **Next**

### 7. Revisar e criar

- Verifique se as permissões estão corretas:
  - `AWSLambdaBasicExecutionRole`
  - `AmazonKinesisFullAccess`
- Clique em **Create role**

---

