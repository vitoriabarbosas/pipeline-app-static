# Pipeline de Aplicação Estática

![Fluxo da Pipeline de Aplicação, onde é possível entender a configuração dada a estrutura de repositório do usuario, iniciando um trigger no GitHub Actions, seguindo para o deploy na conta AWS. Este Deploy, necessita de um Bucket S3 pré existente, ao qual, poderá ser utilizado com a arquitetura sugerida: Route53, Certificado ACM, CloudFront com origem neste Bucket que irá conter os arquivos. Para garantir segurança, o CloudFront pode-se integrar com WAF e OAC, para que tenha acesso exclusivo ao Bucket.](/docs/poc.jpg)

## Requisitos 
- Criação de Bucket S3 nas contas de teste e produção.
- Criação e configuração das IAM Roles para acesso nas Contas AWS a serem realizadas o deploy, dentro das secrets do repositório.

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
- [/app](/app/): Devem conter todos os arquivos necessários a serem deployados no bucket de origem
- [.config](.config): Devem conter as informações necessárias a serem realizadas o deploy

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

![Um pipeline de CI/CD (Continuous Integration/Continuous Deployment) geralmente inclui as seguintes etapas: Integração Contínua (CI) e Entrega Contínua (CD). Na etapa de CI, temos o Checkout de Código, Instalação de dependências e configuração do ambiente de build. Execução de Testes, Compilação do código e geração de artefatos de build. Na etapa de Entrega Contínua (CD), temos o Deploy em Ambiente de Teste, Upload do Artefato, Criação da TAG do repositório e lançamento da release no repositório. Seguido para a Aprovação, que é necessária antes de prosseguir para a produção. Se aprovado, temos o Deploy em Produção: Implantação dos artefatos de build no ambiente de produção. Em caso de falha, é feito o Envio de notificações em caso de falhas em qualquer estágio do pipeline.](/docs/diagrama.png)

[Clique aqui para acessar o arquivo do diagrama](/docs/diagramas.drawio)





