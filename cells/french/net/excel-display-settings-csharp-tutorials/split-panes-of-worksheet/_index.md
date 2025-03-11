---
title: Diviser les volets d'une feuille de calcul
linktitle: Diviser les volets d'une feuille de calcul
second_title: Référence de l'API Aspose.Cells pour .NET
description: Découvrez comment diviser les volets d'une feuille de calcul dans Aspose.Cells pour .NET grâce à notre guide étape par étape. Améliorez la navigation dans les fichiers Excel grâce à ce didacticiel simple.
weight: 130
url: /fr/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Diviser les volets d'une feuille de calcul

## Introduction

Êtes-vous prêt à diviser les volets d'une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET ? Imaginez : vous avez une feuille Excel gigantesque et vous en avez assez de faire défiler constamment les en-têtes juste pour vous rappeler sur quelle colonne vous travaillez. Entrez « Fractionner les volets ». Cette fonctionnalité pratique vous permet de figer une partie de votre feuille de calcul, ce qui facilite grandement la navigation. Que vous travailliez avec des données financières, la gestion des stocks ou des ensembles de données volumineux, la division des volets peut décupler votre productivité. 

## Prérequis

Avant de commencer à fractionner les volets comme un assistant de feuille de calcul, commençons par configurer correctement notre système. Voici ce dont vous aurez besoin :

-  Aspose.Cells pour .NET : assurez-vous de l'avoir téléchargé et installé. Si ce n'est pas encore fait, téléchargez-le[ici](https://releases.aspose.com/cells/net/).
- .NET Framework : ce guide suppose que vous travaillez dans un environnement .NET.
- Un classeur Excel : nous utiliserons un exemple de fichier Excel pour montrer comment cette fonctionnalité fonctionne.
-  Une licence temporaire ou complète : Aspose.Cells nécessite une licence. Si vous ne faites qu'essayer, procurez-vous-en une[permis temporaire gratuit](https://purchase.aspose.com/temporary-license/) pour éviter les limitations d’évaluation.

## Paquets d'importation

Avant de nous plonger dans le code, importons d'abord les espaces de noms nécessaires. Vous ne pouvez pas vraiment faire quoi que ce soit dans Aspose.Cells sans les inclure.

```csharp
using System.IO;
using Aspose.Cells;
```

Maintenant que nous avons couvert l'essentiel, passons à la partie passionnante : le fractionnement des vitres !

## Étape 1 : créer une instance d'un classeur

 La première étape de ce processus consiste à créer un`Workbook` objet, qui représentera le fichier Excel que vous souhaitez modifier. Dans ce cas, nous allons charger un fichier à partir d'un répertoire. Il s'agit de votre toile, la feuille Excel sur laquelle vous allez travailler votre magie.

Avant de pouvoir diviser des volets, nous avons besoin d'un classeur avec lequel travailler ! Cette étape est aussi essentielle que l'ouverture d'un livre avant de commencer à le lire.

```csharp
// Le chemin vers le répertoire des documents
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Instancier un nouveau classeur et ouvrir un fichier modèle
Workbook book = new Workbook(dataDir + "Book1.xls");
```

 Dans le code ci-dessus, remplacez`"YOUR DOCUMENT DIRECTORY"` avec le chemin réel où se trouve votre fichier Excel.`Workbook`la classe charge le fichier Excel en mémoire.

## Étape 2 : définir la cellule active

 Après avoir chargé le classeur, il est temps de définir la cellule active. En termes Excel, la cellule active est celle qui est actuellement sélectionnée ou mise au point. Dans ce didacticiel, nous allons sélectionner la cellule`A20` dans la première feuille de travail.

Le choix de la cellule active est crucial, car le fractionnement du panneau démarre à partir de cette cellule active. C'est comme choisir où faire la première coupe dans une pizza : choisissez votre part !

```csharp
// Définir la cellule active
book.Worksheets[0].ActiveCell = "A20";
```

 Ce morceau de code fait`A20` la cellule active. C'est important car le fractionnement se produit autour de ce point, tout comme la navigation dans Excel se concentre souvent autour d'une cellule spécifique.

## Étape 3 : diviser la feuille de calcul

Maintenant que la cellule active est définie, passons à la partie amusante : diviser la feuille de calcul ! C'est à cette étape que la magie opère. Vous pourrez diviser la feuille de calcul en plusieurs volets pour faciliter la visualisation et la navigation.

Il s'agit du cœur de l'ensemble du didacticiel. En divisant la feuille de calcul, vous créez des volets distincts qui vous permettent de faire défiler différentes sections de votre feuille Excel sans perdre de vue les en-têtes ou d'autres zones importantes.

```csharp
// Diviser la fenêtre de la feuille de calcul
book.Worksheets[0].Split();
```

 Avec le`Split()` méthode, vous dites à Aspose.Cells de diviser la feuille de calcul au niveau de la cellule active (`A20` dans ce cas). À partir de ce point, Excel crée une division dans la feuille qui sépare les volets pour que vous puissiez naviguer de manière indépendante.

## Étape 4 : Enregistrer le classeur

Après avoir divisé les volets, il ne vous reste plus qu'à enregistrer votre travail. Cette dernière étape garantit que vos modifications sont enregistrées dans le fichier de sortie spécifié.

À quoi sert tout votre dur labeur si vous ne le conservez pas ? En sauvegardant, vous vous assurez que vos vitres magnifiquement séparées restent intactes pour une utilisation ultérieure.

```csharp
// Enregistrer le fichier Excel
book.Save(dataDir + "output.xls");
```

 Ici, le`Save()` La méthode enregistre le classeur avec vos volets nouvellement divisés dans un fichier Excel de sortie. Les modifications que vous avez apportées sont désormais prêtes à être utilisées par vous ou par quelqu'un d'autre.

## Conclusion

Et voilà ! Vous venez d'apprendre à fractionner les volets d'une feuille de calcul Excel à l'aide d'Aspose.Cells pour .NET. Plus besoin de faire défiler sans fin ni de perdre la trace de vos données. Cette méthode rend la gestion des fichiers Excel volumineux beaucoup moins fastidieuse et beaucoup plus efficace. Grâce à la possibilité de fractionner les volets, vous pouvez désormais suivre les points de données critiques tout en travaillant avec des feuilles de calcul complexes.

## FAQ

### Puis-je diviser plus de deux volets ?  
 Oui, vous pouvez diviser la feuille de calcul en plusieurs volets en spécifiant différentes cellules actives et en appelant la`Split()` méthode.

### Quelle est la différence entre diviser des vitres et geler des vitres ?  
Le fractionnement des volets vous permet de faire défiler les deux volets indépendamment. Le gel des volets verrouille les en-têtes ou des lignes/colonnes spécifiques afin qu'ils restent visibles lors du défilement.

### Puis-je retirer le split après l'avoir appliqué ?  
Oui, vous pouvez supprimer la division en fermant et en rouvrant le classeur ou en le réinitialisant par programmation.

### Le fractionnement des volets fonctionne-t-il de la même manière pour différents formats de fichiers Excel (XLS, XLSX) ?  
 Oui, le`Split()` la méthode fonctionne pour les formats XLS et XLSX.

### Puis-je utiliser Aspose.Cells sans licence ?  
 Oui, mais cela comporte des limites. Pour une expérience complète, il est préférable d'utiliser un[temporaire](https://purchase.aspose.com/temporary-license/) ou[licence payante](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
