# modularite_TD_1_Partie_1

# Modularite partie 1

Voici un exemple de portefeuille de cas d'injection SQL. Chaque exemple est suivi d'une explication de l'attaque visée :

### Exemple d'attaque d'injection SQL : récupération de toutes les données d'une table
``sql``

``
SELECT * FROM utilisateurs WHERE id='1' OR '1'='1';
``
> Cette attaque vise à récupérer toutes les données de la table "utilisateurs". En utilisant la clause OR '1'='1', l'attaquant parvient à contourner la condition et à obtenir toutes les lignes de la table.


### Exemple d'attaque d'injection SQL : suppression de données
``sql``

``
DELETE FROM utilisateurs WHERE id='1' OR '1'='1';``
>Cette attaque vise à supprimer des données de la table "utilisateurs". En utilisant la clause OR '1'='1', l'attaquant parvient à contourner la condition de suppression et à supprimer toutes les lignes de la table.

### Exemple d'attaque d'injection SQL : récupération des informations d'identification
``sql``

``
SELECT * FROM utilisateurs WHERE nom_utilisateur='admin' -- ' AND mot_de_passe='123456';``
>Cette attaque vise à récupérer les informations d'identification d'un utilisateur en exploitant une injection SQL aveugle. En utilisant le symbole "--" pour commenter la fin de la requête, l'attaquant peut contourner la vérification du mot de passe et récupérer les informations de l'utilisateur "admin".

### Exemple d'attaque d'injection SQL : ajout d'un nouvel utilisateur
``sql``

``INSERT INTO utilisateurs (nom_utilisateur, mot_de_passe) VALUES ('pirate', 'password123');``
>Cette attaque vise à ajouter un nouvel utilisateur à la table "utilisateurs". L'attaquant peut insérer des valeurs arbitraires dans la requête pour créer un nouvel utilisateur avec des informations d'identification de son choix.

### Exemple d'attaque d'injection SQL : mise à jour des données
``sql``
``UPDATE utilisateurs SET mot_de_passe='newpassword' WHERE id='1';``
>Cette attaque vise à mettre à jour les données d'un utilisateur existant. En modifiant la valeur de la colonne "mot_de_passe", l'attaquant peut changer le mot de passe d'un utilisateur sans autorisation appropriée.




### Exemple d'attaque d'injection SQL : contournement de l'authentification
``sql``

``
SELECT * FROM utilisateurs WHERE nom_utilisateur='' OR '1'='1' -- ' AND mot_de_passe='' OR '1'='1';
``
>Cette attaque vise à contourner le processus d'authentification en exploitant l'injection SQL. En utilisant la clause OR '1'='1' pour chaque condition, l'attaquant peut bypasser la vérification du nom d'utilisateur et du mot de passe, lui permettant d'accéder aux informations de l'utilisateur sans connaître les informations d'identification correctes.


### Exemple d'attaque d'injection SQL : récupération des données sensibles
``sql``

``SELECT * FROM informations_sensibles WHERE id=1 UNION SELECT numéro_de_carte_de_crédit, NULL, NULL FROM utilisateurs;``
>Cette attaque vise à récupérer des données sensibles, telles que les numéros de carte de crédit, en exploitant l'injection SQL. L'attaquant utilise une injection UNION pour combiner les résultats de deux requêtes : une requête légitime et une requête qui extrait les numéros de carte de crédit de la table des utilisateurs.

### Exemple d'attaque d'injection SQL : exécution de commandes SQL supplémentaires
``sql``

``
SELECT * FROM utilisateurs; DROP TABLE utilisateurs;``
>Cette attaque vise à exécuter des commandes SQL supplémentaires, en l'occurrence, la suppression de la table "utilisateurs". L'attaquant insère une commande DROP TABLE après la requête légitime pour supprimer la table et causer des dommages à la base de données.

### Exemple d'attaque d'injection SQL : exfiltration de données
``sql``

``SELECT * INTO OUTFILE '/var/www/html/attaque.txt' FROM utilisateurs;``
>Cette attaque vise à exfiltrer des données de la base de données vers un fichier externe. L'attaquant utilise la clause INTO OUTFILE pour spécifier un emplacement de fichier sur le serveur web, lui permettant de récupérer toutes les données de la table "utilisateurs" dans un fichier texte.

### Exemple d'attaque d'injection SQL : exécution de commandes système
``sql``

``
SELECT * FROM utilisateurs; ; DELETE FROM utilisateurs;``
>Cette attaque vise à exécuter des commandes système en utilisant une injection SQL. L'attaquant insère une commande supplémentaire après la requête légitime en utilisant un point-virgule (;) pour exécuter la commande DELETE FROM utilisateurs, ce qui entraîne la suppression de toutes les données de la table "utilisateurs".