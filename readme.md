Angular project Pamiers
===

<h2>Point sur TypeScript</h2>

<h2>Masterclass Angular</h2>

<h2>Install Angular</h2>

<h2>Principales commandes</h2>

<h2>Démo appli E-commerce</h2>

**SPECIFICATION GENERALE**

L'appli propose d'afficher des produits ou articles classés par catégories accessibles via notre api, d'en selectionner un ou plusieurs pour constituer un caddy avec la possibilitée de passer commande à tout moment à condition d'être aunthentifié, enfin de "régler en ligne".

D'après les cas d'utilisation identifiés, il y a 3 rôles : 
- utilisateur non connecté ou individu lambda qui peut naviguer sur votre site et consulter les infos des produits proposés par catégorie
- utilisateur connecté donc authentifié qui peut réaliser un panier constitué d'un ou plusieurs produits puis passer commande
- administrateur qui peut changer les photos des produits, modifier les infos.

**SPECIFICATIONS TECHNIQUES / CONCEPTION** 

- Spring au niveau du back (java 8, api Rest) ou constituer une api avec Php/Rest
- bdd mysql ou mariadb
- Angular 8 pour le front (bootstrap3, jquery) 
- Intégration continue avec Git

- Gestion des photos : elles ne seront pas stocké en base pour ne pas alourdir celle-ci, chaque produit aura un attribut qui pointe sur le fichier correspondant (chemin) 
- vous ne devez pas accepter les photos de plus de 1.5MB (back)
- les photos des produits seront stockés dans un dossier respectant ce chemin : "user.home" + /ecom/products
- les photos des catégories seront dans : "user.home" + /ecom/categories

- la gestion de l'authentification se fera pour le moment côté front avec des données fictives locales (tableau avec noms des utilisateurs et leurs rôles : USER et(ou) ADMIN) "prochain Sprint : il faudra le gérer côté back"
- L'utilisateur ou token (user + roles) sera stocké en local storage afin de permettre la navigation sans déconnexion


**SPECIFICATIONS FONCTIONELLES -> POUR LES VISITEURS DU SITE, l'appli doit :**

- afficher la liste des produits selectionnable (ou accessible) au niveau du back (page d'accueil ou home)
		
		-> afficher les photos de chaque produit, prévoir une photo de substitution
		
- afficher la liste des produits correspondant à une catégorie par le simple clic sur celle ci	
- afficher le pointer vers la catégorie ou produit survolée avec la souris (pour clic)
- afficher la liste des produits d'une catégorie cliqué
- les catégories non selectionnés doivent apparaitre en grisées
- afficher sous chaque produit des icones signifiant s'ils sont selectionnés, en promotion ou disponible
- lorsqu'on clic sur une photo, afficher les informations détaillées sur le produit correspondant 

		-> (nom, description, prix, promotion o/n, selection o/n, dispo o/n)

**SPECIFICATIONS FONCTIONELLES -> POUR LES ADMINISTRATEURS DU SITE, l'appli permet :**

- considérant ici, qu'ils ont déjà un compte, il faut proposer un formulaire d'authentification (côté front uniquement)
- une fois authentifié, il doit le rester tant qu'il ne se déconnecte pas (stockage dans le local storage)
- de changer la photo d'un produit par l'accès à l'explorateur de fichiers côté front :

		-> cela provoquera l'envoi de la photo au niveau du back ou elle sera stocké

		-> la nouvelle photo devra instantanément être affiché sur le front

- l'admin peut acceder naturellement aux infos d'un produit mais en plus, il peut les modifier, ce qui met à jour le back...

**SPECIFICATIONS FONCTIONELLES -> POUR LES UTILISATEURS donc authentifiés, l'appli doit :**

- considérant ici, qu'ils ont déjà un compte, il faut proposer un formulaire d'authentification (côté front uniquement)
	"la création d'un compte utilisateur inexistant pourra faire l'objet d'un 3ème sprint (à gérer en base côté back]"
- une fois authentifié, il doit le rester tant qu'il ne se déconnecte pas (stockage dans le local storage)
- permettre de créer un panier/caddy dans le local storage, composé d'un ou plusieurs produits
- afficher le contenu d'un caddy (id,liste des produits, quantité, prix(qté*prix produit), total caddy)
- prévoir un bouton pour supprimer un ou plusieurs éléments de notre caddy
- revenir à tout moment sur la liste des produits pour ajouter dans le caddy en cours
		
		-> si l'ajout concerne un produit déjà présent dans le caddy, il faut juste augmenter la quantité de celui-ci
- passer une commande d'un caddy pour l'utilisateur ou une tierce personne :
		
		-> prévoir de remplir tous les champs de la fiche client : nom adresse tel email => NEXT
		
		-> afficher une fiche récapitulative de la commande avec toutes les infos : Client + N° cde + date cde + total
		
		-> une fois la commande validé, il faut la céer au niveau du back avec id, numéro de commande, date puis l'indiquer côté front instantanément
		
		-> passer à la phase paiement bien qu'elle soit fictive ici (pour l'ex, nous n'utiliserons pas de vraies plate forme de paiement en ligne)

<h2>Ressources</h2>

https://angular.io/tutorial

[YouTube](https://youtu.be/xpMGCZw0UBA)

**DERNIERES CONSIGNES :**

- Ne réinventez pas la roue, si le framework propose déjà des méthodes ou micro services, utiliser les au lieu de refaire les choses
- Documenter vos codes
- Bonnes pratiques de code/fichier (maj/min, indentation..)
- Les noms de composants, classe, attributs, méthodes/fonctions et variables in english please (explicite et compréhensible)
- Astuce ici : la partie back peut être développé par une seule personne, une fois lancé, les micro services seront accessibles uniquement sur son pc tel un serveur dédié !

**LE SAVIEZ VOUS ?**

--> NOTRE APPLI UTILISE LA SPECIFICATION JPA POUR LE MAPPING OBJET RELATIONNEL, SPRING UTILISE PAR DEFAUT HYBERNATE QUI EST UNE IMPLEMENTATION DE CELLE-CI MAIS EN REALITE ON PEUT EN UTILISER D'AUTRE DANS LA CONFIGURATION DE NOTRE APPLI...

--> NOTRE APPLI UTILISE LA SPECIFICATION JAXRS POUR LES SERVICES WEB DE TYPE RESTFUL, JERSEY EST UNE IMPLEMENTATION DE CELLE-CI...

--> NB CONCERNANT LE DEPLOIEMENT : Si votre hébergeur a déjà un serveur d'appli tel "Tomcat", vous devez générer un war, s'il n'en dispose pas (ex : serveur dédié), le jar est indispensable, dans ce cas, en démarrant l'appli, celle-ci démarre tomcat...

--> S'AGISSANT DE LA SECURITE, il y a 2 modes :
	- Sécurité basée sur les sessions et le cookies (stateful) / une session est stockée côté serveur qui envoi un cookie côté client
	- s'agissant des applis basées sur des api rest, on utilise JWT (stateless), on envoi username + pwd, on reçoit un token sécurisé

