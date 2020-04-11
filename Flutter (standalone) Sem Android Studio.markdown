# Introdução

O propósito deste tutorial é criar uma instalação portável para desenvolvimento com Flutter.

# 1 - Download das Ferramentas

Todos os downloads não devem ser feitos das versões de instalação e sim das versões compactadas (zip).

## 1.1 - Download, Java JDK (ODK):

Acesse [https://github.com/ojdkbuild/ojdkbuild](https://github.com/ojdkbuild/ojdkbuild) e clique no link conforme a imagem:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/download-odk.png?raw=true)
  
## 1.2 - Download, Flutter

### 1.2.1 - Download, Flutter - Passo 1

Acesse [https://flutter.dev/](https://flutter.dev/) e clique em **get started**:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/download-flutter-1.png?raw=true)

### 1.2.2 - Download, Flutter - Passo 2

Na página seguinte role até encontrar o botão de download para windows:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/download-flutter-2.png?raw=true)

### 1.2.3 - Download, Flutter - Passo 3

Na próxima página encontre o botão de download do Flutter, clique e aguarde o download iniciar:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/download-flutter-3.png?raw=true)
  
## 1.3 - Download, GitSCM

### 1.3.1 - Download, GitSCM - Passo 1

Acesse [https://git-scm.com/](https://git-scm.com/) e clique no botão de download:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/download-gitscm-1.png?raw=true)
  
---
**ATENÇÃO**

Na próxima página um download da versão instalável iniciará automaticamente, cancele esta ação pois é preciso baixar a versão portátil da aplicação.
---

### 1.3.2 - Download, GitSCM - Passo 2

Clique no link de download para a versão portátil da aplicação:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/download-gitscm-2.png?raw=true)
  
## 1.4 - Download, Android SDK (commandlinetools-win - sem android studio)
 
### 1.4.1 - Download, Android SDK - Passo 1

Acesse [https://developer.android.com/studio](https://developer.android.com/studio) e clique em **DOWNLOAD OPTIONS**:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/download-androidsdk-1.png?raw=true)

### 1.4.2 - Download, Android SDK - Passo 2

Na página seguinte, role a página até encontrar o item **Command Line Tools Only**, e encontrei o link para download para windows:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/download-androidsdk-2.png?raw=true)

### 1.4.3 - Download, Android SDK - Passo 3

Aceite os ** termos e condições de uso** e clique em **fazer download de android command line tools para windows** e aguarde o download iniciar:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/download-androidsdk-3.png?raw=true)

## 1.5 - Download, Visual Studio Code (VSCode)

### 1.5.1 - Download, Visual Studio Code - Passo 1

Acesse [https://code.visualstudio.com/](https://code.visualstudio.com/) e clique na seta para baixo que fica ao lado do botão de download, em seguida clique em **Other downloads**:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/download-vscode-1.png?raw=true)
 
### 1.5.2 - Download, Visual Studio Code - Passo 2

Na próxima página encontre a versão portátil para download:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/download-vscode-2.png?raw=true)

# 2 - Descompactação das Ferramentas

Certifique-se que todos os arquivos foram baixados, corretamente:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/uncompress-files-list.png?raw=true)

## 2.1 - Descompactação das Ferramentas

Descompacte os arquivos com sua ferramenta de extração favorita 7-Zip, WinRar, Winzip, mas não utilize o extrator do windows pois alguns arquivos são corrompidos; O único arquivo que não será necessário utilizar uma ferramenta para descompactação é o **PortableGit-\*.7z.exe** pois ele tem um extrator embutido, apenas de dois cliques e escolha a pasta e clique em ok.

## 2.2 - Renomeando as pastas

Após a descompactação você deve ter uma pasta com as seguintes subpastas:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/uncompress-files-a.png?raw=true)

para facilitar o processo vamos renomear as pastas conforme a tabela a seguir:

| Renomear de:                                                     | Para:         |
| ---------------------------------------------------------------- | ------------- |
| flutter                                                          |               |
| commandlinetools-win-6200805_latest                              | android-sdk   |
| java-1.8.0-openjdk-1.8.0.242-1.b08.ojdkbuild.windows.x86_64      | jdk           |
| PortableGit                                                      | gitscm        |
| VSCode-win32-x64-1.44.0                                          | vscode        |

**Opcionalmente é possível excluir os arquivos compactados deixando somente as pastas das aplicações**, ao término deste processo a estrutura de pastas devem estar como a imagem a seguir:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/a.png?raw=true)

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/b.png?raw=true)

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/c.png?raw=true)

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/d.png?raw=true)

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/e.png?raw=true)

# 3 Arquivo de Configuração de Ambiente

Crie um arquivo chamado **run.cmd** e abra em seu editor de texto/ide favorito.

Para prosseguir é preciso compreensão do que são variáveis de ambiente, caso não saiba sobre o que se tratam sugiro uma pesquisa na internet acerca do assunto, também é interessante entender como a variável de ambiente **PAT** funciona, segue uma breve descrição:

_A variável path contém uma lista de pastas separadas por _;_, ela serve para dizer para o ambiente onde encontrar os arquivos a serem executados._

Como dito anteriormente, talvez seja interessante uma pesquisa mais aprofundada sobre o funcionamento da variável de ambiente **PATH**.

Na primeira linha de nosso arquivo vamos adicionar o seguinte trecho de código ```@ECHO OFF```, para que não sejam impressos no terminal as instruções que iremos adicionar no arquivo.

## 3.1 - Variáveis Comuns

No arquivo **run.cmd** crie as seguintes variáveis, **APP_ROOT**, para armazenar o caminho raiz de nosso ambiente e **APP_DATA**, para armazenar o caminho onde serão salvos os dados de nosso ambiente portátil:

```bat
SET APP_ROOT=%~dp0
SET APP_DATA=%APP_ROOT%\.appdata
```

## 3.2 - Configuração, JDK (ODK)

No arquivo vamos adicionar a variável **JAVA_HOME**, que serve para apontar onde está a pasta raiz do JDK e também vamos adicionar na variável **PATH** onde estão os arquivos _executáveis_ do Java:

```bat
SET JAVA_HOME=%APP_ROOT%jdk
SET PATH=%JAVA_HOME%\bin;%PATH%
```

## 3.3 - Configuração, Flutter

Para configurar Flutter tudo que é preciso fazer é adicionar a sua pasta **bin** na lista de pastas da variável de ambiente **PATH**:

```bat
SET PATH=%APP_ROOT%flutter\bin;%PATH%
```

## 3.4 - Configuração, GitSCM

Assim como o Flutter, para configurar o GitSCM é necessário adicionar a pasta **bin** na lista de pastas da variável de ambiente **PATH**, porém é necessário adicionar também a pasta **mingw64\bin**:

```bat
SET PATH=%APP_ROOT%gitscm\bin;%PATH%
SET PATH=%APP_ROOT%gitscm\mingw64\bin;%PATH%
```

## 3.5 - Configuração, Android SDK

_Para configurar o Android SDK, vamos apontar para pastas que ainda não existem, pois ainda não foi executado o passo onde os dowloads das ferramentas serão feitos, mas isso não será um problema._

Para o Android SDK é necessário criar a várivael de ambiente **ANDROID_SDK_ROOT** que serve para indicar em que pasta o Android SDK esta descompactado, também é necessário adicionar duas pastas ao **PATH**, **platform-tools**, **cmdline-tools\latest\bin**:

---
**ERRO DA VERSÃO DO FLUTTER**

por conta de um erro da versão atual do flutter precisaremos também adicionar **tools\bin** ao **PATH**.
---

```bat
SET ANDROID_SDK_ROOT=%SOFTWARES_HOME%\android-sdk
SET PATH=%ANDROID_SDK_ROOT%\tools\bin;%PATH%
SET PATH=%ANDROID_SDK_ROOT%\platform-tools;%PATH%
SET PATH=%ANDROID_SDK_ROOT%\cmdline-tools\latest\bin;%PATH%
```

## 3.6 - Configuração, Visual Studio Code (VSCode)

Por último precisamos configurar as variáveis de ambiente para o VSCode, porém temos que garantir que o VSCode irá funcionar de forma portátil, por isso é preciso configurar as sguintes váriaveis **VSCODE_EXTENSIONS**, responsável por onde as extensões do VSCode são salvas; **VSCODE_APPDATA**, responsável por informar onde serão salvos os dados pessoais do usuário, como preferência de cores, tamanho de fonte etc; **VSCODE_LOGS**, responsável por informar onde serão salvos os logs do VSCode.

Além das variáveis que farão com que o VSCode funcione de maneira portátil, também é preciso adicionar a pasta **bin** do VSCode ao **PATH**.

```bat
SET VSCODE_EXTENSIONS=%APP_DATA%\vscode\extentions
SET VSCODE_APPDATA=%APP_DATA%\vscode\data
SET VSCODE_LOGS=%APP_DATA%\vscode\logs
SET PATH=%APP_ROOT%\vscode\bin;%PATH%
```
## 3.6 - Configuração, Terminal

Por último será adicionado a seguinte instrução ```CMD /K```, para que o terminal fique livre para executarmos os próximos passos.

## 3.7 - Configuração, Finalmente

Após tudo pronto o arquivo deve se parecer com o seguinte:

```bat
@ECHO OFF

::
:: VARIÁVEIS COMUNS
::

SET APP_ROOT=%~dp0
SET APP_DATA=%APP_ROOT%.appdata

::
:: JAVA
::

SET JAVA_HOME=%APP_ROOT%jdk
SET PATH=%JAVA_HOME%\bin;%PATH%

::
:: FLUTTER
::

SET PATH=%APP_ROOT%flutter\bin;%PATH%

::
:: GitSCM
::

SET PATH=%APP_ROOT%gitscm\bin;%PATH%
SET PATH=%APP_ROOT%gitscm\mingw64\bin;%PATH%

::
::  ANDROID SDK
::

SET ANDROID_SDK_ROOT=%APP_ROOT%\android-sdk
SET PATH=%ANDROID_SDK_ROOT%\tools\bin;%PATH%
SET PATH=%ANDROID_SDK_ROOT%\platform-tools;%PATH%
SET PATH=%ANDROID_SDK_ROOT%\cmdline-tools\latest\bin;%PATH%

::
:: VSCode
::

SET VSCODE_EXTENSIONS=%APP_DATA%\vscode\extentions
SET VSCODE_APPDATA=%APP_DATA%\vscode\data
SET VSCODE_LOGS=%APP_DATA%\vscode\logs
SET PATH=%APP_ROOT%\vscode\bin;%PATH%

::
:: Terminal
::

CMD /K
```

# 4 Instalação 

## 4.1 - Instalação, Android SDK


