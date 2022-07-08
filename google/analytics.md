# Consumindo APIs do Google Analytics

Há vários jeitos de consumir as APIs do google analytics em suas
aplicações, utilizando chaves de API, IDs de cliente ou contas de
serviço.
Essa documentação engloba apenas a modalidade de conta de serviço, que
estabelece a comunicação do servidor da aplicação diretamente com o
servidor do google por meiodas bibliotecas - desenvolvidas e mantidas
pelo google - da linguagem Python. Também é possível fazer as
requisições por HTTP pleno.

## Pré-requisitos
No Google Cloud:
Em APIs e serviços, na aba APIs e serviços ativados, selecione e ative
as APIs que deseja consumir utilizando o botão "ATIVAR APIS E SERVIÇOS". 
Em credenciais, crie uma conta de serviço e uma chave privada para esta
conta. As requisições serão feitas pela conta de serviço e a autenticação
utilizará a chave privada criada, portanto é necessário **adicionar o
e-mail da conta de serviço como usuário no google analytics**.

## Consumindo com Biblioteca Python

### Criando as Credenciais

Utilize o método from_service_account_file(FILE, SCOPES) para criar o
objeto contendo as credenciais do usuário:

SCOPES = ['https://www.googleapis.com/auth/analytics.readonly']

SERVICE_ACCOUNT_FILE = 'path/to/client_secrets.json'

credentials = service_account.Credentials.from_service_account_file(SERVICE_ACCOUNT_FILE, scopes=SCOPES)

Cada API precisa de escopos específicos, que devem ser passados no
momento de criação das credenciais.

### Construindo o Objeto de Serviço

Crie um objeto de serviço analytics usando o método build:

analytics = build('analyticsreporting', 'v4', credentials=credentials)

O objeto possui um método .reports(), que gera um report a partir da
resposta de uma GET request, realizada com .batchGet(body). Exemplo
de execução:

analytics.reports().batchGet(
    body={'reportRequests': [
        {
            'viewId': VIEW_ID,
            'dateRanges': [{'startDate': '7daysAgo', 'endDate': 'today'}],
            'metrics': [{'expression': 'ga:sessions'}],
            'dimensions': [{'name': 'ga:country'}]
        }
    ]}).execute()

É possível realizar até 5 requests simultâneas utilizando um batchGet.

## Referências
- https://developers.google.com/analytics/devguides/reporting/core/v4/quickstart/service-py
- https://github.com/googleapis/google-api-python-client/blob/main/docs/README.md
- https://github.com/googleapis/google-api-python-client/blob/main/docs/oauth.md
- https://github.com/googleapis/google-api-python-client/blob/main/docs/start.md
- https://developers.google.com/identity/protocols/oauth2

### Documentações Específicas
- APIs Suportadas: https://github.com/googleapis/google-api-python-client/blob/main/docs/dyn/index.md
- https://googleapis.github.io/google-api-python-client/docs/dyn/analyticsreporting_v4.html
- https://googleapis.github.io/google-api-python-client/docs/dyn/analytics_v3.html
- https://analyticsreporting.googleapis.com/$discovery/rest?version=v4
