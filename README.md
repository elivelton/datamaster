# Case Data Master
Repositorio para salvar os códigos e instruções para a capacitação do datamaster

## I - Objetivo do Case
Desenvolver um sistema de alertas climáticos que detecte eventos extremos em tempo real e envie notificações precisas aos usuários .

## II - Arquitetura da Solução e Técnica
### Arquitetura da Solução
<img width="1151" height="647" alt="image" src="https://github.com/user-attachments/assets/182d6223-4266-4c48-92aa-f4349b1add0f" />



### Arquitetura Técnica 
<img width="1555" height="1031" alt="image" src="https://github.com/user-attachments/assets/2a30ca4c-6155-4ebd-9ebc-a1b4d6d0e880" />





## III - Explicação sobre o case desenvolvido
**1. Extração dos dados**
Os são extraidos da api da plataforma Tommorrow IO que contém dados metereológicos de diversas cidades do mundo com informações entre outras Velocidade do Vento, Probrabilidade de Chuva, Umidade do Ar etc.

**2. Ingestão de dados**
Há duas forma de ingestão de dados no projeto . Uma por streaming para enviar os alertas para os usuários e outra via batch para guardar os dados dos alertas emitidos para análise posterior

**3. Armazenamento dos dados**
Há duas forma de ingestão de dados no projeto . Uma por streaming para enviar os alertas para os usuários e outra via batch para guardar os dados dos alertas emitidos para análise posterior





## IV - Melhorias e Considerações Finais

Envio de dados pelo Whatsapp/Telegram

