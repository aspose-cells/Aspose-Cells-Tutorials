---
category: general
date: 2026-06-30
description: Créez une sparkline en ligne dans Excel avec C# rapidement. Apprenez
  comment ajouter une sparkline, créer un classeur Excel en C# et ajouter une sparkline
  à une cellule en quelques étapes.
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: fr
og_description: Créer une sparkline en ligne dans Excel avec C#. Ce tutoriel montre
  comment ajouter une sparkline, créer un classeur Excel en C# et intégrer la sparkline
  dans une cellule.
og_title: Créer une sparkline de type ligne dans Excel avec C# – Guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Créer une sparkline de type ligne dans Excel avec C# – Guide complet de programmation
url: /fr/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer line sparkline dans Excel avec C# – Guide complet de programmation

Vous vous êtes déjà demandé comment **create line sparkline** dans un fichier Excel en utilisant C# ? Vous n'êtes pas le seul — les développeurs demandent constamment « comment ajouter une sparkline à un rapport sans ouvrir Excel manuellement ? ». La bonne nouvelle, c’est qu’avec quelques lignes de code vous pouvez générer une line sparkline élégante directement dans le classeur, sans interface utilisateur.

Dans ce tutoriel, nous passerons en revue tout ce que vous devez savoir : des bases de **create Excel workbook C#**, en passant par le remplissage des données, jusqu’aux étapes précises pour **add line sparkline** et **add sparkline to cell**. À la fin, vous disposerez d’un fichier *.xlsx* prêt à l’emploi qui visualise les tendances de ventes mensuelles d’un seul coup d’œil. Pas de blabla, juste une solution pratique et exécutable.

---

## Ce que vous allez créer

- Un nouveau classeur Excel nommé *KPI_Sparklines.xlsx*  
- Une feuille de calcul appelée **KPI** contenant des chiffres de ventes d’exemple  
- Une **line sparkline** placée dans la cellule **D2** qui fait référence à la plage de données **B2:B13**  
- Un formatage de base (couleur, épaisseur de ligne) pour faire ressortir la sparkline  

Prérequis ? Juste le .NET SDK (3.1+ ou .NET 6) et la bibliothèque gratuite Aspose.Cells for .NET (disponible via NuGet). Si vous n’avez jamais utilisé Aspose.Cells auparavant, pensez‑y comme à un moteur Excel puissant que vous pouvez appeler depuis le code — pas d’interop COM, pas d’installation d’Excel requise.

---

![Create line sparkline in Excel using C#](https://example.com/images/create-line-sparkline.png "Créer line sparkline dans Excel avec C#")

*Texte alternatif de l’image : créer line sparkline dans Excel en utilisant du code C#*

---

## Étape 1 : **Create Excel workbook C#** – Configurer le fichier et la feuille

Tout d’abord. Nous avons besoin d’un objet workbook et d’une worksheet où les données seront stockées. C’est la base de toute automatisation Excel, que vous ajoutiez plus tard une **add line sparkline** ou que vous écriviez des formules.

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **Pourquoi c’est important :** La classe `Workbook` représente le fichier complet, tandis que `Worksheet` est la toile pour les lignes, colonnes et, finalement, notre sparkline. Nommer la feuille dès le départ garde le fichier propre et auto‑documenté.

---

## Étape 2 : Remplir les données – La plage source pour la sparkline

Une sparkline a besoin de données à tracer. Simulons 12 mois de chiffres de ventes. Vous pourriez les extraire d’une base de données, mais pour plus de clarté nous les générerons à la volée.

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **Astuce :** `PutValue` détecte automatiquement le type de donnée, vous n’avez donc pas besoin de le convertir en `double` ou `int`. Si vous devez formater les cellules (monnaie, séparateur de milliers), vous pourrez appliquer un objet `Style` plus tard.

---

## Étape 3 : **Create line sparkline** – Ajouter la sparkline à une cellule précise

Voici la star du spectacle : la **line sparkline**. Aspose.Cells regroupe les sparklines, nous créons donc d’abord un `SparklineGroup` de type `Line`, puis indiquons où placer le visuel.

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **Comment ça fonctionne :**  
> - `firstRow/firstColumn` et `lastRow/lastColumn` définissent la *cellule cible* (où la sparkline apparaît).  
> - `firstDataRow/lastDataRow` pointent vers la plage source.  
> Parce que nous utilisons une **line sparkline**, le visuel sera une simple ligne fine qui suit la tendance des nombres.

### Optionnel : **How to add sparkline** avec un style personnalisé

Si vous voulez que la sparkline se démarque, ajustez quelques propriétés :

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **Pourquoi le styliser ?** Une ligne bleu foncé sur fond blanc est agréable pour les yeux, tandis que les marqueurs donnent un indice rapide sur les points de données individuels—pratique pour les présentations.

---

## Étape 4 : Enregistrer le classeur – Vérifier le résultat

Avec la sparkline en place, il ne reste plus qu’à écrire le fichier sur le disque. Choisissez un dossier où vous avez les droits d’écriture ; l’exemple utilise un chemin factice que vous devez remplacer.

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **Vérification :** Ouvrez le fichier généré dans Excel (ou tout visualiseur supportant le .xlsx). Vous devriez voir une **line sparkline** dans la cellule **D2** qui reflète la hausse des ventes dans la colonne **B**. En survolant la sparkline, une info-bulle affichera les valeurs sous‑jacentes.

---

## Étape 5 : Pièges courants lors de l’**add sparkline to cell**

Même un exemple simple peut surprendre les débutants. Voici quelques points à surveiller :

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Coordonnées de cellule incorrectes | La cible de la sparkline utilise un indice de colonne zéro‑based mais un indice de ligne un‑based. | Rappelez‑vous que `Cells[row, column]` où `row` est zéro‑based, `column` l’est également. Dans `SparklineGroup.Add`, les lignes et colonnes sont **1‑based**. |
| Aucune donnée affichée | La plage source est vide ou contient des valeurs non numériques. | Assurez‑vous que la plage (par ex. `B2:B13`) contient des nombres. Utilisez `PutValue` avec des types numériques. |
| La sparkline disparaît après l’enregistrement | Incompatibilité de version de la bibliothèque ou licence manquante. | Utilisez la dernière version du package Aspose.Cells et fournissez une licence valide si vous dépassez les limites d’évaluation. |
| Le formatage n’est pas appliqué | Les changements de style ont été faits avant d’ajouter la sparkline. | Appliquez le style **après** la création du groupe, comme montré ci‑dessus. |

---

## Code source complet – Copiez‑collez en une fois

Voici le programme complet, prêt à être exécuté. Collez‑le dans un nouveau projet console, ajoutez le package NuGet Aspose.Cells, puis appuyez sur **F5**.

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Résultat attendu :** Lorsque vous ouvrez *KPI_Sparklines.xlsx*, la colonne **B** répertorie douze nombres (5 000 → 13 250) et la cellule **D2** contient une line sparkline bleu foncé lisse qui monte régulièrement. Les marqueurs apparaissent comme de petits points orange‑rouge si vous avez activé `ShowMarkers`.

---

## Et après ? Étendre vos compétences en sparkline

Maintenant que vous avez maîtrisé **create line sparkline** avec Aspose.Cells, envisagez d’explorer ces sujets connexes :

- **Add column sparkline** – idéal pour afficher des données empilées.  
- **Create multi‑sparkline groups** sur la même feuille pour des comparaisons côte à côte.  
- **Export to PDF** tout en conservant les sparklines (Aspose.Cells prend en charge la conversion PDF).  
- **Dynamic data sources** – extraire les vraies ventes depuis une base de données SQL au lieu de valeurs codées en dur.  

Chacun de ces points s’appuie sur les mêmes concepts de base : **create Excel workbook C#**, remplir les données, et **add sparkline to cell** dans le style souhaité.

---

### TL;DR

Nous avons montré comment **create line sparkline** dans un classeur Excel en utilisant C#. Les étapes—*create workbook, fill data, add sparkline, style it, and save*—sont toutes encapsulées dans un programme autonome. N’hésitez pas à ajuster les couleurs, l’épaisseur de ligne ou la plage source pour répondre à vos besoins de reporting.

Vous avez une variante à partager ? Laissez un commentaire ci‑dessous, et bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}