---
category: general
date: 2026-02-14
description: Créez un objet de données maître en C# et générez facilement une feuille
  de détail. Apprenez le flux de travail complet de SmartMarker avec des exemples
  de code pratiques.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: fr
og_description: Créez un objet de données maître en C# et générez une feuille de détail
  avec SmartMarker. Suivez notre tutoriel détaillé pour une solution prête à l'emploi.
og_title: Créer un objet de données de référence – Guide complet
tags:
- C#
- SmartMarker
- Excel Automation
title: Créer un objet de données maître – Guide étape par étape pour générer la feuille
  de détail
url: /fr/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un objet de données maître – Tutoriel complet

Vous avez déjà eu besoin de **créer un objet de données maître** pour une feuille de calcul Excel mais vous ne saviez pas comment le lier à une feuille de détail SmartMarker ? Vous n'êtes pas seul. Dans de nombreux scénarios de reporting, l'objet maître alimente une feuille de détail dynamique, et obtenir le bon câblage peut ressembler à assembler un puzzle sans image.  

Dans ce guide, nous parcourrons l’ensemble du processus — construction de l’objet de données maître, configuration des options SmartMarker pour **générer une feuille de détail**, puis déclenchement du processeur. À la fin, vous disposerez d’un extrait exécutable que vous pourrez coller dans n’importe quel projet .NET utilisant la bibliothèque GrapeCity Documents for Excel (GcExcel).

## Ce dont vous avez besoin

- .NET 6+ (ou .NET Framework 4.7.2) avec une référence à `GcExcel.dll`
- Connaissances de base en C# (variables, types anonymes, initialiseurs d’objets)
- Un classeur Excel contenant déjà des balises SmartMarker comme `{{OrderId}}` et un tableau d’articles
- Visual Studio, Rider ou tout éditeur de votre choix

C’est tout — aucun package NuGet supplémentaire au‑delà de la distribution de base de GcExcel.

## Étape 1 : Créer l’objet de données maître

La première chose à faire est de **créer un objet de données maître** qui reflète la structure attendue par les balises SmartMarker. Considérez‑le comme un petit modèle de rapport en mémoire.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Pourquoi utiliser un type anonyme ici ? Parce qu’il vous permet de définir un conteneur léger sans déclarer une classe complète—idéal pour des démonstrations rapides ou lorsque la forme ne risque pas de changer. Si vous avez besoin d’un modèle réutilisable plus tard, remplacez simplement `var` par un POCO approprié.

> **Astuce :** Conservez les noms de propriétés (`OrderId`, `Product`, `Quantity`) identiques aux espaces réservés de votre feuille ; SmartMarker les compare sans tenir compte de la casse.

## Étape 2 : Configurer les options SmartMarker pour générer une feuille de détail

Nous indiquons maintenant à SmartMarker que nous souhaitons une feuille de calcul distincte pour le tableau des lignes d’articles. C’est ici que le mot‑clé **generate detail sheet** entre en jeu.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

Le modèle `DetailSheetNewName` utilise des espaces réservés entre accolades qui sont remplacés à l’exécution. Dans notre exemple, la feuille sera nommée `Order_1`. Si vous parcourez plus tard plusieurs commandes, chacune obtient son propre onglet—exactement ce que la plupart des comptables attendent.

## Étape 3 : Exécuter le processeur SmartMarker

Avec les données et les options prêtes, la dernière étape consiste à invoquer le processeur sur la feuille de calcul cible.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

En coulisses, SmartMarker parcourt la feuille à la recherche de balises, injecte les valeurs `orderData`, et comme `DetailSheet` est `true`, il clone le modèle dans une nouvelle feuille nommée `Order_1`. Toutes les lignes d’articles apparaissent dans la zone de détail, en conservant le formatage que vous avez appliqué au modèle.

### Exemple complet fonctionnel

Voici un programme console autonome qui ouvre un classeur modèle (`Template.xlsx`), exécute les trois étapes, puis enregistre le résultat sous `Result.xlsx`. Vous pouvez le copier‑coller dans un nouveau projet console et appuyer sur **F5**.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Résultat attendu

- **Result.xlsx** contient une feuille appelée `Order_1`.
- La cellule `A1` (ou l’endroit où vous avez placé `{{OrderId}}`) affiche maintenant `1`.
- Un tableau commençant au bloc SmartMarker répertorie deux lignes :
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

Si vous ouvrez le fichier, vous verrez le formatage du modèle préservé — bordures, polices, mise en forme conditionnelle—tout est intact.

## Questions fréquentes et cas particuliers

### Et si j’ai plusieurs commandes ?

Enveloppez l’objet maître dans une collection et laissez SmartMarker itérer automatiquement :

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Chaque commande génère sa propre feuille (`Order_1`, `Order_2`, …). Le processeur considère le tableau externe comme la collection maître.

### Comment contrôler la position de la feuille ?

Définissez `smartMarkerOptions.DetailSheetInsertIndex = 2;` pour placer la nouvelle feuille après le deuxième onglet, ou utilisez `DetailSheetInsertAfter = "Summary"` pour l’insérer après une feuille nommée.

### Puis‑je désactiver la feuille de détail pour une exécution particulière ?

Il suffit de basculer `DetailSheet = false;`. SmartMarker écrira alors les lignes d’articles dans la même feuille où résident les balises maîtres.

### Qu’en est‑il des grands ensembles de données ?

SmartMarker diffuse les données efficacement, mais si vous dépassez quelques centaines de milliers de lignes, vous pourriez atteindre la limite de 1 048 576 lignes d’Excel. Dans ce cas, divisez les données en plusieurs enregistrements maîtres ou envisagez d’exporter en CSV.

## Vue d’ensemble visuelle

![Diagramme illustrant comment créer un objet de données maître et générer une feuille de détail avec SmartMarker](/images/smartmarker-flow.png)

*L’illustration montre le flux depuis l’objet maître C# → options SmartMarker → traitement de la feuille de calcul → nouvelle feuille de détail.*

## Conclusion

Vous savez maintenant comment **créer un objet de données maître** en C# et configurer SmartMarker pour **générer automatiquement une feuille de détail**. Le schéma en trois étapes — données, options, processeur—couvre la majorité des scénarios d’automatisation Excel avec GcExcel.  

À partir d’ici, vous pourriez explorer :

- Ajouter des données d’en‑tête/pied de page à chaque feuille de détail
- Utiliser la mise en forme conditionnelle en fonction du statut de la commande
- Exporter le classeur généré en PDF avec `workbook.SaveAsPdf(...)`

N’hésitez pas à expérimenter, à casser des choses, puis à les remettre en place. C’est la façon la plus rapide de maîtriser l’automatisation des feuilles de calcul. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}