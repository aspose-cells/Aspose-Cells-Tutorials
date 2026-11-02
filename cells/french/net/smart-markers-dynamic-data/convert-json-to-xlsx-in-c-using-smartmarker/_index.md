---
category: general
date: 2026-10-10
description: Convertir JSON en XLSX en C# avec SmartMarker – apprenez comment importer
  du JSON dans Excel et remplir un classeur de façon programmatique.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert json to xlsx
- how to import json into excel
- populate excel from json
- create excel workbook c#
- import json into worksheet
language: fr
lastmod: 2026-10-10
og_description: Convertir JSON en XLSX en C# avec SmartMarker. Suivez ce guide pour
  importer du JSON dans Excel, créer un classeur Excel en C# et remplir Excel à partir
  du JSON.
og_image_alt: Diagram showing JSON data being converted to an XLSX workbook using
  C#
og_title: Convertir JSON en XLSX en C# – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  headline: Convert JSON to XLSX in C# using SmartMarker
  type: TechArticle
- description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  name: Convert JSON to XLSX in C# using SmartMarker
  steps:
  - name: '**Create an Excel workbook** in memory.'
    text: '**Create an Excel workbook** in memory.'
  - name: '**Load JSON data** that represents a simple list of people.'
    text: '**Load JSON data** that represents a simple list of people.'
  - name: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
    text: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
  - name: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
    text: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
  - name: '**Save the workbook** as an `.xlsx` file.'
    text: '**Save the workbook** as an `.xlsx` file.'
  type: HowTo
tags:
- JSON
- Excel
- C#
- Aspose.Cells
title: Convertir JSON en XLSX en C# avec SmartMarker
url: /fr/net/smart-markers-dynamic-data/convert-json-to-xlsx-in-c-using-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir JSON en XLSX en C# avec SmartMarker

Si vous devez **convertir JSON en XLSX en C#**, ce guide vous montre comment **importer JSON dans Excel** et **remplir Excel à partir de JSON** en quelques lignes de code seulement. Vous verrez comment **créer un classeur Excel C#**, configurer le processeur SmartMarker, puis **importer JSON dans les cellules de la feuille**.

> **Ce que vous obtiendrez** – un exemple complet et exécutable qui lit un tableau JSON, le traite comme un enregistrement unique, et écrit les données dans un fichier `.xlsx` prêt pour le reporting ou l’analyse en aval.

## Convertir JSON en XLSX – aperçu

SmartMarker fait partie de la bibliothèque Aspose.Cells et vous permet de lier JSON, XML ou tout objet .NET directement à un modèle Excel. Dans ce tutoriel nous :

1. **Créons un classeur Excel** en mémoire.  
2. **Chargeons les données JSON** représentant une petite liste de personnes.  
3. **Configurons SmartMarker** pour traiter le tableau JSON comme un enregistrement unique (`ArrayAsSingle = true`).  
4. **Traitons la feuille**, laissant SmartMarker remplacer les marqueurs par les valeurs JSON.  
5. **Enregistrons le classeur** sous forme de fichier `.xlsx`.

Le flux complet s’exécute sur .NET 6+ et ne nécessite que le package NuGet `Aspose.Cells`.

## Étape 1 : Créer un classeur Excel en C#

Tout d’abord, ajoutez le package Aspose.Cells à votre projet :

```bash
dotnet add package Aspose.Cells
```

Vous pouvez maintenant instancier un nouveau `Workbook`. Le classeur démarre vide, mais vous pouvez ajouter une feuille de calcul et placer des balises SmartMarker là où les données JSON doivent apparaître.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToXlsxDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (this also creates the default first worksheet)
            Workbook workbook = new Workbook();

            // Optional: give the first sheet a friendly name
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Name = "People";
```

> **Pourquoi créer d’abord le classeur** – SmartMarker agit sur un objet `Worksheet` existant ; le classeur fournit le conteneur pour toutes les opérations suivantes.

## Étape 2 : Définir les données JSON et configurer SmartMarker

Nous utiliserons une petite charge JSON qui répertorie deux personnes. L’option `ArrayAsSingle` indique à SmartMarker de traiter l’ensemble du tableau comme un seul enregistrement logique, idéal pour obtenir un tableau simple sans boucles imbriquées.

```csharp
            // Step 2: Define the JSON data to populate the worksheet
            string jsonData = "[{'Name':'John','Age':30},{'Name':'Anna','Age':25}]";

            // Step 3: Initialise the SmartMarker processor
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // Important: treat the JSON array as a single record
            processor.Options.ArrayAsSingle = true;
```

> **Astuce :** Si vous omettez `ArrayAsSingle`, SmartMarker tenterait de créer un enregistrement distinct pour chaque élément du tableau, ce qui peut entraîner des lignes dupliquées ou une mise en page inattendue.

## Étape 3 : Insérer les balises SmartMarker dans la feuille

Les balises SmartMarker sont des espaces réservés en texte brut entourés de `&`. Placez‑les dans les cellules où vous voulez que les valeurs JSON apparaissent. Dans cet exemple nous écrivons les balises directement via le code, mais vous pouvez également concevoir un modèle dans Excel au préalable.

```csharp
            // Step 4: Write SmartMarker tags into the first row (header) and second row (data)
            sheet.Cells["A1"].PutValue("Name");                // Header
            sheet.Cells["B1"].PutValue("Age");                 // Header
            sheet.Cells["A2"].PutValue("&=Name&");             // Data placeholder
            sheet.Cells["B2"].PutValue("&=Age&");              // Data placeholder
```

> **Explication :** `&=Name&` indique à SmartMarker de remplacer la cellule par le champ `Name` de l’objet JSON, tandis que `&=Age&` fait de même pour `Age`.

## Étape 4 : Traiter la feuille – remplir Excel à partir de JSON

Laissez maintenant SmartMarker lire la chaîne JSON et remplir les espaces réservés.

```csharp
            // Step 5: Apply the JSON data to the worksheet
            processor.Process(sheet, jsonData);
```

En arrière‑plan, SmartMarker analyse `jsonData`, associe chaque propriété d’objet à la balise correspondante, et développe automatiquement les lignes parce que `ArrayAsSingle` est à `true`. Après le traitement, la feuille ressemble à ceci :

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 25  |

## Étape 5 : Enregistrer le fichier XLSX

Enfin, écrivez le classeur rempli sur le disque.

```csharp
            // Step 6: Save the populated workbook as an .xlsx file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "SmartMarkerJson.xlsx");

            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

L’exécution du programme crée `SmartMarkerJson.xlsx` sur votre bureau. L’ouverture du fichier dans Excel montre un tableau propre avec les données JSON correctement importées.

## Pièges courants lors de l’importation de JSON dans une feuille

| Problème | Pourquoi cela se produit | Comment l’éviter |
|----------|--------------------------|------------------|
| **Balises SmartMarker manquantes** | SmartMarker ne remplace que les cellules contenant `&=...&`. | Vérifiez l’orthographe exacte et la casse des balises. |
| **Format JSON incorrect** | Les apostrophes simples (`'`) ne sont pas du JSON valide pour le parseur intégré. | Utilisez des guillemets doubles (`"`) ou laissez Aspose.Cells gérer le format souple comme indiqué. |
| **Tableau traité comme plusieurs enregistrements** | La valeur par défaut de `ArrayAsSingle` est `false`. | Définissez `processor.Options.ArrayAsSingle = true` lorsque vous voulez un tableau plat. |
| **Enregistrement dans un dossier en lecture‑seule** | `workbook.Save` lève une exception. | Choisissez un répertoire accessible en écriture (ex. : Bureau ou un dossier temporaire). |

## Étendre la solution

- **Plusieurs feuilles** : créez des feuilles supplémentaires et appelez `processor.Process` sur chacune avec des sources JSON différentes.  
- **Mise en forme** : après le traitement, appliquez des styles de cellule (polices, bordures) comme pour toute opération Aspose.Cells classique.  
- **Jeux de données volumineux** : pour des milliers de lignes, envisagez le streaming du classeur afin de réduire la consommation mémoire (`WorkbookDesigner` ou `SaveOptions` avec `EnableMemoryOptimization`).

## Conclusion

Vous savez maintenant comment **convertir JSON en XLSX en C#** en utilisant SmartMarker d’Aspose.Cells. Le flux complet—**créer un classeur Excel C#**, ajouter des balises SmartMarker, configurer le processeur, **remplir Excel à partir de JSON**, puis enregistrer le fichier—vous permet **d’importer JSON dans les cellules d’une feuille** avec un minimum de code.

N’hésitez pas à expérimenter avec des structures JSON plus complexes, à ajouter des formules, ou à générer des graphiques directement à partir des données remplissées. Si ce guide vous a plu, essayez le prochain tutoriel sur **comment importer JSON dans Excel** pour la création de graphiques ou sur **créer un classeur Excel C#** avec une mise en forme avancée.

---


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Convertir JSON en Excel avec C# – Guide étape par étape](/cells/english/net/smart-markers-dynamic-data/convert-json-to-excel-with-c-step-by-step-guide/)
- [Comment insérer JSON dans un modèle Excel – Étape par étape](/cells/english/net/data-loading-and-parsing/how-to-insert-json-into-excel-template-step-by-step/)
- [Créer un classeur Excel C# – Insérer JSON et enregistrer en XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}