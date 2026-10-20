---
category: general
date: 2026-08-11
description: Créer une feuille Excel à partir d’un DataTable en C# et exporter le
  DataTable vers Excel avec un nommage automatique des feuilles. Apprenez comment
  ajouter des lignes à un DataTable et enregistrer le classeur au format xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: fr
lastmod: 2026-08-11
og_description: Créer une feuille Excel à partir d’un DataTable en C#. Ce tutoriel
  montre comment exporter le DataTable vers Excel, ajouter des lignes au DataTable,
  générer plusieurs feuilles Excel et enregistrer le classeur au format xlsx.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: Créer une feuille Excel à partir d’un DataTable en C# – guide complet de
  programmation
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Créer une feuille Excel à partir d’un DataTable en C# – guide étape par étape
url: /fr/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer une feuille Excel à partir d’un DataTable en C# – guide étape par étape

Si vous devez **créer une feuille Excel** à partir d’un `DataTable` en C#, ce guide vous montre exactement comment le faire. Vous verrez comment **exporter un datatable vers Excel**, ajouter des lignes, gérer les noms de feuilles en double, et enfin **enregistrer le classeur au format xlsx**.

L’exemple utilise Aspose.Cells, une bibliothèque .NET largement utilisée pour l’automatisation d’Excel. Les mêmes concepts s’appliquent à d’autres bibliothèques supportant le traitement de type SmartMarker, mais le code ci‑dessous fonctionne immédiatement avec Aspose.Cells 22.12 ou version ultérieure.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* le SDK .NET 6.0 ou une version ultérieure installé  
* une référence au package NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`)  
* une connaissance de base du `DataTable` et des applications console C#  

Ces exigences permettent de garder le tutoriel autonome et d’éviter les outils externes.

## Étape 1 : Créer un DataTable qui sera exporté vers Excel

La première étape consiste à construire un `DataTable` qui reflète les données que vous voulez dans la feuille de calcul. Ici nous créons une table nommée **Sheet1**, ajoutons une colonne `Id`, et insérons deux lignes.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**Pourquoi c’est important :**  
`DataTable` est une représentation en mémoire pratique des données tabulaires. Nommer la table `"Sheet1"` indique à Aspose.Cells quelle feuille cibler lors du traitement des SmartMarkers.

## Étape 2 : Ajouter des lignes au DataTable (extension optionnelle)

Si vos données sources sont dynamiques, vous devrez souvent ajouter des lignes dans une boucle. L’extrait suivant montre un schéma typique :

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**Astuce :** Lors de l’ajout d’un grand nombre de lignes, envisagez de désactiver les contraintes (`dataTable.Constraints.Clear()`) pour améliorer les performances.

## Étape 3 : Configurer les options SmartMarker pour créer plusieurs feuilles Excel automatiquement

Les options SmartMarker vous permettent de contrôler la façon dont les noms de feuilles en double sont gérés. Définir `DetailSheetNewName` à `"Sheet1_{0}"` indique à Aspose.Cells de renommer les feuilles suivantes en `Sheet1_1`, `Sheet1_2`, etc.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**Pourquoi c’est important :**  
Lorsque vous traitez plusieurs objets `DataTable` qui partagent le même nom, Excel génère normalement une erreur parce que les noms de feuilles doivent être uniques. Le modèle `DetailSheetNewName` élimine automatiquement ce conflit.

## Étape 4 : Traiter les SmartMarkers et exporter le datatable vers Excel

Nous créons maintenant un nouveau `Workbook`, exécutons `ProcessSmartMarkers`, et laissons Aspose.Cells remplir la (les) feuille(s) à partir du `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**Explication :**  
`ProcessSmartMarkers` parcourt le classeur à la recherche de marqueurs comme `&=Sheet1!A1` (non affichés ici) et les remplace par les données du `dataTable`. Comme nous avons commencé avec un classeur vide, Aspose.Cells crée une nouvelle feuille correspondant au nom de la table et la remplit avec les lignes ajoutées.

## Étape 5 : Enregistrer le classeur au format xlsx

Enfin, écrivez le classeur sur le disque avec le format OpenXML moderne (`.xlsx`). Vous pouvez modifier le chemin pour l’adapter à votre environnement.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Résultat :**  
L’exécution du programme produit un fichier Excel contenant :

| Nom de la feuille | Lignes |
|-------------------|--------|
| Sheet1            | 1, 2, 3, 4, 5 |
| Sheet1_1          | (si un autre DataTable portant le même nom était traité) |

La logique de renommage des feuilles assure **la création de plusieurs feuilles Excel** sans gestion manuelle des noms.

## Variations courantes et cas limites

| Situation | Comment le gérer |
|-----------|------------------|
| **Tables très volumineuses** (≥ 100 000 lignes) | Utilisez `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` avant le traitement pour limiter la consommation mémoire. |
| **Ordre de colonnes personnalisé** | Réordonnez les objets `DataColumn` dans le `DataTable` avant d’appeler `ProcessSmartMarkers`. |
| **Plusieurs DataTables avec des noms différents** | Appelez `ProcessSmartMarkers` pour chaque table ; Aspose.Cells créera automatiquement une feuille distincte pour chaque nom. |
| **Besoin d’une ligne d’en‑tête avec style** | Après le traitement, accédez à `Worksheet.Cells["A1"]` et appliquez les propriétés `Style` (police, arrière‑plan). |
| **Enregistrement dans un flux au lieu d’un fichier** | Remplacez `workbook.Save(outputPath, SaveFormat.Xlsx)` par `workbook.Save(stream, SaveFormat.Xlsx)`. |

**Pro tip :** Enveloppez toujours les opérations système de fichiers dans des blocs `try…catch` afin de détecter rapidement les problèmes de permissions.

## Code source complet (prêt à copier)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Sortie attendue

L’exécution du programme affiche :

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

L’ouverture de `DuplicateSheets.xlsx` montre une feuille nommée **Sheet1** avec la colonne `Id` contenant les valeurs `1, 2, 3, 4, 5`. Si vous traitez plus tard un autre `DataTable` nommé `"Sheet1"` dans le même classeur, Aspose.Cells créera **Sheet1_1**, **Sheet1_2**, etc., automatiquement.

## Conclusion

Vous savez maintenant comment **créer une feuille Excel** à partir d’un `DataTable` en C#, **exporter le datatable vers Excel**, **ajouter des lignes au datatable**, générer **plusieurs feuilles Excel** avec un nommage automatique, et **enregistrer le classeur au format xlsx**. L’exemple complet et exécutable montre le flux de travail de bout en bout et fournit des astuces pratiques pour les grands ensembles de données et le style personnalisé.

### Et après ?

* Explorez le **formatage des cellules** (polices, couleurs, bordures) en accédant à `Worksheet.Cells` après `ProcessSmartMarkers`.  
* Utilisez les boucles **SmartMarker** pour générer des rapports maître‑détail dans un même classeur.  
* Passez à l’**export CSV** en changeant `SaveFormat.Csv` si vous avez besoin d’une représentation texte brut.  

N’hésitez pas à adapter le code à vos propres sources de données — qu’il s’agisse d’une requête de base de données, d’une réponse d’API ou d’une collection en mémoire. Bon codage !

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos projets.

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}