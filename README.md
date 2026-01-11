# Lab 4 : Mise en place d’un pipeline CI/CD complet pour un projet Machine Learning
## Étape 1 : Créer le dépôt GitHub et connecter le remote

Lors de cette étape, un nouveau dépôt GitHub a été créé afin d’héberger le projet MLOps. Le dépôt local existant a ensuite été connecté à ce dépôt distant en configurant l’URL du remote *origin*. La branche principale a été renommée en *main* puis l’ensemble du projet a été poussé vers GitHub, établissant ainsi le lien entre le code local et le dépôt distant pour la suite du pipeline CI/CD.

<img width="1919" height="715" alt="image" src="https://github.com/user-attachments/assets/13e3034b-08d1-42f5-9f1d-c059e4d92713" />

<img width="1919" height="735" alt="image" src="https://github.com/user-attachments/assets/720cb2fc-9476-47a2-b9c1-28dd6de1fede" />

<img width="1159" height="380" alt="image" src="https://github.com/user-attachments/assets/faef5444-26a1-4acd-ae79-8aeb0697b856" />

## Étape 2 : Définir les secrets GitHub

Dans cette étape, les **variables** et **secrets** du dépôt GitHub ont été configurés afin d’être utilisés de manière sécurisée dans le workflow CI/CD.

Les variables `PY_VERSION`, `F1_GATE_THRESHOLD` et `APP_ENV` ont été ajoutées comme **Repository Variables**, tandis que `DEMO_SECRET` a été défini comme **Repository Secret**.

Cette configuration permet de paramétrer le pipeline sans modifier le code source et d’assurer la confidentialité des informations sensibles lors de l’exécution des jobs GitHub Actions.

<img width="1024" height="626" alt="2-1" src="https://github.com/user-attachments/assets/177da92c-5670-49eb-b582-4c4be4dec334" />

<img width="983" height="505" alt="2-2" src="https://github.com/user-attachments/assets/a51a6ea7-1ee5-41ee-8b44-eaa80420084a" />

## Étape 3 : Créer le workflow CI/CD

Lors de cette étape, un workflow CI/CD a été configuré via GitHub Actions à l’aide du fichier `mlops.yml` placé dans `.github/workflows/`.

Le workflow est déclenché sur chaque *push* et *pull request* vers la branche `main`.

Le job **CI** installe l’environnement Python, restaure les caches, exécute le pipeline DVC, vérifie la métrique F1 via un *Quality Gate* et sauvegarde les artefacts générés.

Le job **CD**, exécuté uniquement sur `main`, récupère ces artefacts et simule une phase de déploiement SSH en utilisant les variables et secrets GitHub.

Cette étape permet d’automatiser l’intégration continue et de préparer le déploiement du modèle de manière reproductible.
<img width="1844" height="951" alt="3" src="https://github.com/user-attachments/assets/61340fa0-3104-4d3c-b3d6-27aee5a84d9a" />



## Étape 4 : Commit et push

Après le commit et le push sur la branche *main*, le workflow CI/CD (`.github/workflows/mlops.yml`) est automatiquement déclenché via GitHub Actions. Le job **CI** exécute l’entraînement du modèle avec DVC, vérifie les métriques (Quality Gate F1) et génère les artefacts Machine Learning. Le job **CD (simulé)** télécharge les artefacts validés, lit les variables GitHub (*APP_ENV*, *F1_GATE_THRESHOLD*), masque correctement les secrets, liste les dossiers *models*, *registry* et *reports*, puis simule un déploiement via SSH en environnement *staging*. Les logs confirment la réussite de toutes les étapes, indiquant que le pipeline est **valide et prêt pour un déploiement réel**.



<img width="1916" height="772" alt="4-1" src="https://github.com/user-attachments/assets/84ed0a51-2a18-499b-a262-0cb0365f90af" />

<img width="1907" height="1012" alt="4-2" src="https://github.com/user-attachments/assets/b973f8b1-7a70-4049-8bdc-59ecf84bd1c6" />

<img width="1888" height="997" alt="4-3" src="https://github.com/user-attachments/assets/ab8f1387-5f7b-4253-827e-c7ce8059571c" />

