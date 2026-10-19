---
category: general
date: 2026-05-30
description: Comment utiliser SmartMarkerProcessor pour renommer une feuille existante
  et automatiser les tâches de renommage de feuilles Excel en quelques étapes simples.
draft: false
keywords:
- how to use smartmarkerprocessor
- rename existing sheet
- automate excel sheet rename
language: fr
og_description: Comment utiliser SmartMarkerProcessor pour renommer une feuille existante
  et automatiser les tâches de renommage de feuilles Excel dans un guide concis, étape
  par étape.
og_title: Comment utiliser SmartMarkerProcessor – Renommer une feuille existante dans
  Excel
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use SmartMarkerProcessor to rename existing sheet and automate
    Excel sheet rename tasks in a few simple steps.
  headline: How to Use SmartMarkerProcessor – Rename Existing Sheet in Excel
  type: TechArticle
- description: How to use SmartMarkerProcessor to rename existing sheet and automate
    Excel sheet rename tasks in a few simple steps.
  name: How to Use SmartMarkerProcessor – Rename Existing Sheet in Excel
  steps:
  - name: 1. Multiple Existing Detail Sheets
    text: If your template already contains **Detail**, **Detail_1**, and **Detail_2**,
      the processor will generate **Detail_3**. This behavior is deterministic, so
      you can rely on it for batch processing.
  - name: 2. Custom Prefixes or Suffixes
    text: You might want the new sheet to start with a date stamp, e.g., `"Detail_2023-09-01"`.
      Set `DetailSheetNewName = $"Detail_{DateTime.Today:yyyy-MM-dd}"`. The processor
      will still add numeric suffixes if needed.
  - name: 3. Renaming Other Sheets
    text: '`SmartMarkerOptions` also provides `HeaderSheetNewName` and `SummarySheetNewName`.
      Use them the same way to **rename existing sheet** types beyond the detail sheet.'
  - name: 4. Performance Considerations
    text: When processing large workbooks (hundreds of sheets), instantiate **one**
      `SmartMarkerProcessor` and reuse it across files. This reduces memory churn
      and speeds up the **automate excel sheet rename** workflow.
  type: HowTo
tags:
- Excel automation
- GemBox
- SmartMarker
title: Comment utiliser SmartMarkerProcessor – Renommer une feuille existante dans
  Excel
url: /fr/net/worksheet-management/how-to-use-smartmarkerprocessor-rename-existing-sheet-in-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser SmartMarkerProcessor – Renommer une feuille existante dans Excel

Vous vous êtes déjà demandé **comment utiliser SmartMarkerProcessor** pour renommer une feuille existante pendant que vous remplissez des données ? Vous n'êtes pas le seul. De nombreux développeurs se heurtent à un problème lorsque leur modèle contient déjà une feuille de calcul « Detail » et que le moteur SmartMarker tente d’en créer une autre avec le même nom. La bonne nouvelle ? En quelques lignes de code, vous pouvez **automatiser le renommage des feuilles Excel** sans interrompre votre flux de travail.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui montre exactement comment configurer le processeur, renommer les feuilles existantes et garder vos fichiers Excel bien organisés. Pas de devinettes — juste du code clair, des explications sur *pourquoi* chaque ligne est importante, et des astuces pour gérer les cas limites que vous rencontrerez inévitablement.

---

## Prérequis

Avant de plonger, assurez‑vous d’avoir :

- **GemBox.Spreadsheet** (ou toute bibliothèque qui fournit `SmartMarkerProcessor`) version 2024‑latest installé via NuGet.  
- Un environnement de développement .NET (Visual Studio, VS Code, Rider—au choix).  
- Un modèle Excel de base (`Template.xlsx`) contenant déjà une feuille de calcul nommée **Detail**.  
- Une source de données simple (par ex. un `DataTable`, `List<T>` ou un objet anonyme) que vous souhaitez fusionner dans le modèle.

C’est tout. Si l’un de ces éléments vous manque, récupérez le package NuGet maintenant :

```bash
dotnet add package GemBox.Spreadsheet
```

---

![exemple d’utilisation de smartmarkerprocessor](/images/smartmarkerprocessor-rename.png "exemple d’utilisation de smartmarkerprocessor")

*L'image ci‑dessus illustre la feuille de calcul avant et après l'opération de renommage.*

---

## Étape 1 : Configurer l’instance SmartMarkerProcessor  

La première chose dont vous avez besoin est un objet **SmartMarkerProcessor**. Pensez‑y comme le moteur qui lit votre modèle, recherche les Smart Markers (comme `{{Name}}`) et écrit les données dans les cellules appropriées.

```csharp
using GemBox.Spreadsheet;
using GemBox.Spreadsheet.SmartMarkers;

// Initialize the component (license key is optional for the free version)
SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

// Load the workbook that contains the template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Create the processor instance.
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

> **Pourquoi c’est important :** Instancier le processeur **une seule fois** et le réutiliser tout au long de l’application réduit la surcharge. De plus, charger le classeur d’abord vous donne un accès à la collection de feuilles, dont nous aurons besoin lors du renommage des feuilles.

---

## Étape 2 : Configurer les options de renommage de feuille existante  

Voici le cœur du sujet : indiquer à SmartMarker comment se comporter lorsqu’il rencontre un conflit de nom de feuille. La classe `SmartMarkerOptions` expose une propriété appelée `DetailSheetNewName`. Si une feuille nommée `"Detail"` existe déjà, le processeur ajoutera automatiquement un suffixe (`_1`, `_2`, …) pour éviter le conflit.

```csharp
// Define processing options.
// The DetailSheetNewName property controls the base name for the detail sheet.
SmartMarkerOptions options = new SmartMarkerOptions
{
    // If "Detail" exists, the new sheet will become "Detail_1"
    DetailSheetNewName = "Detail"
};
```

> **Astuce :** Si vous préférez un suffixe personnalisé (par ex. `"Detail-Backup"`), définissez simplement `DetailSheetNewName = "Detail-Backup"`. Le processeur ajoutera toujours des numéros si nécessaire.  
> **Pourquoi c’est important :** Sans cette option, SmartMarker lancerait une exception ou écraserait silencieusement la feuille existante, entraînant une perte de données. Configurer explicitement le comportement de renommage **automatise le renommage des feuilles Excel** et préserve vos modèles.

---

## Étape 3 : Préparer la source de données  

SmartMarker peut travailler avec pratiquement n’importe quelle source de données énumérable. Pour l’illustration, utilisons une simple liste d’objets anonymes représentant des lignes de facture.

```csharp
var dataSource = new[]
{
    new { Item = "Widget A", Quantity = 5, Price = 9.99 },
    new { Item = "Widget B", Quantity = 2, Price = 19.95 },
    new { Item = "Widget C", Quantity = 1, Price = 49.50 }
};
```

Si vous avez déjà un `DataTable` ou un `IEnumerable<T>`, branchez‑le simplement — aucune conversion supplémentaire n’est nécessaire.

---

## Étape 4 : Appliquer le traitement SmartMarker à la première feuille de calcul  

Avec le processeur, les options et les données prêts, il est temps d’exécuter la fusion. Nous ciblerons la **première feuille** (`wb.Worksheets[0]`) car c’est là que se trouve notre modèle. La méthode `Process` accepte trois arguments : la feuille, la source de données et les options que nous avons définies précédemment.

```csharp
// Apply SmartMarker processing.
// This will insert the data into the template and rename the detail sheet if needed.
processor.Process(wb.Worksheets[0], dataSource, options);
```

> **Ce qui se passe en coulisses :**  
> 1. SmartMarker parcourt la feuille à la recherche de marqueurs comme `{{Item}}`, `{{Quantity}}`, etc.  
> 2. Il crée une nouvelle feuille de détail en utilisant le nom défini dans `DetailSheetNewName`.  
> 3. Si une feuille nommée « Detail » existe déjà, elle devient automatiquement « Detail_1 ».  
> 4. Les lignes de données sont écrites dans la nouvelle feuille, en conservant le formatage.

---

## Étape 5 : Enregistrer le résultat et vérifier le renommage  

Après le traitement, vous voudrez persister le classeur sur le disque et vérifier que la feuille a bien été renommée.

```csharp
// Save the processed workbook.
wb.Save("Result.xlsx");

// Quick verification (optional console output)
Console.WriteLine("Worksheets in the resulting file:");
foreach (var sheet in wb.Worksheets)
    Console.WriteLine($"- {sheet.Name}");
```

Lorsque vous ouvrez `Result.xlsx`, vous devriez voir une feuille nommée **Detail_1** (ou **Detail_2** si « Detail_1 » existait déjà). Les lignes de données apparaîtront sous la ligne d’en‑tête que vous avez placée dans le modèle.

---

## Gestion des cas limites courants  

### 1. Plusieurs feuilles Detail existantes  

Si votre modèle contient déjà **Detail**, **Detail_1** et **Detail_2**, le processeur générera **Detail_3**. Ce comportement est déterministe, vous pouvez donc vous y fier pour le traitement par lots.

### 2. Préfixes ou suffixes personnalisés  

Vous pouvez vouloir que la nouvelle feuille commence par un horodatage, par ex. `"Detail_2023-09-01"`. Définissez `DetailSheetNewName = $"Detail_{DateTime.Today:yyyy-MM-dd}"`. Le processeur ajoutera toujours des suffixes numériques si nécessaire.

### 3. Renommer d’autres feuilles  

`SmartMarkerOptions` propose également `HeaderSheetNewName` et `SummarySheetNewName`. Utilisez‑les de la même façon pour **renommer les types de feuilles** au‑delà de la feuille de détail.

```csharp
options.HeaderSheetNewName = "Header";
options.SummarySheetNewName = "Summary";
```

### 4. Considérations de performance  

Lors du traitement de classeurs volumineux (des centaines de feuilles), instanciez **un seul** `SmartMarkerProcessor` et réutilisez‑le pour tous les fichiers. Cela réduit la consommation de mémoire et accélère le workflow **automatiser le renommage des feuilles Excel**.

---

## Exemple complet fonctionnel  

En rassemblant le tout, voici un programme autonome que vous pouvez copier‑coller dans une application console et exécuter immédiatement :

```csharp
using System;
using GemBox.Spreadsheet;
using GemBox.Spreadsheet.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1. License & load template.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");
        var wb = ExcelFile.Load("Template.xlsx");

        // 2. Create processor.
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 3. Define rename options.
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // 4. Prepare data source.
        var dataSource = new[]
        {
            new { Item = "Widget A", Quantity = 5, Price = 9.99 },
            new { Item = "Widget B", Quantity = 2, Price = 19.95 },
            new { Item = "Widget C", Quantity = 1, Price = 49.50 }
        };

        // 5. Process the first worksheet.
        processor.Process(wb.Worksheets[0], dataSource, options);

        // 6. Save the result.
        wb.Save("Result.xlsx");

        // 7. Verify sheet names.
        Console.WriteLine("Worksheets after processing:");
        foreach (var sheet in wb.Worksheets)
            Console.WriteLine($"- {sheet.Name}");
    }
}
```

**Sortie attendue** (console) :

```
Worksheets after processing:
- Sheet1
- Detail_1
```

Ouvrez `Result.xlsx` et vous verrez les données correctement peuplées sous le nouvel onglet **Detail_1**.

---

## Récapitulatif  

Nous avons couvert **comment utiliser SmartMarkerProcessor** pour renommer en toute sécurité une feuille existante et **automatiser le renommage des feuilles Excel**. Les points clés sont :

1. Créez une instance unique de `SmartMarkerProcessor`.  
2. Définissez `DetailSheetNewName` (ou d’autres options de nom de feuille) pour contrôler la logique de renommage.  
3. Transmettez votre source de données et vos options à `Process`.  
4. Enregistrez et vérifiez que la feuille a bien été renommée comme prévu.

Avec ces étapes, vous pouvez intégrer SmartMarker dans n’importe quel pipeline de reporting — que vous génériez des factures, des journaux d’audit ou des tableaux de bord mensuels. L’approche est évolutive, gère les collisions de noms de façon élégante et garde vos modèles Excel réutilisables.

---

## Prochaines étapes  

- **Explorer d’autres SmartMarkerOptions** : `HeaderSheetNewName`, `SummarySheetNewName` et `InsertBlankRows` pour un contrôle plus fin.  
- **Combiner avec le style** : utilisez l’API de mise en forme riche de GemBox pour appliquer des couleurs, bordures ou mise en forme conditionnelle après la fusion.  
- **Traiter plusieurs classeurs en lot** : parcourez un répertoire de modèles, en réutilisant la même instance de processeur pour un débit maximal.

N’hésitez pas à expérimenter — peut‑être créerez‑vous une feuille « Report_2024_Q1 » qui ajoute automatiquement un numéro de version à chaque exécution. Les possibilités sont infinies, et vous disposez maintenant d’une base solide pour **renommer les feuilles existantes** de façon automatisée.

Bon codage, et que vos fichiers Excel restent toujours bien organisés !

## Que devriez‑vous apprendre ensuite ?

- [Comment fusionner et renommer des feuilles Excel avec Aspose.Cells pour .NET : guide pas à pas](/cells/english/net/worksheet-management/merge-rename-excel-sheets-aspose-cells-net/)
- [Comment modifier les ID de feuilles Excel en .NET avec Aspose.Cells : guide complet](/cells/english/net/worksheet-management/change-excel-sheet-id-net-aspose-cells/)
- [Comment utiliser Aspose.Cells pour .NET afin de regrouper des lignes et colonnes dans Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}