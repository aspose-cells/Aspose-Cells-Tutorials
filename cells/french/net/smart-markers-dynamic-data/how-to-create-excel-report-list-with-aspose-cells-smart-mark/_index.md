---
category: general
date: 2026-09-08
description: Créez rapidement une liste de rapports Excel et exportez les commandes
  vers Excel en utilisant les smart markers d’Aspose.Cells. Suivez ce guide étape
  par étape pour une solution complète.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel report list
- export orders to excel
- aspose.cells smart markers
language: fr
lastmod: 2026-09-08
og_description: Créez une liste de rapports Excel en utilisant les smart markers d’Aspose.Cells.
  Ce guide vous montre comment exporter rapidement les commandes vers Excel, avec
  le code complet et les étapes du modèle.
og_image_alt: Generated Excel report list preview created with Aspose.Cells smart
  markers
og_title: Créer une liste de rapports Excel avec les marqueurs intelligents d'Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Create excel report list quickly and export orders to excel using Aspose.Cells
    smart markers. Follow this step‑by‑step guide for a complete solution.
  headline: How to create excel report list with Aspose.Cells smart markers
  type: TechArticle
- description: Create excel report list quickly and export orders to excel using Aspose.Cells
    smart markers. Follow this step‑by‑step guide for a complete solution.
  name: How to create excel report list with Aspose.Cells smart markers
  steps:
  - name: Define the data models for orders and items
    text: You need plain‑old C# classes that represent the hierarchy you want to print.
      The `Order` class holds an identifier and a collection of `Item` objects; each
      `Item` stores a name and a price.
  - name: Build sample nested data
    text: Create a collection of `Order` objects that mimics real‑world data. The
      example includes two orders, one of which contains two items and the other a
      single item.
  - name: Prepare the Excel template with smart markers
    text: 'Open **SmartMarkerTemplate.xlsx** in Excel and place the following markers
      in the first worksheet:'
  - name: Process smart markers to export orders to excel
    text: Load the workbook, invoke the `SmartMarkersProcessor`, and bind the `orderList`
      to the `Orders` placeholder. This single call populates the entire report list.
  - name: Save the populated workbook
    text: Finally, write the result to a new file. The output file contains a fully
      populated **excel report list** that you can open in any spreadsheet application.
  type: HowTo
tags:
- Aspose.Cells
- Excel automation
- C#
title: Comment créer une liste de rapports Excel avec les marqueurs intelligents d’Aspose.Cells
url: /fr/net/smart-markers-dynamic-data/how-to-create-excel-report-list-with-aspose-cells-smart-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer une liste de rapports Excel avec les smart markers d'Aspose.Cells

Si vous devez **créer une liste de rapports Excel** à partir de données de commandes imbriquées, ce tutoriel vous fournit une solution prête à l'emploi. Vous verrez comment **exporter des commandes vers Excel** en utilisant les smart markers d'Aspose.Cells, de sorte que le processus complet se termine par un seul appel de méthode.

Générer une liste de rapports structurée implique souvent de parcourir des collections et d'écrire les cellules manuellement. Les smart markers éliminent ce code répétitif, vous permettant de vous concentrer sur le modèle de données plutôt que sur les coordonnées des cellules. À la fin de ce guide, vous disposerez d'un modèle réutilisable pour toute sortie Excel centrée sur les commandes.

## Prérequis

* .NET 6.0 ou version ultérieure installé  
* Aspose.Cells for .NET (package NuGet `Aspose.Cells`)  
* Visual Studio 2022 ou tout éditeur C# de votre choix  
* Un fichier de modèle Excel nommé **SmartMarkerTemplate.xlsx** contenant la syntaxe des smart markers (expliquée à l'étape suivante)

Tous les outils sont gratuits à télécharger, et le code s'exécute sous Windows, macOS et Linux avec .NET Core.

## Comment créer une liste de rapports Excel avec les smart markers d'Aspose.Cells

Les sections suivantes parcourent chaque partie de la solution. Les blocs de code sont complets et peuvent être copiés dans un nouveau projet console sans modification.

### Étape 1 : Définir les modèles de données pour les commandes et les articles

Vous avez besoin de simples classes C# qui représentent la hiérarchie que vous souhaitez imprimer. La classe `Order` contient un identifiant et une collection d'objets `Item` ; chaque `Item` stocke un nom et un prix.

```csharp
using System.Collections.Generic;

// Order represents a purchase transaction
class Order
{
    public string Id { get; set; }
    public List<Item> Items { get; set; }
}

// Item represents a single product line in an order
class Item
{
    public string Name { get; set; }
    public double Price { get; set; }
}
```

Ces modèles sont intentionnellement simples car les smart markers peuvent parcourir automatiquement n'importe quelle profondeur d'imbrication. Le type `List<T>` permet au processeur de répéter les lignes pour chaque élément de la collection.

### Étape 2 : Construire des données imbriquées d'exemple

Créez une collection d'objets `Order` qui imite des données réelles. L'exemple comprend deux commandes, dont l'une contient deux articles et l'autre un seul article.

```csharp
// Build a list of orders with nested items
var orderList = new List<Order>
{
    new Order
    {
        Id = "O001",
        Items = new List<Item>
        {
            new Item { Name = "Pen",   Price = 1.2 },
            new Item { Name = "Paper", Price = 2.5 }
        }
    },
    new Order
    {
        Id = "O002",
        Items = new List<Item>
        {
            new Item { Name = "Ruler", Price = 0.8 }
        }
    }
};
```

Vous pouvez remplacer cette liste codée en dur par des données récupérées depuis une base de données, une API ou toute autre source. Le processeur de smart markers traite le graphe d'objets exactement de la même manière.

### Étape 3 : Préparer le modèle Excel avec les smart markers

Ouvrez **SmartMarkerTemplate.xlsx** dans Excel et placez les marqueurs suivants dans la première feuille de calcul :

| Cell | Content |
|------|---------|
| A1   | ID de la commande : **${Orders.Id}** |
| A3   | Nom de l'article | Prix de l'article |
| A4   | **${Orders.Items.Name}** | **${Orders.Items.Price}** |

* `${Orders}` indique à Aspose.Cells d'itérer sur la collection `Orders`.  
* `${Orders.Items}` itère sur chaque `Item` appartenant à la commande courante.  

Lorsque le processeur s'exécute, il développe les lignes sous les marqueurs, remplissant les valeurs à partir des objets fournis.

> **Astuce :** Gardez les lignes de marqueurs ensemble et évitez de fusionner les cellules autour d'elles ; la fusion peut interrompre la logique d'expansion.

### Étape 4 : Traiter les smart markers pour exporter les commandes vers Excel

Chargez le classeur, invoquez le `SmartMarkersProcessor`, et liez le `orderList` à l'espace réservé `Orders`. Cet appel unique remplit toute la liste de rapports.

```csharp
using Aspose.Cells;

// Load the template workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

// Bind the data and process all markers in the first worksheet
workbook.Worksheets[0].SmartMarkersProcessor.Process(new
{
    Orders = orderList          // <-- name matches the ${Orders} marker
});
```

Le processeur parcourt le graphe d'objets, répète les lignes pour chaque commande, puis répète les lignes internes pour chaque article. Comme le modèle de données correspond à la hiérarchie des marqueurs, aucune configuration supplémentaire n'est requise.

### Étape 5 : Enregistrer le classeur rempli

Enfin, écrivez le résultat dans un nouveau fichier. Le fichier de sortie contient une **liste de rapports Excel** entièrement remplie que vous pouvez ouvrir dans n'importe quelle application de tableur.

```csharp
// Save the generated report
workbook.Save("YOUR_DIRECTORY/SmartMarkerResult.xlsx");
```

Ouvrez `SmartMarkerResult.xlsx` et vous verrez un tableau similaire à :

```
Order ID: O001
Item Name   Item Price
Pen         1.2
Paper       2.5

Order ID: O002
Item Name   Item Price
Ruler       0.8
```

La liste de rapports est prête pour la distribution, une analyse supplémentaire ou l'archivage.

## Code source complet

En réunissant tous les éléments, le programme console complet ressemble à ceci :

```csharp
using Aspose.Cells;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Define data models
        // (see Step 1 for class definitions)

        // 2️⃣ Create sample data
        var orderList = new List<Order>
        {
            new Order
            {
                Id = "O001",
                Items = new List<Item>
                {
                    new Item { Name = "Pen",   Price = 1.2 },
                    new Item { Name = "Paper", Price = 2.5 }
                }
            },
            new Order
            {
                Id = "O002",
                Items = new List<Item>
                {
                    new Item { Name = "Ruler", Price = 0.8 }
                }
            }
        };

        // 3️⃣ Load template containing smart markers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

        // 4️⃣ Process smart markers – this is where we **export orders to excel**
        workbook.Worksheets[0].SmartMarkersProcessor.Process(new
        {
            Orders = orderList
        });

        // 5️⃣ Save the populated workbook – the **excel report list** is ready
        workbook.Save("YOUR_DIRECTORY/SmartMarkerResult.xlsx");
    }
}

// Data model definitions (Step 1)
class Order
{
    public string Id { get; set; }
    public List<Item> Items { get; set; }
}
class Item
{
    public string Name { get; set; }
    public double Price { get; set; }
}
```

Copiez ce fichier dans un nouveau projet console, remplacez `YOUR_DIRECTORY` par le chemin réel de votre modèle, puis exécutez le programme. Le `SmartMarkerResult.xlsx` généré apparaîtra dans le même dossier.

## Pièges courants et conseils pratiques

| Problème | Pourquoi cela se produit | Comment l'éviter |
|----------|--------------------------|------------------|
| Les marqueurs sont placés dans des cellules fusionnées | Aspose.Cells développe les lignes mais ne peut pas séparer les plages fusionnées | Gardez les lignes de marqueurs non fusionnées |
| Les noms de propriétés des données diffèrent des marqueurs | Le processeur fait correspondre les noms de façon sensible à la casse | Assurez-vous que `${Orders.Id}` correspond exactement à la propriété `Id` |
| Le chemin du modèle est incorrect | Le constructeur `Workbook` lève `FileNotFoundException` | Utilisez des chemins absolus ou intégrez le modèle comme ressource |
| Les grands ensembles de données provoquent une pression mémoire | Les smart markers chargent le classeur complet en mémoire | Diffusez le modèle avec `LoadOptions` et libérez les objets rapidement |

Aborder ces points vous fait gagner du temps lorsque vous mettez à l'échelle la logique **d'exportation des commandes vers Excel** pour des milliers de lignes.

## Conclusion

Vous savez maintenant comment **créer une liste de rapports Excel** en utilisant les smart markers d'Aspose.Cells et comment **exporter des commandes vers Excel** avec un code minimal. Cette approche sépare le modèle de la logique métier, ce qui facilite la maintenance et l'extension.  

Les étapes suivantes que vous pourriez explorer incluent :

* Ajouter des formules ou une mise en forme conditionnelle au modèle  
* Utiliser `SmartMarkerProcessor.ProcessDataSource` pour des sources de données autres que des objets anonymes  
* Intégrer cette routine dans une API ASP.NET Core pour générer des rapports à la demande  

Expérimentez avec différentes dispositions de marqueurs, et vous maîtriserez rapidement l'automatisation d'Excel avec Aspose.Cells.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Créer des objets de liste Excel avec Aspose.Cells .NET : Guide étape par étape](/cells/english/net/tables-structured-references/create-excel-list-objects-aspose-cells-net/)
- [Comment créer et styliser des tableaux Excel avec Aspose.Cells pour .NET | Guide étape par étape](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [Comment exporter les lignes Excel visibles avec Aspose.Cells pour .NET : Guide étape par étape](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}