# 1. Pré-requisitos

## 1.1 Instalação NodeJS e NPM

Para esse projeto precisaremos do NodeJS e do NPM, caso não conheça essas tecnologias, deixarei linkado aqui alguns sites para maiores informações

- [Sobre o NodeJS](https://nodejs.org/pt-br/about/)
- [Sobre o NPM](https://docs.npmjs.com/about-npm)

### 1.1.1 Windows/MacOS
Instale o NodeJS + NPM, acessese [https://nodejs.org/en/download/]() e siga as instruções de instalação.

### 1.1.2 Linux/Windows/MacOs via Package Manager
caso esteja esteja fazendo a instalação em uma distribuição linux acesse [https://nodejs.org/en/download/package-manager/]() e siga as instruções para sua distribuição, certifique-se de ter instalado o **NPM** também.

### 1.2.3 Verificação de instalação

Para verificar se o NodeJS esta instalado corretamente abra seu terminal e digite o seguinte comando:

```
node --version
```

Se tudo ocorreu bem na instalação isso deve apresentar a versão do NodeJS instalado atualmente.

Para verificar se o **NPM** também está instalado corretamente execute o seguinte comando:

``` 
npm --version
```

assim como no caso do comando anterior apresentava a versão do NodeJS instalado, este deve mostrar a versão do NPM instalado no momento, caso a instalação tenha sido bem sucedida.

## 1.2 Preparando a estrutura de pastas e pacotes

Crie uma pasta com o nome que preferir, o nome escolhido para este tutorial foi `tuto_crud` (evite a utilização de caracteres especiais), dentro desta pasta criaremos uma subpasta chamada `src`, abreviação de _source_, é aqui onde colocaremos todos os fontes de nosso projeto, também criaremos uma subpasta chamada `dis` abreviação para _distributable_ é nesta pasta onde nossos arquivos prontos para serem distribuidos ficaram.

O próximo passo é criar o arquivo `package.json`, este arquivo é responsável por manter informações importantes sobre o projeto, como comandos para empacotamento e quais pacotes de terceiro serão utilizados etc. para criar este arquivo iremos utilizar o **NPM**, abra seu terminal e navegue até a pasta do projeto e então digite o seguinte comando:

```
npm init -y
```

Este comando criará um arquivo chamado `package.json` sem fazer nenhuma pergunta ao usuário, para ter a possíbilidade de criar o arquivo já com dados customizados, execute o mesmo comando porém sem o parâmetro `-y`.

O arquivo gerado terá uma estrutura semelhante ao listado aqui:

```json
{
  "name": "tuto_crud",
  "version": "1.0.0",
  "description": "tutorial crud",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "Daniel de A. Varela",
  "license": "ISC"
}
```

### 1.2.1 Pacote para desenvolvimento: Parcel

Neste projeto utilizaremos o empacotador `Parcel`, ele será responsável por criar os arquivos para distribuição do projeto como por exemplo compilando arquivos TypeScript e SCSS para Javascript e CSS para que possam serem interpretados pelo browser, como este pacote será utilizado somente no momento do desenvolvimento, instalaremos o pacote da seguinte maneira, pelo terminal na pasta raiz do executaaresmos o seguinte comando:

```
npm install parcel --save-dev
```

Todos os comandos de instalação de pacotes irá demorar um pouco, pois o NPM irá baixar estes pacotes dos servidores oficiais, após a primeira instalação de qualquer pacote uma nova pasta será criada com o nome `node_modules` onde ficaram todas as bibliotecas que utilizaremos no desenvolvimento da aplicação, o arquivo `package.json` irá ser atualizado, adicionando o trecho onde temos a lista de `dependencias de desenvolvimento`, ou seja os pacotes que serão utilizados somente durante o desenvolvimento:

```json
...
"devDependencies": {
    "parcel": "^1.12.4"
}
...
```

### 1.2.2 Pacotes Express e SQLite

Outros dois pacotes que utilizaremos é o `sqlite` e o `express`, um responsável ao acessar e escrever em nosso banco de dados e outro responsável por manipular o acesso via HTTP ao nosso projeto, para instalar estes dois pacotes de uma única vez, utilizaremos o seguinte comando:

```
npm install sqlite express
```

Note que desta vez não utilizamos o parâmetro `--save-dev`, pois estes pacotes serão necessários para o funcionamento da aplicação após a versão distribuição.

Como a aplicação depende desses pacotes para funcionar mesmo depois de empacotada, o arquivo `package.json` irá ser atualizado com a seguinte sessão:

```json
...
"dependencies": {
    "express": "^4.17.1",
    "sqlite": "^4.0.15"
}
...
```

### 1.2.3 Como recriar a pasta node_module

A pasta `node_modules` pode ser excluida e recriada, pois o arquivo `package.json` possui toda a lista de pacotes necessários para o funcionamento e desenvolvimento da aplicação, o comando para recriar a pasta `node_module` é o seguinte:

```
npm install
```

este comando ira baixar novamente todos os modulos listados no arquivo `package.json`.

### 1.2.4 Arquivos de projeto: HTML, SCSS e TS

Em nosso proejto  utilizaremos HTML, SCSS e TS, então na pasra `src` criaremos os seguintes arquivos com os seguintes conteúdos:

index.html
```html
<!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>CRUD</title>
  </head>
  
  <body>
    <script src="./main.ts"></script>
  </body>
</html>
```

main.ts
```ts
import "./main.scss";

alert("Hello World!");
```

main.scss
```scss
body {
    background: lightgreen;
}
```

### 1.2.5 Estrutura final das pastas

A estrutura final das pastas devem ficar da seguinte maneira:

- tuto_crud
  - node_module
    - ...
  - dist
  - src
    - index.html
    - main.scss
    - main.ts
  - package.json


## 1.3 Preparando aplicação para execução

Para que possamos testar nosso projeto adicionaremos ao arquivo `package.json` o comando para depuação e teste de nossa aplicação, então adicione dentro da chave `scripts` o seguinte comando 

```json
...
  "scripts": {
    "debug": "parcel src/index.html",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
...
```

O arquivo `package.json` final ficará parecido com o seguinte:

```json
{
  "name": "tuto_crud",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "debug": "parcel src/index.html",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "parcel": "^1.12.4",
    "typescript": "^4.0.5"
  },
  "dependencies": {
    "express": "^4.17.1",
    "sqlite": "^4.0.15"
  }
}
```

## 1.3 Execução da aplicação

Para executar a aplicação o seguinte comando deve ser executato no terminal na pasta raiz da aplicação:

```
npm run debug
```

 Na primeira execução esse comando deve demorar um pouco, pois serão instalados as dependencias, como o TypeScrip que terá a função de transformar os arquivos .ts em arquivos .js e o SASS que terá a responsabilidade de tranformar os arquivos .scss em .css, para que seja possível do navegador interpretar.

 Assim que o comando terminar, será apresentado uma mensagem com o seguinte enderço ip: `http://127.0.0.1:1234`, abra este endereço no _browser_ e você verá uma página azul com o alerta "Hello World".

 ## 1.4 Conexão com o Banco de Dados


...
