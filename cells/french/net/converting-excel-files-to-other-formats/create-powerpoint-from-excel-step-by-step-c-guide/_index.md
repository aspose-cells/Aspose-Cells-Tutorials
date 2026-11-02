---
category: general
date: 2026-03-30
description: Créez PowerPoint à partir d’Excel rapidement avec Aspose.Cells et Aspose.Slides.
  Apprenez à exporter la feuille de calcul en image et à enregistrer la présentation
  au format PPTX en C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: fr
og_description: Créer un PowerPoint à partir d’Excel en C# avec Aspose. Exporter la
  feuille de calcul en image, conserver les formes éditables et enregistrer le résultat
  au format PPTX.
og_title: Créer un PowerPoint à partir d'Excel – Tutoriel complet C#
tags:
- Aspose
- C#
- Office Automation
title: Créer PowerPoint à partir d’Excel – Guide C# étape par étape
url: /fr/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PowerPoint à partir d’Excel – Tutoriel complet en C#

Vous avez déjà eu besoin de **créer un PowerPoint à partir d’Excel** sans savoir quelle bibliothèque pouvait garder vos graphiques modifiables ? Vous n’êtes pas seul. Dans de nombreux scénarios de reporting, vous souhaiterez transformer une feuille de calcul en diaporama sans perdre la possibilité d’ajuster les zones de texte plus tard. Ce guide vous montre exactement comment **convertir Excel en PowerPoint** en utilisant Aspose.Cells et Aspose.Slides, tout en expliquant comment **exporter la feuille de calcul en image** et enfin **enregistrer la présentation au format PPTX**.

Nous passerons en revue chaque ligne de code, expliquerons *pourquoi* chaque paramètre est important, et discuterons même de ce qu’il faut faire si votre classeur contient des graphiques complexes que vous préférez exporter sous forme d’image. À la fin, vous disposerez d’une application console C# prête à l’emploi qui prend `ShapesDemo.xlsx` et génère `Result.pptx` – le tout avec des zones de texte éditables et des images nettes.

## Ce dont vous avez besoin

- .NET 6.0 ou version ultérieure (l’API fonctionne aussi avec le .NET Framework, mais .NET 6 est le meilleur compromis).  
- Packages NuGet **Aspose.Cells** et **Aspose.Slides** (les licences d’essai gratuites suffisent pour les tests).  
- Une connaissance de base de la syntaxe C# – si vous savez écrire un `Console.WriteLine`, vous êtes prêt.  

Pas d’interop COM supplémentaire, pas d’Office installé sur le serveur, et pas de copier‑coller manuel d’images. Tout est géré programmétiquement.

---

## Créer un PowerPoint à partir d’Excel – Charger le classeur et définir les options d’exportation

La première chose que nous faisons est d’ouvrir le fichier Excel et d’indiquer à Aspose.Cells comment nous voulons que la feuille soit rendue. L’objet `ImageOrPrintOptions` est où la magie opère : nous activons `ExportShapes` et `ExportEditableTextBoxes` afin que toutes les formes (y compris les graphiques) deviennent partie de la diapositive **et** restent éditables après la conversion.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**Pourquoi ces indicateurs ?**  
- `OnePagePerSheet` empêche la feuille d’être découpée en plusieurs diapositives – vous obtenez une image unique, pleine taille.  
- `ExportShapes` indique à Aspose.Cells de rasteriser les graphiques *et* les formes vectorielles, en préservant leur apparence.  
- `ExportEditableTextBoxes` est le secret qui vous permet de double‑cliquer sur une zone de texte dans PowerPoint et de modifier le texte sans rouvrir Excel.

> **Astuce pro :** Si vous avez seulement besoin d’une image statique d’un graphique, définissez `ExportShapes = false` et utilisez la méthode `ExportExcelChartAsPicture` plus tard (voir la section finale).

---

## Convertir Excel en PowerPoint – Générer une image à partir de la feuille

Avec les options prêtes, nous transformons maintenant la feuille en un `System.Drawing.Image`. Le `WorksheetToImageConverter` fait le gros du travail, en appliquant les paramètres que nous venons de définir.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

L’argument `0` indique la première page (nous n’en avons qu’une grâce à `OnePagePerSheet`). L’`sheetImage` résultante conserve le DPI d’origine, de sorte que votre diapositive ne paraîtra pas pixelisée même sur des écrans haute résolution.

---

## Enregistrer la présentation au format PPTX – Insérer l’image dans une diapositive

Nous créons maintenant un nouveau fichier PowerPoint, ajoutons une diapositive, et déposons le bitmap dessus. Aspose.Slides traite l’image comme une forme *picture frame*, que vous pouvez redimensionner ou déplacer comme n’importe quel objet natif de PowerPoint.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **Et si l’image est plus grande que la diapositive ?**  
> PowerPoint découpera automatiquement tout ce qui dépasse les dimensions de la diapositive. Une solution rapide consiste à redimensionner l’image avant de l’insérer :

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

Vous pouvez alors passer `newWidth` et `newHeight` à `AddPictureFrame`.

---

## Exporter la feuille de calcul en image – Enregistrer le fichier PPTX

Enfin, nous persistons la présentation sur le disque. Le drapeau `SaveFormat.Pptx` garantit le format moderne OpenXML, qui fonctionne avec toutes les versions récentes de PowerPoint.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

Lorsque vous ouvrez `Result.pptx`, vous verrez une seule diapositive qui ressemble exactement à votre feuille Excel, mais vous pourrez toujours cliquer sur n’importe quelle zone de texte et modifier son contenu directement dans PowerPoint.

---

## Exporter le graphique Excel en image – Quand les images raster sont préférées

Parfois, vous n’avez pas besoin de formes éditables ; un PNG de haute qualité d’un graphique suffit. Aspose.Cells peut exporter un graphique spécifique en image sans convertir toute la feuille :

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

Vous pouvez alors intégrer `chart.png` dans une diapositive de la même façon que nous avons ajouté `sheetImage`. Cette approche réduit la taille du fichier PPTX et est utile lorsque les données environnantes ne sont pas nécessaires sur la diapositive.

---

## Pièges courants & comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Le texte apparaît flou** | Exporté à un DPI faible (96 par défaut). | Définir `imageOptions.Dpi = 300;` avant la conversion. |
| **Les formes disparaissent** | `ExportShapes` laissé à `false`. | S’assurer que `ExportShapes = true` lorsque vous avez besoin de graphiques éditables. |
| **Mauvaise correspondance de taille de diapositive** | Image plus grande que les dimensions de la diapositive. | Redimensionner l’image (voir l’extrait de code) ou modifier la taille de la diapositive via `presentation.SlideSize`. |
| **Exception de licence** | Utilisation de la version d’essai sans activation correcte. | Appeler `License license = new License(); license.SetLicense("Aspose.Total.lic");` tôt dans `Main`. |

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet, prêt à être placé dans un nouveau projet console. Remplacez `YOUR_DIRECTORY` par le dossier contenant votre fichier Excel.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**Sortie attendue :**  
L’exécution du programme affiche `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`. L’ouverture du PPTX montre une seule diapositive reproduisant la feuille Excel d’origine, avec des zones de texte éditables.

---

## Récapitulatif & étapes suivantes

Vous savez maintenant comment **créer un PowerPoint à partir d’Excel** en utilisant les API puissantes d’Aspose, comment **exporter la feuille de calcul en image**, et comment **enregistrer la présentation au format PPTX** tout en préservant l’éditabilité. Le même schéma fonctionne pour les classeurs multi‑feuilles — il suffit de boucler sur `workbook.Worksheets` et d’ajouter une nouvelle diapositive pour chacune.

**Que pouvez‑vous explorer ensuite ?**  

- **Conversion par lots :** Parcourir un dossier de fichiers Excel et générer un diaporama par fichier.  
- **Mises en page dynamiques :** Utiliser `slide.LayoutSlide` pour appliquer des modèles PowerPoint pré‑conçus.  
- **Exportation de graphiques uniquement :** Combiner le fragment « Export Excel chart as picture » avec des espaces réservés de diapositive pour un deck plus léger.  
- **Style avancé :** Appliquer des arrière‑plans de diapositive personnalisés, des transitions ou des animations via Aspose.Slides.

N’hésitez pas à expérimenter — modifiez le DPI, remplacez `ShapeType.Ellipse` par un cadre circulaire, ou même intégrez plusieurs images par diapositive. Le ciel est la limite quand vous avez le contrôle programmatique sur

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}