---
category: general
date: 2026-07-13
description: Comment exporter une plage de cellules en tant que tableau avec C# et
  ExportTableOptions. Apprenez, étape par étape, la configuration du classeur, le
  formatage et l’exportation du tableau.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: fr
lastmod: 2026-07-13
og_description: Comment exporter une plage de cellules en tant que tableau en C# avec
  ExportTableOptions. Suivez ce guide pour formater les cellules, créer un classeur
  et exporter un tableau sans effort.
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: Comment exporter une plage de cellules en tableau – Guide complet C#
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: Comment exporter une plage de cellules en tant que tableau – Guide complet
  C#
url: /fr/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter une plage de cellules en tant que tableau – Guide complet C#

Vous vous êtes déjà demandé **comment exporter une plage de cellules en tant que tableau** sans perdre vos cheveux à cause des bizarreries de formatage ? Vous n'êtes pas seul. Que vous alimentiez un pipeline de rapports ou que vous ayez simplement besoin d'un dump rapide à la façon CSV, maîtriser le processus d'exportation peut vous faire gagner des heures de copier‑coller manuel.

Dans ce tutoriel, nous passerons en revue les étapes exactes pour prendre une cellule numérique, appliquer la notation scientifique et l'exporter en tant que tableau à l'aide de **ExportTableOptions**. À la fin, vous disposerez d'un extrait fonctionnel, comprendrez le *pourquoi* de chaque appel et saurez comment ajuster le code pour des plages plus grandes ou des formats différents.

## Prérequis

- .NET 6 ou ultérieur (l'API fonctionne de la même façon sur .NET Framework 4.7+)
- Aspose.Cells for .NET installé (`Install-Package Aspose.Cells`)
- Une compréhension de base de la syntaxe C# ; aucune connaissance approfondie d'Excel n'est requise

Vous avez tout cela ? Parfait—plongeons‑y.

## Étape 1 : Configurer les options d’exportation – Comment exporter une plage de cellules en tant que tableau

La première chose dont vous avez besoin est une instance **ExportTableOptions** qui indique à la bibliothèque comment traiter le contenu des cellules. Sans cela, l'exportation utilise les valeurs numériques brutes, ce qui peut casser les consommateurs en aval qui attendent du texte.

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**Pourquoi c’est important :**  
- `ExportAsString = true` force la bibliothèque à écrire le texte affiché de la cellule, et non son double sous‑jacent.  
- `CustomFormat` vous permet d’imposer une **exportation en notation scientifique**, utile lorsqu’on travaille avec des nombres très grands ou très petits.

> **Astuce :** Si vous avez besoin d’un format date ou monnaie, remplacez `"0.00E+00"` par `"yyyy‑MM‑dd"` ou `"$#,##0.00"` respectivement.

## Étape 2 : Créer un classeur et récupérer la première feuille – Gestion du classeur et de la feuille

Un **Workbook** représente le fichier Excel complet, tandis qu’une **Worksheet** correspond à un onglet unique. Pour une exportation simple, nous resterons sur la première feuille, toujours présente à l’index 0.

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**Pourquoi c’est important :**  
Créer un `Workbook` vierge garantit une ardoise propre—pas de styles cachés ou de données résiduelles qui pourraient vous surprendre. Accéder à `Worksheets[0]` est le moyen le plus rapide d’obtenir une référence à la feuille active sans se soucier des noms de feuilles.

## Étape 3 : Remplir la cellule cible – Formatage de la valeur de cellule en C#

Nous insérons maintenant une valeur numérique dans la cellule **A1** (ligne 0, colonne 0). La valeur choisie possède volontairement de nombreux décimaux afin que vous puissiez voir la notation scientifique en action.

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**Pourquoi c’est important :**  
L’appel à `PutValue` déduit automatiquement le type de données de la cellule. Comme nous exportons ensuite en tant que chaîne, le double brut sera converti à l’aide du format que nous avons défini précédemment, produisant un résultat propre comme `"1.23E+04"`.

## Étape 4 : Exporter la plage de cellules définie en tant que tableau – Exportation de la plage de cellules en tableau

Avec les options et les données en place, l’étape finale consiste à demander à Aspose.Cells d’écrire la plage. La méthode `ExportTable` attend la ligne/colonne de départ, la taille de la plage et l’objet d’options que nous avons construit.

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**Pourquoi c’est important :**  
- `totalRows = 1` et `totalColumns = 1` limitent l’exportation à une seule cellule, mais vous pouvez augmenter ces nombres pour couvrir des blocs plus larges (par ex., `5, 3` pour une plage de 5 lignes × 3 colonnes).  
- La méthode écrit les données dans une structure de tableau interne qui peut être enregistrée en CSV, HTML, ou même diffusée directement vers un client.

### Enregistrement du résultat (optionnel)

Si vous souhaitez persister le tableau exporté sur le disque, vous pouvez l’écrire dans un fichier CSV :

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

L’exécution du code ci‑dessus générera un fichier contenant :

```
1.23E+04
```

## Cas limites et variantes courantes

| Situation | Ce qu’il faut modifier | Raison |
|-----------|------------------------|--------|
| **Exportation de plusieurs lignes** | Ajuster `totalRows` et boucler sur les lignes si nécessaire | Permet une exportation par lots sans appeler `ExportTable` à chaque fois |
| **Conservation des formules** | Définir `ExportAsString = false` | Conserve la formule originale au lieu de la valeur affichée |
| **Délimiteurs différents** | Utiliser la surcharge `ExportTableToCSV(..., ',', ...)` | Passe du séparateur virgule à un séparateur tabulation ou pipe |
| **Grandes feuilles de calcul** | Diffuser l’exportation pour éviter `OutOfMemoryException` | Fonctionne bien pour plus de 10 000 lignes |

## Exemple complet fonctionnel

Voici le programme complet, prêt à copier‑coller. Il compile avec n’importe quel projet console .NET qui référence Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**Sortie attendue :**  
Un fichier nommé `ExportedTable.csv` contenant une seule ligne :

```
1.23E+04
```

Si vous ouvrez le CSV dans un éditeur de texte, vous verrez la notation scientifique appliquée exactement comme définie.

## Conclusion

Nous avons couvert **comment exporter une plage de cellules en tant que tableau** du début à la fin : configuration de `ExportTableOptions`, création d’un `Workbook`, insertion de données, puis appel à `ExportTable`. En comprenant chaque composant, vous pouvez désormais adapter la méthode à des plages plus larges, à d’autres formats, ou même l’intégrer à une API web qui sert des données dérivées d’Excel à la volée.

En perspective, vous pourriez explorer :

- **ExportTableToHTML** pour des aperçus prêts pour le web  
- **ExportTableToDataTable** pour alimenter directement des pipelines ADO.NET  
- Formats **personnalisés avancés** pour les dates, monnaies ou pourcentages  

Essayez ces options, et vous transformerez une simple exportation de cellule en un moteur de livraison de données polyvalent. Des questions ou un cas d’usage particulier ? Laissez un commentaire ci‑dessous—bon codage !

## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants abordent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Access an Excel Cell by Name Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}