---
tags: git, módulo, módulo parcial
---

# Introdução

Este tutorial ira demonstrar como utilizar submódulos com git, tornando possível utilizar outro repositório dentro do seu repositório principal e configurá-lo para considerar apenas algumas pastas no checkout.


# 1. Criando submódulo em seu repositório GIT

Dentro da árvore de trabalho do seu repositório GIT, abra a pasta onde você deseja iniciar seu submódulo GIT e entre com o seguinte comando:

    git submodule add git://some.url/of/repo.git **NOME-DO-MODULO**


# 2. Criado submódulo com checkout parcial

Isso fará o clone do repositório como um submódulo em sua árvore de trabalho atual, para criar um clone parcial vá até a pasta raiz da sua árvore de trabalho e abra .git/modules/**NOME-DO-MODULO**/info/ e crie um arquivo chamado **sparse-checkout** e neste arquivo adicione as únicas pastas que você deseja que seja copiada do módulo, por exemplo:

    pasta-do-repositório/
	outra-pasta-do-repositório/subpasta
		
Agora habilite o **sparse checkout**. Na pasta raiz do módulo digite:

    git config core.sparsecheckout true
	
Para finalizar aplique os filtros que você criou, com o seguinte comando na raiz do módulo:

    git read-tree -mu HEAD


# 3. Atualizar módulos 

## 3.1. Atualizar um único módulo do projeto

Cada módulo é um repositório normal do git, isso significa se estiver na raiz do módulo, você será capaz de executar:

    git pull

## 3.2. Atualizando todos os módulos do projeto

Para atualizar todos os módulos do projeto de uma só vez, execute o seguinte comando na raiz de seu projeto:

    git submodule foreach git pull origin master
