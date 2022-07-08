# Consuming APIs

## Escopo
Esse repositório é dedicado a condensar informações sobre o consumo de
APIs Google e Facebook.

### Google 

#### Pré-requisitos

Para consumir qualquer API google é necessário ter uma conta ativa no
google cloud com um projeto configurado.

**ATENÇÃO:** Ao criar uma chave privada um arquivo JSON será gerado, 
baixe o arquivo e guarde-o em um local seguro. Esse arquivo é a **única
cópia** da chave privada, e deve ser armazenado com cuidado.

É necessário instalar as bibliotecas de autenticação do google:

```
pip install --upgrade google-auth google-auth-oauthlib google-auth-httplib2
```

e a biblioteca de consumo de APIs:

```
pip install --upgrade google-api-python-client
```
