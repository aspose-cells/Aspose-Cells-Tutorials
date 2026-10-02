---
category: general
date: 2026-05-30
description: Remplissez rapidement un modèle Excel et apprenez à alimenter Excel avec
  des données en utilisant Aspose.Cells SmartMarker. Guide complet en C# avec du code
  exécutable.
draft: false
keywords:
- populate excel template
- fill excel with data
- Aspose.Cells SmartMarker
- automate Excel reporting
- C# Excel automation
language: fr
og_description: Remplissez le modèle Excel et alimentez le classeur avec des données
  en utilisant Aspose.Cells SmartMarker. Suivez ce tutoriel C# étape par étape pour
  des résultats instantanés.
og_title: Remplir le modèle Excel – Remplir les données Excel via SmartMarker
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  headline: Populate Excel Template – Fill Excel Data via SmartMarker
  type: TechArticle
- description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  name: Populate Excel Template – Fill Excel Data via SmartMarker
  steps:
  - name: Empty Collections
    text: 'If `Items` is empty, SmartMarker will leave the table header intact but
      won’t insert any rows. To avoid a blank space, you can add a conditional block:'
  - name: Custom Number Formats
    text: 'Sometimes you need currency symbols or thousands separators. After processing,
      you can apply a style programmatically:'
  - name: Large Data Sets
    text: 'For thousands of rows, enable the `UseFastMode` option to improve performance:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Remplir le modèle Excel – Remplir les données Excel via SmartMarker
url: /fr/net/smart-markers-dynamic-data/populate-excel-template-fill-excel-data-via-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Remplir le modèle Excel – Remplir les données Excel via SmartMarker

Vous avez déjà eu besoin de **remplir un modèle Excel** mais vous ne saviez pas comment automatiser le processus ? Dans ce tutoriel, nous vous montrerons comment **remplir Excel avec des données** en utilisant Aspose.Cells SmartMarker — un outil qui transforme un classeur statique en générateur de rapports dynamique.

Imaginez que vous avez une feuille de facture pré‑conçue, un tableau de bord de ventes ou tout formulaire réutilisable. Au lieu de saisir manuellement les valeurs, vous pouvez fournir un objet C# et laisser SmartMarker faire le travail lourd. À la fin de ce guide, vous disposerez d’un projet entièrement exécutable qui prend un modèle, injecte des lignes, des totaux et même du formatage conditionnel — le tout sans toucher à l’interface utilisateur.

## Ce que vous apprendrez

- Comment préparer une source de données qui correspond aux marqueurs de votre modèle Excel.  
- Comment instancier **SmartMarkerProcessor** et activer la prise en charge des plages.  
- Comment **remplir le modèle Excel** avec des collections imbriquées, comme les articles de commande.  
- Conseils pour gérer les cas particuliers tels que les collections vides ou les formats numériques personnalisés.  

Aucun service externe, aucune macro VBA — uniquement du pur C# et Aspose.Cells. Tout ce dont vous avez besoin, c’est de .NET 6 (ou version ultérieure) et du package NuGet Aspose.Cells.

## Prérequis

- Visual Studio 2022 (ou tout IDE de votre choix).  
- .NET 6 SDK installé.  
- Aspose.Cells for .NET (vous pouvez obtenir un essai gratuit sur le site d'Aspose).  
- Un modèle Excel de base avec des balises SmartMarker (nous en créerons un dans un instant).

Si l’un de ces éléments vous est inconnu, ne paniquez pas ; les étapes ci‑dessous vous guideront à travers chaque exigence.

## Étape 1 : Concevoir le modèle Excel avec des balises SmartMarker

Tout d’abord, ouvrez un nouveau classeur et disposez les parties statiques — logo de l’entreprise, en‑têtes, etc. Insérez ensuite les espaces réservés SmartMarker là où les données dynamiques doivent apparaître.

| Cellule | Contenu |
|---------|---------|
| A1      | **Facture** |
| A3      | `{{CompanyName}}` |
| A5      | **Détails de la commande** |
| A7      | `{{Orders.Items.Name}}` |
| B7      | `{{Orders.Items.Qty}}` |
| C7      | `{{Orders.Items.Price}}` |
| D7      | `{{Orders.Items.Price * Orders.Items.Qty}}` |

**Pourquoi c’est important :** SmartMarker lit les accolades doubles et les associe aux propriétés de l’objet que vous transmettez plus tard. La collection `Orders.Items` indique au moteur de répéter la ligne pour chaque élément de la liste.

> **Astuce :** Utilisez l’option `RangeSmartMarker` (nous l’activerons plus tard) lorsque vous avez besoin que le moteur étende automatiquement la plage — idéal pour les tableaux qui s’agrandissent ou se rétrécissent.

Enregistrez le fichier sous le nom `InvoiceTemplate.xlsx` dans le dossier `Resources` de votre projet.

## Étape 2 : Préparer la source de données qui correspond aux marqueurs du modèle

Nous créons maintenant un objet anonyme C# (ou une classe fortement typée) dont les noms de propriétés correspondent exactement aux marqueurs. L’essentiel est de reproduire la hiérarchie à la lettre.

```csharp
// Step 2: Prepare the data source that matches the template markers
var data = new
{
    CompanyName = "Acme Corp.",
    Orders = new[]
    {
        new
        {
            Items = new[]
            {
                new { Name = "Pen",   Qty = 2, Price = 1.5m },
                new { Name = "Notebook", Qty = 1, Price = 3.75m },
                new { Name = "Stapler",  Qty = 1, Price = 5.0m }
            }
        }
    }
};
```

**Pourquoi c’est important :** Le tableau `Orders` contient une seule commande, et chaque commande possède un tableau `Items`. SmartMarker itérera sur `Items`, dupliquant la ligne pour chaque élément. Si vous avez besoin de plusieurs commandes plus tard, il suffit d’ajouter d’autres objets au tableau `Orders` — aucune modification de code n’est requise.

## Étape 3 : Charger le modèle et créer une instance de SmartMarkerProcessor

Avec les données prêtes, nous chargeons le classeur, créons le processeur et indiquons qu’il doit respecter les marqueurs de plage.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook
Workbook workbook = new Workbook("Resources/InvoiceTemplate.xlsx");

// Get the first worksheet (where our markers live)
Worksheet ws = workbook.Worksheets[0];

// Step 3: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

**Pourquoi c’est important :** `SmartMarkerProcessor` est le moteur qui analyse les marqueurs, étend les plages et écrit les valeurs. En séparant le processeur du classeur, vous gardez le code propre et réutilisable.

## Étape 4 : Traiter la feuille avec RangeSmartMarker activé

La magie opère lorsque nous appelons `Process`. Le réglage `RangeSmartMarker = true` indique à SmartMarker de traiter toute la plage de lignes comme un bloc répétable, insérant ou supprimant automatiquement des lignes selon les besoins.

```csharp
// Step 4: Process the worksheet using SmartMarker with range support enabled
processor.Process(ws, data, new SmartMarkerOptions { RangeSmartMarker = true });
```

À ce stade, le moteur a :

1. Scanné la feuille à la recherche des balises `{{...}}`.  
2. Associé chaque balise à une propriété de `data`.  
3. Détecté la plage du tableau (A7:D7) et dupliqué celle‑ci trois fois — une fois par article.  
4. Calculé l’expression `Price * Qty` pour la colonne total.

## Étape 5 : Enregistrer le classeur résultant

Enfin, écrivez le classeur rempli sur le disque (ou renvoyez‑le via un flux à un client web).

```csharp
// Step 5: Save the populated workbook
workbook.Save("Output/InvoicePopulated.xlsx");
```

Ouvrez `InvoicePopulated.xlsx` et vous verrez un tableau correctement rempli :

| Nom      | Quantité | Prix | Total |
|----------|----------|------|-------|
| Pen       | 2   | 1.5   | 3.00 |
| Notebook  | 1   | 3.75  | 3.75 |
| Stapler   | 1   | 5.00  | 5.00 |

L’étape **remplir le modèle Excel** est maintenant terminée, et vous avez réussi à **remplir Excel avec des données** pour n’importe quel nombre de lignes.

## Gestion des cas particuliers courants

### Collections vides

Si `Items` est vide, SmartMarker laissera l’en‑tête du tableau intacte mais n’insérera aucune ligne. Pour éviter un espace blanc, vous pouvez ajouter un bloc conditionnel :

```csharp
{{#if Orders.Items.Length > 0}}
    ... table rows ...
{{else}}
    No items were ordered.
{{/if}}
```

### Formats numériques personnalisés

Parfois vous avez besoin de symboles monétaires ou de séparateurs de milliers. Après le traitement, vous pouvez appliquer un style par programme :

```csharp
Style style = workbook.CreateStyle();
style.Number = 164; // Built‑in currency format
StyleFlag flag = new StyleFlag { NumberFormat = true };

foreach (Cell cell in ws.Cells["C8:D12"])
{
    cell.SetStyle(style, flag);
}
```

### Grands ensembles de données

Pour des milliers de lignes, activez l’option `UseFastMode` afin d’améliorer les performances :

```csharp
processor.Process(ws, data, new SmartMarkerOptions { 
    RangeSmartMarker = true,
    UseFastMode = true
});
```

## Exemple complet fonctionnel

Voici le programme complet, autonome, que vous pouvez copier‑coller dans une application console. Il comprend toutes les directives `using`, la préparation des données, le traitement et l’enregistrement.



## Que devriez‑vous apprendre ensuite ?

- [Remplir Excel avec des données en utilisant Aspose.Cells et Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Comment remplir les cellules Excel avec Aspose.Cells pour .NET : Guide étape par étape](/cells/english/net/cell-operations/aspose-cells-dotnet-populate-excel-data/)
- [Automatiser l’exportation de données Excel avec Aspose.Cells pour .NET : Guide étape par étape](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}