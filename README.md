Table of contents

Dia-a-dia

* [Crie uma tarefa](#markdown-header-crie-uma-tarefa)
* [Iniciar uma tarefa](#markdown-header-iniciar-uma-tarefa)
* [Finalizar tarefa](#markdown-header-finalizar-tarefa)
* [Desfazer 1 commit e refazer!](#markdown-header-desfazer-1-commit-e-refazer)
* [Preciso mudar de branch, e agora?](#markdown-header-preciso-mudar-de-branch-e-agora)

Primeira vez

* [Configuração do git](#markdown-header-configuracao-do-git)
* [Github - Adicionar a chave SSH](#markdown-header-github---adicionar-a-chave-ssh)
* [BitBucket - Adicionar a chave SSH](#markdown-header-bitbucket---adicionar-a-chave-ssh)
* [Configuração do git-town](#markdown-header-configuracao-do-git-town)
* [Instalação](#markdown-header-instalacao)

Alguns comandos abaixo não são padrão do git. Ver <http://www.git-town.com/>.

## Crie uma tarefa

Para criar uma tarefa (ou bug) basta clicar em **Incidentes** > **Criar incidente**.

Descreva a tarefa e depois de salvar um número será gerado. Utilize essa referência como nome do branch no qual você irá trabalhar (por exemplo issue \#1).

## Iniciar uma tarefa

Sempre crie um branch para cada tarefa.

```
git checkout master
git hack issue-1
```

Começe a trabalhar normalmente.

## Finalizar tarefa

Faça o commit das alterações em seu branch. Uma alguma ferramenta de commit para te auxiliar e evitar commit de arquivos desnecessários.

* Eclipse: <https://www.eclipse.org/egit/documentation/>
* Linux: gitg - `apt-get install gitg`
* NetBeans já tem suporte por padrão

Exemplo:

```
Resolução da tarefa CRUD pessoa.

Fixed #1.
```

A ideia é escrever o commit da seguinte forma:

```
[título - até 80 caracteres]

[descrição detalhada se for preciso]

Fixed #[número da issue]
```

Em seguida crie um Pull Request:

```
git new-pull-request
```

Depois que o Pull Request for aceito você pode apagar seu branch:

```
git checkout master
git branch -d issue-1
```

## Desfazer 1 commit e refazer!

Caso você tenha feito um commit mas viu que fez coisa errada siga o procedimento
abaixo:

~~~
git reset --soft HEAD^
~~~

Isso vai fazer com que o último commit seja apagado. Faça as alterações necessárias
e execute o comando abaixo para recuperar a mensagem de commit, caso necessário:

~~~
git show ORIG_HEAD
~~~

Volte ao gitg para finalizar o processo.

## Preciso mudar de branch, e agora?

**Antes de tudo faça commit das alterações do seu branch**.

Em seguida volte ao branch `master` e crie outro branch baseado nele (`master`).

```
git checkout master
git hack tarefa-rapida
```

Resolva o problema e faça o mesmo descrito na seção **Finalizar tarefa**.

Volte ao seu branch `tarefa-1` e faça o merge com as alterações se necessário.

```
git checkout tarefa-1
git sync
```

Um arquivo será aberto mostrando os commits que entrarão no merge. Basta salvar e sair.

## Configuração do git

Instalação: `sudo apt-get install git gitg`

Configuração inicial:

~~~
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR EMAIL ADDRESS"
~~~

Gere uma chave para fazer operações através do SSH:

~~~
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
~~~

Siga os passos e por fim digite uma senha para a chave.

Adicione sua chave ao agente SSH:

~~~
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
~~~

### Github - Adicionar a chave SSH

Acesse a página para adicionar sua chave SSH: <https://github.com/settings/keys>

Clique no botão ["New SSH key"](https://github.com/settings/ssh/new "New SSH key")

Copie o conteúdo do arquivo `~/.ssh/id_rsa.pub` para o campo Key. Se preferir, dê um nome para sua chave.

### BitBucket - Adicionar a chave SSH

Acesse a página para adicionar sua chave SSH: <https://bitbucket.org/account/settings/ssh-keys/>

Clique no botão "Add Key" e copie o conteúdo do arquivo `~/.ssh/id_rsa.pub` para o campo Key. Se preferir, dê um nome para sua chave.

## Configuração do git-town

O [git-town](http://www.git-town.com/) adiciona comandos ao git para facilitar nossa vida.

### Instalação

Baixe o projeto e o coloque no diretório adequado:

~~~
git clone https://github.com/Originate/git-town.git /tmp/git-town
sudo mv /tmp/git-town /usr/local
~~~

Edite o arquivo `~/.profile` e adicione o conteúdo abaixo ao final.

~~~
export PATH=/usr/local/git-town/src/:$PATH
export MANPATH=/usr/local/git-town/man/:$MANPATH
~~~
