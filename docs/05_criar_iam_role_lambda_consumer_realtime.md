
# Criar IAM Role `Consumer-Realtime` para Lambda na AWS

Este guia mostra como criar uma IAM Role chamada `Consumer-Realtime` com permissões necessárias para uma função Lambda que consome dados e envia alertas via SNS.

---

## ✅ Pré-requisitos

- Conta AWS com permissões para acessar o serviço **IAM**
- Entendimento básico sobre funções Lambda e SNS
- A função Lambda que usará essa role deve estar planejada ou criada

---

## 🔹 Etapa 1: Acessar o Console do IAM

1. Acesse o [Console da AWS](https://console.aws.amazon.com/)
2. No campo de busca, digite **IAM** e selecione o serviço
3. No menu à esquerda, clique em **Roles**
4. Clique em **Create role**

---

## 🔹 Etapa 2: Configurar a entidade confiável (Trusted Entity)

1. Em **Trusted entity type**, selecione: `AWS service`
2. Em **Use case**, selecione ou digite: `Lambda`
3. Clique em **Next**

---

## 🔹 Etapa 3: Adicionar permissões

1. Pesquise e selecione as duas políticas abaixo:
   - `AmazonSNSFullAccess`
   - `AWSLambdaKinesisExecutionRole`
2. Clique em **Next**

---

## 🔹 Etapa 4: Revisar e nomear a Role

1. Em **Role name**, digite: `Consumer-Realtime`
2. (Opcional) Adicione uma descrição para facilitar a identificação futura
3. Verifique se as duas permissões foram atribuídas corretamente
4. Clique em **Create role**

---

## ✅ Resultado

A role `Consumer-Realtime` foi criada com sucesso e agora pode ser atribuída a uma função Lambda que consome dados de um stream e publica alertas via SNS.
