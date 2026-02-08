# Rapport-Ventes-Power-BI

#### 1.	Lancer Power BI Desktop
#### 2.	Importer le fichier sales_1.csv dans Power Query
####

## 3.	Analyser le type de données et leur qualité 
o	Utiliser l’analyseur Power Query : 
- Qualité de la colonne
-	Distribution des colonnes
-	Profil de la colonne
o	Vérifier que les bons types de données sont appliqués à chaque colonne.

## 4.	Renommer les colonnes avec un libellé explicite 
Colonne initiale	Nouveau nom
OrderID	Id commande
CustomerID	Id client
CompanyName	Nom client
ProductID	Id produit
ProductName	Nom produit
Category	Catégorie produit
RegionID	Id région
RegionName	Nom région
OrderDate	Date commande
Quantity	Quantité
UnitPrice	Prix unitaire
TotalPrice	Prix total
OrderStatus	Statut commande
________________________________________
## 3) Normalisation
1.	Créer des tables de référence
o	À partir de la table brute (via l’option Référence), créer : 
-	Une table Clients (regroupement par Id client et Nom client)
-	Une table Produits (regroupement par Id produit, Nom produit et Catégorie produit)
-	Une table Régions (regroupement par Id région et Nom région)
## 2.	Vérifier l’absence d’anomalies
o	Contrôler qu’un même produit ou un même client n’apparaît pas sous deux identifiants différents.
o	Supprimer la colonne de comptage (“count”) générée par le regroupement.
o	Trier chaque table par son identifiant dans l’ordre croissant.
## 3.	Créer la table Ventes
o	Conserver la table d’origine pour la création de la table “Ventes”, mais ne pas la charger dans le modèle
o	Créez une référence à cette table et supprimez toutes les colonnes qui sont maintenant inutiles (notamment les colonnes d’id)
o	Charger les tables finales (Clients, Produits, Régions, Ventes) dans le modèle.
________________________________________
## 4) Création du modèle de données
1.	Observer les relations automatiques
o	Dans la vue Modélisation de Power BI, vérifier que des relations ont été créées automatiquement.
o	Afficher le détail d’une des relations (ex. relation entre la table Ventes et la table Clients).
2.	Démonstration de la relation
o	Insérer l’Id de commande et afficher le nom de produit pour vérifier la cohérence.
o	Supprimer une relation, puis la recréer manuellement.
________________________________________
## 5) Création du dashboard
5.1 Définition du thème
1.	Sélectionner un thème
o	Dans l’onglet Affichage > Thèmes, importez un thème personnalité
o	Exemple : Loomy Lime Theme. 
-	Télécharger le fichier JSON puis l’importer dans Power BI.
2.	Paramètres d’affichage
o	Régler la hauteur à 2000 px pour la page.
o	Définir la couleur de fond (#1E2D38) et la couleur des briques (#232448).
o	Disposer les éléments visuels selon un modèle prédéfini (maquette).
5.2 Création des mesures DAX
1.	Créer une table de mesures
o	Accueil > Entrer des données > Valider (vide) puis renommer en “Mesures”.
2.	Définir les mesures principales
o	Total ventes = SUM(Ventes[Prix total])
o	Nombre de commandes = DISTINCTCOUNT(Ventes[Id commande])
o	Quantité vendue = SUM(Ventes[Quantité])
o	Commande moyenne = DIVIDE([Total ventes], [Nombre de commandes])
5.3 Ajout des visuels dans le premier onglet
1.	4 indicateurs clés (KPI)
o	Afficher : 
-	Total ventes
-	Nombre de commandes
-	Quantité vendue
-	Commande moyenne
o	Personnalisez les éléments pour assurer la cohérence graphique du rapport
2.	Évolution du chiffre d’affaire et des volumes de ventes dans le temps
o	Créer un graphique de type Courbe ou Aires (personnaliser les couleurs dans les sous-menus).
3.	Répartition du CA par région
o	Graphique en barres horizontales pour comparer le chiffre d’affaires par région.
4.	Répartition du CA par catégorie de produit
o	Graphique en Donut (camembert en anneau).
5.	Tableau des commandes
o	Inclure les informations détaillées (id commande, client, produit, etc.).
o	Personnaliser les options (couleurs, police…).
5.4 Ajout des filtres
1.	Filtre de plage de dates
2.	Filtre sur le statut de commande
3.	Filtre sur la région
________________________________________
## 6) Création du deuxième onglet (commandes annulées)
1.	Dupliquer le premier onglet
o	Conserver la disposition générale des visuels.
2.	Créer 3 nouvelles mesures
o	Total commandes annulées =
CALCULATE(COUNT(Ventes[Id commande]), Ventes[Statut commande] = "Cancelled")
o	Montant commandes annulées =
CALCULATE(SUM(Ventes[Prix total]), Ventes[Statut commande] = "Cancelled")
o	Pourcentage commandes annulées =
DIVIDE([Total commandes annulées], [Nombre de commandes])
3.	Ajouter 3 KPI
o	Basés sur les mesures ci-dessus.
4.	Courbe d’évolution du % de commandes annulées
o	Représenter dans le temps l’évolution du pourcentage et du nombre de commandes annulées.
5.	Histogramme vertical
o	Répartition de la part de commandes annulées par région.
6.	Treemap
o	Répartition du CA des commandes annulées par catégorie de produits et par produit.
7.	Évolution trimestrielle par produit
o	Utiliser la visualisation “Ruban” pour analyser le nombre de commandes annulées par produit, au fil des trimestres.
________________________________________
## 7) Création du menu
1.	Ajouter les icônes fournies 
o	Les placer dans la bande de gauche.
o	Ajouter un lien vers chaque onglet du rapport (navigation).
________________________________________
## 8) Création d’info-bulles (tooltips)
1.	Info-bulle pour l’histogramme par région
o	Créer une page dédiée pour afficher la courbe d’évolution des ventes.
o	Configurer cette page en tant qu’info-bulle (tooltip) pour l’histogramme.
2.	Info-bulle pour le donut par catégorie de produit
o	Créer une page dédiée avec un visuel “Ruban” pour l’évolution des ventes par produit.
o	Configurer la page en tant qu’info-bulle pour le donut.
________________________________________
## Bonus
1.	Afficher le Pourcentage de Données Disponibles après Filtrage
o	Utiliser la visualisation personnalisée “PayPal KPI Donut Chart”.
o	Ajouter un cercle autour du KPI “Ventes totales” indiquant la part du chiffre d’affaires filtré.
2.	Ajouter des signets (Bookmarks)
o	Créer un signet pour filtrer les produits “mobiles” (Smartphone, Headphone, SmartWatch).
o	Créer un signet pour filtrer les produits “bureautique” (Tablet, Monitor, Laptop, Keyboard, Mouse).
o	Créer un signet pour réinitialiser tous les filtres.
o	Associer chaque signet à de nouvelles icônes (fournies) dans le menu.
3.	Créer des rôles (Row-Level Security)
o	Rôle 1 : accès uniquement aux commandes des sociétés “AI Systems” et “TechCorp”.
o	Rôle 2 : accès uniquement aux commandes de la région “South”.
4.	Créer une version mobile du tableau de bord
o	Dans la vue Création de la version mobile, adapter le premier onglet “Suivi ventes” : 
-	Conserver les filtres principaux (date, statut, région).
-	Supprimer les éléments de menu.
-	Replacer les visuels de manière adaptée (sauf le tableau détaillé qui peut être omis).
5.	Publier le rapport sur Power BI Service
o	Se connecter à Power BI Service et procéder à la publication du fichier .pbix.
________________________________________

Fin de projet. Vous disposez désormais d’un tableau de bord Power BI avec un modèle de données correctement structuré, plusieurs onglets d’analyse, un système de filtres, des info-bulles avancées, un menu de navigation, des signets et des rôles de sécurité.

