# Indrocução

O propósito deste tútorial é criar uma instalação portável para desenvolvimento com Flutter.

# 1 - Download das Ferramentas

Todos os downloads não devem ser feitos das versões de instalação e sim das verões compactadas (zip).

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

Na próxima página um download da versão instalavel iniciará automaticamente, cancele esta ação pois é preciso baixar a versão portátil da aplicação.
---

### 1.3.2 - Download, GitSCM - Passo 2

Clique no link de download para a versão portatil da aplicação:

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

Descompacte os arquivos com sua ferramenta de extração favorita ou utilize o extrator do windows, o único arquivo que não será necessário utilizar uma ferramente para descompactação é o **PortableGit-\*.7z.exe** que já é um arquivo auto extrator.

## 2.2 - Renomenado as pastas

Após a descompactação você deve ter uma pasta com as seguintes sub-pastas:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/uncompress-files-a.png?raw=true)

para fácilitar o processo vamos renomear as pastas conforme a tabela a seguir:

| Renomear de:                                                     | Para:         |
| ---------------------------------------------------------------- | ------------- |
| flutter                                                          |               |
| commandlinetools-win-6200805_latest                              | android-sdk   |
| java-1.8.0-openjdk-1.8.0.242-1.b08.ojdkbuild.windows.x86_64      | jdk           |
| PortableGit                                                      | gitscm        |
| VSCode-win32-x64-1.44.0                                          | vscode        |

**Opcionalmente é possível escluir os arquivos compactados deixando somente as pastas das aplicações**, ao término deste processo a estrutura de pastas devem estar como a imagem a seguir:

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/a.png?raw=true)

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/b.png?raw=true)

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/c.png?raw=true)

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/d.png?raw=true)

![](https://github.com/drachehavoc/tuto/blob/master/Flutter%20(standalone)%20Sem%20Android%20Studio/e.png?raw=true)
