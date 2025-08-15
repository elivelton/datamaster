
# Criar Tópico SNS `SNS-Alerta` na AWS

Este guia mostra como criar um tópico SNS chamado `SNS-Alerta` para envio de alertas via **e-mail** e **SMS**.

---

## ✅ Pré-requisitos

- Conta AWS com permissões para utilizar o serviço **SNS (Simple Notification Service)**
- Acesso a um e-mail válido
- Acesso a um número de telefone com DDI (ex: +55 para Brasil)

---

## 🔹 Etapa 1: Criar o Tópico SNS

1. Acesse o [Console da AWS](https://console.aws.amazon.com/)
2. No campo de busca, digite **SNS** e selecione o serviço **Simple Notification Service**
3. Clique em **Topics** no menu lateral
4. Clique em **Create topic**
5. Em **Type**, selecione `Standard`
6. Em **Name**, digite: `SNS-Alerta`
7. (Opcional) Em **Display name**, deixe em branco
8. Mantenha as configurações padrão (criptografia, políticas etc.)
9. Clique em **Create topic**

---

## 🔹 Etapa 2: Criar uma Subscription por E-mail

1. No painel do tópico `SNS-Alerta`, clique em **Create subscription**
2. Em **Protocol**, selecione: `Email`
3. Em **Endpoint**, digite o seu e-mail (ex: `seuemail@exemplo.com`)
4. Clique em **Create subscription**
5. Acesse seu e-mail e clique no link **Confirm subscription**
6. Atualize a página no console da AWS para verificar se o status mudou para `Confirmed`

---

## 🔹 Etapa 3: Criar uma Subscription por SMS

1. Clique novamente em **Create subscription**
2. Em **Protocol**, selecione: `SMS`
3. Em **Endpoint**, digite seu número de celular no formato internacional:
   - Exemplo (Brasil): `+5511999999999`
4. Clique em **Create subscription**
5. Se for a primeira vez utilizando esse número, será enviado um código SMS de confirmação
6. Digite o código para confirmar a inscrição
7. Se o número já tiver sido utilizado antes, a confirmação pode ser automática

---

## 🔍 Verificar Subscriptions

1. Volte para a aba do tópico `SNS-Alerta`
2. Verifique a coluna **Status**:
   - Deve aparecer `Confirmed` para e-mail e SMS
3. Agora o tópico está pronto para enviar alertas para os assinantes

---

✅ **Pronto!** O tópico `SNS-Alerta` foi criado e está configurado com subscriptions de e-mail e SMS.
