# Case Data Master
Repositorio para salvar os códigos e instruções para a capacitação do datamaster

## I - Objetivo do Case
Desenvolver um sistema de alertas climáticos que detecte eventos extremos em tempo real e envie notificações precisas aos usuários, além de armazenar os dados para futuras análises

## II - Arquitetura da Solução e Técnica
### Arquitetura da Solução
A entrada dos dados é feita via chamada de API, aonde com scripts python é feito o tratamento dos dados capturados e verificação d
<img width="1151" height="647" alt="image" src="https://github.com/user-attachments/assets/182d6223-4266-4c48-92aa-f4349b1add0f" />

### Arquitetura Técnica 
<img width="1555" height="1031" alt="image" src="https://github.com/user-attachments/assets/2a30ca4c-6155-4ebd-9ebc-a1b4d6d0e880" />

## III - Explicação sobre o case desenvolvido
**1. Extração dos dados**
Os daos são extraídos da api da plataforma Tommorrow IO https://docs.tomorrow.io/reference/welcome que contém dados metereológicos de Probrabilidade de Chuva, Velocidade do Vento e Intensidade da Chuva entre outros

**2. Ingestão de dados**
Há duas forma de ingestão de dados no projeto . Uma por streaming para enviar os alertas para os usuários e outra via batch para guardar os dados no banco de dados dos alertas emitidos para análise posterior

**3. Armazenamento dos dados**
O armazenamento dos dados é feito primeiramente n em buckets divididos dados brutos (RAW) e dados tratados (Gold). E depois para visualizar essas informações utilizamos o banco de dados Athena

**4. Observabilidade**
O

**5. Segurança dos Dados**

**6. Mascaramento de Dados**

**7. Arquitetura de dados**

**8. Escalabilidade**


 **9. Reprodutibilidade da arquitetura**
 Seguir o 
[dsasa](url)




## IV - Melhorias e Considerações Finais

Envio de dados pelo Whatsapp/Telegram

