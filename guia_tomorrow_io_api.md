
# Guia: Criar Conta e Gerar Chave de API no Tomorrow.io

## 1. Criar uma Conta no Tomorrow.io

1. Acesse: [https://app.tomorrow.io/signup](https://app.tomorrow.io/signup)
2. Escolha uma das opções:
   - Cadastre-se com **Google**, **Microsoft** ou **GitHub**  
   - Ou clique em **Sign up with Email**
3. Preencha os dados:
   - Nome completo
   - E-mail
   - Senha
4. Clique em **Create Account** ou equivalente.
5. Verifique seu e-mail (se solicitado) para ativar a conta.

---

## 2. Gerar uma Chave de API (API Key)

1. Após o login, vá para o painel principal (dashboard).
2. No menu lateral esquerdo, clique em **API Keys** ou acesse diretamente:  
   [https://app.tomorrow.io/development/keys](https://app.tomorrow.io/development/keys)
3. Clique em **+ Create API Key**.
4. Dê um nome à chave, como `meu-projeto-clima`.
5. Clique em **Create**.
6. Copie a **API Key** gerada.

> 🔐 **Atenção**: Guarde essa chave em local seguro. Evite expor em repositórios públicos.

---

## 3. Usar a API Key

Você pode utilizar a chave com as APIs da Tomorrow.io, por exemplo:

```bash
curl "https://api.tomorrow.io/v4/weather/forecast?location=São%20Paulo&apikey=SUA_API_KEY"
```

> 📚 Documentação oficial: [https://docs.tomorrow.io](https://docs.tomorrow.io)

---

✅ Pronto! Você está apto a usar os dados climáticos do Tomorrow.io em seus projetos.
