---
category: general
date: 2026-11-16
description: Créer un fichier Excel à partir de JSON avec SmartMarker. Apprenez comment
  convertir du JSON en Excel, intégrer du JSON dans Excel et enregistrer le classeur
  au format xlsx en quelques minutes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- convert json to excel
- embed json in excel
- save workbook xlsx
language: fr
lastmod: 2026-11-16
og_description: Créez rapidement un fichier Excel à partir de JSON. Ce tutoriel montre
  comment convertir du JSON en Excel, intégrer du JSON dans Excel et enregistrer le
  classeur au format xlsx avec Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet showing JSON data inserted into a single
  cell
og_title: Créer un Excel à partir de JSON avec SmartMarker – guide C# étape par étape
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  headline: Create Excel from JSON with SmartMarker in C#
  type: TechArticle
- description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  name: Create Excel from JSON with SmartMarker in C#
  steps:
  - name: Build and run the console app (`dotnet run`).
    text: Build and run the console app (`dotnet run`).
  - name: Verify the console prints the full path to the generated file.
    text: Verify the console prints the full path to the generated file.
  - name: Open the file in Excel or any spreadsheet viewer.
    text: Open the file in Excel or any spreadsheet viewer.
  - name: Confirm that cell A1 holds the JSON array string exactly as shown above.
    text: Confirm that cell A1 holds the JSON array string exactly as shown above.
  type: HowTo
tags:
- SmartMarker
- Aspose.Cells
- C#
- JSON
title: Créer un fichier Excel à partir de JSON avec SmartMarker en C#
url: /fr/net/smart-markers-dynamic-data/create-excel-from-json-with-smartmarker-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un fichier Excel à partir de JSON avec SmartMarker en C#

Si vous devez **créer un Excel à partir de JSON** dans un projet .NET, ce guide présente une solution complète et exécutable. En utilisant le processeur Smart Marker d’Aspose.Cells, vous pouvez **convertir du JSON en Excel**, insérer la chaîne JSON directement dans une cellule et **enregistrer le classeur au format xlsx** sans écrire de code de parsing manuel.

Vous verrez comment enregistrer une source de données JSON, insérer un Smart Marker qui restitue tout le tableau sous forme d’une seule chaîne JSON, traiter la feuille de calcul, puis écrire le fichier sur le disque. À la fin du tutoriel, vous pourrez générer un fichier Excel contenant la charge JSON d’origine dans la cellule A1, prêt pour un traitement en aval ou pour des rapports.

## Prérequis

- .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework 4.7+)
- Aspose.Cells for .NET (package NuGet `Aspose.Cells`)
- Connaissances de base en C# et en format JSON
- Un IDE tel que Visual Studio ou VS Code

## Étape 1 : Configurer le projet et importer les espaces de noms

Créez une nouvelle application console et ajoutez le package Aspose.Cells :

```bash
dotnet new console -n JsonToExcelDemo
cd JsonToExcelDemo
dotnet add package Aspose.Cells
```

Puis incluez les espaces de noms requis en haut de `Program.cs` :

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
```

**Pourquoi ?**  
`Aspose.Cells` fournit le modèle de classe du classeur, tandis que `Aspose.Cells.SmartMarkers` contient la classe `SmartMarkerProcessor` qui interprète les marqueurs `&=` dans la feuille de calcul.

## Étape 2 : Définir la source de données JSON

Placez la chaîne JSON dans une variable. Dans cet exemple, nous avons un tableau de commandes :

```csharp
// Step 2: Define the JSON data source
string json = @"{
    ""Orders"": [
        { ""Id"": 1, ""Amount"": 100 },
        { ""Id"": 2, ""Amount"": 150 }
    ]
}";
```

**Pourquoi ?**  
Smart Marker fonctionne avec n’importe quel JSON bien formé. Conserver le JSON sous forme de chaîne vous permet de l’enregistrer directement sans avoir besoin d’un fichier sur le disque.

## Étape 3 : Enregistrer les données JSON avec SmartMarkerProcessor

Créez une instance de `SmartMarkerProcessor` et associez la chaîne JSON à un nom que vous référencerez plus tard dans la feuille de calcul :

```csharp
// Step 3: Register the JSON data with the Smart Marker processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.RegisterJsonDataSource("OrdersJson", json);
```

**Pourquoi ?**  
`RegisterJsonDataSource` analyse le JSON et rend sa hiérarchie disponible aux Smart Markers. Le nom `"OrdersJson"` devient l’objet racine dans les expressions de marqueur.

## Étape 4 : Créer un classeur et insérer le Smart Marker

Instanciez un nouveau classeur, récupérez sa première feuille de calcul, et écrivez un Smart Marker dans la cellule A1 qui affichera l’ensemble du tableau `Orders` sous forme d’une seule chaîne JSON :

```csharp
// Step 4: Create a workbook and get the first worksheet
Worksheet ws = new Workbook().Worksheets[0];

// Insert a Smart Marker that outputs the whole array as a single JSON string
ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");
```

**Pourquoi ?**  
L’expression `OrdersJson.Orders.ArrayAsSingle` indique à Smart Marker de prendre le tableau `Orders`, de le sérialiser à nouveau en JSON et de placer le résultat dans la cellule cible. C’est la façon la plus directe **d’intégrer du JSON dans Excel**.

## Étape 5 : Traiter la feuille de calcul

Exécutez le processeur afin qu’il remplace le marqueur par la vraie chaîne JSON :

```csharp
// Step 5: Process the worksheet – the marker is replaced with the JSON array string
processor.Process(ws);
```

**Pourquoi ?**  
Le traitement examine chaque cellule à la recherche de marqueurs `&=`, les évalue par rapport aux sources de données enregistrées, puis écrit la valeur évaluée dans la feuille de calcul.

## Étape 6 : Enregistrer le classeur au format .xlsx

Enfin, écrivez le classeur sur le disque. Ajustez le chemin vers un dossier où vous avez les droits d’écriture :

```csharp
// Step 6: Save the workbook
string outputPath = Path.Combine(
    Environment.CurrentDirectory,
    "JsonArraySingleCell.xlsx");

ws.Workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

**Pourquoi ?**  
`SaveFormat.Xlsx` garantit que le fichier est stocké au format moderne Office Open XML, répondant ainsi à l’exigence **save workbook xlsx**.

## Code source complet

En assemblant toutes les pièces, voici le programme complet, prêt à être exécuté :

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // Step 2: Define the JSON data source
        string json = @"{
            ""Orders"": [
                { ""Id"": 1, ""Amount"": 100 },
                { ""Id"": 2, ""Amount"": 150 }
            ]
        }";

        // Step 3: Register the JSON data with the Smart Marker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.RegisterJsonDataSource("OrdersJson", json);

        // Step 4: Create a workbook and get the first worksheet
        Worksheet ws = new Workbook().Worksheets[0];

        // Insert a Smart Marker that will output the whole array as a single JSON string
        ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");

        // Step 5: Process the worksheet – the marker is replaced with the JSON array string
        processor.Process(ws);

        // Step 6: Save the workbook
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "JsonArraySingleCell.xlsx");
        ws.Workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Résultat attendu dans Excel

Ouvrez `JsonArraySingleCell.xlsx`. La cellule A1 contiendra :

```
[{"Id":1,"Amount":100},{"Id":2,"Amount":150}]
```

La chaîne JSON est une représentation compacte du tableau `Orders` d’origine, ce qui facilite son transport ou sa consommation dans des flux de travail basés sur Excel.

## Variantes courantes et cas limites

| Situation | Ajustement |
|-----------|------------|
| **Plusieurs objets JSON** | Enregistrez chaque objet avec un nom distinct (par ex., `processor.RegisterJsonDataSource("CustomerJson", customerJson);`) et référez‑vous à eux avec des marqueurs séparés. |
| **JSON formaté (pretty‑printed) dans une cellule** | Utilisez l’option `ArrayAsSinglePretty` : `ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSinglePretty");` |
| **Charges JSON volumineuses** | Envisagez d’écrire le JSON dans une feuille cachée ou d’utiliser la conversion `DataTable` pour de meilleures performances. |
| **Intégration du JSON dans plusieurs cellules** | Placez différents marqueurs dans d’autres cellules, par ex., `&=OrdersJson.Orders[0].Id` pour extraire des champs individuels. |

**Astuce :** Lors du traitement de JSON très volumineux, augmentez le tampon mémoire du classeur (`WorkbookSettings.MemorySetting`) afin d’éviter les `OutOfMemoryException`.

## Tester la solution

1. Compilez et exécutez l’application console (`dotnet run`).  
2. Vérifiez que la console affiche le chemin complet du fichier généré.  
3. Ouvrez le fichier dans Excel ou tout autre visualiseur de feuilles de calcul.  
4. Confirmez que la cellule A1 contient exactement la chaîne JSON du tableau comme indiqué ci‑dessus.

Si la cellule contient le texte du marqueur (`&=OrdersJson...`) au lieu du JSON, revérifiez que le processeur a bien été invoqué **après** l’insertion du marqueur et que la chaîne JSON est valide.

## Conclusion

Vous savez maintenant comment **créer un Excel à partir de JSON** en utilisant les Smart Markers d’Aspose.Cells, comment **convertir du JSON en Excel**, intégrer directement la charge JSON dans une cellule, et **enregistrer le classeur au format xlsx** avec une seule ligne de code. Cette approche élimine le parsing manuel, fonctionne avec n’importe quelle structure JSON et produit un fichier Excel propre et conforme aux standards.

### Prochaines étapes

- Explorez les **boucles Smart Marker** (`&=OrdersJson.Orders`) pour générer une ligne par commande au lieu d’une seule chaîne JSON.  
- Combinez cette technique avec des **formules Excel** pour calculer des totaux à partir des données intégrées.  
- Examinez la **lecture du JSON depuis Excel** à l’aide de `Workbook.Load` et de `SmartMarkerProcessor` en sens inverse.

N’hésitez pas à expérimenter avec différentes formes de JSON, plusieurs feuilles de calcul, ou l’exportation vers d’autres formats tels que CSV ou PDF. Bon codage !

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos projets.

- [Create Excel from JSON with Aspose.Cells Smart Marker](/cells/english/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)
- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Save Excel Workbook from JSON – Complete Guide](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}