# Pipeline de Aplicação Estática

![Fluxo da Pipeline de Aplicação, onde é possível entender a configuração dada a estrutura de repositório do usuario, iniciando um trigger no GitHub Actions, seguindo para o deploy na conta AWS. Este Deploy, necessita de um Bucket S3 pré existente, ao qual, poderá ser utilizado com a arquitetura sugerida: Route53, Certificado ACM, CloudFront com origem neste Bucket que irá conter os arquivos. Para garantir segurança, o CloudFront pode-se integrar com WAF e OAC, para que tenha acesso exclusivo ao Bucket.](/docs/desafio.jpg)

## Requisitos 
- Criação de Bucket S3 nas contas de teste e produção
- Acesso nas Contas AWS a serem realizadas o deploy 

## Estrutura do repositório a ser utilizado pela pipeline

```plaintext
nome-do-repo/
├── .github/
│   └── workflows/
│       └── develop.yml
│       └── prod.yml
├── app/
│   └── index.html
│   └── package.json
│   ├── tests/
│       └── App.test.js
├── .config
```

Seu repositório deve conter os seguintes arquivos:
- [.github](/.github): Contém todos os arquivos e estrutura dos workflows a serem seguidos pela pipeline
- [/app](/exemplo/app/): Devem conter todos os arquivos necessários a serem deployados no bucket de origem
- [.config](/exemplo/.config): Devem conter as informações necessárias a serem realizadas o deploy

## Entendendo o arquivo de Config
Este arquivo, é o arquivo que deve conter todas as informações do deploy. Sendo assim, você **precisa** informar as seguintes variáveis:

```txt
BUCKET_ORIGIN_TEST_NAME=nome-do-bucket-de-teste
BUCKET_ORIGIN_PROD_NAME=nome-do-bucket-de-prod
AWS_ACCOUNT_TEST_ID=123456789012
AWS_ACCOUNT_PROD_ID=120987654321
USER_EMAIL=seuemail@email.com.br
NODE_VERSION=14
```

**Atenção: Não é permitida a customização das variáveis acima, por serem variáveis esperadas pela pipeline**

## Diagrama das etapas da Pipeline 

![](/docs/diagrama.drawio.png)

[Clique aqui para acessar o arquivo do diagrama](/docs/diagrama.drawio)





