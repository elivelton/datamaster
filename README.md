# datamaster
Repositorio para salvar os códigos e instruções para a capacitação do datamaster

# Guia Rápido: Criar Conta AWS, Usuário de Serviço e Configurar AWS CLI

## 1. Criar uma Conta na AWS

1. Acesse: [https://aws.amazon.com/pt/free](https://aws.amazon.com/pt/free)
2. Clique em **Criar uma conta da AWS**.
3. Insira seu e-mail, nome de usuário e senha.
4. Escolha o tipo de conta (Pessoal ou Empresarial).
5. Adicione as informações de pagamento (necessário mesmo para o plano gratuito).
6. Verifique sua identidade (via SMS).
7. Escolha um plano (pode selecionar o **Plano Básico Gratuito**).

---

## 2. Criar um Usuário de Serviço com Access Key e Secret Key

> ⚠️ **Importante**: Nunca use o usuário root para automações.

1. Acesse o [Console da AWS](https://console.aws.amazon.com/)
2. Vá até o serviço **IAM** (Gerenciamento de Identidade e Acesso).
3. No menu lateral, clique em **Usuários** > **Adicionar usuários**.
4. Nomeie o usuário (ex: `meu-usuario-servico`).
5. Selecione **Acesso programático**.
6. Clique em **Permissões**:
   - Escolha **Anexar políticas diretamente**.
   - Para testes, selecione **AdministratorAccess** (ou crie uma política personalizada).
7. Avance e crie o usuário.
8. Copie e salve:
   - **Access Key ID**
   - **Secret Access Key**

> 🔐 **Nunca compartilhe essas chaves**. Trate como senhas.

---

## 3. Baixar e Configurar o AWS CLI

### 3.1 Instalar AWS CLI

#### Windows

- Baixe o instalador:  
  [https://aws.amazon.com/cli/](https://aws.amazon.com/cli/)
- Execute o `.msi` e siga os passos da instalação.

#### Linux / macOS

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install


