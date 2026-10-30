---
category: general
date: 2026-09-18
description: Créer un PowerPoint à partir d’Excel avec Aspose.Cells – copier les tableaux
  croisés dynamiques, exporter des plages et enregistrer en PPTX en quelques lignes
  de code C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: fr
lastmod: 2026-09-18
og_description: Créez rapidement des présentations PowerPoint à partir d’Excel. Apprenez
  à copier les tableaux croisés dynamiques, à exporter des plages et à enregistrer
  un classeur au format PPTX avec Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Créer un PowerPoint à partir d’Excel avec Aspose.Cells – guide étape par
  étape
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Comment créer un PowerPoint à partir d'Excel en utilisant Aspose.Cells
url: /fr/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un PowerPoint à partir d'Excel avec Aspose.Cells

Si vous devez créer un PowerPoint à partir d'Excel, ce guide vous montre une solution concise, de bout en bout. Vous verrez comment copier un tableau croisé dynamique, exporter une plage sélectionnée et enregistrer le résultat sous forme de fichier PPTX en quelques lignes de C#.

Générer un diaporama directement à partir des données d’une feuille de calcul élimine l’étape manuelle de copier‑coller qui ralentit les flux de travail de reporting. Le tutoriel couvre tout ce dont vous avez besoin, de la configuration du projet au fichier PPTX final, et il fonctionne avec la dernière version d’Aspose.Cells pour .NET.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* **Aspose.Cells for .NET** (version 23.12 ou plus récente). Installez‑le via NuGet : `Install-Package Aspose.Cells`.
* Un environnement de développement **.NET 6+** (Visual Studio 2022 ou VS Code convient).
* Un classeur Excel (`Source.xlsx`) contenant les données et le tableau croisé dynamique que vous souhaitez réutiliser.
* Des droits d’écriture sur le dossier de sortie.

Aucune bibliothèque tierce supplémentaire n’est requise.

## Créer un PowerPoint à partir d'Excel – étape par étape

Le processus se compose de quatre étapes logiques qui correspondent directement à l’exemple de code que vous verrez plus loin.

### Étape 1 : Charger le classeur source et définir la plage

Vous devez charger le classeur qui contient les données source et le tableau croisé dynamique. Sélectionner une plage précise garantit que seules les cellules nécessaires sont transférées, ce qui maintient la diapositive résultante légère.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Pourquoi c’est important :**  
`CreateRange` crée un objet `Range` qui peut être copié en une fois. En limitant la plage à `A1:G20`, vous évitez d’inclure des cellules non pertinentes, ce qui pourrait sinon alourdir le fichier PowerPoint.

### Étape 2 : Préparer le classeur de destination

Aspose.Cells traite une diapositive PowerPoint comme un classeur lorsqu’on l’enregistre au format PPTX. Créer un nouveau classeur vous donne une toile vierge pour la plage copiée.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Astuce :** Si vous avez besoin de plusieurs diapositives, vous pouvez ajouter des feuilles de calcul supplémentaires et les enregistrer chacune comme un fichier PPTX distinct.

### Étape 3 : Copier la plage tout en conservant le tableau croisé dynamique

La méthode `CopyRange` accepte un objet `PasteOptions`. En définissant `CopyPivotTables = true`, vous indiquez à Aspose.Cells de conserver la structure du tableau croisé dynamique, pas seulement les valeurs rendues.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**Comment cela fonctionne :**  
Lorsque `CopyPivotTables` est vrai, la feuille de destination reçoit à la fois les données source et le cache du tableau croisé dynamique. Cela signifie que le tableau reste pleinement fonctionnel et peut être actualisé plus tard si les données source changent.

### Étape 4 : Enregistrer le classeur sous forme de fichier PowerPoint

Enfin, exportez le classeur au format PPTX. Le drapeau `SaveFormat.Pptx` indique à Aspose.Cells d’écrire la feuille de calcul comme une diapositive PowerPoint.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Résultat :**  
`CopyWithPivot.pptx` s’ouvre dans Microsoft PowerPoint (ou tout visualiseur compatible) avec une seule diapositive affichant la plage copiée, incluant un tableau croisé dynamique actif qui peut être manipulé dans PowerPoint.

## Exemple complet exécutable

Voici le programme complet que vous pouvez coller dans un nouveau projet console et exécuter immédiatement.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Sortie attendue :**  
L’exécution du programme affiche « PowerPoint file created successfully. » et crée un fichier nommé `CopyWithPivot.pptx`. L’ouverture du fichier dans PowerPoint montre une seule diapositive où la plage Excel copiée apparaît exactement comme dans la feuille source, avec un tableau croisé dynamique actif pouvant être actualisé depuis PowerPoint.

## Variantes courantes et cas limites

| Situation | Ce qu’il faut modifier |
|-----------|------------------------|
| **Plusieurs tableaux croisés dynamiques** | Définissez des objets `Range` distincts pour chaque tableau et appelez `CopyRange` pour chacun, ou copiez la feuille entière s’ils partagent la même source de données. |
| **Jeux de données volumineux** | Augmentez la plage (par ex., `"A1:Z5000"`). Envisagez d’activer `PasteOptions.CompressData = true` pour réduire la taille du PPTX. |
| **Mises en page de diapositive différentes** | Après l’enregistrement en PPTX, ouvrez le fichier dans PowerPoint et appliquez une mise en page ou un thème personnalisé ; les données restent modifiables. |
| **Enregistrement dans un flux** | Utilisez `destinationWorkbook.Save(stream, SaveFormat.Pptx)` lorsque vous devez renvoyer le PPTX via une API web. |
| **Conservation du formatage des cellules** | Définissez `PasteOptions.PasteType = PasteType.All` pour garder les polices, les couleurs et les bordures. |

**Conseil pro :** Vérifiez toujours que le dossier de destination existe avant d’appeler `Save`. Si le dossier est absent, `Save` lève une `DirectoryNotFoundException`.

## Conclusion

Vous savez maintenant comment créer un PowerPoint à partir d'Excel, copier un tableau croisé dynamique et exporter le résultat sous forme de fichier PPTX avec Aspose.Cells. Les étapes — chargement du classeur source, définition d’une plage, copie avec `CopyPivotTables` et enregistrement en PPTX — couvrent l’ensemble du flux de travail de manière fiable et prête pour la production.

Ensuite, explorez **comment exporter Excel vers PPTX** pour plusieurs feuilles de calcul, ou apprenez **comment copier une plage entre classeurs** lorsque vous devez fusionner des données provenant de plusieurs sources avant de générer le diaporama. Les deux sujets s’appuient sur la même surface d’API et peuvent être combinés pour automatiser des pipelines de reporting complexes.

Bon codage, et profitez de la transformation de vos feuilles de calcul en présentations soignées !


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}