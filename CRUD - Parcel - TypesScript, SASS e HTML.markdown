# Cadastro de Pessoas
 
…

## 1. Servidor - RESTFul api

…

### Pré-requisitos
 
> [Introdução Express/Node](https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Express_Nodejs/Introdu%C3%A7%C3%A3o): 
> caso tenha pouco conhecimento sobre NodeJs e Express, sugiro a leitura deste 
> artigo do site _MDN Web Docs_.

Aqui veremos o que é necessário para que seja possível o desenvolvimento deste tutorial, caso não tenha conhecimento prévio dos itens listados abaixo é extremamente indicado que leia sobre o assunto, porém não é necessário que entenda o assunto a fundo cada um dos temas, é apenas necessário que saiba o básico para a execução do tutorial:

- Conhecimento básico de banco de dados:
  - DDL - Criação de tabelas
  - SQL
    - insert - inserção de dados
    - update - alteração de dados
    - select - busca e seleção de dados 
    - delete - exclusão de dados
- Conhecimento básico sobre o protocolo HTTP:
  - Fluxo de Comunicação
  - Códigos de respostas
  - Métodos de requisição
- REST e RESTFul:
  - Conceitos básicos
- Programação Básica em Javascript e/ou Typescript
- Estrutura de arquivos JSON

Também será necessário a instalação dos softwares a seguir, certifique que todos estejam instalados e funcionando:

- [NodeJS e NPM](https://nodejs.org/)
  - É possível entender um pouco mais sobre o que é o NodeJS [na página oficial _sobre_](https://nodejs.org/pt-br/about/), também é possível entender um pouco mais sobre o NPM [na página oficial _sobre_](https://docs.npmjs.com/about-npm).
- [VSCode](https://code.visualstudio.com/)
  - Neste tutorial utilizaremos o VSCode como editor, é possível conhecer um pouco mais sobre o VSCode [na página oficial _sobre_](https://code.visualstudio.com/docs).
- [DB Browser for SQLite](https://sqlitebrowser.org/) - *ou outro cliente para SQLite*
  - Para testar e visualizar o banco de dados que criaremos no decorrer deste tutorial, utilizaremos o cliente de banco de dados SQLite _DB Browser for SQLite_, é possível conhecer mais sobre este cliente [na página oficial _sobre_](https://sqlitebrowser.org/about/).
 
### Estrutura do Projeto 
 
Para iniciarmos o desenvolvimento crie uma pasta vazia chamada `cadastro-pessoa` e dentro desta pasta crie uma subpasta chamada `server`, esta será a pasta onde criaremos a API de nossa aplicação, após a criação abra a pasta `server` no VSCode (arraste a pasta `server` para dentro do VSCode).

A estrutura inicial do projeto deve ficar parecido com a seguir, note que a pasta que deve ser aberta no **VSCode** é a `server` e não a pasta `cadastro-pessoa`.
 
```shell
🗁 cadastro-pessoa
 └▹🗀 server          <---arraste esta pasta para o VSCode
```
 
#### Comandos de terminal NPM e NPX
 
O NPM (Node Package Manager) é responsável por controlar os pacotes que serão usados em nosso projeto, bem como o arquivo `package.json` que é o arquivo onde as informações de projetos `NodeJS` são mantidos.
 
Já o NPX tem a premissa de executar comandos de terminal sem que sejam necessários ter instalado a aplicação (que executará o comando) localmente, em resumo o NPX baixa o pacote que deseja executar o comando no terminal e assim que a execução do comando termina ele apaga este pacote.
 
segue alguns exemplo de comandos e explicações que utilizaremos em nosso projeto:
 
- npm init -y
  - _este comando é responsável por criar o arquivo `package.json`, o parâmetro `-y` indica que a resposta para todas as eventuais perguntas durante a criação do arquivo será respondida com `sim`, caso queira criar o arquivo `package.json` de maneira personalizada, remova este parâmetro._
- npm install _nome_dos_pacotes_
  - _este comando é responsável por baixar pacotes a partir da base do NPM e salvá-los na pasta `node_modules`, além de baixar eventuais pacotes interdependentes dos que solicitamos instalação, para controle destes pacotes extras é criado um segundo arquivo `package-lock.json`._
  - _cada pacote baixado é o adiciona à lista de dependências do arquivo `package.json` assim como sua respectiva versão, na chave `dependeces` do arquivo, caso seja adicionado o parâmetro `--save-dev` estes pacotes são adicionada na lista de dependências de desenvolvimento, o que significa que para a versão de distribuição estes pacotes não são necessários, a chave para esta lista no arquivo `package.json` é `devDependences`._
  - _O NPM é capaz de recriar todas as dependências a partir do arquivo `package.json`, por isso em uma eventual distribuição do projeto, não é necessário o compartilhamento da pasta `node_modules` nem do arquivo `package-lock.json`, pois executando o comando `npm install` sem especificar nome de módulos, o node irá procurar no arquivo `package.json` todos os módulos a serem instalados, recriando assim a pasta `node_modules` e o arquivo `package-lock.json`._
- npm run _chave_do_script_
  - _este comando executa um dos comandos listados na chave `scripts` do arquivo `package.json`, vale ressaltar que `npm run` executa comandos no contexto local do `npm`, sendo possível executar comandos de módulos que foram instalados localmente_.
- npx _nome_do_pacote_
  - _este comando irá baixar o pacote e executá-lo, assim que sua execução terminar o pacote é excluído._
 
#### Inicialização do Projeto (arquivo package.json)
 
Para criarmos o arquivo `package.json` iremos utilizar o `NPM`, este arquivo é responsável por manter informações importantes sobre o projeto, como comandos para empacotamento e execução, quais pacotes de terceiro serão utilizados, além de nome do autor, versão do projeto etc. abra o **terminal do VSCode** _ctrl+'_ e digite o seguinte comando:
 
```shell
npm init -y
```

Este comando criará um arquivo chamado `package.json` sem fazer nenhuma pergunta, para ter a possibilidade de criar o arquivo já com dados customizados, execute o mesmo comando porém sem o parâmetro `-y` (este parâmetro significa, responda _yes_ para todas perguntas).

O arquivo gerado terá uma estrutura semelhante a esta:

_package.json_
```json
{
  "name": "server",
  "version": "1.0.0",
  "description": "tutorial - desenvolvimento de uma API",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "Daniel de A. Varela",
  "license": "Apache-2.0"
}
```

Neste momento não alteraremos o arquivo `package.json` gerado, mas logo mais o configuraremos com as especificidades de nosso projeto.
 
#### Instalação de dependências para execução da aplicação
 
Aqui instalaremos bibliotecas essenciais para a execução de nossa aplicação, ou seja, sem elas nossa aplicação não pode ser executada, instalaremos o framework `Express`, que será utilizado para manipulação das requisições HTTP de nossa aplicação, também instalaremos a biblioteca `body-parser` para facilitar a leitura dos dados enviados no corpo de nossas requisições HTTP, para efetuar a instalação dessas bibliotecas, abra o **terminal do VSCode** _ctrl+'_ e digite o seguinte comando:

```shell
npm install express body-parser
```

Para acesso e manipulação do banco de dados utilizaremos duas bibliotecas, a primeira é a `sqlite3`, que servirá de _driver_ para conexão com o banco de dados, e para que seja possível fazer requisições assíncronas ao banco utilizaremos a biblioteca `sqlite`. No **terminal do VSCode** _ctrl+'_ digite o seguinte comando para instalarmos estas bibliotecas:
 
```shell
npm install sqlite3 sqlite
```

Após o término da instalação dos módulos é possível notar que o arquivo `package.json` foi acrescido com a seguinte entrada, isso descreve quais pacotes são essenciais para a execução da aplicação que estamos desenvolvendo:

_package.json_
```json
{
  …
  "dependencies": {
    "body-parser": "*",
    "express": "*",
    "body-parser": "*",
    "sqlite": "*",
    "sqlite3": "*"
  }
  …
}
```

> Abaixo temos uma versão do arquivo `package.json` mostrando as chaves que foram adicionadas, note que esta é uma representação parcial do arquivo, `…` representa a parte removida na representação.

#### Instalação de dependências para desenvolvimento da aplicação
 
Aqui instalaremos as bibliotecas necessárias para o desenvolvimento da aplicação, estas não precisam fazer parte da _versão de produção_ do sistema, note que adicionamos o parâmetro `--save-dev` no comando de instalação, isto se dá justamente para informar que estas bibliotecas são necessárias somente para o desenvolvimento.
 
Instalaremos a biblioteca `typescript` para que possamos compilar a _versão de produção_, esta biblioteca será responsável por converter os arquivos `.ts` para arquivos `.js` além de criar arquivos `.js.map` para que seja possível vincular eventuais erros ocorridos durante a execução dos arquivos `.js` com os códigos dos arquivos `.ts`. 

Instalaremos também a biblioteca `ts-node`, esta nos permitirá executar a aplicação sem que seja necessário a criação dos arquivos `.js` e `.js.map`, isso poupará tempo durante o desenvolvimento.

```shell
npm install --save-dev typescript ts-node
```

Outra biblioteca importante para o desenvolvimento é a `@types/express`, como o desenvolvimento desta aplicação é baseada em **TypeScript** as bibliotecas essencialmente desenvolvidas em **Javascript** não possuem tipos e notação de objetos, classes etc, então arquivos de tipos são necessários para que o **VSCode** consiga _autocompletar_, para a instalção desta biblioteca digite o seguinte comando no **terminal do VSCode** _ctrl+'_:

```shell
npm install --save-dev @types/express
```

Após a instalação dos módulos é possível notar que o arquivo `package.json` foi acrescido com a seguinte entrada, isso descreve quais pacotes são essenciais para o desenvolvimento da aplicação:

_packaje.json_
```json
{
  …
  "devDependencies": {
    "@types/express": "*",
    "ts-node": "*",
    "typescript": "*"
  }
  …
}
```

> Abaixo temos uma versão do arquivo `package.json` mostrando as chaves que foram adicionadas, note que esta é uma representação parcial do arquivo, `…` representa a parte removida na representação.

#### Criação do arquivo de configuração do compilador TypeScript (arquivo tsconfig.json)
 
Para que seja possível informar ao `typescript` e ao `ts-node` como compilar e/ou interpretar os arquivos `.ts` é necessário a criação de um arquivo `tsconfig.json`; A fim de facilitar este passo, utilizaremos o **NPX**, no **terminal do VSCode** digite o seguinte comando:  
 
```shell
npx typescript --init
```

Neste momento não alteraremos o arquivo `tsconfig.json` gerado, mas logo mais o configuraremos com as especificidades de nosso projeto.
 
#### Criação manual de pastas e arquivos
 
Além de todos os arquivos gerados automaticamente será necessário criar pastas e arquivos manualmente, então dentro da estrutura atual de nosso projeto adicione os arquivos e pastas listado abaixo:
 
```shell
🗁 server
├▹🗀 dist             <---pasta onde os arquivo compilados serão armazenados
└▹🗁 src              <---pasta com os códigos fontes
  ├▹🗎 main.ts         <---arquivo de entrada da aplicação
  └▹🗎 database.ts     <---arquivo responsável pela conexão com o banco de dados

```

Nesta estrutura o único item opcional é a pasta `./dist`, pois a mesma será criada automaticamente quando utilizarmos o `typescript` para compilar os arquivos `.ts`.
 
#### Conclusão (estrutura)
 
Ao término desse processo, nossa estrutura de arquivos deve ser parecida com a abaixo apresentada, note que a pasta `node_module` e `dist` estão fechadas, não sendo assim listadas na representação abaixo: 
 
```shell
🗁 server
├🗀 dist
├🗀 node_module
├🗁 src
│ ├▹🗎 database.ts
│ └▹🗎 main.ts
├▹🗎 openapi.yaml
├▹🗎 package-lock.json
├▹🗎 package.json
└▹🗎 tsconfig.json
```
 
### Preparando para compilação e execução
 
Neste tópico alteraremos os arquivos de configuração para que se _encaixe_ nas necessidades específicas de nosso projeto. 
 
#### TypeScript (tsconfig.json)

Iniciaremos configurando o arquivo `tsconfig.json`, este arquivo como dito anteriormente, tem a responsabilidade de configurar como o `typescript` e `ts-node` irá interpretar e/ou executar os arquivos `.ts`, segue as chaves que devem ser alteradas com as devidas descrições de motivo de alteração:

- `target` - alterar para `ES2020`
  - _aqui definimos que os arquivos `.js` gerados devem ser feitos para a versão `ES20202` do `Javascript`_.
- `sourceMap` - descomentar e definir o valor como `true`
  - _aqui informamos que o typescript deve gerar arquivos `.js.map`, para que seja possível rastrear os erros ocorridos nos arquivos `.js` nos arquivos `.ts`_
- `outDir` - descomentar e definir o valor para `./dis`
  - _aqui definimos que ao compilar os arquivos `.ts`, os mesmos devem ser salvos na pasta `./dist` (esta será a pasta que contém os arquivos da aplicação que serão distribuídos como versão produção)_.

_tsconfig.json_
```json
{
  "compilerOptions": {
    "target": "ES2020",    <---alterado
    "module": "commonjs",
    "sourceMap": true,     <---alterado
    "outDir": "./dist",    <---alterado
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  }
}
```

> Abaixo temos uma versão do arquivo `tsconfig.json` mostrando as chaves que foram alteradas, note que os comentários foram removidos e que o texto `<---alterado` é somente para demonstrar onde foram feitas as alterações e não devem estar presentes no arquivo real. 


#### Scripts de testes e Execuções (package.json)

Para que seja possível executar e testar a aplicação em desenvolvimento, criaremos dois scripts no arquivo `package.json`, dentro da chave `scripts` adicionaremos a entrada `"build": "tsc"`, este comando é responsável por iniciar o processo de compilação do `typescript`, a segunda entrada que deve ser adicionada é a seguinte `"debug": "ts-node-script src/main.ts"`, este comando será responsável por executar nosso projeto no momento de desenvolvimento e testes. 
 
_packaje.json_
```json
{
  …
  "scripts": {
    "build": "tsc",                                        <---adicionado
    "debug": "ts-node-script src/main.ts",                 <---adicionado
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  …
}
```

> Abaixo temos uma versão do arquivo `package.json` mostrando as chaves que foram adicionadas, note que esta é uma representação parcial do arquivo, `…` representa a parte removida na representação, note também e que o texto `<---adicionado` é somente para demonstrar onde foram feitas as alterações e não devem estar presentes no arquivo real. 

No tópico seguinte será demonstrado com executar esses scripts.
 
### Teste da estrutura do projeto
 
Para que possamos testar os `scripts` e configurações que fizemos no passo anterior, teremos que atualizar o arquivo `src/main.ts`, adicionaremos `console.log("Olá mundo!");` no início do arquivo, salvaremos para que possamos executar o comando de teste.
 
_src/main.ts_
```typescript
console.log("Olá mundo!");
```
 
Agora podemos executar o comando de testes, abra o **terminal do VSCode** _ctrl+'_ e execute o seguinte comando:
 
```shell
npm run debug
```
 
Se tudo estiver _ok_ você deve ver o seguinte resultado no terminal:
 
```
> server@1.0.0 debug C:\cadastro-de-pessoa\server
> ts-node-script src/main.ts
 
Olá mundo!
```
 
Podemos testar se a compilação para a versão final está ocorrendo sem problemas para isso, abra o **terminal do VSCode** _ctrl+'_ e execute:
 
```shell
npm run build
```
 
Se tudo estiver _ok_ você deve ver os arquivos criados na pasta `./dist`, para verificar se a compilação foi bem sucedida execute o seguinte comando:
 
```shell
node dist/main.js
```
 
Se estiver tudo _ok_ você verá a mensagem `Olá mundo!` no terminal.

### Criando rotas de acesso ao Servidor 

Criaremos neste momento a capacidade do nosso servidor a responder requisições HTTP, mais específicamente criaremos duas rotas de acesso sendo a primeira, `/pessoa`, `GET` e `POST`, e a segunda rota será `/pessoa/:id` que responderá os métodos HTTP `GET`, `PUT` e `DELETE`.

Segue descrição de quais são as atribuições de cada uma dessas rotas assim que fizermos conexão com o banco de dados:

- /pessoa
  - `GET` - responsável por listar todos os dados de todas as pessoas no banco de dados.
  - `POST` - responsável por criar um nova pessoa no banco de dados.
- /pessoa/:id
  - `GET` - responsável por listar somente os dados de uma pessoa específica, encontrada pelo valor contido em `:id`.
  - `PUT` - responsável por atualizar os dados de uma pessoa específica, encontrada pelo valor contido em `:id`.
  - `DELETE` - responsável por excluir somente os dados de uma pessoa específica, encontrada pelo valor contido em `:id`.

Criaremos neste momento a capacidade do nosso servidor a responder requisições HTTP, mais específicamente criaremos duas rotas de acesso sendo a primeira, `/pessoa`, `GET` e `POST`, e a segunda rota será `/pessoa/:id` que responderá os métodos HTTP `GET`, `PUT` e `DELETE`.
 
Segue descrição de quais são as atribuições de cada uma dessas rotas assim que fizermos conexão com o banco de dados:
 
- /pessoa
  - `GET` - responsável por listar todos os dados de todas as pessoas no banco de dados.
  - `POST` - responsável por criar uma nova pessoa no banco de dados.
- /pessoa/:id
  - `GET` - responsável por listar somente os dados de uma pessoa específica, encontrada pelo valor contido em `:id`.
  - `PUT` - responsável por atualizar os dados de uma pessoa específica, encontrada pelo valor contido em `:id`.
  - `DELETE` - responsável por excluir somente os dados de uma pessoa específica, encontrada pelo valor contido em `:id`.
 
O arquivo a seguir ainda não é capaz de comunicar-se com o banco de dados, mas nos permitirá testar se o servidor é capaz de responder as requisições HTTP que o cliente fará, o arquivo está comentado linha-a-linha para que seja possível compreender seu funcionamento, nos próximos passos daremos a capacidade de nosso servidor comunicar-se com o banco de dados, assim efetivamente criando, alterando, listando e excluindo informações em nossa base de dados.
 
Abra o arquivo `src/main.ts` e substitua seu conteúdo pelo seguinte:

_src/main.ts_
```typescript
//
// IMPORTA A BIBLIOTECA EXPRESS PARA CONTROLE DE REQUISEÇÃO HTTP.
//

import express from "express";

//
// IMPORTA A BIBLIOTECA BODY-PARSER PARA FACILITAR A LEITURA DO CORPO HTTP  DA 
// REQUISIÇÃO RECEBIDA PELO CLIENTE.
//

import bodyParser from "body-parser";

//
// CRIA OBJETO QUE IRÁ CONTROLAR AS REQUISIÇÕES HTTP DA APLICAÇÃO.
//

const app = express();

//
// ADICIONA AO CABEÇALHO DE TODAS AS RESPOSTAS DAS REQUISIÇÕES HTTP, INFORMAÇÕES 
// QUE PERMITEM O ACESSO POR QUALQUER ORIGEM AOS MÉTODOS [GET,PUT,POST,DELETE].
//

// adiciona função a ser executada antes de qualquer requisição HTTP.
app.use(
    // função que será executada antes da função de qualquer função definida 
    // para a `rota` e `método HTTP` que atualmente esta sendo requisitada.
    function (request, response, next) {
        // define no cabeçalho de resposta que as requisições podem ser feitas 
        // a partir de qualquer domínio (*).
        response.header('Access-Control-Allow-Origin', '*');
        // define no cabeçalho de resposta que os métodos GET, PUT, POST, DELETE
        // são permitidos.
        response.header('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE');
        // define no cabeçalho de resposta que é permitido a chave Content-Type 
        // no cabeçalho de requisição.
        response.header('Access-Control-Allow-Headers', 'Content-Type');
        // segue o fluxo para execução.
        next();
    }
);

//
// INICIA A TRADUÇÃO DO CORPO HTTP RECEBIDO PELO CLIENTE EM QUAISQUER UMA DAS 
// REQUISIÇÕES.
//

// adiciona função de `tratamento` do corpo da requisição HTTP recebida para que 
// seja executada antes de qualquer função definida para a `rota`  e `método 
// HTTP` atual.
app.use(bodyParser.json());

//
// RESPONDE SOLICITAÇÃO DO CLIENTE: LISTAGEM DE DADOS DE TODAS AS PESSOAS.
//

// espera requisições `GET` na rota `/pessoa`
app.get('/pessoa',
    // Função que o servidor executará quando receber a requisição nesta rota: 
    // - o parâmetro `request` é um objeto que nos ajuda a entender os dados 
    //   contidos nas requisições HTTP
    // - o parâmetro `response`  é um objeto que nos ajuda a responder as 
    //   requisições HTTP
    function (request, response) {
        // cria o objeto que utilizaremos para responder a requisição HTTP, 
        // enviaremos os dados contidos neste objeto no corpo da resposta HTTP 
        // para que seja possível verifica se o servidor está recebendo as 
        // requisições corretamente, bem como se está respondendo corretamente.
        const responseData = {
            // adiciona a chave `teste` ao objeto para verificar se o servidor 
            // consegue responder corretamente as esta requisição.
            teste: "buscar dados de todas as pessoas pessoas"
        };
        // responde para o cliente em formato JSON o objeto criado anteriormente.
        response.json(responseData);
    }
);

//
// RESPONDE SOLICITAÇÃO DO CIENTE: INSERÇÃO DE NOVA PESSOA.
//

// espera requisições `POST` na rota `/pessoa`.
app.post('/pessoa',
    // Função que o servidor executará quando receber a requisição nesta rota: 
    // - o parâmetro `request` é um objeto que nos ajuda a entender os dados 
    //   contidos nas requisições HTTP
    // - o parâmetro `response`  é um objeto que nos ajuda a responder as 
    //   requisições HTTP
    function (request, response) {
        // cria o objeto que utilizaremos para responder a requisição HTTP, 
        // enviaremos os dados contidos neste objeto no corpo da resposta HTTP 
        // para que seja possível verifica se o servidor está recebendo as 
        // requisições corretamente, bem como se está respondendo corretamente.
        const responseData = {
            // adiciona a chave `teste` ao objeto para verificar se o servidor 
            // consegue responder corretamente as esta requisição.
            teste: "adicionar dados de pessoa no banco de dados",
            // adiciona a chave `vindoDoCliente` ao objeto para que o servidor 
            // responda o que recebeu no corpo da requisição HTTP, para que 
            // assim seja possível verificar-mos se o servidor está recebendo os 
            // dados corretamente.
            vindoDoCliente: request.body
        };
        // responde para o cliente em formato JSON o objeto criado anteriormente.
        response.json(responseData);
    }
);

//
// RESPONDE SOLICITAÇÃO DO CIENTE: LISTAGEN DE DADOS DE UMA PESSOA ESPECÍFICA.
//

// espera requisições `GET` na rota `/pessoa/:id`.
app.get('/pessoa/:id',
    // Função que o servidor executará quando receber a requisição nesta rota: 
    // - o parâmetro `request` é um objeto que nos ajuda a entender os dados 
    //   contidos nas requisições HTTP
    // - o parâmetro `response`  é um objeto que nos ajuda a responder as 
    //   requisições HTTP
    function (request, response) {
        // cria o objeto que utilizaremos para responder a requisição HTTP, 
        // enviaremos os dados contidos neste objeto no corpo da resposta HTTP 
        // para que seja possível verifica se o servidor está recebendo as 
        // requisições corretamente, bem como se está respondendo corretamente.
        const responseData = {
            // adiciona a chave id ao objeto para que seja possível verifica se 
            // o servidor está recebendo corretamente a chave `:id` pela rota 
            // atual.
            id: request.params.id,
            // adiciona a chave `teste` ao objeto para verificar se o 
            // servidor consegue responder corretamente as esta requisição.
            teste: "buscar dados de uma pessoa específica"
        };
        // responde para o cliente em formato JSONo objeto criado anteriormente.
        response.json(responseData);
    }
);

//
// RESPONDE SOLICITAÇÃO DO CIENTE: ALTERAÇÂO DE DADOS DE UMA PESSOA ESPECÍFICA.
//

// espera requisições `PUT` na rota `/pessoa/:id`.
app.put('/pessoa/:id',
    // Função que o servidor executará quando receber a requisição nesta rota: 
    // - o parâmetro `request` é um objeto que nos ajuda a entender os dados 
    //   contidos nas requisições HTTP
    // - o parâmetro `response`  é um objeto que nos ajuda a responder as 
    //   requisições HTTP
    function (request, response) {
        // cria o objeto que utilizaremos para responder a requisição HTTP, 
        // enviaremos os dados contidos neste objeto no corpo da resposta HTTP 
        // para que seja possível verifica se o servidor está recebendo as 
        // requisições corretamente, bem como se está respondendo corretamente.
        const responseData = {
            // adiciona a chave id ao objeto para que seja possível verifica se 
            // o servidor está recebendo corretamente a chave `:id` pela rota 
            // atual.
            id: request.params.id,
            // adiciona a chave `teste` ao objeto para verificar se o servidor 
            // consegue responder corretamente as esta requisição.
            teste: "atualiza dados de uma pessoa específica",
            // adiciona a chave `vindoDoCliente` ao objeto para que o servidor 
            // responda o que recebeu no corpo da requisição HTTP, para que 
            // assim seja possível verificar-mos se o servidor está recebendo os 
            // dados corretamente.
            vindoDoCliente: request.body
        };
        // responde para o cliente em formato JSON o objeto criado anteriormente.
        response.json(responseData);
    }
);

//
// RESPONDE SOLICITAÇÃO DO CIENTE: EXCLUISÃO DE DADIS DE UMA PESSOA ESPECÍFICA.
//

// espera requisições `DELETE` na rota `/pessoa/:id`.
app.delete('/pessoa/:id',
    // Função que o servidor executará quando receber a requisição nesta rota: 
    // - o parâmetro `request` é um objeto que nos ajuda a entender os dados 
    //   contidos nas requisições HTTP
    // - o parâmetro `response`  é um objeto que nos ajuda a responder as 
    //   requisições HTTP
    function (request, response) {
        // cria o objeto que utilizaremos para responder a requisição HTTP, 
        // enviaremos os dados contidos neste objeto no corpo da resposta HTTP 
        // para que seja possível verifica se o servidor está recebendo as 
        // requisições corretamente, bem como se está respondendo corretamente.
        const responseData = {
            // adiciona a chave id ao objeto para que seja possível verifica se 
            // o servidor está recebendo corretamente a chave `:id` pela rota 
            // atual.
            id: request.params.id,
            // adiciona a chave `teste` ao objeto para verificar se o servidor 
            // consegue responder corretamente as esta requisição.
            teste: "exclui dados de uma pessoa específica",
        };
        // responde para o cliente em formato JSON o objeto criado anteriormente.
        response.json(responseData);
    }
);

//
// INICIA ESPERA DE REQUISIÇÃO NA PORTA 8081 E IMPRIME A MENSAGEM `running...` 
// NO TERMINAL.
//

app.listen(8081, () => console.log("running..."));
```

#### Testando as requisições HTTP

…

#### Arquivo para teste do servidor
 
Será necessário criar artifícios para que possamos testar o que fizemos até o momento, existem muitas alternativas para que nossos testes de requisição possam ser realizados, existem aplicações como o `Insomnia.rest` e `Postman` que são desenvolvidos para isso, bem como temos o `OpenApi/Swagger` que também pode auxiliar nesta tarefa, porém nossa abordagem consistirá em desenvolver uma pequena página com HTML e Javascript, neste momento não entraremos nos detalhes de como esta funciona, pois utilizaremos ela novamente no desenvolvimento da `aplicação cliente`, ai sim detalharemos o funcionamento de cada uma das funções que desenvolvemos aqui.
 
Crie um arquivo chamado `teste-api.html` (de preferência fora da estrutura do projeto) e adicione o seguinte código:

_teste-api.html_
```html
<html>
  <head>
      <title>Teste API</title>
  </head>
  <body>
      Abra o console do browser para executar os testes:
      <pre>
        await buscarPessoas();
        await adicionarPessoa({nome: "Daniel", sobrenome: "de Andrade Varela", apelido: "Varela"});
        await buscarPessoa(43);
        await alterarPessoa(43, {nome: "Daniel", sobrenome: "de Andrade Varela", apelido: "Varela"});
        await excluirPessoa(43);
      </pre>
      <script>
          // ENDEREÇO LOCAL ONDE A API SERÁ EXECUTADA.
          const host = "http://localhost:8081";

          // SOLICITA AO SERVIDOR: LISTAGEM DE DADOS DE TODAS AS PESSOAS.
          async function buscarPessoas() {
              const configReq = { method: "get" };
              const req = await fetch(host+"/pessoa")
              const res = await req.json();
              return res;
          }

          // SOLICITA AO SERVIDOR: INSERÇÃO DE NOVA PESSOA.
          async function adicionarPessoa(dadosDePessoa) {
              const configReq = {
                  method: "post",
                  headers: { "Content-Type": "application/json" },
                  body: JSON.stringify(dadosDePessoa)
              };
              const req = await fetch(host+"/pessoa", configReq);
              const res = await req.json();
              return res;
          }

          // SOLICITA AO SERVIDOR: LISTAGEN DE DADOS DE UMA PESSOA ESPECÍFICA.
          async function buscarPessoa(id) {
              const configReq = { method: "get" };
              const req = await fetch(host + "/pessoa/" + id)
              const res = await req.json();
              return res;
          }

          // SOLICITA AO SERVIDOR: ALTERAÇÂO DE DADOS DE UMA PESSOA ESPECÍFICA.
          async function alterarPessoa(id, dadosDePessoa) {
              const configReq = {
                  method: "put",
                  headers: { "Content-Type": "application/json" },
                  body: JSON.stringify(dadosDePessoa)
              };
              const req = await fetch(host + "/pessoa/" + id, configReq);
              const res = await req.json();
              return res;
          }

          // SOLICITA AO SERVIDOR: EXCLUISÃO DE DADIS DE UMA PESSOA ESPECÍFICA.
          async function excluirPessoa(id) {
              const configReq = { method: "delete" };
              const req = await fetch(host + "/pessoa/" + id, configReq);
              const res = await req.json();
              return res;
          }
      </script>
  </body>
</html>
```

#### Executando os testes

Para que possamos executar os testes em nosso servidor é necessário iniciá-lo, no **terminal do VSCode** _ctrl+'_ digite o seguinte comando `npm run debug`, se tudo estiver _ok_ você verá a mensagem `running...` em seu terminal.

Agora abra o arquivo `teste-api.html` que criamos no passo anterior em seu _browser_ preferido.

##### Testar a rota `GET /pessoa` - _listar todas as pessoas_

Execute o seguinte comando no console do seu browser com a página `teste-api.html` aberta:

```javascript
await buscarPessoas();
```

O resultado deve ser o seguinte:

```javascript
{teste: "buscar dados de todas as pessoas pessoas"}
```

##### Testar a rota `POST /pessoa` - _adicionar uma pessoa_

Execute o seguinte comando no console do seu browser com a página `teste-api.html` aberta:

```javascript
await adicionarPessoa({nome: "Daniel", sobrenome: "de Andrade Varela", apelido: "Varela"});
```

O resultado deve ser o seguinte:

```javascript
{teste: "adicionar dados de pessoa no banco de dados", vindoDoCliente: {…}}
```

> note que  `vindoDoCliente> {...}` é exatamente o que foi enviado para o servidor, para poder ler o retorno clique em `{...}`.

##### Testar a rota `GET /pessoa/:id` - _listar informações de uma pessoa específica_

Execute o seguinte comando no console do seu browser com a página `teste-api.html` aberta:

```javascript
await buscarPessoa(43);
```

O resultado deve ser o seguinte:

```javascript
{id: "43", teste: "buscar dados de uma pessoa específica"}
```

> note que o valor da chave `id` é exatamente o que foi enviado para o servidor.

##### Testar a rota `PUT /pessoa/:id` - _adicionar uma pessoa_

Execute o seguinte comando no console do seu browser com a página `teste-api.html` aberta:

```javascript
await alterarPessoa(43, {nome: "Daniel", sobrenome: "de Andrade Varela", apelido: "Varela"});
```

O resultado deve ser o seguinte:

```javascript
{id: "43", teste: "atualiza dados de uma pessoa específica", vindoDoCliente: {…}}
```
> note que o valor da chave `id` é exatamente o que foi enviado para o servidor.

> note que  `vindoDoCliente> {...}` é exatamente o que foi enviado para o servidor, para poder ler o retorno clique em `{...}`.

##### Testar a rota `DELETE /pessoa/:id` - _listar informação de uma pessoa específica_

Execute o seguinte comando no console do seu browser com a página `teste-api.html` aberta:

```javascript
await excluirPessoa(43);
```

O resultado deve ser o seguinte:

```javascript
{id: "43", teste: "exclui dados de uma pessoa específica"}
```

> note que o valor da chave `id` é exatamente o que foi enviado para o servidor.

#### ZZZZZ […]

É possível notar que o `browser` (aqui agindo como cliente), está fazendo requisições ao servidor que desenvolvemos, note que as respostas são consequência das constantes `responseData` que criamos no arquivo `src/main.ts`, dentro de cada uma das rotas, e que nas rotas `POST /pessoa` e `PUT /pessoa/:id` o cliente envia informações pelo corpo da requisição HTTP e o servidor as devolve no corpo da resposta HTTP, mais especificamente dentro da chave `vindoDoCliente`; além disso é possível notar que nas rotas `GET /pessoa/:id`, `PUT /pessoa/:id` e `DELETE /pessoa/:id`, o valor `:id` recebido na rota (pela `URL`) é adicionado na chave `id` da resposta do servidor, em resumo podemos notar que é possível enviar informações tanto pela `URL` da requisição HTTP como pelo corpo da requisição, porém o corpo é utilizado em métodos `POST` e `PUT` ou seja, métodos que de fato necessitam enviar informações mais complexas para que o servidor execute alguma ação específica.

> **`DICA`**: Altere os valores das variáveis, tanto das requisições como no arquivo `src/main.ts` para testar e buscar um melhor entendimento de como as `requisições` e `resposta` funcionam em nosso projeto.

### Criação do banco de Dados
 
…
 
_src/database.ts_
```typescript
// IMPORTA O DRIVE DE CONEXÃO DA BIBLIOTECA SQLITE3.
import { Database } from 'sqlite3';
 
// IMPORTA O MÉTODO `OPEN` DA BIBLIOTECA SQLITE, ESTA BIBLIOTECA NOS PERMITE
// TRABALHAR COM BANCOS SQLITE DE MANEIRA ASSÍNCRONA.
import { open } from 'sqlite';
 
// CRIA UMA FUNÇÃO ASSÍNCRONA CHAMADA INIT() E A EXPORTA PARA QUE SEJA POSSÍVEL 
// UTILIZÁ-LA FORA DESTE MÓDULO.
export async function init() {
    // AGUARDA QUE A FUNÇÃO `OPEN`SEJA EXECUTADA, ONDE SERÁ CRIADO O ARQUIVO DE 
    // BANCO DE DADOS `SRV/DATABASE.DB` E RETORNARÁ O OBJETO DE CONEXÃO QUE
    // NOS PERMITIRÁ MANIPULAR O BANCO DE DADOS.
    const db = await open({
        filename: './database.db',
        driver: Database,
    });
 
    // CRIA A TABELA PESSOA CASO ELA NÃO EXISTA.
    await db.exec(`
        CREATE TABLE IF NOT EXISTS pessoa (
            id        INTEGER PRIMARY KEY AUTOINCREMENT,
            nome      TEXT NOT NULL,
            sobrenome TEXT NOT NULL,
            apelido   TEXT NOT NULL UNIQUE
        )
    `);
 
    // A FUNÇÃO INIT() RETORNA O OBJETO D E CONEXÃO COM O BANCO DE DADOS.
    return db;
}
```
 
#### Juntando as partes

Para que possamos executar a função do arquivo `src/database.ts` em nosso arquivo `src/main.ts`, precisamos primeiro importa-la, isso é possível ser feito com o seguinte comando `import { init } from "./database";`, porém a função que criamos no arquivo `src/database.ts` é assíncrona e portanto para que possamos utilizar a palavra reservada `await` que permite que esperemos o término da execução da função, será necessário que a chamada da função assíncrona seja feita dentro de outra função assíncrona, que chamaremos de `init`, mesmo nome que utilizamos no arquivo `src/database`, criando assim um conflito de nomes, para que possamos resolver este conflito iremos apelidar a função `init` importada do arquivo `src/database.ts`, para isso vamos alterar a linha de importação de `import { init } from "./database";` para `import { init as initDatabase } from "./database";`.

Todos os métodos que dependerão do banco de dados serão movidos para dentro da função `init` que acabamos de criar; Para ficar fácil o entendimento do que foi alterado no arquivo `src/main.ts`, as linhas que não necessitam serem movidas foram marcadas com o comentário `// *`, já as que necessitam serem movidas para dentro da função `init`, foram marcadas com o comentário `// **` e as linhas que foram adicionadas foram comentadas com a sua devida explicação.
 
_src/main.ts_
```typescript
// IMPORTA A FUNÇÃO INIT E A APELIDA DE INITDATABASE DO ARQUIVO `DATABASE.TS`, 
// NOTE QUE A EXTENSÃO `.TS` É OMITIDA AQUI.
import { init as initDatabase } from "./database";

// *
import express from "express";

// *
import bodyParser from "body-parser";

// *
const app = express();

// *
app.use(function (request, response, next) {
    response.header('Access-Control-Allow-Origin', '*');
    response.header('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE');
    response.header('Access-Control-Allow-Headers', 'Content-Type');
    next();
});

// *
app.use(bodyParser.json());

// CRIA UMA FUNÇÃO ASSÍNCRONA CHAMADA INIT() (NÃO CONFUNDIR COM A INIT DO 
// ARQUIVO DATABASE.TS) ESTA FUNÇÃO FOI CRIADA PARA QUE POSSAMOS MANIPULAR 
// EXECUÇÕES ASSÍNCRONAS UTILIZANDO AS PALAVRAS RESERVADAS ASYNC E AWAIT 
// FACILITANDO O ENTENDIMENTO DO CÓDIGO.
async function init() {
    // AGUARDA A EXECUÇÃO DA FUNÇÃO `INIT()` DO ARQUIVO `DATABASE.TS` E ARMAZENA 
    // O RETORNO DA FUNÇÃO NA CONSTANTE `DB`.
    const db = await initDatabase();

    // **
    app.get('/pessoa', function (request, response) {
        const responseData = {
            teste: "buscar dados de todas as pessoas pessoas"
        };
        response.json(responseData);
    });

    // **
    app.post('/pessoa', function (request, response) {
        const responseData = {
            teste: "adicionar dados de pessoa no banco de dados",
            vindoDoCliente: request.body
        };
        response.json(responseData);
    });

    // **
    app.get('/pessoa/:id', function (request, response) {
        const responseData = {
            id: request.params.id,
            teste: "buscar dados de uma pessoa específica"
        };
        response.json(responseData);
    });

    // **
    app.put('/pessoa/:id', function (request, response) {
        const responseData = {
            id: request.params.id,
            teste: "atualiza dados de uma pessoa específica",
            vindoDoCliente: request.body
        };
        response.json(responseData);
    });

    // **
    app.delete('/pessoa/:id', function (request, response) {
        const responseData = {
            id: request.params.id,
            teste: "exclui dados de uma pessoa específica",
        };
        response.json(responseData);
    });

    // **
    app.listen(8081, () => console.log("running..."));
}

// EXECUTA A FUNÇÃO INIT() DESTE ARQUIVO.
init();
```

##### Testando se a conexão foi bem sucedida

Execute o comando `npm run debug` no **terminal do VSCode** _ctrl+'_ para iniciar o servidor, caso esteja tudo _ok_ você verá a mensagem `running...` em seu terminal e o arquivo `database.db` aparecerá na pasta raiz de do projeto, abra este arquivo utilizando o **DB Browser** para verificar se a estrutura da tabela foi criada corretamente, caso queira é possível adicionar, alterar, listar e remover dados direto na tabela utilizando o **DB Browser**.

### Manipulação do banco de dados pela API

Estamos chegando na reta final do desenvolvimento da API, o que nos falta fazer é acrescentar a capacidade para que as rotas executem suas referidas ações no banco de dados, os passos a seguir mostram os trechos de códigos que iremos alterar explicando linha-a-linha que será alterado, com isso exemplificando como se dá o acesso ao banco de dados.

#### Função de `busca ao banco de dados` para a rota `GET /pessoa` do servidor - `app.get('/pessoa', function (request, response) { … }`

```typescript
// DEFINE A ROTA `GET /pessoa`.
app.get('/pessoa', 
    // ADICIONADO A PALAVRA RESERVADA ASYNC ANTES DA DECLARAÇÃO DA FUNÇÃO QUE É 
    // EXECUTADA QUANDO ESTA ROTA É REQUISITADA PELO CLIENTE, SERÁ NECESSÁRIO 
    // ESPERAR A RESPOSTA DO BANCO DE DADOS PARA QUE A EXECUÇÃO DA FUNÇÃO POSSA 
    // PROSSEGUIR, POR ISSO A ADIÇÃO DA PALAVRA ASYNC.
    async function (request, response) {
        // EXECUTA O MÉTODO `all` DO OBJETO DE CONEXÃO COM BANCO DE DADOS `db` E 
        // SEU VALOR DE RETORNO É ARMAZENADO NA CONSTANTE `responseData`; ESTE 
        // MÉTODO EXECUTA UMA SELEÇÃO NO BANCO DE DADOS E RETORNA UM ARRAY 
        // CONTENDO TODAS AS LINHAS ENCONTRADAS.
        //
        // O PRIMEIRO PARÂMETRO É UM SQL SELECT GENÉRICO QUE RETORNARÁ TODOS OS 
        // ITENS DA TABELA.
        const responseData = await db.all("SELECT * FROM pessoa");
        // RESPONDE A REQUISIÇÃO HTTP COMO UM JSON QUE CONTÉM OS VALORES 
        // ENCONTRADOS NO BANCO DE DADOS, NOTE QUE NÃO DEFINIMOS O HTTP STATUS 
        // CODE, POR PADRÃO O HTTP STATUS CODE É `200 Ok`.
        response.json(responseData);
    }
);
```
 
#### Função de `inserção ao banco de dados` para a rota `POST /pessoa` do servidor - `app.post('/pessoa', function (request, response) { … }`
 
```typescript
// DEFINE A ROTA `POST /pessoa`.
app.post('/pessoa', 
    // ADICIONADO A PALAVRA RESERVADA ASYNC ANTES DA DECLARAÇÃO DA FUNÇÃO QUE É 
    // EXECUTADA QUANDO ESTA ROTA É REQUISITADA PELO CLIENTE, SERÁ NECESSÁRIO 
    // ESPERAR A RESPOSTA DO BANCO DE DADOS PARA QUE A EXECUÇÃO DA FUNÇÃO POSSA 
    // PROSSEGUIR, POR ISSO A ADIÇÃO DA PALAVRA ASYNC.
    async function (request, response) {
        // VERIFICA SE NO CORPO DO TEXTO NÃO TEM AS CHAVES `nome`, `sobrenome` E 
        // `apelido`.
        if (!request.body.nome || !request.body.sobrenome || !request.body.apelido) {
            // CASO NÃO EXISTA UMA DAS CHAVES, O SERVIDOR RETORNA O `HTTP STATUS 
            // CODE`, `422` INFORMANDO QUE A ENTIDADE RECEBIDA NÃO PODE SER 
            // PROCESSADA.
            response.status(422); // Unprocessable Entity
            // RETORNA NO CORPO DA RESPOSTA UM OBJETO COM A CHAVE `error` QUE 
            // EXPLICA DE FORMA VERBOSA O ERRO OCORRIDO.
            response.json({ error: "dados incompletos." });
            // PARA A EXECUÇÃO DA FUNÇÃO NESTE MOMENTO, POIS SEM ESSAS 
            // INFORMAÇÕES NÃO HÁ MOTIVOS DE CONTINUAR A EXECUÇÃO.
            return;
        }
 
        // INICIA BLOCO DE TENTATIVA, ISSO SIGNIFICA QUE SE ALGUM DOS COMANDOS 
        // DEFINIDOS DENTRO DELE RETORNAR (throw) A EXECUÇÃO DO BLOCO É 
        // INTERROMPIDO E O FLUXO PASSA PARA O BLOCO`catch` PASSANDO COMO 
        // PARÂMETRO VALOR RETORNADO PELA LINHA QUE APRESENTOU O ERRO.
        try {
            // EXECUTA O MÉTODO `run` DO OBJETO DE CONEXÃO COM BANCO DE DADOS 
            // `db` E O RESULTADO DE SUA EXECUÇÃO É ARMAZENADO NA CONSTANTE 
            // `responseData`; ESTE MÉTODO EXECUTA QUALQUER SQL E RETORNA 
            // INFORMAÇÕES COMO A QUANTIDADE DE LINHAS AFETADAS; 
            //
            // O PRIMEIRO PARÂMETRO É UM SQL DE INSERÇÃO DE DADOS NA TABELA 
            // `pessoa` (note que os valores não foram adicionados, em seu lugar 
            // foram adicionadas âncoras `:` que serão substituídas pelos valores 
            // no momento da execução, permitindo assim que o método trate 
            // ataques de sql injection) E O SEGUNDO É UM OBJETO COM OS VALORES 
            // A SEREM SUBSTITUÍDOS PELASÃNCORAS DA STRING SQL DO PRIMEIRO 
            // PARÂMETRO.
            const responseData = await db.run(
                "INSERT INTO pessoa(nome, sobrenome, apelido) VALUES(:nome, :sobrenome, :apelido)",
                {
                    ":nome": request.body.nome,
                    ":sobrenome": request.body.sobrenome,
                    ":apelido": request.body.apelido
                }
            );
            // RETORNA NO CORPO DA RESPOSTA UM OBJETO INFORMAÇÕES DE QUANTAS
            // LINHAS FORAM AFETADAS, NOTE QUE NÃO DEFINIMOS O HTTP STATUS CODE,
            // POR PADRÃO O HTTP STATUS CODE É `200 Ok`.
            response.json(responseData);
        } 
        // CASO UM ERRO ACONTEÇA NO BLOCO TRY, O FLUXO DE EXECUÇÃO VEM PARA O
        // BLOCO CATCH RECEBENDO COMO PARÂMETRO O ERRO OCORRIDO
        catch (e) {
            // CASO UM ERRO ACONTEÇA, O SERVIDOR RETORNA O `HTTP STATUS CODE`, 
            // `500` INFORMANDO QUE UM ERRO DE PROGRAMAÇÃO OCORREU.
            response.status(500); // Internal Server Error
            // RETORNA NO CORPO DA RESPOSTA UM OBJETO COM A CHAVE `error` QUE 
            // EXPLICA DE FORMA VERBOSA O ERRO OCORRIDO, E TAMBÉM UMA CHAVE 
            // `detail` QUE RETORNA EXATAMENTE O OBJETO DE ERRO RECEBIDO PELO 
            // BLOCO CATCH.
            response.json({ error: "database error", detail: e });
        }
    }
);
```
 
#### Função de `busca no banco de dados` para a rota `GET /pessoa/:id` do servidor - `app.get('/pessoa/:id', function (request, response) { … }`
 
```typescript
// DEFINE A ROTA `GET /pessoa/:id`.
app.get('/pessoa/:id', 
    // ADICIONADO A PALAVRA RESERVADA ASYNC ANTES DA DECLARAÇÃO DA FUNÇÃO QUE É 
    // EXECUTADA QUANDO ESTA ROTA É REQUISITADA PELO CLIENTE, SERÁ NECESSÁRIO 
    // ESPERAR A RESPOSTA DO BANCO DE DADOS PARA QUE A EXECUÇÃO DA FUNÇÃO POSSA 
    // PROSSEGUIR, POR ISSO A ADIÇÃO DA PALAVRA ASYNC.
    async function (request, response) {
        // EXECUTA O MÉTODO `get` DO OBJETO DE CONEXÃO COM BANCO DE DADOS `db` E 
        // SEU VALOR DE RETORNO É GUARDADO NA CONSTANTE `responseData`; ESTE 
        // MÉTODO EXECUTA UMA SELEÇÃO NO BANCO DE DADOS E RETORNA UM OBJETO 
        // CONTENDO TODOS OS DADOS DE UMA PESSOA.
        //
        // O PRIMEIRO PARÂMETRO É UM SQL SELECT COM UMA CLÁUSULA WHERE QUE 
        // RETORNARÁ APENAS UM ITEM DA TABELA, O SEGUNDO PARÂMETRO É O VALOR A 
        // SER SUBSTITUÍDO PELA ÂNCORA, AQUI FOI OPTADO POR UTILIZAR ÃNCORAS NÃO
        // NOMEADAS `?` AO INVÉS DE ÃNCORAS NOMEADAS `:` POR TRATAR-SE DE APENAS
        // UM VALOR A SER SUBSTITUÍDO NA STRING SQL DO PRIMEIRO PARÂMETRO.
        const responseData = await db.get("SELECT * FROM pessoa WHERE id=? LIMIT 1", request.params.id);
 
        // VERIFICA SE EXISTE ALGUM VALOR NA CONSTANTE `responseData`, CASO NÃO
        // EXISTA É PORQUE O SELECT NÃO ENCONTROU UMA PESSOA COM O `id` INFORMADO.
        if (responseData == undefined) {
            // CASO O SELECT NÃO RETORNE VALORES, O SERVIDOR RETORNA O `HTTP 
            // STATUS CODE 404` INFORMANDO QUE NÃO FOI ENCONTRADO O DADO 
            // SOLICITADO.
            response.status(404); // Not Found
            // RETORNA NO CORPO DA RESPOSTA UM OBJETO COM A CHAVE `error` QUE 
            // EXPLICA DE FORMA VERBOSA O ERRO OCORRIDO.
            response.json({ error: "Pessoa não encontrada." });
        } 
        
        // CASO CONTRÁRIO: QUANDO `responseData` NÃO FOR INDEFINIDO (VAZIO).
        else {
            // CASO O SELECT EXECUTADO ENCONTRE ALGUM VALOR, O SERVIDOR RETORNA
            // O OBJETO CONTENDO AS INFORMAÇÕES DE PESSOA NO FORMATO JSON, NOTE 
            // QUE NÃO DEFINIMOS O HTTP STATUS CODE, POR PADRÃO O HTTP STATUS 
            // CODE É `200 Ok`.
            response.json(responseData);
        }
    }
);
```
 
#### Função de `alteração no banco` de dados para a rota `PUT /pessoa/:id` do servidor - `app.put('/pessoa/:id', function (request, response) { … }`
 
```typescript
// DEFINE A ROTA `PUT /pessoa/:id`.
app.put('/pessoa/:id', 
    // ADICIONADO A PALAVRA RESERVADA ASYNC ANTES DA DECLARAÇÃO DA FUNÇÃO QUE É 
    // EXECUTADA QUANDO ESTA ROTA É REQUISITADA PELO CLIENTE, SERÁ NECESSÁRIO 
    // ESPERAR A RESPOSTA DO BANCO DE DADOS PARA QUE A EXECUÇÃO DA FUNÇÃO POSSA 
    // PROSSEGUIR, POR ISSO A ADIÇÃO DA PALAVRA ASYNC.
    async function (request, response) {
        // VERIFICA SE NO CORPO DO TEXTO NÃO TEM AS CHAVES `nome`, `sobrenome` E 
        // `apelido`.
        if (!request.body.nome || !request.body.sobrenome || !request.body.apelido) {
            // CASO NÃO EXISTA UMA DAS CHAVES, O SERVIDOR RETORNA O `HTTP STATUS 
            // CODE` `422` QUE INFORMA QUE A ENTIDADE RECEBIDA NÃO PODE SER 
            // PROCESSADA.
            response.status(422); // Unprocessable Entity
            // RETORNA NO CORPO DA RESPOSTA UM OBJETO COM A CHAVE `error` QUE 
            // EXPLICA DE FORMA VERBOSA O ERRO OCORRIDO.
            response.json({ error: "dados incompletos." });
            // PARA A EXECUÇÃO DA FUNÇÃO NESTE MOMENTO, POIS SEM ESSAS 
            // INFORMAÇÕES NÃO HÁ MOTIVOS DE CONTINUAR A EXECUÇÃO.
            return;
        }
 
        // INICIA BLOCO DE TENTATIVA, ISSO SIGNIFICA QUE SE ALGUM DOS COMANDOS 
        // DEFINIDOS DENTRO DELE RETORNAR (throw) A EXECUÇÃO DO BLOCO É 
        // INTERROMPIDO E O FLUXO PASSA PARA O BLOCO `catch` PASSANDO COMO 
        // PARÂMETRO VALOR RETORNADO PELA LINHA QUE APRESENTOU O ERRO.
        try {
            // EXECUTA O MÉTODO `run` DO OBJETO DE CONEXÃO COM BANCO DE DADOS 
            // `db` E O RESULTADO DE SUA EXECUÇÃO É ARMAZENADO NA CONSTANTE 
            // `responseData`; ESTE MÉTODO EXECUTA QUALQUER SQL E RETORNA 
            // INFORMAÇÕES COMO A QUANTIDADE DE LINHAS AFETADAS; 
            //
            // O PRIMEIRO PARÂMETRO É UM SQL DE ATUALIZAÇÃO DE DADOS NA TABELA 
            // `pessoa` (note que os valores não foram adicionados, em seu lugar 
            // foram adicionadas âncoras `:` que serão substituídas pelos valores 
            // no momento da execução, permitindo assim que o método trate 
            // ataques de sql injection) E O SEGUNDO É UM OBJETO COM OS VALORES 
            // A SEREM SUBSTITUÍDOS PELAS ÃNCORAS DA STRING SQL DO PRIMEIRO 
            // PARÂMETRO.
            const responseData = await db.run(
                "UPDATE pessoa SET nome=:nome, sobrenome=:sobrenome, apelido=:apelido WHERE id=:id",
                {
                    ":id": request.params.id,
                    ":nome": request.body.nome,
                    ":sobrenome": request.body.sobrenome,
                    ":apelido": request.body.apelido
                }
            );
 
            // VERIFICA SE EXISTE ALGUM VALOR NA CONSTANTE `responseData`, CASO 
            // NÃO EXISTA É PORQUE O SELECT NÃO ENCONTROU UMA PESSOA COM O `id` 
            // INFORMADO.
            if (responseData == undefined) {
                // CASO O SELECT NÃO RETORNE VALORES, O SERVIDOR RETORNA O `HTTP 
                // STATUS CODE 404` INFORMANDO QUE NÃO FOI ENCONTRADO O DADO 
                // SOLICITADO.
                response.status(404); // Not Found
                // RETORNA NO CORPO DA RESPOSTA UM OBJETO COM A CHAVE `error` 
                // QUE EXPLICA DE FORMA VERBOSA O ERRO OCORRIDO.
                response.json({ error: "Pessoa não encontrada." });
            } 
            
            // CASO CONTRÁRIO: QUANDO `responseData` NÃO FOR INDEFINIDO (VAZIO).
            else {
                // CASO O SELECT EXECUTADO ENCONTRE ALGUM VALOR, O SERVIDOR 
                // RETORNA O OBJETO CONTENDO AS INFORMAÇÕES DE PESSOA NO FORMATO 
                // JSON, NOTE QUE NÃO DEFINIMOS O HTTP STATUS CODE, POR PADRÃO O 
                // HTTP STATUS CODE É `200 Ok`.
                response.json(responseData);
            }
        }
        
        // CASO UM ERRO ACONTEÇA NO BLOCO TRY, O FLUXO DE EXECUÇÃO VEM PARA O
        // BLOCO CATCH RECEBENDO COMO PARÂMETRO O ERRO OCORRIDO
        catch (e) {
            // CASO UM ERRO ACONTEÇA, O SERVIDOR RETORNA O `HTTP STATUS CODE`, 
            // `500` INFORMANDO QUE UM ERRO DE PROGRAMAÇÃO OCORREU.
            response.status(500); // Internal Server Error
            // RETORNA NO CORPO DA RESPOSTA UM OBJETO COM A CHAVE `error` QUE 
            // EXPLICA DE FORMA VERBOSA O ERRO OCORRIDO, E TAMBÉM UMA CHAVE 
            // `detail` QUE RETORNA EXATAMENTE O OBJETO DE ERRO RECEBIDO PELO 
            // BLOCO CATCH.
            response.json({ error: "database error", detail: e });
    }
);
```
 
#### Função de `exclusão no banco de dados` para a rota `DELETE /pessoa/:id` do servidor -  `app.delete('/pessoa/:id', function (request, response) { … }`
 
```typescript
// DEFINE A ROTA `PUT /pessoa/:id`.
app.delete('/pessoa/:id', 
    // ADICIONADO A PALAVRA RESERVADA ASYNC ANTES DA DECLARAÇÃO DA FUNÇÃO QUE É 
    // EXECUTADA QUANDO ESTA ROTA É REQUISITADA PELO CLIENTE, SERÁ NECESSÁRIO 
    // ESPERAR A RESPOSTA DO BANCO DE DADOS PARA QUE A EXECUÇÃO DA FUNÇÃO POSSA 
    // PROSSEGUIR, POR ISSO A ADIÇÃO DA PALAVRA ASYNC.
    async function (request, response) {
        // EXECUTA O MÉTODO `run` DO OBJETO DE CONEXÃO COM BANCO DE DADOS `db` E 
        // O RESULTADO DE SUA EXECUÇÃO É ARMAZENADO NA CONSTANTE `responseData`; 
        // ESTE MÉTODO EXECUTA QUALQUER SQL E RETORNA INFORMAÇÕES COMO A 
        // QUANTIDADE DE LINHAS AFETADAS; 
        //
        // O PRIMEIRO PARÂMETRO É UM SQL SELECT COM UMA CLÁUSULA WHERE QUE 
        // FORÇA A BUSCA DE DADOS DE PESSOA POR ID, FAZENDO COM QUE APENAS UM 
        // ITEM DA TABELA SEJA RETORNADO, O SEGUNDO PARÂMETRO É O VALOR A 
        // SER SUBSTITUÍDO PELA ÂNCORA, AQUI FOI OPTADO POR UTILIZAR ÃNCORAS NÃO
        // NOMEADAS `?` AO INVÉS DE ANCORAS NOMEADAS `:` POR TRATAR-SE DE APENAS
        // UM VALOR A SER SUBSTITUÍDO NA STRING SQL DO PRIMEIRO PARÂMETRO.
        const responseData = await db.run("DELETE FROM pessoa WHERE id=? LIMIT 1", request.params.id);
 
        // VERIFICA A QUANTIDADE DE LINHAS AFETADAS PELO DELETE, CASO O VALOR 
        // SEJA 0 SIGNIFICA QUE NADA FOI EXCLUÍDO
        if(responseData.changes == 0) {
            // CASO O DELETE ALTERE NENHUMA LINHA, O SERVIDOR RETORNA O `HTTP 
            // STATUS CODE 404` INFORMANDO QUE NÃO FOI ENCONTRADO O DADO 
            // SOLICITADO.
            response.status(404); // Not Found
            // RETORNA NO CORPO DA RESPOSTA UM OBJETO COM A CHAVE `error` QUE 
            // EXPLICA DE FORMA VERBOSA O ERRO OCORRIDO.
            response.json({ error: "Pessoa não encontrada." });
        } 
        
        // CASO CONTRÁRIO: QUANDO O NÚMERO DE LINHAS AFETADAS FOR MAIOR QUE 0.
        else {
            // CASO O DELETE ALTERE MAIS QUE 0 LINHAS, O SERVIDOR RETORNA O 
            // OBJETO CONTENDO INFORMAÇÕES COMO O NÚMERO DE LINHAS AFETADAS, 
            // NOTE QUE POR PADRÃO O HTTP STATUS CODE É `200 Ok`, POR ISSO NÃO 
            // FOI PRECISO ALTERAR O HTTP STATUS CODE.
            response.json(responseData);
        }
    }
);
```

#### Resultado final

…

```typescript
import { init as initDatabase } from "./database";
import express from "express";
import bodyParser from "body-parser";

const app = express();

app.use(function (request, response, next) {
    response.header('Access-Control-Allow-Origin', '*');
    response.header('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE');
    response.header('Access-Control-Allow-Headers', 'Content-Type');
    next();
});

app.use(bodyParser.json());

async function init() {
    const db = await initDatabase();

    app.get('/pessoa', async function (request, response) {
        const responseData = await db.all("SELECT * FROM pessoa")
        response.json(responseData);
    });

    app.post('/pessoa', async function (request, response) {
        if (!request.body.nome || !request.body.sobrenome || !request.body.apelido) {
            response.status(422); // Unprocessable Entity
            response.json({ error: "dados incompletos." });
            return;
        }

        try {
            const responseData = await db.run(
                "INSERT INTO pessoa(nome, sobrenome, apelido) VALUES(:nome, :sobrenome, :apelido)",
                {
                    ":nome": request.body.nome,
                    ":sobrenome": request.body.sobrenome,
                    ":apelido": request.body.apelido
                }
            );
            response.json(responseData);
        } catch (e) {
            response.status(500); // Internal Server Error
            response.json({ error: "Erro de Banco de Dados.", detail: e });
        }
    });

    app.get('/pessoa/:id', async function (request, response) {
        const responseData = await db.get("SELECT * FROM pessoa WHERE id=?", request.params.id);
        if (responseData == undefined) {
            response.status(404); // Not Found
            response.json({ error: "Pessoa não encontrada." });
        } else {
            response.json(responseData);
        }
    });

    app.put('/pessoa/:id', async function (request, response) {
        if (!request.body.nome || !request.body.sobrenome || !request.body.apelido) {
            response.status(422); // Unprocessable Entity
            response.json({ error: "dados incompletos." });
            return;
        }

        try {
            const responseData = await db.run(
                "UPDATE pessoa SET nome=:nome, sobrenome=:sobrenome, apelido=:apelido WHERE id=:id",
                {
                    ":id": request.params.id,
                    ":nome": request.body.nome,
                    ":sobrenome": request.body.sobrenome,
                    ":apelido": request.body.apelido
                }
            );

            if(responseData.changes == 0) {
                response.status(404);
                response.json({ error: "pessoa não encontrada" });
            } else {
                response.json(responseData);
            }
        } catch (e) {
            response.status(500); // Internal Server Error
            response.json({ error: "Erro de Banco de Dados.", detail: e });
        }
    });

    app.delete('/pessoa/:id', async function (request, response) {
        const responseData = await db.run("DELETE FROM pessoa WHERE id=?", request.params.id);
        if(responseData.changes == 0) {
            response.status(404);
            response.json({ error: "pessoa não encontrada" });
        } else {
            response.json(responseData);
        }
    });

    app.listen(8081, () => console.log("running..."));
}

init();
```

### Teste final

…

## 2. Cliente - Browser/Navegador

…
