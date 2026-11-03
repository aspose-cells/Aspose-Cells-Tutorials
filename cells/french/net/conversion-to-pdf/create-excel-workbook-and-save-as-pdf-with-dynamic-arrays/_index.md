---
category: general
date: 2026-09-15
description: Créer un classeur Excel en C# et apprendre à enregistrer le classeur
  au format PDF tout en déversant des tableaux dynamiques à l'aide de la fonction
  EXPAND.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: fr
lastmod: 2026-09-15
og_description: Créez un classeur Excel en C# et enregistrez‑le rapidement au format
  PDF tout en utilisant la fonction EXPAND pour générer un tableau dynamique à débordement.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: Créer un classeur Excel et l’enregistrer au format PDF avec des tableaux
  dynamiques
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Créer un classeur Excel et l’enregistrer au format PDF avec des tableaux dynamiques
url: /fr/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel et l’enregistrer en PDF avec des tableaux dynamiques

Si vous devez **créer un classeur Excel** de façon programmatique puis **enregistrer le classeur au format PDF**, ce guide vous montre une solution complète, de bout en bout, en C#. Vous verrez également comment **déverser les résultats d’un tableau dynamique** en utilisant la **fonction EXPAND**, qui est la méthode moderne pour générer des tableaux sans VBA.  

Que vous construisiez un service de reporting, une fonction d’exportation pour un système ERP, ou un tableau de bord piloté par les données, les étapes ci‑dessous vous permettent de générer un classeur, le remplir avec des données Smart‑Marker, et produire un PDF qui préserve les fonctionnalités avancées des polices.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 ou supérieur (le code fonctionne également avec .NET Framework 4.8)
* Une version récente de **Aspose.Cells for .NET** (v25.8 ou plus) – elle fournit `Workbook`, `PdfSaveOptions` et `SmartMarkerProcessor`.
* Un IDE tel que Visual Studio 2022 (tout éditeur capable de compiler du C# convient).

Ajoutez le package NuGet à votre projet :

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Étape 1 : Créer le classeur Excel et configurer la première feuille

La première tâche consiste à **créer un classeur Excel** et à obtenir une référence à la feuille de calcul par défaut. Cette feuille hébergera le tableau dynamique et le modèle Smart Marker.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Pourquoi c’est important* : L’instanciation de `Workbook` alloue la structure interne du classeur, tandis que l’accès à `Worksheets[0]` vous fournit une feuille prête à l’emploi sans avoir à en ajouter une manuellement.

## Étape 2 : Déverser le tableau dynamique avec la fonction EXPAND

La **fonction EXPAND** d’Excel peut transformer un littéral de tableau statique en une plage de débordement de n’importe quelle taille. Ici, nous demandons à Excel d’étendre `{1,2,3}` en une plage de 5 lignes × 1 colonne à partir de `A1`.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Pourquoi c’est important* : Utiliser `EXPAND` évite les boucles manuelles en C#. Le moteur calcule la plage de débordement et stocke les valeurs directement dans la feuille, qui apparaîtront ensuite dans le PDF.

## Étape 3 : Enregistrer le classeur au format PDF tout en préservant les sélecteurs de variation de police

Lorsque vous devez **enregistrer le classeur au format PDF**, vous pouvez également activer les fonctionnalités typographiques avancées telles que les sélecteurs de variation de police (disponibles depuis Aspose.Cells v25.8). Cela garantit que les PDF rendent correctement les scripts complexes.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Pourquoi c’est important* : Définir `FontVariationSelectors` à `true` est essentiel pour les langues qui reposent sur la variation de glyphe (par ex., le chinois, le japonais, les emojis). Le PDF produit reflète la vue Excel à l’écran.

## Étape 4 : Insérer un modèle Smart Marker qui référence une source de données imbriquée

Les Smart Markers vous permettent d’insérer des espaces réservés directement dans la feuille. Le modèle ci‑dessous générera une liste de commandes et leurs articles.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Pourquoi c’est important* : En plaçant le modèle dans `A1`, vous indiquez à Aspose.Cells où commencer à développer les données. La syntaxe `:` (`Items:ItemName`) indique au processeur d’itérer sur une collection imbriquée.

## Étape 5 : Définir la source de données imbriquée (commandes contenant des articles)

Nous créons un tableau anonyme de commandes, chacune contenant sa propre collection d’objets article. Cela reflète un scénario maître‑détail typique.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Pourquoi c’est important* : La structure imbriquée montre **comment créer un tableau dynamique dans Excel** via les Smart Markers, sans écrire de VBA ni de boucles de cellules manuelles.

## Étape 6 : Traiter les Smart Markers et enregistrer le fichier Excel final

Nous transmettons maintenant le classeur et la source de données à `SmartMarkerProcessor`. Après le traitement, les espaces réservés sont remplacés par les lignes réelles, et nous enregistrons le résultat sous forme de fichier `.xlsx` ordinaire.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Pourquoi c’est important* : `SmartMarkerProcessor` développe automatiquement le modèle, crée les lignes nécessaires et les remplit avec les données. Le classeur final peut être ouvert dans Excel pour vérifier que chaque commande et ses articles apparaissent correctement.

## Résultat attendu

* **VarSelector.pdf** – un fichier PDF qui montre les nombres 1‑3 se déversant sur cinq lignes, rendu avec les variations OpenType que vous avez activées.
* **NestedSmartMarker.xlsx** – un fichier Excel contenant les lignes suivantes (à partir de `A1`) :

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

La version PDF conserve le même débordement numérique parce que l’état de la feuille a été sauvegardé avant le traitement des Smart Markers ; vous pouvez répéter l’enregistrement PDF après le traitement si vous avez besoin des données finales en PDF également.

## Astuces professionnelles et pièges courants

| Astuce | Explication |
|--------|-------------|
| **Réutiliser le même `PdfSaveOptions`** | Créer l’objet d’options une fois et le réutiliser évite des différences subtiles de rendu (par ex., des sélecteurs de variation manquants). |
| **Appeler `ws.Calculate()` après avoir défini les formules** | Sans calcul explicite, la plage de débordement peut rester vide lors de l’inspection du classeur par programme. |
| **Placer les modèles Smart Marker sur une feuille propre** | Mélanger les modèles avec des données existantes peut entraîner des insertions de lignes inattendues. Utilisez une feuille dédiée si possible. |
| **Faire attention aux chemins de fichiers** | Utilisez `Path.Combine(Environment.CurrentDirectory, "output.pdf")` pour éviter les répertoires codés en dur sur différentes machines. |
| **Vérifier la version** | `FontVariationSelectors` n’est disponible qu’à partir de la version 25.8 ; les versions antérieures ignoreront la propriété sans lever d’exception. |

## Prochaines étapes

Maintenant que vous savez comment **créer un classeur Excel**, **déverser un tableau dynamique**, et **enregistrer le classeur au format PDF**, vous pouvez explorer :

* Ajouter des graphiques ou des images avant la conversion en PDF.
* Exporter le même classeur vers d’autres formats (par ex., HTML, CSV) en utilisant les surcharges de `Save`.
* Utiliser les **expressions Smart Marker** (`${Orders.Total:SUM(Items.Price)}`) pour calculer des agrégats à la volée.
* Intégrer ce code dans une API ASP.NET Core afin que les utilisateurs puissent télécharger le PDF généré directement depuis un point de terminaison web.

---

**Résumé** – Ce tutoriel vous a montré comment **créer un classeur Excel**, utiliser la **fonction EXPAND** pour **déverser un tableau dynamique**, intégrer un **Smart Marker** fonctionnant avec une source de données imbriquée, puis **enregistrer le classeur au format PDF** tout en préservant les fonctionnalités avancées des polices. L’exemple complet et exécutable peut être copié dans n’importe quel projet C# et adapté à vos propres structures de données. Bon codage !

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}