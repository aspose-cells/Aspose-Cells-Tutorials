---
category: general
date: 2026-10-10
description: Générez un rapport Excel en fusionnant un modèle Excel à l'aide de Smart
  Markers — remplacez les smart tags et gérez efficacement les balises de la feuille
  de détail.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate Excel report
- merge Excel template
- detail sheet tag
- use smart markers
- replace smart tags
language: fr
lastmod: 2026-10-10
og_description: Générez un rapport Excel en utilisant les Smart Markers. Apprenez
  comment fusionner un modèle Excel, remplacer les balises intelligentes et travailler
  avec une balise de feuille de détail dans un exemple complet en C#.
og_image_alt: Generated Excel report after merging template with Smart Markers
og_title: Générer un rapport Excel en fusionnant un modèle Excel avec des Smart Markers
schemas:
- author: GroupDocs
  dateModified: '2026-10-10'
  description: Generate Excel report by merging an Excel template using Smart Markers—replace
    smart tags and handle detail sheet tag efficiently.
  headline: How to generate Excel report by merging an Excel template with Smart Markers
  type: TechArticle
- description: Generate Excel report by merging an Excel template using Smart Markers—replace
    smart tags and handle detail sheet tag efficiently.
  name: How to generate Excel report by merging an Excel template with Smart Markers
  steps:
  - name: '**Load the Excel template** – The template holds the layout, formulas,
      and styling. Smart Markers are placeholders like `${MasterSheet:Orders}` that
      the processor will replace.'
    text: '**Load the Excel template** – The template holds the layout, formulas,
      and styling. Smart Markers are placeholders like `${MasterSheet:Orders}` that
      the processor will replace.'
  - name: '**Prepare the data source** – `SmartMarkerProcessor` works with any enumerable
      collection. Here we use a list of `Order` objects that contain a nested list
      of `OrderDetail` objects, which is exactly what a master‑detail report needs.'
    text: '**Prepare the data source** – `SmartMarkerProcessor` works with any enumerable
      collection. Here we use a list of `Order` objects that contain a nested list
      of `OrderDetail` objects, which is exactly what a master‑detail report needs.'
  - name: '**Create the processor** – Instantiating `SmartMarkerProcessor` is cheap;
      you can reuse it for multiple worksheets if you need to generate several reports
      in one run.'
    text: '**Create the processor** – Instantiating `SmartMarkerProcessor` is cheap;
      you can reuse it for multiple worksheets if you need to generate several reports
      in one run.'
  - name: '**Process the worksheet** – This single call does three things:'
    text: '**Process the worksheet** – This single call does three things:'
  - name: '**Save the result** – The output file (`GeneratedReport.xlsx`) is a fully‑populated
      Excel report ready for distribution.'
    text: '**Save the result** – The output file (`GeneratedReport.xlsx`) is a fully‑populated
      Excel report ready for distribution.'
  - name: Creates a new worksheet for every master row.
    text: Creates a new worksheet for every master row.
  - name: Copies the formatting from the template’s detail area.
    text: Copies the formatting from the template’s detail area.
  - name: Inserts each item from the enumerable into consecutive rows.
    text: Inserts each item from the enumerable into consecutive rows.
  - name: A **master sheet** named *Sheet1* with two rows—one for each order. Columns
      display Order ID, Customer, Order Date, and Total.
    text: A **master sheet** named *Sheet1* with two rows—one for each order. Columns
      display Order ID, Customer, Order Date, and Total.
  - name: Two **detail sheets** named `OrderDetails_1001` and `OrderDetails_1002`.
      Each sheet lists the products, quantities, and unit prices for the corresponding
      order.
    text: Two **detail sheets** named `OrderDetails_1001` and `OrderDetails_1002`.
      Each sheet lists the products, quantities, and unit prices for the corresponding
      order.
  type: HowTo
tags:
- Excel
- C#
- SmartMarkers
title: Comment générer un rapport Excel en fusionnant un modèle Excel avec des Smart
  Markers
url: /fr/net/smart-markers-dynamic-data/how-to-generate-excel-report-by-merging-an-excel-template-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment générer un rapport Excel en fusionnant un modèle Excel avec des Smart Markers

Si vous devez **générer un rapport Excel** à partir d’un classeur réutilisable, les Smart Markers vous permettent de fusionner les données rapidement et de façon fiable. En adoptant une approche **fusion de modèle Excel**, vous séparez la mise en page de la logique métier, et le même modèle peut servir des dizaines de rapports.

Ce tutoriel vous montre comment définir une **étiquette de feuille de détail**, **utiliser les smart markers** pour remplir les données maître‑détail, et **remplacer les smart tags** dans le fichier final. Vous obtiendrez un programme C# complet et exécutable qui produit un rapport Excel au rendu professionnel en quelques secondes.

## Ce dont vous avez besoin

- .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework 4.7+)
- Visual Studio 2022 ou tout IDE C#
- Le package NuGet `GroupDocs.Viewer` / `Aspose.Cells` (ou toute bibliothèque qui fournit `SmartMarkerProcessor`)
- Un fichier modèle Excel (`ReportTemplate.xlsx`) contenant les balises Smart Marker décrites ci‑dessous

> **Astuce :** Conservez le modèle dans le dossier `Resources` du projet et définissez sa propriété *Copy to Output Directory* sur *Copy if newer* afin que le code puisse le localiser à l’exécution.

## Générer un rapport Excel : étape par étape avec les Smart Markers

Vous trouverez ci‑dessous le fichier source complet `Program.cs`. Chaque région est expliquée dans les sections suivantes.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Cells;               // SmartMarkerProcessor lives in this namespace
using Aspose.Cells.Tables;        // For master‑detail handling

namespace ExcelReportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the Excel template that contains Smart Marker tags
            string templatePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "ReportTemplate.xlsx");
            Workbook workbook = new Workbook(templatePath);
            Worksheet ws = workbook.Worksheets[0];   // assume the first sheet is the master sheet

            // 2️⃣ Prepare the data source – a list of orders, each with order lines
            List<Order> ordersData = GetSampleOrders();

            // 3️⃣ Create a SmartMarkerProcessor instance
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // 4️⃣ Process the worksheet, merging the template with the data source
            // This replaces all ${...} tags with real values and expands the detail sheet tag.
            processor.Process(ws, ordersData);

            // 5️⃣ Save the merged workbook as the final report
            string outputPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "GeneratedReport.xlsx");
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Report generated successfully: {outputPath}");
        }

        // Sample data generator – in a real project you would pull from a database or service
        private static List<Order> GetSampleOrders()
        {
            return new List<Order>
            {
                new Order
                {
                    OrderId = 1001,
                    Customer = "Acme Corp",
                    OrderDate = new DateTime(2024, 9, 15),
                    Total = 1250.75,
                    Details = new List<OrderDetail>
                    {
                        new OrderDetail { Product = "Widget A", Quantity = 10, UnitPrice = 25.00 },
                        new OrderDetail { Product = "Widget B", Quantity = 5,  UnitPrice = 75.00 }
                    }
                },
                new Order
                {
                    OrderId = 1002,
                    Customer = "Beta Ltd.",
                    OrderDate = new DateTime(2024, 9, 16),
                    Total = 980.00,
                    Details = new List<OrderDetail>
                    {
                        new OrderDetail { Product = "Gadget X", Quantity = 8, UnitPrice = 80.00 },
                        new OrderDetail { Product = "Gadget Y", Quantity = 4, UnitPrice = 50.00 }
                    }
                }
            };
        }
    }

    // Simple POCO classes that represent master‑detail data
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime OrderDate { get; set; }
        public double Total { get; set; }
        public List<OrderDetail> Details { get; set; }
    }

    public class OrderDetail
    {
        public string Product { get; set; }
        public int Quantity { get; set; }
        public double UnitPrice { get; set; }
    }
}
```

### Pourquoi chaque partie est importante

1. **Charger le modèle Excel** – Le modèle contient la mise en page, les formules et le style. Les Smart Markers sont des espaces réservés comme `${MasterSheet:Orders}` que le processeur remplacera.

2. **Préparer la source de données** – `SmartMarkerProcessor` fonctionne avec n’importe quelle collection énumérable. Ici nous utilisons une liste d’objets `Order` contenant une liste imbriquée d’objets `OrderDetail`, exactement ce dont un rapport maître‑détail a besoin.

3. **Créer le processeur** – Instancier `SmartMarkerProcessor` est peu coûteux ; vous pouvez le réutiliser pour plusieurs feuilles si vous devez générer plusieurs rapports en une seule exécution.

4. **Traiter la feuille de calcul** – Cet appel unique effectue trois actions :
   - **Remplacer les smart tags** tels que `${MasterSheet:Orders}` par les valeurs réelles des champs.
   - **Développer l’étiquette de feuille de détail** (`${DetailSheetNewName:OrderDetails}`) en une nouvelle feuille pour chaque ligne maître.
   - **Copier le formatage** du modèle vers les lignes générées, en préservant votre conception.

5. **Enregistrer le résultat** – Le fichier de sortie (`GeneratedReport.xlsx`) est un rapport Excel entièrement renseigné, prêt à être distribué.

## Fusionner le modèle Excel avec la source de données

Le cœur de la technique **fusion de modèle Excel** repose sur la syntaxe des Smart Markers. Dans `ReportTemplate.xlsx` vous placeriez des balises comme :

| Cellule | Valeur |
|---------|--------|
| A1      | `${MasterSheet:Orders.OrderId}` |
| B1      | `${MasterSheet:Orders.Customer}` |
| C1      | `${MasterSheet:Orders.OrderDate:MM/dd/yyyy}` |
| D1      | `${MasterSheet:Orders.Total}` |
| A5      | `${DetailSheetNewName:OrderDetails}` |
| A6      | `${DetailSheet:OrderDetails.Product}` |
| B6      | `${DetailSheet:OrderDetails.Quantity}` |
| C6      | `${DetailSheet:OrderDetails.UnitPrice}` |

- `${MasterSheet:Orders}` indique au processeur de lire la collection `Orders` depuis la source de données.
- `${DetailSheetNewName:OrderDetails}` crée une **étiquette de feuille de détail** qui génère une nouvelle feuille nommée d’après la ligne maître (par ex., `OrderDetails_1001`).
- `${DetailSheet:OrderDetails.*}` remplit chaque ligne de détail.

Lorsque `processor.Process(ws, ordersData)` s’exécute, la bibliothèque **remplace automatiquement les smart tags** par les valeurs provenant de `ordersData` et duplique la feuille de détail pour chaque commande.

## Syntaxe de l’étiquette de feuille de détail

Une **étiquette de feuille de détail** suit le modèle `${DetailSheetNewName:TagName}`. Le `TagName` doit correspondre à une propriété renvoyant un `IEnumerable` (dans notre cas `Order.Details`). Le processeur :

1. Crée une nouvelle feuille pour chaque ligne maître.
2. Copie le formatage de la zone de détail du modèle.
3. Insère chaque élément de l’énumérable dans des lignes consécutives.

Si vous avez besoin que la feuille de détail conserve le même nom pour chaque ligne maître (par ex., une seule feuille contenant tous les détails), remplacez `${DetailSheetNewName:OrderDetails}` par `${DetailSheet:OrderDetails}`. Cette variante est utile dans les scénarios **générer un rapport Excel** où chaque commande possède son propre onglet.

## Utiliser les smart markers pour remplacer les smart tags

Les Smart Markers sont plus que de simples espaces réservés. Ils supportent :

- **Chaînes de formatage** (`:MM/dd/yyyy` dans l’exemple) pour contrôler l’affichage des dates ou des nombres.
- **Sections conditionnelles** (`${if:Orders.Total > 1000}`) pour masquer des lignes selon les données.
- **Boucles** sur des collections sans écrire de code supplémentaire au-delà de la balise.

Comme le processeur gère ces fonctionnalités en interne, vous **remplacez les smart tags** dans le modèle sans écrire de boucles personnalisées ou d’affectations cellule par cellule. Cela réduit les bugs et rend le modèle plus maintenable.

## Résultat attendu

Après l’exécution du programme, ouvrez `GeneratedReport.xlsx`. Vous devriez voir :

1. Une **feuille maître** nommée *Sheet1* avec deux lignes — une pour chaque commande. Les colonnes affichent l’ID de la commande, le client, la date de commande et le total.
2. Deux **feuilles de détail** nommées `OrderDetails_1001` et `OrderDetails_1002`. Chaque feuille répertorie les produits, les quantités et les prix unitaires de la commande correspondante.
3. Tout le formatage original (polices, couleurs, bordures) préservé depuis `ReportTemplate.xlsx`.

![Generated Excel report after merging template with Smart Markers](generated-report.png "Generated Excel report after merging template


## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Aspose Cells Smart Markers: Load Excel Template & Generate Excel from Template](/cells/english/java/templates-reporting/aspose-cells-smart-markers-load-excel-template-generate-exce/)
- [Generate Dynamic Excel Reports Using Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Aspose Cells Smart Markers: Generate Excel from Model in C#](/cells/english/net/smart-markers-dynamic-data/aspose-cells-smart-markers-generate-excel-from-model-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}