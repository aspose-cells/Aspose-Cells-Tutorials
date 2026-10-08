---
category: general
date: 2026-03-27
description: Créer un classeur Excel en C# avec Aspose.Cells, appliquer une mise en
  forme conditionnelle, importer un DataTable dans Excel et enregistrer le classeur
  au format xlsx — le tout dans un seul tutoriel.
draft: false
keywords:
- create excel workbook c#
- apply conditional formatting
- import datatable to excel
- save workbook as xlsx
- create excel file programmatically
language: fr
og_description: Créer un classeur Excel en C# avec Aspose.Cells, appliquer une mise
  en forme conditionnelle, importer un DataTable dans Excel et enregistrer le classeur
  au format xlsx en quelques minutes.
og_title: Créer un classeur Excel en C# – Guide complet avec mise en forme conditionnelle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Créer un classeur Excel en C# – Guide étape par étape avec mise en forme conditionnelle
url: /fr/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel C# – Tutoriel complet de programmation

Vous avez déjà eu besoin de **créer un classeur Excel C#** à la volée sans savoir par où commencer ? Vous n'êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu'ils automatisent leurs rapports pour la première fois. Dans ce guide, nous vous montrons exactement comment créer un classeur Excel C# avec Aspose.Cells, appliquer une mise en forme conditionnelle, importer un DataTable dans Excel et enfin enregistrer le classeur au format xlsx.  

Ce que vous obtiendrez à la fin de ce tutoriel, c’est une application console prête à l’emploi qui produit un fichier Excel coloré, ainsi qu’une explication claire de chaque ligne afin que vous puissiez l’adapter à vos propres projets. Aucun document externe requis ; copiez‑collez et exécutez.  

### Prérequis

- .NET 6+ (ou .NET Framework 4.7.2+) installé  
- Visual Studio 2022 ou tout éditeur C# de votre choix  
- Aspose.Cells for .NET (vous pouvez récupérer le package NuGet en version d’essai gratuite)  

Si vous avez tout cela, plongeons‑y.

## Créer un classeur Excel C# – Initialiser le classeur

La première chose à faire est de **créer un classeur Excel C#** en instanciant la classe `Workbook`. Cet objet représente l’ensemble du fichier Excel en mémoire.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                // <-- creates the workbook
        Worksheet worksheet = workbook.Worksheets[0];      // first sheet (Sheet1)
```

> **Pourquoi c’est important :** La classe `Workbook` abstrait le format de fichier, vous n’avez donc pas à manipuler du XML bas‑niveau ou de l’interop COM. Elle vous donne également accès aux styles, aux tables et aux smart markers dès le départ.

## Appliquer une mise en forme conditionnelle

Maintenant que le classeur existe, **appliquons une mise en forme conditionnelle** pour mettre en évidence les lignes où la quantité dépasse 100. La mise en forme conditionnelle vit sur la feuille de calcul, pas sur la cellule, ce qui la rend réutilisable.

```csharp
        // Step 4: Apply conditional formatting to highlight quantities > 100
        int cfIndex = worksheet.ConditionalFormattings.Add();               // add a new CF collection
        var conditionalFormatting = worksheet.ConditionalFormattings[cfIndex];
        var condition = conditionalFormatting.AddCondition(
            FormatConditionType.CellValue, OperatorType.Greater, "100");   // > 100

        // Define the style that will be applied when the condition is true
        condition.Style = workbook.CreateStyle();
        condition.Style.Font.Color = Color.Red;               // red font
        condition.Style.Pattern = BackgroundType.Solid;       // solid background
        condition.Style.ForegroundColor = Color.Yellow;      // yellow fill
```

> **Astuce :** Si vous avez besoin de règles plus complexes (par ex., entre deux valeurs), appelez simplement `AddCondition` à nouveau avec `OperatorType.Between`.

## Écrire les en‑têtes et les smart markers

Avant de **importer un DataTable dans Excel**, nous avons besoin de cellules de remplacement — les smart markers — que la bibliothèque remplacera par les données réelles. Pensez‑y comme à des balises de modèle.

```csharp
        // Step 2: Write the header row
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // Step 3: Define smart markers that will be replaced by data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");
```

> **Pourquoi les smart markers ?** Ils vous permettent de garder la mise en page Excel séparée du code. Vous concevez la feuille une fois, puis vous fournissez un `DataTable` et la bibliothèque fait le reste.

## Importer le DataTable dans Excel

Voici le cœur de **l’importation d’un DataTable dans Excel**. Nous construisons un `DataTable` qui reflète les champs des smart markers et le transmettons à `ImportDataTable`.

```csharp
        // Step 5: Build a simple DataTable that matches the smart marker fields
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // Step 6: Populate the worksheet with the DataTable via smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");
```

> **Cas limite :** Si votre table possède plus de colonnes que nécessaire, il suffit d’omettre les colonnes supplémentaires des smart markers ; elles seront ignorées.

## Enregistrer le classeur au format XLSX

Enfin, nous **enregistrons le classeur au format xlsx** sur le disque. La méthode `Save` détermine automatiquement le format à partir de l’extension du fichier.

```csharp
        // Step 7: Save the result to an Excel file
        workbook.Save("SmartMarkersConditional.xlsx");   // <-- saves as .xlsx
    }
}
```

C’est le programme complet. Lorsque vous l’exécutez, vous verrez un fichier nommé `SmartMarkersConditional.xlsx` dans le dossier de sortie.

### Résultat attendu

| Product | Quantity | Status |
|---------|----------|--------|
| Apple   | 120      | High   |
| Banana  | 80       | Low    |
| Cherry  | 150      | High   |

Les lignes avec **Quantity > 100** (Apple et Cherry) auront du texte rouge sur fond jaune grâce à la mise en forme conditionnelle que nous avons ajoutée précédemment.

## Créer un fichier Excel programmatique – Listing complet du code source

Ci‑dessous se trouve le code source complet, prêt à être copié. Il contient chaque élément abordé, ainsi que quelques commentaires supplémentaires pour plus de clarté.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write header cells
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // 3️⃣ Insert smart markers – placeholders for our data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");

        // 4️⃣ Apply conditional formatting (highlight >100)
        int cfIdx = worksheet.ConditionalFormattings.Add();
        var cf = worksheet.ConditionalFormattings[cfIdx];
        var cond = cf.AddCondition(FormatConditionType.CellValue, OperatorType.Greater, "100");
        cond.Style = workbook.CreateStyle();
        cond.Style.Font.Color = Color.Red;
        cond.Style.Pattern = BackgroundType.Solid;
        cond.Style.ForegroundColor = Color.Yellow;

        // 5️⃣ Build a DataTable that matches the markers
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // 6️⃣ Import the DataTable – this replaces the smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");

        // 7️⃣ Save the workbook – this will create an .xlsx file
        workbook.Save("SmartMarkersConditional.xlsx");
    }
}
```

> **Conseil :** Si vous devez générer plusieurs feuilles, répétez simplement les étapes 2‑6 sur une nouvelle instance `Worksheet` obtenue via `workbook.Worksheets.Add()`.

## Pourquoi utiliser Aspose.Cells pour l’automatisation Excel en C# ?

- **Performance :** Fonctionne entièrement en mémoire, sans interop COM, ce qui le rend rapide même avec de gros ensembles de données.  
- **Richesse fonctionnelle :** Prend en charge les smart markers, la mise en forme conditionnelle, les graphiques, les tableaux croisés dynamiques, etc.  
- **Multiplateforme :** Fonctionne sous Windows, Linux et macOS avec .NET Core/5/6+.  

Si vous êtes bloqué sur une fonctionnalité particulière — par exemple, ajouter un graphique ou protéger une feuille — recherchez simplement “asp​ose.cells add chart c#” et vous trouverez un modèle similaire.

## Prochaines étapes & sujets associés

- **Exportation en PDF :** Après avoir **crée un classeur Excel C#**, vous pouvez immédiatement exporter en PDF avec `workbook.Save("output.pdf")`.  
- **Lire des fichiers Excel existants :** Utilisez `new Workbook("ExistingFile.xlsx")` pour modifier un modèle.  
- **Importation massive :** Pour de très gros volumes, envisagez `ImportArray` ou `ImportDataTable` avec `ImportOptions` afin d’améliorer la vitesse.  

N’hésitez pas à expérimenter avec différentes règles conditionnelles, couleurs, ou même à ajouter une ligne de total avec des formules. Le ciel est la limite lorsque vous **créez un fichier Excel programmatique**.

---

*Prêt à essayer ? Récupérez le code, exécutez‑le et ouvrez le `SmartMarkersConditional.xlsx` généré. Si vous rencontrez le moindre problème, laissez un commentaire ci‑dessous—bon codage !*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}