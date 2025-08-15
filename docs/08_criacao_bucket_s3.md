# Passo a Passo: Criação de Buckets no Amazon S3

Este guia descreve como criar um bucket no **Amazon S3** e configurar duas pastas para armazenar dados em diferentes estágios do pipeline.

---

## 1. Acessar o Amazon S3
1. No Console da AWS, pesquise por **S3** na barra de busca.
2. Clique no serviço **S3**.

---

## 2. Criar um Novo Bucket
1. Clique em **Create bucket**.
2. No campo **Bucket name**, insira um nome único globalmente (o nome não pode ser igual a outro bucket já existente na AWS).
   - Exemplo: `weather-rt` ou outro nome que não esteja em uso.
3. Mantenha todas as outras opções com os valores **padrão**.
4. Clique em **Create bucket**.

---

## 3. Criar Pastas no Bucket
1. Clique no bucket recém-criado.
2. Na raiz do bucket, clique em **Create folder** e crie a pasta **raw**.
   - Essa pasta armazenará os dados brutos recebidos, sem transformações.
3. Volte para a raiz do bucket.
4. Clique novamente em **Create folder** e crie a pasta **gold**.
   - Essa pasta armazenará os dados transformados e estruturados (por exemplo, em formato Parquet).

---

## 4. Estrutura Final do Bucket
Após esses passos, a estrutura do bucket ficará assim:

```
nome-do-bucket/
│
├── raw/
│   └── (dados brutos)
│
└── gold/
    └── (dados processados/estruturados)
```

---

✅ Agora você tem um bucket no S3 pronto para receber dados brutos e processados.
