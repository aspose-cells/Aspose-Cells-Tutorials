---
category: general
date: 2026-08-07
description: Créer un fichier Excel à partir de JSON avec Aspose.Cells Smart Marker
  – apprenez comment remplir un modèle Excel, appliquer une dénomination dynamique
  des feuilles et générer plusieurs feuilles de calcul.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- populate excel template
- dynamic sheet naming
- generate multiple worksheets
- aspose.cells smart marker
language: fr
lastmod: 2026-08-07
og_description: Créez un fichier Excel à partir de JSON avec Aspose.Cells Smart Marker
  pour remplir rapidement les modèles, utilisez le nommage dynamique des feuilles
  et générez plusieurs feuilles de calcul.
og_image_alt: Screenshot of generated Excel workbook with multiple dynamically named
  sheets
og_title: Créer un fichier Excel à partir de JSON – Guide Smart Marker d’Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  headline: Create Excel from JSON with Aspose.Cells Smart Marker
  type: TechArticle
- description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  name: Create Excel from JSON with Aspose.Cells Smart Marker
  steps:
  - name: Define the JSON‑compatible source data
    text: '```csharp // Step 1: Define the source data that will be merged into the
      workbook var ordersData = new { Orders = new[] { new { Id = 1, Items = new[]
      { "Apple", "Banana" } }, new { Id = 2, Items = new[] { "Orange" } } } }; ```'
  - name: Prepare the workbook template and insert a Smart Marker
    text: '```csharp // Step 2: Create a new workbook and place a Smart Marker that
      references the data collection var workbook = new Workbook(); // creates an
      empty workbook workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}"); ```'
  - name: Configure dynamic sheet naming
    text: '```csharp // Step 3: Configure how duplicated detail sheets should be named
      during processing var smartMarkerOptions = new SmartMarkerOptions { // {0} will
      be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …) DetailSheetNewName
      = "DetailSheet_{0}" }; ```'
  - name: Process the template with the data and naming options
    text: '```csharp // Step 4: Process the workbook with the data and the naming
      options var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
      smartMarkerProcessor.Process(ordersData); ```'
  - name: Save the resulting workbook
    text: '```csharp // Step 5: Save the resulting workbook – the detail sheets are
      created automatically workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
      ```'
  - name: Populate Excel template with additional fields
    text: 'If your JSON includes more properties (e.g., `CustomerName`, `TotalAmount`),
      add corresponding markers to the template:'
  - name: Generate multiple worksheets from nested collections
    text: 'You can create a second level of duplication by placing a marker inside
      the detail sheet that references a nested collection, such as `Items`:'
  - name: Custom naming with data from the record
    text: '```csharp var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName
      = "Order_{Id}" }; ```'
  - name: Next steps
    text: '* Explore **conditional formatting** inside the detail sheet to highlight
      high‑value orders. * Replace the anonymous object with a strongly typed model
      deserialized via `System.Text.Json`. * Combine Smart Markers with **PivotTable**
      generation for advanced reporting.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Créer un Excel à partir de JSON avec le Smart Marker d'Aspose.Cells
url: /fr/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un Excel à partir de JSON avec Aspose.Cells Smart Marker

Si vous devez **créer un Excel à partir de JSON**, ce tutoriel présente une solution complète, prête pour la production. Vous verrez comment **remplir un modèle Excel**, configurer la **nomination dynamique des feuilles**, et **générer plusieurs feuilles de calcul** automatiquement avec le moteur **Aspose.Cells Smart Marker**.

Le guide vous accompagne à travers chaque étape requise, depuis la définition de l'objet source de type JSON jusqu'à l'enregistrement du classeur final. Aucun script externe n'est nécessaire, et le code s'exécute sur .NET 6 ou version ultérieure.

## Ce que vous allez réaliser

* Charger un objet de données de style JSON en mémoire.  
* Insérer un espace réservé Smart Marker dans un modèle de classeur.  
* Appliquer un modèle de nommage afin que chaque feuille de détail dupliquée reçoive un nom unique.  
* Traiter le modèle pour créer une feuille de calcul distincte pour chaque commande de la collection.  
* Enregistrer le résultat sous forme de fichier `.xlsx` prêt pour une consommation en aval.

Prérequis : Visual Studio 2022 (ou tout IDE C#), .NET 6+, et le package NuGet **Aspose.Cells**. L'exemple utilise C# ; les mêmes concepts s'appliquent à VB.NET ou à d'autres langages .NET.

## Créer un Excel à partir de JSON – flux de travail global

Les sections suivantes divisent le flux de travail en cinq étapes logiques. Chaque étape comprend le code exact dont vous avez besoin, une explication de son importance, et des astuces pour faire évoluer la solution.

### Étape 1 : Définir les données source compatibles JSON

```csharp
// Step 1: Define the source data that will be merged into the workbook
var ordersData = new
{
    Orders = new[]
    {
        new { Id = 1, Items = new[] { "Apple", "Banana" } },
        new { Id = 2, Items = new[] { "Orange" } }
    }
};
```

**Pourquoi c’est important** – L'objet `ordersData` reflète la structure que vous recevriez d’une vraie API JSON. Aspose.Cells Smart Marker lit les propriétés publiques, donc un type anonyme fonctionne tant que les noms de propriétés correspondent aux balises du marqueur (`{{Orders}}`). Lorsque vous remplacerez plus tard le type anonyme par un objet JSON désérialisé, aucune modification du code n’est nécessaire.

### Étape 2 : Préparer le modèle de classeur et insérer un Smart Marker

```csharp
// Step 2: Create a new workbook and place a Smart Marker that references the data collection
var workbook = new Workbook();                     // creates an empty workbook
workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");
```

**Pourquoi c’est important** – Le marqueur `{{Orders}}` indique au processeur d’itérer sur la collection `Orders`. Placer le marqueur dans la cellule `A1` de la première feuille fait de cette feuille la feuille *maître*. Le processeur dupliquera cette feuille pour chaque commande, en conservant tout formatage que vous ajouterez ultérieurement.

> **Astuce :** Si vous disposez d’un modèle pré‑conçu (par ex., avec des en‑têtes, des formules ou du style), chargez‑le avec `new Workbook("Template.xlsx")` au lieu de créer un classeur vierge.

### Étape 3 : Configurer la nomination dynamique des feuilles

```csharp
// Step 3: Configure how duplicated detail sheets should be named during processing
var smartMarkerOptions = new SmartMarkerOptions
{
    // {0} will be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …)
    DetailSheetNewName = "DetailSheet_{0}"
};
```

**Pourquoi c’est important** – Par défaut, Aspose.Cells nomme les feuilles dupliquées `Sheet1`, `Sheet2`, etc. Le modèle `DetailSheetNewName` insère un indice incrémental (`{0}`) afin que chaque feuille reçoive un nom significatif. Vous pouvez intégrer des espaces réservés supplémentaires (par ex., `{Id}`) pour inclure des données de l’enregistrement courant.

> **Conseil pro :** Utilisez `DetailSheetNewName = "Order_{Id}"` pour nommer les feuilles d’après l’identifiant de la commande, ce qui facilite la navigation dans de grands classeurs.

### Étape 4 : Traiter le modèle avec les données et les options de nomination

```csharp
// Step 4: Process the workbook with the data and the naming options
var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
smartMarkerProcessor.Process(ordersData);
```

**Pourquoi c’est important** – Le `SmartMarkerProcessor` fusionne les `ordersData` dans le classeur, crée une nouvelle feuille pour chaque élément de `Orders`, et applique le modèle de nommage défini précédemment. Le processeur développe également toute collection imbriquée (par ex., `Items`) si vous ajoutez des marqueurs supplémentaires à l’intérieur de la feuille de détail.

### Étape 5 : Enregistrer le classeur résultant

```csharp
// Step 5: Save the resulting workbook – the detail sheets are created automatically
workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
```

**Pourquoi c’est important** – La méthode `Save` écrit le classeur entièrement rempli sur le disque. Le fichier contient maintenant une feuille maître (qui peut être masquée ou supprimée) et une série de feuilles de détail nommées `DetailSheet_1`, `DetailSheet_2`, …, chacune contenant les données d’une seule commande.

#### Résultat attendu

| Nom de la feuille | Contenu (simplifié)                     |
|-------------------|------------------------------------------|
| DetailSheet_1     | Order Id = 1, Items: Apple, Banana       |
| DetailSheet_2     | Order Id = 2, Items: Orange              |

Toutes les feuilles conservent tout formatage que vous avez appliqué à la feuille maître avant le traitement.

## Variations avancées

### Remplir le modèle Excel avec des champs supplémentaires

Si votre JSON inclut davantage de propriétés (par ex., `CustomerName`, `TotalAmount`), ajoutez les marqueurs correspondants au modèle :

```csharp
workbook.Worksheets[0].Cells["B1"].PutValue("{{CustomerName}}");
workbook.Worksheets[0].Cells["C1"].PutValue("{{TotalAmount}}");
```

Le processeur remplacera chaque marqueur par la valeur de la propriété correspondante.

### Générer plusieurs feuilles de calcul à partir de collections imbriquées

Vous pouvez créer un deuxième niveau de duplication en plaçant un marqueur à l’intérieur de la feuille de détail qui fait référence à une collection imbriquée, comme `Items` :

```csharp
// Inside the detail sheet (e.g., cell A2)
workbook.Worksheets[0].Cells["A2"].PutValue("{{Items}}");

// Inside the same sheet, cell B2 will list each item
workbook.Worksheets[0].Cells["B2"].PutValue("{{Items}}");
```

Lors du traitement, Aspose.Cells crée une ligne pour chaque élément du tableau `Items`, vous permettant de générer des listes détaillées par commande.

### Nomination personnalisée avec les données de l’enregistrement

```csharp
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheetNewName = "Order_{Id}"
};
```

Les feuilles sont maintenant nommées `Order_1`, `Order_2`, ce qui aligne le nom de la feuille avec l’identifiant métier.

## Pièges courants et comment les éviter

| Piège                                                          | Solution |
|----------------------------------------------------------------|----------|
| Le texte du marqueur ne correspond pas au nom de la propriété (sensible à la casse) | Assurez‑vous que le marqueur (`{{Orders}}`) correspond exactement à la propriété, y compris la casse. |
| Le modèle contient des cellules fusionnées qui couvrent la zone du marqueur | Séparez les cellules fusionnées ou placez le marqueur dans une seule cellule non fusionnée pour éviter des changements de mise en page inattendus. |
| Les collections JSON volumineuses provoquent une pression mémoire | Traitez les données par lots ou diffusez le JSON dans un `DataTable` et utilisez `SmartMarkerProcessor` avec `DataSource`. |
| Le chemin du fichier enregistré est invalide | Utilisez `Path.Combine(Environment.CurrentDirectory, "output.xlsx")` ou vérifiez les permissions d’écriture. |

## Exemple complet fonctionnel

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1️⃣ Define JSON‑compatible data
        var ordersData = new
        {
            Orders = new[]
            {
                new { Id = 1, Items = new[] { "Apple", "Banana" } },
                new { Id = 2, Items = new[] { "Orange" } }
            }
        };

        // 2️⃣ Create workbook and add master Smart Marker
        var workbook = new Workbook();
        workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");

        // 3️⃣ Set up dynamic sheet naming
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "DetailSheet_{0}"
        };

        // 4️⃣ Process template with data
        var processor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
        processor.Process(ordersData);

        // 5️⃣ Save the result
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "SmartMarkerDupSheets.xlsx");
        workbook.Save(outputPath);
    }
}
```

L’exécution du programme génère un fichier Excel sur le bureau contenant deux feuilles de détail (`DetailSheet_1` et `DetailSheet_2`). Chaque feuille reflète l’enregistrement de commande correspondant.

## Conclusion

Vous savez maintenant comment **créer un Excel à partir de JSON** en utilisant **Aspose.Cells Smart Marker**, comment **remplir un modèle Excel**, appliquer la **nomination dynamique des feuilles**, et **générer automatiquement plusieurs feuilles de calcul**. Le même modèle s’étend à des dizaines ou des milliers d’enregistrements, prend en charge les collections imbriquées, et s’intègre parfaitement à n’importe quelle bibliothèque de désérialisation JSON .NET.

### Prochaines étapes

* Explorez la **mise en forme conditionnelle** dans la feuille de détail pour mettre en évidence les commandes de grande valeur.  
* Remplacez l’objet anonyme par un modèle fortement typé désérialisé via `System.Text.Json`.  
* Combinez les Smart Markers avec la génération de **Tableaux croisés dynamiques** pour des rapports avancés.  

Expérimentez avec le modèle de nommage, ajoutez plus de marqueurs, et intégrez ce flux de travail dans vos pipelines d’exportation de données existants. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Générer des rapports Excel dynamiques en utilisant Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Remplir Excel avec des données en utilisant Aspose.Cells et Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Comment créer et fusionner des classeurs Excel en utilisant Aspose.Cells pour Java | Guide complet](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}