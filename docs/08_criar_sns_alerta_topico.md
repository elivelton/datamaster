
# Criar Tópico SNS na AWS para Alertas

Este guia mostra como criar um tópico SNS na AWS para enviar alertas via **e-mail** e **SMS**.

---

## ✅ Objetivo

O tópico SNS será usado pela função Lambda **Consumer** para enviar alertas quando determinados parâmetros forem atingidos.

---

## 🔹 Etapa 1: Acessar o Console SNS

1. Acesse o [Console da AWS](https://console.aws.amazon.com/)
2. No campo de busca, digite **SNS** e selecione **Simple Notification Service**

---

## 🔹 Etapa 2: Criar o Tópico

1. No menu lateral, clique em **Topics**
2. Clique em **Create topic**
3. Em **Type**, selecione: `Standard`
4. Em **Name**, digite: `SNS-Alerta`
5. Deixe o campo **Display name** em branco (opcional)
6. Mantenha as demais configurações padrão (criptografia, políticas, etc.)
7. Clique em **Create topic**

---

## 🔹 Etapa 3: Criar Subscription para E-mail

1. Dentro do tópico `SNS-Alerta`, clique em **Create subscription**
2. Em **Protocol**, selecione: `Email`
3. Em **Endpoint**, digite o seu e-mail (ex: `seuemail@exemplo.com`)
4. Clique em **Create subscription**
5. Acesse seu e-mail e clique no link **Confirm subscription**
6. Volte ao console da AWS e verifique que o status está como `Confirmed`

---

## 🔹 Etapa 4: Criar Subscription para SMS

1. Clique novamente em **Create subscription**
2. Em **Protocol**, selecione: `SMS`
3. Em **Endpoint**, insira seu número de celular no formato internacional:
   - Exemplo (Brasil): `+55DDXXXXXXXXX`
4. Clique em **Create subscription**
5. Se for a primeira vez usando esse número, você receberá um código via SMS
6. Digite o código para confirmar
7. Caso já tenha usado esse número antes, a confirmação será automática

---

## 🔹 Etapa 5: Guardar o ARN do Tópico

- O **ARN** (Amazon Resource Name) do tópico `SNS-Alerta` será necessário para configurar a função Lambda `Consumer`
- O ARN pode ser encontrado na página de detalhes do tópico

---

## ✅ Resultado

O tópico SNS `SNS-Alerta` estará pronto para receber mensagens e repassá-las por e-mail e SMS.
