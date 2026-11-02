---
category: general
date: 2026-10-07
description: Créer des feuilles de détail dupliquées dans Excel en utilisant C#. Apprenez
  à générer plusieurs feuilles de calcul et à créer un rapport à partir de tables
  en une seule exécution.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: fr
lastmod: 2026-10-07
og_description: Créez des feuilles de détail dupliquées dans Excel avec C#. Ce tutoriel
  montre comment générer plusieurs feuilles de calcul et produire un rapport Excel
  complet à partir de tableaux.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Créer des feuilles de détail dupliquées dans Excel – guide C# étape par
  étape
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  headline: Create duplicated detail sheets in Excel using C#
  type: TechArticle
- description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  name: Create duplicated detail sheets in Excel using C#
  steps:
  - name: '**Obtain the data source** that contains a master table and two detail
      tables.'
    text: '**Obtain the data source** that contains a master table and two detail
      tables.'
  - name: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
    text: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
  - name: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
    text: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
  - name: '**Run the processor** to generate the master sheet and all detail sheets.'
    text: '**Run the processor** to generate the master sheet and all detail sheets.'
  - name: '**Save the workbook** – each detail sheet now has a distinct name.'
    text: '**Save the workbook** – each detail sheet now has a distinct name.'
  type: HowTo
tags:
- C#
- Excel automation
- Aspose.Cells
title: Créer des feuilles de détail dupliquées dans Excel avec C#
url: /fr/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer des feuilles de détail dupliquées dans Excel avec C#

Si vous devez **créer des feuilles de détail dupliquées** dans un classeur Excel, ce guide vous accompagne pas à pas dans le processus complet. Vous verrez comment **générer plusieurs feuilles de calcul** à partir d’un ensemble de données maître‑détail et produire un rapport Excel soigné directement à partir de tables.

Générer un rapport Excel à partir de tables est une exigence courante pour les systèmes de facturation, les tableaux de bord d’inventaire ou tout scénario où un enregistrement maître possède plusieurs lignes de détail associées. À la fin de ce tutoriel, vous disposerez d’un programme C# exécutable qui crée un classeur avec une feuille maître et une feuille nommée de façon unique pour chaque groupe de détails.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 (ou version ultérieure) installé  
* Visual Studio 2022 ou tout IDE compatible C#  
* Le package NuGet **Aspose.Cells for .NET** (fournit `SmartMarkerProcessor`)  

Vous pouvez ajouter le package avec la commande suivante :

```bash
dotnet add package Aspose.Cells
```

## Vue d’ensemble de la solution

La solution suit ces cinq étapes :

1. **Obtenir la source de données** contenant une table maître et deux tables de détail.  
2. **Configurer le processeur Smart‑marker** afin que chaque feuille de détail dupliquée reçoive un nom unique.  
3. **Créer un nouveau classeur** et placer un smart‑marker qui fait référence à la table maître.  
4. **Exécuter le processeur** pour générer la feuille maître et toutes les feuilles de détail.  
5. **Enregistrer le classeur** – chaque feuille de détail possède désormais un nom distinct.

Chaque étape est détaillée ci‑dessous, avec le code complet et les explications.

## Étape 1 : Obtenir la source de données qui contient une table maître et deux tables de détail

La première tâche consiste à construire un `DataSet` qui imite les données que vous récupéreriez normalement depuis une base de données. Le `DataSet` doit contenir une table nommée **Master** et une ou plusieurs tables nommées **Detail**. Le moteur Smart‑marker utilise ces noms de tables pour remplir le classeur.

```csharp
using System.Data;

/// <summary>
/// Returns a DataSet with a master table and two detail tables.
/// In a real application you would fill these tables from a database.
/// </summary>
static DataSet GetReportDataSet()
{
    var ds = new DataSet();

    // Master table – one row per invoice
    var master = new DataTable("Master");
    master.Columns.Add("InvoiceId", typeof(int));
    master.Columns.Add("CustomerName", typeof(string));
    master.Columns.Add("InvoiceDate", typeof(DateTime));
    master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
    master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
    ds.Tables.Add(master);

    // Detail table – multiple rows per invoice
    var detail = new DataTable("Detail");
    detail.Columns.Add("InvoiceId", typeof(int));
    detail.Columns.Add("Product", typeof(string));
    detail.Columns.Add("Quantity", typeof(int));
    detail.Columns.Add("Price", typeof(decimal));

    // Detail rows for Invoice 101
    detail.Rows.Add(101, "Widget A", 5, 9.99m);
    detail.Rows.Add(101, "Widget B", 2, 19.95m);

    // Detail rows for Invoice 102
    detail.Rows.Add(102, "Gadget X", 1, 99.00m);
    detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
    ds.Tables.Add(detail);

    return ds;
}
```

**Pourquoi c’est important :**  
*Smart‑marker* travaille avec des objets `DataSet `; chaque nom de table devient un marqueur que le moteur peut remplacer. En structurant les données de cette façon, vous permettez au processeur de dupliquer automatiquement la feuille de détail pour chaque `InvoiceId` distinct.

## Étape 2 : Configurer le processeur Smart‑marker pour donner à chaque feuille de détail dupliquée un nom unique

Lorsque le processeur rencontre un marqueur de détail, il crée une nouvelle feuille de calcul pour chaque groupe de lignes. Par défaut, les nouvelles feuilles partagent le même nom, ce qui entraîne un conflit de nommage. Définir `DetailSheetNewName` indique au moteur comment renommer chaque copie.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

/// <summary>
/// Configures the SmartMarkerProcessor to rename duplicated detail sheets.
/// The placeholder {0} is replaced with a sequential number (1, 2, …).
/// </summary>
static SmartMarkerProcessor ConfigureProcessor()
{
    var processor = new SmartMarkerProcessor();

    // The pattern "Detail_{0}" becomes Detail_1, Detail_2, …
    processor.Options.DetailSheetNewName = "Detail_{0}";

    // Optional: keep the original sheet as a template (if you have one)
    processor.Options.KeepTemplateSheet = false;

    return processor;
}
```

**Pourquoi c’est important :**  
Sans un modèle de nommage unique, le classeur lèverait une exception lorsque le processeur essaie d’ajouter une seconde feuille de détails. Le placeholder `{0}` garantit que chaque feuille reçoit un nom distinct et prévisible.

## Étape 3 : Créer un nouveau classeur et placer un smart‑marker qui fait référence à la table maître

Vous créez maintenant un `Workbook` vierge, ajoutez un marqueur qui pointe vers la table **Master**, et, si vous le souhaitez, formatez la ligne d’en‑tête.

```csharp
/// <summary>
/// Creates a workbook with a single cell that contains the master smart‑marker.
/// </summary>
static Workbook CreateTemplateWorkbook()
{
    var workbook = new Workbook();
    var sheet = workbook.Worksheets[0];

    // Put the master smart‑marker in cell A1.
    // The double braces {{ }} tell SmartMarker to replace the content with the Master table.
    sheet.Cells["A1"].PutValue("{{Master}}");

    // Optional: add a header row for visual clarity.
    sheet.Cells["A2"].PutValue("Invoice ID");
    sheet.Cells["B2"].PutValue("Customer");
    sheet.Cells["C2"].PutValue("Date");
    sheet.Cells["A2:C2"].Style.Font.IsBold = true;

    return workbook;
}
```

**Pourquoi c’est important :**  
Le marqueur `{{Master}}` indique au processeur d’étendre la table maître à partir de `A1`. Les lignes suivantes deviennent les lignes de données pour chaque en‑registrement maître. C’est le point d’entrée pour **générer un rapport Excel à partir de tables**.

## Étape 4 : Exécuter le processeur Smart‑marker pour générer la feuille maître et les feuilles de détail

Avec la source de données, le processeur et le modèle prêts, vous invoquez `Process`. Le moteur développe le marqueur maître, puis crée une feuille de détail distincte pour chaque `InvoiceId` unique.

```csharp
static void GenerateReport()
{
    // 1️⃣ Obtain data
    DataSet reportData = GetReportDataSet();

    // 2️⃣ Configure processor
    SmartMarkerProcessor processor = ConfigureProcessor();

    // 3️⃣ Create template workbook
    Workbook workbook = CreateTemplateWorkbook();

    // 4️⃣ Process the smart‑markers – this creates the master sheet and duplicated detail sheets
    processor.Process(workbook, reportData);

    // 5️⃣ Save the file
    string outputPath = Path.Combine(
        Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
        "DuplicatedDetailSheets.xlsx");
    workbook.Save(outputPath);

    Console.WriteLine($"Report generated successfully: {outputPath}");
}
```

**Pourquoi c’est important :**  
`processor.Process` effectue le travail lourd : il lit les lignes maîtres, crée une feuille de détail pour chaque clé unique, et renomme ces feuilles selon le modèle défini précédemment. Le résultat est un classeur qui répond à la demande **how to generate multiple worksheets**.

## Étape 5 : Enregistrer le classeur résultant – chaque feuille de détail possède maintenant un nom distinct

L’appel `Save` écrit le fichier sur le disque. Lorsque vous ouvrez le classeur, vous verrez :

* **Sheet1** – la feuille maître contenant les en‑têtes de factures.  
* **Detail_1**, **Detail_2**, … – chaque feuille contient les lignes de la table **Detail** qui appartiennent à une facture particulière.

Voici une maquette de la disposition attendue du classeur (l’image est illustrative ; vous pouvez la remplacer par une vraie capture d’écran si vous le souhaitez).

![Capture d’écran d’un fichier Excel qui a créé des feuilles de détail dupliquées en sortie](https://example.com/images/duplicated-detail-sheets.png)

### Résultat attendu

| Nom de la feuille | Description du contenu |
|-------------------|------------------------|
| **Sheet1** | Lignes maîtres : InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Lignes de détail où `InvoiceId = 101` |
| **Detail_2** | Lignes de détail où `InvoiceId = 102` |

L’ouverture de `DuplicatedDetailSheets.xlsx` doit afficher exactement cette structure.

## Code source complet (prêt à copier)



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Name Sheets Automatically – Generate Multiple Sheets in C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [How to Create Worksheets – Step‑by‑Step Guide for Dynamic Excel Generation](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [How to Generate Excel Report in C# – Full Guide Using SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}