---
title: Trier les données dans une colonne avec une liste de tri personnalisée dans Excel
linktitle: Trier les données dans une colonne avec une liste de tri personnalisée dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment trier des données dans Excel à l'aide d'une liste de tri personnalisée avec Aspose.Cells pour .NET dans ce didacticiel complet.
weight: 10
url: /fr/net/excel-data-sorting-exporting/sort-data-in-a-column-with-custom-sort-list-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trier les données dans une colonne avec une liste de tri personnalisée dans Excel

## Introduction

Ce didacticiel vous guidera tout au long du processus de configuration de votre projet, de chargement d'un fichier Excel et de tri des données dans une plage spécifiée à l'aide d'un ordre de tri personnalisé. En suivant ce guide, vous acquerrez une expérience pratique qui peut améliorer vos compétences en gestion des données et la convivialité de la bibliothèque Aspose.Cells.

## Prérequis

Avant de plonger dans le didacticiel, décrivons quelques prérequis pour garantir une expérience d'apprentissage fluide.

### Connaissances de base de C#

Bien que le didacticiel soit conçu pour vous guider à travers chaque étape, une compréhension fondamentale de C# facilitera la compréhension des concepts présentés.

### Environnement de développement .NET

Assurez-vous de disposer d'un environnement de développement .NET fonctionnel. Vous pouvez utiliser Visual Studio ou tout autre IDE prenant en charge le développement .NET.

### Package NuGet Aspose.Cells pour .NET

Vous devez installer la bibliothèque Aspose.Cells pour .NET dans votre projet. Vous pouvez facilement l'ajouter via le gestionnaire de packages NuGet. 

Voici comment procéder :

1. Ouvrez votre projet dans Visual Studio.
2. Accédez à « Outils » > « Gestionnaire de packages NuGet » > « Gérer les packages NuGet pour la solution ».
3.  Rechercher`Aspose.Cells` et installez la dernière version.

### Fichier Excel de base pour les tests

Vous aurez besoin d'un fichier Excel d'exemple pour travailler. Vous pouvez créer un fichier Excel simple avec des noms de pays aléatoires et leurs codes.

## Paquets d'importation

Pour commencer, importons les packages nécessaires dans votre projet. Voici un extrait de la configuration de votre code :

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Avec les packages importés, nous sommes prêts à avancer.

## Étape 1 : définir les répertoires source et de sortie 

La première étape consiste à définir où se trouve votre fichier d'entrée et où vous souhaitez que le fichier de sortie (fichier trié) soit enregistré. Vous devez spécifier deux chemins : un pour le fichier Excel source et un autre pour enregistrer le fichier de sortie après le tri.

```csharp
string sourceDir = "Your Document Directory\\";
string outputDir = "Your Document Directory\\";
```

## Étape 2 : charger le fichier Excel source

Ensuite, nous allons charger le fichier Excel qui contient les données que vous souhaitez trier. Pour cela, il faut créer une instance de`Workbook` classe et en passant le chemin de votre fichier source.

```csharp
Workbook wb = new Workbook(sourceDir + "sampleSortData_CustomSortList.xlsx");
```

## Étape 3 : Accéder à la première feuille de travail 

Une fois le fichier chargé, nous devons accéder à la feuille de calcul spécifique qui contient les données que nous souhaitons trier. Dans ce cas, nous ciblons la première feuille de calcul.

```csharp
Worksheet ws = wb.Worksheets[0];
```

## Étape 4 : Spécifiez la zone de cellule à trier

 Nous devons déterminer la plage de cellules que nous allons trier. Dans cet exemple, nous allons trier les cellules de A1 à A40. Utilisez l'`CellArea.CreateCellArea` méthode pour définir la zone de la cellule.

```csharp
CellArea ca = CellArea.CreateCellArea("A1", "A40");
```

## Étape 5 : Créer une liste de tri personnalisée

Avant de procéder au tri, nous devons établir les critères que nous utiliserons pour notre tri personnalisé. Vous pouvez définir une liste de tri sous la forme d'un tableau de chaînes. La liste de tri personnalisée dictera l'ordre de tri.

```csharp
string[] customSortList = new string[] { "USA,US", "Brazil,BR", "China,CN", "Russia,RU", "Canada,CA" };
```

## Étape 6 : ajouter une clé de tri et effectuer le tri

Il est maintenant temps de trier ! Nous utiliserons pour cela la classe DataSorter. Créez une clé pour le tri en fonction de notre liste personnalisée et exécutez l'opération de tri.

```csharp
wb.DataSorter.AddKey(0, SortOrder.Ascending, customSortList);
wb.DataSorter.Sort(ws.Cells, ca);
```

## Étape 7 : Enregistrer le fichier Excel de sortie

Une fois le tri terminé, la dernière étape consiste à enregistrer les modifications dans un nouveau fichier Excel. Spécifiez le nom du fichier de sortie et enregistrez le classeur.

```csharp
wb.Save(outputDir + "outputSortData_CustomSortList.xlsx");
```

## Étape 8 : Confirmer l’exécution réussie

Pour vous assurer que tout s'est bien déroulé, vous pouvez imprimer un message de confirmation sur la console. Cela facilite le débogage et vous donne la satisfaction de savoir que l'opération a réussi.

```csharp
Console.WriteLine("SortDataInColumnWithCustomSortList executed successfully.\r\n");
```

## Conclusion

Et voilà ! Vous avez réussi à trier les données d'une colonne Excel à l'aide d'une liste de tri personnalisée avec Aspose.Cells pour .NET. Le tri permet d'apporter structure et clarté à vos données, ce qui facilite leur analyse et leur interprétation. J'espère que ce guide vous permettra d'améliorer vos compétences et vous aidera à réaliser à quel point Aspose.Cells peut être puissant pour vos tâches liées à Excel.

## FAQ

### Qu'est-ce qu'Aspose.Cells pour .NET ?
Aspose.Cells pour .NET est une bibliothèque complète qui vous permet de manipuler des fichiers Excel dans des applications .NET, notamment de les créer, de les modifier et de les convertir.

### Puis-je trier plusieurs colonnes à l’aide d’une liste de tri personnalisée ?
Oui ! Vous pouvez ajouter des clés supplémentaires pour trier par plusieurs colonnes si nécessaire, suivez simplement la même procédure pour chaque clé.

### Ai-je besoin de connaissances préalables en C# pour utiliser Aspose.Cells ?
Bien que cela soit utile, vous pouvez suivre ce tutoriel et apprendre au fur et à mesure ! Une compréhension de base de C# améliorera votre expérience d'apprentissage.

### Est-il possible d'utiliser une licence temporaire pour Aspose.Cells ?
Absolument ! Vous pouvez acquérir une licence temporaire si vous souhaitez tester toutes les fonctionnalités de la bibliothèque sans restrictions.

### Puis-je télécharger des exemples ou de la documentation pour Aspose.Cells ?
 Oui ! Aspose fournit une documentation complète et des exemples de projets qui peuvent vous être d'une grande aide. Découvrez le[Documentation sur Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
