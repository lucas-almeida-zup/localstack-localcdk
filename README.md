# Instalação localstack

## Indice
- [Configuração/verificação requisitos](#Configuração/verificação-requisitos)
- [LocalStack](#LocalStack)
- [CDK Local](#CDK-Local)
- [Referências](#Referencias)

## Configuração/verificação requisitos
### Python/pip
[Verificar instalação com Homebrew](https://docs.brew.sh/Homebrew-and-Python#python-3x)  

### Docker
Seguir passos de instalação em: [Get Docker](https://docs.docker.com/get-docker/)

## LocalStack
### Intalação
```
pip install localstack
```

### Iniciar localstack
```
localstack start
```

### Executar diretamente com Docker
```
docker run --rm -it -p 4566:4566 -p 4571:4571 localstack/localstack
```

### Utilizar awslocal
Com `awslocal` facilita o uso do LocalStack no CLI  
> Ex.:  
> Comando: `aws --endpoint-url=http://localhost:4566 kinesis list-streams`  
> Pode ser resumido para: `awslocal kinesis list-streams`

Executando o comando abaixo habilita o uso de `awslocal` para comunicação com `localstack`
```
pip install awscli-local
```

### Variáveis de ambiente
Utilizar variáveis de ambiente AWS com valor `test`

> AWS_ACCESS_KEY_ID=test AWS_SECRET_ACCESS_KEY=test

```
export AWS_ACCESS_KEY_ID=test
export AWS_SECRET_ACCESS_KEY=test
```

### Verificação status LocalStack
Comando para verificar se o `localstack` esta executando normalmente:

```
curl http://localhost:4566
```

O comando deve retornar o status:

```
# {"status": "running"}
```

## CDK Local
CDK Local é configurado diretamente no projeto (typescript) com a instalação da dependência de *desenvolvimento* `aws-cdk-local`  dessa forma é possível fazer deploy da stack no localstack  

```
# Comando que adiciona a dependência no projeto 
npm i --save-dev aws-cdk-local
```

Abrir `package.json` do projeto para adição de script `cdklocal`  
Nesse exemplo cria o comando `local` para execução por meio do `npm run <script>`

```
"scripts": {
    "local": "cdklocal"
},
```

Testar comando executando:

```
npm run local synth
```

## Referências
- Repositório/informações [localstack](https://github.com/localstack/localstack)
- Repositório/informações [awscli-local](https://github.com/localstack/awscli-local)
- [Utilizando cdk com localstack e cdklocal](https://blog.dennisokeeffe.com/blog/2021-08-07-using-the-aws-cdk-with-localstack-and-aws-cdk-local)
