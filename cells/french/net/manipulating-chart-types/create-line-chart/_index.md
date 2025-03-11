---
title: Créer un graphique linéaire
linktitle: Créer un graphique linéaire
second_title: API de traitement Excel Aspose.Cells .NET
description: Créez de superbes graphiques en courbes à l'aide d'Aspose.Cells pour .NET. Suivez notre guide étape par étape pour visualiser efficacement vos données.
weight: 11
url: /fr/net/manipulating-chart-types/create-line-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un graphique linéaire

## Introduction

Êtes-vous prêt à visualiser vos données avec une clarté époustouflante ? Les graphiques en courbes sont un moyen fantastique d'afficher les tendances au fil du temps ou la relation entre deux variables. Que vous gériez des données pour un projet professionnel ou que vous analysiez des indicateurs personnels, la possibilité de créer des graphiques en courbes par programmation peut vous faire gagner du temps et vous offrir une plus grande flexibilité. Dans ce guide, nous vous guiderons à travers chaque étape de la création d'un graphique en courbes à l'aide d'Aspose.Cells pour .NET. Prêt à vous lancer ? Commençons !

## Prérequis

Avant de passer aux détails de la création d'un graphique linéaire, assurons-nous que vous êtes équipé pour suivre :

1. Visual Studio : assurez-vous que Visual Studio est installé sur votre ordinateur, car il s’agit de l’un des IDE les plus populaires pour le développement .NET.
2.  Bibliothèque Aspose.Cells pour .NET : vous aurez besoin de la bibliothèque Aspose.Cells, que vous pouvez télécharger à partir de[ici](https://releases.aspose.com/cells/net/).
3. Connaissances de base de C# : la familiarité avec le langage de programmation C# vous aidera à mieux comprendre les exemples et les extraits de code.
4. .NET Framework ou .NET Core : une configuration de base de l’un ou l’autre framework, car ce sera la base de nos applications.

Une fois ces conditions préalables réglées, vous êtes prêt à créer des graphiques !

## Paquets d'importation

Maintenant que nous avons configuré notre environnement, nous devons importer les packages nécessaires dans notre code C#. Tout comme vous rassemblez vos outils avant de démarrer un projet, l'importation de packages est essentielle pour vous assurer d'avoir tout ce dont vous avez besoin.

Voici comment procéder :

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

 Cette ligne importe le`Aspose.Cells` espace de noms, qui contient toutes les classes et méthodes que nous utiliserons pour créer notre graphique linéaire.

Décomposons maintenant l'ensemble du processus en étapes simples et digestes. Chaque étape vous guidera à travers le flux logique de création d'un graphique en courbes à l'aide d'Aspose.Cells pour .NET.

## Étape 1 : Configurer le répertoire de sortie

La première étape consiste à définir l'emplacement où vous souhaitez enregistrer votre fichier de sortie. C'est comme configurer votre espace de travail avant de commencer à vous salir les mains. 

```csharp
// Répertoire de sortie
string outputDir = "Your Output Directory";
```
 Remplacer`"Your Output Directory"`avec le chemin réel où vous souhaitez enregistrer le fichier Excel généré.

## Étape 2 : instancier l'objet classeur

Ensuite, nous devons créer une nouvelle instance de classeur. Considérez le classeur comme la toile sur laquelle votre créativité va s'exprimer. 

```csharp
// Instanciation d'un objet Workbook
Workbook workbook = new Workbook();
```
Cette ligne initialise un nouveau classeur qui contiendra toutes vos données et visuels.

## Étape 3 : Accéder à la feuille de travail

Dans notre classeur nouvellement créé, nous devons obtenir une référence à la feuille de calcul dans laquelle nous allons saisir nos données. Si le classeur est notre toile, alors la feuille de calcul est notre palette.

```csharp
// Obtention de la référence de la feuille de calcul nouvellement ajoutée en passant son index de feuille
Worksheet worksheet = workbook.Worksheets[0];
```
 Ici, nous accédons à la première feuille de calcul (index`0`).

## Étape 4 : ajouter des exemples de valeurs aux cellules

Vient maintenant la partie amusante ! Nous allons saisir quelques exemples de valeurs dans notre feuille de calcul. Ces données serviront de base à notre graphique linéaire. 

```csharp
// Ajout de valeurs d'échantillon aux cellules
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
Dans cet extrait, nous ajoutons des valeurs aux cellules des colonnes A et B. La colonne A représente les valeurs de l'axe X, tandis que la colonne B représente les valeurs de l'axe Y.

## Étape 5 : ajouter un graphique linéaire à la feuille de calcul

Ensuite, nous allons introduire notre graphique linéaire dans la feuille de calcul. C'est là que vos données prendront vraiment vie !

```csharp
// Ajout d'un graphique à la feuille de calcul
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Line, 5, 0, 25, 10);
```
Ici, nous ajoutons un graphique en courbes à l'emplacement spécifié. Les paramètres (5, 0, 25, 10) définissent la position et la taille du graphique dans la feuille de calcul.

## Étape 6 : Accéder à la nouvelle instance de graphique

Une fois notre graphique ajouté, il est temps de mettre la main sur l'objet graphique nouvellement créé. 

```csharp
// Accéder à l'instance du graphique nouvellement ajouté
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```
Ce code nous connecte au graphique afin que nous puissions le manipuler davantage.

## Étape 7 : ajouter SeriesCollection au graphique

Nous devons maintenant indiquer à notre graphique les données à afficher. C'est ici que nous définissons la source de données de notre graphique en courbes en ajoutant une SeriesCollection.

```csharp
// Ajout de SeriesCollection (source de données du graphique) au graphique allant de la cellule « A1 » à « B3 »
chart.NSeries.Add("A1:B3", true);
```
Dans cet exemple, nous demandons au graphique d’utiliser les valeurs des cellules A1 à B3.

## Étape 8 : Enregistrez le fichier Excel

La grande finale ! Après tout votre travail acharné, il est temps d'enregistrer le fichier Excel et de voir votre graphique en courbes en action.

```csharp
// Sauvegarde du fichier Excel
workbook.Save(outputDir + "outputHowToCreateLineChart.xlsx");
```
 Cette ligne enregistre votre classeur dans le répertoire de sortie spécifié avec le nom`outputHowToCreateLineChart.xlsx`.

## Étape 9 : Exécuter et vérifier

Enfin, vous pouvez maintenant exécuter votre code et vérifier que le graphique linéaire a été créé avec succès dans votre répertoire de sortie ! 

```csharp
Console.WriteLine("HowToCreateLineChart executed successfully.");
```
Cela affichera un message sur votre console, vous indiquant que tout s'est bien passé.

## Conclusion

Créer un graphique en courbes à l'aide d'Aspose.Cells pour .NET est un moyen efficace de donner vie à vos données. En suivant ce guide étape par étape, vous pouvez facilement visualiser les tendances et les relations dans vos ensembles de données. Que vous soyez un développeur expérimenté ou que vous débutiez, Aspose.Cells vous offre la flexibilité et la puissance nécessaires pour automatiser vos tâches de visualisation de données. 

## FAQ

### Qu'est-ce qu'Aspose.Cells pour .NET ?  
Aspose.Cells pour .NET est une bibliothèque puissante conçue pour gérer et manipuler des fichiers Excel par programmation, permettant aux développeurs de créer, modifier et convertir des feuilles de calcul.

### Aspose.Cells prend-il en charge les graphiques ?  
Oui, Aspose.Cells fournit une prise en charge étendue de divers types de graphiques, notamment les graphiques linéaires, les graphiques à secteurs, les graphiques à barres, etc.

### Puis-je utiliser Aspose.Cells gratuitement ?  
Oui, vous pouvez télécharger une version d'essai gratuite pour découvrir ses fonctionnalités. Pour une utilisation à long terme, pensez à acheter une licence.

### Existe-t-il un forum de support ?  
 Absolument ! Vous pouvez trouver des réponses et poser des questions sur le[Forum Aspose.Cells](https://forum.aspose.com/c/cells/9).

### Comment acheter une licence ?  
 Les licences peuvent être achetées facilement via le[page d'achat](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
