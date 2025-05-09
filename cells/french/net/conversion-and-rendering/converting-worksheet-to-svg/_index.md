---
"description": "Apprenez à convertir une feuille de calcul Excel en SVG avec Aspose.Cells pour .NET grâce à ce guide étape par étape. Idéal pour les développeurs .NET souhaitant convertir Excel en SVG."
"linktitle": "Conversion d'une feuille de calcul en SVG dans .NET"
"second_title": "API de traitement Excel Aspose.Cells .NET"
"title": "Conversion d'une feuille de calcul en SVG dans .NET"
"url": "/fr/net/conversion-and-rendering/converting-worksheet-to-svg/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Conversion d'une feuille de calcul en SVG dans .NET

## Introduction

Si vous souhaitez convertir une feuille de calcul Excel au format SVG, vous êtes au bon endroit ! Aspose.Cells pour .NET est un outil puissant qui permet aux développeurs de manipuler des fichiers Excel et de les convertir dans différents formats, dont le format SVG (Scalable Vector Graphics), largement pris en charge. Ce tutoriel vous guidera pas à pas dans la conversion d'une feuille de calcul au format SVG avec .NET, pour que même les débutants puissent la suivre facilement.

## Prérequis

Avant de plonger dans le code, assurons-nous que vous avez tout ce dont vous avez besoin :

1. Aspose.Cells pour .NET : téléchargez et installez la dernière version d'Aspose.Cells pour .NET à partir de [Aspose.Cells pour .NET](https://releases.aspose.com/cells/net/).
2. Environnement de développement .NET : vous aurez besoin de Visual Studio ou de tout autre IDE .NET installé.
3. Connaissances de base de C# : une connaissance de C# est requise, mais ne vous inquiétez pas, nous vous expliquerons tout clairement.
4. Fichier Excel : préparez un fichier Excel que vous souhaitez convertir au format SVG.

## Importation des packages nécessaires

Avant de passer à la partie codage, assurez-vous d’inclure les espaces de noms requis en haut de votre fichier C#.

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

Ces packages sont nécessaires pour travailler avec Aspose.Cells et gérer les options de rendu telles que l'exportation SVG.

Maintenant que les bases sont couvertes, passons aux étapes réelles de conversion d'une feuille de calcul Excel en image SVG.

## Étape 1 : définissez le chemin d’accès à votre répertoire de documents

La première étape consiste à définir le chemin d'accès au dossier contenant votre fichier Excel. Ceci est crucial, car votre code référencera ce répertoire pour charger et enregistrer les fichiers.

```csharp
// Le chemin vers le répertoire des documents
string dataDir = "Your Document Directory";
```

Assurez-vous de remplacer `"Your Document Directory"` avec le chemin réel où réside votre fichier Excel.

## Étape 2 : Charger le fichier Excel à l’aide de `Workbook`

Ensuite, nous devons charger le fichier Excel dans une instance du `Workbook` classe. Le `Workbook` la classe représente l'intégralité du fichier Excel, y compris toutes les feuilles de calcul qu'il contient.

```csharp
string filePath = dataDir + "Template.xlsx";
Workbook book = new Workbook(filePath);
```

Ici, `"Template.xlsx"` est le nom du fichier Excel utilisé. Assurez-vous que ce fichier existe dans le répertoire spécifié, sinon vous risquez de rencontrer des erreurs.

## Étape 3 : définir les options d’image ou d’impression pour la conversion SVG

Avant de pouvoir convertir la feuille de calcul au format SVG, nous devons spécifier les options d'image. `ImageOrPrintOptions` Cette classe permet de contrôler la conversion de la feuille de calcul. Plus précisément, nous devons définir la classe `SaveFormat` à `SVG` et assurez-vous que chaque feuille de calcul est convertie en une seule page.

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.SaveFormat = SaveFormat.Svg;
imgOptions.OnePagePerSheet = true;
```

Le `SaveFormat.Svg` l'option garantit que le format de sortie sera SVG, tandis que `OnePagePerSheet` garantit que chaque feuille de calcul sera rendue sur une seule page.

## Étape 4 : Parcourez chaque feuille de calcul du classeur

Nous devons maintenant parcourir toutes les feuilles de calcul du fichier Excel. Chaque feuille sera convertie individuellement.

```csharp
foreach (Worksheet sheet in book.Worksheets)
{
    // Nous traiterons chaque feuille de travail une par une
}
```

Cette boucle garantit que quel que soit le nombre de feuilles de calcul présentes dans votre classeur, chacune d'entre elles sera traitée.

## Étape 5 : Créer un `SheetRender` Objet pour le rendu

Pour chaque feuille de travail, nous allons créer un `SheetRender` objet. Cet objet est responsable de la conversion de la feuille de calcul au format d'image souhaité, qui dans ce cas est SVG.

```csharp
SheetRender sr = new SheetRender(sheet, imgOptions);
```

Le `SheetRender` L'objet prend deux arguments : la feuille de calcul que vous convertissez et les options d'image que vous avez définies précédemment.

## Étape 6 : Convertir la feuille de calcul en SVG

Enfin, dans la boucle, nous convertirons chaque feuille de calcul au format SVG. Nous utiliserons une boucle imbriquée pour parcourir les pages (bien que, dans ce cas, il n'y ait qu'une seule page par feuille de calcul, grâce à la `OnePagePerSheet` option).

```csharp
for (int i = 0; i < sr.PageCount; i++)
{
    // Exporter la feuille de calcul au format d'image Svg
    sr.ToImage(i, filePath + sheet.Name + i + ".out.svg");
}
```

Ce code enregistre la feuille de calcul au format SVG dans le même répertoire que le fichier Excel. Chaque fichier SVG sera nommé selon le nom de la feuille de calcul et un numéro d'index afin d'éviter les conflits de noms.

## Conclusion

Et voilà ! Vous avez converti avec succès une feuille de calcul Excel au format SVG grâce à Aspose.Cells pour .NET. Ce processus vous permet de conserver la mise en page et le design de votre feuille de calcul tout en la rendant lisible sur tous les navigateurs et appareils prenant en charge le format SVG, soit la quasi-totalité. Que vous travailliez avec des fichiers Excel complexes ou un simple tableau, cette méthode garantit un rendu impeccable de vos données dans un format web optimisé.

## FAQ

### Qu'est-ce que SVG et pourquoi devrais-je l'utiliser ?
SVG (Scalable Vector Graphics) est un format web adaptable à l'infini sans perte de qualité. Il est idéal pour les graphiques, diagrammes et images devant être affichés à différentes tailles.

### Aspose.Cells peut-il gérer des fichiers Excel volumineux pour la conversion ?
Oui, Aspose.Cells peut gérer efficacement des fichiers Excel volumineux et les convertir en SVG sans problèmes de performances significatifs.

### Existe-t-il une limite au nombre de feuilles de calcul que je peux convertir en SVG ?
Non, Aspose.Cells n'impose aucune limite inhérente à la conversion de plusieurs feuilles de calcul. La seule contrainte concerne la mémoire et les performances de votre système.

### Ai-je besoin d'une licence pour utiliser Aspose.Cells ?
Oui, Aspose.Cells nécessite une licence pour une utilisation en production. Vous pouvez obtenir une licence temporaire. [ici](https://purchase.aspose.com/temporary-license/) ou explorez le [essai gratuit](https://releases.aspose.com/).

### Puis-je personnaliser la sortie SVG ?
Oui, vous pouvez modifier le `ImageOrPrintOptions` pour personnaliser divers aspects de la sortie SVG, tels que la résolution et la mise à l'échelle.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}