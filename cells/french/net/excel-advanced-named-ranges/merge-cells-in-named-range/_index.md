---
"description": "Apprenez à fusionner des cellules d'une plage nommée avec Aspose.Cells pour .NET dans ce tutoriel pas à pas. Découvrez comment formater, styliser et automatiser des rapports Excel."
"linktitle": "Fusionner les cellules d'une plage nommée dans Excel"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Fusionner les cellules d'une plage nommée dans Excel"
"url": "/fr/net/excel-advanced-named-ranges/merge-cells-in-named-range/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Fusionner les cellules d'une plage nommée dans Excel

## Introduction

Lorsque vous travaillez avec des fichiers Excel par programmation, la fusion de cellules au sein d'une plage nommée est une tâche courante. Que vous automatisiez la génération de rapports, créiez des tableaux de bord ou gériez simplement de grands ensembles de données, la fusion de cellules est une technique essentielle. Dans ce tutoriel, nous allons découvrir comment fusionner des cellules au sein d'une plage nommée à l'aide d'Aspose.Cells pour .NET, une puissante bibliothèque permettant aux développeurs de manipuler des fichiers Excel sans avoir à installer Microsoft Excel.

## Prérequis

Avant de commencer, assurez-vous d’avoir les éléments suivants à disposition :

- Aspose.Cells pour .NET : vous pouvez le télécharger à partir du [Page de publication d'Aspose.Cells](https://releases.aspose.com/cells/net/).
- .NET Framework installé sur votre machine.
- Compréhension de base de C# : une familiarité avec des concepts tels que les classes, les méthodes et les objets sera utile.

## Importer des packages

Avant de passer au codage, vous devez importer les espaces de noms nécessaires. Ces espaces vous donneront accès aux fonctionnalités de la bibliothèque Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

Une fois les prérequis et les packages réglés, passons à la partie amusante : le codage !

Voici une description de la manière dont vous pouvez fusionner des cellules dans une plage nommée dans une feuille Excel à l'aide d'Aspose.Cells pour .NET.

## Étape 1 : Créer un nouveau classeur

La première chose dont nous avons besoin est un classeur. Dans Excel, un classeur est l'équivalent d'un fichier Excel. Créons-en un.

```csharp
// Instancier un nouveau classeur.
Workbook wb1 = new Workbook();
```

En initialisant un nouveau classeur, nous disposons désormais d'un fichier Excel vide, prêt à être manipulé. C'est comme partir d'une page blanche !

## Étape 2 : Accéder à la première feuille de travail

Chaque classeur contient des feuilles de travail, et dans ce cas, nous souhaitons travailler avec la première. Allons-y !

```csharp
// Obtenez la première feuille de travail du classeur.
Worksheet worksheet1 = wb1.Worksheets[0];
```

Considérez la feuille de calcul comme les onglets individuels d'un fichier Excel où se trouvent les données. Par défaut, nous accédons au tout premier onglet.

## Étape 3 : Créer une plage de cellules

Maintenant que nous avons notre feuille de calcul, il est temps de créer une plage. Une plage désigne un bloc de cellules pouvant s'étendre sur plusieurs lignes et colonnes.

```csharp
// Créer une gamme.
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

Ici, nous sélectionnons les cellules de D6 à I12, un bloc couvrant plusieurs lignes et colonnes. Nous allons bientôt fusionner cette plage !

## Étape 4 : nommer la plage

Nommer une plage facilite la référence ultérieure, en particulier lorsqu'il s'agit de grands ensembles de données.

```csharp
// Nommez la gamme.
mrange.Name = "TestRange";
```

En nommant cette plage « TestRange », nous pouvons la récupérer rapidement plus tard dans le code, sans avoir besoin de spécifier à nouveau les coordonnées de la cellule.

## Étape 5 : fusionner la plage de cellules

Passons maintenant à la magie : fusionner les cellules de la plage que nous venons de créer !

```csharp
// Fusionner les cellules de la plage.
mrange.Merge();
```

Cette étape fusionne toutes les cellules de D6 à I12 en une seule. Idéal pour les titres ou les résumés !

## Étape 6 : Récupérer la plage nommée

Une fois les cellules fusionnées, nous souhaiterons peut-être appliquer une mise en forme. Commençons par récupérer notre plage nommée.

```csharp
// Obtenez la gamme.
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

La récupération de la plage par nom nous permet d'effectuer d'autres opérations, comme l'ajout de styles ou la saisie de données.

## Étape 7 : Définir un style pour les cellules fusionnées

À quoi sert une cellule fusionnée si elle n'est pas soignée ? Créons un objet de style pour aligner le texte et appliquer une couleur d'arrière-plan.

```csharp
// Définir un objet de style.
Style style = wb1.CreateStyle();

// Définir l'alignement.
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

Ici, nous alignons le texte horizontalement et verticalement au centre, et définissons un arrière-plan bleu clair (aqua). Élégant, non ?

## Étape 8 : Appliquer le style à la plage

Après avoir défini le style, il est temps de l'appliquer à la plage fusionnée.

```csharp
// Créez un objet StyleFlag.
StyleFlag flag = new StyleFlag();

// Activez l'attribut de style relatif.
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

// Appliquer le style à la plage.
range1.ApplyStyle(style, flag);
```

Le `StyleFlag` indique à Aspose.Cells quelles propriétés de style appliquer : alignement, ombrage, etc. Cela vous donne un contrôle précis sur la façon dont le style est appliqué.

## Étape 9 : Saisir les données dans la plage fusionnée

Qu'est-ce qu'une plage formatée sans contenu ? Ajoutons du texte.

```csharp
// Saisissez les données dans la plage.
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

Le texte « Bienvenue dans les API Aspose » est alors placé dans la première cellule de notre plage fusionnée. Une fois la cellule fusionnée, ce texte s'étendra sur toutes les cellules de D6 à I12.

## Étape 10 : Enregistrez le fichier Excel

Enfin, enregistrons le classeur sous forme de fichier Excel.

```csharp
// Enregistrez le fichier Excel.
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

Ici, le classeur est enregistré avec le nom « outputMergeCellsInNamedRange.xlsx » dans votre répertoire spécifié.

## Conclusion

Et voilà ! Vous avez réussi à fusionner des cellules d'une plage nommée, à appliquer une mise en forme soignée et même à saisir des données, tout cela avec Aspose.Cells pour .NET. Que vous travailliez à l'automatisation de rapports, à la manipulation de fichiers Excel ou que vous appreniez simplement de nouvelles techniques, ce guide étape par étape devrait vous donner les bases nécessaires.

## FAQ

### Puis-je fusionner plusieurs plages non contiguës dans Aspose.Cells ?  
Non, vous ne pouvez fusionner que des cellules contiguës dans Aspose.Cells.

### Puis-je annuler une opération de fusion par programmation ?  
Une fois les cellules fusionnées, vous pouvez les dissocier à l'aide de la `UnMerge()` méthode dans Aspose.Cells.

### La fusion des cellules supprime-t-elle les données qu'elles contiennent ?  
S'il y a des données dans les cellules avant la fusion, les données de la première cellule de la plage seront conservées.

### Puis-je appliquer différents styles à des cellules individuelles dans une plage fusionnée ?  
Non, une plage fusionnée agit comme une seule cellule, vous ne pouvez donc pas appliquer des styles différents à des cellules individuelles à l'intérieur.

### Comment accéder à une cellule fusionnée après la fusion ?  
Après la fusion, vous pouvez toujours accéder à la cellule fusionnée en utilisant les coordonnées de son coin supérieur gauche.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}