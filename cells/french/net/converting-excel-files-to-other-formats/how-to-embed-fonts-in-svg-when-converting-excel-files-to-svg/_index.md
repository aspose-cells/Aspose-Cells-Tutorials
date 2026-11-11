---
category: general
date: 2026-09-15
description: Apprenez à incorporer des polices dans les SVG et à exporter un graphique
  Excel vers PowerPoint, en couvrant la conversion de XLSX en SVG et la conversion
  de XLSX en PPTX avec des exemples de code complets.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: fr
lastmod: 2026-09-15
og_description: Intégrez les polices dans le SVG et exportez le graphique Excel vers
  PowerPoint avec du code C# étape par étape. Convertissez XLSX en SVG et XLSX en
  PPTX rapidement et de manière fiable.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Intégrer des polices dans SVG et exporter un graphique Excel vers PowerPoint
  – guide complet
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment intégrer des polices dans le SVG lors de la conversion de fichiers
  Excel en SVG et PowerPoint
url: /fr/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment intégrer des polices dans SVG lors de la conversion de fichiers Excel en SVG et PowerPoint  

Si vous devez **intégrer des polices dans SVG** lors de la conversion d’un classeur Excel, ce guide vous montre exactement comment le faire. Vous apprendrez également comment **exporter un graphique Excel vers PowerPoint**, et comment **convertir XLSX en SVG** ainsi que **convertir XLSX en PPTX** avec des graphiques éditables.  

Travailler avec les données Excel de façon programmatique signifie souvent qu’il faut déplacer le même contenu visuel entre différents formats de fichier. Recréer manuellement un graphique dans PowerPoint ou réappliquer les polices dans un SVG est source d’erreurs et chronophage. À la fin de ce tutoriel, vous disposerez d’un extrait C# unique et réutilisable qui :

* Enregistre un classeur au format SVG avec les polices et les sélecteurs de variation de police intégrés.  
* Exporte le même classeur au format PPTX où le graphique reste éditable.  

Le seul prérequis est une version récente de **Aspose.Cells for .NET** (2024‑x ou ultérieure) et un environnement de développement .NET tel que Visual Studio 2022.

---

## Ce dont vous aurez besoin  

* .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.8).  
* Le package NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  
* Un fichier Excel (`input.xlsx`) contenant au moins un graphique.  
* Le droit d’écriture sur le répertoire de sortie.  

---

## Intégrer des polices dans SVG lors de la conversion XLSX en SVG  

L’intégration des polices garantit que le SVG s’affiche correctement sur n’importe quel appareil, même si le système cible ne possède pas les polices d’origine. La classe `SvgSaveOptions` fournit deux indicateurs qui rendent cela possible : `EmbedFonts` et `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Pourquoi cela fonctionne :**  
* `EmbedFonts = true` copie les fichiers de police dans la section `<defs>` du SVG, éliminant les dépendances externes.  
* `FontVariationSelectors = true` ajoute les sélecteurs nécessaires pour les polices qui supportent les fonctionnalités OpenType, préservant les variantes de glyphes telles que les ligatures.  

**Résultat attendu :** Ouvrez `WithFonts.svg` dans n’importe quel navigateur moderne ; le texte du graphique ou des cellules apparaît avec la police exacte utilisée dans Excel, même sur des machines qui n’ont pas cette police installée.

---

## Exporter un graphique Excel vers PowerPoint avec des graphiques éditables  

Lorsque vous devez intégrer un graphique dans une diapositive PowerPoint tout en permettant au destinataire de modifier les données du graphique, le `PptxSaveOptions` d’Aspose.Cells propose l’indicateur `ExportEditableChart`.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Pourquoi c’est important :**  
Définir `ExportEditableChart` à `true` stocke le graphique comme un objet de graphique Office Open XML plutôt que comme une image statique. Lorsque vous ouvrez `EditableChart.pptx` dans PowerPoint, vous pouvez faire un clic droit sur le graphique → **Edit Data** et modifier les séries comme pour un graphique PowerPoint natif.

**Étapes de vérification :**  

1. Ouvrez `EditableChart.pptx` dans PowerPoint.  
2. Localisez la diapositive contenant le graphique.  
3. Choisissez **Chart Tools → Design → Edit Data**.  
4. Confirmez que la grille de données de type Excel apparaît et que vous pouvez modifier les valeurs.

---

## Convertir XLSX en SVG – récapitulatif du flux complet  

Voici une version compacte qui combine le chargement, la manipulation éventuelle des données, et l’enregistrement en SVG. Utilisez‑la lorsque vous avez uniquement besoin du rendu SVG.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

Appelez la méthode ainsi :

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Astuce pour les cas limites :** Si votre classeur contient des polices personnalisées qui ne sont pas installées sur le serveur, intégrez‑les manuellement avant d’appeler `Save`. Utilisez `FontInfoCollection` pour ajouter les fichiers de police aux `SvgSaveOptions` via la propriété `CustomFonts` (disponible dans les versions récentes d’Aspose.Cells).

---

## Convertir XLSX en PPTX – préservation de l’éditabilité du graphique  

La méthode d’assistance suivante montre le chemin **convert XLSX to PPTX** tout en garantissant que le graphique reste éditable.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Utilisation :

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Question fréquente :** *Et si mon classeur possède plusieurs feuilles avec des graphiques ?*  
**Réponse :** Aspose.Cells exporte la première feuille par défaut. Pour inclure des feuilles supplémentaires, parcourez `workbook.Worksheets`, copiez chaque graphique sur une nouvelle diapositive, et enregistrez chaque diapositive individuellement à l’aide des objets `Presentation` d’Aspose.Slides. Ce scénario avancé dépasse le flux de base « save workbook as SVG » et « export Excel chart to PowerPoint », mais les indicateurs principaux restent les mêmes.

---

## Conseils pratiques et pièges courants  

* **Performance :** L’intégration des polices augmente la taille du fichier SVG. Si la taille est un problème, définissez `EmbedFonts = false` et utilisez des polices web‑safe.  
* **Licence des polices :** Assurez‑vous de disposer des droits nécessaires pour intégrer les polices que vous utilisez ; certaines polices commerciales restreignent l’intégration.  
* **Compatibilité des graphiques :** Les graphiques éditables sont enregistrés comme parties `chart.xml` à l’intérieur du PPTX. Les graphiques très complexes (par ex. 3‑D ou combinés) peuvent perdre une partie du style lorsqu’ils sont modifiés dans PowerPoint. Testez les types de graphiques les plus courants dont vous avez besoin.  
* **Incohérences de version :** L’indicateur `ExportEditableChart` nécessite Aspose.Cells 20.10 ou ultérieur. Une version antérieure reviendra silencieusement à une image raster.  
* **Sécurité des threads :** Les objets `Workbook` ne sont pas thread‑safe. Créez une nouvelle instance `Workbook` par requête dans un scénario de service web.  

---

## Exemple complet de bout en bout  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

L’exécution de ce programme produit deux fichiers :

* **WithFonts.svg** – un SVG qui s’affiche exactement comme la vue Excel, polices incluses.  
* **EditableChart.pptx** – une présentation PowerPoint où le graphique peut être édité directement.

---

## Conclusion  

Vous savez maintenant comment **intégrer des polices dans SVG** lorsque vous **convertissez XLSX en SVG**, et comment **exporter un graphique Excel vers PowerPoint** tout en conservant le graphique éditable. Le même code montre également une façon propre de **sauvegarder un classeur en SVG** et de **convertir XLSX en PPTX** avec un effort minimal.  

À partir d’ici, vous pouvez explorer des sujets supplémentaires tels que :

* Ajouter des polices personnalisées par programme (`svgOptions.CustomFonts`).  
* Traiter en lot plusieurs classeurs dans un service en arrière‑plan.  
* Utiliser Aspose.Slides pour créer des fichiers PPTX multi‑diapositives combinant plusieurs graphiques Excel.  

Expérimentez avec les options, adaptez les extraits à votre projet, et profitez de conversions fiables d’Excel vers SVG/PPTX sans post‑traitement manuel. Bon codage !


## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}