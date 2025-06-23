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

## 03 Criar lambda producer

### 1. Acessar o serviço Lambda

1. Faça login no [Console da AWS](https://console.aws.amazon.com/)
2. No campo de busca, digite `Lambda` e abra o serviço.
3. Clique em **Create function**.

### 2. Configurar a função

1. Selecione **Author from scratch**.
2. Em **Function name**, digite: `Producer`
3. Em **Runtime**, selecione: `Python 3.12`  
   > (ou a versão mais próxima disponível do seu ambiente)
4. Em **Execution role**, clique em **Change default execution role**
5. Selecione **Use an existing role**
6. Escolha a role `Lambda-Producer`
7. Clique em **Create function**

---

### 3. Fazer upload do código da função

1. Na página da função criada, vá até a seção **Code source**
2. Clique em **Upload from** > **.zip file**
3. Em seguida clique em **Upload** e selecione o arquivo `.zip` da função
4. Clique em **Save**

---

### 4. Adicionar variável de ambiente

1. Vá até a aba **Configuration**
2. Clique em **Environment variables**
3. Clique em **Edit**
4. Adicione a variável:
   - **Key**: `TOMORROW_API_KEY` *(deve ser exatamente como o código espera)*
   - **Value**: sua chave da API Tomorrow.io
5. Clique em **Save**

---

### 5. Testar a função

1. Clique em **Test**
2. Crie um novo evento:
   - **Event name**: `teste`
   - **Event JSON**: deixe como `{}` (vazio)
3. Clique em **Save**
4. Clique em **Test** para executar a função

Se tudo estiver correto:
- O log de execução será exibido em verde
- A resposta incluirá `statusCode: 200`

---

## 🔍 Verificar envio de dados para o Kinesis

1. Vá até o serviço **Kinesis** na AWS
2. Clique no stream `broker`
3. Vá até a aba **Monitoring**
4. Observe os gráficos:
   - **Incoming data**
   - **Put records**

Se os pontos estiverem aparecendo nos gráficos, os dados estão sendo recebidos com sucesso.

> Caso não apareçam de imediato, aguarde alguns segundos e atualize a página.

