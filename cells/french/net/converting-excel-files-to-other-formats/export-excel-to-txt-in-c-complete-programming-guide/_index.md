---
category: general
date: 2026-08-11
description: Exporter Excel en txt en C# avec un guide étape par étape. Apprenez à
  convertir xlsx en texte brut à l'aide d'Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: fr
lastmod: 2026-08-11
og_description: Exporter Excel vers txt en C# rapidement. Ce tutoriel montre comment
  convertir xlsx en texte brut, configurer les formats et gérer de grandes feuilles
  de calcul.
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: Exporter Excel en TXT avec C# – guide étape par étape pour les développeurs
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: Exporter Excel en txt en C# – guide complet de programmation
url: /fr/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter Excel vers TXT en C# – guide complet de programmation

Si vous devez **exporter excel vers txt**, vous pouvez obtenir le résultat avec quelques lignes de code C#. Ce guide montre comment convertir un classeur `.xlsx` en un fichier texte brut tout en conservant le format de données que vous définissez.

Exporter des feuilles de calcul en tant que fichiers texte est une exigence courante lorsque les systèmes en aval n'acceptent que des données délimitées ou lorsque vous devez auditer les valeurs brutes des cellules. Dans les sections suivantes, vous apprendrez comment configurer les formats de date et de nombre, gérer les grandes feuilles et éviter les pièges typiques.

## Prérequis pour convertir xlsx en texte brut

* .NET 6.0 (ou ultérieur) installé – le code cible .NET Standard 2.0, il fonctionne donc également avec .NET Framework 4.6+.
* Une licence pour **Aspose.Cells** (l'évaluation gratuite fonctionne pour les tests).
* Un IDE tel que Visual Studio 2022 ou Visual Studio Code.
* Un fichier Excel nommé `input.xlsx` placé dans un dossier que vous pouvez référencer depuis votre projet.

Ces éléments sont les seules exigences externes ; le tutoriel ne dépend d'aucun package NuGet supplémentaire.

## Comment exporter excel vers txt avec Aspose.Cells

Aspose.Cells fournit la classe `ExportTableOptions` qui vous permet de contrôler la façon dont les valeurs des cellules sont rendues sous forme de chaînes. En définissant `ExportAsString` à `true`, vous forcez chaque cellule à être écrite en texte, ce qui est essentiel lorsque vous souhaitez une sortie texte déterministe.

### Étape 1 – charger le classeur

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*Le constructeur `Workbook` lit le fichier Excel en mémoire. Si le fichier n'existe pas, une exception est levée, il peut donc être judicieux d'encapsuler cet appel dans un bloc try‑catch pour le code de production.*

### Étape 2 – obtenir la première feuille de calcul

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*Les feuilles de calcul sont indexées à partir de zéro, donc l'index 0 fait référence au premier onglet. Vous pouvez remplacer l'index par un nom de feuille (`workbook.Worksheets["Sheet1"]`) lorsque vous devez cibler un onglet spécifique.*

### Étape 3 – définir les options d'exportation pour la conversion en texte

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` garantit que chaque cellule, quel que soit son type d'origine, devient une chaîne dans le fichier de sortie. Les propriétés `DateTimeFormat` et `NumberFormat` vous permettent de contrôler l'apparence des dates et des nombres, ce qui est crucial lorsque vous **convertissez xlsx en texte brut** pour des systèmes qui attendent un format spécifique.*

### Étape 4 – exporter la feuille de calcul en fichier texte

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` écrit le contenu de la feuille de calcul dans un fichier texte en utilisant les options que vous avez fournies. Le délimiteur par défaut est le caractère tabulation (`\t`). Si vous avez besoin d'un autre délimiteur, vous pouvez utiliser la surcharge qui accepte une instance `ExportTableOptions` et spécifier `ExportTableOptions.Separator`. Le fichier résultant peut être ouvert dans n'importe quel éditeur de texte ou importé dans une base de données.*

#### Sortie attendue

Supposons que `input.xlsx` contienne :

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Sample text|

Avec les options ci‑dessus, le fichier `Exported.txt` contiendra :

```
2023-05-01	1,234.50	Sample text
```

Chaque colonne est séparée par une tabulation, les dates suivent le format `yyyy‑MM‑dd`, et les nombres utilisent une virgule comme séparateur de milliers et deux décimales.

## Pièges courants lors de l'exportation d'une feuille de calcul en fichier texte

| Problème | Pourquoi cela se produit | Comment l'éviter |
|----------|--------------------------|-------------------|
| Format de nombre dépendant de la locale | Le format par défaut respecte la culture du système d'exploitation, ce qui peut produire des virgules ou des points de manière incohérente. | Définissez explicitement `NumberFormat` dans `ExportTableOptions`. |
| Les lignes ou colonnes masquées apparaissent dans la sortie | Aspose.Cells exporte toute la plage utilisée, y compris les lignes masquées. | Définissez `ExportTableOptions.ExportHiddenRows = false` et `ExportHiddenColumns = false` si vous souhaitez les ignorer. |
| Les grandes feuilles de calcul provoquent une pression mémoire | Le classeur complet est chargé en mémoire avant l'exportation. | Utilisez `Workbook.LoadOptions` avec `LoadDataOnly = true` pour réduire l'utilisation de la mémoire, ou traitez le fichier par morceaux. |
| Cellules de date stockées en texte dans le fichier source | Si une cellule contient déjà une chaîne formatée, l'exportateur la traite comme du texte et ignore `DateTimeFormat`. | Assurez-vous que le classeur source stocke les dates en tant que types de date Excel appropriés. |

Résoudre ces problèmes rend le processus **d'exportation d'une feuille de calcul Excel en texte** fiable sur différents environnements.

## Étendre la solution – délimiteurs personnalisés et exportation en flux

Si vous avez besoin d'un fichier de valeurs séparées par des virgules (CSV) au lieu d'un fichier à tabulations, modifiez les options :

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

Pour les fichiers supérieurs à 500 Mo, l'exportation en flux empêche l'application d'épuiser la RAM :

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

La surcharge qui accepte un `Stream` écrit les lignes de manière incrémentielle, ce qui est idéal pour les jobs batch ou les services web qui renvoient le fichier texte directement à un client.

## Vérifier le résultat programmétiquement

Après la fin de l'exportation, vous pouvez lire la première ligne en mémoire pour confirmer le format :

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

L'exécution de cet extrait devrait afficher la même ligne que celle présentée dans la section *Sortie attendue*, vous assurant que la conversion a réussi.

## Récapitulatif du code complet

Assembler toutes les pièces donne un programme autonome que vous pouvez copier dans une application console :

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

Compilez et exécutez le programme ; le fichier `Exported.txt` apparaît dans le même répertoire que le classeur source.

## Prochaines étapes et sujets associés

* **Export worksheet as text file** – expérimentez différents délimiteurs, encodages (UTF‑8 vs. ASCII) et styles de fin de ligne pour une compatibilité multiplateforme.
* **Bulk conversion** – parcourez `workbook.Worksheets` pour générer un fichier texte distinct pour chaque onglet.
* **Integration with databases** – canalisez le texte généré directement dans une opération d'insertion en masse pour SQL Server ou PostgreSQL.
* **

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment exporter des fichiers Excel en .NET avec Aspose.Cells : Guide complet](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Comment exporter les lignes Excel visibles avec Aspose.Cells pour .NET : Guide étape par étape](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Comment exporter des graphiques Excel en PDF avec Aspose.Cells pour .NET : Guide étape par étape](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}