
# Deploying this app inside of Azure Container Apps

## Deploy models

gpt-35-turbo
text-embedding-ada-002

Environment variables
```bash
  SEMANTICMEMORY__DATAINGESTION__VECTORDBTYPES_0=Qdrant
  SEMANTICMEMORY__RETRIEVAL__VECTORDBTYPE=Qdrant
  SEMANTICMEMORY__SERVICES__QDRANT__ENDPOINT=

  SEMANTICMEMORY__SERVICES__AZUREOPENAITEXT__DEPLOYMENT=
  SEMANTICMEMORY__SERVICES__AZUREOPENAITEXT__APIKEY=
  SEMANTICMEMORY__SERVICES__AZUREOPENAITEXT__ENDPOINT=

  SEMANTICMEMORY__SERVICES__AZUREOPENAIEMBEDDING__APIKEY=
  SEMANTICMEMORY__SERVICES__AZUREOPENAIEMBEDDING__ENDPOINT=
  SEMANTICMEMORY__SERVICES__AZUREOPENAIEMBEDDING__DEPLOYMENT=  

```

Disbale ssl

```json
  {
  //Server endpoints
  
  "Kestrel": {
    "Endpoints": {
      "Https": {
        "Url": "https://localhost:40443"
      }
    }
  }
  }
```

## WebApi is  deployed to Azure Container Apps

```bash
  
  # build
  docker build -t azureopenai.azurecr.io/azureopenaibot -f 'webapi/Dockerfile'

  # az login -n azureopenai
  # deploy
  docker push azureopenai.azurecr.io/azureopenaibot
```



## Qdrant Db is deployed to Azure Container Apps

http://qdrant-db

## webapp is deployed to static web app

```bash
  yarn install

  yarn add @azure/static-web-apps-cli -d

  npm build run

  # copy .env and swa-cli.config.json
  npx swa login
  
  # publish 
  npx swa publish
```

two files are needed to be not checked in
- `.env`
- `swa-cli.config.json`