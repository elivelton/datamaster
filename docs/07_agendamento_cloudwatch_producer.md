
# Agendar execução do Lambda **Producer** com CloudWatch (EventBridge Scheduler)

Este guia cria um **agendamento** para chamar a função **Lambda `Producer`** em intervalos regulares.

---

## ✅ Objetivo
Acionar periodicamente a função `Producer`, que consulta a API e envia dados ao **Kinesis Data Stream (`broker`)**.

---

## 📋 Pré‑requisitos
- Função **Lambda `Producer`** já criada e testada.
- Permissões para acessar **CloudWatch / EventBridge** e **Lambda** na sua conta AWS.

---

## 1) Abrir o EventBridge / CloudWatch
1. Acesse o **Console da AWS**.
2. Procure por **CloudWatch** (ou **Amazon EventBridge**).
3. No menu lateral, vá em **Events** → **Rules** (EventBridge).
4. Clique em **Create rule**.

---

## 2) Definir a regra (Rule)
1. **Rule name**: `Producer-Event`
2. **Description**: (opcional)
3. **Event bus**: `default`
4. **Rule type**: selecione **Schedule** (importante! não use *event pattern* para este caso).
5. Clique em **Continue**.

---

## 3) Configurar o agendamento (Schedule)
1. Em **EventBridge Scheduler**, mantenha o **Schedule group** padrão.
2. **Time zone**: `America/Sao_Paulo`.
3. Escolha um dos padrões:
   - **Rate-based schedule** (simples): a cada `1` ou `3` minutos.
   - **Cron-based schedule** (mais comum e flexível). Exemplos:
      - A cada **1 minuto**:
        ```
        cron(0/1 * * * ? *)
        ```
      - A cada **3 minutos**:
        ```
        cron(0/3 * * * ? *)
        ```
4. **Flexible time window**: `Off`.
5. Clique em **Next**.

> 💡 Dica: para testes, use 1 minuto; para uso contínuo, prefira 3 minutos (respeite limites da sua API).

---

## 4) Escolher o alvo (Target)
1. **Target type**: `AWS service`.
2. **Select a target**: `Lambda function`.
3. **Function**: selecione **`Producer`**.
4. (Opcional) **Payload**: deixe vazio, a função não requer parâmetros.
5. Clique em **Next**.

---

## 5) Ajustes finais
1. **After invocation**: deixe padrão (nenhuma ação adicional).
2. **Retry policy**: padrão.
3. **Encryption**: padrão.
4. **Permissions**: selecione **Create a new role for this schedule** (o EventBridge criará a role automaticamente).
5. Clique em **Next**.

---

## 6) Revisar e criar
1. Revise o resumo da regra.
2. Clique em **Create schedule**.
3. Aguarde a criação (pode levar alguns segundos).

---

## 7) Gerenciar, testar e verificar
- O schedule aparecerá como **Enabled** em **EventBridge → Schedules**.
- Para **pausar**, clique na regra e selecione **Disable** (não é necessário excluir).
- **Teste o fluxo**: aguarde 1–3 minutos e verifique se:
  - O `Producer` executou (aba **Monitor** da função).
  - O `Consumer-Realtime` foi acionado pelo Kinesis e, se os limiares forem atingidos, o **SNS** enviou **e‑mail/SMS**.
- **Logs**: veja **CloudWatch Logs** do `Producer`/`Consumer-Realtime` para confirmar execuções e depurar possíveis erros.

---

## ✅ Resultado
O **EventBridge Scheduler** está acionando o **Lambda `Producer`** no intervalo configurado. Você pode **habilitar/desabilitar** o agendamento conforme a necessidade do seu workflow.
