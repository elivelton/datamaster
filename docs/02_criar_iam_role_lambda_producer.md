
# Criar Role no IAM com Nome `Lambda-Producer`

Este guia mostra o passo a passo para criar uma **IAM Role** chamada `Lambda-Producer` com permissões básicas para execução de funções Lambda e acesso total ao Amazon Kinesis.

---

## ✅ Pré-requisitos

- Conta AWS ativa
- Permissões de administrador ou políticas suficientes para criar roles no IAM
- Acesso ao Console da AWS

---

## 🔹 Passo a Passo: Criar a Role

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

1. Em **Role name**, digite: `Lambda-Producer`
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

## ✅ Resultado

A Role `Lambda-Producer` foi criada com sucesso. Agora ela pode ser atribuída a funções Lambda que precisam enviar dados para o Amazon Kinesis.

