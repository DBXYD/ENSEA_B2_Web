# TP Django : Gestion de la cafétéria

## Contexte

Vous allez développer une **application web pour la cafétéria de l'école**.  
Chaque étudiant a un **crédit personnel**, qu'il peut utiliser pour acheter des produits.  
L'application permettra de gérer :

- Les étudiants et leur crédit
- Les produits disponibles à la vente, leur stock et leur valeur
- Les transactions lors des achats
- Une interface moderne avec **Bootstrap**

---

## Objectifs pédagogiques

- Découvrir le framework **Django (MVT)**  
- Créer des **models** pour gérer les données  
- Utiliser des **views** et des **templates** pour afficher des pages  
- Appliquer du **CSS / Bootstrap / JS** pour l'interface  
- Concevoir la base de données avec **dbdiagram.io**  
- Comprendre **IP / LAN / localhost / accès réseau**  
- Gérer un **environnement Python isolé**  
- Versionner et sauvegarder son projet avec **Git / GitHub**  
- Répondre à des **quiz courts** pour valider la compréhension

---

## Etape 1 : Préparer le terrain : environnement Python et repository Github

### Créer un compte GitHub et un nouveau repository

Si vous n'avez pas encore de compte GitHub, commencez par en créer un :

1. Rendez-vous sur [GitHub.com](https://github.com) et cliquez sur "Sign up" (S'inscrire).
2. Remplissez le formulaire avec votre adresse email, un nom d'utilisateur unique et un mot de passe.
3. Vérifiez votre email pour activer le compte.

Une fois connecté, créez un nouveau repository :

1. Cliquez sur le bouton "+" en haut à droite et sélectionnez "New repository".
2. Donnez un nom à votre repository (ex. : "cafeteria-django").
3. Choisissez la visibilité : public (visible par tous) ou private (privé) : 
   - **Public** : Tout le monde peut voir votre code, le cloner et contribuer (si vous le permettez). Idéal pour des projets open-source ou pour partager votre travail.  
   - **Privé** : Seuls vous et les collaborateurs que vous invitez peuvent voir et accéder au repository. Utile pour des projets personnels ou confidentiels. Pour ce TP, un repository public est recommandé pour faciliter le partage.
4. Ne cochez pas "Add a README file" ni "Add .gitignore" pour l'instant, car nous les créerons localement.  
   - **README.md** : Un fichier qui décrit votre projet (objectifs, installation, utilisation). Il s'affiche automatiquement sur la page du repository GitHub.  
   - **.gitignore** : Un fichier qui liste les fichiers/dossiers à ignorer lors des commits (ex. : fichiers temporaires, environnements virtuels, secrets). Cela évite de pousser des fichiers inutiles ou sensibles.
5. Cliquez sur "Create repository" et copiez l'URL du repository (ex. : `https://github.com/votre-nom-utilisateur/cafeteria-django.git`).

#### Utiliser SSH pour synchroniser avec GitHub (recommandé)

Au lieu d'utiliser l'URL HTTPS, vous pouvez configurer SSH pour une synchronisation plus sécurisée et sans saisie répétée de mot de passe. Voici comment faire sur Ubuntu 24 :

1. **Générer une clé SSH** : Ouvrez un terminal et exécutez :
   ```bash
   ssh-keygen -t ed25519 -C "votre-email@example.com"
   ```
   Appuyez sur Entrée pour accepter les valeurs par défaut (clé sauvegardée dans `~/.ssh/id_ed25519`).

1. **Copier la clé publique** :
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
   Après avoir exécuté cette commande, la clé publique s'affichera dans le terminal. Sélectionnez et copiez toute la ligne (elle commence par `ssh-ed25519`). Vous l'ajouterez ensuite sur GitHub.

1. **Ajouter la clé à GitHub** : 
   - Allez dans vos paramètres GitHub (cliquez sur votre avatar > Settings > SSH and GPG keys).
   - Cliquez sur "New SSH key", donnez un titre (ex. : "Ubuntu 24"), collez la clé publique et sauvegardez.

1. **Utiliser l'URL SSH** : Pour cloner ou push, utilisez l'URL SSH du repository (ex. : `git@github.com:votre-nom-utilisateur/cafeteria-django.git`) au lieu de l'URL HTTPS.

![Diagramme de la base de données](img/github_ssh.png)

#### Guide de github

**Important : Sauvegardez régulièrement votre travail**  
Pendant le développement, il est essentiel de sauvegarder fréquemment vos modifications pour éviter de perdre du code. Utilisez ces commandes régulièrement :  
- `git add .` : Ajoute tous les fichiers modifiés à l'index (staging area).  
- `git commit -m "Description des changements"` : Enregistre les modifications avec un message descriptif.  
- `git push` : Envoie les commits vers GitHub pour une sauvegarde en ligne.  
Faites-le après chaque fonctionnalité importante ou avant de quitter votre session de travail.

**Travailler sur plusieurs ordinateurs :**  
Si vous travaillez sur un autre PC, clonez le repository la première fois avec `git clone <URL-du-repo>`. Ensuite, pour récupérer les dernières modifications avant de travailler, utilisez `git pull`.


### Lancer son premier projet Django

Pour commencer le développement de votre application Django, suivez ces étapes :

1. **Créer un repository GitHub** : Si ce n'est pas déjà fait, rendez-vous sur [GitHub](https://github.com/new), créez un nouveau repository public ou privé nommé par exemple "cafeteria-django", et copiez l'URL du repository.

2. **Cloner le repository** : Sur votre machine, ouvrez un terminal et exécutez `git clone <URL-du-repo>`. Cela créera un dossier local synchronisé avec GitHub.

3. **Créer un environnement virtuel Python (venv)** : Un environnement virtuel isole les dépendances de votre projet, évitant les conflits avec d'autres projets Python. Dans le dossier cloné, exécutez `python3 -m venv venv` pour créer le venv nommé "venv".

4. **Script bash pour initialiser le projet Django** : Voici un script à exécuter dans le **terminal (ctrl+alt+t)** après avoir activé le venv avec `source venv/bin/activate` :

   ```bash
   #!/bin/bash
   # Installer Django
   pip install django
   
   # Créer le projet Django dans le dossier actuel
   django-admin startproject cafeteria .
   
   # Créer une application Django
   python manage.py startapp cafeteria_app
   
   # Effectuer les migrations initiales
   python manage.py migrate
   ```

5. **Lancer le serveur Django pour la première fois** : Après avoir exécuté le script, testez votre projet en lançant le serveur de développement avec `python manage.py runserver`. Le serveur démarrera sur http://127.0.0.1:8000/ (ou http://localhost:8000/). Ouvrez cette URL dans votre navigateur pour voir la page d'accueil de Django. Appuyez sur Ctrl+C dans le terminal pour arrêter le serveur.

6. **Créer un compte administrateur** : Pour accéder à l'interface d'administration de Django, créez un superutilisateur avec `python manage.py createsuperuser`. Suivez les invites pour définir un nom d'utilisateur, email et mot de passe. Ensuite, allez sur http://127.0.0.1:8000/admin/ et connectez-vous avec ces identifiants pour gérer les données via l'interface admin.

7. **Commit et push** : Ajoutez les fichiers avec `git add .`, commitez avec `git commit -m "Initialisation du projet Django"`, puis poussez sur GitHub avec `git push origin main`.

## Etape 2 : Réflexion sur l'architecture de la base de donnée

### Structure d'une base de donnée
#### Exemple :

```sql
Table Student {
  id int [pk]
  name varchar
  email varchar
  credit float
}

Table Product {
  id int [pk]
  name varchar
  price float
  available boolean
}

Table Transaction {
  id int [pk]
  student_id int [ref: > Student.id]
  product_id int [ref: > Product.id]
  date datetime
}
```

#### Structure de base d'une base de donnée de Django : 
```sql
Table auth_user {
  id int [pk, increment]
  username varchar(150) [unique, not null]
  first_name varchar(150)
  last_name varchar(150)
  email varchar(254) [not null]
  password varchar(128) [not null] // Hashed password
  is_staff boolean [default: false, not null]
  is_active boolean [default: true, not null]
  is_superuser boolean [default: false, not null]
  date_joined datetime [not null]
  last_login datetime
}

Table auth_group {
  id int [pk, increment]
  name varchar(150) [unique, not null]
}

Table auth_user_groups {
  id int [pk, increment]
  user_id int [not null, ref: > auth_user.id]
  group_id int [not null, ref: > auth_group.id]
}

Table auth_permission {
  id int [pk, increment]
  name varchar(255) [not null]
  codename varchar(100) [not null]
  content_type_id int [not null]
}

Table auth_user_user_permissions {
  id int [pk, increment]
  user_id int [not null, ref: > auth_user.id]
  permission_id int [not null, ref: > auth_permission.id]
}

Table auth_group_permissions {
  id int [pk, increment]
  group_id int [not null, ref: > auth_group.id]
  permission_id int [not null, ref: > auth_permission.id]
}
```

![Diagramme de la base de données](img/db_django_users.png)

### Synthaxe de la base de donnée Django 

Après avoir conçu votre diagramme sur dbdiagram.io, vous devez créer les **modèles Django** correspondants. Les modèles Django sont des classes Python qui définissent la structure de vos tables de base de données.

**Qu'est-ce que models.py ?**  
Le fichier `models.py` est au coeur de votre application Django. Il contient les définitions des **modèles**, qui sont des classes Python représentant les tables de votre base de données. Chaque modèle définit les champs (colonnes) de la table, leurs types de données, et les relations entre tables (comme les clés étrangères). Django utilise ces modèles pour créer automatiquement les tables SQL via les migrations, et pour interagir avec la base de données dans vos vues et templates.

1. **Ouvrez le fichier `models.py`** : Dans votre application Django (ex. : `cafeteria_app/models.py`), importez les modules nécessaires :
   ```python
   from django.db import models
   ```

2. **Créez une classe pour chaque table** : Chaque table de dbdiagram devient une classe héritant de `models.Model`. Le champ `id` est automatiquement créé par Django.

3. **Correspondance des types de champs** :

| Type dbdiagram    | Type Django Field                     |
|-------------------|---------------------------------------|
| int               | `models.IntegerField()`               |
| varchar           | `models.CharField(max_length=...)`    |
| float             | `models.FloatField()`                 |
| boolean           | `models.BooleanField()`               |
| datetime          | `models.DateTimeField()`              |
| email (spécial)   | `models.EmailField()`                 |

4. **Exemple de traduction** :
   - **dbdiagram** :
     ```sql
     Table Student {
       id int [pk]
       name varchar
       email varchar
       credit float
     }
     ```
   - **Django model** :
     ```python
     class Student(models.Model):
         name = models.CharField(max_length=100)
         email = models.EmailField()
         credit = models.FloatField(default=0.0)
     ```

5. **Relations** :
   - Pour une référence (clé étrangère) : `student_id int [ref: > Student.id]` → `models.ForeignKey(Student, on_delete=models.CASCADE)`
   - Exemple pour Transaction :
     ```python
     class Transaction(models.Model):
         student = models.ForeignKey(Student, on_delete=models.CASCADE)
         product = models.ForeignKey(Product, on_delete=models.CASCADE)
         date = models.DateTimeField(auto_now_add=True)
     ```

6. **Après création** : Exécutez `python manage.py makemigrations` puis `python manage.py migrate` pour appliquer les changements à la base de données.

7. **Rendre les modèles disponibles dans l'interface admin** : Pour gérer vos modèles via l'interface d'administration, ouvrez `cafeteria_app/admin.py` et ajoutez :

   ```python
   from django.contrib import admin
   from .models import Student, Product, Transaction

   admin.site.register(Student)
   admin.site.register(Product)
   admin.site.register(Transaction)
   ```

   Puis redémarrez le serveur avec `python manage.py runserver` et allez sur http://127.0.0.1:8000/admin/ pour voir et gérer vos modèles.

### Principe fondamental de CRUD
CRUD est un acronyme désignant les **opérations de base** que l'on peut effectuer sur les données dans une base de données. Ces opérations sont essentielles pour toute application web gérant des informations. Voici le détail de chaque lettre :

- **C - Create (Créer)** : Ajouter de nouvelles données dans la base. Exemple : Inscrire un nouvel étudiant avec son nom, email et crédit initial.
- **R - Read (Lire)** : Consulter et récupérer des données existantes. Exemple : Afficher la liste des produits disponibles ou les informations d'un étudiant.
- **U - Update (Modifier)** : Mettre à jour des données existantes. Exemple : Modifier le crédit d'un étudiant après un achat ou changer le prix d'un produit.
- **D - Delete (Supprimer)** : Retirer des données de la base. Exemple : Supprimer un produit qui n'est plus disponible ou retirer un étudiant inactif.

Dans votre application Django, vous implémenterez ces opérations pour gérer les étudiants, les produits et les transactions de la cafétéria.

## Etape 3 : Architecture Model / View / Template

Django suit l'architecture **MVT (Model-View-Template)**, une variante du pattern MVC (Model-View-Controller). Voici une explication de chaque composant et leur lien avec les fichiers Django :

- **Model (Modèle)** : Représente les données de votre application. Les modèles définissent la structure des tables de la base de données.  
  - **Fichier associé** : `models.py` (ex. : `cafeteria_app/models.py`)  
  - **Rôle** : Créer, lire, mettre à jour et supprimer des données (CRUD). Exemple : La classe `Student` définit les champs comme `name`, `email`, `credit`.

- **View (Vue)** : Gère la logique métier et traite les requêtes HTTP. Les vues décident quoi afficher et comment.  
  - **Fichier associé** : `views.py` (ex. : `cafeteria_app/views.py`)  
  - **Rôle** : Récupérer des données depuis les modèles, les traiter, et les passer aux templates. Exemple : Une vue pour afficher la liste des étudiants.

- **Template (Gabarit)** : Gère la présentation et l'affichage des données à l'utilisateur.  
  - **Fichier associé** : Dossier `templates/` (ex. : `cafeteria_app/templates/`) contenant des fichiers HTML.  
  - **Rôle** : Mélanger HTML avec des variables dynamiques (via le langage de template Django). Exemple : Un template pour afficher une liste d'étudiants avec Bootstrap.

Dans Django, le "Controller" est géré par le framework lui-même (URLs, settings), laissant le développeur se concentrer sur M, V et T. Cette architecture sépare clairement les préoccupations : données, logique et présentation.

### Modèle (Model) : Déjà réalisé

Les modèles `Student`, `Product` et `Transaction` ont été créés et enregistrés dans l'admin lors des étapes précédentes. Ils définissent la structure de vos données.

### Vue (View) : Exercice - Lister tous les produits disponibles

Pour cet exercice, créez une vue qui affiche la liste de tous les produits qui peuvent être vendus (c'est-à-dire où `available = True`).

**Étapes à suivre :**

1. **Ouvrez `views.py`** : Dans `cafeteria_app/views.py`, importez les modules nécessaires :
   ```python
   from django.shortcuts import render
   from .models import Product
   ```

2. **Créez une fonction vue** :
   ```python
   def product_list(request):
       products = Product.objects.filter(available=True)
       return render(request, 'product_list.html', {'products': products})
   ```

3. **Configurez l'URL** : Dans `cafeteria/urls.py`, ajoutez :
   ```python
   from cafeteria_app.views import product_list

   urlpatterns = [
       path('admin/', admin.site.urls),
       path('products/', product_list, name='product_list'),
   ]
   ```

4. **Créez le template** : Dans `cafeteria_app/templates/product_list.html` :
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>Liste des Produits</title>
       <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
   </head>
   <body>
       <div class="container mt-5">
           <h1>Produits Disponibles</h1>
           <table class="table table-striped">
               <thead>
                   <tr>
                       <th>Nom</th>
                       <th>Prix</th>
                   </tr>
               </thead>
               <tbody>
                   {% for product in products %}
                   <tr>
                       <td>{{ product.name }}</td>
                       <td>{{ product.price }} €</td>
                   </tr>
                   {% endfor %}
               </tbody>
           </table>
       </div>
   </body>
   </html>
   ```

5. **Testez** : Lancez le serveur avec `python manage.py runserver` et allez sur http://127.0.0.1:8000/products/.

### Template (Gabarit) : Proposition de base

Le template ci-dessus est un exemple simple utilisant Bootstrap pour styliser une table HTML. Il utilise la syntaxe de template Django (`{% for %}`, `{{ }}`) pour afficher dynamiquement les données passées par la vue.

## Etape 4 : Généralisation des Model / View / Template

#### Configuration du fichier urls.py
Expression Regex

#### Détail des données récupérees : **request**

#### Intégration des données de la view vers le template

Dans Django, les vues envoient des données aux templates via la fonction `render()`. Par exemple, `return render(request, 'template.html', {'variable': valeur})` passe un dictionnaire de contexte au template.

Les syntaxes les plus utilisées pour accéder et afficher ces données dans les templates sont les suivantes :

- **Affichage de variables simples** : Utilisez `{{ variable }}` pour afficher la valeur d'une variable.  
  Exemple : Si la vue passe `{'message': 'Bonjour le monde'}`, dans le template : `<p>{{ message }}</p>` affiche "Bonjour le monde".

- **Boucles pour listes ou querysets** : Utilisez `{% for item in liste %} ... {% endfor %}` pour itérer sur une collection.  
  Exemple : Pour une liste de produits `{'products': products}`, dans le template :  
  ```html
  <ul>
  {% for product in products %}
      <li>{{ product.name }} - {{ product.price }} €</li>
  {% endfor %}
  </ul>
  ```

- **Conditions** : Utilisez `{% if condition %} ... {% endif %}` pour afficher du contenu conditionnellement.  
  Exemple : `{% if products %}Il y a des produits disponibles.{% else %}Aucun produit.{% endif %}`

- **Accès aux attributs d'objets** : Pour les objets modèles, accédez aux champs avec le point : `{{ object.champ }}`.  
  Exemple : `{{ student.name }}` pour afficher le nom d'un étudiant.

- **Filtres** : Appliquez des filtres avec `{{ variable|filtre }}`, comme `{{ date|date:"d/m/Y" }}` pour formater une date.

- **Inclusion d'autres templates** : Utilisez `{% include 'partial.html' %}` pour inclure des templates partiels. Très utilisé pour travailler sur le corps d'une page HTML avec appelé automatique l'entête et le pieds de pages.

- **Liens vers URLs** : Utilisez `{% url 'nom_url' %}` pour générer des URLs dynamiques.

Ces syntaxes permettent de rendre les templates dynamiques en intégrant les données envoyées par les vues.

## Etape 5 : Opération CRUD, GET/POST

Dans cette étape, nous allons implémenter les opérations CRUD (Create, Read, Update, Delete) pour gérer les étudiants, produits et transactions. Nous utiliserons les méthodes HTTP GET et POST pour différencier les requêtes de lecture et d'écriture.

### Différence entre GET et POST

- **GET** : Utilisé pour récupérer des données. Les paramètres sont passés dans l'URL (ex. : `?id=1`). Les données sont visibles dans l'URL, ce qui n'est pas idéal pour les informations sensibles. GET est idempotent (peut être répété sans effet secondaire).

- **POST** : Utilisé pour envoyer des données au serveur (ex. : formulaires). Les données sont dans le corps de la requête, invisibles dans l'URL. POST n'est pas idempotent et est utilisé pour créer ou modifier des ressources.

#### urls.py pour la redirection automatique

Pour gérer les URLs, modifiez `cafeteria/urls.py` pour inclure les vues CRUD :

```python
from django.urls import path
from cafeteria_app import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.home, name='home'),
    path('students/', views.student_list, name='student_list'),
    path('students/add/', views.student_add, name='student_add'),
    path('students/<int:pk>/edit/', views.student_edit, name='student_edit'),
    path('students/<int:pk>/delete/', views.student_delete, name='student_delete'),
    # Ajoutez pour products et transactions
]
```

**Explication des paramètres d'URL :**  
- `<int:pk>` : Capture un entier (id primaire) dans l'URL. `pk` est le nom du paramètre passé à la vue (ex. : `views.student_edit(request, pk=1)`).  
- **Syntaxes possibles pour les convertisseurs de chemin :**  
  - `<int:variable>` : Entier (ex. : 123).  
  - `<str:variable>` : Chaîne non vide (ex. : 'hello').  
  - `<slug:variable>` : Slug (lettres, chiffres, tirets, ex. : 'my-post').  
  - `<uuid:variable>` : UUID (ex. : '12345678-1234-5678-9012-123456789012').  
  - `<path:variable>` : Chemin avec slashes (ex. : 'folder/subfolder/file').  
  Ces convertisseurs valident et convertissent automatiquement les valeurs passées à la vue.

#### Conditions

Dans les vues, utilisez des conditions pour vérifier les méthodes HTTP :

```python
def student_add(request):
    if request.method == 'POST':
        # Traiter le formulaire
        form = StudentForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('student_list')
    else:
        form = StudentForm()
    return render(request, 'student_form.html', {'form': form})
```
### Les autres types de requêtes

- **PUT** : Pour mettre à jour une ressource complète.
- **PATCH** : Pour mettre à jour partiellement.
- **DELETE** : Pour supprimer une ressource.

Django gère principalement GET et POST, mais vous pouvez utiliser des bibliothèques comme Django REST Framework pour les autres.

### Automatisation des formulaires avec Django

Django fournit `ModelForm` pour automatiser la création de formulaires basés sur les modèles :

```python
from django import forms
from .models import Student

class StudentForm(forms.ModelForm):
    class Meta:
        model = Student
        fields = ['name', 'email', 'credit']
```

Utilisez ce formulaire dans les vues et templates pour simplifier le CRUD.

#### Exercice : Créer une page pour ajouter un nouvel étudiant

**Objectif :** Implémentez une page web permettant d'ajouter un nouvel étudiant à la base de données en utilisant un formulaire automatique généré par Django.

**Étapes à suivre :**

1. **Créer le ModelForm** : Dans `cafeteria_app/forms.py` (créez le fichier si nécessaire), définissez `StudentForm` comme indiqué ci-dessus.

2. **Modifier la vue** : Dans `views.py`, implémentez la fonction `student_add` pour gérer GET (afficher le formulaire vide) et POST (valider et sauvegarder).

3. **Créer le template** : Créez `student_form.html` qui étend `base.html` et utilise `{{ form.as_p }}` pour afficher le formulaire automatiquement.

4. **Configurer l'URL** : Assurez-vous que l'URL `students/add/` pointe vers `student_add`.

5. **Tester** : Lancez le serveur, allez sur `/students/add/`, remplissez et soumettez le formulaire. Vérifiez que l'étudiant est ajouté en base.

**Analyse du code HTML généré :**  
Après avoir créé le formulaire, inspectez le code HTML généré dans le navigateur (clic droit > Inspecter). Analysez :
- Les balises `<form>`, `<input>`, `<label>` créées automatiquement.
- Les attributs `name`, `id`, `type` des champs.
- Le token CSRF ajouté pour la sécurité.
- Comment Django gère les erreurs de validation (essayez de soumettre un formulaire invalide).
- Comparez avec un formulaire HTML manuel pour voir les avantages de `ModelForm`.

**Questions d'analyse :**
- Quels sont les avantages d'utiliser `ModelForm` par rapport à un formulaire HTML manuel ?
- Comment Django valide-t-il les données côté serveur ?
- Que se passe-t-il si le formulaire n'est pas valide (données non conforme au type défini dans le modèle) ?

## Etape 6 : Mise en forme, Architecture des fichiers

Pour rendre l'application moderne et responsive, nous utiliserons HTML, CSS avec Bootstrap, et JavaScript. Nous organiserons les fichiers statiques correctement.

### HTML : HyperText Markup Language pour la structure et le contenu

HTML est le langage de balisage standard pour créer des pages web. Il définit la structure et le contenu d'une page (titres, paragraphes, liens, images) à l'aide de balises comme `<h1>`, `<p>`, `<a>`. Dans Django, les templates utilisent HTML pour afficher les données dynamiques.

Créez un template de base `base.html` dans `cafeteria_app/templates/base.html` :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>{% block title %}Cafétéria{% endblock %}</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    {% block extra_head %}{% endblock %}
</head>
<body>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container">
            <a class="navbar-brand" href="{% url 'home' %}">Cafétéria</a>
            <!-- Menu -->
        </div>
    </nav>
    <div class="container mt-4">
        {% block content %}{% endblock %}
    </div>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    {% block extra_js %}{% endblock %}
</body>
</html>
```

Utilisez `{% extends 'base.html' %}` dans les autres templates pour importer cette base.

### CSS : Cascading Style Sheets pour le style

CSS (Cascading Style Sheets) est un langage pour styliser les pages web. Il contrôle l'apparence (couleurs, polices, mises en page) des éléments HTML. Bootstrap est un framework CSS populaire pour créer des interfaces responsive et modernes sans coder from scratch.

Bootstrap fournit un framework CSS responsive. Pour des styles personnalisés, créez `static/css/style.css` et incluez-le avec `{% load static %}` puis `<link rel="stylesheet" href="{% static 'css/style.css' %}">`.

### JS : Javascript pour le dynamisme

JavaScript est un langage de programmation pour ajouter de l'interactivité aux pages web (animations, validations, requêtes AJAX). Il s'exécute côté client dans le navigateur. Bootstrap inclut des composants JS pour des éléments interactifs comme les modales ou les carrousels.

Pour l'interactivité, ajoutez JavaScript. Par exemple, pour confirmer une suppression :

```javascript
function confirmDelete() {
    return confirm('Êtes-vous sûr de vouloir supprimer ?');
}
```

Incluez-le dans `{% block extra_js %}`.

### Implémentation sous Django et arborescence : Fichiers statiques

- Créez le dossier `static/` à la racine de l'app.
- Dans `settings.py`, ajoutez `'django.contrib.staticfiles'` et configurez `STATIC_URL = '/static/'`.
- En développement, Django sert les fichiers statiques automatiquement.
- En production, utilisez `python manage.py collectstatic` pour les collecter.

#### Exercice : Intégrer un template Bootstrap gratuit

**Objectif :** Trouver et intégrer un template Bootstrap gratuit dans votre projet Django, en plaçant les fichiers au bon endroit, et personnaliser l'en-tête et le pied de page. Ajouter également des images correctement.

**Étapes à suivre :**

1. **Trouver un template gratuit :**
   - Rendez-vous sur des sites comme [Start Bootstrap](https://startbootstrap.com/), [BootstrapMade](https://bootstrapmade.com/), ou [Free Bootstrap Templates](https://www.free-css.com/free-css-templates).
   - Choisissez un template simple et moderne (ex. : "SB Admin" ou "Creative").
   - Téléchargez l'archive ZIP du template.

2. **Analyser la structure du template :**
   - Ouvrez l'archive : vous trouverez généralement des dossiers `css/`, `js/`, `img/`, et des fichiers HTML.
   - Identifiez le fichier HTML principal (souvent `index.html`).

3. **Intégrer dans Django :**
   - Créez le dossier `static/` dans `cafeteria_app/` si ce n'est pas déjà fait.
   - Copiez les dossiers `css/`, `js/`, `img/` du template dans `cafeteria_app/static/`.
   - Pour les images : Placez-les dans `cafeteria_app/static/img/`. Utilisez `{% static 'img/mon-image.jpg' %}` dans les templates pour les référencer.
   - Modifiez `base.html` pour inclure les CSS et JS du template au lieu de Bootstrap CDN. Exemple :
     ```html
     <link href="{% static 'css/styles.css' %}" rel="stylesheet">
     <script src="{% static 'js/scripts.js' %}"></script>
     ```

4. **Personnaliser l'en-tête et le pied de page :**
   - Copiez la structure HTML de l'en-tête et du pied de page du template dans `base.html`.
   - Adaptez les liens de navigation : Utilisez `{% url 'home' %}` pour les liens internes.
   - Ajoutez du contenu dynamique : Intégrez des blocs comme `{% if user.is_authenticated %}` pour afficher le nom de l'utilisateur.
   - Pour les images dans l'en-tête/pied : Utilisez `<img src="{% static 'img/logo.png' %}" alt="Logo">`.

5. **Gérer les fichiers statiques :**
   - Assurez-vous que `{% load static %}` est au début de `base.html`.
   - En développement, les fichiers sont servis automatiquement.
   - Testez en lançant `python manage.py runserver` et vérifiez que les styles et images se chargent.

6. **Ajouter des images personnalisées :**
   - Placez vos propres images (ex. : logo ENSEA) dans `static/img/`.
   - Référencez-les dans les templates avec `{% static 'img/logo.png' %}`.
   - Pour les images dynamiques (uploadées par utilisateurs), utilisez `MEDIA_URL` et `MEDIA_ROOT` dans `settings.py`, et servez-les via une vue ou un serveur statique.

**Conseils :**
- Choisissez un template responsive pour une bonne expérience mobile.
- Vérifiez la compatibilité avec la version de Bootstrap utilisée (actuellement 5.x).
- Si le template utilise des polices Google, incluez-les via `<link>` dans le `<head>`.
- Testez sur différents navigateurs et tailles d'écran.

**Questions d'analyse :**
- Quels sont les avantages d'utiliser un template pré-conçu par rapport à coder le HTML/CSS from scratch ?
- Comment Django gère-t-il les fichiers statiques en développement vs production ?
- Pourquoi est-il important de placer les images dans le bon dossier ?

## Etape 7 : Plug-in Django

### Principe d'authentification, intégration du CAS ENSEA
Django fournit un système d'authentification intégré. Pour l'ENSEA, nous intégrerons le CAS (Central Authentication Service). Ainsi tous les utilisateurs pourront avoir accès à votre application sans devoir les créer à la main.

**Qu'est-ce qu'un serveur CAS ?**  
CAS (Central Authentication Service) est un protocole d'authentification unique (Single Sign-On) qui permet aux utilisateurs de se connecter une fois et d'accéder à plusieurs applications sans se reconnecter. Le serveur CAS gère l'authentification centralisée, vérifie les identifiants, et délivre des tickets pour autoriser l'accès aux services. Pour l'ENSEA, il utilise les comptes étudiants au format "4 lettres du prénom + 4 lettres du nom + 2 chiffres".

#### Authentification de base
- Utilisez `django.contrib.auth` pour les utilisateurs.
- Créez des vues de login/logout avec `LoginView` et `LogoutView`.
- Protégez les vues avec `@login_required`.

Exemple d'utilisation du décorateur :

```python
from django.contrib.auth.decorators import login_required

@login_required
def student_list(request):
    # Vue protégée, accessible seulement aux utilisateurs connectés
    ...
```

#### Intégration CAS
Depuis votre environnement, installez `django-cas-ng` :

```bash
pip install django-cas-ng
```

Dans `settings.py` :

```python
INSTALLED_APPS = [
    # ...
    'django_cas_ng',
]


CAS_SERVER_URL = 'https://identites.ensea.fr/cas/' # URL du serveur CAS de l'école
CAS_LOGIN_URL_NAME = 'cas_ng_login'
CAS_LOGOUT_URL_NAME = 'cas_ng_logout'
```

Dans `urls.py` :

```python
from django_cas_ng import views as cas_views

urlpatterns = [
    # ...
    path('accounts/login/', cas_views.login, name='cas_ng_login'),
    path('accounts/logout/', cas_views.logout, name='cas_ng_logout'),
]
```

Cela permet l'authentification via le CAS de l'ENSEA.

**Remarque :**

L'évolution de ce plugin est assez rapide, il se peut que cette configuration ne suffise pas, il faudrait éventuellement la compléter. N'hésiter pas à fouiller le web et la documentation officiel Django. Si le problème persiste, appelez votre enseignant.

### Import/export en masse : Django import-export
Le plugin `django-import-export` permet d'importer/exporter des données en CSV, XLS, etc.
- Depuis votre environnement, installez : `pip install django-import-export`.
- Dans `settings.py` : Ajoutez `'import_export'` à `INSTALLED_APPS`.
- Dans `admin.py`, modifier de la façon suivante votre code pour permettre l'accès au plugin d'import-export à vos modèles  :

```python
from import_export.admin import ImportExportModelAdmin
from .models import Student

@admin.register(Student)
class StudentAdmin(ImportExportModelAdmin):
    pass
```

Cela ajoute des boutons Import/Export dans l'admin pour gérer les données en masse.

## Etape 8 : Compréhension de la stack TCP/IP

### Le modèle OSI (Open Systems Interconnection)

Le modèle OSI est un cadre conceptuel standardisé décrivant comment les systèmes informatiques communiquent sur un réseau. Il divise les fonctions réseau en 7 couches hiérarchiques, de la plus basse (physique) à la plus haute (application). Chaque couche communique uniquement avec les couches adjacentes.

#### Couches du modèle OSI

1. **Couche Physique (Layer 1)** : Gère la transmission brute des bits sur le support physique (câbles, ondes radio). Définit les caractéristiques électriques, mécaniques et procédurales. Exemples : Ethernet, Wi-Fi, Bluetooth.

2. **Couche Liaison de données (Layer 2)** : Assure la transmission fiable des données entre deux nœuds directement connectés. Gère l'adressage physique (MAC), la détection d'erreurs, et le contrôle d'accès au média. Protocoles : Ethernet, PPP, Wi-Fi.

3. **Couche Réseau (Layer 3)** : Gère le routage des paquets à travers le réseau. Utilise des adresses logiques (IP) pour atteindre des destinations distantes. Protocoles : IP, ICMP, OSPF.

4. **Couche Transport (Layer 4)** : Assure la livraison fiable des données de bout en bout. Gère la segmentation, le contrôle de flux, et la correction d'erreurs. Protocoles : TCP, UDP.

5. **Couche Session (Layer 5)** : Établit, gère et termine les sessions de communication entre applications. Protocoles : NetBIOS, RPC.

6. **Couche Présentation (Layer 6)** : Traduit les données entre le format réseau et le format application (encodage, chiffrement, compression). Exemples : JPEG, ASCII, SSL/TLS.

7. **Couche Application (Layer 7)** : Interface directe avec les applications utilisateur. Fournit des services réseau aux programmes. Protocoles : HTTP, FTP, SMTP, DNS.

#### Comparaison avec TCP/IP

Le modèle TCP/IP, utilisé dans Internet, simplifie OSI en 4 couches :
- **Réseau d'accès** (équivalent Layers 1-2 OSI) : Couche Physique + Liaison.
- **Internet** (Layer 3 OSI) : Routage IP.
- **Transport** (Layer 4 OSI) : TCP/UDP.
- **Application** (Layers 5-7 OSI) : HTTP, etc.

TCP/IP est plus pratique que OSI, mais OSI reste une référence pédagogique.

### Layer 1 : Couche Physique

La couche physique gère la transmission brute des bits sur le support physique. Elle définit comment les signaux électriques, optiques, ou radio sont convertis en bits.

#### Supports de transmission
- **Câble Ethernet (Twisted Pair)** : Câbles UTP/STP pour connexions filaires. Catégories : Cat5e, Cat6, Cat6a (plus rapide = plus cher). Distance maximale : ~100m.
- **Fibre optique** : Transmission par lumière, très rapide (10 Gbps+), haute portée (plusieurs km), immun aux interférences.
- **Wi-Fi** : Ondes radio sans fil, portée limitée (~50m), plus lent qu'Ethernet, pratique pour la mobilité.
- **Cable coaxial** : Rarement utilisé aujourd'hui, anciennement pour le TV câblée.

#### Signaux et bits
- Les données sont représentées par des voltages électriques (par ex., +5V = bit 1, 0V = bit 0).
- En Wi-Fi, des modulations radio codent les bits.
- La fréquence d'horloge détermine la vitesse (ex. : 1 Gbps = 1 milliard de bits/sec).

#### Matériel Layer 1
- **Hub** : Répète les signaux reçus sur tous les ports (rarement utilisé). Crée une collision si plusieurs appareils envoient simultanément.
- **Répéteur** : Amplifie les signaux pour augmenter la portée.

#### Exemple concret
Quand vous branchez un câble Ethernet, les bits du signal du serveur voyagent par impulsions électriques à travers le câble jusqu'à votre ordinateur.

### Layer 2 : Liaison de données

La couche 2 assure la communication fiable entre deux appareils directement connectés sur le même réseau local (LAN). Elle utilise l'adresseage MAC (Media Access Control).

#### Adresse MAC en détail

Une adresse MAC est un identifiant unique de 48 bits (6 octets) attribué à chaque interface réseau. Elle s'écrit en notation hexadécimale : `XX:XX:XX:XX:XX:XX`.

**Structure de l'adresse MAC :**
- **3 premiers octets (24 bits)** : OUI (Organizationally Unique Identifier) - Identifie le fabricant. Exemples :
  - `00:1A:2B` = Intel
  - `00:0A:95` = Apple
  - `00:50:F2` = Microsoft
- **3 derniers octets (24 bits)** : Numéro de série unique de l'interface (NIC) chez ce fabricant.

**Exemple :** `00:1B:44:11:3A:B7`
- `00:1B:44` = Constructeur (par ex., Cisco)
- `11:3A:B7` = Numéro d'interface unique

#### Communication Layer 2 - Trame Ethernet
Les données sont encapsulées dans des **trames Ethernet** :
```
[MAC dest | MAC source | Type | Données | CRC]
```
- Le commutateur utilise les adresses MAC source/destination pour transmettre.
- Chaque appareil a une adresse MAC unique ; les autres l'ignorent.

#### Switch (matériel Layer 2)
Un **switch** (commutateur) connecte plusieurs appareils sur un LAN. Il mémorise une **table MAC** (MAC Address Table) :

| Port | Adresse MAC |
|------|-------------|
| 1    | 00:1B:44:11:3A:B7 |
| 2    | 00:0A:95:22:4C:D3 |
| 3    | 00:50:F2:33:5D:E4 |

Quand il reçoit une trame, il regarde l'adresse MAC destination et l'envoie uniquement au port correspondant (unicast), pas à tous les ports (contrairement au hub).

**Broadcast** : Si la MAC destination est `FF:FF:FF:FF:FF:FF`, le switch envoie à tous les ports.

#### Exemple concret
Votre PC (MAC: A) envoie un message au serveur (MAC: B).
1. Votre PC crée une trame Ethernet avec : MAC source = A, MAC destination = B, Données
2. Le switch regarde le tableau MAC, trouve que la MAC B est sur le port 5
3. Le switch envoie la trame seulement au port 5 (efficace, pas d'interférence)

### Layer 3 : IPv4 (Réseau)
La couche 3 permet la communication entre réseaux distants en utilisant des adresses logiques (adresses IP). Elle gère le routage des paquets.

#### Notions binaire et hexadécimale
- **Binaire** : Base 2 (0 et 1). Ex. : `11111111` = 255 en décimal.
- **Décimale** : Base 10 (0-9). Ex. : 255.
- **Hexadécimale** : Base 16 (0-9, A-F). Ex. : `FF` en hex = 255 en décimal.
  - `0` = 0000 (binaire)
  - `1` = 0001
  - `F` = 1111
  - `FF` = 11111111 = 255

Conversion : `0x1A` (hex) = 1×16¹ + 10×16⁰ = 26 (décimal).

#### Adresse IPv4 en détail

Une adresse IPv4 est un nombre de 32 bits divisé en 4 octets, notés en **décimal pointé** : `192.168.1.100`.

**Conversion binaire ↔ décimal :**
- `192.168.1.100` en binaire :
  - 192 = 11000000
  - 168 = 10101000
  - 1 = 00000001
  - 100 = 01100100
  - **Binaire complet** : `11000000.10101000.00000001.01100100`

Chaque octet varie de 0 à 255 (2⁸ = 256 valeurs).

#### Masque de sous-réseau (Netmask)

Le masque définit quelle partie de l'adresse IP est l'adresse réseau et quelle partie est l'adresse d'hôte.

- **Notation décimale pointée** : `255.255.255.0`
- **Notation CIDR** : `/24` (nombre de bits réseau)

**Classe d'adresses courantes :**
| Classe | Masque | CIDR | Plage | Supports | Hosts |
|--------|--------|------|-------|----------|-------|
| A | 255.0.0.0 | /8 | 1.0.0.0 - 126.255.255.255 | 126 | ~16M |
| B | 255.255.0.0 | /16 | 128.0.0.0 - 191.255.255.255 | 16K | ~65K |
| C | 255.255.255.0 | /24 | 192.0.0.0 - 223.255.255.255 | 2M | 254 |

**Calcul du masque :**
Pour un masque `/24` :
- 24 bits = 1 pour le réseau, 8 bits = 0 pour les hôtes
- `11111111.11111111.11111111.00000000` = `255.255.255.0`

Pour `/25` :
- 25 bits réseau, 7 bits hôtes
- `11111111.11111111.11111111.10000000` = `255.255.255.128`

#### Adresse réseau, adresse de broadcast, plage d'hôtes

Exemple : `192.168.1.100/24` (masque `255.255.255.0`)

- **Adresse réseau** : Tous les bits hôtes à 0 → `192.168.1.0`
- **Adresse de broadcast** : Tous les bits hôtes à 1 → `192.168.1.255`
- **Plage d'hôtes utilisables** : `192.168.1.1` à `192.168.1.254` (254 adresses)
- L'hôte `.0` est le réseau, `.255` est le broadcast

**Comment calculer :**
1. Convertir l'IP et le masque en binaire.
2. Appliquer un AND binaire : Bit IP AND Bit Masque.
3. Résultat = Adresse réseau.

Exemple : `192.168.1.100` AND `255.255.255.0`
```
IP:     11000000.10101000.00000001.01100100
Mask:   11111111.11111111.11111111.00000000
Réseau: 11000000.10101000.00000001.00000000 = 192.168.1.0
```

#### Routeur (matériel Layer 3)

Un **routeur** relie plusieurs réseaux et dirige les paquets entre eux en fonction des adresses IP.

**Table de routage :** Carte des réseaux accessibles et des chemins pour les atteindre.

| Destination | Masque | Passerelle (Gateway) | Interface |
|-------------|--------|----------------------|-----------|
| 192.168.1.0 | 255.255.255.0 | 0.0.0.0 (Direct) | eth0 |
| 10.0.0.0 | 255.255.255.0 | 192.168.1.1 | eth0 |
| 0.0.0.0 | 0.0.0.0 | 192.168.1.254 (Défaut) | eth0 |

**Processus de routage :**
1. Le routeur reçoit un paquet IP avec destination `10.0.0.5`.
2. Il cherche dans sa table de routage quel réseau correspond.
3. Il envoie le paquet au prochain saut (hop) via la passerelle indiquée.

#### Réseaux privés et adresses réservées

Les adresses IP privées ne sont pas routées sur Internet :
- **Classe A privée** : `10.0.0.0/8` (10.0.0.0 à 10.255.255.255)
- **Classe B privée** : `172.16.0.0/12` (172.16.0.0 à 172.31.255.255)
- **Classe C privée** : `192.168.0.0/16` (192.168.0.0 à 192.168.255.255)

Ces plages sont utilisées dans les réseaux locaux (LAN) derrière un NAT (Network Address Translation). Cette notion de classe est obselète, mais les /8, /16 et /24 sont encore massivement utiliés.

#### Exemple concret

Réseau cafétéria : `192.168.100.0/24`
- Serveur : `192.168.100.10`
- Client 1 : `192.168.100.50`
- Client 2 : `192.168.100.75`
- Broadcast : `192.168.100.255`
- Gateway (sortie Internet) : `192.168.100.1`

Pour communiquer, tous les appareils doivent avoir le même masque `/24` et des IPs dans cette plage.

#### Exercice : Analyser les réseaux locaux (Eduroam et salle)

**Objectif :** Explorez les configurations réseau réelles du campus (Eduroam) et de la salle de TP, analysez les paramètres IPv4/IPv6, identifiez la passerelle, et calculez la taille des réseaux.

**Étapes à suivre :**

1. **Sur Linux (Ubuntu/Debian) :**
   Ouvrez un terminal et exécutez :
   ```bash
   ip a
   ```

   **Exemple de sortie :**
   ```
   1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536
       inet 127.0.0.1/8 scope host lo
   
   2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500
       inet 172.23.45.128/19 brd 172.23.63.255 scope global dynamic eth0
       inet6 fe80::a00:27ff:fe4e:66a1/64 scope link
   
   3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500
       inet 192.168.50.75/24 brd 192.168.50.255 scope global dynamic wlan0
       inet6 2001:db8::1/64 scope global
   ```

   **Exemple avec un masque inhabituel (/19) :**
   ```
   inet 172.23.45.128/19 brd 172.23.63.255 scope global dynamic eth0
   ```

   **Analyse :**
   - **Adresse IP** : `172.23.45.128`
   - **Masque** : `/19` = `255.255.224.0`
   - **Adresse réseau** : `172.23.32.0` (calcul : 45 en binaire 00101101, /(19) laisse les 5 derniers bits, donc 00100000 = 32)
   - **Adresse de broadcast** : `172.23.63.255`
   - **Nombre d'hôtes** : 2^(32-19) - 2 = 2^13 - 2 = 8190 machines possibles
   - **Plage d'IP** : `172.23.32.1` à `172.23.63.254`

2. **Trouver la passerelle (Gateway) :**
   ```bash
   ip route
   ```
   **Exemple complet de sortie `ip route` :**
   ```
   default via 192.168.1.1 dev eth0 proto dhcp metric 100
   172.23.0.0/16 via 192.168.0.1 dev wlan0 proto static metric 50
   192.168.1.0/24 dev eth0 proto dhcp scope link metric 100
   192.168.50.0/24 dev wlan0 proto dhcp scope link metric 600
   169.254.0.0/16 dev eth0 scope link metric 1002
   ```

   **Décodage ligne par ligne :**

   | Ligne | Destination | Via (Passerelle) | Interface | Type | Priorité |
   |------|-------------|------------------|-----------|------|----------|
   | 1 | Toute destination (défaut) | 192.168.1.1 | eth0 | DHCP | 100 |
   | 2 | Réseau 172.23.0.0/16 | 192.168.0.1 | wlan0 | Static | 50 |
   | 3 | Réseau 192.168.1.0/24 (local) | Direct (pas de via) | eth0 | DHCP | 100 |
   | 4 | Réseau 192.168.50.0/24 (local) | Direct | wlan0 | DHCP | 600 |
   | 5 | Link-local (169.254.0.0/16) | Direct | eth0 | - | 1002 |

   **Comprendre chaque colonne :**
   - **Destination** : Réseau ou adresse cible.
   - **via** : Passerelle (routeur intermédiaire). Si absent = communication directe (réseau local).
   - **dev** : Interface réseau utilisée (eth0, wlan0, etc.).
   - **proto** (protocole) : `dhcp` (attribué dynamiquement), `static` (manuel), `kernel`, etc.
   - **metric** : Priorité (plus bas = plus prioritaire). Pour choisir entre plusieurs chemins.
   - **scope** : `link` = réseau local, `global` = peut être atteint via n'importe quelle interface.

   **Règles de routage :**
   1. Chercher la destination la plus précise (plus de bits de masque).
   2. Utiliser la route `default` si aucune correspondance.
   3. Si plusieurs routes ont la même spécificité, utiliser celle avec le plus bas `metric`.

   **Exemple d'utilisation :**
   - Pour atteindre `8.8.8.8` (Google DNS) : Aucune route spécifique ne le cible → Utiliser `default via 192.168.1.1` → Passer par le routeur `192.168.1.1`.
   - Pour atteindre `192.168.1.50` : Route exacte `192.168.1.0/24` via `eth0` → Communication directe (pas de passerelle).
   - Pour atteindre `172.23.5.100` : Correspond à `172.23.0.0/16` → Passer par `192.168.0.1` sur `wlan0`.

3. **Analyser les deux réseaux :**

   **Réseau Eduroam (Wi-Fi du campus) :**
   - Exécutez `ip a` et identifiez l'interface Wi-Fi (souvent `wlan0`).
   - Noter l'adresse IP, le masque (CIDR).
   - Calculer l'adresse réseau et de broadcast.
   - Exécutez `ip route` pour trouver la passerelle.
   - Calculer le nombre de machines possibles dans ce réseau.

   **Réseau local de la salle (connecté via câble Ethernet) :**
   - Exécutez `ip a` et identifiez l'interface Ethernet (souvent `eth0`).
   - Répétez les mêmes analyses.

4. **Remplir le tableau comparatif :**

   | Paramètre | Eduroam (Wi-Fi) | Salle (Ethernet) |
   |-----------|-----------------|------------------|
   | Interface | wlan0 | eth0 |
   | Adresse IP | X.X.X.X | Y.Y.Y.Y |
   | Masque CIDR | /XX | /YY |
   | Adresse réseau | | |
   | Adresse broadcast | | |
   | Passerelle | | |
   | Nombre d'hôtes max | | |
   | Plage d'IPs | à | à |

5. **Alternative sous Windows :**
   Ouvrez l'Invite de Commandes (cmd) ou PowerShell et exécutez :
   ```powershell
   ipconfig /all
   ```

   **Exemple de sortie :**
   ```
   Carte Ethernet :
      Adresse IPv4 . . . . . . . . : 192.168.1.100
      Masque de sous-réseau . . . : 255.255.255.0
      Passerelle par défaut . . . : 192.168.1.1
   
   Carte réseau sans fil (Wi-Fi) :
      Adresse IPv4 . . . . . . . . : 172.23.45.128
      Masque de sous-réseau . . . : 255.255.224.0
   ```

   Pour un affichage plus détaillé sur Windows (équivalent à `ip route` sous Linux) :
   ```cmd
   route print
   ```

6. **Analyse et calculs :**

   **Exemple avec le masque /19 :**
   ```
   IP: 172.23.45.128/19
   Masque décimal: 255.255.224.0
   
   Binaire masque: 11111111.11111111.11100000.00000000
   Les 19 premiers bits (1) = réseau
   Les 13 derniers bits (0) = hôtes
   
   Calcul de l'adresse réseau:
   IP:      10101100.00010111.00101101.10000000
   Masque:  11111111.11111111.11100000.00000000
   Réseau:  10101100.00010111.00100000.00000000 = 172.23.32.0
   
   Calcul du broadcast:
   Réseau avec tous les bits hôtes à 1:
   10101100.00010111.00111111.11111111 = 172.23.63.255
   
   Nombre d'adresses: 2^13 = 8192
   Nombre d'hôtes utilisables: 8192 - 2 = 8190
   (on soustrait l'adresse réseau et l'adresse broadcast)
   ```

**Questions pour aller plus loin :**
- Quel est le protocole utilisé pour que votre PC reçoive automatiquement une adresse IP ?
- Pourquoi certains réseaux utilisent-ils un masque /19 au lieu de /24 ?
- Quelle est la différence entre IPv4 et IPv6 ? (Vous verrez des adresses comme `fe80::1/64` pour IPv6)
- Pouvez-vous communiquer directement avec une machine sur le réseau Eduroam si vous êtes sur le réseau ethernet de la salle ? Pourquoi ?

**Conseils :**
- Les adresses commençant par `fe80::` sont des adresses link-local IPv6 (automatique).
- Les adresses commençant par `127.` (loopback) sont pour tester localement.
- Les réseaux du campus (Eduroam) sont souvent beaucoup plus grands que `/24` pour de l'ordre de `/16` ou `/19`.

#### Ports

Un **port** est un point de terminaison de communication sur un hôte, identifié par un nombre de 0 à 65535. Il permet à un ordinateur de distinguer plusieurs conversations simultanées.

**Socket = IP + Port + Protocole**  
Exemple : `192.168.1.100:8000/TCP` identifie de manière unique un service sur ce PC.

##### TCP vs UDP

Les protocoles TCP et UDP sont les deux principaux protocoles de la couche Transport (Layer 4). Ils gèrent différemment le transport des données.

**TCP (Transmission Control Protocol) :**
- **Connexion** : Établit une connexion avec 3-way handshake avant d'envoyer des données.
- **Fiabilité** : Garantit que tous les paquets arrivent dans l'ordre et sans erreur. Retransmet les paquets perdus.
- **Vitesse** : Plus lent en raison des vérifications.
- **Ordre** : Respecte l'ordre des paquets reçus.
- **Utilisation** : HTTP(S), SMTP, SSH, FTP, Telnet, MySQL, etc. (tous les services critiques).
- **Exemple** : `192.168.1.100:22/TCP` pour SSH.

| Caractéristique | TCP |
|-----------------|-----|
| Connexion | Oui (3-way handshake) |
| Fiabilité | Garantie |
| Ordre des données | Respecté |
| Vitesse | Normale (contrôle d'erreur) |
| Perte de paquets | Retransmission |

**UDP (User Datagram Protocol) :**
- **Connexion** : Pas de connexion préalable. EnvoieDirectement les données (connectionless).
- **Fiabilité** : Pas de garantie de livraison. Les paquets peuvent être perdus ou en désordre.
- **Vitesse** : Très rapide, pas de vérifications.
- **Ordre** : L'ordre n'est pas garanti.
- **Utilisation** : DNS, DHCP, SNMP, livestream vidéo/audio, jeux en ligne, appels VoIP (applications temps réel).
- **Exemple** : `192.168.1.100:53/UDP` pour DNS.

| Caractéristique | UDP |
|-----------------|-----|
| Connexion | Non (connectionless) |
| Fiabilité | Non garantie |
| Ordre des données | Non respecté |
| Vitesse | Très rapide (pas de contrôle) |
| Perte de paquets | Aucune retransmission |

**Comparaison visuelle :**

```
TCP (Fiable mais lent)
Client          Serveur
  │ SYN ────→ │  (Établir une connexion)
  │ ←──── SYN-ACK │
  │ ACK ────→ │  (Connexion établie)
  │ Données ────→ │  (Vérifié, retransmis si nécessaire)
  │ ←──── ACK │
  │ FIN ────→ │  (Fermer la connexion)
  │ ←──── FIN-ACK │

UDP (Rapide mais pas fiable)
Client          Serveur
  │ Données ────→ │  (Envoyé directement, pas de vérification)
  │ Données ────→ │  (Peut être perdu ou en désordre)
```

**Quand utiliser quoi :**

| Cas d'usage | Protocole | Raison |
|------------|-----------|--------|
| Télécharger un fichier | TCP | Chaque bit doit arriver correctement |
| Consulter une page web | TCP | Les données HTML doivent être intactes |
| Appel vidéo avec quelques pertes | UDP | La perte de 1-2% est tolérable, la vitesse compte |
| Jeu en ligne (position du joueur) | UDP | 1 paquet perdu = un léger lag, pas grave |
| Base de données distante | TCP | L'intégrité des données est critique |
| Streaming vidéo | UDP | Quelques images perdues sont acceptables |
| DNS | UDP | Léger, rapide. Si pas de réponse, on renvoit |

**Exemple réel - DNS sur UDP :**
```
Client: "Quelle est l'IP de google.com ?" (UDP:53)
Serveur: "8.8.8.8" (UDP:53)
```
2 paquets simples, pas de vérification. Très rapide.

**Exemple réel - HTTP sur TCP :**
```
Client établit connexion (TCP 3-way handshake)
Client: "GET / HTTP/1.1" 
Serveur: "HTTP/1.1 200 OK [page HTML]"
Client et serveur vérifient la réception
Connexion fermée proprement
```
Plus lent mais garantit la page complète.

##### Plages de ports

| Plage | Catégorie | Description |
|-------|-----------|-------------|
| 0-1023 | Ports réservés | Nécessitent des privilèges root/admin. Utilisés pour les services système (SSH, HTTP, etc.). |
| 1024-49151 | Ports enregistrés | Utilisés par les applications. Peuvent être ouverts par n'importe quel utilisateur. |
| 49152-65535 | Ports dynamiques/privés | Utilisés temporairement par les clients pour les connexions sortantes. Généralement pas ouverts en "écoute". |

##### Ports par défaut courants

| Port | Protocole | Service | Type |
|------|-----------|---------|------|
| 20/21 | TCP | FTP (Transfert de fichiers) | Serveur |
| 22 | TCP | SSH (Accès sécurisé distant) | Serveur |
| 23 | TCP | Telnet (Accès distant non sécurisé) | Serveur |
| 25 | TCP | SMTP (Envoi e-mail) | Serveur |
| 53 | TCP/UDP | DNS (Résolution de noms) | Serveur |
| 67/68 | UDP | DHCP (Attribution IP) | Serveur/Client |
| 80 | TCP | HTTP (Web) | Serveur |
| 110 | TCP | POP3 (Réception e-mail) | Serveur |
| 143 | TCP | IMAP (Réception e-mail) | Serveur |
| 443 | TCP | HTTPS (Web sécurisé) | Serveur |
| 3306 | TCP | MySQL (Base de données) | Serveur |
| 5432 | TCP | PostgreSQL (Base de données) | Serveur |
| 8000-8999 | TCP | Développement (Django, etc.) | Serveur |
| 3389 | TCP | RDP (Accès distant Windows) | Serveur |

##### Comment lister les ports ouverts

**Sur Linux :**

1. **Avec `netstat` (ancienne méthode, toujours disponible) :**
   ```bash
   netstat -tuln
   ```
   - `-t` : TCP
   - `-u` : UDP
   - `-l` : Écoute (LISTEN)
   - `-n` : Affiche les numéros, pas les noms (plus rapide)

   **Exemple de sortie :**
   ```
   Proto Recv-Q Send-Q Local Address         Foreign Address    State
   tcp        0      0 0.0.0.0:22            0.0.0.0:*          LISTEN
   tcp        0      0 127.0.0.1:8000        0.0.0.0:*          LISTEN
   tcp6       0      0 :::443                :::*               LISTEN
   udp        0      0 0.0.0.0:53            0.0.0.0:*
   udp        0      0 0.0.0.0:67            0.0.0.0:*
   ```

   **Interprétation :**
   - **Local Address** : Où le service écoute (IP:port).
   - **State** : `LISTEN` = en attente de connexion, `ESTABLISHED` = connexion active.
   - **0.0.0.0:22** = Écoute sur toutes les interfaces au port 22 (SSH).
   - **127.0.0.1:8000** = Écoute seulement localement (Django par défaut).

2. **Pour voir aussi les processus associés :**
   ```bash
   sudo netstat -tulnp
   ```
   ou
   ```bash
   sudo ss -tulnp
   ```
   L'option `-p` (PID/Program) affiche le processus. Nécessite `sudo`.

   **Exemple :**
   ```
   Proto Recv-Q Send-Q Local Address    Foreign Address   State    PID/Program name
   tcp        0      0 127.0.0.1:8000   0.0.0.0:*         LISTEN   1234/python
   tcp        0      0 0.0.0.0:22       0.0.0.0:*         LISTEN   567/sshd
   ```

##### Droits nécessaires pour ouvrir des ports

**Ports < 1024 (réservés) :**
- **Linux** : Nécessité `sudo` (root).
  ```bash
  sudo python manage.py runserver 0.0.0.0:80  # ✓ Fonctionne
  python manage.py runserver 0.0.0.0:80       # ✗ Erreur "Permission denied"
  ```
- **Windows** : Nécessité des droits administrateur.

**Ports ≥ 1024 (non-réservés) :**
- Utilisateur normal peut ouvrir sans privilèges.
  ```bash
  python manage.py runserver 0.0.0.0:8000  # ✓ Fonctionne sans sudo
  ```

**Conseil :** En développement, utilisez toujours des ports ≥ 1024 pour éviter les problèmes de permissions.

##### Ouverture dynamique des ports en sortie

Quand un client établit une connexion **sortante** (il initie), l'OS lui attribue dynamiquement un port temporaire de la plage **49152-65535**.

**Exemple de flux TCP :**

1. Client (PC) veut tester la connexion au serveur web.
   ```bash
   curl http://google.com:80
   ```

2. Le client ouvre un socket avec un port dynamique (ex. : 52341) :
   - IP locale : 192.168.1.100:52341
   - IP distante : 8.8.8.8:80

3. Trois-way handshake TCP :
   ```
   Client → Serveur : SYN (j'aimerais me connecter)
   Serveur → Client : SYN-ACK (d'accord)
   Client → Serveur : ACK (connexion établie)
   ```

4. Échange de données (HTTP request/response).

5. Fermeture :
   ```
   Client/Serveur → : FIN (fermer la connexion)
   ```

**Visualiser les connexions actives :**
```bash
netstat -tan | grep ESTABLISHED
```

**Qu'est-ce que `grep` ?**  
`grep` (Global Regular Expression Print) est un outil Linux pour **filtrer et chercher du texte**. Il lit une entrée (directement ou via un pipe `|`) et affiche seulement les lignes correspondant au motif spécifié.

- `grep ESTABLISHED` : Affiche seulement les lignes contenant le mot "ESTABLISHED"
- `grep "^tcp"` : Affiche les lignes commençant par "tcp" (^ = début de ligne)
- `grep -c "pattern"` : Compte le nombre de lignes correspondant
- `grep -i "PATTERN"` : Insensible à la casse
- `grep -v "pattern"` : Inverse (affiche les lignes ne contenant PAS le motif)

Ainsi, `netstat -tan | grep ESTABLISHED` affiche toutes les connexions établies (entrantes et sortantes).

**Exemple :**
```
Proto Local Address        Foreign Address    State
TCP   192.168.1.100:52341  8.8.8.8:80        ESTABLISHED
TCP   192.168.1.100:52342  1.1.1.1:443       ESTABLISHED
```

Le port 52341 et 52342 sont des ports dynamiques attribués à chaque nouvelle connexion sortante. Les anciens ports sont remis à disposition après `TIME_WAIT` (typiquement 2 minutes).



##### SSH

Protocole sécurisé pour l'accès distant (port 22 par défaut). Utilise le chiffrement pour protéger les données.

**Utilisation :**
```bash
ssh user@192.168.1.100
ssh -p 2222 user@example.com  # Port personnalisé
```

**Sur le serveur Linux :**
```bash
sudo systemctl start ssh      # Démarrer le service SSH
sudo systemctl status ssh     # Vérifier le statut
netstat -tuln | grep 22       # Voir si le port 22 est en écoute
```

#### Exercice 1 : Connexion SSH et observation des connexions

**Objectif :** Établissez une connexion SSH avec le PC d'un voisin et observez les connexions établies et les ports utilisés des deux côtés.

**Prérequis :**
- Les deux PCs doivent être sur le même réseau (salle de TP, Eduroam, ou LAN).
- Vérifier que SSH est actif sur le PC du voisin : `sudo systemctl status ssh` (le serveur SSH tourne généralement par défaut sur les machines de l'ENSEA)
- Connaître l'adresse IP du voisin : `ip a`

**Étapes :**

1. **Scanner le réseau local pour trouver les IPs des machines :**

   **Première étape : Identifier votre sous-réseau :**
   ```bash
   ip a
   ```
   Cherchez votre interface réseau (eth0, wlan0) et notez l'adresse IP et le CIDR (ex. : `192.168.50.100/24`).

   **Deuxième étape : Scanner les machines actives du réseau :**

   Utilisez `nmap` (Network Mapper) pour scanner le réseau :
   ```bash
   nmap -sn 192.168.50.0/24
   ```
   - `-sn` : Ping scan (détecte les machines actives sans scanner les ports)
   - Remplacez `192.168.50.0/24` par votre sous-réseau

   **Exemple de sortie :**
   ```
   Starting Nmap 7.93 ( https://nmap.org )
   Nmap scan report for 192.168.50.1
   Host is up (0.0019s latency).
   Nmap scan report for 192.168.50.50
   Host is up (0.015s latency).
   Nmap scan report for 192.168.50.75
   Host is up (0.018s latency).
   Nmap scan report for 192.168.50.100
   Host is up (0.0001s latency).
   ```
   Choisissez une IP autre que la vôtre (ex. : `192.168.50.75`), idéalement celle d'un voisin identifié visuellement à côté de vous.

2. **Sur votre PC : Établir la connexion SSH :**
   ```bash
   ssh user@192.168.50.75
   ```
   Tapez le mot de passe du voisin. Si vous ne connaissez pas le nom d'utilisateur par défaut, utilisez `student`.

3. **Pendant la connexion SSH :**
   - **Sur votre PC (client)** : Ouvrez un autre terminal et exécutez :
     ```bash
     netstat -tan | grep 22
     ```
     **Vous verrez :**
     ```
     tcp  0  0 192.168.50.100:52341  192.168.50.75:22  ESTABLISHED
     ```
     - Votre port dynamique : 52341 (port sortant alloué automatiquement)
     - Port du voisin : 22 (SSH)
     - État : ESTABLISHED

   - **Sur le PC du voisin (serveur)** : Exécutez également :
     ```bash
     ss -tan | grep 22
     ```
     **Le voisin verra :**
     ```
     tcp  0  0 0.0.0.0:22             0.0.0.0:*         LISTEN
     tcp  0  0 192.168.50.75:22       192.168.50.100:52341  ESTABLISHED
     ```
     - Le serveur SSH en attente sur le port 22 (LISTEN)
     - Votre connexion établie (ESTABLISHED) avec votre port dynamique 52341

5. **Comparer les deux vues :**

   | Côté Client (Vous) | Côté Serveur (Voisin) |
   |-------------------|----------------------|
   | `192.168.50.100:52341 → 192.168.50.75:22` | `192.168.50.75:22 ← 192.168.50.100:52341` |
   | État : ESTABLISHED | État : ESTABLISHED |
   | Port dynamique : 52341 | Port réservé : 22 |
   | Processus : ssh | Processus : sshd |

6. **Quitter la session SSH :**
   ```bash
   exit
   ```
   Vérifiez que la connexion disparaît de `netstat` des deux côtés.

**Questions :**
- Pourquoi le port client change-t-il à chaque connexion ?
- Que se passe-t-il si vous exécutez `ssh user@ip-voisin` deux fois en parallèle ? Quel port aura la deuxième connexion ?
- Pourquoi le serveur SSH écoute toujours sur le port 22 pendant que la connexion utilise un autre port ?
- Quels sont les risques de garder le port SSH (22) ouvert et accessible depuis le réseau ? Comment peut-on sécuriser un serveur SSH ? (Indice : authentification par clés, changement du port, firewall, fail2ban...)

---

#### Wireshark : Analyser le trafic réseau

**Qu'est-ce que Wireshark ?**  
Wireshark est un analyseur de paquets (packet sniffer) graphique qui capture et dissèque tous les paquets réseau passant par votre carte réseau. Il permet de voir exactement ce qui se passe sur le réseau : les adresses MAC/IP, les ports, les protocoles, les données brutes, etc. C'est un outil essentiel pour déboguer les problèmes réseau et comprendre le fonctionnement des protocoles.

**Installation :**
```bash
sudo apt install wireshark
# À la fin, répondez "oui" pour autoriser les non-root à capturer
sudo usermod -aG wireshark $USER
# Redémarrez le terminal ou reconnectez-vous
```

**Lancer Wireshark :**
```bash
wireshark &
```
ou depuis le menu d'applications.

---

**Interface Wireshark :**

```
┌─ Barre d'outils ─────────────────────────────────────┐
│ [  ] Start   [  ] Stop   Interfaces   Settings        │
└──────────────────────────────────────────────────────┘
┌─ Capture interface selection ──────────────────────┐
│ eth0 (Ethernet) 
│ wlan0 (Wi-Fi)
│ lo (Loopback)
└──────────────────────────────────────────────────┘
```

**Les 3 sections principales :**
1. **Liste de paquets** (en haut) : Tous les paquets capturés avec numéro, timestamp, source, destination, protocole, longueur
2. **Détails du paquet** (au milieu) : Hiérarchie arborescente montrant tous les protocoles (Ethernet → IP → TCP → Données)
3. **Données brutes** (en bas) : Représentation hexadécimale et ASCII des données

---

**Filtres Wireshark courants :**

Wireshark permet de filtrer les paquets pour voir uniquement ce qui vous intéresse.

| Filtre | Signification |
|--------|---------------| 
| `ip.src == 192.168.1.100` | Paquets d'origine cette IP |
| `ip.dst == 192.168.1.1` | Paquets vers cette IP |
| `eth.src == 00:1B:44:11:3A:B7` | Paquets d'une MAC |
| `eth.dst == 00:0A:95:22:4C:D3` | Paquets vers une MAC |
| `ip.src == 192.168.1.100 && ip.dst == 192.168.1.1` | Combinaison AND |
| `tcp.port == 22` | Port TCP 22 (SSH) |
| `udp.port == 53` | Port UDP 53 (DNS) |
| `http` | Protocole HTTP |
| `dns` | Protocole DNS |
| `ssh` | Protocole SSH |
| `!arp` | Tous sauf ARP (utiliser ! pour inverser) |

**Comment utiliser les filtres :**
1. Ouvrez Wireshark et commencez la capture
2. Dans la barre "Display Filter" en haut, entrez un filtre
3. Appuyez sur Entrée
4. Seuls les paquets correspondant s'affichent

---

**Exemple pratique : Filtrer le trafic SSH**

1. **Démarrez une capture :**
   - Cliquez sur votre interface (eth0)
   - Cliquez sur le bouton "Start" (triangle bleu)

2. **Établissez une connexion SSH :**
   ```bash
   ssh user@192.168.1.100
   ```

3. **Dans Wireshark, entrez le filtre :**
   ```
   ip.src == 192.168.1.100 && tcp.port == 22
   ```
   Vous voyez seulement les paquets SSH de ce serveur.

4. **Cliquez sur un paquet pour voir les détails :**
   - Couche Ethernet (MAC source/destination)
   - Couche IP (adresses IP source/destination)
   - Couche TCP (ports source/destination, flags SYN/ACK/FIN)
   - Données (chiffrées pour SSH)

---

**Filtrage par adresse MAC :**

Si vous voulez analyser le trafic d'un PC spécifique sur le réseau :

```
eth.dst == 00:1B:44:11:3A:B7
```

Cela affiche uniquement les paquets envoyés **à cette MAC**. C'est utile pour voir tout ce qui arrive à un PC (ARP, IPv4, IPv6, etc.).

**Combinaisons :**
```
eth.src == 00:1B:44:11:3A:B7 || eth.dst == 00:1B:44:11:3A:B7
```
Montre tous les paquets **provenant OU allant vers** cette MAC.

---

**Cas d'usage : Déboguer une connexion SSH**

1. **Démarrez Wireshark**
2. **Filtrez :**
   ```
   ip.src == <votre IP> && ip.dst == <serveur SSH>
   ```
3. **Établissez une connexion SSH**
4. **Regardez :**
   - Paquets TCP SYN (établissement)
   - Handshake SSL/TLS si applicable
   - Données chiffrées SSH
   - Paquets RST/FIN (fermeture)

---

**Cas d'usage : Voir qui émet un requête DNS**

1. **Filtrez :**
   ```
   dns
   ```
2. **Ouvrez un navigateur et allez à google.com**
3. **Wireshark affiche :**
   ```
   Source: 192.168.1.100
   Destination: 8.8.8.8 (DNS Google)
   Proto: UDP
   Port 53
   Query: google.com
   ```

---

#### Exercice 2 : Ouvrir un port personnalisé avec Netcat (nc)

**Objectif :** Utilisez `netcat` pour ouvrir un port spécifique en écoute et établissez une communication bidirectionnelle avec le PC du voisin.

**Qu'est-ce que netcat (nc) ?**  
`nc` est un outil pour créer des connexions TCP/UDP. Il permet d'ouvrir des ports d'écoute (serveur) et de se connecter (client) très simplement, sans protocole spécifique.

**Prérequis :**
- `netcat` doit être installé : `sudo apt install netcat` (appeler l'enseignant si ce n'est pas installé)

**Étapes :**

1. **Sur le PC du voisin (Serveur) :**
   Ouvrez un port en écoute (ex. : port 9999) :
   ```bash
   nc -l -p 9999
   ```
   ou (version plus récente) :
   ```bash
   nc -l 9999
   ```
   - `-l` : Mode écoute (listen)
   - `-p 9999` : Port 9999
   - **Résultat :** Le terminal attend une connexion, pas de prompt.

2. **Sur votre PC (Client) :**
   Connectez-vous au serveur du voisin :
   ```bash
   nc 192.168.50.75 9999
   ```
   - Remplacez `192.168.50.75` par l'IP du voisin.
   - **Résultat :** Vous êtes maintenant connecté.

3. **Communication bidirectionnelle :**
   - **Sur votre PC client :** Tapez un message :
     ```
     Bonjour, c'est le client !
     ```
     Appuyez sur Entrée. Le message s'affiche sur le terminal du voisin.

   - **Sur le PC du voisin (serveur)** : Tapez une réponse :
     ```
     Salut ! Je suis le serveur.
     ```
     Appuyez sur Entrée. Vous la recevez.

   C'est une vraie communication TCP/IP simplifiée !

4. **Observer les connexions avec `netstat` :**
   Ouvrez un **troisième terminal** (sur chaque PC) et exécutez :
   ```bash
   netstat -tan | grep 9999
   ```

   **Sur le client :**
   ```
   Proto Recv-Q Send-Q Local Address       Foreign Address     State
   tcp        0      0 192.168.50.100:52342 192.168.50.75:9999  ESTABLISHED
   ```

   **Sur le serveur :**
   ```
   Proto Recv-Q Send-Q Local Address       Foreign Address     State
   tcp        0      0 0.0.0.0:9999        0.0.0.0:*           LISTEN
   tcp        0      0 192.168.50.75:9999  192.168.50.100:52342 ESTABLISHED
   ```

5. **Fermer la connexion :**
   - Sur l'un des deux terminaux, appuyez sur Ctrl+C.
   - La connexion se termine immédiatement.
   - Le serveur `nc` reste en attente d'une nouvelle connexion (appuyez sur Ctrl+C pour arrêter).

**Variantes avec netcat :**

**Transférer un fichier :**
- Serveur (receveur) : `nc -l 9999 > fichier_reçu.txt`
- Client (envoyeur) : `nc 192.168.50.75 9999 < mon_fichier.txt`

**Questions :**
- Quel est la différence entre nc et ssh pour les connexions distantes ?
- Pourquoi nc ouvre-t-il automatiquement un port dynamique côté client ?

---

##### DHCP

DHCP (Dynamic Host Configuration Protocol) attribue automatiquement des adresses IP aux appareils. Utilise les ports UDP 67 (serveur) et 68 (client).

**Flux DHCP (processus DORA) :**

Le processus d'attribution d'une adresse IP passe par 4 phases appelées **DORA** : Discover, Offer, Request, Acknowledgement.

**Phase 1 : DHCP Discover (Client → Broadcast)**
- **Qui envoie ?** : Le client (nouvel appareil) qui vient de démarrer
- **À qui ?** : À tous les serveurs DHCP du réseau (broadcast UDP:68 → UDP:67)
- **Message** : "Bonjour ! Y a-t-il un serveur DHCP ? J'aurais besoin d'une adresse IP."
- **Détails du paquet** :
  - Adresse source du client : 0.0.0.0 (il n'en a pas encore)
  - Adresse destination : 255.255.255.255 (broadcast)
  - Identifiant client : Un ID unique généré aléatoirement (ex. : MAC address)
  - Options demandées : Adresse IP, masque, passerelle, DNS, durée de bail

**Phase 2 : DHCP Offer (Serveur → Client)**
- **Qui envoie ?** : Le serveur DHCP
- **À qui ?** : Au client (unicast, ou broadcast si le client n'a pas encore d'IP)
- **Message** : "Salut ! Je suis un serveur DHCP. Voici une adresse IP que je te propose : 192.168.1.100"
- **Détails du paquet** :
  - Adresse IP proposée : 192.168.1.100
  - Masque de sous-réseau : 255.255.255.0
  - Passerelle (routeur) : 192.168.1.1
  - Serveur DNS : 8.8.8.8
  - Durée du bail (lease time) : Ex. 24 heures (86400 secondes)
  - Identifiant serveur DHCP : Adresse IP du serveur
- **Plusieurs serveurs peuvent répondre** : Si plusieurs serveurs DHCP sont présents, le client recevra plusieurs offres

**Phase 3 : DHCP Request (Client → Broadcast)**
- **Qui envoie ?** : Le client
- **À qui ?** : À tous les serveurs (broadcast), pour informer tous les serveurs de son choix
- **Message** : "Merci serveur X ! J'accepte l'adresse 192.168.1.100 que tu me proposes. Les autres serveurs, veuillez reprendre leurs offres."
- **Détails du paquet** :
  - Adresse IP demandée : 192.168.1.100
  - Identifiant du serveur choisi : Adresse du serveur DHCP retenu
  - Identifiant client : Le même que dans Discover
- **Raison du broadcast** : Prévenir les autres serveurs DHCP de ne pas réserver cette adresse pour un autre client

**Phase 4 : DHCP Acknowledgement (DHCP ACK) - Serveur → Client**
- **Qui envoie ?** : Le serveur DHCP choisi
- **À qui ?** : Au client
- **Message** : "Confirmé ! L'adresse IP 192.168.1.100 est maintenant la tienne pour 24 heures. Voici tous les paramètres de ton réseau."
- **Détails du paquet** :
  - Adresse IP attribuée : 192.168.1.100
  - Masque : 255.255.255.0
  - Passerelle : 192.168.1.1
  - Serveurs DNS : 8.8.8.8, 8.8.4.4
  - Durée du bail : 24 heures
- **Le client configure son interface réseau** avec tous ces paramètres et peut maintenant communiquer

**Cas particuliers :**

1. **DHCP Starvation** : Un attaquant envoie des milliers de DHCP Discover pour épuiser le pool d'adresses. Défense : DHCP snooping.

2. **DHCP Spoofing** : Un serveur DHCP malveillant propose des configurations fausses (ex. : passerelle malveillante). Défense : Authentification DHCP, DHCP snooping.

3. **Renouvellement du bail (Rebinding)** :
   - À 50% : Client essaie de renouveler avec le serveur original (RENEWING)
   - À 87.5% : Si pas de réponse, broadcast à tous les serveurs (REBINDING)
   - À 100% : Le bail expire, l'IP est libérée

**Visualiser la configuration DHCP :**
Si le serveur tourne sous Linux, non accessible dans le cadre du TP.
```bash
cat /etc/dhcp/dhcpd.conf      # Fichier de config serveur DHCP (Linux)
cat /etc/dhcp/dhcpd.leases    # Base de données des baux attribués
```

**Sur le client - Voir son configuration DHCP :**
```bash
ip a                           # Voir l'IP attribuée par DHCP
nmcli device show              # Détails de la connexion DHCP (NetworkManager)
cat /etc/resolv.conf           # Serveurs DNS assignés par DHCP
```

##### DNS

DNS (Domain Name System) résout les noms de domaine en adresses IP (port 53 TCP/UDP).

**Qu'est-ce que DNS ?**
DNS est un système hiérarchique et distribué qui traduit les noms de domaine lisibles (`google.com`) en adresses IP (`142.250.185.46`). Sans DNS, vous devriez mémoriser l'IP de chaque site web !

**Exemple simple :**
- Vous tapez `google.com` dans le navigateur.
- Votre PC demande au serveur DNS : "Quelle est l'IP de google.com ?"
- DNS répond : "C'est 142.250.185.46"
- Votre navigateur se connecte à `142.250.185.46:443` (HTTPS).

**Architecture DNS - Hiérarchie des serveurs :**

```
                        Root Nameservers (.)
                        ├─.com, .org, .fr, .net...
                        │
                    google.com
                    ├ DNS Primaire (Master)
                    ├ DNS Secondaire (Slave)
                    └ DNS Tertiaire (pour résilience)
```

1. **Root Nameservers** : Au sommet de la hiérarchie. Ils connaissent où trouver les serveurs pour chaque TLD (.com, .org, .fr, etc.). Il en existe 13 dans le monde entier.

2. **TLD Nameservers** : Pour chaque extension (.com, .org, .fr). Ils connaissent où trouver le serveur DNS de chaque domaine.

3. **Authoritative Nameservers** : Serveurs DNS officiels pour un domaine spécifique (ex. : google.com). Ils stockent les enregistrements DNS (A, AAAA, MX, CNAME, etc.).

**Requête DNS - Processus détaillé :**

```
Client (192.168.1.100)
     │
     ├─ Query: "Quelle est l'IP de www.google.com ?"
     │  Destination: DNS Récursif (ISP ou 8.8.8.8)
     │
Récurseur DNS (ISP)
     │
     ├─ Query: "Où est www.google.com ?"
     │  Destination: Root Nameserver
     │
Root Nameserver
     │
     └─ Réponse: "Demande au TLD .com"
     │
Récurseur → TLD .com
     │
     ├─ Query: "Où est www.google.com ?"
     │  Destination: TLD .com Nameserver
     │
TLD .com Nameserver
     │
     └─ Réponse: "Demande à google.com (142.250.185.46)"
     │
Récurseur → google.com Authoritative
     │
     ├─ Query: "Quelle est l'IP de www.google.com ?"
     │  Destination: DNS Primaire google.com
     │
DNS Primaire google.com
     │
     └─ Réponse: "142.250.185.46"
     │
Récurseur → Client
     │
     └─ Réponse finale: "142.250.185.46"
```

Ce processus s'appelle **résolution DNS récursive**. Le client demande une réponse finale, et le récurseur (DNS ISP) interroge l'ensemble de la chaîne.

**DNS Primaire vs Secondaire :**

Les serveurs DNS d'un domaine travaillent en paires (ou groupes) pour la résilience :

| Type | Rôle | Caractéristiques |
|------|------|------------------|
| **DNS Primaire (Master)** | Serveur principal | Stocke les fichiers de zone originaux. C'est ici que les administrateurs font les modifications (ajouter des enregistrements, etc.). Les changements sont appliqués ici en premier. |
| **DNS Secondaire (Slave)** | Serveur de secours | Reçoit une copie des données du primaire via un transfert de zone (Zone Transfer). En cas de panne du primaire, les requêtes vont au secondaire. Lecture seule (généralement). |
| **DNS Tertiaire+** | Redondance supplémentaire | Utilisés par les grandes organisations pour diffuser les données à plusieurs endroits du monde. |

**Enregistrements DNS courants :**

| Type | Fonction | Exemple |
|------|----------|---------|
| **A** | Mappe un domaine à une adresse IPv4 | `google.com` → `142.250.185.46` |
| **AAAA** | Mappe un domaine à une adresse IPv6 | `google.com` → `2607:f8b0:4004:80d::200e` |
| **CNAME** | Alias d'un domaine vers un autre | `www.google.com` → `google.com` (créé un alias) |
| **MX** | Serveur de mail | `google.com` → `aspmx.l.google.com` (pour les emails) |
| **NS** | Serveurs DNS pour le domaine | `google.com` → `ns1.google.com`, `ns2.google.com` |
| **SOA** | Données d'autorité (primaire, contact, ttl) | Métadonnées de la zone |
| **TXT** | Texte libre (spamming, vérifications) | Vérification de domaine, SPF, DKIM |
| **PTR** | Résolution inverse (IP → domaine) | `142.250.185.46` → `google.com` |

**DNS Cache et TTL :**

- **TTL (Time To Live)** : Durée pendant laquelle une réponse DNS est mémorisée. Ex. : TTL = 3600 secondes (1 heure).
- **Cache du client** : Votre navigateur / OS mémorise les résolutions DNS localement pour éviter de recontacter le serveur DNS.
- **Cache du récurseur** : L'ISP DNS mémorise aussi les réponses pour que le prochain client qui demande `google.com` ait une réponse instantanée.

**Voir votre serveur DNS et faire des tests :**
```bash
cat /etc/resolv.conf          # Linux: voir les serveurs DNS configurés
nslookup google.com           # Tester la résolution DNS
dig google.com                # Plus détaillé (si dig est installé)
dig google.com +trace         # Voir la chaîne complète de résolution
host google.com               # Alternative simple
```

**Exemple de sortie `dig` :**
```
; <<>> DiG 9.16.1-Ubuntu <<>> google.com
;; QUESTION SECTION:
;google.com.                    IN      A

;; ANSWER SECTION:
google.com.             300     IN      A       142.250.185.46

;; SERVER: 8.8.8.8#53(8.8.8.8)
;; WHEN: Thu Mar 22 10:30:00 UTC 2026
;; MSG SIZE  rcvd: 55
```

**Sécurité DNS :**

1. **DNS Spoofing** : Attaquant prétend être un serveur DNS et redirection vers un site malveillant.
2. **DNS Amplification Attack** : Attaquant envoie des requêtes DNS avec l'IP de la victime, submergeant la victime de réponses.
3. **DNSSEC** : Signe les enregistrements DNS pour vérifier leur authenticité.

#### Exercice 1 : Découvrir le serveur DNS local de l'école

**Objectif :** Identifiez le serveur DNS configuré sur votre machine et testez la résolution DNS locale du domaine ENSEA.

**Étapes :**

1. **Identifier votre serveur DNS actuel :**

   **Sur Linux :**
   ```bash
   nmcli device show | grep DNS
   ```


2. **Tester la résolution DNS locale vers ENSEA :**

   Testez si le domaine ENSEA est résolvable localement :
   ```bash
   nslookup ensea.fr
   dig ensea.fr
   host ensea.fr
   ```

   **Exemple de sortie :**
   ```
   ; <<>> DiG 9.16.1-Ubuntu <<>> ensea.fr
   ; (1 server found)
   ;; global options: +cmd
   ;; Got answer:
   ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 12345
   ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1
   
   ;; QUESTION SECTION:
   ;ensea.fr.                      IN      A
   
   ;; ANSWER SECTION:
   ensea.fr.               300     IN      A       192.168.x.x
   
   ;; SERVER: 192.168.1.1#53(192.168.1.1)
   ```

   **Analyse :**
   - Si vous voyez une réponse : Le serveur DNS local connaît `ensea.fr` (résolution locale fonctionne).
   - Si `SERVFAIL` ou timeout : Le serveur DNS n'a pas la réponse (demande au DNS externe).

3. **Tracer la résolution DNS complète :**

   Utilisez `dig +trace` pour voir le chemin complet :
   ```bash
   dig ensea.fr +trace
   ```

   **Résultat :**
   ```
   ; <<>> DiG 9.16.1-Ubuntu <<>> ensea.fr +trace
   ; (1 server found)
   ;; global options: +cmd
   .                       518400  IN      NS      a.root-servers.net.
   .                       518400  IN      NS      b.root-servers.net.
   ...
   fr.                     172800  IN      NS      d.nic.fr.
   fr.                     172800  IN      NS      e.nic.fr.
   ...
   ensea.fr.               3600    IN      NS      dns1.ensea.fr.
   ensea.fr.               3600    IN      NS      dns2.ensea.fr.
   
   ensea.fr.               3600    IN      A       192.168.x.x
   ```

   Cela montre l'ensemble de la chaîne : Root → Zone `fr` → Serveurs ENSEA.

4. **Interroger directement le serveur DNS ENSEA :**

   Si vous connaissez l'IP du serveur DNS ENSEA (redemmander à votre prof l'ip du DNS interne de l'école) :
   ```bash
   dig @192.168.1.254 ensea.fr
   ```

   L'option `@` spécifie le serveur DNS à interroger.

**Questions :**
- Quel est l'adresse IP du serveur DNS de votre réseau local ?
- Est-ce que le domaine ENSEA est résolvable depuis le réseau local ou doit-on aller sur Internet ?
- Pourquoi l'ENSEA a-t-elle probablement son propre serveur DNS interne ?
- Il se peut que le DNS de l'école ne réponde pas la même adresse que le DNS accessible depuis internet, pourquoi ? Quel serait l'avantage d'une différence d'adresse ?

---

#### Exercice 2 : Configurer une résolution DNS locale personnalisée

**Objectif :** Ajoutez une entrée DNS locale dans le fichier `/etc/hosts` pour faire pointer une URL locale interne vers une IP spécifique de votre serveur Django.

**Contexte :** 
Normalement, vous accédez à votre Django par `http://localhost:8000` ou `http://127.0.0.1:8000`. Mais sur un réseau d'entreprise ou scolaire, on voudrait accéder par un nom comme `http://cafeteria.local` ou `http://cafeteria.ensea`.

**Méthode 1 : Utiliser le fichier `/etc/hosts` (Simple, local)**

**Sur Linux/Mac :**

1. **Ouvrez le fichier `/etc/hosts` en édition :**
   ```bash
   sudo nano /etc/hosts
   ```

2. **Ajoutez une ligne à la fin du fichier :**
   ```
   127.0.0.1       localhost
   ::1             localhost
   
   # Ajoutez cette ligne :
   127.0.0.1       cafeteria.local
   192.168.50.100  cafeteria.ensea
   ```

   **Explication :**
   - `127.0.0.1 cafeteria.local` : Sur votre PC, `cafeteria.local` pointe vers votre serveur Django local (127.0.0.1).
   - `192.168.50.100 cafeteria.ensea` : Sur le réseau, `cafeteria.ensea` pointe vers l'IP 192.168.50.100 (votre PC sur le réseau).

3. **Sauvegardez** (Ctrl+O, Entrée, Ctrl+X).

4. **Testez la résolution :**
   ```bash
   ping cafeteria.local
   nslookup cafeteria.local
   ```

   **Résultat :**
   ```
   PING cafeteria.local (127.0.0.1): 56 data bytes
   64 bytes from 127.0.0.1: icmp_seq=0 ttl=64 time=0.054 ms
   ```

5. **Accédez à votre application :**
   - Lance Django : `python manage.py runserver 0.0.0.0:8000`
   - Ouvrez le navigateur : `http://cafeteria.local:8000`
   - ✓ Fonctionne !

**Limitation de `/etc/hosts` :** Fonctionne seulement sur votre machine. Les autres PCs du réseau ne pourront pas utiliser ce nom (sauf s'ils le configurent aussi).

---

**Questions d'approfondissement :**
- Quelle est la différence entre `/etc/hosts` et un serveur DNS pour la résolution locale ?
- Comment Django devrait-il être configuré pour accepter les requêtes de `cafeteria.ensea` ?
  
**Indice pour Django :** Dans `settings.py`, modifiez `ALLOWED_HOSTS` :
```python
ALLOWED_HOSTS = ['127.0.0.1', 'localhost', 'cafeteria.local', 'cafeteria.ensea']
```

##### HTTP(S)

HTTP (HyperText Transfer Protocol) est le protocole fondamental du web. Il fonctionne sur TCP/IP et utilise un modèle **requête-réponse** sans état (stateless).

**Caractéristiques principales :**
- **Port 80** : HTTP non sécurisé (données en clair)
- **Port 443** : HTTPS sécurisé (chiffrement SSL/TLS)
- **Stateless** : Chaque requête est indépendante. Le serveur ne mémorise pas les requêtes précédentes (d'où les cookies et les sessions).
- **Requête-Réponse** : Le client envoie toujours une requête en premier, le serveur répond.
- **Connexions persistantes** : HTTP/1.1 peut réutiliser la même connexion TCP pour plusieurs requêtes.

#### Méthodes HTTP

Les méthodes HTTP définissent l'action désirée sur une ressource :

| Méthode | Intention | Corps | Réponse | Idempotent |
|---------|-----------|-------|---------|------------|
| **GET** | Récupérer une ressource | Non | Données de la ressource | Oui |
| **POST** | Créer une nouvelle ressource | Oui | Réponse du serveur | Non |
| **PUT** | Remplacer entièrement une ressource | Oui | Statut de succès | Oui |
| **PATCH** | Modifier partiellement une ressource | Oui | Réponse modifiée | Non |
| **DELETE** | Supprimer une ressource | Non | Statut de suppression | Oui |
| **HEAD** | Comme GET, mais sans corps (métadonnées) | Non | En-têtes seulement | Oui |
| **OPTIONS** | Quelles méthodes sont disponibles ? | Non | Liste des méthodes | Oui |
| **TRACE** | Trace la route vers la ressource (debug) | Non | Trace complète | Oui |

**Idempotent** = Exécuter 2 fois = même résultat qu'une fois.
- GET 2 fois : Récupère les mêmes données ✓
- POST 2 fois : Crée 2 ressources différentes ✗

#### Structure d'une requête HTTP

Exemple concret :
```
GET /api/students HTTP/1.1
Host: cafeteria.ensea:8000
User-Agent: Mozilla/5.0 (X11; Linux x86_64)
Accept: application/json
Accept-Language: fr-FR,fr;q=0.9,en;q=0.8
Connection: keep-alive
Cookie: sessionid=abc123def456789
```

**Parties d'une requête :**

1. **Ligne de requête (Request Line) :**
   ```
   GET /api/students HTTP/1.1
   [Méthode] [Chemin] [Version HTTP]
   ```
   - **Méthode** : GET, POST, etc.
   - **Chemin** : Ressource demandée (/api/students, /index.html)
   - **Version** : HTTP/1.1 ou HTTP/2

2. **En-têtes (Headers) :**
   ```
   Host: cafeteria.ensea:8000
   User-Agent: Mozilla/5.0
   Accept: application/json
   Connection: keep-alive
   ```
   Métadonnées de la requête.

3. **Ligne vide** : Sépare les en-têtes du corps.

4. **Corps (Body)** : Données (seulement pour POST, PUT, PATCH).
   ```
   POST /api/students HTTP/1.1
   Content-Type: application/json
   Content-Length: 45
   
   {"name": "Alice", "email": "alice@ensea.fr"}
   ```

#### Codes de réponse HTTP

Le serveur répond avec une code parmi 5 catégories :

| Code | Signification | Exemples |
|------|---------------|---------| 
| **1xx** | Information | 100 Continue, 101 Switching Protocols |
| **2xx** | Succès | 200 OK, 201 Created, 204 No Content |
| **3xx** | Redirection | 301 Moved Permanently, 302 Found, 304 Not Modified |
| **4xx** | Erreur client | 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found |
| **5xx** | Erreur serveur | 500 Internal Server Error, 502 Bad Gateway, 503 Service Unavailable |

**Codes courants en détail :**

| Code | Signification | Quand ? |
|------|---------------|---------| 
| **200 OK** | Succès, réponse incluse | GET réussi, POST réussi |
| **201 Created** | Ressource créée | POST créant une nouvelle ressource |
| **204 No Content** | Succès, mais pas de données | DELETE réussi, PUT sans réponse |
| **301 Moved Permanently** | Redirection permanente | L'URL a changé définitivement |
| **302 Found** | Redirection temporaire | L'URL a changé temporairement |
| **304 Not Modified** | Cache valide | Fichier pas modifié depuis la dernière requête |
| **400 Bad Request** | Requête mal formée | Données invalides envoyées |
| **401 Unauthorized** | Non authentifié | Pas connecté / identifiants invalides |
| **403 Forbidden** | Authentifié mais pas autorisé | Admin seulement, vous n'êtes pas admin |
| **404 Not Found** | Ressource introuvable | Page n'existe pas |
| **500 Internal Server Error** | Bug du serveur | Erreur non gérée dans le code |
| **502 Bad Gateway** | Serveur proxy reçoit erreur du backend | Serveur Django crash |
| **503 Service Unavailable** | Serveur surchargé / maintenance | Serveur en maintenance |

#### Structure d'une réponse HTTP

Exemple concret :
```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 156
Set-Cookie: sessionid=xyz789uvw; Path=/; HttpOnly
Cache-Control: max-age=3600
Connection: keep-alive

[{"id": 1, "name": "Alice", "email": "alice@ensea.fr"},
 {"id": 2, "name": "Bob", "email": "bob@ensea.fr"}]
```

**Parties d'une réponse :**

1. **Ligne de statut (Status Line) :**
   ```
   HTTP/1.1 200 OK
   [Version] [Code] [Message]
   ```

2. **En-têtes (Headers) :**
   ```
   Content-Type: application/json
   Content-Length: 156
   Set-Cookie: sessionid=xyz789uvw
   ```

3. **Ligne vide** : Sépare en-têtes du corps.

4. **Corps (Body)** : Les données de réponse (HTML, JSON, fichier binaire...).

#### En-têtes HTTP courants

**Requête :**
| En-tête | Sens | Exemple |
|---------|------|---------|
| **Host** | Domaine du serveur | `Host: cafeteria.ensea:8000` |
| **User-Agent** | Navigateur/client | `User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)` |
| **Accept** | Types de contenu acceptés | `Accept: application/json, text/html` |
| **Accept-Language** | Langues préférées | `Accept-Language: fr-FR,en` |
| **Authorization** | Identifiants d'authentification | `Authorization: Bearer token123` |
| **Content-Type** | Type des données envoyées | `Content-Type: application/json` |
| **Content-Length** | Taille du corps | `Content-Length: 256` |
| **Cookie** | Données stockées | `Cookie: sessionid=abc123; theme=dark` |
| **Referer** | Page d'origine | `Referer: https://google.com` |
| **Connection** | Gestion de la connexion | `Connection: keep-alive` (ou `close`) |

**Réponse :**
| En-tête | Sens | Exemple |
|---------|------|---------|
| **Content-Type** | Type des données renvoyées | `Content-Type: text/html; charset=utf-8` |
| **Content-Length** | Taille du corps | `Content-Length: 1024` |
| **Set-Cookie** | Stocker un cookie client | `Set-Cookie: sessionid=xyz789; Path=/` |
| **Cache-Control** | Directive de cache | `Cache-Control: max-age=3600, public` |
| **Location** | URL de redirection (3xx) | `Location: /new-page` |
| **Server** | Logiciel serveur | `Server: Apache/2.4.41` |
| **Access-Control-Allow-Origin** | CORS (domaines autorisés) | `Access-Control-Allow-Origin: *` |
| **ETag** | Identifiant version du contenu | `ETag: "12345abcde"` |

#### Cycle complet d'une requête HTTP

Illustration timeline :

```
Client (Navigateur)              Serveur Django
      │                                 │
      ├─ DNS lookup: cafeteria.ensea    │
      ├────────────────────────────────→ DNS Server
      │← IP: 192.168.50.100             │
      │                                 │
      ├─ TCP Connection (3-way)         │
      ├─ SYN ──────────────────────────→│
      │←─ SYN-ACK ──────────────────────│
      ├─ ACK ──────────────────────────→│
      │                                 │
      ├─ HTTP GET /students HTTP/1.1   │
      ├────────────────────────────────→│ (Port 8000)
      │  Host: cafeteria.ensea:8000     │
      │  Accept: text/html              │
      │  ...                            │
      │                                 │
      │          Processing...          │
      │    views.student_list(request)  │
      │    Database query...            │
      │    Template rendering...        │
      │                                 │
      │←─ HTTP/1.1 200 OK ─────────────│
      │  Content-Type: text/html        │
      │  Content-Length: 2048           │
      │  Set-Cookie: sessionid=abc      │
      │                                 │
      │  [HTML Page with students list] │
      │                                 │
      │ Browser renders HTML            │
      │ +───────────────────────────+   │
      │ | Students List            |   │
      │ | Alice (alice@ensea.fr)   |   │
      │ | Bob (bob@ensea.fr)       |   │
      │ +───────────────────────────+   │
```

#### HTTP vs HTTPS

**HTTP :**
- Port 80
- Données en clair (lisibles par n'importe qui sur le réseau)
- Pas de chiffrement
- ⚠️ Risque : Interception, modification des données

**HTTPS (HTTP + SSL/TLS) :**
- Port 443
- Données chiffrées (illisibles sans les clés)
- Certificat SSL/TLS authentifie le serveur
- ✓ Sécurisé pour les données sensibles (mots de passe, cartes bancaires, etc.)

**Processus HTTPS :**
1. **TCP Connection** : Établir connexion TCP au port 443
2. **TLS Handshake** :
   - Client → Serveur : "Bonjour, quelles chiffrements supporterez vous ?"
   - Serveur → Client : "Voici mon certificat SSL et je choisis le chiffrement X"
   - Exchange de clés de session
3. **Encrypted Communication** : Toutes les données HTTP sont chiffrées
4. **Fermeture** : Disconnection TCP

**Vérifier un certificat SSL :**
```bash
openssl s_client -connect google.com:443
# Voir le certificat, la date d'expiration, l'émetteur (CA)
```


---

**Partie 1 : Capturer une requête HTTP brute**

1. **Sur le PC serveur, ouvrez netcat sur un port arbitraire (ex. : 9999) :**
   ```bash
   nc -l 9999 > requete.txt
   ```
   - `-l` : Mode écoute
   - `> requete.txt` : Redirection de la requête reçue dans un fichier
   - Le terminal reste bloqué en attente

2. **Sur le même PC : Ouvrez un navigateur et tapez :**
   ```
   http://127.0.0.1:9999/
   ```


3. **Résultat dans netcat :**
   - Le navigateur attend une réponse (le terminal reste figé)
   - Appuyez sur Ctrl+C dans le terminal netcat

4. **Consultez le fichier capturé :**
   ```bash
   cat requete.txt
   ```

   **Exemple de sortie (requête brute du navigateur) :**
   ```
   GET / HTTP/1.1
   Host: 127.0.0.1:9999
   User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36
   Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
   Accept-Language: fr-FR,fr;q=0.9,en;q=0.8
   Accept-Encoding: gzip, deflate
   Connection: keep-alive
   Upgrade-Insecure-Requests: 1
   
   ```

   Vous voyez la requête **brute** telle qu'elle a été envoyée par le navigateur.

---

**Partie 2 : Modifier la requête pour faire un GET vers Django**

1. **Editez le fichier requete.txt :**
   ```bash
   nano requete.txt
   ```
   ou directement depuis VS Code.

2. **Modifiez la première ligne et les en-têtes :**
   
   **Avant :**
   ```
   GET / HTTP/1.1
   Host: 127.0.0.1:9999
   ```

   **Après :**
   ```
   GET /api/students/ HTTP/1.1
   Host: 127.0.0.1:8000
   Accept: application/json
   Connection: close
   ```

   **Explications des changements :**
   - `GET /api/students/ HTTP/1.1` : Demander l'endpoint API (pas la racine `/`)
   - `Host: 127.0.0.1:8000` : Serveur Django (pas le port 9999)
   - `Accept: application/json` : Dire au serveur qu'on veut du JSON
   - `Connection: close` : Fermer la connexion après (plus simple pour tester)
   - **Supprimez** les lignes inutiles (User-Agent, Accept-Language, etc.)

3. **Envoyez la requête modifiée vers Django :**
   ```bash
   cat requete.txt | nc 127.0.0.1 8000
   ```

   **Résultat :**
   ```
   HTTP/1.1 200 OK
   Content-Type: application/json
   Content-Length: 156
   
   [{"id": 1, "name": "Alice", "email": "alice@ensea.fr"},
    {"id": 2, "name": "Bob", "email": "bob@ensea.fr"}]
   ```

   **Vous venez d'interroger l'API en envoyant une requête HTTP brute modifiée !**

---

**Partie 3 : Créer un POST pour ajouter un étudiant**

1. **Créez une nouveau fichier requete_post.txt :**
   ```bash
   nano requete_post.txt
   ```

2. **Écrivez une requête POST pour créer un nouvel étudiant :**
   ```
   POST /api/students/ HTTP/1.1
   Host: 127.0.0.1:8000
   Content-Type: application/json
   Content-Length: 51
   Connection: close
   
   {"name": "David", "email": "david@ensea.fr"}
   ```

   **Explications :**
   - `POST /api/students/` : Créer une nouvelle ressource
   - `Content-Type: application/json` : Les données envoyées sont du JSON
   - `Content-Length: 51` : Exactement 51 bytes du JSON (calculé ci-dessous)
   - **Ligne vide** : Sépare en-têtes du corps
   - **Corps JSON** : Les données de l'étudiant

3. **Calculer Content-Length :**
   ```bash
   echo -n '{"name": "David", "email": "david@ensea.fr"}' | wc -c
   ```
   Retourne `51` (nombre exact de caractères).

4. **Envoyez la requête POST :**
   ```bash
   cat requete_post.txt | nc 127.0.0.1 8000
   ```

   **Réponse attendue :**
   ```
   HTTP/1.1 201 Created
   Content-Type: application/json
   Location: /api/students/3/
   
   {"id": 3, "name": "David", "email": "david@ensea.fr"}
   ```

   **Un nouvel étudiant "David" a été créé !**

5. **Vérifiez en base de données :**
   Depuis l'interface admin de Django, vérifier la création d'un nouveau étudiant. Vous vous êtes fait passer pour une page web depuis nc. Nous avons fait cela en HTTP le port 8000 en non-chiffré, cela serait un peu plus compliqué en HTTPS sur le port 443 avec le chiffrement

---

**Partie 4 : Exercice bonus - Modifier (PUT) et supprimer (DELETE)**

**Modifier un étudiant (PUT) :**
```
PUT /api/students/1/ HTTP/1.1
Host: 127.0.0.1:8000
Content-Type: application/json
Content-Length: 55
Connection: close

{"name": "Alice New", "email": "alice.new@ensea.fr"}
```

**Supprimer un étudiant (DELETE) :**
```
DELETE /api/students/1/ HTTP/1.1
Host: 127.0.0.1:8000
Connection: close

```

Exécutez-les de la même manière avec `cat | nc`.

---

**Résumé de l'exercice :**

| Opération | Fichier | Commande |
|-----------|---------|----------|
| Capturer | `requete.txt` | `echo "..." > requete.txt` |
| GET | `requete_get.txt` | `cat requete_get.txt \| nc 127.0.0.1 8000` |
| POST | `requete_post.txt` | `cat requete_post.txt \| nc 127.0.0.1 8000` |
| PUT | `requete_put.txt` | `cat requete_put.txt \| nc 127.0.0.1 8000` |
| DELETE | `requete_delete.txt` | `cat requete_delete.txt \| nc 127.0.0.1 8000` |

C'est extrêmement puissant : Vous comprenez maintenant peu HTTP fonctionne vraiment peu le capot !

**Questions :**
- Pourquoi `Content-Length` doit-il être exact pour POST ?
- Que se passe-t-il si on envoie du JSON mal formé dans le corps ?
- Django valide-t-il l'email ? Comment tester ?
- Comment faire de l'authentification (`Authorization` header) ?

#### Déploiement en réseau local
- `0.0.0.0:8000` : Écoute sur toutes les interfaces.
- `localhost` : 127.0.0.1, accès local.
- `ALLOWED_HOSTS` : Dans `settings.py`, listez les hôtes autorisés (ex. : ['localhost', '192.168.1.1']).

## Etape 11 : Mise en place d'une API
### Notion d'API

Une API transforme votre application en un service que d'autres applications peuvent utiliser. Plutôt que de servir uniquement des pages HTML, votre projet peut partager des données et des fonctionnalités avec des clients externes :
- une application mobile,
- un front-end JavaScript séparé,
- un service partenaire,
- un script automatisé.

L'idée clé est de permettre à des applications tierces de consommer votre application via HTTP. Vous partagez des ressources comme des étudiants, des menus ou des commandes, sans obliger l'utilisateur à passer par l'interface web.

### JSON, le format des API

JSON est le format standard des API REST : léger, lisible et supporté par tous les langages.

Exemple :

```json
{
  "id": 3,
  "name": "Charlie",
  "email": "charlie@ensea.fr"
}
```

Exemple de JSON imbriqué :

```json
{
  "id": 3,
  "name": "Charlie",
  "email": "charlie@ensea.fr",
  "address": {
    "street": "12 rue de la Paix",
    "city": "Paris",
    "zip": "75001"
  },
  "courses": [
    {"code": "CS101", "name": "Programmation"},
    {"code": "DB201", "name": "Bases de données"}
  ]
}
```

Pour les API Django, on renvoie généralement du JSON avec l'en-tête `Content-Type: application/json`.

### Modifications de urls.py et views.py

Pour créer une API propre et réutilisable, la meilleure extension Django est `Django REST Framework` (`djangorestframework`).

`REST` signifie « Representational State Transfer ». C'est un style d'architecture pour les API HTTP où chaque ressource est accessible via une URL et où les méthodes HTTP (GET, POST, PUT, DELETE) décrivent l'action à effectuer.

La `sérialisation` consiste à convertir des objets Python/Django en un format transportable comme JSON, puis à retransformer les données JSON reçues en objets Python pour les traiter. DRF (Django REST Framework) automatise cette conversion pour les modèles, les vues et les routes.

Installation :

```bash
pip install djangorestframework
```

Dans `settings.py` :

```python
INSTALLED_APPS = [
    # ...
    'rest_framework',
]
```

Puis créez un serializer et un viewset :

`serializers.py`
```python
from rest_framework import serializers
from .models import Student

class StudentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Student
        fields = '__all__'
```

`views.py`
```python
from rest_framework import viewsets
from .models import Student
from .serializers import StudentSerializer

class StudentViewSet(viewsets.ModelViewSet):
    queryset = Student.objects.all()
    serializer_class = StudentSerializer
```

`urls.py`
```python
from rest_framework.routers import DefaultRouter
from . import views

router = DefaultRouter()
router.register(r'students', views.StudentViewSet)

urlpatterns = [
    # autres urls...
] + router.urls
```

Avec ce router, Django REST Framework génère automatiquement les endpoints CRUD pour `/api/students/` et `/api/students/<id>/`.

### Tests de l'API

Pour tester l'API, vous pouvez utiliser `curl` :

```bash
curl http://localhost:8000/api/students/
```

Pour une expérience plus agréable sous Firefox, utilisez l'extension `RESTED` :
- installez `RESTED` depuis les modules complémentaires Firefox,
- envoyez des requêtes GET, POST, PUT, DELETE,
- inspectez les réponses JSON et les en-têtes HTTP.

`RESTED` facilite les tests de votre API localement sans quitter le navigateur.

### Automatisation avec une extension Django

La meilleure extension pour automatiser une API Django est `Django REST Framework`.

DRF vous permet de :
- sérialiser automatiquement les modèles,
- utiliser des viewsets génériques,
- générer des routes avec un router,
- obtenir une API navigable et réutilisable.

En installant `djangorestframework` et en ajoutant `rest_framework` à `INSTALLED_APPS`, vous automatisez la création de votre API et simplifiez le partage de votre application avec des applications tierces.

### Exercice : API des transactions

Proposez une API `transactions` qui retourne les consommations jour par jour pour une période donnée.

- Exposez un endpoint `/api/transactions/` pour récupérer toutes les transactions.
- Ajoutez un filtre possible sur la plage de dates : `?start=2026-03-01&end=2026-03-07`.
- Ajoutez un endpoint ou une vue annexe `/api/transactions/daily/` qui renvoie un résumé jour par jour :

```json
[
  {"date": "2026-03-01", "total_amount": 123.45},
  {"date": "2026-03-02", "total_amount": 98.70}
]
```

Cet exercice permet de tester l'API de transactions en affichant les consommations quotidiennes et en vérifiant que les données peuvent être groupées et agrégées par date.

<!-- ## Etape 9 : Déploiement sur un serveur, manipulations à faire, sécurisation

Pour déployer en production : **Docker** permet de conteneuriser l'application pour un déploiement facile.

Docker est un outil de virtualisation légère. Il emballe l'application et toutes ses dépendances dans une image unique, ce qui garantit que le code s'exécute de la même manière sur votre machine de développement, sur un serveur de test, ou en production. En pratique, on définit un `Dockerfile` qui indique :
- l'image de base à utiliser (ici Python 3.9),
- où copier les fichiers de l'application,
- les commandes d'installation des dépendances,
- l'exposition du port,
- la commande de démarrage.

### Dockerfile
Créez un `Dockerfile` :

```dockerfile
FROM python:3.9
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
RUN python manage.py collectstatic --noinput
EXPOSE 8000
CMD ["gunicorn", "cafeteria.wsgi", "--bind", "0.0.0.0:8000"]
```

### docker-compose.yml
Pour orchestrer services (app,

Effectuez des tests utilisateurs pour valider l'application :

### Notion d'API
Une API (Application Programming Interface) permet à d'autres applications d'interagir avec la vôtre via HTTP.

### JSON, le format des API
JSON est le format standard pour échanger des données : `{"key": "value"}`.


#### Exemple REST API avec HTTP

**Créer un étudiant (POST) :**
```
POST /api/students HTTP/1.1
Host: cafeteria.ensea:8000
Content-Type: application/json
Content-Length: 45

{"name": "Charlie", "email": "charlie@ensea.fr"}
```
**Réponse (201 Created) :**
```
HTTP/1.1 201 Created
Content-Type: application/json
Location: /api/students/3

{"id": 3, "name": "Charlie", "email": "charlie@ensea.fr"}
```

**Récupérer tous les étudiants (GET) :**
```
GET /api/students HTTP/1.1
Host: cafeteria.ensea:8000
Accept: application/json
```
**Réponse (200 OK) :**
```
HTTP/1.1 200 OK
Content-Type: application/json

[{"id": 1, "name": "Alice"}, {"id": 2, "name": "Bob"}, {"id": 3, "name": "Charlie"}]
```

**Mettre à jour un étudiant (PUT) :**
```
PUT /api/students/1 HTTP/1.1
Host: cafeteria.ensea:8000
Content-Type: application/json

{"name": "Alice Updated", "email": "alice.new@ensea.fr"}
```
**Réponse (200 OK) :**
```
HTTP/1.1 200 OK
Content-Type: application/json

{"id": 1, "name": "Alice Updated", "email": "alice.new@ensea.fr"}
```

**Supprimer un étudiant (DELETE) :**
```
DELETE /api/students/1 HTTP/1.1
Host: cafeteria.ensea:8000
```
**Réponse (204 No Content) :**
```
HTTP/1.1 204 No Content
``` -->


<!-- Dans `settings.py` : Ajoutez `'rest_framework'` à `INSTALLED_APPS`.

Créez des serializers :

```python
from rest_framework import serializers
from .models import Student

class StudentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Student
        fields = '__all__'
```

Dans `views.py` :

```python
from rest_framework import viewsets
from .models import Student
from .serializers import StudentSerializer

class StudentViewSet(viewsets.ModelViewSet):
    queryset = Student.objects.all()
    serializer_class = StudentSerializer
```

Dans `urls.py` :

```python
from rest_framework.routers import DefaultRouter
from . import views

router = DefaultRouter()
router.register(r'students', views.StudentViewSet)

urlpatterns = [
    # ...
] + router.urls
```

### Tests de l'API
Utilisez curl : `curl http://localhost:8000/api/students/`.
```
Ou Postman pour tester les endpoints CRUD.
version: '3'
services:
  web:
    build: .
    ports:
      - "8000:8000"
    depends_on:
      - db
  db:
    image: postgres
    environment:
      POSTGRES_DB: cafeteria
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
``` -->
<!-- 
Lancez avec `docker-compose up`.

1. **Serveur** : Utilisez un VPS (ex. : DigitalOcean, OVH).
2. **Installer Python et pip** : `sudo apt update && sudo apt install python3 python3-pip`.
3. **Cloner le repo** : `git clone <url>`.
4. **Configurer l'environnement** : Créer venv, installer requirements (`pip install -r requirements.txt`).
5. **Base de données** : Utilisez PostgreSQL au lieu de SQLite. Installez `psycopg2`, configurez `DATABASES` dans `settings.py`.
6. **Collecter statiques** : `python manage.py collectstatic`.
7. **Serveur web** : Utilisez Gunicorn (`pip install gunicorn`), lancez avec `gunicorn cafeteria.wsgi`.
8. **Reverse proxy** : Installez Nginx, configurez pour proxy vers Gunicorn.
9. **Sécurisation** :
   - Changez `DEBUG = False`.
   - Utilisez HTTPS (Let's Encrypt).
   - Configurez `SECRET_KEY` sécurisée.
   - Limitez `ALLOWED_HOSTS`.
   - Utilisez un firewall (ufw). -->

<!-- ## Etape 9 : Conteneurisation Docker et docker-compose -->

