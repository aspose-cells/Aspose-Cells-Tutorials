---
title: Définition des données de catégorie
linktitle: Définition des données de catégorie
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment définir des données de catégorie dans des graphiques Excel à l'aide d'Aspose.Cells pour .NET. Suivez notre tutoriel étape par étape pour une mise en œuvre facile.
weight: 15
url: /fr/net/advanced-chart-operations/setting-category-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définition des données de catégorie

## Introduction

Lorsqu'il s'agit de gérer et de manipuler des fichiers Excel par programmation, disposer des bons outils peut faire toute la différence. Aspose.Cells pour .NET se distingue comme l'un de ces outils, permettant aux développeurs de créer, de modifier et de convertir des fichiers Excel sans effort. Que vous créiez une application d'analyse de données complexe ou que vous ayez simplement besoin d'automatiser la génération de rapports, Aspose.Cells est là pour vous. 

## Prérequis 

Avant de plonger dans les détails, assurons-nous que vous avez tout ce dont vous avez besoin :

1. Environnement de développement : assurez-vous de disposer d'un environnement de développement .NET. Visual Studio est recommandé.
2.  Bibliothèque Aspose.Cells pour .NET : téléchargez la dernière version de la bibliothèque à partir du[Page de téléchargement d'Aspose.Cells](https://releases.aspose.com/cells/net/).
3. Compréhension de base de C# : la familiarité avec les concepts de C# et d’Excel vous aidera à mieux appréhender le contenu.
4.  Accès à la documentation : Avoir accès à[Documentation sur Aspose.Cells](https://reference.aspose.com/cells/net/) peut fournir des informations supplémentaires si vous êtes bloqué. 

Maintenant que tout est en place, découvrons la magie de la manipulation d'Excel étape par étape.

## Paquets d'importation 

Avant de commencer à coder, il est essentiel d'importer les packages nécessaires. Cela nous permet d'accéder aux fonctionnalités fournies par Aspose.Cells.

## Étape 1 : Importer l’espace de noms

Pour commencer, importons l’espace de noms Aspose.Cells dans votre fichier C#.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

En incluant cette ligne en haut de votre fichier, vous pouvez accéder à toutes les classes et méthodes pertinentes dans la bibliothèque Aspose.Cells.

Maintenant que nous connaissons les conditions préalables et que nous avons importé la bibliothèque nécessaire, explorons comment définir les données de catégorie dans un graphique Excel.

## Étape 2 : définissez votre répertoire de sortie

Tout d'abord, vous devez spécifier l'emplacement où le fichier Excel sera enregistré. Créez une variable pour votre répertoire de sortie. 

```csharp
string outputDir = "Your Output Directory";
```

 Remplacer`"Your Output Directory"` avec le chemin d'accès réel vers l'emplacement où vous souhaitez enregistrer votre fichier Excel de sortie. Cela vous permet de savoir exactement où trouver votre produit fini !

## Étape 3 : Instanciation d'un objet de classeur

Ensuite, vous allez créer une nouvelle instance de l'objet Workbook. Cet objet sert de conteneur pour votre fichier Excel.

```csharp
Workbook workbook = new Workbook();
```

## Étape 4 : Accéder à la première feuille de calcul

Vous devrez travailler avec la première feuille de calcul du classeur. Pour accéder à la feuille de calcul, c'est aussi simple que :

```csharp
Worksheet worksheet = workbook.Worksheets[0];
```

 L'indice`0` pointe vers la première feuille de calcul. Dans Excel, considérez cela comme l'ouverture du premier onglet de votre classeur.

## Étape 5 : Ajout d'échantillons de valeurs aux cellules

Complétons quelques données avec lesquelles travailler. Vous pouvez ajouter des valeurs numériques aux deux premières colonnes. 

```csharp
worksheet.Cells["A1"].PutValue(10);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(170);
worksheet.Cells["A4"].PutValue(200);
worksheet.Cells["B1"].PutValue(120);
worksheet.Cells["B2"].PutValue(320);
worksheet.Cells["B3"].PutValue(50);
worksheet.Cells["B4"].PutValue(40);
```

Dans cet extrait, nous remplissons les lignes A1 à A4 avec différentes valeurs numériques et les colonnes B1 à B4 également. Ces données serviront de base à notre graphique.

## Étape 6 : Ajout de données de catégorie

Maintenant, étiquetons nos catégories de données. Cela se fait dans la troisième colonne (colonne C) :

```csharp
worksheet.Cells["C1"].PutValue("Q1");
worksheet.Cells["C2"].PutValue("Q2");
worksheet.Cells["C3"].PutValue("Y1");
worksheet.Cells["C4"].PutValue("Y2");
```

Ici, nous désignons chaque ensemble de données par des catégories telles que « T1 » et « Y1 », ce qui facilite l'interprétation ultérieure de notre graphique.

## Création du graphique

Avec nos données en place, nous sommes prêts à ajouter un graphique pour représenter visuellement ces données.

## Étape 7 : Ajout d’un graphique à la feuille de calcul

Maintenant, ajoutons un graphique de type « Colonne » sur la feuille de calcul.

```csharp
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```

Cette ligne crée un nouveau graphique à colonnes commençant à la ligne 5 et à la colonne 0 de la feuille de calcul.

## Étape 8 : Accéder à l'instance de graphique

Avant de pouvoir remplir le graphique avec des données, nous devons accéder à l'instance du graphique nouvellement créé :

```csharp
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Avec cette étape, nous sommes désormais prêts à ajouter notre série de données au graphique.

## Étape 9 : Ajout de séries de données au graphique

Ensuite, vous ajouterez la collection de séries, qui définit les données que le graphique affichera. 

```csharp
chart.NSeries.Add("A1:B4", true);
```

Cette ligne spécifie que le graphique doit prendre des données des plages A1 à B4, ce qui lui permet d'afficher ces valeurs visuellement.

## Étape 10 : Définition des données de catégorie

Voici la partie cruciale : définir nos données de catégorie. C'est ce qui identifie nos points de données sur l'axe des x.

```csharp
chart.NSeries.CategoryData = "C1:C4";
```

En attribuant cette plage, nous indiquons au graphique les cellules qui correspondent aux catégories de notre série de données. Sans cette étape, votre graphique ne serait qu'un ensemble de chiffres !

## Étape 11 : enregistrement du fichier Excel

Maintenant que tout est en place, il est temps de sauvegarder notre dur labeur. 

```csharp
workbook.Save(outputDir + "outputSettingCategoryData.xlsx");
```

Cette commande enregistre votre classeur dans le répertoire de sortie spécifié sous le nom « outputSettingCategoryData.xlsx ». 

## Étape 12 : Message de confirmation

Enfin, nous pouvons ajouter un petit retour pour confirmer que tout a bien fonctionné :

```csharp
Console.WriteLine("SettingCategoryData executed successfully.");
```

Cela imprime un message dans la console, vous informant que le processus est terminé. Simple, non ?

## Conclusion

Et voilà ! Vous avez réussi à définir des données de catégorie pour un graphique dans un classeur Excel à l'aide d'Aspose.Cells pour .NET. La beauté de cette approche réside dans la façon dont elle vous permet d'automatiser la manipulation des fichiers Excel sans avoir Excel installé sur votre ordinateur. 

## FAQ

### Qu'est-ce qu'Aspose.Cells ?
Aspose.Cells est une bibliothèque .NET permettant de gérer des fichiers Excel sans avoir recours à Microsoft Excel. Elle permet de créer, d'éditer et de convertir des documents Excel par programmation.

### Puis-je utiliser Aspose.Cells gratuitement ?
 Oui, vous pouvez essayer Aspose.Cells gratuitement. Ils proposent une version d'essai gratuite disponible[ici](https://releases.aspose.com/).

### Aspose.Cells est-il adapté aux grands ensembles de données ?
Absolument ! Aspose.Cells est conçu pour gérer efficacement de grands ensembles de données, ce qui en fait un choix fiable pour les applications gourmandes en données.

### Comment ajouter des graphiques à l'aide d'Aspose.Cells ?
Vous pouvez ajouter des graphiques en créant un nouvel objet graphique et en le liant à des plages de cellules contenant vos données, comme illustré dans ce didacticiel.

### Où puis-je trouver plus d’exemples d’utilisation d’Aspose.Cells ?
 Vous pouvez explorer plus d'exemples et une documentation détaillée sur le[Page de documentation d'Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
