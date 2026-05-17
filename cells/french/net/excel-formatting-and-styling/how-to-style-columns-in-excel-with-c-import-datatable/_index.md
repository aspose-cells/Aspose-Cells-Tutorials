---
category: general
date: 2026-02-21
description: Apprenez à styliser les colonnes lors de l'importation d'un DataTable
  vers Excel avec C#. Inclut des astuces pour colorer la deuxième colonne dans Excel
  et importer un DataTable dans Excel en C#.
draft: false
keywords:
- how to style columns
- import datatable to excel
- how to import datatable
- color second column excel
- import datatable excel c#
language: fr
og_description: Comment styliser les colonnes lors de l'importation d'un DataTable
  vers Excel avec C#. Code étape par étape, colorer la deuxième colonne dans Excel,
  et meilleures pratiques.
og_title: Comment styliser les colonnes dans Excel avec C# – Guide complet
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Comment mettre en forme les colonnes dans Excel avec C# – Importer DataTable
url: /fr/net/excel-formatting-and-styling/how-to-style-columns-in-excel-with-c-import-datatable/
---

unchanged.

Now produce final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment styliser les colonnes dans Excel avec C# – Importer DataTable

Vous vous êtes déjà demandé **comment styliser les colonnes** dans une feuille Excel tout en récupérant les données directement depuis un `DataTable` ? Vous n'êtes pas le seul. De nombreux développeurs se heurtent à un mur lorsqu'ils ont besoin d'une touche rapide de couleur—peut‑être rouge pour la première colonne, bleu pour la deuxième—sans devoir manipuler manuellement chaque cellule après l'importation.  

Bonne nouvelle ? La réponse tient en quelques lignes de code C#, et vous disposerez d’une feuille entièrement stylisée dès que les données seront importées. Dans ce tutoriel, nous aborderons également **import datatable to excel**, vous montrerons **color second column excel**, et expliquerons pourquoi cette approche fonctionne à la fois avec .NET Framework et les projets .NET 6+.

---

## Ce que vous allez apprendre

- Récupérer un `DataTable` rempli (ou en créer un à la volée).  
- Définir des objets `Style` par colonne pour définir les couleurs de premier plan.  
- Créer un classeur, obtenir la première feuille de calcul, et importer le tableau avec les styles appliqués.  
- Gérer les cas limites comme les tables vides, les lignes de départ personnalisées et le nombre dynamique de colonnes.  

À la fin, vous pourrez déposer un fichier Excel stylisé dans n'importe quel pipeline de reporting—sans aucun post‑traitement requis.

> **Prérequis :** Une connaissance de base de C# et une référence à une bibliothèque de feuilles de calcul qui prend en charge `ImportDataTable` (par ex., Aspose.Cells, GemBox.Spreadsheet, ou EPPlus avec un helper). Le code ci‑dessous utilise **Aspose.Cells** car sa surcharge `ImportDataTable` accepte directement un `Style[]`.

---

## Étape 1 : Configurer le projet et ajouter la bibliothèque Excel

Avant de pouvoir styliser quoi que ce soit, nous avons besoin d’un projet qui référence une bibliothèque de manipulation Excel.

```csharp
// Install-Package Aspose.Cells -Version 24.7
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;   // For Color
```

*Astuce :* Si vous êtes sur .NET 6, ajoutez le package via `dotnet add package Aspose.Cells`. La bibliothèque fonctionne sous Windows, Linux et macOS, vous garantissant ainsi une compatibilité future.

---

## Étape 2 : Récupérer ou créer le DataTable source

Le cœur du tutoriel porte sur le stylisme, mais vous avez toujours besoin d’un `DataTable`. Ci‑dessous se trouve un petit helper qui crée des données d'exemple ; remplacez‑le par votre appel `GetTable()` en production.

```csharp
/// <summary>
/// Returns a DataTable with three columns and five rows of demo data.
/// </summary>
static DataTable GetTable()
{
    var dt = new DataTable("Demo");
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));

    dt.Rows.Add(1, "Alice", 92.5);
    dt.Rows.Add(2, "Bob", 85.3);
    dt.Rows.Add(3, "Charlie", 78.9);
    dt.Rows.Add(4, "Diana", 88.1);
    dt.Rows.Add(5, "Ethan", 91.4);

    return dt;
}
```

> **Pourquoi c’est important :** Utiliser un `DataTable` rend votre source de données agnostique—qu’elle provienne de SQL, CSV ou d’une collection en mémoire, la logique d’importation reste la même. C’est la pierre angulaire de **how to import datatable** efficacement.

---

## Étape 3 : Définir les styles de colonne (Le cœur de « How to Style Columns »)

Nous indiquons maintenant à la feuille de calcul comment chaque colonne doit apparaître. La classe `Style` vous permet de définir les polices, les couleurs, les bordures, etc. Pour cet exemple, nous ne modifions que la couleur de premier plan.

```csharp
// Step 3: Define column styles – red for first, blue for second, default for others
Style[] columnStyles = new Style[3]; // Assuming three columns; adjust as needed

// Style for column 0 (first column) – red text
columnStyles[0] = new Style();
columnStyles[0].ForegroundColor = Color.Red;

// Style for column 1 (second column) – blue text
columnStyles[1] = new Style();
columnStyles[1].ForegroundColor = Color.Blue;

// Column 2 (third column) – keep default styling
columnStyles[2] = new Style(); // No changes, but array entry required
```

*Et si vous avez plus de colonnes ?* Il suffit d’augmenter la taille du tableau et de remplir les styles qui vous intéressent. Les colonnes non stylisées héritent automatiquement du style par défaut de la feuille.

---

## Étape 4 : Créer le classeur et importer le DataTable avec les styles

Avec les données et les styles prêts, il est temps de tout rassembler.

```csharp
static void Main()
{
    // Retrieve the data
    DataTable dataTable = GetTable();

    // Initialize a new workbook (in‑memory)
    Workbook workbook = new Workbook();

    // Grab the first worksheet (index 0)
    Worksheet worksheet = workbook.Worksheets[0];

    // Import the DataTable starting at cell A1 (row 0, column 0)
    // The 'true' flag tells Aspose.Cells to include column headers
    worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

    // Optional: Auto‑fit columns for a cleaner look
    worksheet.AutoFitColumns();

    // Save the result to disk
    string outputPath = "StyledDataTable.xlsx";
    workbook.Save(outputPath);

    Console.WriteLine($"Excel file saved to {outputPath}");
}
```

**Que s’est‑il passé ?**  
- `ImportDataTable` copie les lignes, les colonnes et *optionnellement* la ligne d’en‑tête.  
- En passant `columnStyles`, chaque colonne reçoit le `Style` que nous avons défini précédemment.  
- L’appel ne tient qu’une seule ligne, ce qui signifie que **import datatable excel c#** est aussi simple que cela.

---

## Étape 5 : Vérifier le résultat – Sortie attendue

Ouvrez `StyledDataTable.xlsx` dans Excel (ou LibreOffice). Vous devriez voir :

| **ID** (rouge) | **Name** (bleu) | **Score** (par défaut) |
|----------------|-----------------|--------------------------|
| 1              | Alice           | 92.5                     |
| 2              | Bob             | 85.3                     |
| …              | …               | …                        |

- Le texte de la première colonne apparaît en **rouge**, répondant à l’exigence « how to style columns ».  
- Le texte de la deuxième colonne est **bleu**, ce qui couvre également la requête **color second column excel**.  

Si le fichier s’ouvre sans erreur, vous avez maîtrisé avec succès **how to import datatable** tout en stylisant les colonnes.

---

## Questions fréquentes & cas limites

### Et si le DataTable est vide ?
`ImportDataTable` créera quand même la ligne d’en‑tête (si vous avez passé `true`). Aucune ligne de données n’est ajoutée, mais les styles s’appliquent toujours aux cellules d’en‑tête.

### Besoin de commencer l’importation à une autre cellule ?
Modifiez les paramètres `rowIndex` et `columnIndex` dans `ImportDataTable`. Par exemple, pour commencer à `B2`, utilisez `1, 1` au lieu de `0, 0`.

### Vous voulez styliser les lignes plutôt que les colonnes ?
Vous pouvez parcourir `worksheet.Cells.Rows` après l’importation et attribuer un `Style` par ligne. Cependant, le stylisme au niveau des colonnes est beaucoup plus performant car la bibliothèque applique le style une fois par colonne.

### Utilisation d’EPPlus ou de ClosedXML ?
Ces bibliothèques n’exposent pas de surcharge directe `ImportDataTable` avec un tableau de styles. La solution de contournement consiste à importer d’abord le tableau, puis à parcourir la plage de colonnes et à définir `Style.Font.Color.SetColor(...)`. La logique reste la même, avec seulement quelques lignes supplémentaires.

---

## Astuces pro pour un code prêt à la production

- **Réutiliser les styles :** Créer un nouveau `Style` pour chaque colonne peut être gaspilleur. Stockez les styles réutilisables dans un dictionnaire indexé par couleur ou poids de police.  
- **Éviter les comptes de colonnes codés en dur :** Détectez `dataTable.Columns.Count` et construisez le tableau `columnStyles` dynamiquement.  
- **Sécurité des threads :** Si vous générez de nombreux classeurs en parallèle, créez un `Workbook` distinct par thread ; les objets Aspose.Cells ne sont pas thread‑safe.  
- **Performance :** Pour des tables de plus de 10 k lignes, envisagez de désactiver `AutoFitColumns` (cela parcourt chaque cellule) et définissez les largeurs de colonne manuellement.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
// ------------------------------------------------------------
// Full example: How to style columns while importing a DataTable
// ------------------------------------------------------------
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetTable();

        // 2️⃣ Define per‑column styles
        int colCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[colCount];

        // Red for first column
        columnStyles[0] = new Style { ForegroundColor = Color.Red };

        // Blue for second column (if it exists)
        if (colCount > 1)
            columnStyles[1] = new Style { ForegroundColor = Color.Blue };

        // Default style for remaining columns
        for (int i = 2; i < colCount; i++)
            columnStyles[i] = new Style(); // no special formatting

        // 3️⃣ Create workbook and import with styles
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
        sheet.AutoFitColumns();

        // 4️⃣ Save to file
        string path = "StyledDataTable.xlsx";
        workbook.Save(path);
        Console.WriteLine($"File saved: {path}");
    }

    // Helper: sample DataTable
    static DataTable GetTable()
    {
        var dt = new DataTable("Demo");
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        dt.Rows.Add(1, "Alice", 92.5);
        dt.Rows.Add(2, "Bob", 85.3);
        dt.Rows.Add(3, "Charlie", 78.9);
        dt.Rows.Add(4, "Diana", 88.1);
        dt.Rows.Add(5, "Ethan", 91.4);
        return dt;
    }
}
```

Exécutez le programme, ouvrez le `StyledDataTable.xlsx` généré, et vous verrez immédiatement les colonnes colorées. Voilà le flux complet **import datatable excel c#** en quelques lignes.

---

## Conclusion

Nous venons de couvrir **how to style columns** lorsque vous **import datatable to excel** avec C#. En définissant un tableau `Style[]` et en le passant à `ImportDataTable`, vous pouvez colorer la première colonne en rouge, la deuxième en bleu, et laisser le reste tel quel—le tout en une seule ligne de code.  

L’approche est évolutive : ajoutez d’autres objets `Style` pour des colonnes supplémentaires, ajustez les lignes de départ, ou remplacez Aspose.Cells par une autre bibliothèque offrant une API similaire. Vous pouvez désormais générer des rapports Excel soignés sans jamais toucher manuellement le fichier.

**Prochaines étapes** que vous pourriez explorer :

- Utiliser le **formatage conditionnel** pour mettre en évidence les valeurs dynamiquement (lié à “color second column excel”).  
- Exporter plusieurs feuilles de calcul à partir d’un même ensemble de `DataTable` (idéal pour les tableaux de bord mensuels).  
- Combiner cela avec la conversion **CSV → DataTable** pour construire une chaîne de bout en bout…

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}