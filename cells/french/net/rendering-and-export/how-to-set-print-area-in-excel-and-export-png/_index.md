---
category: general
date: 2026-09-27
description: Définir la zone d’impression dans Excel et apprendre à exporter des images
  PNG des cellules sélectionnées. Ce guide couvre également l’enregistrement d’une
  plage en tant qu’image et l’ajout d’une image à la feuille de calcul.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: fr
lastmod: 2026-09-27
og_description: Définissez la zone d’impression dans Excel et exportez le PNG avec
  Aspose.Cells. Suivez ce guide étape par étape pour enregistrer la plage en tant
  qu’image et ajouter une image à la feuille de calcul.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Définir la zone d'impression dans Excel – exporter en PNG avec C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Comment définir la zone d'impression dans Excel et exporter en PNG
url: /fr/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir la zone d'impression dans Excel et exporter en PNG

Si vous devez **set print area excel** avant de créer une image, ce guide vous montre exactement comment le faire. Vous apprendrez également **how to export png** des fichiers à partir d'une plage spécifique, **save range as image**, et **add picture to worksheet** dans un flux de travail unique et répétable.

Travailler avec Excel de manière programmatique signifie souvent que vous ne souhaitez qu'un sous‑ensemble de cellules — par exemple un tableau croisé dynamique ou un graphique — devenir une image. En définissant d'abord une zone d'impression, vous vous assurez que le PNG exporté contient exactement les cellules attendues, ni plus ni moins. Ce tutoriel vous guide à travers chaque étape, du chargement du classeur à l'enregistrement du fichier PNG final, et explique pourquoi chaque paramètre est important.

## Prérequis

* .NET 6.0 ou version ultérieure installé  
* Visual Studio 2022 (ou tout IDE C#)  
* Le package NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`)  
* Un fichier Excel (`input.xlsx`) situé dans un répertoire connu  

Ces exigences garantissent que le code s'exécute sans configuration supplémentaire.

## Étape 1 : Charger le classeur avec lequel vous souhaitez travailler

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

La classe `Workbook` représente le fichier Excel complet. Le charger d'abord vous donne accès aux feuilles de calcul, aux cellules et aux options de mise en page.

## Étape 2 : **Set print area excel** pour la plage cible

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

Définir la **print area** indique à Excel (et à Aspose.Cells) quelles cellules appartiennent à la page imprimable. Lorsque vous exporterez ensuite la feuille sous forme d'image, seule cette zone sera rendue, ce qui est essentiel pour un **export selected cells image** propre.

## Étape 3 : Configurer les options d'exportation d'image – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` contrôle le format de sortie. En choisissant `ImageFormat.Png`, vous assurez une image haute résolution, avec un arrière‑plan transparent, qui fonctionne bien dans les contextes web et bureau.

## Étape 4 : Créer une image à partir de la plage définie et **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

La méthode `Pictures.Add` insère une nouvelle image dans la feuille de calcul. En transmettant la plage créée à l’Étape 2, vous **save range as image** directement sur la feuille, ce qui est utile si vous devez ensuite référencer l'image dans d'autres parties du classeur.

## Étape 5 : **Save the picture as an image file** – finaliser le flux de travail **export selected cells image**

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

L'appel à `Save` écrit l'image sur le système de fichiers en utilisant les options définies à l’Étape 3. Le fichier `selected_range.png` résultant contient exactement les cellules définies par la commande **set print area excel**.

## Exemple complet et exécutable

Assembler toutes les pièces vous fournit un programme compact que vous pouvez intégrer dans n'importe quelle application console :

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Résultat attendu

Running the program prints:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

Et vous trouverez un fichier `selected_range.png` qui ne montre que les cellules A1 à G20 du fichier `input.xlsx`.

## Pièges courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| L'image exportée contient toute la feuille | Aucune zone d'impression n'a été définie | Assurez‑vous de **set print area excel** avant de créer l'image |
| Le PNG est flou | Le DPI par défaut est faible | Définissez `imageOptions.DpiX` et `imageOptions.DpiY` à une valeur plus élevée (par ex., 300) |
| Erreur fichier non trouvé | Chemin du répertoire incorrect | Utilisez `Path.Combine` ou vérifiez que le dossier existe |
| L'image apparaît décalée | Indices de ligne/colonne incorrects | Les deux premiers paramètres de `Pictures.Add` sont la cellule en haut‑à‑gauche où l'image est placée ; conservez‑les à `0,0` pour une exportation propre |

## Astuce pro : Exporter plusieurs plages en une seule exécution

Si vous devez **export selected cells image** pour plusieurs zones, répétez les Étapes 2‑5 dans une boucle, en modifiant `printArea` à chaque itération. N'oubliez pas d'attribuer à chaque image un nom de fichier unique, sinon l'enregistrement ultérieur écrasera le fichier précédent.

## Conclusion

Vous savez maintenant comment **set print area excel**, configurer **how to export png**, **save range as image**, et **add picture to worksheet** avec Aspose.Cells. Cette solution de bout en bout vous permet de transformer n'importe quel bloc de cellules en PNG de haute qualité avec seulement quelques lignes de code C#.

Ensuite, vous pourriez explorer :

* Ajouter des bordures ou des filigranes au PNG exporté (recherchez *add picture to worksheet* avec style)  
* Exporter directement en PDF pour des rapports imprimables (*export selected cells image* → flux de travail PDF)  
* Automatiser le processus pour plusieurs classeurs dans un travail par lots  

N'hésitez pas à expérimenter avec différentes plages, réglages DPI ou formats d'image pour répondre aux besoins de votre projet. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Définir la zone d'impression dans Excel et exporter vers PowerPoint – Guide étape par étape](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Exporter la zone d'impression Excel vers HTML avec Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [Comment définir une zone d'impression dans Excel en utilisant Aspose.Cells pour .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}