
# Criar Função Lambda `Producer` na AWS

Este guia descreve como criar uma função Lambda chamada `Producer` que consulta a API da Tomorrow.io e envia os dados para um Kinesis Data Stream chamado `broker`.

---

## ✅ Pré-requisitos

- Conta AWS com permissões para criar funções Lambda
- IAM Role `Lambda-Producer` já criada
- Arquivo `.zip` com o código da função Lambda disponível
- Chave da API Tomorrow.io válida

---

## 🔹 Passo a Passo: Criar a Função Lambda

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
3. Em seguida clique em **Upload** e selecione o arquivo `lambda_function_producer.zip` da função
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

---

✅ Pronto! A função `Producer` está criada, configurada e enviando dados corretamente para o Kinesis.
