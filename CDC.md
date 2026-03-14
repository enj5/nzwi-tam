# Cahier des charges
# NZWÌ-TAM, The Panther of the Game 

## 1-	Présentation du projet  

### 1-1-	Contexte 
Projet personnel réalisé dans le cadre d'une alternance en Data Analysis, visant à monter en compétence sur la modélisation et la manipulation de bases de données relationnelles complexes, à travers la conception d'un projet full-stack complet.
### 1-2-	Présentation de la marque
NZWÌ-TAM est une marque sportive africaine à rayonnement international, spécialisée dans la conception et la commercialisation d'équipements de football. Son nom, issu de la langue Mə̀dʉ̂mbὰ (Medumba) de l'Ouest Cameroun, il provient de “Nzwìmα̂ntɔ̀” = “Panthère” et de “Tamnkò” = “Football” qu’on peut traduire par "La Panthère du Football". La marque sponsorise des joueurs et des clubs de football, et commercialise ses produits auprès de particuliers (BtoC) et de revendeurs (BtoB).
### 1-3-	Objectifs du projet
-	Concevoir et modéliser une base de données relationnelle complexe sous PostgreSQL
-	Développer un site web full-stack connecté à cette base de données
-	Intégrer un module de reporting via Power BI Desktop
-	Produire un projet de portfolio démontrant des compétences en data et développement web

### 1-4-	Public cible de la plateforme
-	Clients particuliers (BtoC) — achat de produits en ligne
-	Clients revendeurs (BtoB) — commandes en volume
-	Employés internes — gestion du stock, sponsoring, reporting (back-office)
Profil	Accès	Description
Client particulier	Public	Achète des produits en ligne (BtoC)
Client revendeur	Public	Passe des commandes en volume (BtoB)
Employé — Commercial	Back-office	Gère les commandes, clients BtoB
Employé — Logisticien	Back-office	Gère le stock et l'entrepôt
Employé — Responsable sponsoring	Back-office	Gère les contrats, joueurs, clubs
Administrateur	Back-office	Accès total, gestion des utilisateurs

Architecture de navigation
/ ..................................... Accueil
/boutique ....................... Catalogue produits
/boutique/produit ........... Fiche produit
/commande .................... Panier & commande
/compte .......................... Espace client (login)
/ambassadeurs ................ Vitrine sponsoring (public)
/admin ............................. Back-office (login requis)
     /admin/sponsoring ...... Joueurs, clubs, contrats
    /admin/stock ................ Entrepôt, mouvements
    /admin/commercial ...... Clients BtoB, commandes
    /admin/reporting …...... Dashboards Power BI
    /admin/users ................. Gestion des utilisateurs

Comportement à implémenter :
Navigation boutique et fiches produits → libre, sans compte
Ajout au panier ou commande → redirection automatique vers /auth/connexion
Si pas de compte → lien vers /auth/inscription – et MAJ de la BDD
Une fois connecté → retour automatique au panier


## 2-	Périmètre fonctionnel : 
### 2-1-	Module 1 — Boutique (Public)
#### a-	Catalogue produits
•	Affichage de tous les produits disponibles
•	Filtres par catégorie, taille, couleur, prix
•	Tri par popularité, prix croissant/décroissant, nouveautés
•	Pagination des résultats

#### b-	Fiche produit
•	Affichage des détails du produit (nom, description, prix, stock disponible)
•	Sélection de la taille et de la couleur
•	Produits associés (même catégorie)
•	Ajout au panier → redirection login si non connecté

#### c-	Authentification client
•	Création de compte (nom, prénom, email, mot de passe, adresse)
•	Connexion / Déconnexion
•	Mot de passe oublié

#### d-	Espace client
•	Gestion du profil et des adresses
•	Panier (ajout, modification, suppression)
•	Passage de commande
•	Suivi et historique des commandes

#### e-	Vitrine Ambassadeurs
•	Liste des joueurs et clubs sponsorisés
•	Fiche ambassadeur (identité, club, palmarès, produits associés)

### 2-2-	Module 2 – Back-office (Accès restreint)
#### a-	Gestion des utilisateurs (Administrateur)
•	Création et gestion des comptes employés
•	Attribution des rôles (administrateur, commercial, logisticien, responsable sponsoring)
•	Activation / désactivation des comptes

#### b-	 Gestion du stock & entrepôt (Logisticien)
•	Tableau de bord stock (niveaux, alertes rupture)
•	Entrées de stock (approvisionnements fournisseurs)
•	Sorties de stock (commandes expédiées)
•	Historique des mouvements de stock
•	Gestion des fournisseurs

### 2.3	Gestion commerciale BtoB et BtoC (Commercial)
•	Gestion des clients revendeurs (fiche entreprise, conditions tarifaires)
•	Gestion des commandes BtoB et BtoC (volume, délais, conditions de paiement)
•	Suivi des paiements

### 2.4	Gestion du sponsoring (Responsable sponsoring)
•	Fiche joueur (identité, club, championnat, statistiques de performance)
•	Fiche club (identité, championnat, palmarès, effectif)
•	Gestion des contrats de sponsoring (durée, montant, conditions)
•	Module d'aide à la décision pour la négociation
•	Alertes contrats expirant bientôt
### 2.5	Reporting (Tous rôles selon périmètre)
•	Dashboards Power BI intégrés
•	Ventes BtoC et BtoB
•	Performance des stocks
•	Analyse des sponsorisations

## 3-	Périmètre technique 
### 3-1-	Stack technique
Composant	Outil	Rôle
BDD	PostgreSQL + pgAdmin4	Stockage et gestion des données - Administration et requêtage
Back-end	WampServer (PHP)	nvironnement de développement
Front-end	HTML/CSS/JavaScript	Interface utilisateur
Reporting	Power BI desktop	Dashboards et analyses
Versionning	Git/GitHub	Suivi du code et sauvegarde

### 3-2-	Contraintes techniques
•	La BDD est entièrement conçue et modélisée from scratch
•	Les données footballistiques sont issues de sources publiques (Kaggle, football-data.co.uk)
•	Les données e-commerce (produits, clients, commandes) sont générées ou saisies manuellement
•	Projet hébergé en local via WampServer (pas de mise en production)
•	Tout le code est versionné sur GitHub dès le début du projet
Options Claude IA : 
________________________________________
🗂️ Options pour les données e-commerce
Option 1 — Génération automatique (recommandé)
Des outils génèrent des fausses données réalistes automatiquement :
•	Mockaroo (mockaroo.com) — tu définis tes colonnes, il génère un CSV prêt à importer dans PostgreSQL. Clients, commandes, adresses... tout est personnalisable
•	Faker (bibliothèque Python) — génère des données en masse via un script, très flexible
Option 2 — Datasets publics e-commerce
Des jeux de données e-commerce réels existent sur :
•	Kaggle — cherche "e-commerce dataset", tu trouveras des datasets avec commandes, clients, produits
•	Tu adaptes ensuite la structure à ton schéma BDD
Option 3 — Saisie manuelle partielle
Uniquement pour les produits NZWÌ-TAM — tu crées toi-même une vingtaine de produits réalistes (maillots, chaussures, ballons...) pour que la boutique soit crédible
________________________________________
💡 Ma recommandation
Données	Source
Produits	Saisie manuelle (une trentaine de produits)
Clients	Mockaroo
Commandes	Mockaroo ou Kaggle
Joueurs / Clubs	Kaggle / football-data.co.uk
________________________________________

### 3-3-	Sécurité
•	Gestion des rôles et accès en BDD
•	Protection contre les injections SQL via PDO et requêtes préparées (secondaire)
•	Authentification par session PHP (secondaire)
•	Mots de passe hashés (bcrypt) (intersting)

## 4-	Modélisation des données (Peut-être pas ici !!)

## 5-	Livrables attendus
### 5-1-	Base de données
•	Schéma relationnel complet (MCD + MLD) 
•	Script SQL de création de la BDD
•	Scripts SQL d'insertion des données
•	Bibliothèque de requêtes SQL avancées documentées
### 5-2-	Application web
•	Site e-commerce public (boutique, fiches produits, espace client)
•	Back-office complet (stock, sponsoring, commercial, reporting)
•	Code source versionné sur GitHub
### 5-3-	Reporting
•	Dashboards Power BI connectés à PostgreSQL
•	Rapport de ventes BtoC / BtoB
•	Rapport de performance des stocks
•	Rapport d'analyse des sponsorisations
### 5-4-	Documention
•	Cahier des charges (ce document)
•	Dictionnaire de données (description de chaque table et colonne)
•	Guide d'installation et de configuration de l'environnement


## 6-	Hors périmètre
… (many things)

## 7-	Planification
Je me fixe 3 mois pour le réaliser. Pour y arriver, je dois être discipliné, ne pas viser absolument la perfection à chaque étape. L’objectif ici est d’avoir un projet fonctionnel et propre, pas un produit commercial fini.


