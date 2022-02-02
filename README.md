# git-tutorial

* [Configure](#configure)
    * [Alias](#alias)
* [Crie repositórios](#crie-repositórios)
    * [Adicionando um novo repo](#adicionando-um-novo-repo)
* [Ignorando arquivos](#ignorando-arquivos)
* [Faça mudanças](#faça-mudanças)
* [Branchs](#branchs)
    * [Resumo de branchs](#resumo-de-branchs)
    * [Resumo: Manipulando branchs para trabalho em equipe](#resumo-manipulando-branchs-para-trabalho-em-equipe)
* [Fechando Issues com commit](#fechando-issues-com-commit)
* [Refatore nomes dos arquivos](#refatore-nomes-dos-arquivos)
* [Salve fragmentos](#salve-fragmentos)
* [Revise histórico](#revise-histórico)
* [Desfaça commits](#desfaça-commits)
* [Sincronize mudanças](#sincronize-mudanças)
* [Sincronizando Fork](#sincronizando-fork)
* [Recuperando um commit](#recuperando-um-commit)
* [Anotações de Danilo Bellini](#anotações-adicionais-de-danilo-bellini)
* [Adicional: gitlab-cli e bitbucket-cli](#adicional)


## Primeiro comando

```
git --help
git help -a
```

## git-cheat-sheet

https://education.github.com/git-cheat-sheet-education.pdf

http://onlywei.github.io/explain-git-with-d3/#

## Configure

Configura o nome que você quer ligado as suas transações de commit.

`git config --global user.name "seu_nome"`

Configura o email que você quer ligado as suas transações de commit.

`git config --global user.email "seu_email"`

Configura cores automaticamente.

`git config --global color.ui auto`

Listando suas configurações.

`git config --list`

git config --global user.name "rg3915"
git config --global user.email "******@yahoo"

### Alias

Renomear comandos do git

```
git config --global alias.ch checkout
git config --global alias.br branch
git config --global alias.co commit
git config --global alias.st status
```


## Crie repositórios

Cria um novo repositório local com um nome específico.

`git init [nome-do-projeto]`

Baixa um projeto e seu histórico de versão inteiro.

`git clone [url]`


### Adicionando um novo repo

```
git remote add origin git@github.com:rg3915/estoque.git
```

Criando um repo localmente

```
git remote add origin ~/t/repo/
```

Mostrando os últimos commits e suas alterações.

```
git show
```


## Ignorando arquivos

Exclua arquivos e diretórios temporários.

Um arquivo de texto chamado `.gitignore` suprime o versionamento acidental de arquivos e diretórios correspondentes aos padrões especificados.


```
*.log
build/
temp-*
env
.env
venv
venv/
*.sqlite3
```

Lista todos os arquivos ignorados neste projeto.

`git ls-files --other --ignored --exclude-standard`


Leia [gitignore.io](https://www.gitignore.io/) sobre quais arquivos devem ser ignorados para cada tipo de projeto, dependendo da linguagem de programação utilizada.

Veja meu [.gitignore](https://github.com/rg3915/estoque/blob/master/.gitignore) para Python.

Também não devem ser versionados:

```
/media  # upload de arquivos
.idea
.vscode
```


## Faça mudanças

Lista todos os arquivos novos ou modificados para serem commitados.

`git status`

Mostra diferenças no arquivo que não foram realizadas.

`git diff`

Faz o snapshot de um arquivo na preparação para versionamento.

`git add [arquivo]`

Mostra a diferença entre arquivos selecionados e as suas últimas versões.

`git diff --staged`

Deseleciona o arquivo, mas preserva seu conteúdo.

`git reset [arquivo]`

Grava o snapshot permanentemente do arquivo no histórico de versão.

`git commit -m "[mensagem descritiva]"`




## Branchs

Lista todos os branches locais no repositório atual.

`git branch`

Cria uma nova branch.

`git branch [nome-da-branch]` ou `git checkout -b [nome-da-branch]`

Muda para a branch específica e atualiza o diretório de trabalho.

`git checkout [nome-da-branch]`

Combina o histórico da branch específica com a branch atual.

`git merge [branch]`

Deleta a branch específica.

`git branch -D [nome-da-branch]`


### Resumo de branchs

```
git branch -r                           # Lista todas as branchs remotas
git branch gh-pages origin/gh-pages     # Cria uma branch local a partir da branch remota
git checkout gh-pages                   # Alterna para a branch especificada
git branch                              # Lista todas as branchs locais
git fetch origin                        # Atualiza a branch local com os dados da branch remota
```


### Resumo: Manipulando branchs para trabalho em equipe

```
git checkout -b new-branch  # cria nova branch
# Faça suas alterações...
git status
git add .
git commit -m 'Fix mensagem sobre suas alterações. Close #1'
```

Caso você precise atualizar sua branch com o que tem na master, leia *Atualizando sua branch* logo abaixo.

#### Atualizando a master

```
git checkout master
git merge mybranch
git branch
git pull
```

#### Atualizando sua branch

Caso ainda esteja trabalhando na sua branch, você precisa atualizá-la com a master.

```
git checkout master
git pull
git checkout mybranch
git merge master
```




### Fechando Issues com commit

```
# Fecha a Issue 1 do repositório.
git commit -m 'Fix mensagem sobre suas alterações. Close #1'
```

[Opções disponíveis para o GitHub](https://help.github.com/pt/github/managing-your-work-on-github/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword)

* `close`, `closes`, `closed`
* `fix`, `fixes`, `fixed`
* `resolve`, `resolve`, `resolved`

[Opções disponíveis para o GitLab](https://docs.gitlab.com/ee/user/project/issues/managing_issues.html#default-closing-pattern)

* `Close`, `Closes`, `Closed`, `Closing`, `close`, `closes`, `closed`, `closing`
* `Fix`, `Fixes`, `Fixed`, `Fixing`, `fix`, `fixes`, `fixed`, `fixing`
* `Resolve`, `Resolves`, `Resolved`, `Resolving`, `resolve`, `resolves`, `resolved`, `resolving`
* `Implement`, `Implements`, `Implemented`, `Implementing`, `implement`, `implements`, `implemented`, `implementing`

[Opções disponíveis para o Bitbucket](https://confluence.atlassian.com/bitbucket/resolve-issues-automatically-when-users-push-code-221451126.html)

* `close`, `closes`, `closed`, `closing`, `fix`, `fixed`, `fixes`, `fixing`, `resolve`, `resolves`, `resolved`, `resolving`
* `reopen`, `reopens`, `reopening`
* `hold`, `holds`, `holding`
* `wontfix`
* `invalidate`, `invalidates`, `invalidated`, `invalidating`
* `addresses`, `re`, `references`, `ref`, `refs`, `see`


## Refatore nomes dos arquivos

Remove o arquivo do diretório de trabalho e seleciona para remoção.

`git rm [arquivo]`

Remove o arquivo do controle de versão mas preserva o arquivo localmente.

`git rm --cached [arquivo]`

Muda o nome do arquivo e o seleciona para o convite.

`git mv [arquivo-original] [arquivo-renomeado]`



## Salve fragmentos

Armazena temporariamente todos os arquivos rastreados modificados.

`git stash`

Restaura os arquivos recentes em stash.

`git stash pop`

Lista todos os conjuntos de alterações em stash.

`git stash list`

Descarta os conjuntos de alterações mais recentes em stash.

`git stash drop`


## Revise histórico

Lista o histórico de versões para o branch atual.

`git log`

Lista o histórico de versões para um arquivo incluindo mudança de nome.

`git log --follow [arquivo]`

Mostra a diferença de conteúdo entre duas branchs.

`git diff [primeiro-branch]...[segundo-branch]`

Retorna mudanças de metadata e conteúdo para o commit específico.

`git show [commit]`

## Desfaça commits

Desfaz todos os commits depois de commit preservando mudanças.

`git reset [commit]`

Descarta todo histórico e mudanças para o commit específico.

`git reset --hard [commit]`


## Sincronize mudanças

Baixe todo o histórico de um marcador de repositório.

`git fetch [marcador]`

Combina o marcador do branch no branch local.

`git merge [marcador]/[branch]`

Envia todos os commits do branch local para o Github.

`git push [alias][branch]`

Baixa o histórico e incorporar as mudanças.

`git pull`



## Sincronizando Fork


Como sincronizar o seu Fork com o repo principal

* Adicione um remote que aponte para o repositório de origem com o comando:

```
git remote add upstream https://github.com/rg3915/estoque.git
```

* Agora você vai ter um remote chamado origin e o recém adicionado upstream. Para conferir digite

```
git remote -v
```

* Com o comando a seguir baixe as alterações do remote upstream.

```
git fetch upstream
```

* Vá para a branch master.

```
git checkout master
```

* Faça o merge da branch master com upstream no seu repositório local.

```
git merge upstream/master
```

* Envie suas alterações para o seu repositório.

```
git push
```

**Referências:**

[Configuring a remote for a fork](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/configuring-a-remote-for-a-fork)

[Syncing a fork](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork)



### Vendo o conteúdo que foi alterado

```
git blame file.txt
```

### Recuperando um commit

```
git reset 7d820c5
```

Atualizar arquivos novos do repo original

```
git fetch repo
```

## Resolvendo conflitos

Manualmente :/


# Anotações adicionais de Danilo Bellini

https://github.com/danilobellini/git-tutorial-br

`git checkout origin/newbranch`

`git log -1`

`git show origin/newbranch`

`git tag v1`

`git log -n 20 --oneline --graph --decorate=false`

`git log --oneline --follow setup.py`

`git blame`



### Ex 6.

```
git log -1 --reverse --format=%p

git log --format='%h %p' | awk '{print length($0), $0}' | sort -rn

```

### Branch

```
git merge C5 C6

n=C0; touch $n.txt; git add $n.txt; git commit -m $n
n=C1; touch $n.txt; git add $n.txt; git commit -m $n
n=C2; touch $n.txt; git add $n.txt; git commit -m $n
n=C3; touch $n.txt; git add $n.txt; git commit -m $n

git checkout -b new-branch

n=C5; touch $n.txt; git add $n.txt; git commit -m $n

git log --oneline --all --grep C3

git checkout -b abc 462144b

git log --oneline --all --grep C1

git checkout 76d59bb

n=C8; touch $n.txt; git add $n.txt; git commit -m $n

git tag azul

n=C9; touch $n.txt; git add $n.txt; git commit -m $n
n=C10; touch $n.txt; git add $n.txt; git commit -m $n

git merge abc new-branch

git tag triplo

git checkout master

git merge new-branch

git tag azul -f

git tag triplo -d

git reflog

git tag undelete 1a5ba9c

```

```
# Apagar do servidor
git push --delete origin features
```

### Ex. branch

```
g ch -b b1
n=a; touch $n.py; git add $n.py -m ${n^}; git commit -m $n

cria_commit() {
  printf "%s\n" '#!/usr/bin/env python' \
                "print('$1')" \
         > "$1".py
  chmod +x "$1".py
  git add "$1".py
  git commit -m "${1^}.py"
}

for n in A B C @ L M; do cria_commit $n; done

g log --oneline --graph --all

g ch -b b2 c457f81 # C

for n in F D G H; do cria_commit $n; done

g log --oneline --graph --all

g ch -b b3 c457f81 # F

for n in I K; do cria_commit $n; done

g log --oneline --graph --all

g ch -b master c457f81 # B

for n in E J; do cria_commit $n; done

```

```
# evitar conflito
g merge tmp tmp2 --allow-unrelated-histories -s ours

```

### cherry-pick

```
g ch 0.6.0
g cherry-pick origin/django_extensions
```

## Adicional

### gitlab-cli

https://gist.github.com/rg3915/fa2cc157dba848ddb92d94caeea2ed2f

### bitbucket-cli

https://gist.github.com/rg3915/288af481e993731864192027400b0057


