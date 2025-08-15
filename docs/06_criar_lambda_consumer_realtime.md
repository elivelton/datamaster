
# Criar Função Lambda `Consumer-Realtime` na AWS

Este guia mostra como criar e configurar a função Lambda `Consumer-Realtime` que consome dados do Kinesis Data Stream e dispara alertas via SNS com base em limiares definidos por variáveis de ambiente.

---

## ✅ Objetivo

A função Lambda `Consumer-Realtime`:

- Lê mensagens do Kinesis Data Stream (broker)
- Avalia 4 parâmetros: probabilidade de chuva, velocidade do vento, rajadas de vento, intensidade de chuva
- Se qualquer valor estiver acima de um limiar, dispara um alerta via SNS (e-mail e SMS)

---

## 🔹 Etapa 1: Criar a Função Lambda

1. Acesse o [Console da AWS](https://console.aws.amazon.com/)
2. No campo de busca, digite **Lambda** e abra o serviço
3. Clique em **Create function**
4. Escolha **Author from scratch**
5. Configure os campos:
   - **Function name**: `Consumer-Realtime`
   - **Runtime**: `Python 3.12`
6. Em **Execution role**, selecione:
   - **Use an existing role**
   - Escolha: `Consumer-Realtime`

7. Clique em **Create function**

---

## 🔹 Etapa 2: Adicionar o Código

1. Apague o código de exemplo da aba `lambda_function.py`
2. Cole o código `consumer_realtime.py`
3. **Importante**: Substitua o valor da variável `sns_topic_arn` pelo ARN do seu tópico SNS real
4. Clique em **Deploy**

---

## 🔹 Etapa 3: Configurar Variáveis de Ambiente

1. Acesse a aba **Configuration > Environment variables**
2. Clique em **Edit** e **Add environment variable**
3. Adicione as seguintes variáveis (exemplo):

| Name                         | Value |
|-----------------------------|-------|
| PRECIPITATION_PROB_THRESHOLD | 70    |
| WIND_SPEED_THRESHOLD         | 10    |
| WIND_GUST_THRESHOLD          | 0     |
| RAIN_INTENSITY_THRESHOLD     | 5     |

> ⚠️ Use valores baixos (como 0) para facilitar o teste. Em produção, ajuste conforme necessário.

---

## 🔹 Etapa 4: Adicionar Gatilho do Kinesis

1. Acesse a aba **Configuration > Triggers**
2. Clique em **Add trigger**
3. Escolha o serviço: `Kinesis`
4. Em **Kinesis stream**, selecione: `broker`
5. Clique em **Add**

---

## 🔹 Etapa 5: Testar o Pipeline

1. Volte à função `Producer`
2. Clique em **Test** para executá-la manualmente
3. O Producer envia dados à stream `broker`
4. O `Consumer-Realtime` é acionado automaticamente
5. Se as condições forem atendidas, um **e-mail** e um **SMS** serão enviados

---

## 🔹 Etapa 6: Monitorar e Depurar

1. Acesse a aba **Monitor > View CloudWatch Logs**
2. Analise os logs para mensagens de erro ou confirmação de envio
3. Verifique se os alertas chegaram no e-mail e celular

---

## ✅ Pronto!

A função `Consumer-Realtime` está funcionando e processando dados em tempo real com base nos critérios definidos.

