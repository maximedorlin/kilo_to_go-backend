
# PROCESSUS DE TRAVAIL GIT - KILOTOGO

## I. Structure des Branches

### Rôle des branches :
main (production)
└── develop (intégration)
└── feature/nom-du-module (branches de travail)

text

**Description :**
- **main** : Branche de production, contient le code stable et déployé
- **develop** : Branche d'intégration, contient les nouvelles fonctionnalités en cours de développement
- **feature/** : Branches de travail individuelles pour chaque nouvelle fonctionnalité

## II. Convention de Nommage des Branches

### Format : `type/description-du-travail`

### Types de branches autorisés :
- `feature/` - Nouvelles fonctionnalités
- `fix/` - Corrections de bugs
- `refactor/` - Refactoring de code
- `docs/` - Documentation
- `chore/` - Tâches techniques

### Exemples pour Kilotogo :
-  `feature/gestion-annonces`
-  `feature/systeme-paiement`
-  `feature/suivi-colis`
-  `fix/calcul-frais-transport`
-  `refactor/optimisation-bdd`
-  `docs/guide-utilisation`

## III. Workflow Complet

### 1. Étape 1 : Initialisation

```bash
# Cloner le repository (récupérer le code source)
git clone https://github.com/votre-username/kilotogo.git

# Se déplacer dans le dossier du projet
cd kilotogo

# Vérifier toutes les branches disponibles
git branch -a

# Se positionner sur la branche develop
git checkout develop

# Récupérer les derniers changements de develop
git pull origin develop
2. Étape 2 : Création d'une Branche de Travail
bash
# Se mettre à jour avec la dernière version de develop
git checkout develop
git pull origin develop

# Créer et basculer sur une nouvelle branche
git checkout -b feature/nom-du-module

# Exemples concrets :
git checkout -b feature/gestion-utilisateurs
git checkout -b feature/creation-annonces
git checkout -b feature/systeme-messagerie
3. Étape 3 : Développement Quotidien
bash
# Vérifier sur quelle branche on se trouve
git status
git branch

# Ajouter tous les fichiers modifiés pour le commit
git add .

# OU ajouter des fichiers spécifiques
git add src/main/java/com/kilotogo/Service.java
git add src/main/webapp/app/components/

# Créer un commit avec message descriptif
git commit -m "feat: ajout création annonces

- Implémentation formulaire création
- Validation des champs obligatoires
- Upload d'images pour les annonces
- Tests unitaires pour le service"

# Pousser la branche vers le dépôt distant pour la première fois
git push -u origin feature/nom-du-module

# Pour les pushes suivants
git push
4. Étape 4 : Mise à Jour Régulière
bash
# Se synchroniser avec les derniers changements de develop
git checkout develop
git pull origin develop
git checkout feature/ma-branche
git rebase develop

# En cas de conflits :
# Voir les fichiers en conflit
git status

# Éditer manuellement les fichiers conflictuels
# Marquer les conflits comme résolus
git add .

# Continuer le rebase
git rebase --continue

# Ou annuler le rebase en cas de problème
git rebase --abort
5. Étape 5 : Préparation de la Fusion
bash
# Exécuter les tests avant la fusion
./mvnw test        # Tests backend
npm test           # Tests frontend
npm run lint       # Vérification du code

# Dernière mise à jour avec develop
git rebase develop

# Pousser la version finale (forcer si nécessaire après rebase)
git push -f origin feature/ma-branche
6. Étape 6 : Création de la Pull Request
Sur GitHub/GitLab :

Aller dans l'onglet "Pull Requests"

Cliquer "New Pull Request"

Base : develop ← Compare : feature/ma-branche

Remplir le template :

Titre descriptif

Description des changements

Screenshots si applicable

Liste des tests effectués

Assigner des reviewers (2 personnes minimum)

Attendre les approbations

Après fusion approuvée :

bash
# Retourner sur develop
git checkout develop

# Récupérer la version fusionnée
git pull origin develop

# Supprimer la branche locale
git branch -d feature/ma-branche

# Nettoyer les branches distantes supprimées
git fetch --prune
IV. Standards des Messages de Commit
Structure :
text
type: description courte (50 caractères max)

Description détaillée (optionnelle)
- Point 1
- Point 2
- Point 3
Types de commits :
feat - Nouvelle fonctionnalité

fix - Correction de bug

docs - Modification documentation

style - Changements de formatage

refactor - Refactoring sans changement fonctionnel

test - Ajout/modification de tests

chore - Tâches de maintenance

Exemples :
Bon exemple :

text
feat: implémentation paiement sécurisé

- Intégration API Stripe pour les transactions
- Gestion des webhooks de confirmation
- Tests d'intégration avec mock serveur
- Documentation API dans README
Mauvais exemple :

text
fix: bug
V. Commandes Git Essentielles
A. Configuration
bash
# Configurer l'identité (à faire une seule fois)
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@company.com"

# Configurer VS Code comme éditeur par défaut
git config --global core.editor "code --wait"

# Voir la configuration
git config --list
B. Navigation et Inspection
bash
# Voir l'état actuel des fichiers
git status

# Voir l'historique des commits (format compact)
git log --oneline --graph -10

# Voir l'historique détaillé
git log --pretty=format:"%h - %an, %ar : %s"

# Voir toutes les branches (locales et distantes)
git branch -a

# Voir les différences avec la dernière version
git diff

# Voir les différences pour un fichier spécifique
git diff src/main/java/com/kilotogo/Service.java
C. Gestion des Branches
bash
# Lister les branches locales
git branch

# Lister toutes les branches
git branch -a

# Changer de branche
git checkout nom-branche

# Créer une nouvelle branche
git branch nouvelle-branche

# Créer et basculer sur nouvelle branche
git checkout -b nouvelle-branche

# Supprimer une branche locale (sécurisée)
git branch -d nom-branche

# Supprimer une branche locale (forcée)
git branch -D nom-branche

# Supprimer une branche distante
git push origin --delete nom-branche
D. Gestion des Modifications
bash
# Voir les modifications en cours
git diff

# Annuler les modifications d'un fichier non commité
git checkout -- fichier.txt

# Annuler tous les changements non commités
git checkout -- .

# Déplacer/renommer un fichier
git mv ancien-nom nouveau-nom

# Supprimer un fichier
git rm fichier.txt
E. Sauvegarde Temporaire
bash
# Sauvegarder les modifications en cours
git stash

# Voir les sauvegardes
git stash list

# Récupérer la dernière sauvegarde
git stash pop

# Supprimer les sauvegardes
git stash clear
VI. Règles Importantes
À FAIRE :
Créer toujours des branches depuis develop

bash
git checkout develop && git pull origin develop
git checkout -b feature/ma-fonctionnalite
Commiter régulièrement avec des messages clairs et descriptifs

Mettre à jour sa branche quotidiennement avec develop

bash
git checkout develop && git pull origin develop
git checkout feature/ma-branche
git rebase develop
Tester avant de créer une PR

Tests unitaires

Tests d'intégration

Vérification manuelle des fonctionnalités

Rester sur une branche par fonctionnalité

Une fonctionnalité = une branche

Un correctif = une branche

Ne pas mélanger plusieurs travaux

À ÉVITER :
Pousser directement sur main ou develop

Toujours passer par les Pull Requests

Toujours avoir des reviews

Travailler directement sur develop

develop est une branche d'intégration

Toujours créer une branche feature

Créer des commits trop volumineux

Un commit = une logique métier

Éviter les commits "fourre-tout"

Oublier de mettre à jour sa branche

Risque de conflits importants

Difficulté de fusion

Fusionner sans review

Minimum 2 approbations requises

Vérification du code par les pairs

VII. Résolution des Conflits
Processus de résolution :
Détecter le conflit :

bash
git status
# Affiche les fichiers en conflit
Ouvrir les fichiers conflictuels :

bash
code fichier-en-conflit.java
Résoudre manuellement :

xml
<<<<<<< HEAD
Votre code actuel
=======
Code venant de la branche fusionnée
>>>>>>> feature/autre-branche
Marquer comme résolu :

bash
git add fichier-resolu.java
Finaliser la fusion :

bash
git rebase --continue
# ou
git merge --continue
VIII. Checklist avant Pull Request
Code compilé sans erreurs

Tous les tests passent

Aucun conflit avec develop

Messages de commit clairs

Code review effectué localement

Documentation mise à jour

Fonctionnalité testée manuellement

