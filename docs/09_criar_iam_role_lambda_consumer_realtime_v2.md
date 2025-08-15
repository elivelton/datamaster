
# Criar IAM Role `Consumer-Realtime` para Lambda na AWS

Este guia mostra como criar uma IAM Role chamada `Consumer-Realtime` com as permissões necessárias para a função Lambda que atuará como consumidor do Kinesis Data Stream e disparará alertas via SNS.

---

## ✅ Objetivo

A função `Consumer-Realtime` irá:

- Receber notificações do **Kinesis Data Stream** (broker)
- Avaliar dados recebidos
- Disparar mensagens no tópico **SNS** quando critérios forem atendidos

Para isso, precisaremos criar uma Role no IAM com permissões adequadas.

---

## 🔹 Etapa 1: Acessar o Console IAM

1. Acesse o [Console da AWS](https://console.aws.amazon.com/)
2. No campo de busca, digite **IAM** e abra o serviço
3. No menu lateral, clique em **Roles**
4. Clique em **Create role**

---

## 🔹 Etapa 2: Configurar Entidade Confiável (Trusted Entity)

1. Em **Trusted entity type**, selecione: `AWS service`
2. Em **Use case**, selecione ou digite: `Lambda`
3. Clique em **Next**

---

## 🔹 Etapa 3: Adicionar Permissões

1. Pesquise e selecione as políticas:
   - `AmazonSNSFullAccess`
   - `AWSLambdaKinesisExecutionRole`
2. Clique em **Next**

---

## 🔹 Etapa 4: Revisar e Nomear a Role

1. Em **Role name**, digite: `Consumer-Realtime`
2. (Opcional) Adicione uma descrição para facilitar a identificação futura
3. Revise as permissões atribuídas para confirmar que as duas políticas estão presentes
4. Clique em **Create role**

---

## ✅ Resultado

A Role `Consumer-Realtime` foi criada com sucesso e agora pode ser atribuída à função Lambda consumidora.

---

**Dica:** Esta role será usada no momento da criação da função Lambda `Consumer-Realtime` para permitir que ela leia dados do Kinesis e envie notificações via SNS.
