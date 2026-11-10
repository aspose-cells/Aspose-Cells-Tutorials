---
category: general
date: 2026-10-01
description: Apprenez comment intégrer des polices dans le HTML lors de la conversion
  d’Excel en HTML avec Aspose.Cells. Exportez Excel en HTML avec des polices intégrées
  en quelques étapes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: fr
lastmod: 2026-10-01
og_description: Comment intégrer des polices dans le HTML lors de l’exportation de
  fichiers Excel. Suivez ce guide étape par étape pour convertir Excel en HTML avec
  des polices intégrées.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: Comment intégrer des polices dans HTML à partir d'Excel – Guide Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Comment intégrer des polices lors de la conversion d’Excel en HTML avec Aspose.Cells
url: /fr/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment intégrer des polices lors de la conversion d'Excel en HTML avec Aspose.Cells

Intégrer des polices dans le HTML lors de la conversion d’un classeur Excel est essentiel pour préserver l’aspect original sur tous les navigateurs. Si vous devez convertir Excel en HTML tout en conservant les polices personnalisées, ce guide montre le processus complet. Vous verrez également comment exporter Excel en HTML et pourquoi l’intégration des polices dans le HTML est importante pour un rendu cohérent.

Ce tutoriel couvre tout ce que vous devez savoir : bibliothèques requises, configuration du code et vérification du fichier HTML généré. À la fin, vous pourrez exporter Excel en HTML avec des polices intégrées en quelques lignes de C#.

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d’avoir :

* **.NET 6.0 ou version ultérieure** – le code cible .NET 6, mais toute version de .NET qui prend en charge Aspose.Cells fonctionne.
* **Aspose.Cells for .NET** – obtenez une licence ou utilisez la version d’évaluation gratuite depuis le site d’Aspose.
* Un environnement de développement **C#** (Visual Studio, Rider ou VS Code) – tout IDE capable de compiler des projets .NET.
* Un classeur Excel (`Styled.xlsx`) qui utilise les polices personnalisées que vous souhaitez conserver.

## Étape 1 : Configurer Aspose.Cells dans votre projet .NET

Tout d’abord, ajoutez le package NuGet Aspose.Cells à votre projet :

```bash
dotnet add package Aspose.Cells
```

Ensuite, incluez l’espace de noms en haut de votre fichier C# :

```csharp
using Aspose.Cells;
```

L’ajout du package rend les classes `Workbook`, `HtmlSaveOptions` et les classes associées disponibles.

## Étape 2 : Charger le classeur Excel

Le chargement du classeur est la première étape concrète dans **comment exporter les données Excel**. Le constructeur `Workbook` lit le fichier depuis le disque :

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*Pourquoi c’est important :* Aspose.Cells analyse le classeur, y compris les styles de cellules, les formules et les informations de police. Si le fichier est introuvable, une exception est levée, assurez‑vous donc que le chemin est correct.

## Étape 3 : Configurer les options de sauvegarde HTML pour intégrer les polices

Le cœur de **l’intégration des polices dans le HTML** réside dans la classe `HtmlSaveOptions`. Réglez `EmbedFonts` sur `true` afin que chaque police utilisée dans le classeur soit écrite dans la sortie HTML sous forme de règle `@font-face` encodée en Base64.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*Pourquoi c’est important :* Par défaut, Aspose.Cells référence des fichiers de police externes, qui peuvent ne pas être disponibles sur la machine cliente. Activer `EmbedFonts` garantit que le HTML rendu ressemble exactement à la feuille Excel originale, quel que soit le jeu de polices installé chez le lecteur.

### Cas particulier : polices non prises en charge

Si le classeur utilise une police qui n’est pas installée sur le serveur, Aspose.Cells revient à une police système par défaut. Pour éviter cela, installez les polices requises sur le serveur ou intégrez‑les manuellement après l’exportation.

## Étape 4 : Enregistrer le classeur au format HTML avec les options configurées

Vous pouvez maintenant écrire le fichier HTML. La méthode `Save` prend le chemin de sortie et l’instance `HtmlSaveOptions` :

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

Après exécution, `Styled.html` contient les données de la feuille de calcul ainsi qu’un bloc `<style>` avec les définitions `@font-face` encodées en Base64 pour chaque police personnalisée.

## Étape 5 : Vérifier les polices intégrées

Ouvrez `Styled.html` dans un navigateur. Inspectez la section `<head>` ; vous devriez voir quelque chose comme :

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

Si les polices s’affichent correctement dans le tableau rendu, l’intégration a réussi. Si vous remarquez des glyphes manquants, revérifiez que les fichiers de police source sont installés sur la machine qui effectue la conversion.

## Variantes courantes et options supplémentaires

### Conversion de plusieurs feuilles de calcul

Si vous devez **convertir Excel en HTML** pour toutes les feuilles, définissez `ExportActiveWorksheetOnly = false` (valeur par défaut). Aspose.Cells créera un fichier HTML séparé pour chaque feuille.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### Contrôle de la sortie CSS

Vous pouvez réduire la taille du HTML en désactivant le CSS en ligne :

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### Utiliser un flux au lieu d’un fichier

Lors de l’intégration dans une API web, écrivez le HTML dans un `MemoryStream` et renvoyez‑le directement :

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## Astuce pro : licence du produit pour supprimer les filigranes d’évaluation

Si vous utilisez la version d’évaluation, le HTML généré peut contenir un commentaire de filigrane. Appliquez votre licence Aspose.Cells avant de charger le classeur afin de produire une sortie propre :

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## Exemple complet fonctionnel

Voici un programme complet et exécutable qui montre **comment intégrer des polices**, **convertir Excel en HTML** et **exporter Excel en HTML** en une seule opération :

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**Résultat attendu :** Après l’exécution du programme, `Styled.html` apparaît dans `YOUR_DIRECTORY`. L’ouverture du fichier dans n’importe quel navigateur moderne montre la feuille de calcul avec les mêmes polices que le fichier Excel original, même sur des machines qui ne possèdent pas ces polices.

## Conclusion

Vous savez maintenant **comment intégrer des polices** lorsque vous **convertissez Excel en HTML** avec Aspose.Cells, et vous avez vu le flux complet depuis le chargement du classeur jusqu’à la vérification des polices intégrées. Cette approche garantit que la fidélité visuelle de vos fichiers Excel est conservée dans le HTML généré, ce qui est idéal pour les rapports web, les newsletters par e‑mail ou tout scénario où vous devez **exporter Excel en HTML** avec une typographie personnalisée.

Ensuite, explorez des sujets connexes tels que **l’exportation d’Excel en PDF**, **la mise en forme de la sortie HTML avec du CSS personnalisé**, ou **le traitement par lots de plusieurs classeurs**. Chacun de ces cas s’appuie sur le même modèle `HtmlSaveOptions`, vous permettant d’adapter le code avec peu de modifications.

Bon codage !

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment exporter Excel en HTML – Guide étape par étape](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [Comment intégrer des polices dans le HTML – Guide complet C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [Comment intégrer des polices lors de la conversion d’Excel en PDF – Guide étape par étape](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}