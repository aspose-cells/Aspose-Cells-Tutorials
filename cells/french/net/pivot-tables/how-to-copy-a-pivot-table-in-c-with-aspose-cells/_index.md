---
category: general
date: 2026-09-27
description: Apprenez à copier un tableau croisé dynamique en C# avec Aspose.Cells.
  Comprend la copie de lignes avec mise en forme, la copie du tableau croisé dynamique
  vers une autre feuille et l'exportation du tableau croisé dynamique vers un nouveau
  classeur.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: fr
lastmod: 2026-09-27
og_description: Comment copier un tableau croisé dynamique en C# avec Aspose.Cells.
  Suivez le guide étape par étape pour copier des lignes avec mise en forme, déplacer
  un tableau croisé dynamique vers une autre feuille et l’exporter vers un nouveau
  classeur.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: Comment copier un tableau croisé dynamique en C# – guide complet d'Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Comment copier un tableau croisé dynamique en C# avec Aspose.Cells
url: /fr/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier un tableau croisé dynamique en C# avec Aspose.Cells

Si vous devez **copier un tableau croisé dynamique** d’une feuille de calcul à une autre, apprendre **comment copier un tableau croisé dynamique** en C# avec Aspose.Cells peut vous faire gagner des heures de travail manuel. Cette approche vous permet également de **copier des lignes avec mise en forme**, de conserver le cache du tableau croisé dynamique intact, et même de **exporter le tableau croisé dynamique vers un nouveau classeur** lorsque vous avez besoin d’un fichier autonome.

Ce tutoriel vous guide à travers le flux de travail complet :

* créer un classeur,
* copier la plage du tableau croisé dynamique tout en préservant la mise en forme,
* placer les données copiées sur une nouvelle feuille, et
* enregistrer le résultat dans un fichier séparé.

Vous verrez pourquoi la méthode intégrée `CopyRows` est la façon la plus fiable de **copier un tableau croisé dynamique vers une autre feuille**, et vous recevrez des conseils pour gérer les cas particuliers tels que les lignes masquées ou les sources de données externes.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later | Aspose.Cells prend en charge .NET 6+ et offre les meilleures performances. |
| Visual Studio 2022 (or any C# IDE) | Vous avez besoin d’un éditeur capable de restaurer les packages NuGet. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Cette bibliothèque fournit l’API `CopyRows` utilisée dans l’exemple. |
| A source Excel file (`source.xlsx`) that contains a pivot table in the range `A1:G20` | Le code copie cette plage spécifique ; ajustez la plage si votre tableau croisé dynamique est plus grand. |

Install the library with the NuGet CLI or Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## Étape 1 : Charger le classeur qui contient le tableau croisé dynamique

La première ligne crée un objet `Workbook` qui représente le fichier Excel complet. Charger le fichier une fois vous donne un accès en lecture/écriture à chaque feuille de calcul.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Pourquoi cette étape est importante** – Sans charger le classeur, aucun des appels `CopyRows` suivants ne peut référencer les données source ou le cache du tableau croisé dynamique.

## Étape 2 : Préparer les feuilles source et destination

Vous avez besoin d’une feuille de destination où le tableau croisé dynamique copié sera placé. Le code ci‑dessous récupère la première feuille de calcul (où se trouve le tableau croisé dynamique original) et ajoute une nouvelle feuille nommée **Copy**.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Astuce :** Si la feuille de destination existe déjà, appelez d’abord `Worksheets.RemoveAt(index)` pour éviter les noms en double.

## Étape 3 : Définir la zone de cellules qui englobe le tableau croisé dynamique

Un objet `CellArea` décrit les cellules en haut‑à‑gauche et en bas‑à‑droite de la plage que vous souhaitez déplacer. Dans cet exemple, le tableau croisé dynamique occupe `A1:G20`. Ajustez les coordonnées pour des tables plus grandes.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Étape 4 : Copier les lignes avec mise en forme et préserver le cache du tableau croisé dynamique

La méthode `CopyRows` copie les **lignes** de la feuille source vers la feuille de destination. En passant `CopyOptions.CopyAll`, vous vous assurez que les valeurs, la mise en forme, les graphiques et les objets incorporés — tous faisant partie d’un tableau croisé dynamique — sont transférés.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Pourquoi `CopyRows` fonctionne mieux que `Copy` pour les tableaux croisés dynamiques

* `CopyRows` respecte le cache interne du tableau croisé dynamique, de sorte que le tableau copié reste fonctionnel.
* Il préserve **copy rows with formatting** exactement comme elles apparaissent dans la feuille originale.
* Contrairement à une simple `Copy` d’une plage, il déplace également les lignes masquées et les segments associés.

## Étape 5 : Enregistrer le classeur avec le tableau croisé dynamique copié

Enfin, écrivez le classeur modifié sur le disque. Le nouveau fichier contient la feuille originale ainsi qu’une feuille **Copy** qui contient un duplicata pleinement fonctionnel du tableau croisé dynamique original.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Résultat attendu

Lorsque vous ouvrez `pivot_copied.xlsx` :

* Feuille **Sheet1** contient toujours les données et le tableau croisé dynamique originaux.
* Feuille **Copy** affiche un tableau croisé dynamique identique avec la même disposition, les mêmes filtres et la même mise en forme.
* Toutes les formules et connexions de données restent intactes car le cache du tableau croisé dynamique a été copié avec les lignes.

## Comment copier un tableau croisé dynamique vers une autre feuille dans le même classeur

Si vous avez seulement besoin du tableau croisé dynamique dans une autre feuille existante (par ex., “Report”), remplacez l’étape de création de la destination par une référence à la feuille cible :

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Cet extrait montre **copy pivot table to another sheet** sans créer une nouvelle feuille de calcul.

## Exporter le tableau croisé dynamique vers un nouveau classeur

Parfois, vous souhaitez le tableau croisé dynamique dans un fichier complètement séparé. Après l’opération de copie, vous pouvez supprimer toutes les feuilles sauf celle qui contient le tableau croisé dynamique copié, puis enregistrer :

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Maintenant, `pivot_only.xlsx` contient une seule feuille avec le tableau croisé dynamique dupliqué, répondant à l’exigence **export pivot table to new workbook**.

## Comment copier des lignes Excel sans perdre la mise en forme

Le même appel `CopyRows` fonctionne pour n’importe quelle plage, pas seulement les tableaux croisés dynamiques. Si vous devez **copy excel rows** qui incluent une mise en forme conditionnelle, une validation de données ou des cellules fusionnées, utilisez la même méthode :

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Parce que `CopyOptions.CopyAll` transfère tout, les lignes de destination ressemblent exactement aux lignes source.

## Pièges courants et comment les éviter

| Piège | Symptôme | Solution |
|-------|----------|----------|
| La plage source n’inclut pas l’ensemble du tableau croisé dynamique | Le tableau croisé dynamique copié apparaît tronqué. | Vérifiez que le `CellArea` couvre toutes les lignes/colonnes du tableau croisé dynamique. |
| La feuille de destination contient déjà des données | Les lignes écrasées entraînent une perte de données. | Choisissez une nouvelle feuille ou commencez la copie à un indice de ligne plus élevé. |
| Le tableau croisé dynamique utilise une source de données externe | La copie perd sa connexion. | Après la copie, appelez `pivotTable.RefreshData()` pour rétablir le lien. |
| Les lignes masquées sont omises | Certaines lignes disparaissent dans la copie. | `CopyRows` copie automatiquement les lignes masquées ; assurez‑vous de ne pas utiliser `CopyOptions.CopyValuesOnly`. |

## Exemple complet et exécutable

Ci‑dessous se trouve un programme autonome que vous pouvez coller dans un nouveau projet console. Il démontre chaque étape abordée ci‑dessus.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**Exécuter le programme** crée `pivot_copied.xlsx` avec un duplicata du tableau croisé dynamique original sur une nouvelle feuille nommée **Copy**.

## Conclusion

Vous savez maintenant **comment copier un tableau croisé dynamique** en C# en utilisant

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un nouveau classeur – Comment copier une feuille de calcul avec un tableau croisé dynamique](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copier un tableau croisé dynamique en C# – Guide complet étape par étape](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Comment copier une plage avec des tableaux croisés dynamiques en C# – Guide complet](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}