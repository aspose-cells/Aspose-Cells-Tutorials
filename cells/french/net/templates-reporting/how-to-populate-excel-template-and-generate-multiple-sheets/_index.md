---
category: general
date: 2026-11-22
description: remplir le modèle Excel à l’aide d’Aspose.Cells pour générer plusieurs
  feuilles, enregistrer le classeur Aspose, et créer un rapport maître‑détail en C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- populate excel template
- generate multiple sheets
- save aspose workbook
- generate master detail report
language: fr
lastmod: 2026-11-22
og_description: remplir un modèle Excel avec Aspose.Cells, générer plusieurs feuilles,
  enregistrer le classeur Aspose, et créer un rapport maître‑détail dans un seul programme
  C#.
og_image_alt: Screenshot showing a populated Excel workbook with multiple detail sheets
og_title: Remplir le modèle Excel et générer plusieurs feuilles avec Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: populate excel template using Aspose.Cells to generate multiple sheets,
    save aspose workbook, and create a master‑detail report in C#.
  headline: How to populate Excel template and generate multiple sheets with Aspose.Cells
  type: TechArticle
- description: populate excel template using Aspose.Cells to generate multiple sheets,
    save aspose workbook, and create a master‑detail report in C#.
  name: How to populate Excel template and generate multiple sheets with Aspose.Cells
  steps:
  - name: What the resulting workbook looks like
    text: '| Sheet name | Content | |------------|----------| | **Master** | Header
      row with order summary (OrderId, Customer) | | **Details_1** | All `OrderLines`
      where `OrderId = 1` (Pen, Notebook) | | **Details_2** | All `OrderLines` where
      `OrderId = 2` (Pencil) |'
  - name: Expected output
    text: 'Open `MasterDetailResult.xlsx` and you will see:'
  - name: Next steps
    text: '* Explore **SmartMarkerOptions** such as `EnableFormulaCalculation` to
      evaluate formulas after data insertion. * Add charts to the master sheet and
      let the processor update series ranges automatically. * Combine this approach
      with **Aspose.Slides** to export the same data to PowerPoint presentations'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment remplir un modèle Excel et générer plusieurs feuilles avec Aspose.Cells
url: /fr/net/templates-reporting/how-to-populate-excel-template-and-generate-multiple-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment remplir un modèle Excel et générer plusieurs feuilles avec Aspose.Cells

Si vous devez **remplir un modèle Excel** avec des données dynamiques, ce guide vous montre une solution complète, prête à l'exécution. En utilisant le moteur Smart Marker d'Aspose.Cells, vous pouvez **générer plusieurs feuilles**, enregistrer le **cahier de travail Aspose**, et produire un **rapport maître‑détail** complet sans copie manuelle ni macros VBA.

Le tutoriel parcourt chaque étape — de la préparation des collections maître‑détail à l'enregistrement du fichier final — afin que vous puissiez copier le code dans votre propre projet et voir les résultats immédiatement.

## Prérequis

* .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework 4.7+)
* Aspose.Cells for .NET installé (`dotnet add package Aspose.Cells`)
* Un environnement de développement C# de base (Visual Studio, VS Code, Rider, etc.)
* Un modèle Excel (`MasterDetailTemplate.xlsx`) contenant des balises Smart Marker telles que `&=Orders.OrderId` et une table de détail marquée avec `&=OrderLines`.

> **Astuce :** Conservez le modèle dans le même dossier que le projet ou utilisez un chemin absolu pour éviter `FileNotFoundException`.

## Vue d'ensemble de la solution

1. **Préparer les collections de données maître‑détail** – les objets source qui alimentent le rapport.  
2. **Charger le modèle Excel** qui contient déjà des espaces réservés Smart Marker.  
3. **Créer un `SmartMarkerProcessor`** pour interpréter les marqueurs.  
4. **Appliquer les données** et laisser Aspose.Cells **générer plusieurs feuilles** automatiquement.  
5. **Enregistrer le cahier de travail Aspose** sur le disque.

Chaque étape est expliquée ci‑dessous, avec le code complet et le résultat attendu.

![populate excel template example](https://example.com/images/populate-excel-template.png "populate excel template example")

## Étape 1 : Préparer les collections de données maître‑détail

Les rapports maître‑détail reposent sur deux collections liées : une liste de commandes (maître) et une liste de lignes de commande (détail). Le moteur Smart Marker associe les lignes au champ `OrderId`.

```csharp
using System.Collections.Generic;

// Master collection – one record per order
var orders = new List<object>
{
    new { OrderId = 1, Customer = "Alice" },
    new { OrderId = 2, Customer = "Bob" }
};

// Detail collection – multiple rows per order
var orderLines = new List<object>
{
    new { OrderId = 1, Item = "Pen",      Qty = 10 },
    new { OrderId = 1, Item = "Notebook", Qty = 5  },
    new { OrderId = 2, Item = "Pencil",   Qty = 20 }
};
```

**Pourquoi c’est important :**  
Le `SmartMarkerProcessor` parcourt le modèle à la recherche de marqueurs tels que `&=Orders.OrderId` et `&=OrderLines.Item`. En fournissant deux collections distinctes, Aspose.Cells crée automatiquement une nouvelle feuille pour chaque enregistrement maître et remplit les lignes de détail en conséquence.

## Étape 2 : Charger le modèle Excel contenant des Smart Markers

Le modèle contient la mise en page, le formatage et les balises d'espace réservé. Conservez le nom de fichier et le chemin exacts.

```csharp
using Aspose.Cells;

// Adjust the path to where you stored the template
string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
Workbook workbook = new Workbook(templatePath);
```

**Pourquoi c’est important :**  
Le chargement du modèle fournit au processeur un objet workbook qui sait déjà où insérer les données. Tout le formatage (polices, bordures, formules) reste intact, de sorte que le rapport généré a l’air professionnel sans code de style supplémentaire.

## Étape 3 : Créer un SmartMarkerProcessor

Le processeur est le moteur qui remplace les marqueurs par les valeurs réelles.

```csharp
// Initialise the processor with the loaded workbook
var processor = new SmartMarkerProcessor(workbook);
```

**Pourquoi c’est important :**  
`SmartMarkerProcessor` isole la logique Smart Marker du reste du classeur, vous permettant de réutiliser le même classeur pour d’autres opérations (par ex., graphiques) après l’application des données.

## Étape 4 : Appliquer les données maître‑détail et générer plusieurs feuilles

Ici nous associons les deux collections au processeur et indiquons à Aspose.Cells comment nommer chaque feuille générée.

```csharp
using Aspose.Cells.SmartMarkers;

// Combine the collections into an anonymous object matching the marker names
var data = new { Orders = orders, OrderLines = orderLines };

// Options let you control sheet naming and other behaviours
var options = new SmartMarkerOptions
{
    // {0} will be replaced by the master record index (1‑based)
    DetailSheetNewName = "Details_{0}"
};

// Apply the data – this step creates a new sheet for each order
processor.ApplyTemplate(data, options);
```

**Pourquoi c’est important :**  
Le modèle `DetailSheetNewName` crée des feuilles nommées `Details_1`, `Details_2`, etc., correspondant à chaque commande de la collection maître. Cette génération automatique de feuilles est le cœur de **la génération de plusieurs feuilles** sans boucle manuelle sur le classeur.

### À quoi ressemble le classeur résultant

| Nom de la feuille | Contenu |
|-------------------|----------|
| **Master** | Ligne d’en‑tête avec le résumé de la commande (OrderId, Customer) |
| **Details_1** | Tous les `OrderLines` où `OrderId = 1` (Pen, Notebook) |
| **Details_2** | Tous les `OrderLines` où `OrderId = 2` (Pencil) |

La feuille maître peut également être remplie en ajoutant une table Smart Marker qui itère sur `Orders`. Les feuilles de détail sont créées automatiquement par le processeur.

## Étape 5 : Enregistrer le cahier de travail Aspose

Enfin, écrivez le classeur rempli dans un nouveau fichier.

```csharp
// Choose the output path – ensure the folder exists
string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
workbook.Save(resultPath);
```

**Pourquoi c’est important :**  
L’appel à `Save` écrit le classeur en mémoire dans un fichier `.xlsx` physique, complétant l’étape **enregistrer le cahier de travail Aspose**. Le fichier peut être ouvert dans Excel, Google Sheets ou tout visualiseur supportant le format OpenXML.

### Résultat attendu

Ouvrez `MasterDetailResult.xlsx` et vous verrez :

* **Feuille “Master”** – un tableau répertoriant Order 1 (Alice) et Order 2 (Bob).  
* **Feuille “Details_1”** – deux lignes : Pen (10) et Notebook (5).  
* **Feuille “Details_2”** – une ligne : Pencil (20).

Tout le formatage du modèle original (couleurs d’en‑tête, largeurs de colonnes, formats numériques) est conservé.

## Gestion des cas limites courants

| Situation | Approche recommandée |
|-----------|----------------------|
| **Template not found** | Enveloppez l’appel `new Workbook(...)` dans un `try/catch` et consignez `FileNotFoundException`. |
| **Large data sets (10 000+ rows)** | Augmentez `SmartMarkerOptions.MaxRowsPerSheet` si vous avez besoin de plus de lignes par feuille, ou paginez manuellement. |
| **Custom sheet naming** | Utilisez une chaîne de format comme `DetailSheetNewName = "Order_{0}_{1}"` où `{1}` peut être une propriété de l’enregistrement maître (par ex., `Customer`). |
| **Conditional formatting per order** | Ajoutez une règle de mise en forme conditionnelle au modèle qui référence un marqueur (par ex., `&=Orders.Status`) et laissez le processeur l’évaluer. |

## Programme complet exécutable

Ci‑dessous se trouve l’application console C# complète qui assemble tous les éléments. Remplacez `YOUR_DIRECTORY` par un chemin de dossier réel sur votre machine.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class SmartMarkerDetailSheetDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Prepare master‑detail data collections
        // -------------------------------------------------
        var orders = new List<object>
        {
            new { OrderId = 1, Customer = "Alice" },
            new { OrderId = 2, Customer = "Bob" }
        };

        var orderLines = new List<object>
        {
            new { OrderId = 1, Item = "Pen",      Qty = 10 },
            new { OrderId = 1, Item = "Notebook", Qty = 5  },
            new { OrderId = 2, Item = "Pencil",   Qty = 20 }
        };

        // -------------------------------------------------
        // Step 2: Load the template workbook that contains smart markers
        // -------------------------------------------------
        string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
        Workbook workbook = new Workbook(templatePath);

        // -------------------------------------------------
        // Step 3: Create a SmartMarkerProcessor to handle the template
        // -------------------------------------------------
        var processor = new SmartMarkerProcessor(workbook);

        // -------------------------------------------------
        // Step 4: Apply the master‑detail data and generate multiple sheets
        // -------------------------------------------------
        var data = new { Orders = orders, OrderLines = orderLines };
        var options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Details_{0}"
        };

        processor.ApplyTemplate(data, options);

        // -------------------------------------------------
        // Step 5: Save the populated Aspose workbook
        // -------------------------------------------------
        string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
        workbook.Save(resultPath);

        Console.WriteLine($"Report generated successfully: {resultPath}");
    }
}
```

Exécutez le programme (`dotnet run` ou `Ctrl+F5` dans Visual Studio). Lorsqu’il se termine, ouvrez `MasterDetailResult.xlsx` pour vérifier que **remplir le modèle Excel** a produit le rapport maître‑détail attendu avec **plusieurs feuilles**.

## Conclusion

Vous savez maintenant comment **remplir un modèle Excel** avec Aspose.Cells, **générer plusieurs feuilles**, **enregistrer le cahier de travail Aspose**, et créer un **rapport maître‑détail** robuste en quelques lignes de C#. Le moteur Smart Marker supprime le besoin de boucles manuelles, conserve votre formatage intact et s’adapte facilement à des ensembles de données plus volumineux.

### Prochaines étapes

* Explore **SmartMarkerOptions** telles que `EnableFormulaCalculation` pour évaluer les formules après l’insertion des données.  
* Ajoutez des graphiques à la feuille maître et laissez le processeur mettre à jour les plages de séries automatiquement.  
* Combinez cette approche avec **Aspose.Slides** pour exporter les mêmes données vers des présentations PowerPoint.

N’hésitez pas à expérimenter avec différents agencements de modèle, des schémas de nommage de feuilles personnalisés, ou des collections de détail supplémentaires. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code fonctionnels complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un rapport maître‑détail en C# – Remplir le modèle Excel avec SmartMarker](/cells/english/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/)
- [Comment générer Excel à partir d’un modèle avec C# et Aspose.Cells](/cells/english/net/templates-reporting/how-to-generate-excel-from-template-with-c-and-aspose-cells/)
- [Aspose Cells Smart Markers – Remplir le modèle Excel](/cells/english/java/templates-reporting/aspose-cells-smart-markers-populate-excel-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}