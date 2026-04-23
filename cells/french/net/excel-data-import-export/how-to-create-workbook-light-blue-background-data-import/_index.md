---
category: general
date: 2026-02-09
description: Comment créer un classeur en C# avec un arrière‑plan bleu clair et importer
  des données avec des en‑têtes. Apprenez à ajouter un arrière‑plan bleu clair, à
  utiliser le style par défaut d’Excel et à importer un DataTable.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: fr
og_description: Comment créer un classeur en C# avec un arrière‑plan bleu clair, importer
  des données avec des en‑têtes et appliquer le style par défaut d’Excel — le tout
  dans un guide concis.
og_title: Comment créer un classeur – Fond bleu clair, importation de données
tags:
- C#
- Excel
- Aspose.Cells
title: Comment créer un classeur – Fond bleu clair, importation de données
url: /fr/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

Keep them.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer Workbook – Fond bleu clair, importation de données

Vous vous êtes déjà demandé **how to create workbook** en C# qui ait un aspect un peu plus joli dès le départ ? Peut-être avez‑vous extrait un `DataTable` d’une base de données et en avez‑vous assez des cellules blanches par défaut. Dans ce tutoriel, nous allons créer un nouveau workbook, ajouter un fond bleu clair à une colonne, et importer des données avec des en‑têtes — tout en utilisant le style par défaut fourni par Excel.

Nous ajouterons également quelques scénarios « what‑if », comme la gestion des valeurs nulles ou la personnalisation de plusieurs colonnes. À la fin, vous disposerez d’un fichier Excel entièrement stylisé que vous pourrez envoyer aux parties prenantes sans aucun post‑traitement.

## Prérequis

* **.NET 6+** (le code fonctionne également sur .NET Framework 4.6+)  
* **Aspose.Cells for .NET** – la bibliothèque qui alimente les appels `Workbook`, `Style` et `ImportDataTable`. Installez‑la via NuGet :  

  ```bash
  dotnet add package Aspose.Cells
  ```

* Une source `DataTable` – nous en créerons une factice dans l’exemple, mais vous pouvez la remplacer par n’importe quelle requête ADO.NET.

Vous avez tout cela ? Super, commençons.

## Étape 1 : Initialiser un nouveau Workbook (Mot‑clé principal)

La première chose à faire est **how to create workbook** – littéralement. La classe `Workbook` représente le fichier Excel complet, et son constructeur vous fournit une page blanche.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Pourquoi c’est important :** Commencer avec un `Workbook` vierge vous assure de contrôler chaque style dès le départ. Si vous ouvrez un fichier existant, vous héritez des styles laissés par l’auteur original, ce qui peut entraîner un formatage incohérent.

## Étape 2 : Préparer le DataTable à importer

À des fins d’illustration, créons un `DataTable` simple. Dans des scénarios réels, vous appelleriez probablement une procédure stockée ou une méthode d’ORM.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Conseil :** Si vous devez conserver l’ordre des colonnes exactement tel qu’il apparaît dans la base de données, définissez le paramètre `importColumnNames` de `ImportDataTable` sur `true`. Cela indique à Aspose.Cells d’écrire les en‑têtes de colonnes pour vous.

## Étape 3 : Définir les styles de colonne – Par défaut + Fond bleu clair

Nous répondons maintenant à la partie **add light blue background** du problème. Aspose.Cells vous permet de fournir un tableau d’objets `Style` correspondant à chaque colonne que vous importez. La première entrée est le style pour la colonne 0, la deuxième pour la colonne 1, etc. Si vous avez moins de styles que de colonnes, les colonnes restantes utilisent le style par défaut.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Pourquoi seulement deux styles ?** Dans notre exemple nous avons quatre colonnes, mais nous voulons que seule la deuxième colonne (Name) se démarque. La longueur du tableau n’a pas besoin de correspondre au nombre de colonnes ; les entrées manquantes héritent automatiquement du style par défaut du workbook.

## Étape 4 : Importer le DataTable avec en‑têtes et styles

C’est ici que nous combinons **excel import datatable c#** et **import data with headers**. La méthode `ImportDataTable` fait le gros du travail : elle écrit les noms de colonnes, les lignes, et applique le tableau de styles que nous venons de créer.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Résultat attendu

Après l’exécution du programme, le `workbook` contiendra une seule feuille de calcul qui ressemble à ceci :

| **ID** | **Name** (bleu clair) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* La colonne **Name** possède un fond bleu clair, prouvant que le tableau de styles fonctionne.
* Les en‑têtes de colonnes sont générés automatiquement parce que nous avons passé `true` pour `importColumnNames`.
* Les valeurs nulles apparaissent comme des cellules vides, ce qui est le comportement par défaut d’Aspose.Cells.

## Étape 5 : Enregistrer le Workbook (Optionnel mais utile)

Vous voudrez probablement écrire le fichier sur le disque ou le diffuser à un client web. L’enregistrement est simple :

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Astuce pro :** Si vous ciblez d’anciennes versions d’Excel, remplacez `SaveFormat.Xlsx` par `SaveFormat.Xls`. L’API gère la conversion pour vous.

## Cas limites & variantes

### Plusieurs colonnes stylisées

Si vous avez besoin de plus d’une colonne stylisée, élargissez simplement le tableau `columnStyles` :

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Désormais, les colonnes **Name** et **Salary** seront en bleu clair.

### Mise en forme conditionnelle au lieu de styles fixes

Parfois, vous voulez qu’une colonne devienne rouge lorsqu’une valeur dépasse un seuil. C’est là que **use default style excel** rencontre la mise en forme conditionnelle :

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Importation sans en‑têtes

Si votre système en aval fournit déjà ses propres en‑têtes, passez simplement `false` pour l’argument `importColumnNames`. Les données commenceront à `A1` et vous pourrez écrire des en‑têtes personnalisées ensuite.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Exemple complet (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}