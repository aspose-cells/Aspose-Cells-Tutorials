---
category: general
date: 2026-02-28
description: Créer un rapport maître‑détail en C# et apprendre à remplir un modèle
  Excel, à fusionner les données dans Excel et à charger un classeur Excel en C# en
  quelques étapes seulement.
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: fr
og_description: Créez un rapport maître‑détail en C# en utilisant Aspose.Cells SmartMarker.
  Apprenez à charger un classeur Excel en C#, à fusionner des données dans Excel et
  à remplir un modèle Excel.
og_title: Créer un rapport maître‑détail en C# – Remplir un modèle Excel
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: Créer un rapport maître‑détail en C# – Remplir le modèle Excel avec SmartMarker
url: /fr/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un rapport maître‑détail en C# – Remplir un modèle Excel avec SmartMarker

Vous avez déjà eu besoin de **créer un rapport maître‑détail** en C# mais vous ne saviez pas comment mettre les données dans un fichier Excel ? Vous n'êtes pas seul. Dans ce guide, nous passerons en revue les étapes exactes pour **remplir le modèle Excel**, **fusionner les données dans Excel**, et **charger le classeur Excel en C#**‑style afin d'obtenir un rapport maître‑détail soigné, prêt à être distribué.

Nous utiliserons Aspose.Cells SmartMarker, un moteur puissant qui comprend les relations maître‑détail dès le départ. À la fin du tutoriel, vous disposerez d'un exemple complet et exécutable que vous pourrez intégrer à n'importe quel projet .NET. Pas de raccourcis vagues du type « voir la documentation » — juste une solution autonome que vous pouvez copier‑coller et exécuter.

## Ce que vous allez apprendre

- Comment **créer des structures de données maître‑détail** en C# qui correspondent directement à un modèle Excel.
- La façon exacte de **charger le classeur Excel en C#** avec du code qui ouvre un fichier `.xlsx` contenant des balises SmartMarker.
- Le processus pour **remplir le modèle Excel** en exécutant `SmartMarkerProcessor`.
- Conseils pour gérer les cas limites, comme les balises manquantes ou les ensembles de données volumineux.
- Comment vérifier le résultat et à quoi ressemble le **rapport maître‑détail** final.

### Prérequis

- .NET 6.0 ou ultérieur (le code fonctionne également sur .NET Framework 4.8).
- Aspose.Cells pour .NET (vous pouvez obtenir le package d'essai gratuit NuGet : `Install-Package Aspose.Cells`).
- Un fichier Excel de base (`template.xlsx`) contenant des balises SmartMarker (nous montrerons le balisage minimal dont vous avez besoin).

Si vous avez tout cela prêt, plongeons‑y.

## Étape 1 – Créer la source de données maître‑détail *(comment créer un maître‑détail)*

La première chose dont vous avez besoin est un objet C# qui représente les lignes maîtres (commandes) et leurs lignes enfants (articles de commande). SmartMarker lira automatiquement cette hiérarchie lorsque `MasterDetail` est défini sur `true`.

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**Pourquoi c’est important :**  
SmartMarker recherche une propriété nommée `Orders` (le maître) puis, pour chaque commande, il cherche une collection appelée `Items`. En faisant correspondre ces noms, vous obtenez automatiquement un **rapport maître‑détail** sans écrire de boucles vous‑même.

> **Astuce :** Gardez les noms de propriétés courts et significatifs ; ils deviennent les espaces réservés dans votre modèle Excel.

## Étape 2 – Configurer les options SmartMarker pour le traitement maître‑détail

Indiquez au moteur que vous traitez un scénario maître‑détail et fournissez le nom de la feuille de détail qui recevra les lignes enfants.

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**Pourquoi c’est important :**  
Si vous omettez `MasterDetail = true`, SmartMarker traitera les données comme une liste plate et les lignes de détail n’apparaîtront jamais. `DetailSheetName` doit correspondre exactement au nom de la feuille que vous avez créée dans le modèle (sensible à la casse).

## Étape 3 – Charger le classeur Excel en style C#

Nous ouvrons maintenant le modèle contenant les balises SmartMarker. Il s'agit de l'étape **load Excel workbook C#** sur laquelle de nombreux développeurs trébuchent parce qu'ils oublient d'utiliser le bon chemin de fichier ou de libérer correctement le classeur.

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**Pourquoi c’est important :**  
Aspose.Cells lit l'intégralité du classeur en mémoire, de sorte que le fichier peut être sur le disque, intégré comme ressource, ou même diffusé depuis un service web. Assurez‑vous simplement que le chemin pointe vers un fichier `.xlsx` valide contenant les balises que nous aborderons ensuite.

## Étape 4 – Insérer les balises SmartMarker dans le modèle (remplir le modèle Excel)

Si vous ouvrez `template.xlsx` maintenant, vous verrez deux feuilles :

- **Orders** – la feuille maître avec une ligne comme `&=Orders.Id`.
- **OrderDetail** – la feuille de détail avec des lignes comme `&=Items.Sku` et `&=Items.Qty`.

Voici une vue minimale du balisage :

| Sheet | Cell A1 | Cell B1 |
|-------|---------|---------|
| Orders | `&=Orders.Id` | *(empty)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

Vous n’avez pas besoin d’écrire du code pour les balises — elles résident dans le fichier Excel. L’étape **populate Excel template** consiste simplement à appeler le processeur :

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**Pourquoi c’est important :**  
Le processeur parcourt chaque feuille, remplace les espaces réservés `&=` par les valeurs réelles, et développe les lignes pour chaque enregistrement maître et détail. Comme `MasterDetail` est activé, il crée automatiquement une nouvelle ligne pour chaque article sous la commande correspondante.

## Étape 5 – Enregistrer le rapport maître‑détail

Enfin, écrivez le classeur rempli sur le disque. C’est le moment où vous obtenez un **rapport maître‑détail** prêt à être partagé.

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Sortie attendue :**  

- La feuille **Orders** montre deux lignes : `1` et `2` (identifiants de commande).  
- La feuille **OrderDetail** montre trois lignes :
  - SKU 101 Qty 2
  - SKU 102 Qty 1
  - SKU 202 Qty 1  

C’est un **create master detail report** entièrement fonctionnel que vous pouvez envoyer par e‑mail, imprimer ou injecter dans un autre système.

## Cas limites & questions fréquentes

### Que faire si le modèle manque une balise ?

SmartMarker ignore silencieusement les balises inconnues, mais vous vous retrouverez avec des cellules vides. Vérifiez l’orthographe des balises et assurez‑vous que les noms de propriétés de votre objet C# correspondent exactement.

### Comment gère‑t‑il les grands ensembles de données ?

Le processeur diffuse les lignes, de sorte que même des milliers d’enregistrements de détail n’épuiseront pas la mémoire. Cependant, pour des fichiers extrêmement volumineux, vous pourriez vouloir augmenter le `MemorySetting` dans `LoadOptions`.

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### Puis‑je utiliser un nom de feuille différent pour le maître ?

Oui—renommez simplement la feuille dans le modèle et ajustez le `DetailSheetName` si vous avez une feuille de détail. Le nom de la feuille maître est déduit du placeholder (`&=Orders.Id`).

### Que faire si je dois ajouter une ligne de totaux ?

Ajoutez une formule Excel classique dans le modèle (par ex., `=SUM(B2:B{#})`). SmartMarker conservera la formule après l’insertion des données.

## Exemple complet exécutable

Ci‑dessous se trouve le programme complet que vous pouvez copier‑coller dans une application console. Il comprend toutes les directives `using`, le modèle de données, les options et la gestion des fichiers.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

Exécutez le programme, ouvrez `output.xlsx`, et vous verrez les données maître‑détail magnifiquement peuplées.

## Référence visuelle

![Create master detail report output screenshot](https://example.com/images/master-detail-report.png "Create master detail report example")

*L’image montre la feuille Orders avec les ID 1 et 2, et la feuille OrderDetail avec les trois lignes SKU‑Qty.*

## Conclusion

Vous savez maintenant **comment créer un rapport maître‑détail** en C# en utilisant Aspose.Cells SmartMarker, depuis la construction de la source de données jusqu’à **charger le classeur Excel en C#**, **remplir le modèle Excel**, et enfin

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}