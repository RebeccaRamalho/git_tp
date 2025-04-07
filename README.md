# 🧪 TP : Maîtriser Git et GitHub (CLI & IntelliJ IDEA)

## 🎯 Objectifs

- 📌 Comprendre les bases de Git et GitHub  
- 🗃️ Créer et gérer un dépôt distant  
- 🌿 Utiliser les branches, commits et fusions  
- 💻 Maîtriser Git en ligne de commande et avec un IDE (IntelliJ)

---

## 🧰 Prérequis

- 👤 [Avoir un compte GitHub](https://github.com)  
- ⚙️ [Installer Git](https://git-scm.com)  
- 🧠 Connaître les bases du terminal  
- 🛠️ [Installer IntelliJ IDEA](https://www.jetbrains.com/idea)

---

## 🔹 Partie 1 — Création du dépôt GitHub

1. Allez sur [GitHub](https://github.com) et connectez-vous  
2. Cliquez sur ➕ **New repository**  
3. Remplissez :
   - **Repository name** : `mon-projet-git`
   - **Description** : (optionnelle)
   - Visibilité : Public ou Private  
   - ✅ Cochez **Add a README file**
4. Cliquez sur **Create repository**
5. Copiez l'URL HTTPS :  
   `https://github.com/ton-utilisateur/mon-projet-git.git`

```bash
git clone https://github.com/ton-utilisateur/mon-projet-git.git
cd mon-projet-git
```

✅ **Résultat attendu**  
Le dépôt est bien cloné localement. Le fichier `README.md` est présent.

👉 **Vérifiez** : via `ls` ou un explorateur de fichiers

---

## 🔹 Partie 2 — Modification du README

1. Ouvrez le fichier `README.md`  
2. Remplacez son contenu par le texte du fichier `TP_Git_Complet.md`  
3. Enregistrez et exécutez :

```bash
git status
git add README.md
git commit -m "Mise à jour du README"
git push origin main
```

✅ **Résultat attendu**  
Le README est mis à jour sur GitHub.

👉 **Vérifiez** : Sur la page d’accueil du dépôt GitHub

---

## 🔹 Partie 3 — Création d’une branche

```bash
git checkout -b develop
```

1. Créez un fichier `notes.md` avec 3 idées de projets ou des notes  
2. Puis :

```bash
git add notes.md
git commit -m "Ajout de notes"
git push origin develop
```

✅ **Résultat attendu**  
Branche `develop` créée avec `notes.md` visible sur GitHub

👉 **Vérifiez** : Via l’onglet "branches" ou "code"

---

## 🔹 Partie 4 — Structure du projet

Dans `develop`, créez cette arborescence :

```
mon-projet-git/
├── src/
│   └── main.py
├── data/
│   └── sample.txt
└── README.md
└── notes.md
```

Dans `main.py` :

```python
print("Hello Git")
```

```bash
git add .
git commit -m "Structure de projet"
git push origin develop
```

✅ **Résultat attendu**  
Structure de dossier bien visible sur GitHub

👉 **Vérifiez** : Explorez la branche `develop`

---

## 🔹 Partie 5 — Merge via Pull Request

1. Allez sur GitHub > Onglet "Pull Requests" > **Compare & pull request**  > "Compare : develop" to "base: main"
2. Ajoutez un commentaire, cliquez sur **Create pull request**  
3. Cliquez sur **Merge pull request**  
4. (Optionnel) Supprimez `develop` → **Delete branch**

✅ **Résultat attendu**  
Fusion réussie, branche supprimée et intégrée à `main`

👉 **Vérifiez** : onglet Pull Requests / historique de commits

---

## 🔹 Partie 6 — Revenir en arrière : `git revert`

```bash
git log --oneline
git revert <commit_id>
```

✅ **Résultat attendu**  
Un nouveau commit annule un précédent

👉 **Vérifiez** : `git log` montre le commit de revert

---

## 🔹 Partie 7 — Réinitialiser l’historique : `git reset`
--soft

--mixed (par défaut)

--hard

Sur une branche temporaire "temp" :

🧪 Étapes de test avec git reset
🔁 1. git reset --soft HEAD~1
```bash
git reset --soft HEAD~1
```

✅ Effets :
Le commit est annulé, mais...

Les modifications sont conservées dans le staging area (index).

C’est comme si vous n’aviez jamais lancé git commit.

🔍 Vérification :
```bash
git status
```

Vous verrez :
✅ demo.txt est en staging avec les modifications de "ligne 2".

🔁 2. git reset --mixed HEAD~1
```bash
git reset --mixed HEAD~1
```

✅ Effets :
Le commit est annulé.

Les modifications sont conservées dans le working directory.

Le fichier est retiré du staging.

🔍 Vérification :
```bash
git status
```

Vous verrez :
🟡 demo.txt est modifié mais non indexé (non ajouté avec git add).

🔁 3. git reset --hard HEAD~1
```bash
git reset --hard HEAD~1
```

⚠️ Effets :
Le commit est annulé.

Les modifications sont perdues dans le working directory et dans le staging area.

Le fichier revient à l'état du commit précédent.

🔍 Vérification :
```bash
git status
```

cat demo.txt
✅ demo.txt ne contient que "ligne 1".

✅ **Résultat attendu**  
Compréhension des types de reset

👉 **Vérifiez** : `git log`, `git status`

---

## 🔹 Partie 8 — Gérer un conflit

1. Créez une branche `conflict-a` et une branche `conflict-b`. Assurez vous de créer les 2 branches à partir de "main"
2. Modifiez une même ligne dans un même fichier
3. Commitez et pushez les 2 branches
4. Mergez dans un premier lieu la branche `conflict-a` dans `main`, puis mergez `conflict-b` dans `main` aussi.
5. Git détecte que demo.txt a été modifié dans conflict-a et conflict-b, sur la même ligne.

Vous verrez un message comme :

Auto-merging demo.txt
CONFLICT (content): Merge conflict in demo.txt
Automatic merge failed; fix conflicts and then commit the result.

🔧 Résolution du conflit
Ouvrez le fichier demo.txt :


<<<<<<< HEAD
Modif depuis A
=======
Modif depuis B
>>>>>>> conflict-b
Cela signifie :

<<<<<<< HEAD → contenu de la branche actuelle (main, avec les changements de conflict-a)

======= → séparateur

>>>>>>> conflict-b → contenu de la branche fusionnée

👉 Résolvez le conflit manuellement en choisissant :

une version

ou en les combinant

Par exemple :

Modif depuis A et B


💾 Finaliser la fusion
Une fois le fichier corrigé :

```bash
git add demo.txt
git commit -m "Résolution du conflit entre A et B"
git push origin main
```

✅ Résultat attendu
Le fichier est fusionné proprement

Le commit de résolution est visible dans git log

Le fichier contient la version choisie

🔍 Vérifications
```bash
git log --oneline
cat demo.txt
```

---
🔹 Partie 9 — Copier un commit : git cherry-pick
🎯 Objectif
Comprendre comment copier un commit spécifique d’une branche dans une autre sans tout fusionner.

🔧 Contexte de départ
Supposons que vous ayez une branche other-branch avec un ou plusieurs commits intéressants, mais que vous ne souhaitez pas tout fusionner dans main, juste un seul commit précis.

🛠️ Étapes détaillées
1. Préparer une branche de travail
```bash
git checkout main
```

2. Voir les commits d’une autre branche
```bash
git log other-branch --oneline
```

Exemple de sortie :

e3a1c2d (other-branch) Ajout d'une fonction utile
a5f3b1a Correction d’un bug

3. Copier un commit spécifique dans main
```bash
git cherry-pick e3a1c2d
```

✅ Git va rejouer ce commit dans main, comme si vous l’aviez écrit ici.

🔍 Résultat
```bash
git log --oneline
```

Vous verrez le commit Ajout d'une fonction utile ajouté à la fin de main.

📌 Il s'agit d’un nouveau commit avec un nouvel ID, mais le même contenu (message + modifs) que dans other-branch.

---

## 🔹 Partie 10 — Manipulations avec IntelliJ IDEA

### 🔸 Faire un commit

1. Créez `hello.py` :

```python
print("Bonjour depuis IntelliJ !")
```

2. Clic droit → Git → Add  
3. Commit → "Commit and Push"

### 🔸 Travailler avec des branches

- En bas à droite → `main` → **New Branch**
- Travaillez → Commit → retour sur `main` → **Merge Changes**

### 🔸 Push / Pull

- Git → **Push**
- Git → **Pull**

✅ **Résultat attendu**  
Les commits sont visibles dans Git et sur GitHub

👉 **Vérifiez** : Git > Log

---

## 🔹 Partie 11 — Fonctions avancées avec IntelliJ IDEA

### 🔸 Revert

- Git → Log → clic droit → **Revert Commit**

### 🔸 Reset

- Git → Log → clic droit → **Reset Current Branch to Here...**

### 🔸 Résolution de conflits

- Git → **Merge Conflicts**  
- Interface visuelle pour résoudre

### 🔸 Cherry-pick

- Git → Log → clic droit → **Cherry-pick**

✅ **Résultat attendu**  
Toutes les actions peuvent être réalisées via IntelliJ

👉 **Vérifiez** : Git > Log

---

## 🏁 Conclusion

🎉 **Félicitations !** Tu viens de parcourir tout le cycle de travail Git/GitHub  
🧠 Tu maîtrises maintenant **Git en ligne de commande et avec IntelliJ IDEA**