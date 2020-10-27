link to description of git merge tool

https://stackoverflow.com/questions/161813/how-to-resolve-merge-conflicts-in-git



git checkout GitTest.txt** - usuwa dodane zmiany  w pliku ktore nie zostaly jeszcze skomitowan

**git commit --amend -m** "Zmiana wiadomosci w komicie" - zmienia wiadomosc w komicie, ale zmienai tez hash code commitu co powoduje zmiane histori UWAZAC GDY ROBIMY ZMIANY W KOMITACH KTORE SA NA REMOTE

**git cherry-pick 5df5e246** - wykonujac ta komende na branczce B, przenosimy konkretny commit z branczki A

**git reset --soft 5df5e24** - cofa wszystkie commit do podanego

**git reset 5df5e24** - usuwa zmian yjakie zaszly w podanych komicie z working area do stagin area

**git reset --soft 5df5e24** - usuwa plii konkretnego commitu z stagin area

**git clean** **-df** - remove untrakted files

**git reflog** - show what happend on repo (do 30 dnie wstecz)

=====================================================

TWORZENIE BRANCZI Z KONKRETNEGO COMMITU:

**git checout numercommitu** - tworzymy branczkez konkretnego commitu, co sprawiam ze jestesmy w statusie DETACHED HEAD

**git branch asdzc** - tworzymy branczke, zmiany z DETACHED HEAD  zapisuja sie na tej branczce

**git  checkout asdzc**

====================================================

**git revert hashcommitu** - odwraca zmiany z onkretnego commitu, tworzy nowy commit ktory trzeba zpuszowac w celu nadpisania zmian na remote









Changing Your Last Commit
One of the common undos takes place when you commit too early and possibly forget to add
some files, or you mess up your commit message. If you want to try that commit again, you can
34
Scott Chacon Pro Git Section 2.4 Undoing Things
run commit with the --amend option:

```
$ git commit --amend  
```


