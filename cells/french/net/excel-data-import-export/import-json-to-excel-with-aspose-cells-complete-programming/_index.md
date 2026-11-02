---
category: general
date: 2026-06-21
description: Importez rapidement du JSON dans Excel et apprenez comment convertir
  du JSON en XLSX, générer un fichier Excel à partir de JSON et exporter du JSON vers
  une feuille de calcul en quelques étapes simples.
draft: false
keywords:
- import json to excel
- convert json to xlsx
- generate excel from json
- save json as excel
- export json to spreadsheet
language: fr
og_description: Importez JSON vers Excel sans effort. Ce guide vous montre comment
  convertir JSON en XLSX, générer Excel à partir de JSON et exporter JSON vers une
  feuille de calcul en utilisant C#.
og_title: Importer JSON dans Excel avec Aspose.Cells – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  headline: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  type: TechArticle
- description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  name: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints:'
  - name: 1. Import Multiple JSON Arrays into Different Sheets
    text: 'If you have several arrays—say `"Employees"` and `"Departments"`—you can
      import each into its own worksheet:'
  - name: 2. Styling the Generated Table
    text: 'You can apply a style after the data expands:'
  - name: 3. Using a JSON File Instead of a String
    text: 'If your JSON lives on disk, just read it first:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Importer JSON vers Excel avec Aspose.Cells – Guide complet de programmation
url: /fr/net/excel-data-import-export/import-json-to-excel-with-aspose-cells-complete-programming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Import JSON to Excel – Guide complet de programmation

Vous êtes-vous déjà demandé **comment importer du JSON dans Excel** sans écrire un analyseur personnalisé ? Vous n'êtes pas seul. De nombreux développeurs se retrouvent bloqués lorsqu'ils doivent transformer une charge JSON en une feuille de calcul propre pour le reporting ou l'analyse de données. La bonne nouvelle ? Avec Aspose.Cells, vous pouvez **convertir du JSON en XLSX** en quelques lignes seulement, et le processus est à la fois rapide et sûr au niveau du typage.

Dans ce tutoriel, nous passerons en revue chaque étape nécessaire pour **générer Excel à partir de JSON**, enregistrer le résultat sous forme de fichier `.xlsx`, et même explorer quelques variantes pratiques — comme exporter du JSON vers une feuille qui se met à jour automatiquement lorsque vous modifiez les données sources. À la fin, vous disposerez d’un extrait réutilisable que vous pourrez intégrer à n’importe quel projet .NET.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- .NET 6.0 ou supérieur (le code fonctionne également avec .NET Framework)
- Une licence valide d’Aspose.Cells for .NET ou une clé d’évaluation temporaire
- Visual Studio 2022 (ou tout autre IDE C# de votre choix)
- Une connaissance de base des structures JSON et de la syntaxe C#

Aucun package NuGet supplémentaire au‑delà d’**Aspose.Cells** n’est requis, ce qui rend l’installation légère.

## Étape 1 : Installer Aspose.Cells et configurer le projet

Première chose, ajoutez la bibliothèque Aspose.Cells à votre projet. Ouvrez la console du gestionnaire de packages et exécutez :

```powershell
Install-Package Aspose.Cells
```

Si vous utilisez le CLI .NET, l’équivalent est :

```bash
dotnet add package Aspose.Cells
```

> **Astuce :** Après l’installation, ajoutez votre fichier de licence (`Aspose.Cells.lic`) à la racine du projet et chargez‑le au démarrage :

```csharp
// Load the Aspose.Cells license (optional but removes evaluation watermark)
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Vous êtes maintenant prêt à **importer du JSON dans Excel**.

## Étape 2 : Préparer la charge JSON

Pour la démonstration, nous utiliserons un tableau simple d’objets personnes. Dans un scénario réel, vous pourriez lire cette chaîne depuis un fichier, une réponse d’API ou une base de données.

```csharp
// Step 2: Define the JSON data to be imported
string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";
```

Remarquez que le JSON est un tableau plat — exactement la forme qui fonctionne le mieux avec les smart markers d’Aspose.Cells.

## Étape 3 : Configurer les options de chargement JSON

Aspose.Cells vous permet de traiter l’ensemble du tableau JSON comme une *seule* source de données. C’est crucial lorsque vous voulez que les lignes s’étendent automatiquement dans la feuille de calcul.

```csharp
// Step 3: Configure JSON loading options to treat the whole array as a single data source
var loadOptions = new Aspose.Cells.JsonLoadOptions
{
    // When true, the whole array becomes one data source (e.g., "People")
    ArrayAsSingle = true
};
```

Définir `ArrayAsSingle = true` indique à la bibliothèque **de générer un smart marker qui se répète pour chaque élément** du tableau, ce qui constitue le cœur du workflow **convert JSON to XLSX**.

## Étape 4 : Créer le classeur et importer le JSON

Nous créons maintenant une nouvelle instance de `Workbook` et importons le JSON à l’aide d’un smart marker nommé `"People"`.

```csharp
// Step 4: Create a new workbook and import the JSON using a smart marker named "People"
var workbook = new Aspose.Cells.Workbook();
workbook.ImportJson(json, loadOptions, new Aspose.Cells.SmartMarkerOptions
{
    DataSourceName = "People"
});
```

En coulisses, Aspose.Cells analyse le JSON, associe chaque propriété (`Name`, `Age`) à une colonne, et prépare un espace réservé qui sera ensuite développé en lignes.

## Étape 5 : Placer le smart marker dans la feuille

Un smart marker ressemble à `{{People}}`. Lors de l’enregistrement du classeur, Aspose.Cells remplace ce marqueur par un tableau contenant toutes les données du tableau JSON.

```csharp
// Step 5: Put the smart marker in cell A1 so the data expands when saved
workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");
```

Vous pouvez déplacer le marqueur où vous le souhaitez — le coin supérieur gauche est un choix fréquent car il laisse de la place au tableau pour croître vers le bas et vers la droite.

## Étape 6 : Enregistrer le classeur au format XLSX

Enfin, écrivez le classeur sur le disque. C’est ici que nous **enregistrons le JSON en Excel** et obtenons un véritable fichier `.xlsx` que vous pouvez ouvrir avec Excel, Google Sheets ou tout autre tableur.

```csharp
// Step 6: Save the workbook to a file (convert JSON to XLSX)
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
workbook.Save(outputPath, Aspose.Cells.SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Lorsque vous ouvrez `JsonSingleCell.xlsx`, vous verrez quelque chose comme :

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 28  |

C’est le résultat de **generate Excel from JSON** en action.

## Exemple complet fonctionnel

En rassemblant le tout, voici le programme complet, prêt à être exécuté :

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // Step 1: Define JSON data
        string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Step 2: Configure loading options
        var loadOptions = new JsonLoadOptions { ArrayAsSingle = true };

        // Step 3: Create workbook and import JSON
        var workbook = new Workbook();
        workbook.ImportJson(json, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });

        // Step 4: Insert smart marker
        workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");

        // Step 5: Save as XLSX (export JSON to spreadsheet)
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Excel file generated successfully at: {outputPath}");
    }
}
```

### Résultat attendu

L’exécution du programme affiche :

```
Excel file generated successfully at: C:\YourProject\JsonSingleCell.xlsx
```

L’ouverture du fichier montre un tableau à deux lignes avec les en‑têtes **Name** et **Age**, correspondant exactement au tableau JSON d’origine.

## Variantes avancées

### 1. Importer plusieurs tableaux JSON dans différentes feuilles

Si vous avez plusieurs tableaux—par exemple `"Employees"` et `"Departments"`—vous pouvez importer chacun dans sa propre feuille :

```csharp
// Load a more complex JSON with two arrays
string complexJson = @"
{
  ""Employees"": [{""Name"":""John"",""Age"":30}],
  ""Departments"": [{""Dept"":""HR"",""Count"":5}]
}";
var options = new JsonLoadOptions { ArrayAsSingle = false };
var wb = new Workbook();
wb.ImportJson(complexJson, options, new SmartMarkerOptions());

// Place markers
wb.Worksheets[0].Cells["A1"].PutValue("{{Employees}}");
wb.Worksheets.Add();
wb.Worksheets[1].Cells["A1"].PutValue("{{Departments}}");
wb.Save("MultipleSheets.xlsx");
```

Vous avez ainsi **exporté du JSON vers une feuille de calcul** avec plusieurs onglets, chacun reflétant un jeu de données distinct.

### 2. Appliquer un style au tableau généré

Vous pouvez appliquer un style après l’expansion des données :

```csharp
var table = workbook.Worksheets[0].Cells["A1"].GetSmartMarkerTable();
var style = workbook.CreateStyle();
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightBlue;
style.Pattern = BackgroundType.Solid;
table.ApplyStyle(style);
```

Cette petite astuce fait ressortir la ligne d’en‑tête, ce qui est pratique pour les tableaux de bord de reporting.

### 3. Utiliser un fichier JSON au lieu d’une chaîne

Si votre JSON se trouve sur le disque, lisez‑le simplement d’abord :

```csharp
string jsonFromFile = File.ReadAllText(@"C:\Data\people.json");
workbook.ImportJson(jsonFromFile, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });
```

Le reste des étapes reste exactement le même, vous pouvez donc **enregistrer le JSON en Excel** depuis n’importe quelle source.

## Pièges courants et comment les éviter

- **`ArrayAsSingle` manquant** – Oublier ce drapeau traitera chaque objet comme une source de données distincte, entraînant des cellules vides. Toujours le définir quand votre JSON est un tableau de niveau supérieur.
- **Nom de smart marker incorrect** – Le marqueur (`{{People}}`) doit correspondre au `DataSourceName` que vous avez passé (`"People"`). Une faute de frappe laissera le placeholder intact.
- **Licence non chargée** – En mode évaluation, le fichier de sortie comporte un filigrane. Chargez votre licence dès le départ pour obtenir un classeur propre.
- **Permissions du chemin de fichier** – Tenter d’enregistrer dans un dossier protégé lève une exception. Utilisez `Environment.CurrentDirectory` ou un chemin accessible en écriture.

## Tester le résultat par programme

Si vous souhaitez vérifier que l’export a réussi sans ouvrir Excel, vous pouvez relire la première cellule :

```csharp
var wbCheck = new Workbook("JsonSingleCell.xlsx");
string firstName = wbCheck.Worksheets[0].Cells["A2"].StringValue; // Should be "John"
Console.WriteLine($"First imported name: {firstName}");
```

Un rapide contrôle console comme celui‑ci confirme que **convert JSON to XLSX** a fonctionné comme prévu.

## Conclusion

Nous venons de couvrir tout ce qu’il faut pour **importer du JSON dans Excel** avec Aspose.Cells : de l’installation de la bibliothèque, à la préparation du JSON, la configuration des smart markers, jusqu’à **enregistrer le JSON en Excel**. Que vous ayez besoin de **convertir du JSON en XLSX**, **générer Excel à partir de JSON**, ou **exporter du JSON vers une feuille de calcul** pour l’analyse, le schéma reste le même — les smart markers font le gros du travail.

N’hésitez pas à expérimenter avec le style, plusieurs feuilles, ou même des mises à jour dynamiques en réimportant le JSON à l’exécution. L’étape logique suivante consiste à intégrer ce code dans une API web qui délivre des rapports Excel à la demande — remplacez simplement la ligne d’enregistrement par un flux renvoyé au client.

Des questions sur les cas particuliers, comme les objets JSON imbriqués ou les gros jeux de données ? Laissez un commentaire ci‑dessous, et bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants abordent des sujets étroitement liés qui prolongent les techniques présentées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos projets.

- [Importation efficace de JSON vers Excel avec Aspose.Cells pour Java : guide complet](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)
- [Importer des données JSON dans Excel avec Aspose.Cells Java : guide complet](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Importation sans effort de JSON dans Excel avec Aspose.Cells pour .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}