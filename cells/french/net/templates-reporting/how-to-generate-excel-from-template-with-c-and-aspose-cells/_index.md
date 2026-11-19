---
category: general
date: 2026-11-19
description: Apprenez à générer Excel à partir d’un modèle en C# rapidement. Ce guide
  vous montre également comment générer un rapport Excel en C# en utilisant les Smart
  Markers.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate excel from template
- generate excel report c#
- Aspose.Cells Smart Marker
- master‑detail Excel export
- C# Excel automation
language: fr
lastmod: 2026-11-19
og_description: Générez un fichier Excel à partir d’un modèle en C# avec Aspose.Cells.
  Suivez ce tutoriel pour créer un rapport Excel en C# en utilisant les Smart Markers
  et les données maître‑détail.
og_image_alt: Screenshot showing C# code that generates Excel from a template file
og_title: Générer un Excel à partir d'un modèle en C# – guide complet étape par étape
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to generate Excel from template in C# quickly. This guide
    also shows you how to generate Excel report C# using Smart Markers.
  headline: How to generate Excel from template with C# and Aspose.Cells
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Comment générer un Excel à partir d'un modèle avec C# et Aspose.Cells
url: /fr/net/templates-reporting/how-to-generate-excel-from-template-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Générer Excel à partir d'un modèle en C# – guide complet étape par étape

Si vous devez **générer Excel à partir d'un modèle** dans un projet .NET, ce tutoriel vous montre une solution prête à l'emploi. En utilisant Aspose.Cells Smart Markers, vous pouvez remplir un classeur pré‑conçu avec des données maître‑détail et produire un rapport soigné sans écrire vous-même de formules spécifiques à Excel.

Vous verrez également comment la même approche vous permet de **générer un rapport Excel C#** pour des factures, des résumés de commandes ou tout jeu de données hiérarchique. À la fin du guide, vous disposerez d’une méthode réutilisable qui transforme un fichier modèle en un classeur entièrement rempli.

## Ce que couvre ce tutoriel

* Chargement d'un modèle `.xlsx` existant contenant déjà des espaces réservés Smart Marker.  
* Préparation d'un objet maître‑détail correspondant à la hiérarchie du modèle.  
* Configuration du `SmartMarkerProcessor` pour créer une feuille de détail séparée pour les collections imbriquées.  
* Traitement de la feuille de calcul et sauvegarde du résultat dans un nouveau fichier.  

Aucun service externe n'est requis — uniquement la bibliothèque Aspose.Cells pour .NET (version d'essai gratuite ou version sous licence) et un projet .NET 6+.

## Prérequis

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| **Aspose.Cells for .NET** (NuGet package `Aspose.Cells`) | Fournit le `SmartMarkerProcessor` et les API de manipulation Excel. |
| **.NET 6 SDK** ou version ultérieure | Assure les fonctionnalités modernes du langage et la compatibilité avec la dernière version d'Aspose.Cells. |
| **Un classeur modèle** (`template.xlsx`) avec des Smart Markers placés dans la première feuille | Les Smart Markers pilotent la liaison des données ; le modèle définit la mise en page, les styles et le contenu statique. |
| Connaissances de base des collections C# et des types anonymes | La source de données est construite comme un objet anonyme qui reflète la structure du modèle. |

Vous pouvez créer le modèle dans Excel en tapant `&=Orders.Id` pour la colonne d'ID de commande et `&=Orders.Items.Name` pour les éléments imbriqués. Le préfixe `&=` indique aux Smart Markers de remplacer la cellule par les données à l'exécution.

## Étape 1 : Configurer le projet C# et ajouter Aspose.Cells

Créez une application console (ou intégrez-la dans un service existant) et ajoutez le package NuGet :

```bash
dotnet new console -n ExcelTemplateDemo
cd ExcelTemplateDemo
dotnet add package Aspose.Cells
```

> **Astuce :** Utilisez le drapeau `--version` pour verrouiller à une version stable connue, par ex., `Aspose.Cells 23.12`.

## Étape 2 : Définir la source de données maître‑détail

La source de données doit refléter la hiérarchie utilisée dans le modèle. Dans cet exemple, nous avons des commandes (maître) contenant chacune une collection d'articles (détail).

```csharp
using System;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Create the data source with master‑detail information
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Name = "A" },
                            new { Name = "B" }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Name = "C" }
                        }
                    }
                }
            };
```

**Pourquoi cela fonctionne :**  
*Le type anonyme* vous permet de créer rapidement une représentation en mémoire sans définir de classes POCO explicites. Chaque `Order` possède un `Id` et un tableau `Items`, ce qui correspond aux marqueurs `&=Orders.Id` et `&=Orders.Items.Name` du modèle.

## Étape 3 : Charger le modèle Excel contenant des Smart Markers

```csharp
            // Step 3: Load the Excel template that contains Smart Markers
            string templatePath = @"YOUR_DIRECTORY\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
```

**Explication :**  
`Workbook` lit le fichier `.xlsx` en mémoire. Le modèle doit déjà contenir la syntaxe Smart Marker (`&=Orders.Id`, `&=Orders.Items.Name`, etc.) placée à l'endroit où vous souhaitez que les données apparaissent.

## Étape 4 : Obtenir la feuille de calcul où les Smart Markers sont placés

```csharp
            // Step 4: Get the worksheet where the Smart Markers are placed
            Worksheet worksheet = workbook.Worksheets[0];   // first sheet (index 0)
```

**Pourquoi la première feuille ?**  
La plupart des modèles conservent le tableau maître sur la première feuille, mais vous pouvez référencer n'importe quelle feuille par son nom (`workbook.Worksheets["SheetName"]`) si votre conception diffère.

## Étape 5 : Configurer le processeur SmartMarker

Le `SmartMarkerProcessor` gère le travail lourd. En définissant `DetailSheetNewName` nous indiquons à Aspose.Cells de créer une nouvelle feuille pour chaque collection imbriquée.

```csharp
            // Step 5: Set up the SmartMarker processor and configure options
            SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
            smartMarkerProcessor.Options.DetailSheetNewName = "OrderDetails";
```

**Ce que cela fait :**  
Lorsque le processeur rencontre une collection à l'intérieur d'une collection (le tableau `Items`), il crée une nouvelle feuille de calcul nommée `OrderDetails` et la remplit avec les lignes correspondantes. Cela maintient la feuille maître ordonnée et reflète une disposition typique de rapport maître‑détail.

## Étape 6 : Traiter la feuille de calcul en utilisant la source de données

```csharp
            // Step 6: Process the worksheet using the data source
            smartMarkerProcessor.Process(worksheet, orderData);
```

La méthode `Process` remplace chaque Smart Marker par la valeur correspondante provenant de `orderData`. Elle étend également les lignes si nécessaire, de sorte que vous n'ayez pas à pré‑allouer de l'espace dans le modèle.

## Étape 7 : Enregistrer le classeur rempli

```csharp
            // Step 7: Save the populated workbook
            string outputPath = @"YOUR_DIRECTORY\masterDetail.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Résultat :**  
- `masterDetail.xlsx` contient une feuille maître avec les ID de commande.  
- Une nouvelle feuille `OrderDetails` contient les noms d'articles pour chaque commande.  
- Tous les formats (polices, bordures, largeurs de colonnes) du modèle sont conservés.

Vous pouvez ouvrir le fichier dans Excel pour vérifier que les données correspondent à l'objet source.

## Code source complet (prêt à copier‑coller)

```csharp
using System;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create the data source with master‑detail information
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Name = "A" },
                            new { Name = "B" }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Name = "C" }
                        }
                    }
                }
            };

            // Step 2: Load the Excel template that contains Smart Markers
            string templatePath = @"YOUR_DIRECTORY\template.xlsx";
            Workbook workbook = new Workbook(templatePath);

            // Step 3: Get the worksheet where the Smart Markers are placed
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 4: Set up the SmartMarker processor and configure options
            SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
            smartMarkerProcessor.Options.DetailSheetNewName = "OrderDetails";

            // Step 5: Process the worksheet using the data source
            smartMarkerProcessor.Process(worksheet, orderData);

            // Step 6: Save the populated workbook
            string outputPath = @"YOUR_DIRECTORY\masterDetail.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Sortie attendue dans Excel**

| **Commandes** (feuille maître) |
|---|
| Id |
| 1 |
| 2 |

*Feuille OrderDetails* :

| **Articles** |
|---|
| Nom |
| A |
| B |
| C |

## Variations courantes et cas limites

| Situation | Comment adapter le code |
|-----------|--------------------------|
| **Niveaux de détail multiples** (p. ex., Orders → Items → SubItems) | Ajoutez une autre propriété de collection (`SubItems`) et définissez `DetailSheetNewName` à une valeur différente pour chaque niveau. Aspose.Cells créera automatiquement des feuilles supplémentaires. |
| **Nom de feuille personnalisé par enregistrement maître** | Utilisez `smartMarkerProcessor.Options.DetailSheetNameFromData = true;` et incluez un champ `SheetName` dans la collection maître. |
| **Jeux de données volumineux (10 000 + lignes)** | Appelez `workbook.Settings.MemorySetting = MemorySetting.MemoryOptimized;` avant de charger le modèle pour réduire la consommation mémoire. |
| **Modèle sans feuille de détail** (rapport plat) | Omettez `DetailSheetNewName` ; le processeur écrira les données imbriquées directement dans la feuille maître, en développant les lignes si nécessaire. |
| **Exécution sous ASP.NET Core** | Remplacez `Console.WriteLine` par la journalisation (`ILogger`) et utilisez `Path.Combine` pour résoudre les emplacements de fichiers relatifs à `wwwroot`. |

## Conseils pour une génération fiable d'Excel

* **Gardez les espaces réservés dans une ligne séparée** – les Smart Markers développent les lignes sous le marqueur ; les placer dans la ligne d'en-tête préserve le formatage.  
* **Évitez de fusionner des cellules à l'intérieur de la zone de données** – les cellules fusionnées peuvent provoquer des déplacements de lignes inattendus lors de l'expansion.  
* **Testez avec un jeu de données minimal** d'abord ; une fois la mise en page fonctionnelle, passez à des données réelles.  
* **Verrouillage de version** – Notez la version d'Aspose.Cells que vous avez utilisée (`Aspose.Cells 23.12`) pour éviter les ruptures lors d'une mise à jour.  

## Conclusion

Vous savez maintenant comment **générer Excel à partir d'un modèle** en C# en utilisant Aspose.Cells Smart Markers, et vous pouvez facilement étendre le même schéma pour **générer un rapport Excel C#** pour n'importe quel scénario maître‑détail. L'approche sépare la mise en page (le modèle) des données (l'objet C#), vous offrant un moteur de reporting maintenable et réutilisable.

Ensuite, explorez ces sujets liés :

* **Styling cells programmatically** – learn how to apply conditional formatting after data is populated.  
* **Exporting to PDF** – Aspose.Cells can convert the generated workbook to a PDF with a single call.  
* **Integrating with ASP.NET Core** – stream the generated file directly to the browser without writing to disk.

Mettez le code en pratique, modifiez le modèle pour qu'il corresponde à votre identité visuelle, et laissez les rapports Excel générés devenir une partie centrale de vos applications .NET. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment générer un rapport Excel en fusionnant un modèle Excel avec Smart Markers](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-by-merging-an-excel-template-wi/)
- [Comment générer un rapport Excel en C# – Guide complet utilisant SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)
- [Aspose Cells Smart Markers : Générer Excel à partir d'un modèle en C#](/cells/english/net/smart-markers-dynamic-data/aspose-cells-smart-markers-generate-excel-from-model-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}