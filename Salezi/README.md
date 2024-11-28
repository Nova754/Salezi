# SALEZI

## Documentation de l’API Salezi

### Introduction

Nous allons vous accompagner durant tout le long de l'installation et de la prise en main de notre solution qui vise à favoriser les intéractions entre vendeurs, managers Fnac et super administrateurs. Grâce à notre solution vous pourrez publier des offres de vente ainsi que les modifier et les supprimer et réaliser différentes transactions en fonction de votre rôle.

### Installation et configuration 

#### Logiciels utilisés

- **Node.js** : l'environnement d'exécution JavaScript utilisé pour développer et exécuter l'API du projet **Salezi**. [Node.js](https://nodejs.org/en)
  
- **npm** : il est utilisé pour installer et gérer les dépendances du projet, permettant une gestion efficace des packages nécessaires au fonctionnement de l'API.[npm](https://www.npmjs.com/)
  
- **Strapi** : un framework Headless CMS utilisé pour créer et gérer l'API de **Salezi**, avec une configuration flexible pour gérer les produits, les transactions, et les rôles des utilisateurs. [Strapi](https://strapi.io/)
  
- **SQLite** : la base de données relationnelle utilisée par défaut pour stocker les informations sur les produits, transactions et utilisateurs dans **Salezi**. [SQLite](https://www.sqlite.org/)
  
- **Postman** : Postman est l'outil utilisé pour tester l'API de **Salezi**, en particulier pour valider les routes liées à la gestion des produits, transactions et l'inventaire, et pour automatiser les tests avec une collection pré-configurée. [Postman](https://www.postman.com/)

#### Etape 1 - Installation des dépendances (node modules)
Dans le terminal, on installe les dépendances avant de pouvoir exécuter le projet. Dans le dossier racine du projet **Salezi**, on exécute la commande suivante : 

```bash
cd salezi
npm install
```

#### Etape 2 - Démarrage du projet 
Dans le terminal, on va dans le dossier **Salezi** et on exécute la commande suivante :

```bash
cd salezi
npm run develop
```
L'API sera disponible à l'adresse [http://localhost:1337](http://localhost:1337).



### Authentification
L'API utilise une authentification avec des tokens pour limiter l'accès à certaines fonctionnalités. On configure plusieurs utilisateurs :

**Fnac Manager :**
- ***First name*** = fnac manager
- ***Email*** = fnacmanager@gmail.com
- ***Password*** = Fnacmanagerpass.1

**Seller1 :**
- ***First name*** = seller1
- ***Email*** = seller1@gmail.com
- ***Password*** = Seller1pass.1

**Seller2 :**
- ***First name*** = seller2
- ***Email*** = seller2@gmail.com
- ***Password*** = Seller2pass.1

**Super admin :**
- ***First name*** : super admin
- ***Email*** = superadmin@gmail.com
- ***Password*** = Superadminpass.1

### Endpoints de l'API (URL spécifiques sur un serveur web qui permettent aux utilisateurs d'accéder à des bases de données ou des services via à l'API)
On utilise des méthodes HTTP : GET, POST, PUT, DELETE.

#### Authentification 

Pour avoir accès à l'API, on aura besoin de s'authentifier à l'aide d'un token que on devrait récupérer grâce à la route :
***GET***
- `GET /auth/local` : Récupérer le token de l'utilisateur

#### Products

***GET***
- `GET /products?populate=Images&populate=category&populate=seller&populate=transactions` : Récupérer les informations de tous les produits
- `GET /products/:documentId?populate=Images&populate=category&populate=seller&populate=transactions` : Récupérer les informations d'un produit à partir du documentId

***POST***
- `POST /products` : Créer un produit

***PUT*** 
- `PUT /products/:documentId` : Modifier les informations d'un produit à partir du documentId

***DELETE***
- `DELETE /products/:documentId` : Supprimer un produit à partir du documentId

#### Categories
 
***GET***
- `GET /categories` : Récupérer les informations de toutes les catégories
- `GET /categories/:documentId` : Récupérer les informations d'une catégorie à partir du documentId
 
***POST***
- `POST /categories` : Créer une catégorie
 
***PUT***
- `PUT /categories/:documentId` : Modifier les informations d'une catégorie à partir du documentId
 
***DELETE***
- `DELETE /categories/:documentId` : Supprimer une catégorie à partir du documentId
 
#### Transactions
 
***GET***
- `GET /transactions` : Récupérer les informations de toutes les transactions
- `GET /transactions/:documentId` : Récupérer les informations d'une transaction à partir du documentId
 
***POST***
- `POST /transactions` : Créer une transaction
 
***PUT***
- `PUT /transactions/:documentId` : Modifier les informations d'une transaction à partir du documentId
 
***DELETE***
- `DELETE /transactions/:documentId` : Supprimer une transaction à partir du documentId

#### Images
***GET***
- `GET /upload/files` : Récupérer toutes les images de Media Library

### Tester l'API avec Postman

Pour vérifier que les requêtes de l'API fonctionne, on utilise Postman :

1. On ajoute au début de l'URL `http://localhost:1337/api` dans les requêtes.

2. Pour récupérer le token et pouvoir s'authentifier après:
- on va dans l'onglet **Body**
- puis sur **raw**
- on choisit **JSON**
- on écrit l'identifiant (email) et le mot de passe de l'utilisateur : 

***Exemple***
```json
{
    "identifier": "fnacmanager@gmail.com",
    "password": "Fnacmanagerpass.1"
}
```

3. Pour s'authentifier et utiliser les différentes routes :
- on va dans l'onglet **Authorization**
- on choisit le type d'Authentification **Bearer Token**
- on écrit le token JWT qu'on a obtenu avec la route ***GET*** `GET /auth/local`

4. Pour afficher l'image d'un produit après avoir récupérer un produit, on va sur ce lien qui renvoie à une autre requête postman qui affiche l'image :
```json 
{
"url": "/uploads/thumbnail_615_T9_Mo_B_Cv_L_AC_UF_350_350_QL_50_387921bf05.jpg"
}
```

5. Signification des codes de statut HTTP qui s'affichent à chaque requête
    - **200 OK**
      - La requête a réussi. Le serveur a renvoyé la réponse demandée. 

    - **201 Created**
      - La requête a été réussie et qu’une nouvelle ressource a été créée à la suite de cette requête. 

    - **204 No Content**
      - La requête a été réussie, mais qu’il n’y a pas de contenu à renvoyer. 

    - **400 Bad Request**
      - La requête envoyée au serveur est mal formée ou invalide. Cela peut être dû à des données manquantes ou à une syntaxe incorrecte.

    - **401 Unauthorized**
      - L’utilisateur doit s’authentifier pour accéder à la ressource demandée. 

    - **403 Forbidden**
      - Le serveur a compris la requête, mais refuse de l’exécuter. Cela peut être dû à des permissions insuffisantes pour accéder à la ressource.

    - **404 Not Found**
      - Le serveur n’a pas trouvé la ressource demandée. Cela se produit souvent lorsque l’URL demandée est incorrecte ou lorsque la ressource a été supprimée.

    - **500 Internal Server Error**
      - Il y a eu une erreur inattendue sur le serveur lors du traitement de la requête. Cela peut être dû à un bug dans le code du serveur ou à un problème avec la configuration du serveur.