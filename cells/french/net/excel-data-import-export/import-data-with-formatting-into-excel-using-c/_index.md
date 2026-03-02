---
category: general
date: 2026-03-01
description: Importer des données avec mise en forme dans Excel en utilisant C#. Apprenez
  comment importer un DataTable dans Excel et ajouter une couleur d’arrière‑plan aux
  cellules en quelques étapes seulement.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: fr
og_description: Importer des données avec mise en forme dans Excel à l'aide de C#.
  Guide étape par étape montrant comment importer un DataTable et ajouter une couleur
  d'arrière‑plan aux cellules.
og_title: Importer des données avec mise en forme dans Excel – Guide C#
tags:
- C#
- Excel
- DataTable
- Formatting
title: Importer des données avec mise en forme dans Excel à l'aide de C#
url: /fr/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Importer des données avec mise en forme dans Excel avec C#

Vous avez déjà eu besoin d'**importer des données avec mise en forme** dans un classeur Excel mais vous obteniez toujours une feuille simple et ennuyeuse ? Vous n'êtes pas seul. La plupart des développeurs rencontrent ce problème lorsqu'ils découvrent que l'importation par défaut supprime toutes les couleurs et les styles qu'ils ont soigneusement configurés dans leurs données sources.

Dans ce tutoriel, nous allons parcourir une solution complète, prête à l’emploi, qui **importe un DataTable dans Excel** et **ajoute une couleur d’arrière‑plan aux cellules Excel** en même temps. Aucun post‑traitement supplémentaire n’est requis — votre feuille de calcul aura exactement l’aspect souhaité dès la création.

## Ce que vous allez apprendre

- Comment récupérer des données dans un `DataTable`.
- Comment définir un tableau d’objets `Style` contenant les couleurs d’arrière‑plan.
- Comment appeler `ImportDataTable` avec ces styles afin que l’importation conserve la mise en forme.
- Un exemple complet, exécutable, que vous pouvez coller dans une application console et voir le résultat immédiatement.
- Astuces, pièges et variantes pour les projets réels.

### Prérequis

- .NET 6.0 ou supérieur (le code fonctionne également avec .NET Framework 4.6+).
- La bibliothèque **GemBox.Spreadsheet** (la version gratuite suffit pour la démonstration).
- Une connaissance de base du C# et des concepts Excel.

Si vous vous demandez *pourquoi GemBox ?* parce qu’elle offre une méthode `ImportDataTable` en une seule ligne qui accepte des tableaux de styles — exactement ce dont nous avons besoin pour **importer des données avec mise en forme** sans écrire de boucle.

---

## Étape 1 : Configurer le projet et ajouter GemBox.Spreadsheet

Pour commencer, créez une nouvelle application console :

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Astuce :** La version gratuite limite les feuilles de calcul à 150 k cellules, ce qui est largement suffisant pour les démonstrations. Si vous atteignez cette limite, passez à la version payante ou utilisez EPPlus, mais l’API sera légèrement différente.

## Étape 2 : Récupérer les données source sous forme de `DataTable`

La première chose dont nous avons besoin est un `DataTable` qui reproduit les données que vous extrairiez normalement d’une base de données. Voici un petit helper qui en crée un en mémoire :

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Pourquoi c’est important :** En séparant la récupération des données dans sa propre méthode, vous pouvez remplacer la source—SQL, CSV, service web—sans toucher à la logique d’importation. Cela garde le code propre et rend le tutoriel **comment importer un datatable dans excel** réutilisable.

## Étape 3 : Définir les styles à appliquer

Vient maintenant la partie amusante : nous allons créer un tableau d’objets `Style`, chacun avec une `ForegroundColor` distincte. GemBox vous permet de définir `BackgroundPatternColor` (le remplissage de la cellule) et `ForegroundColor` (la couleur du texte). Pour cette démo, nous colorerons les deux premières colonnes différemment.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Explication :**  
- Les objets `Style` sont des conteneurs légers ; vous n’avez pas besoin d’en créer un nouveau pour chaque cellule.  
- En alignant l’ordre du tableau avec l’ordre des colonnes, GemBox applique automatiquement le style correspondant lors de l’importation.  
- C’est la clé pour **importer des données avec mise en forme** — la mise en forme voyage avec les données, pas après coup.

## Étape 4 : Importer le `DataTable` dans la feuille avec les styles

Avec les données et les styles prêts, nous pouvons maintenant créer un classeur, choisir la première feuille, et appeler `ImportDataTable`. La signature de la méthode ressemble à ceci :

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

Voici comment nous l’utilisons :

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**Que se passe-t‑il en coulisses ?**  
- `true` indique à GemBox d’écrire les noms de colonnes en première ligne.  
- `0, 0` positionne l’importation à la cellule A1.  
- `importStyles` associe chaque colonne aux couleurs que nous avons définies précédemment.  

Lorsque vous ouvrez *Report.xlsx*, vous verrez la colonne **ID** ombrée en bleu clair, la colonne **Name** en vert clair, et la colonne **Score** inchangée. C’est **importer des données avec mise en forme** en un seul appel.

## Étape 5 : Vérifier le résultat (sortie attendue)

Ouvrez le fichier `Report.xlsx` généré. Vous devriez voir quelque chose comme ceci :

| ID (bleu clair) | Name (vert clair) | Score |
|-----------------|-------------------|-------|
| 1               | Alice             | 93.5 |
| 2               | Bob               | 78.0 |
| 3               | Charlie           | 85.2 |
| 4               | Diana             | 91.3 |
| 5               | Ethan             | 67.8 |

- Les cellules de la colonne **ID** ont un arrière‑plan bleu clair.  
- Les cellules de la colonne **Name** ont un arrière‑plan vert clair.  
- La colonne **Score** conserve le fond blanc par défaut.

Ce repère visuel rend le rapport immédiatement lisible — une petite touche qui peut améliorer considérablement l’expérience utilisateur.

![Feuille Excel montrant l'importation de données avec mise en forme – colonne ID en bleu clair, colonne Name en vert clair](excel-screenshot.png "exemple d'importation de données avec mise en forme")

*Le texte alternatif de l’image inclut le mot‑clé principal pour le SEO.*

---

## Questions fréquentes & cas particuliers

### Puis‑je appliquer autre chose que des couleurs d’arrière‑plan ?

Absolument. `Style` vous permet de définir les polices, bordures, formats numériques, et même la mise en forme conditionnelle. Par exemple, pour rendre les scores supérieurs à 90 en gras et rouge :

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### Que se passe‑t‑il si mon `DataTable` possède plus de colonnes que de styles ?

GemBox appliquera les styles uniquement aux colonnes qui ont une entrée correspondante dans le tableau. Les colonnes supplémentaires utilisent le style par défaut — aucune erreur n’est levée.

### Cette méthode fonctionne‑t‑elle avec de gros ensembles de données ?

Oui, mais surveillez la limite de cellules de la version gratuite (150 k cellules). Pour des rapports très volumineux, envisagez la licence payante ou le flux de données ligne par ligne avec `worksheet.Cells[row, col].Value = …` — bien que vous perdiez la commodité du one‑liner.

### Comment importer des données avec mise en forme depuis un modèle Excel existant ?

Vous pouvez d’abord charger un classeur modèle :

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

Cela vous permet de conserver les logos d’en‑tête, pieds de page et tout style préexistant tout en **important des données avec mise en forme** pour la partie dynamique.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Exécutez le programme (`dotnet run`) et ouvrez le fichier *Report.xlsx* généré pour voir les couleurs appliquées instantanément.

---

## Conclusion

Vous disposez maintenant d’une solution solide, end

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}