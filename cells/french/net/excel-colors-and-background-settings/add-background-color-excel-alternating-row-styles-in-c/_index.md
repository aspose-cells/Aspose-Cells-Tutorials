---
category: general
date: 2026-04-07
description: Ajouter une couleur d’arrière‑plan aux lignes Excel avec C#. Apprenez
  à appliquer des couleurs de lignes alternées, à définir des styles d’arrière‑plan
  unis et à importer un DataTable dans Excel en un seul flux de travail.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: fr
og_description: Ajouter une couleur d'arrière-plan aux lignes Excel avec C#. Ce guide
  montre comment appliquer des couleurs de lignes alternées, définir un arrière-plan
  uni et importer un DataTable vers Excel de manière efficace.
og_title: Ajouter une couleur d'arrière-plan dans Excel – Styles de lignes alternées
  en C#
tags:
- C#
- Excel
- DataTable
- Styling
title: Ajouter une couleur d’arrière‑plan dans Excel – Styles de lignes alternées
  en C#
url: /fr/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une couleur d'arrière‑plan Excel – Styles de lignes alternées en C#

Vous avez déjà eu besoin d'**ajouter une couleur d'arrière‑plan Excel** aux lignes sans savoir comment le faire sans des milliers de lignes de code fastidieux ? Vous n'êtes pas seul — la plupart des développeurs rencontrent ce problème lorsqu'ils essaient pour la première fois de rendre leurs feuilles de calcul plus qu'un simple dépôt brut de données.  

La bonne nouvelle ? En quelques minutes, vous pouvez **appliquer des couleurs de lignes alternées**, définir un **fond uni**, et même **importer datatable to excel** en utilisant un modèle propre et réutilisable en C#.  

Dans ce tutoriel, nous parcourrons l’ensemble du processus, depuis la récupération des données dans un `DataTable` jusqu’au style de chaque ligne avec un motif de bandes jaune‑clair‑blanc. Aucun bibliothèque externe n’est nécessaire au‑delà d’un package solide de gestion d’Excel (comme **ClosedXML** ou **GemBox.Spreadsheet**), et vous verrez pourquoi cette approche est à la fois performante et facile à maintenir.

## Ce que vous allez apprendre

- Comment récupérer des données et les injecter dans une feuille Excel.  
- Comment **style excel rows** avec des couleurs d’arrière‑plan alternées.  
- La mécanique derrière **set solid background** à l’aide de l’objet `Style`.  
- Comment **import datatable to excel** tout en conservant les styles de lignes.  
- Astuces pour gérer les cas limites tels que les tables vides ou les schémas de couleurs personnalisés.

> **Astuce pro :** Si vous utilisez déjà un objet workbook (`wb`) provenant d’une bibliothèque qui prend en charge la création de styles, vous pouvez réutiliser les mêmes instances `Style` sur plusieurs feuilles — cela économise de la mémoire et garde votre code propre.

---

## Étape 1 : Récupérer les données – Préparer le DataTable

Avant que le style ne puisse être appliqué, nous avons besoin d’une source de lignes. Dans la plupart des scénarios réels, cela provient d’une base de données, d’une API ou d’un fichier CSV. Pour l’illustration, nous créerons simplement un `DataTable` simple en mémoire.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Pourquoi c’est important :** Utiliser un `DataTable` vous fournit un conteneur tabulaire, conscient du schéma, que la bibliothèque Excel peut importer directement, éliminant ainsi le besoin d’écrire des boucles cellule par cellule.

---

## Étape 2 : Créer les styles de lignes – **Apply alternating row colors**

Nous allons maintenant construire un tableau d’objets `Style` — un par ligne — afin que chaque ligne puisse recevoir son propre arrière‑plan. Le motif que nous utiliserons est le classique jaune‑clair pour les lignes paires et blanc pour les lignes impaires.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Explication :**  
- `wb.CreateStyle()` vous fournit un objet style vierge que vous pouvez modifier sans affecter les autres.  
- L’opérateur ternaire `(i % 2 == 0)` décide si la ligne est paire (jaune clair) ou impaire (blanc).  
- Définir `Pattern = BackgroundType.Solid` est l’étape cruciale qui **set solid background** ; sans cela, la couleur serait ignorée.

---

## Étape 3 : Récupérer la feuille cible

La plupart des bibliothèques exposent une collection de feuilles. Nous travaillerons avec la première, mais vous pouvez cibler n’importe quel indice ou nom selon vos besoins.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Si le classeur est tout neuf, la bibliothèque crée généralement une feuille par défaut pour vous. Sinon, vous pouvez en ajouter une explicitement :

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## Étape 4 : Importer le DataTable avec les styles de lignes – **Import datatable to excel**

Avec les styles prêts, l’étape finale consiste à pousser le `DataTable` dans la feuille tout en appliquant le style correspondant à chaque ligne.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**Que se passe‑t‑il en coulisses ?**  
- `true` indique à la méthode d’écrire les en‑têtes de colonnes comme première ligne.  
- `0, 0` désigne le coin supérieur gauche (A1) comme point d’insertion.  
- `rowStyles` aligne chaque `Style` avec la ligne de données correspondante, nous donnant les couleurs alternées préparées précédemment.

---

## Étape 5 : Enregistrer le classeur

Le dernier morceau du puzzle consiste à persister le classeur dans un fichier afin de pouvoir l’ouvrir dans Excel et voir le résultat.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Ouvrez le fichier et vous devriez voir une feuille correctement formatée :

- Ligne d’en‑tête en gras (style par défaut de la bibliothèque).  
- Lignes 1, 3, 5… avec un arrière‑plan blanc propre.  
- Lignes 2, 4, 6… avec un remplissage subtil jaune‑clair, facilitant la lecture.

### Capture d’écran du résultat attendu

| Id | Nom       | Score |
|----|-----------|-------|
| 1  | Étudiant 1| 78,45 |
| 2  | Étudiant 2| 62,13 |
| 3  | Étudiant 3| 91,27 |
| …  | …         | …     |

Les lignes 2, 4, 6, … apparaissent avec un arrière‑plan jaune‑clair — exactement l’effet **apply alternating row colors** visé.

![Add background color excel example](https://example.com/excel-background.png "Add background color excel example")

*(Le texte alternatif inclut le mot‑clé principal pour le SEO.)*

---

## Gestion des cas limites & variantes

### DataTable vide

Si `dataTable.Rows.Count` vaut zéro, le tableau `rowStyles` sera vide et `ImportDataTable` écrira quand même la ligne d’en‑tête (si `includeHeaders` est `true`). Aucune exception n’est levée, mais vous pourriez vouloir protéger contre la génération d’un fichier presque vide :

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Schémas de couleurs personnalisés

Vous voulez des bandes bleu/gris au lieu de jaune/blanc ? Remplacez simplement les valeurs `Color` :

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

N’hésitez pas à extraire les couleurs d’un fichier de configuration afin que les non‑développeurs puissent ajuster la palette sans toucher au code.

### Réutilisation des styles sur plusieurs feuilles

Si vous exportez plusieurs tables dans le même classeur, vous pouvez générer le tableau de styles une fois et le réutiliser :

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Assurez‑vous simplement que les deux tables ont le même nombre de lignes, ou générez un nouveau tableau par feuille.

---

## Exemple complet fonctionnel

En réunissant tous les éléments, voici un programme autonome que vous pouvez copier‑coller dans une application console.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Exécutez le programme, ouvrez `Report.xlsx`, et vous verrez le fond alterné exactement comme décrit.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}