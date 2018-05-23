# UTILISATION DE GIT

## 1. POUR COMMENCER

### INITIALISER PROJET GIT
Aller dans le dossier du projet et taper : 
```
git init
```

puis : 
```
git config --global user.email "email"
git config --global user.name "user"
```

### ETAT DU PROJET
```
git status
```

## 2. STAGING / COMMIT

### STAGING DU FICHIER A COMMIT (Ajout du fichier à la liste des fichiers à commit)
```
git add <fichier>
```

### STAGING DE PLUSIEURS FICHIERS DU MEME TYPE (ex: html)
```
git add *.html
```

### STAGING DE TOUS LES FICHIERS DU PROJET
```
git add --all
```

### STAGING DE TOUS LES FICHIERS DU PROJET SANS LES FICHIERS SUPPRIMES
```
git add .
```

### COMMIT DU Fichier (Ajoute la liste des fichiers à commit au repositorie en local)
```
git commit -m "message"
```

### STAGING DU FICHIER + COMMIT (raccourci)
```
git commit -a -m "message"
```

## 3. IGNORER DES DOSSIERS / FICHIERS

### FICHIER GITIGNORE
Créer un fichier .gitignore dans le projet puis ajouter dedans les extensions de fichiers (ex: \*.tmp) et les chemins des dossiers (ex: tmp/\*) / fichiers (ex: config.php) à ignorer

## 4. LES LOGS

### AFFICHER LES LOGS DES COMMITS
```
git log
```

Pour un formatage plus lisible:
```
git log --oneline
```

### AFFICHER LES n DERNIERS LOGS
```
git log -n <n>
```

### AFFICHER LES LOGS D'UN FICHIER EN PARTICULIER
```
git log -p <fichier>
```

## 5. GIT DIFF

### VOIR LES DIFFERENCES ENTRE FICHIERS DEPUIS LE DERNIER COMMIT
```
git diff
```

## 6. RETOUR EN ARRIERE

### REVENIR A UN COMMIT ANTERIEUR
Retour à un état antérieur du projet (Observation / pas de modification possible)
```
git checkout <id commit>
```

### RETOUR A UN ETAT ANTERIEUR D'UN FICHIER + STAGING + COMMIT
```
git checkout <id> <fichier>
git commit -m "Retour à ..."
```

### RETOUR AU DERNIER ETAT D'UN FICHIER
```
git checkout master <fichier>

```

### DEFAIRE UN COMMIT
Retire un commit de la liste
```
git revert <id commit>
```

### RETIRER LE STAGING D'UN FICHIER
```
git reset HEAD <fichier>
```

ou
```
git reset -- <fichier>
```

### REVENIR A UN COMMIT (suppression définitive)
Dernier commit:
```
git reset --hard
```

Pour cibler un commit en particulier (garde les dernières modifs mais suprrime de l'historique):
```
git reset <id>
```

Revenir au dernier commit en gardant les modifications et le staging (^ = dernier commit, ^^ = avant dernier...):
```
git reset HEAD^ --soft
```

Revenir au dernier commit en gardant les modifications sans le staging:
```
git reset HEAD^ --mixed
```

Revenir au dernier commit en supprimant les modifications sans le staging:
```
git reset HEAD^ --hard
```

## 7. Les branches

### CREER UNE BANCHE
```
git branch <nom branch>
```

### PASSER D'UNE BRANCHE A UNE AUTRE
```
git checkout <nom branch>
```

### FUSIONNER DES BRANCHES
On se place sur la branche sur laquelle on souhaite fusionner puis:
```
git merge <branch à fusionner>
```

Sans fast forward:
```
git merge --no-ff <branch>
```

### SUPPRIMER UNE BRANCHE
```
git branch -d <branch>
```

## 8. MANIPULER L'HISTORIQUE (Utiliser avec précaution)

### MODIFIER LE COMMIT PRECEDENT
On modifie les fichiers puis:
```
git add .
git commit --amend
```

### RAPATRIER LES COMMITS D'UNE BRANCHE SUR UNE AUTRE
On se positionne sur la branche qui contient les commits à rapatrier puis:
```
git rebase <branch qui doit récupérer les commits>
```

puis: 
```
git checkout <branch qui doit récupérer les commits>
git merge <branch à fusionner>
```

### REBASE INTERACTIF
```
git rebase -i <branch qui doit récupérer les commits>
```

Un éditeur de texte s'ouvrir puis on peut changer "pick" en "squash" pour fusionner des commits et renommer. ex:
```
pick 7cf43b8 Ajout nouveau CSS
pick dff46ba Ajout du fichier CSS
```

devient:
```
pick 7cf43b8 Modification du CSS
squash dff46ba Ajout du fichier CSS
```

Les 2 commits n'en formeront plus qu'un

puis: 
```
git checkout <branch qui doit récupérer les commits>
git merge <branch à fusionner>
```


## 9. REMISAGE (stash)
Stocker des modifications pour utilisation ultérieure

## 10. REMOTE
Sauvegarde sur le depot (repository) en ligne

### INITIALISER DEPOT
#### Dans le dossier du depot distant:
```
git init --bare
```

#### Dans le dossier du projet:
Liste des remote:
```
git remote -v
```

Ajoute un nouveau remote:
```
git remote add <nom depot> <url depot>
```

### BRANCHES DISPONIBLES SUR LE DEPOT
```
git branch -r
```

### ENVOYER SUR LE DEPOT
```
git push <nom depot> <branch>
```

### SUPPRIMER BRANCHE SUR LE DEPOT
```
git branch -d <branch>
git push <nom depot> --delete <branch>
```

### RECUPERER LES NOUVEAUX COMMITS DU DEPOT
Dans le cas d'un travail collectif (fusion)
```
git pull <nom depot> <branch>
```

plus propre (sans fusion pour un historique propre)
```
git pull --rebase <nom depot> <branch>
```

### ACCEDER A UN DEPOT EXISTANT ET RECUPERER LES FICHIERS
```
git clone <url depot> <nom depot>
```

le nom du depot peut etre différent de l'original

Récupérer les "n" derniers commits:
```
git clone <url depot> --depth <n>
```

### SUPPRIMER UN DEPOT
```
git remote remove <nom depot>
```


## GITHUB

### GENERER CLE SSH
```
ssh-keygen -t rsa -C "email"
```