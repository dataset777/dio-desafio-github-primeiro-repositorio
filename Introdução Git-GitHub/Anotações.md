# Git / GitHub

[Link para Download do Git](https://git-scm.com/downloads)

> O Git Bash é um terminal extendido para otimizar o uso do Git.

## Anotações das Aulas:

----------------------------------------------------------------

No GitBash, digitar:

#### Criação de Par de Chaves (Pública / Privada)

````mgmac@DESKTOP-DQS3JQO MINGW64 ~/.ssh
$ ssh-keygen -t ed25519 -C mg.macedo@live.com

Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/Users/mgmac/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/mgmac/.ssh/id_ed25519
Your public key has been saved in /c/Users/mgmac/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:NIyKZ58VZKzyEqhaIEqXfjfXPWmIrsID9DvmMdtRka4 mg.macedo@live.com
The key's randomart image is:
+--[ED25519 256]--+
|       .o        |
|       =. .      |
|   .. ..=o       |
|o..=o....o.      |
|+o= =+  Soo o .  |
|o .=.+.=oo o =   |
|..  ++=E+   . .  |
|.    B= ..       |
|    oo+o.        |
+----[SHA256]-----

````
#### Verificando par de chaves criadas
````
mgmac@DESKTOP-DQS3JQO MINGW64 ~/.ssh
$ ll
total 3
-rw-r--r-- 1 mgmac 197609 464 Feb 22 20:07 id_ed25519
-rw-r--r-- 1 mgmac 197609 100 Feb 22 20:07 id_ed25519.pub
-rw-r--r-- 1 mgmac 197609  92 Feb 22 19:44 known_hosts
````

#### On c:\users\mgmac\.ssh\, do:
````cat id_ed25519.pub
#Chave pública, utilizada no GitHub (Seção: SSH and GPG keys)
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIK2ElgrXWNXMGfUh6qqaUTfAUSEQGwUJIEtYh/Ll0xVc mg.macedo@live.com
````


#### Inicializar git agent
On Linux environment: WSL 2 (Ubuntu)
````eval $(ssh-agent -s)
Agent pid xxxx
````
````
mgmac@DESKTOP-DQS3JQO MINGW64 ~/.ssh
$ ssh-add id_ed25519
Enter passphrase for id_ed25519:
Identity added: id_ed25519 (mg.macedo@live.com)
````

#### Criar Pasta para clonar projeto
````
mgmac@DESKTOP-DQS3JQO MINGW64 ~
$ cd /c/Workspace/ssh-test/
````

#### Clonar projeto (Buscar link SSH, NÃO HTTP)
````
mgmac@DESKTOP-DQS3JQO MINGW64 /c/Workspace/ssh-test
$ git clone git@github.com:htop-dev/htop.git
Cloning into 'htop'...
remote: Enumerating objects: 15981, done.
remote: Counting objects: 100% (183/183), done.
remote: Compressing objects: 100% (142/142), done.
remote: Total 15981 (delta 109), reused 58 (delta 41), pack-reused 15798
Receiving objects: 100% (15981/15981), 5.09 MiB | 293.00 KiB/s, done.
Resolving deltas: 100% (12377/12377), done.
````

#### Criar diretório para novo repositório

$ mkdir diretorio
* Iniciar Git				   : git init
* Configurar Email			   : $ git config --global user.email "mg.macedo@live.com"
* Configurar Usuário		   : $ git config --global user.name dataset777
* Iniciar Versionamento		   : git add * (* inclui todos os arquivos não commitados)

* Criar commit				   : git commit -m "commit inicial"
* Verificar Status dos Arquivos: git status

#### Tipos de arquivos:
Tracked: Git possui ciência dos arquivos
Untracked: arquivo fora do Git

#### Estágios:
Untracked / Tracked (Unmodified / Modified / Staged)
Unmodified: arquivo não modificado
Modified: arquivo modificado
Staged: arquivo preparado para commit

#### Ciclo entre os estágios:
`git add` (1): adiciona arquivo "untracked"
arquivo modificado
`git add` (2): modifica arquivo para estado "staged"
git commit: arquivo volta para Unmodified - Cria "snapshot", uma "foto"

#### Estrutura repositórios:
Conforme arquivos vão sendo modificados, estes estão constantemente
mudando seu local na estrutura, de working directory para staging area e vice-versa
repositório local está lotado de commits

#### Quando um arquivo ou diretório é criado/modificado:
````
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    Receita1.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        receitas/

no changes added to commit (use "git add" and/or "git commit -a")
````

#### Após modificações (arquivos, diretórios), realizar novo git add:

````
mgmac@DESKTOP-DQS3JQO MINGW64 /c/Workspace/livro-receitas (master)
$ git add Receita1.md receitas/
warning: LF will be replaced by CRLF in receitas/Receita1.md.
The file will have its original line endings in your working directory

mgmac@DESKTOP-DQS3JQO MINGW64 /c/Workspace/livro-receitas (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    Receita1.md -> receitas/Receita1.md

mgmac@DESKTOP-DQS3JQO MINGW64 /c/Workspace/livro-receitas (master)
$ git commit -m "cria pasta receitas, move arquivo para receitas"
[master 20595e8] cria pasta receitas, move arquivo para receitas
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename Receita1.md => receitas/Receita1.md (100%)
````

#### Exemplos:
arquivo1 -> git add arquivo1; diretorio1/ -> git add diretorio1
git status
arquivo2 -> git add arquivo2; diretorio2/ -> git add diretorio2
git status

#### Verificar configurações gerais:
`git config --list`

#### Modificar email e usuário:
````
git config --global --unset user.email
git config --global --unset user.name
````

#### Ligando repositório local com repositório GitHub
Entrar no perfil e criar novo repositório
"Empurrar" a versão do repositório local para o repositório no GitHub

````
mgmac@DESKTOP-DQS3JQO MINGW64 /c/Workspace/livro-receitas (master)
$ git remote add origin git@github.com:dataset777/livro-receitas.git

mgmac@DESKTOP-DQS3JQO MINGW64 /c/Workspace/livro-receitas (master)
$ git remote -v
origin  git@github.com:dataset777/livro-receitas.git (fetch)
origin  git@github.com:dataset777/livro-receitas.git (push)

mgmac@DESKTOP-DQS3JQO MINGW64 /c/Workspace/livro-receitas (master)
$ git push origin master
Enter passphrase for key '/c/Users/mgmac/.ssh/id_ed25519':
Enumerating objects: 8, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 8 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (8/8), 770 bytes | 36.00 KiB/s, done.
Total 8 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:dataset777/livro-receitas.git
 * [new branch]      master -> master
````

#### Resolução de Problemas (versões diferentes do código em diferentes máquinas)
-  "Puxar" versão atualizada do repositório online:
````
mgmac@DESKTOP-DQS3JQO MINGW64 /c/Workspace/livro-receitas (master)
$ git pull origin master
Enter passphrase for key '/c/Users/mgmac/.ssh/id_ed25519':
From github.com:dataset777/livro-receitas
 * branch            master     -> FETCH_HEAD
Already up to date.
````


-  Realizar modificações necessárias, "commitar" e "empurrar" para o repositório online:
````
git commit -m "resolve conflitos"

git push origin master
````


-----------------------------------------------------------------


#### Seção: Criando seu Primeiro Repositório no GitHub Para Compartilhar Seu Progresso
##### Passos: Criação / Atualização / Sincronização
##### Criar Repositório no GitHub, editar README.md

##### Clonar repositório online
````
mgmac@DESKTOP-DQS3JQO MINGW64 /c/Workspace/DIO
$ git clone https://github.com/dataset777/dio-desafio-github-primeiro-repositorio.git
Cloning into 'dio-desafio-github-primeiro-repositorio'...
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 9 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (9/9), done.
````

##### Verificando status
````
mgmac@DESKTOP-DQS3JQO MINGW64 /c/Workspace/DIO/dio-desafio-github-primeiro-repositorio (main)
$ git status
On branch main
Your branch is up to date with 'origin/main'.
nothing to commit, working tree clean
````

##### Após criação da pasta *Introdução ao GitHub* e do texto *Anotações.md*, o status será o seguinte:
````
mgmac@DESKTOP-DQS3JQO MINGW64 /c/Workspace/DIO/dio-desafio-github-primeiro-repositorio (main)
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        "Introdu\303\247\303\243o Git-GitHub/"

nothing added to commit but untracked files present (use "git add" to track)
````




