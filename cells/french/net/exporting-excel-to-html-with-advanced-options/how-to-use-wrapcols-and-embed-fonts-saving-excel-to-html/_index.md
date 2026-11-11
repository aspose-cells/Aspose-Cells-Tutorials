---
category: general
date: 2026-10-20
description: Apprenez à utiliser wrapcols dans Aspose.Cells, à intégrer des polices
  dans le HTML et à enregistrer Excel au format HTML avec un exemple complet en C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: fr
lastmod: 2026-10-20
og_description: Comment utiliser wrapcols dans Aspose.Cells, incorporer des polices
  dans le HTML et convertir un classeur en HTML avec un guide C# clair pour les développeurs.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Comment utiliser wrapcols et incorporer les polices lors de l'exportation
  d'Excel vers HTML
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Comment utiliser wrapcols et intégrer les polices lors de l’enregistrement
  d’Excel au format HTML
url: /fr/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser wrapcols et incorporer des polices lors de l’enregistrement d’Excel en HTML

Si vous devez **utiliser wrapcols** dans une formule Aspose.Cells, ce guide vous montre les étapes exactes. Vous apprendrez également comment **incorporer des polices dans le HTML** et **enregistrer Excel en HTML** afin que le rendu soit identique sur tous les navigateurs.  

Le tutoriel couvre trois scénarios pratiques : utilisation de la fonction `WRAPCOLS`, exportation d’un classeur avec des polices incorporées, et génération d’un rapport maître‑détail avec Smart Markers. À la fin, vous disposerez d’un programme C# unique et exécutable qui démontre toutes ces fonctionnalités.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 (ou version ultérieure) installé.
* Aspose.Cells for .NET ajouté à votre projet (`dotnet add package Aspose.Cells`).
* Familiarité de base avec C# et les formules Excel.

Aucune bibliothèque tierce supplémentaire n’est requise ; Aspose.Cells gère la conversion HTML et l’incorporation des polices en interne.

## Étape 1 : Démontrer la fonction **utiliser wrapcols** dans une formule

La fonction `WRAPCOLS` divise une plage unidimensionnelle en un tableau bidimensionnel, en remplissant d’abord les colonnes. Cela est utile lorsque vous devez reformater des données pour des rapports ou des graphiques.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Pourquoi cela fonctionne :**  
`WRAPCOLS` prend deux arguments – la plage source et le nombre de colonnes. La fonction remplit le tableau colonne par colonne, en ignorant les valeurs excédentaires (le `3` dans l’exemple). Le résultat apparaît dans la cellule en haut‑à‑gauche de la plage cible (`B1`), et vous pouvez étendre la plage manuellement si vous avez besoin du tableau complet.

> **Astuce :** Après avoir défini la formule, appelez `workbook.CalculateFormula()` pour vous assurer que le résultat est à jour avant de lire les valeurs des cellules.

## Étape 2 : **Convertir le classeur en HTML** et **incorporer des polices dans le html**

Lorsque vous exportez un fichier Excel en HTML, les polices sont souvent remplacées par les polices par défaut du navigateur, ce qui peut altérer la mise en page visuelle. Aspose.Cells vous permet d’incorporer les polices exactes utilisées dans le classeur directement dans le fichier HTML.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Pourquoi l’incorporation des polices est importante :**  
Lorsque `EmbedFonts` est `true`, Aspose.Cells convertit chaque police TrueType/OpenType utilisée en une règle `@font-face` encodée en Base64 dans le HTML généré. Cela élimine la nécessité pour la machine cliente d’avoir les mêmes polices installées, garantissant un rendu pixel‑parfait.

> **Cas particulier :** Si le classeur source référence une police qui n’est pas installée sur le serveur, Aspose.Cells reviendra à une police par défaut et émettra un avertissement. Assurez‑vous que les polices requises sont disponibles

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment utiliser WRAPCOLS en C# – Créer un classeur Excel avec des fonctions de wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Comment incorporer des polices dans le HTML – Convertir Excel en HTML avec C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [Comment convertir des fichiers Excel en HTML avec Aspose.Cells pour .NET : Masquer le contenu superposé](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}