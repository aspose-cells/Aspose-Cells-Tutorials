---
category: general
date: 2026-05-04
description: Exporter une plage de feuille de calcul en C# avec un formatage personnalisé.
  Apprenez comment exporter une plage Excel et comment personnaliser l’exportation
  des cellules en quelques étapes simples.
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: fr
og_description: Exporter une plage de feuille de calcul avec C#. Ce guide montre comment
  exporter une plage Excel et personnaliser l’exportation des cellules rapidement
  et de manière fiable.
og_title: Exporter la plage de feuille de calcul en C# – Guide complet de programmation
tags:
- C#
- Excel
- Data Export
title: Exporter une plage de feuille de calcul en C# – Guide complet de programmation
url: /fr/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter une plage de feuille de calcul en C# – Guide de programmation complet

Vous avez déjà eu besoin d'**exporter une plage de feuille de calcul** mais la sortie par défaut ne correspondait pas à ce que vous vouliez ? Vous n'êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu'ils essaient d'extraire un bloc de cellules vers un fichier CSV ou JSON. La bonne nouvelle ? En quelques lignes de C# vous pouvez non seulement **exporter une plage Excel** mais aussi **personnaliser l'exportation des cellules** pour qu'elle corresponde à n'importe quel format en aval.

Dans ce tutoriel, nous allons parcourir un scénario réel : prendre les cellules *A1:D10* d'un classeur Excel, transformer chaque valeur en une chaîne entre crochets, et écrire le résultat dans un fichier. À la fin, vous saurez exactement **comment exporter une plage de feuille de calcul** avec un contrôle total sur la représentation de chaque cellule, ainsi que quelques astuces pour les cas limites que vous pourriez rencontrer plus tard.

## Ce dont vous aurez besoin

- .NET 6 ou supérieur (le code fonctionne également avec .NET Framework 4.7+)
- Le package NuGet **GemBox.Spreadsheet** (ou toute bibliothèque offrant `ExportTableOptions` ; l'API présentée provient de GemBox)
- Une compréhension de base de la syntaxe C# — rien de compliqué, juste les habituelles instructions `using` et la création d'objets

Si vous avez tout cela, vous êtes prêt à plonger.

## Étape 1 : Configurer les options d'exportation – Point de contrôle principal  

La première chose à faire est de créer une instance de `ExportTableOptions` et de lui indiquer de traiter chaque cellule comme une chaîne. C’est la base pour **comment exporter une plage Excel** tout en conservant le type de données cohérent.

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*Pourquoi forcer l'exportation en chaîne ?*  
Lorsque vous personnaliserez chaque cellule, vous injecterez des crochets et éventuellement d'autres symboles. Garder tout sous forme de chaîne évite les surprises de conversion de type (par ex., les dates qui deviennent des nombres sériels).

## Étape 2 : S'abonner à l'événement CellExport – Personnaliser chaque cellule  

Vient maintenant la partie amusante : **comment personnaliser l'exportation des cellules**. GemBox déclenche un événement `CellExport` pour chaque cellule sur le point d'être écrite. En le gérant, vous pouvez entourer la valeur de crochets, ajouter un préfixe, ou même ignorer complètement une cellule.

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*Astuce pro :* Si vous ne souhaitez modifier que les cellules numériques, vérifiez `e.Value.GetType()` avant d'appliquer les crochets. Cette petite garde peut vous éviter de déformer accidentellement le texte d'en-tête.

## Étape 3 : Exporter la plage souhaitée – Action principale  

Avec les options prêtes, vous appelez `ExportTable`. La méthode prend le classeur que vous avez chargé, l'adresse de la plage que vous voulez, et les options que vous venez de configurer.

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

La surcharge que nous utilisons écrit directement dans un fichier (CSV par défaut). Si vous préférez une chaîne en mémoire, remplacez le dernier argument par un `StringWriter` et lisez le résultat ensuite.

### Exemple complet fonctionnel

Voici une application console autonome que vous pouvez coller dans un nouveau projet et exécuter immédiatement (remplacez simplement les chemins de fichiers).

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**Sortie attendue (extrait CSV) :**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

Chaque cellule de *A1* à *D10* est maintenant entourée de crochets carrés, exactement comme nous l'avons défini dans le gestionnaire `CellExport`.

## Gestion des cas limites courants  

### 1. Cellules vides  
Si une cellule est vide, `e.Value` sera `null`. Tenter de la formater avec l'interpolation de chaîne déclenche une exception. Protégez‑vous contre cela :

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. Grandes plages  
Exporter des millions de lignes peut atteindre les limites de mémoire. Dans ce scénario, diffusez la sortie au lieu de charger tout le classeur en mémoire :

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. Délimiteurs différents  
Le CSV n'est pas le seul format dont vous pourriez avoir besoin. Changez le délimiteur en ajustant `ExportTableOptions.CsvSeparator` :

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## Foire aux questions  

**Q : Cela fonctionne-t-il avec des fichiers .xlsx créés par Excel 365 ?**  
Absolument. GemBox lit le format OpenXML moderne sans configuration supplémentaire.

**Q : Puis‑je exporter plusieurs plages non contiguës en une fois ?**  
Pas directement via un seul appel `ExportTable`. Parcourez chaque chaîne de plage (`"A1:D10"`, `"F1:H5"` etc.) et concaténez les sorties vous‑même.

**Q : Et si je dois appliquer un formatage différent par colonne ?**  
Dans le gestionnaire `CellExport` vous avez accès à `e.ColumnIndex`. Utilisez une instruction `switch` pour appliquer une logique spécifique à chaque colonne.

## Conclusion  

Nous avons couvert **comment exporter une plage de feuille de calcul** avec un contrôle complet sur l'apparence de chaque cellule, démontré **comment exporter une plage Excel** à l'aide de `ExportTableOptions`, et montré **comment personnaliser l'exportation des cellules** via l'événement `CellExport`. La solution complète tient en quelques dizaines de lignes de C#, tout en étant suffisamment flexible pour des scénarios de production.

Prochaines étapes ? Remplacez l'encapsulation entre crochets par un format compatible JSON, ou expérimentez une logique conditionnelle qui ignore les lignes masquées. Vous pouvez également explorer l'exportation directe vers un `MemoryStream` pour les réponses d'API web—sans fichiers temporaires.

Si vous avez suivi le guide, vous disposez maintenant d'un modèle solide et réutilisable pour exporter n'importe quelle plage de feuille de calcul exactement comme vous le souhaitez. Bon codage, et n'hésitez pas à laisser un commentaire si vous rencontrez un problème !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}