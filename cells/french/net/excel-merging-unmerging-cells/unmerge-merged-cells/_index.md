---
title: Annuler la fusion des cellules fusionnées dans Excel
linktitle: Annuler la fusion des cellules fusionnées dans Excel
second_title: API de traitement Excel Aspose.Cells .NET
description: Supprimez facilement la fusion des cellules dans Excel à l'aide d'Aspose.Cells pour .NET. Suivez notre guide étape par étape pour créer de meilleures feuilles de calcul.
weight: 10
url: /fr/net/excel-merging-unmerging-cells/unmerge-merged-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Annuler la fusion des cellules fusionnées dans Excel

## Introduction

Vous en avez assez de devoir gérer des cellules fusionnées dans vos feuilles de calcul Excel ? Vous n'êtes pas seul ! Les cellules fusionnées peuvent être une fonctionnalité pratique pour la mise en forme, mais elles peuvent souvent donner lieu à des maux de tête lorsqu'il s'agit de manipuler et d'analyser des données. Mais devinez quoi ? La fusion de ces cellules ennuyeuses est plus facile que vous ne le pensez, surtout lorsque vous utilisez Aspose.Cells pour .NET. Dans cet article, je vais vous expliquer comment fusionner des cellules étape par étape, en veillant à ce que vos données soient nettes, ordonnées et prêtes à l'emploi ! Alors, prenez votre chapeau de codeur et plongeons dans le monde d'Aspose.Cells.

## Prérequis

Avant de nous salir les mains, il y a quelques éléments essentiels que vous devez mettre en place :

### Connaissances de base de C# et .NET Framework
Si vous connaissez la programmation C# et avez une compréhension de base du framework .NET, vous êtes déjà sur la bonne voie. Sinon, ne vous inquiétez pas ! Ce didacticiel est conçu pour être simple, vous apprendrez donc les concepts nécessaires au fur et à mesure.

### Bibliothèque Aspose.Cells
Assurez-vous que la bibliothèque Aspose.Cells est installée dans votre environnement .NET. Vous pouvez facilement l'obtenir en visitant le[Page de téléchargement d'Aspose.Cells](https://releases.aspose.com/cells/net/).

### Configuration de l'IDE
Vous devez disposer d’un environnement de développement configuré, comme Visual Studio, dans lequel vous pouvez écrire et exécuter votre code C#.

### Exemple de fichier Excel
Prenez un exemple de fichier Excel contenant des cellules fusionnées : vous utiliserez ce fichier pour vous entraîner à fusionner.

Maintenant que tous ces prérequis sont réunis, nous pouvons passer à la partie passionnante : coder notre solution !

## Paquets d'importation

Tout d'abord, importons les packages nécessaires. Avec Aspose.Cells, vous allez interagir avec différentes classes pour gérer efficacement vos fichiers Excel. Voici ce que vous devez inclure en haut de votre fichier C# :

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

En incluant ce package, vous aurez accès à toutes les fonctionnalités offertes par Aspose.Cells.

Décomposons le processus de désintégration en étapes faciles à gérer. Chaque étape sera clairement définie afin que vous puissiez la suivre facilement.

## Étape 1 : Définir les répertoires

La première étape consiste à définir les répertoires dans lesquels se trouvent votre fichier Excel d'entrée (celui contenant les cellules fusionnées) et votre fichier de sortie (celui dans lequel les données non fusionnées seront enregistrées). Voici comment procéder :

```csharp
// Répertoire des sources
string sourceDir = "Your Document Directory"; 

// Répertoire de sortie
string outputDir = "Your Document Directory"; 
```

 Assurez-vous de remplacer`"Your Document Directory"` avec le chemin réel vers vos fichiers.

## Étape 2 : Créer un classeur

Maintenant que vous avez défini les répertoires, il est temps de créer un objet Workbook. Cet objet vous permettra de manipuler le fichier Excel. Vous pouvez le faire avec le code suivant :

```csharp
// Créer un classeur
Workbook wbk = new Aspose.Cells.Workbook(sourceDir + "sampleUnMergingtheMergedCells.xlsx");
```

Cette ligne de code lit votre exemple de fichier Excel et le prépare pour le traitement. 

## Étape 3 : Accéder à la feuille de travail

Chaque classeur est composé de feuilles. Vous devez accéder à la feuille de calcul spécifique dans laquelle vous souhaitez dissocier les cellules. Voici comment procéder :

```csharp
// Créez une feuille de calcul et obtenez la première feuille
Worksheet worksheet = wbk.Worksheets[0];
```

Ce code récupère la première feuille de calcul. Si vos cellules fusionnées se trouvent sur une autre feuille, mettez à jour l'index en conséquence.

## Étape 4 : Accéder aux cellules de la feuille de calcul

Ensuite, vous devrez obtenir une référence aux cellules de votre feuille de calcul. Cela peut être réalisé en utilisant :

```csharp
//Créez un objet Cells pour récupérer toutes les cellules
Cells cells = worksheet.Cells;
```

Avec cette ligne, vous avez désormais accès à toutes les cellules de la feuille de calcul, vous permettant de les manipuler selon vos besoins.

## Étape 5 : Annuler la fusion des cellules

Voici l'étape cruciale : la fusion des cellules ! Vous devez spécifier la plage de cellules fusionnées que vous souhaitez fusionner. Utilisez le code suivant :

```csharp
// Annuler la fusion des cellules
cells.UnMerge(5, 2, 2, 3);
```

 Dans cet exemple, le`UnMerge` La méthode prend quatre paramètres : l'index de la ligne de départ (5), l'index de la colonne de départ (2), le nombre de lignes à fusionner (2) et le nombre de colonnes à fusionner (3). Ajustez ces paramètres pour qu'ils correspondent aux cellules fusionnées spécifiques de votre fichier Excel.

## Étape 6 : Enregistrer le classeur

Après avoir annulé la fusion, vous souhaiterez enregistrer vos modifications dans un nouveau fichier Excel. Voici comment procéder :

```csharp
// Enregistrer le fichier
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

Cette ligne enregistre vos données non fusionnées dans le répertoire de sortie spécifié. C'est aussi simple que ça !

## Étape 7 : Confirmer le processus

Enfin, il est judicieux de vérifier que tout s'est bien passé. Vous pouvez imprimer un message sur la console pour vous informer que l'opération s'est déroulée avec succès :

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

Et voilà ! Vous avez réussi à dissocier des cellules d'un fichier Excel à l'aide d'Aspose.Cells pour .NET.

## Conclusion

La suppression de la fusion de cellules peut sembler fastidieuse, surtout si vous travaillez avec de grandes feuilles de calcul, mais avec Aspose.Cells pour .NET, c'est un jeu d'enfant ! Ce didacticiel vous a expliqué toutes les étapes, de la configuration de votre environnement à l'exécution du code nécessaire pour supprimer efficacement la fusion de cellules. La flexibilité offerte par la bibliothèque Aspose.Cells vous permet de traiter efficacement les feuilles de calcul, ce qui en fait un choix idéal pour les développeurs travaillant avec des fichiers Excel. Alors, lancez-vous et commencez à profiter de feuilles de calcul plus propres et plus faciles à gérer.

## FAQ

### Qu'est-ce qu'Aspose.Cells ?  
Aspose.Cells est une bibliothèque puissante pour créer, manipuler et convertir des documents Excel dans des applications .NET.

### Ai-je besoin d'une licence pour utiliser Aspose.Cells ?  
 Bien qu'Aspose.Cells propose un essai gratuit, une licence est requise pour une utilisation complète. Vous pouvez obtenir un[licence temporaire ici](https://purchase.aspose.com/temporary-license/).

### Puis-je dissocier des cellules de plusieurs feuilles à la fois ?  
Oui, vous pouvez parcourir plusieurs feuilles de calcul dans un classeur et fusionner des cellules selon vos besoins.

### Aspose.Cells est-il compatible avec .NET Core ?  
Oui, Aspose.Cells est compatible avec .NET Core, ce qui le rend polyvalent pour diverses applications .NET.

### Où puis-je trouver plus de documentation sur Aspose.Cells ?  
 Vous pouvez explorer la documentation complète sur le[Page de référence Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
