# Projet de Site de Services

Ce projet consiste à créer un site web permettant aux utilisateurs de demander et de fournir différents services, allant de la réparation de bidet à la peinture des murs et au nettoyage de la maison. Le site est en cours de développement en utilisant Django, un framework web Python.

## Objectifs

Le site devrait permettre deux types d'utilisateurs :

- Entreprise : peut créer de nouveaux services
- Client : peut demander des services existants

Chaque utilisateur doit pouvoir s'inscrire et se connecter en fournissant leur adresse e-mail et leur mot de passe. Cependant, lors de l'inscription, chaque type d'utilisateur doit fournir des informations différentes :

### Client :
- Adresse e-mail
- Mot de passe
- Confirmation de mot de passe
- Nom d'utilisateur
- Date de naissance

### Entreprise :
- Adresse e-mail
- Mot de passe
- Confirmation de mot de passe
- Nom d'utilisateur
- Domaine d'activité

Chaque utilisateur doit avoir sa propre page de profil affichant ses informations (à l'exception du mot de passe) et, pour les clients, tous les services précédemment demandés doivent également être affichés. Pour les profils d'entreprise, en plus de toutes leurs informations, les services qu'elle fournit doivent également être affichés.

L'attribut de domaine d'activité dans les entreprises limitera le type de services qu'elle peut fournir. Cet attribut ne doit accepter que les valeurs suivantes :

- Climatisation
- Tout-en-un
- Menuiserie
- Électricité
- Jardinage
- Machines domestiques
- Ménage
- Design d'intérieur
- Serrures
- Peinture
- Plomberie
- Chauffe-eau

Une entreprise de menuiserie ne peut créer que des services de menuiserie, tout comme une entreprise de ménage ne peut fournir que des services de ménage. Cependant, les entreprises Tout-en-un peuvent créer n'importe quel type de services. Mais qu'est-ce qu'un service inclut ? Un service doit avoir :

- Nom
- Description
- Domaine (peut avoir les mêmes catégories de domaines que les entreprises, sauf que vous ne pouvez pas avoir un service Tout-en-un)
- Prix par heure
- Date de création (cet attribut doit prendre automatiquement une valeur lors de la création d'un service)

Le site devrait avoir une page affichant les services les plus demandés, une page montrant tous les services dans l'ordre de création (le plus récemment créé en premier) et une page pour chaque catégorie de service, qui affiche les services disponibles pour cette catégorie.

Chaque service doit avoir sa propre page, sur laquelle doivent être affichées les informations ci-dessus ainsi que le nom de l'entreprise fournissant ce service. Un utilisateur doit pouvoir consulter tous les services de cette entreprise en cliquant sur le nom affiché et en consultant le profil de l'entreprise.

Une fois qu'un service est créé par une entreprise, chaque utilisateur y a accès. Seuls les clients peuvent demander un service en fournissant l'adresse où le service est requis et la durée du service (en heures). Une fois qu'un client demande un service, il est ajouté à la liste des services précédemment demandés. Dans cette liste, pour chaque service demandé, le client peut voir le nom du service, le domaine du service, le coût calculé du service, la date à laquelle le service a été demandé et l'entreprise qui a fourni le service.

## Architecture du Projet

Le projet Django est organisé par un dossier principal du projet et différentes applications.

Lorsqu'on démarre un nouveau projet Django (avec la commande `django-admin startproject <nom-du-projet>`), le dossier principal (qui porte le même nom que le projet) et un fichier appelé `manage.py` sont créés. Ce fichier est utilisé pour exécuter diverses commandes. Les plus courantes sont :

- `python3 manage.py runserver` : lance un serveur sur le port 8000 par défaut et sert votre projet.
- `python3 manage.py startapp <nom-de-l-application>` : crée une application, autrement dit, crée un répertoire avec la plupart des fichiers nécessaires pour une application.
- `python3 manage.py makemigrations` et `python3 manage.py migrate` : ces deux commandes vont de pair. Nous les utilisons pour déclarer les modifications apportées à la base de données Django (généralement effectuées dans le fichier `models.py` de chaque application).
- `python3 manage.py createsuperuser` : crée un super utilisateur (administrateur) qui peut accéder et modifier les informations dans la base de données Django (accessible à l'URL `localhost:8000/admin`).
- `python3 manage.py` : pour obtenir une liste de toutes les commandes disponibles.

Chaque application est généralement liée à un aspect différent du projet. Par exemple, dans ce projet, il y a trois applications :

- `services` : gère les fonctionnalités essentielles liées aux services (création de service, affichage des services, demande de service ...)
- `users` : gère les fonctionnalités essentielles liées aux utilisateurs (inscription utilisateur, profil utilisateur, connexion utilisateur ...)
- `main` : gère les informations communes à tout le projet (page d'accueil, barre de navigation, page de déconnexion ...)

Par défaut, lors du démarrage d'une application, Django crée plusieurs fichiers très utiles pour le développement d'un site web. Ceux sur lesquels nous passons le plus de temps sont :

- `models.py` : où vous pouvez ajouter des objets et définir leurs attributs dans la base de données Django
- `views.py` : où vous pouvez manipuler l'arrière-plan d'une page web sur le projet

En plus de ces deux fichiers, d'autres fichiers sont généralement créés manuellement :

- `urls.py` : ici, vous pouvez spécifier les URLs de votre projet et les associer à une vue (à partir du fichier `views.py`), afin d'afficher une page web. Par exemple, l'URL `profile/` est associée à la vue `views.ProfileView)`
- `forms.py` : ici, vous pouvez créer vos formulaires à utiliser dans votre fichier `views.py`. Par exemple, vous pouvez créer un formulaire de connexion par défaut à utiliser dans `LoginView` (présent dans le fichier `views.py`).

Généralement, nous créons également un dossier où nous pouvons stocker des modèles (en HTML). Ce dossier suit généralement la structure suivante :

 - nom-du-projet/ # répertoire du projet
 - nom-de-l-application/ # répertoire de l'application
 - pycache/
 - migrations/
 - templates/ # répertoire de modèle de l'application
 - nom-de-l-application/
 - login.html
 - profile.html
 - register.html
 - ...
 - ...
 - urls.py
 - views.py


Vous utiliserez également ce qui est connu sous le nom de modèles Django, qui est utilisé à l'intérieur des fichiers HTML. C'est une façon de coder à l'intérieur de HTML, permettant de parcourir les objets transmis (boucle `for`) ou même de faire des vérifications conditionnelles (instruction `if/else`), entre autres choses intéressantes. Pour en savoir plus à ce sujet, vous pouvez consulter la documentation sur les modèles Django.

## Guide d'Installation

1. Cloner le projet depuis le référentiel Git.

2. Assurez-vous d'avoir Python 3.x installé sur votre système.

3. Créez un environnement virtuel pour le projet et activez-le.

 - python3 -m venv venv
 - source venv/bin/activate


4. Installez les dépendances requises.
 - pip install -r requirements.txt


5. Effectuez les migrations initiales de la base de données.
 - python manage.py makemigrations
 - python manage.py migrate

6. Créez un superutilisateur pour accéder à l'interface d'administration Django.
 - python manage.py createsuperuser

7. Lancez le serveur de développement.
 - python manage.py runserver


8. Accédez à l'application dans votre navigateur à l'adresse `http://127.0.0.1:8000/`.

## Contributeurs

- [Mouhamed Diouf](https://learn.zone01dakar.sn/git/mouhameddiouf)

© 2024 Projet de Site de Services. Distribué sous la licence DioufMouhamed.
