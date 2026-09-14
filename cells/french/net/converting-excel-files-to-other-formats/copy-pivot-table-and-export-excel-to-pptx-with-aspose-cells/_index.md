---
category: general
date: 2026-09-11
description: Copier le tableau croisé dynamique et exporter Excel vers PPTX en utilisant
  Aspose.Cells. Apprenez à générer un PPTX éditable et à enregistrer le classeur au
  format PPTX en C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: fr
lastmod: 2026-09-11
og_description: Copiez le tableau croisé dynamique et exportez Excel vers PPTX en
  C# avec Aspose.Cells. Générez un PPTX éditable et enregistrez le classeur au format
  PPTX en quelques lignes de code.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Copier un tableau croisé dynamique et exporter Excel vers PPTX – guide complet
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Copier le tableau croisé dynamique et exporter Excel vers PPTX avec Aspose.Cells
url: /fr/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copier un tableau croisé dynamique et exporter Excel vers PPTX avec Aspose.Cells

Si vous devez copier un tableau croisé dynamique d’une feuille de calcul à une autre, puis exporter le fichier Excel vers une présentation PowerPoint, ce guide vous montre comment faire. En utilisant Aspose.Cells, vous pouvez générer un PPTX modifiable et enregistrer le classeur au format PPTX en quelques lignes de code C#.

Le tutoriel couvre chaque étape nécessaire pour déplacer un tableau croisé dynamique, préserver son fonctionnement et produire un fichier PPTX où le graphique et les formes restent éditables. Aucun outil externe n’est requis — seulement la bibliothèque Aspose.Cells et un environnement de développement .NET.

## Ce que vous allez réaliser

* **Copier le tableau croisé dynamique** d’une feuille source vers une feuille de destination tout en conservant les connexions de données.  
* **Exporter Excel vers PPTX** afin que la diapositive résultante puisse être modifiée dans PowerPoint.  
* **Générer un PPTX éditable** où les graphiques, tableaux et formes ne sont pas aplatis en images.  
* **Enregistrer le classeur au format PPTX** en utilisant le même appel d’API Aspose.Cells.  

### Prérequis

* .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.6+).  
* Aspose.Cells for .NET (package NuGet `Aspose.Cells`).  
* Une compréhension de base des applications console C#.  

> **Astuce pro :** Installez le package NuGet via la CLI pour garantir que vous disposez de la dernière version :  
> ```bash
> dotnet add package Aspose.Cells
> ```

## Comment copier un tableau croisé dynamique entre feuilles

La première opération consiste à déplacer le tableau croisé dynamique tout en préservant sa définition. Aspose.Cells fournit une méthode `CopyRange` avec un objet `CopyOptions` qui inclut le drapeau `CopyPivotTable`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Pourquoi cela fonctionne :**  
`CopyRange` copie les données des cellules, le formatage et, lorsque `CopyPivotTable` est vrai, le cache et les métadonnées du tableau croisé dynamique. La plage de destination commence à la cellule `A1` (ligne 0, colonne 0), mais vous pouvez modifier les décalages pour placer le tableau croisé dynamique ailleurs.

**Cas particulier fréquent :** Si la feuille de destination contient déjà un tableau croisé dynamique portant le même nom, Aspose.Cells renomme automatiquement celui qui arrive, évitant ainsi un conflit de noms.

## Exporter Excel vers PPTX et générer un PPTX éditable

Une fois le tableau croisé dynamique en place, vous pouvez exporter l’ensemble du classeur vers un fichier PPTX. La classe `ImageOrPrintOptions` vous permet de spécifier `ExportImageFormat = ImageFormat.Pptx`, ce qui indique à Aspose.Cells de traiter la sortie comme une présentation PowerPoint plutôt que comme une image raster.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Pourquoi cela fonctionne :**  
Lorsque `ExportImageFormat` est défini sur `Pptx`, Aspose.Cells traduit chaque feuille de calcul en une diapositive. Les formes, graphiques et tableaux croisés dynamiques sont écrits en tant qu’objets PowerPoint natifs, de sorte que vous pouvez double‑cliquer dessus dans PowerPoint et modifier les données sous‑jacentes.

**Conseil pour les classeurs volumineux :** Si vous n’avez besoin que d’un sous‑ensemble de feuilles, utilisez `workbook.Worksheets.RemoveAt(index)` pour supprimer les feuilles que vous ne souhaitez pas exporter avant d’appeler `Save`. Cela réduit la taille du fichier PPTX.

## Exemple complet, exécutable

Voici le programme complet qui regroupe les étapes précédentes. Remplacez `YOUR_DIRECTORY` par le chemin réel sur votre machine.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Résultat attendu

L’exécution du programme affiche :

```
Pivot table copied and workbook exported to PPTX successfully.
```

Lorsque vous ouvrez `output.pptx` dans Microsoft PowerPoint, vous verrez une diapositive contenant le tableau croisé dynamique copié sous forme de graphique éditable. Un double‑clic sur le graphique ouvre l’éditeur de graphiques PowerPoint, vous permettant de modifier les séries, les axes et les libellés de données sans revenir à Excel.

## Gestion des pièges courants

| Problème | Cause | Solution |
|----------|-------|----------|
| Le tableau croisé dynamique apparaît comme une image statique | Le drapeau `CopyPivotTable` omis ou `ExportImageFormat` défini sur `Png` | Assurez‑vous que `CopyPivotTable = true` et `ExportImageFormat = ImageFormat.Pptx`. |
| La feuille de destination montre des cellules vides | La plage source ne couvre pas toute la zone du tableau croisé dynamique | Étendez la plage (par ex., `"A1:H30"`) pour inclure tous les champs du tableau. |
| Le PPTX exporté est très volumineux | Des feuilles de calcul inutiles sont incluses | Supprimez les feuilles indésirables avant d’appeler `Save`. |
| PowerPoint ne peut pas modifier le graphique | Utilisation d’une version plus ancienne d’Aspose.Cells qui ne prend pas en charge le PPTX | Mettez à jour vers la dernière version d’Aspose.Cells (voir les notes de version). |

## Prochaines étapes et sujets associés

* **Exporter une feuille Excel vers PPTX avec des mises en page de diapositive personnalisées** – explorez `WorksheetToPdfConverter` pour un contrôle plus fin de l’apparence des diapositives.  
* **Exporter Excel vers PDF** – remplacez `ImageFormat.Pptx` par `ImageFormat.Pdf` pour générer un PDF à la place.  
* **Modifier programmatiquement le PPTX après l’export** – utilisez la bibliothèque `Aspose.Slides` pour ajouter des animations ou des notes du présentateur.  

En maîtrisant **copy pivot table**, **export excel to pptx** et **generate editable pptx**, vous pouvez créer des pipelines de reporting de bout en bout qui déplacent les données des feuilles de calcul directement vers des présentations sans perdre l’éditabilité.

---


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}