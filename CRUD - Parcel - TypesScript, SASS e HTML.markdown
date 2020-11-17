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

```shell
node --version
```

Se tudo ocorreu bem na instalação isso deve apresentar a versão do NodeJS instalado atualmente.

Para verificar se o **NPM** também está instalado corretamente execute o seguinte comando:

```shell
npm --version
```

assim como no caso do comando anterior apresentava a versão do NodeJS instalado, este deve mostrar a versão do NPM instalado no momento, caso a instalação tenha sido bem sucedida.

## 1.2 Preparando a estrutura de pastas e pacotes

Crie uma pasta com o nome que preferir, o nome escolhido para este tutorial foi `tuto_crud` (evite a utilização de caracteres especiais), dentro desta pasta criaremos uma subpasta chamada `src`, abreviação de _source_, é aqui onde colocaremos todos os fontes de nosso projeto, também criaremos uma subpasta chamada `dis` abreviação para _distributable_ é nesta pasta onde nossos arquivos prontos para serem distribuidos ficaram.

Além destas duas sub-pastas também criaremos uma terceira chamada `srv`, avreviação para _server_, é nesta pasta que colocaremos os arquivos do servidor de nossa aplicação. 

O próximo passo é criar o arquivo `package.json`, este arquivo é responsável por manter informações importantes sobre o projeto, como comandos para empacotamento e quais pacotes de terceiro serão utilizados etc. para criar este arquivo iremos utilizar o **NPM**, abra seu terminal e navegue até a pasta do projeto e então digite o seguinte comando:

```shell
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

### 1.2.1 Pacotes para desenvolvimento: Parcel e ts-node

Neste projeto utilizaremos o empacotador `Parcel`, ele será responsável por criar os arquivos para distribuição do projeto como por exemplo compilando arquivos TypeScript e SCSS para Javascript e CSS para que possam serem interpretados pelo browser, como este pacote será utilizado somente no momento do desenvolvimento, instalaremos o pacote da seguinte maneira, pelo terminal na pasta raiz do projeto executaresmos o seguinte comando:

```shell
npm install parcel --save-dev
```

Assim como o Parcel também instalaremos o modulo `ts-node`, este será responsavel por permitir exectarmos os arquivos `.ts` sem a necessidade de compila-los para `.js`, no lado servidor, para intalrmos o `ts-node`, na pasta raiz do projeto executatemos o seguinte comando:

```shell
npm install --save-dev ts-node
```

Todos os comandos de instalação de pacotes irá demorar um pouco, pois o NPM irá baixar estes pacotes dos servidores oficiais, após a primeira instalação de qualquer pacote uma nova pasta será criada com o nome `node_modules` onde ficaram todas as bibliotecas que utilizaremos no desenvolvimento da aplicação, o arquivo `package.json` irá ser atualizado, adicionando o trecho onde temos a lista de `dependencias de desenvolvimento`, ou seja os pacotes que serão utilizados somente durante o desenvolvimento:

```json
{
  …
  "devDependencies": {
      "parcel": "^1.12.4",
      "ts-node": "^9.0.0"
  }
  …
}
```

### 1.2.2 Pacotes Express e SQLite

Outros dois pacotes que utilizaremos é o `sqlite3` e o `express`, um responsável pela conexão com nosso banco de dados e outro responsável por manipular o acesso via HTTP ao nosso projeto, além das biliotecas já citadas, tabém instaleremos o pacote `sqlite` que nos permitirar fazer acesso ao banco de dados de maneira assincrona e com maior super as APIs modernas do Jasvascript/TypeScrit, para instalar estes pacotes de uma única vez, utilizaremos o seguinte comando:

```shell
npm install sqlite sqlite3 express
```

Note que desta vez não utilizamos o parâmetro `--save-dev`, pois estes pacotes serão necessários para o funcionamento da aplicação após a versão distribuição.

Como a aplicação depende desses pacotes para funcionar mesmo depois de empacotada, o arquivo `package.json` irá ser atualizado com a seguinte sessão:

```json
{
  …
  "dependencies": {
    "express": "^4.17.1",
    "sqlite": "^4.0.17",
    "sqlite3": "^5.0.0"
  }
  …
}
```

### 1.2.3 Arquivo de configuração de compilação TypsScript

Precisamos criar também o arquivo de configuração que informa como os arquivos `.ts` devem ser compilados para isso executaremos o seguinte comando na pasta raiz do nosso projeto:

```shell
npx tsc --init
```

Este comando cria-rá um arquivo chamado `tsconfig.json`, resposável por informar como os arquivos `.ts` devem ser compilados para `.js`, portanto neste arquivo mudaremos o a chave `target` de `"es5"` para `"ES2019"`, para que possamos assim utilizar APIs mais modernas do Javascript, o arquivo `tsconfig.json` vai deve ficar parecido com o seguinte:

```json
{
  "compilerOptions": {
    …
    "target": "ES2019",
    "module": "commonjs",
    …
    "strict": true,
    …
    "esModuleInterop": true,
    …
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  }
}
```

### 1.2.4 Como recriar a pasta node_module

A pasta `node_modules` pode ser excluida e recriada, pois o arquivo `package.json` possui toda a lista de pacotes necessários para o funcionamento e desenvolvimento da aplicação, o comando para recriar a pasta `node_module` é o seguinte:

```shell
npm install
```

este comando ira baixar novamente todos os modulos listados no arquivo `package.json`.

### 1.2.5 Arquivos de projeto: HTML, SCSS e TS

Em nosso proejto utilizaremos HTML, SCSS e TS, então na pasra `src` e `srv` criaremos os seguintes arquivos com os seguintes conteúdos:

#### 1.2.5.1 Pasta src (Cliente)

./src/index.html
```html
<!DOCTYPE html>
  <html lang="pt-BR">
  <head>
    <meta charset="UTF-8">
    <title>CRUD</title>
  </head>
  
  <body>
    <script src="./main.ts"></script>
  </body>
</html>
```

./src/main.ts
```ts
import "./main.scss";

alert("Hello World!");
```

./src/main.scss
```scss
body {
    background: lightgreen;
}
```

#### 1.2.5.2 Pasta srv (Servidor)

./srv/main.ts
```ts
console.log("Server: Hello World!");
```

### 1.2.5 Estrutura final das pastas

A estrutura final das pastas devem ficar da seguinte maneira:

- tuto_crud
  - node_module
    - …
  - dist
  - src
    - index.html
    - main.scss
    - main.ts
  - srv
    - main.ts
  - package.json
  - tsconfig.json

## 1.3 Preparando aplicação para execução

Para que possamos testar nosso projeto adicionaremos ao arquivo `package.json` o comando para depuação e teste de nossa aplicação, então adicione dentro da chave `scripts` os seguintes comandos 

```json
{
  …
  "scripts": {
    "debug": "parcel src/index.html",
    "server": "ts-node-script srv/main.ts",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  …
}
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

## 1.3 Teste/Execução do ambiente de desenvolvimento

Agora com nossa _ambiente de desenvolvimento_ configurado, vamos testar se tudo esta funcionando, se a aplicação cliente esta sendo empacotada corretamente e se conseguimos executar os arquivos da nossa aplicação servidora sem problemas. 

### 1.3.1 Teste/Execução da aplicação Cliente

Para executar a aplicação o seguinte comando deve ser executato no terminal na pasta raiz da aplicação:

```shell
npm run debug
```

 Na primeira execução esse comando deve demorar um pouco, pois serão instalados as dependencias, como o TypeScrip que terá a função de transformar os arquivos .ts em arquivos .js e o SASS que terá a responsabilidade de tranformar os arquivos .scss em .css, para que seja possível do navegador interpretar.

 Assim que o comando terminar, será apresentado uma mensagem com o seguinte enderço ip: `http://127.0.0.1:1234`, abra este endereço no _browser_ e você verá uma página azul com o alerta "Hello World".

### 1.3.2 Teste/Execução da aplicação Servidora

Para executar a aplicação o seguinte comando deve ser executato no terminal na pasta raiz da aplicação:

```shell
npm run server
```

A executção de comando deve imprimir no terminal o seguinte conteúdo:

```shell
> tuto_crud@1.0.0 server …tuto_crud
> ts-node srv/main.ts

Server: Hello World!
```

# 2. Conexão e criação do banco de dados

Nossa aplicação sera feita utilizando o banco SQLite e é comum que a aplicação que utilizão este banco crie o arquivo de banco de dados as tabelas em sua primeira execução, em nosso caso criaremos as tabelas do banco de dados caso elas não existam assim que iniciarmos a aplicação servidora, além de criar um objeto de conexão que nos permitirá manipular o banco, para que façamos isso de forma organizada criaremos um arquivo `database.ts` dentro da pasta `./srv`, este arquivo tera como responsabilidade, criar o arquivo de banco de dados `databaset.ts` também na pasta `./srv` e caso as tabelas necessárias para a aplicação não existirem este arquivo também será responsável por cria-las, o arquivo a seguir contem cométarios para que seja possível entender o que cada comando representa:

`./srv/database.ts`  
```ts
// importa o drive de conexão da biblioteca sqlite3
import { Database } from 'sqlite3';

// importa o método `open` da biblioteca sqlite, esta biblioteca nos permite
// trabalhar com bancos sqlite de maneira assíncrona
import { open } from 'sqlite';

// cria uma função assíncrona chamada init() e a exporta para que seja 
// possível utiliza-la fora deste modulo 
export async function init() {
    // aguarda quea função `open`seja executada, onde será criado o arquivo de 
    // banco de dados `srv/database.db` e retornará o objeto de conexão que
    // nos permitirá manipular o banco de dados
    const db = await open({
        filename: 'srv/database.db',
        driver: Database,
    });

    // cria a tabela pessoa caso ela não exista
    await db.exec(`
        CREATE TABLE IF NOT EXISTS pessoa (
            id        INTEGER PRIMARY KEY AUTOINCREMENT,
            nome      TEXT NOT NULL,
            sobrenome TEXT NOT NULL,
            email     TEXT NOT NULL UNIQUE,
            telefone  TEXT NOT NULL UNIQUE
        )
    `);

    // a função init() retorna o obejto d e conexão com o banco de dados
    return db;
}
```

Para que possamos executar a função `init()` que criamos no `database.ts` precisamos importa-la no nosso arquivo de entrada do servidor, no nosso caso o arquivo `main.ts`:

./srv/main.ts
```ts
// importa a função init e a apelida de initDatabase do arquivo `database.ts`
// note que a extensão `.ts` é omitida aqui
import { init as initDatabase } from "./database";

// cria uma função assincrona chamada init() (não confundir com a init do arquivo database.ts)
// esta função foi criada para que possamos manipular execuções assincornas utilizando as palavras
// reservadas async e await, facilitando o entendimento do código
async function init() {
    // aguarda a execução da função init() do arquivo database.ts
    await initDatabase();
}

// executa a função init()
init();
```

Para testar o que foi desenvolvido até o momento execute o comando `npm run server`, assim que a execução terminar, um arquivo chamado `database.db` deve aparecer na pasta `./srv`, é possível _abri-lo_ utilizando qualquer programa cliente de SQLite, aqui eu sugiro o [DB Browser for SQLite](https://sqlitebrowser.org/).

# [WIP] 3. Fomulário de cadastro
  
Para manter nossa aplicação cliente organizada e permiter a reunitlização de código, faremos componetes para os elementos de interface gráfica, aqui criaremos um componente que ficará responsável por apresentar dados de pessoas na tela, além de enviar informações para nossa aplicação servidora que permita adicionar, salvar, alterar e excluir pessoas,
para isso adicionaremos uma sub-pasta chamada `components` dentro da pasta `src`, e nesta pasta `components` adicionaremos uma sub-pasta chamada `form` que conterá três arquivos, `index.ts`, `template.html` e `template.scss`, além destes arquivos também criaremos `d.ts` dentro da pasta `./src/components`, este arquivo servirá apenas no momento de desenvolvimento para explicarmos como o `TypeScript` deve interpretar a importação de arquivos `.html`, logo mais falaremos mais sobre isso, no próximo tópico trataremos da criação dos arquivos de components.

## 3.1 Criando componente de formuláio pessoa

./src/components/form/template.html
```html
<link rel="stylesheet" href="./template.scss">

<form>
    <div>
        <label for="nome">Nome</label>
        <input name="nome" id="nome">
    </div>
    <div>
        <label for="sobrenome">Sobrenome</label>
        <input name="sobrenome" id="sobrenome">
    </div>
    <div>
        <label for="email">Email</label>
        <input name="email" id="email">
    </div>
    <div>
        <label for="telefone">Telefone</label>
        <input name="telefone" id="telefone">
    </div>
    <div class="footer">
        <button>salvar</button>
    </div>
</form>
```

./src/components/form/template.scss
```scss
* {
    box-sizing: border-box;
    font-family: Arial, Helvetica, sans-serif;
}

:host {
    display: inline-block;
    width: 100%;
}

form {
    font-size: 1.5em;

    > div {
        position: relative;
        height: 2em;
        margin-top: 1.3em;

        > label,
        > input {
            display: flex;
            align-items: center;
            padding: 0 0.5em;
            position: absolute;
            left: 0;
            right: 0;
            top: 0;
            bottom: 0;
            width: 100%;
            outline: none;
        }

        > label {
            z-index: 1;
            opacity: .3;
            transition: 300ms;
        }

        > input {
            border: 0 none;
            border-bottom: 1px solid rgba(#000000, .5);
            transition: 300ms;
            font-size: inherit;
            border-radius: 5px;

            &:focus {
                border-bottom: 2px solid rgba(#000000, 1);
            }
        }

        &.editing,
        &.not-empty {
            label {
                padding: 0;
                opacity: 1;
                transform: translateY(-1.85em) ;
                font-size: 80%;
            }
        }

        &.footer {
            display: flex;
            justify-content: flex-end;
            
            button {
                cursor: pointer;
                background-color: #FFFFFF;
                border-radius: 5px;
                border: 0 none;
                border-bottom: 1px solid rgba(#000000, .5);
                transition: 300ms;

                &:hover {
                    background: #EEEEEE;
                }
            }
        }
    }
}
```

./src/components/d.ts
```ts
declare module '*.html' {
    const value: string;
    export default value
}
```

./src/components/form/index.ts
```ts
import html from "./template.html";

class CrudModal extends HTMLElement {
    #root: ShadowRoot = this.attachShadow({ mode: 'open' });

    constructor() {
        super();
        this.#root.innerHTML = html;
        this.attachEvents();
    }

    private attachEvents() {
        this.#root.querySelector('form')?.addEventListener('submit', ev => ev.preventDefault());

        const inputs = this.#root.querySelector('form')?.querySelectorAll('input');
        inputs?.forEach(input => {
            input.addEventListener('focus', ev => this.onInputFocus(ev));
            input.addEventListener('keydown', ev => this.onInputFocus(ev));
            input.addEventListener('blur', ev => this.onInputBlurs(ev));
        });
    }

    private onInputFocus(ev: Event) {
        const target = <HTMLInputElement>ev.target;
        target.closest('div')?.classList.remove('not-empty');
        target.closest('div')?.classList.add('editing');
    }

    private onInputBlurs(ev: Event) {
        const target = <HTMLInputElement>ev.target;
        target.closest('div')?.classList.remove('editing');
        if (target.value.trim())
            target.closest('div')?.classList.add('not-empty');
    }
}

customElements.define('crud-form', CrudModal);
```

## 3.2 Adicionando componente de formulário pessoa ao projeto

./src/main.ts
```ts
import "./main.scss";
import "./components/form"; // <- adicionado a importação do componente
```

./src/index.html
```html
<!DOCTYPE html>
  <html lang="pt-BR">
  <head>
    <meta charset="UTF-8">
    <title>CRUD</title>
  </head>
  <body>
    <script src="./main.ts"></script>
    <crud-form></crud-form> <!-- adicionado componente no html -->
  </body>
</html>
```

./src/main.scss
```scss
body {
    background: lightgreen;
}

crud-form {
    max-width: 500px; // <- adicionado largura máxima para os componentes de formulários
}
```

…
