---
category: general
date: 2026-09-24
description: Exporter une plage Excel en image en C# avec Aspose.Cells – guide étape
  par étape pour enregistrer une zone de feuille de calcul au format PNG ou JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- Aspose.Cells export range
- C# Excel to PNG
- ImageOrPrintOptions usage
- export pivot table as image
language: fr
lastmod: 2026-09-24
og_description: Exportez une plage Excel en image en C# avec Aspose.Cells. Apprenez
  à convertir n'importe quelle zone de feuille de calcul, y compris les tableaux croisés
  dynamiques, en PNG ou JPEG en quelques minutes.
og_image_alt: Screenshot of a C# program exporting an Excel range to a PNG image
og_title: Exporter une plage Excel en image avec C# – guide complet d’Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  headline: How to export excel range as image with C# and Aspose.Cells
  type: TechArticle
- description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  name: How to export excel range as image with C# and Aspose.Cells
  steps:
  - name: '**Load** the workbook from disk.'
    text: '**Load** the workbook from disk.'
  - name: '**Define** the cell area that will become the image (the *print area*).'
    text: '**Define** the cell area that will become the image (the *print area*).'
  - name: '**Export** the area using `ImageOrPrintOptions` and write the file.'
    text: '**Export** the area using `ImageOrPrintOptions` and write the file.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Image export
title: Comment exporter une plage Excel en image avec C# et Aspose.Cells
url: /fr/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter une plage Excel en image avec C# et Aspose.Cells

Si vous devez **exporter une plage Excel en image** dans une application .NET, ce guide vous présente une solution complète, prête à l’emploi. Que vous publiiez un tableau de bord, intégriez un tableau croisé dynamique dans une page web ou génériez une vignette de rapport, vous pouvez transformer n’importe quelle zone de feuille de calcul en PNG (ou JPEG) en quelques lignes de code C#.

Dans ce tutoriel, vous apprendrez à :

* Charger un classeur existant (`Workbook` class)  
* Définir la plage de cellules exacte que vous souhaitez capturer (`PrintArea`)  
* Configurer les options d’exportation d’image (`ImageOrPrintOptions`)  
* Enregistrer l’image résultante sur le disque  

Toutes les prérequis, cas limites et pièges courants sont couverts afin que vous puissiez adapter le code à vos propres projets sans surprise.

## Prérequis

| Exigence | Raison |
|----------|--------|
| **Aspose.Cells for .NET** (latest version) | Fournit les API `Workbook`, `Worksheet` et `ImageOrPrintOptions` utilisées dans l’exemple. |
| **.NET 6.0 or later** | L’exemple cible .NET 6, mais toute version .NET Core/Framework supportant Aspose.Cells fonctionne. |
| **A valid Excel file** (e.g., `input.xlsx`) | Le classeur que vous souhaitez convertir. |
| **Write permission to the output folder** | Nécessaire pour que `Save` réussisse. |

You can install Aspose.Cells via NuGet:

```bash
dotnet add package Aspose.Cells
```

## Exporter une plage Excel en image – aperçu du processus

L’opération se compose de trois phases logiques :

1. **Load** le classeur depuis le disque.  
2. **Define** la zone de cellules qui deviendra l’image (la *print area*).  
3. **Export** la zone en utilisant `ImageOrPrintOptions` et enregistrez le fichier.  

Chaque phase est détaillée ci‑dessous en une étape dédiée avec le code source complet et une explication.

## Étape 1 : Charger le classeur

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Path to the source Excel file
string inputPath = @"YOUR_DIRECTORY\input.xlsx";

// Create a Workbook object – this reads the file into memory
Workbook workbook = new Workbook(inputPath);
```

**Pourquoi c’est important :**  
`Workbook` est le point d’entrée pour toutes les opérations Excel. Charger le fichier une seule fois réduit l’utilisation de la mémoire et vous permet d’accéder à n’importe quelle feuille de calcul ultérieurement.

## Étape 2 : Accéder à la feuille de calcul cible

```csharp
// Get the first worksheet (index 0). Change the index or use the sheet name as needed.
Worksheet sheet = workbook.Worksheets[0];
```

**Astuce :** Si vous avez besoin d’une feuille spécifique par son nom, remplacez l’indice par `workbook.Worksheets["SheetName"]`. Cela évite les erreurs lorsque la disposition du classeur change.

## Étape 3 : Définir la plage que vous souhaitez exporter

```csharp
// Define the cell range that will be exported.
// Example: A1:G20 captures a typical pivot‑table area.
sheet.PageSetup.PrintArea = "A1:G20";
```

**Pourquoi définir `PrintArea` ?**  
Aspose.Cells rend la *print area* lors de la création d’une image. En la limitant à la plage exacte, vous évitez les espaces blancs supplémentaires et améliorez les performances.

### Alternative : Exporter la feuille entière

Si vous souhaitez exporter toute la feuille de calcul, il suffit d’omettre l’affectation de `PrintArea`. Aspose.Cells utilisera par défaut la plage utilisée de la feuille.

## Étape 4 : Configurer les options d’exportation d’image

```csharp
// Create an ImageOrPrintOptions object to control the output format.
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    // Choose PNG for lossless quality; change to Jpeg for smaller files.
    ImageFormat = ImageFormat.Png,

    // Optional: set the resolution (DPI). Higher DPI yields sharper images.
    HorizontalResolution = 300,
    VerticalResolution = 300,

    // Optional: set the page orientation if the range is wide.
    PageOrientation = PageOrientationType.Landscape
};
```

**Explication des propriétés clés :**

* `ImageFormat` – Détermine le type de fichier (`Png`, `Jpeg`, `Bmp`, etc.). PNG est idéal pour les graphiques et le texte car il conserve des bords nets.  
* `HorizontalResolution` / `VerticalResolution` – Contrôlent la densité de pixels. Pour les vignettes web, 96 DPI suffit ; pour les graphiques prêts à l’impression, 300 DPI est recommandé.  
* `PageOrientation` – Utile lorsque la plage sélectionnée est plus large que haute.  

## Étape 5 : Exporter la plage vers un fichier image

```csharp
// Define the output path for the image
string outputPath = @"YOUR_DIRECTORY\range.png";

// Save the first picture on the worksheet as an image.
// The Pictures collection is automatically populated after setting PrintArea.
sheet.Pictures[0].Save(outputPath, imgOptions);
```

**Ce qui se passe en coulisses :**  
Lorsque `PrintArea` est défini, Aspose.Cells génère une image temporaire représentant cette zone. L’objet `Pictures[0]` est ensuite enregistré en utilisant les options que vous avez fournies.

### Gestion des feuilles sans images

Si la feuille de calcul ne contient pas déjà d’image (par ex., un fichier tout neuf), vous pouvez en créer une à la volée :

```csharp
// Create a picture from the defined range and add it to the sheet
Picture pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
pic.Save(outputPath, imgOptions);
```

## Exemple complet et exécutable

Putting everything together, here is a self‑contained console application you can copy, paste, and run:

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Define the range to export (e.g., a pivot table)
        sheet.PageSetup.PrintArea = "A1:G20";

        // 4️⃣ Set image export options (PNG, 300 DPI, landscape)
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300,
            PageOrientation = PageOrientationType.Landscape
        };

        // 5️⃣ Save the picture as an image file
        string outputPath = @"YOUR_DIRECTORY\range.png";

        // Ensure a picture exists; create one if necessary
        Picture pic;
        if (sheet.Pictures.Count == 0)
        {
            pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
        }
        else
        {
            pic = sheet.Pictures[0];
        }

        pic.Save(outputPath, imgOptions);

        System.Console.WriteLine($"Export completed: {outputPath}");
    }
}
```

**Sortie attendue :**  
Un fichier nommé `range.png` apparaît dans `YOUR_DIRECTORY`. L’ouvrir montre les cellules exactes de **A1 à G20** rendues en une image PNG nette.

## Variantes courantes et gestion des cas limites

| Scénario | Ajustement |
|----------|------------|
| **Export to JPEG** | Modifiez `ImageFormat = ImageFormat.Jpeg` et, éventuellement, définissez `Quality = 90` (plage 0‑100). |
| **Multiple ranges** | Appelez `sheet.Pictures.Add` pour chaque plage et enregistrez chaque image avec un nom de fichier distinct. |
| **Large worksheets** | Augmentez `HorizontalResolution`/`VerticalResolution` uniquement pour la plage nécessaire afin d’éviter les pics de mémoire. |
| **No picture generated** | Vérifiez que `PrintArea` est correctement formaté (`"A1:G20"`). Une adresse invalide entraîne une collection `Pictures` vide. |
| **Saving to a stream** | Utilisez `pic.Save(Stream, imgOptions)` lorsque vous avez besoin de l’image en mémoire (par ex., pour une réponse ASP.NET). |

## Astuces pro pour une exportation d’image fiable

* **Validez la zone d’impression** – Utilisez le parsing `CellArea` (`CellArea area = CellArea.CreateCellArea("A1", "G20")`) pour construire les plages de façon programmatique et éviter les fautes de frappe.  
* **Libérez les ressources** – Encapsulez `Workbook` dans un bloc `using` si vous traitez de nombreux fichiers afin de libérer rapidement les ressources natives.  
* **Traitement par lots** – Lors de l’exportation de dizaines de plages, réutilisez une seule instance `ImageOrPrintOptions` pour réduire la surcharge d’allocation d’objets.  
* **Sécurité des threads** – Les objets Aspose.Cells ne sont **pas** thread‑safe. Créez un `Workbook` distinct par thread ou synchronisez l’accès.  

## Conclusion

Vous disposez maintenant d’une méthode complète, prête pour la production, pour **exporter une plage Excel en image** en utilisant C# et Aspose.Cells. Les étapes—chargement du classeur, définition de la zone d’impression, configuration de `ImageOrPrintOptions` et enregistrement de l’image—couvrent à la fois le « comment » et le « pourquoi », vous assurant de pouvoir adapter le code aux tableaux croisés dynamiques, graphiques ou tout bloc de cellules personnalisé.

Ensuite, vous pourriez explorer :

* **Exporter une plage Excel en image** dans d’autres formats (SVG, BMP) – un autre mot‑clé secondaire à essayer.  
* **Intégrer le PNG dans un PDF** en utilisant Aspose.PDF pour la génération de rapports de bout en bout.  
* **Automatiser les exportations par lots** sur plusieurs classeurs avec une simple boucle console.  

N’hésitez pas à expérimenter différentes résolutions, orientations et répertoires de sortie. Bon codage !

## Que devriez‑vous apprendre ensuite ?

- [Exporter des cellules Excel en image avec Aspose.Cells .NET : guide étape par étape](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Exporter un classeur Excel en image avec Aspose.Cells pour Java](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Comment exporter une feuille de calcul Excel en PNG avec Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}