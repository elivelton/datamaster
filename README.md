# Case Data Master
Repositorio para salvar os códigos e instruções para a capacitação do datamaster

## I - Objetivo do Case
Desenvolver um sistema de alertas climáticos que detecte eventos extremos em tempo real e envie notificações precisas aos usuários, além de armazenar os dados para futuras análises. O sistema quando atinge os paramêtros configurados envia um alerta por SMS para os clientes para que ele tome as medidaas necessárias.

## II - Arquitetura da Solução e Técnica
### Arquitetura da Solução
A entrada dos dados é feita via chamada de API, aonde com scripts python é feito o tratamento dos dados capturados e verificação dos sinais de alerta , além de tratar os dados para guardar no banco de dados e analisa-los posteriormente. A solução foi desenvolvida utilizado ferramentas e componentes da AWS cloud por ter maior integração e compatibilidade
<img width="950" height="647" alt="image" src="https://github.com/user-attachments/assets/182d6223-4266-4c48-92aa-f4349b1add0f" />

### Arquitetura Técnica 
Segue a arquitetura técnica da solução . A explicação de cada componente está no arquivo https://github.com/elivelton/datamaster/blob/main/Explicacao_Componentes_Ferramentas.pdf
<img width="950" height="1031" alt="image" src="https://github.com/user-attachments/assets/2a30ca4c-6155-4ebd-9ebc-a1b4d6d0e880" />

## III - Explicação sobre o case desenvolvido
**1. Extração dos dados**
Os daos são extraídos da api da plataforma Tommorrow IO https://docs.tomorrow.io/reference/welcome que contém dados metereológicos de Probrabilidade de Chuva, Velocidade do Vento e Intensidade da Chuva entre outros.

**2. Ingestão de dados**
Há duas forma de ingestão de dados no projeto . Uma por streaming para enviar os alertas para os usuários e outra via batch para guardar os dados no banco de dados dos alertas emitidos para análise posterior

**3. Armazenamento dos dados**
O armazenamento dos dados é feito primeiramente n em buckets divididos dados brutos (RAW) e dados tratados (Gold). E depois para visualizar essas informações utilizamos o banco de dados Athena

**4. Observabilidade**
Foi utilizado os monitores da plataforma nos componentes lambda é possivel observar os fluxos de dados, gerenciamento de possíveis erros e chamadas

**5. Segurança dos Dados**
Foi criada Roles com as permissões especificas para cada componente, garantindo que os dados sejam acessa apenas pelos usuários corretos

**6. Mascaramento de Dados**
Não houve necessidade de mascaramento dos dados, pois os dados não são sensíveis

**7. Arquitetura de dados**
A arquitetura utilizado foi a Lambda, uma parte em streaming para enviar os alertas e outra em batch para armazenar os resultados dos alertas

**8. Escalabilidade**
Por estar na plataforma AWS todo os componentes possuem auto-scale que possibilitam o auto-scale.

**9. Reprodutibilidade da arquitetura**
Para reproduzir a arquitetura é necessário seguir os arquivos de passo a passso de configuração que estão na pasta https://github.com/elivelton/datamaster/tree/main/docs
 

## IV - Melhorias e Considerações Finais
-Envio de dados pelo Whatsapp/Telegram
-Adicionar uma tabela com as informações de outras cidades 


