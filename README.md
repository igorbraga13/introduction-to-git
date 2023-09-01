# A short introduction to Git

This is my study about Git, is based (more like a copy) on a course of DataCamp "Introduction to Git".

## What is version control?

Git is one of several version control systems, it's a tool that manages changes made to the files and directories in a project. The advantages of Git are:
- You can always see which reults were generated by which versions of your programs
- Git automatically notifies when your works conflicts with another, making difficult eventuals overwrites
- You and many people can work in the same project in different machines, in this way we have greater scalability

So Git keep track of changes to files, notice conflicts between changes made by different people and synchronize files between different computers

## Where does Git store information?

Each Git projects has two parts:
- Files and directories that we create and edit directly
- Extra info that Git records about the project's history
The combo of this these two things is called __repository__

Git stores all of this "Extra infos" in a directory called `.git` located in the root directory of the repository. The way this information should be storage is a very precise way, so never edit ou delete anything in `.git`

If a home directory `/home/repl` contains a repository called `dental`, which has a  sub-directory called `data`, the information about the history of the files in `/home/repl/dental/data` is in `/home/repl/dental/.git` because all of the information about repository is stored under its root directory and `data` is just a sub-directory

## How can I check the state of a repository?

Everytime in Git you will want to check the status of your repository. To do this, run the command

```
git status
```
which display the branch that you where and a list of all files that have been modified since the last changes were saved

## How can I tell what I have changed?

Git has a staging area in which it stores files with changes that haven't been saved yet. Making an analogy with the email, putting files in the stagging area is like puttin things in a draft that can be changed, adding or taking things. While committing those changes is like send the email, once you send can't make further changes

![](https://miro.medium.com/max/686/1*diRLm1S5hkVoh5qeArND0Q.png)

`git status` shows you which files are in this staging area, and which files have changes that haven't yet been put there. `git diff` compare the file as it currently is to what you last saved. Run the command without any filenames to show all the changes in your repository

```
git diff
```
 and use the command below to show the changes to the files in some directory

```
git diff filename
```

## What is in a diff?

Previously we saw __when__ use the command `git diff`, now we gonna see __what__ is in your output

```
diff --git a/report.txt b/report.txt
index e713b17..4c0742a 100644
--- a/report.txt
+++ b/report.txt
@@ -1,4 +1,5 @@
-# Seasonal Dental Surgeries 2017-18
+# Seasonal Dental Surgeries (2017) 2017-18
+# TODO: write new summary
```

- `a` and `b` are placeholders meaning the first and the second version simultaneously
- The index line will be explored further
- `---a/report.txt` represents the lines there are removed and `+++ b/report.txt` the lines there are added
- A line starting with `@@` that tells where the changes are being made. The pair represents the _start line_ and the _number of lines_, in this case the changes starting at line 1, with 5 lines where there were onde 4
- A line-by-line listing of the changes with `-` to show deletions and `+` to show addictions, we can also configure Git to show deletions in red and additions in green

para utilizar a função tal 

```
git init
```

# Funções:

## CHECKOUT
Ao clonar um respositório se torna necessário criar uma branch para trabalhar `git checkout -b "new_branch"`
`git branch -a` irá listar todas as branchs do repositório
`git checkout "branch"` irá mudar para uma branch já existente
## ADD

## COMMIT

### reset ou revert

Caso ainda não tenha feito o push no commit é possível utilizar o comando `git reset`, caso o push já tenha sido efetuado é necessário utilizar o `git revert` para criar um novo commit que irá apagar o anterior. O comando `git revert HEAD~1` reverte o último commit, enquanto o `git revert HEAD~2` reverte os dois últimos commits.O mesmo se aplica para `git reset HEAD~1`.
Utilizar o `git reset` após ter dado o push irá desfazer o último commit, e como já foi enviado para a branch, a copia local será invalidada.
É importa lembrar que para utilizar essas ferramentas não podem ser feita alterações locais entre o momento do push e do reset/revert, caso contrário ocorrerá conflito entre a branch local e e remota, devido aos arquivos ainda não mergeados.

### amend

O comando `git commit --amend` permite editar o último commit. Ele nos permite combinar alterações preparadas com o commit anterior ao invés de criar um novo commit. Podemos utilizá-lo para editar nossa mensagem de commit anterior sem alterar seu snapshot. Essa alteração substitui o commit, de modo que o commit alterado será uma nova entidade com referência própria.
O comando `git commit --amend -m "an updated commit message"` permite que você passe um novo texto no commit, sem a necessidade de abrir um editor

Caso tenha submetido um commit e queira adicionar mais alguma alteração sem alterar o conteúdo do seu commit é possível utilizar o comando `git commit --amend --no-edit` como no exemplo abaixo:

```bash
# Edit hello.py and main.py
git add hello.py
git commit 
# Realize you forgot to add the changes from main.py 
git add main.py 
git commit --amend --no-edit
```
Nesse caso o `--no-edit` permitirá adicionar o main.py no commit, sem a necessidade de alterar ou criar um novo commit. O commit resultante irá substituir o incompleto e entenderá que fizemos o commit das alterações hello.py e main.py em um único snapshot

## DIFF

## STASH

## PULL

Antes de começar a trabalhar em um projeto é interessante rodar o `git pull origin branch` para puxar a versão mais recente da branch e continuar o trabalho a partir daí.
`git config pull.rebase false` # merge
`git config pull.rebase true` # rebase
O comando `git config pull.ff only` significa fast-forward only, nesse caso fazemos com que esse seu último commit seja o final da branch em questão, sobreponto todos os commits posteriores ao momento em que sua branch foi clonada.


# Referências
https://www.atlassian.com/git/tutorials

stackoverflow.com

https://learngitbranching.js.org/?locale=pt_BR
