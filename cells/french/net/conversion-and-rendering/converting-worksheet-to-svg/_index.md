---
title: Conversion d'une feuille de calcul en SVG dans .NET
linktitle: Conversion d'une feuille de calcul en SVG dans .NET
second_title: API de traitement Excel Aspose.Cells .NET
description: Découvrez comment convertir une feuille de calcul Excel en SVG à l'aide d'Aspose.Cells pour .NET grâce à ce guide étape par étape. Idéal pour les développeurs .NET souhaitant convertir Excel en SVG.
weight: 11
url: /fr/net/conversion-and-rendering/converting-worksheet-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Conversion d'une feuille de calcul en SVG dans .NET

## Introduction

Si vous cherchez à convertir une feuille de calcul Excel au format SVG, vous êtes au bon endroit ! Aspose.Cells pour .NET est un outil puissant qui permet aux développeurs de manipuler des fichiers Excel et de les convertir en divers formats, notamment le format SVG (Scalable Vector Graphics) largement pris en charge. Ce didacticiel vous guidera tout au long du processus de conversion d'une feuille de calcul au format SVG dans .NET, en le décomposant étape par étape, afin que même les débutants puissent le suivre facilement.

## Prérequis

Avant de plonger dans le code, assurons-nous que vous avez tout ce dont vous avez besoin :

1.  Aspose.Cells pour .NET : téléchargez et installez la dernière version d'Aspose.Cells pour .NET à partir de[Aspose.Cells pour .NET](https://releases.aspose.com/cells/net/).
2. Environnement de développement .NET : vous aurez besoin de Visual Studio ou de tout autre IDE .NET installé.
3. Connaissances de base de C# : une familiarité avec C# est requise, mais ne vous inquiétez pas, nous vous expliquerons tout clairement.
4. Fichier Excel : préparez un fichier Excel que vous souhaitez convertir au format SVG.

## Importer les packages nécessaires

Avant de passer à la partie codage, assurez-vous d'inclure les espaces de noms requis en haut de votre fichier C#.

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

Ces packages sont nécessaires pour travailler avec Aspose.Cells et gérer les options de rendu telles que l'exportation SVG.

Maintenant que les bases sont couvertes, passons aux étapes réelles de conversion d'une feuille de calcul Excel en image SVG.

## Étape 1 : définissez le chemin d’accès à votre répertoire de documents

La première chose dont nous avons besoin est de définir le chemin d'accès au dossier où se trouve votre fichier Excel. Ceci est crucial car votre code référencera le répertoire pour charger et enregistrer les fichiers.

```csharp
// Le chemin vers le répertoire des documents
string dataDir = "Your Document Directory";
```

 Assurez-vous de remplacer`"Your Document Directory"`avec le chemin réel où se trouve votre fichier Excel.

##  Étape 2 : chargez le fichier Excel à l'aide de`Workbook`

 Ensuite, nous devons charger le fichier Excel dans une instance du`Workbook` classe. Le`Workbook` la classe représente l'intégralité du fichier Excel, y compris toutes les feuilles de calcul qu'il contient.

```csharp
string filePath = dataDir + "Template.xlsx";
Workbook book = new Workbook(filePath);
```

 Ici,`"Template.xlsx"` est le nom du fichier Excel avec lequel vous travaillez. Assurez-vous que ce fichier existe dans le répertoire spécifié, sinon vous rencontrerez des erreurs.

## Étape 3 : définir les options d'image ou d'impression pour la conversion SVG

 Avant de pouvoir convertir la feuille de calcul au format SVG, nous devons spécifier les options d'image.`ImageOrPrintOptions` La classe vous permet de contrôler la manière dont la feuille de calcul sera convertie. Plus précisément, nous devons définir la classe`SaveFormat` à`SVG` et assurez-vous que chaque feuille de calcul est convertie en une seule page.

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.SaveFormat = SaveFormat.Svg;
imgOptions.OnePagePerSheet = true;
```

 Le`SaveFormat.Svg` l'option garantit que le format de sortie sera SVG, tandis que`OnePagePerSheet` garantit que chaque feuille de calcul sera rendue sur une seule page.

## Étape 4 : Parcourez chaque feuille de calcul du classeur

Nous devons maintenant parcourir toutes les feuilles de calcul du fichier Excel. Chaque feuille de calcul sera convertie individuellement.

```csharp
foreach (Worksheet sheet in book.Worksheets)
{
    // Nous traiterons chaque feuille de travail une par une
}
```

Cette boucle garantit que quel que soit le nombre de feuilles de calcul présentes dans votre classeur, chacune d'entre elles sera traitée.

##  Étape 5 : Créer un`SheetRender` Object for Rendering

 Pour chaque feuille de travail, nous allons créer un`SheetRender` objet. Cet objet est responsable de la conversion de la feuille de calcul au format d'image souhaité, qui dans ce cas, est SVG.

```csharp
SheetRender sr = new SheetRender(sheet, imgOptions);
```

 Le`SheetRender` L'objet prend deux arguments : la feuille de calcul que vous convertissez et les options d'image que vous avez définies précédemment.

## Étape 6 : Convertir la feuille de calcul en SVG

 Enfin, dans la boucle, nous allons convertir chaque feuille de calcul au format SVG. Nous utilisons une boucle imbriquée pour parcourir les pages (bien que dans ce cas, il n'y ait qu'une seule page par feuille de calcul, grâce à la`OnePagePerSheet` option).

```csharp
for (int i = 0; i < sr.PageCount; i++)
{
    // Exporter la feuille de calcul au format d'image SVG
    sr.ToImage(i, filePath + sheet.Name + i + ".out.svg");
}
```

Ce code enregistrera la feuille de calcul sous forme de fichier SVG dans le même répertoire que le fichier Excel. Chaque fichier SVG sera nommé en fonction du nom de la feuille de calcul et d'un numéro d'index pour éviter les conflits de noms.

## Conclusion

Et voilà ! Vous avez converti avec succès une feuille de calcul Excel au format SVG à l'aide d'Aspose.Cells pour .NET. Ce processus vous permet de conserver la mise en page et la conception de votre feuille de calcul tout en la rendant visible dans n'importe quel navigateur ou appareil prenant en charge SVG, ce qui est le cas de la plupart d'entre eux. Que vous travailliez avec des fichiers Excel complexes ou simplement un tableau simple, cette méthode garantit que vos données sont magnifiquement rendues dans un format adapté au Web.

## FAQ

### Qu’est-ce que SVG et pourquoi devrais-je l’utiliser ?
SVG (Scalable Vector Graphics) est un format Web qui peut évoluer à l'infini sans perte de qualité. Il est parfait pour les graphiques, diagrammes et images qui doivent être affichés à différentes tailles.

### Aspose.Cells peut-il gérer des fichiers Excel volumineux pour la conversion ?
Oui, Aspose.Cells peut gérer efficacement des fichiers Excel volumineux et les convertir en SVG sans problèmes de performances significatifs.

### Existe-t-il une limite au nombre de feuilles de calcul que je peux convertir en SVG ?
Non, il n'y a aucune limite inhérente à Aspose.Cells pour la conversion de plusieurs feuilles de calcul. La seule contrainte serait la mémoire et les performances de votre système.

### Ai-je besoin d'une licence pour utiliser Aspose.Cells ?
 Oui, Aspose.Cells nécessite une licence pour une utilisation en production. Vous pouvez obtenir une licence temporaire[ici](https://purchase.aspose.com/temporary-license/) ou explorez le[essai gratuit](https://releases.aspose.com/).

### Puis-je personnaliser la sortie SVG ?
 Oui, vous pouvez modifier le`ImageOrPrintOptions` pour personnaliser divers aspects de la sortie SVG, tels que la résolution et la mise à l'échelle.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
