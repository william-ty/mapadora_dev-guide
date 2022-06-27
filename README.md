# Acrobatt LP4 - Développement
________________________________________
## API

### Outils de développement utilisés
- Visual Studio (IDE)
- DBeaver (Gestion de BDD)
- Postman (Tests)
- Newman (Tests CLI)
- Navigateur Web (Consulter la documentation générée)


### Setup
- Installer Postgresql.
- Installer l'extension Postgis.
- Créer une base de donnée nommée 'acrobatt'.
- Installer Node.js.
- Cloner le repo Gitlab.
- Lancer `npm install` à la racine du projet.
- Dans le dossier 'config' du projet: 
  - Copier et renommer le fichier 'config-example.json' en 'config.json'.
  - Remplacer la valeur du champ 'username' par l'utilisateur Postgresql concerné (par default 'postgres').
  - Remplacer la valeur du champ 'password' par le mot de passe associé à cet utilisateur.
  - Remplacer la valeur du champ 'database' par le nom donné à la base ('acrobatt') .
- Copier le fichier d'environnement d'exemple '.env-exemple' et le renomer '.env'.

- Stocker le jeton secret utilisé pour chiffrer les données (JWT) :
-   À l'aide de node, générer un jeton secret: saisir `node` en CLI, puis `require('crypto').randomBytes(64).toString('hex')`.
    Une chaine de caractère est alors générée.
  - Donner pour valeur la clé générée à la variable 'TOKEN_SECRET='.
- Renseigner les identifiants smtp pour l'envoi d'email :
  - Assigner au variables 'MAILER_PASS' et 'MAILER_SMTP' les identifiants nécessaires à l'envoi d'email.
- Lancer la commande `npm run dev`.
  Les tables de la base de donnée sont générées et le programme lancé.
- Lancer la commande `npm run seed` pour générer les données nécessaires au bon fonctionnement du projet, grâce aux seeders.

###### Vous êtes prêts à vous lancer !

### Tests
- Lancer Postman.
- Se positionner à la racine du dossier 'newman_folder'.
  - Pour Windows, lancer la commande suivante `newman run https://www.getpostman.com/collections/efaee735f77861799640 -e .\localhost.postman_environment.json`
  - Pour Unix, lancer la commande suivante `newman run https://www.getpostman.com/collections/efaee735f77861799640 -e /localhost.postman_environment.json`

### Organisation du projet 

#### Cas d'utilisation : Ajout d'une fonctionnalité

Décrivons les étapes pour ajouter une fonctionnalité fictive afin d'avoir une meilleure compréhention de l'organisation du projet.
(En découle la modification d'une fonctionnalité).

##### Ajout de penses-bêtes (Notes)

##### - Création de l'entité

`npx sequelize-cli model:generate --name Note --attributes name:string`
(Des exemples de scripts sont disponibles dans le fichier '/scripts_sequelize/models')
Le model Note a été créé dans le répértoire /src/models/

##### - Création du controlleur
Le controlleur traveltag_controller est un bon exemple de controleur de base.
En étandant la classe AppControlleur, le controlleur créé hérite des méthodes de base (CRUD) et bénéficie de cette couche d'abstraction.
Elles peuvent étre cependant surchargées pour des cas particuliers.

Controlleur de base :

![Semantic description of image](/images/controleur.png "Controleur de base")

##### - Création des routes

Le fichier de routes traveltag_routes constitue un bon exemple.
Une fois les routes ajoutées, il est possible de les sécuriser à l'aide de JWT par la méthode 'identify_client'.

Routes de base :

![Semantic description of image](/images/routes.png "Routes de base")

Routes sécurisées :

![Semantic description of image](/images/routes_securise.png "Route sécurisée")


##### - Inclusion et paramétrage des routes 

Dans la partie 'ROUTES' du fichier '/app.js' ajouter une variable contenant les routes :
`const note = require("./src/routes/note_routes");`
et la mettre en service : `app.use("/traveltag", traveltag);`


<!-- ![Semantic description of image](/images/path/to/folder/image.png "Image Title") -->


#### Arborescence

Informations principales :

- Le dossier `/src/models/` contient les entités, générables à l'aide de commande en exemple dans le dossier `/scripts_sequelize`
- Le dossier `/src/controllers/` contient les controleurs. Un controleur peut bénéficier de l'abstraction du controleur `/src/controllers/app_controller` (voir l'exemple `/src/controllers/traveltag_controller`), ou etre personnalisé à souhait.
- Le dossier `/src/routes/` contient les routes et la documentation Swagger par annotations. Le fichier `/src/controllers/traveltag_routes` est un exemple de CRUD et de routes de base.
- Le dossier `/src/seeders/` contient les seeders pérmettant de générer des jeux de données. La création d'un tel fichier peut être facilité avec les commandes disponibles dans le dossier `/scripts_sequelize/seeders/`
- Le fichier `/app.js` référence l'ensemble de la configuration de l'API et permet de modifier/ajouter des routes au sein de sa rubrique 'ROUTES'.

#### Documentation
https://mapadora.fr:8443/docs
______________________________________________
## WEB

### Outils de développement utilisés
- Visual Studio (IDE)
- Navigateur Web

### Setup
- Installer Node.js.
- Cloner le repo Gitlab.
- Lancer `npm install` à la racine du projet.
- Lancer `npm start` à la racine du projet.

###### Vous êtes prêts à vous lancer !

### Organisation du projet 

#### Arborescence

Informations principales :

- Le fichier `/src/api/api.ts` référence les fonctions d'appel à l'API, génériques pour certaines (CRUD).
  Il est possible d'ajouter des fonctions de fetch à l'API dans ce fichier. (penser à ajouter le type pour Typescript)
- Le dossier `/src/components/` contient les composants React, eventuellement groupés par dossiers.
- Le dossier `/src/i18n/` comporte les fichiers de contenus textuels de l'application, triés par langues. 
- Le dossier `/src/model/` contient les entités, qui reflètent celles les données renvoyées par l'API. 
- Le dossier `/src/provider/` regroupe les déclarations des 'data providers' utilisés au sein de l'application.
(ex: authentification). 
- Le dossier `/src/theme/` reférence les modifications faites au thème Material UI et les variables facilement éditables pour changer l'identité graphique du site.
- Le fichier `/app.tsx/` est le composant de plus haut niveau, dans lequel est regroupé la logique globale de l'application.
On y retrouve notamment l'ensemble des routes définies renvoyant aux composants adaptés.
Il sert de conteneur pour le reste de l'application.

______________________________________________
## MOBILE

### Outils de développement utilisés
- Visual Studio (IDE)
- Périphérique mobile (Smartphone Android 5+ / IOS 12+)
- Application Expo Go (Google Play Store/Apple Store)

### Setup
- Installer Node.js.
- Installer Expo avec la commande `npm install --global expo-cli`.
- Installer l'application mobile Expo Go sur le périphérique de développment.
- S'assurer que le périphérique soit sur le même réseau que le poste de développement.
- Lancer `npm install` à la racine du projet.
- Lancer `npm start` à la racine du projet.
- Le QR code Expo s'affiche dans la console. Scanner le QR code à l'aide de l'app mobile Expo Go.

###### Vous êtes prêts à vous lancer !

### Organisation du projet 

#### Arborescence

Informations principales (l'application mobile présente une arborescence similaire à celle de l'application Web) :

- Le fichier `/src/api/api.ts` référence les fonctions d'appel à l'API, génériques pour certaines (CRUD).
  Il est possible d'ajouter des fonctions de fetch à l'API dans ce fichier. (penser à ajouter le type pour Typescript)
- Le dossier `/src/components/` contient les composants React, eventuellement groupés par dossiers.
- Le dossier `/src/model/` contient les entités, qui reflètent celles de la base de donnée. 
- Le dossier `/src/screens/` contient les composants plus globaux, des 'écrans' de navigation, eventuellement groupés par dossiers.
<!-- - Le dossier `/src/i18n/` comporte les fichiers de contenus textuels de l'application, triés par langues.  -->
- Le dossier `/src/provider/` regroupe les déclarations des 'data providers' utilisés au sein de l'application.
(ex: authentification). 
- Le dossier `/src/theme/` reférence les modifications faites au thème Material UI et les variables facilement éditables pour changer l'identité graphique du site.
- Le fichier `/app.tsx/` est le composant de plus haut niveau, il sert de conteneur pour le reste de l'application.

