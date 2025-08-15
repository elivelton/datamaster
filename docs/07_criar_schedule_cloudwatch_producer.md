
# Criar Agendamento no CloudWatch para Executar Lambda `Producer`

Este guia mostra como criar um agendamento no **CloudWatch EventBridge Scheduler** para executar automaticamente a função Lambda `Producer` em intervalos regulares.

---

## ✅ Objetivo

Automatizar a execução da função `Producer`, que coleta dados da API e envia para o Kinesis Data Stream (`broker`) periodicamente.

---

## 🔹 Etapa 1: Acessar o Console do CloudWatch

1. Acesse o [Console da AWS](https://console.aws.amazon.com/)
2. No campo de busca, digite **CloudWatch** e abra o serviço
3. No menu lateral, clique em **Rules** (dentro de **Events/EventBridge**)
4. Clique em **Create rule**

---

## 🔹 Etapa 2: Configurar o Agendamento

1. Em **Rule name**, digite: `Producer-Event`
2. Em **Event bus**, mantenha `default`
3. Em **Rule type**, selecione: `Schedule`
4. Clique em **Continue**

---

### Configuração do Horário

1. Em **Schedule pattern**, selecione:
   - **Cron-based schedule** ou **Rate-based schedule**
2. Exemplo de expressão cron para rodar a cada 1 minuto:
   ```
   cron(0/1 * * * ? *)
   ```
   > Para rodar a cada 3 minutos:
   ```
   cron(0/3 * * * ? *)
   ```
3. Em **Time zone**, selecione: `America/Sao_Paulo`
4. Em **Flexible time window**, selecione: `Off`
5. Clique em **Next**

---

## 🔹 Etapa 3: Definir o Alvo (Target)

1. Em **Target types**, selecione: `AWS service`
2. Em **Select a target**, escolha: `Lambda function`
3. Em **Function**, selecione: `Producer`
4. Clique em **Next**

---

## 🔹 Etapa 4: Configurações Adicionais

1. Em **Retry policy**, pode manter o padrão
2. Em **Encryption**, não é necessário alterar
3. Em **Permissions**, selecione:
   - `Create a new role for this schedule`
4. Clique em **Next**

---

## 🔹 Etapa 5: Revisar e Criar

1. Revise todas as configurações
2. Clique em **Create schedule**

---

## 🔍 Gerenciar o Agendamento

- Na tela do **EventBridge Scheduler**, seu agendamento aparecerá como **Enabled**
- Para pausar, clique no agendamento e selecione **Disable**
- Para retomar, clique em **Enable** novamente
- O agendamento executará automaticamente a função `Producer` no intervalo configurado

---

## ✅ Resultado

- O `Producer` executará automaticamente, coletando dados da API e enviando ao Kinesis.
- O `Consumer-Realtime` processará os dados e enviará alertas via SNS (e-mail/SMS) quando os critérios forem atendidos.

---

**Parabéns!** O agendamento foi configurado com sucesso.
