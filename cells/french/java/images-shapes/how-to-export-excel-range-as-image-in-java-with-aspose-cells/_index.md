---
category: general
date: 2026-10-10
description: Apprenez à exporter une plage Excel en tant qu’image en Java avec Aspose.Cells.
  Le guide couvre également l’exportation de cellules sélectionnées en image et l’enregistrement
  d’une feuille de calcul Excel en tant qu’image.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- export selected cells as image
- save excel worksheet as picture
language: fr
lastmod: 2026-10-10
og_description: Exporter une plage Excel en image en Java avec une solution étape
  par étape. Inclut l'exportation des cellules sélectionnées en image et la sauvegarde
  de la feuille de calcul Excel en image.
og_image_alt: Diagram showing export Excel range as image using Java and Aspose.Cells
og_title: Exporter une plage Excel en image en Java – guide complet d’Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  headline: How to export Excel range as image in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  name: How to export Excel range as image in Java with Aspose.Cells
  steps:
  - name: Why this method matters
    text: '* **Separation of concerns:** Loading, option configuration, and exporting
      are clearly divided. * **Flexibility:** You can change the image format or DPI
      without touching the core logic. * **Error handling:** Throwing `Exception`
      lets the caller decide whether to log, retry, or abort.'
  - name: 1. Merged cells
    text: Aspose.Cells automatically preserves merged cell appearance, but if you
      need to control the rendering, set `options.setOnePagePerSheet(true)` to force
      the whole sheet onto a single page before exporting.
  - name: 2. Hidden rows or columns
    text: 'By default, hidden rows/columns are not rendered. To include them, enable:'
  - name: 3. Large ranges and memory consumption
    text: 'Exporting very large ranges can consume significant memory. If you encounter
      `OutOfMemoryError`, consider:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- Image export
title: Comment exporter une plage Excel en image en Java avec Aspose.Cells
url: /fr/java/images-shapes/how-to-export-excel-range-as-image-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter une plage Excel en image en Java avec Aspose.Cells

Si vous devez **exporter une plage Excel en image**, ce tutoriel vous guide à travers une solution Java complète utilisant la bibliothèque Aspose.Cells. Vous apprendrez également comment **exporter des cellules sélectionnées en image** et comment **enregistrer une feuille de calcul Excel en image** à des fins de reporting ou de documentation.

Exporter une partie d’un classeur sous forme d’image élimine le besoin d’outils de capture d’écran tiers et garantit des résultats pixel‑parfait. À la fin de ce guide, vous disposerez d’une méthode réutilisable qui écrit un PNG (ou tout format supporté) directement sur le disque, prête à être intégrée dans des PDF, des e‑mails ou des pages web.

## Prérequis

* Java 17 ou version supérieure installé.
* Maven 3.8+ (ou un autre outil de construction capable de gérer les dépendances Maven).
* Une licence Aspose.Cells for Java (l’évaluation gratuite fonctionne mais ajoute un filigrane).
* Un fichier Excel d’exemple (`input.xlsx`) placé dans un répertoire connu.

Les sections suivantes supposent que vous êtes à l’aise avec le développement Java de base et la configuration d’un projet Maven.

## Étape 1 : Ajouter Aspose.Cells à votre projet

Ajoutez la dépendance Maven Aspose.Cells à votre `pom.xml`. Cette bibliothèque fournit les classes `Workbook`, `Worksheet` et `ImageOrPrintOptions` utilisées dans l’exemple de code.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

> **Astuce :** Gardez le numéro de version à jour ; les nouvelles versions ajoutent la prise en charge de formats et des améliorations de performances.

## Étape 2 : Créer une méthode utilitaire pour exporter une plage

Encapsuler la logique d’exportation dans une méthode facilite la réutilisation entre projets et la prise en charge des cas particuliers tels que les cellules fusionnées ou les lignes masquées.

```java
import com.aspose.cells.*;

import java.io.File;

/**
 * Exports a specific cell range from an Excel worksheet to an image file.
 *
 * @param workbookPath   Full path to the source .xlsx file.
 * @param sheetIndex     Zero‑based index of the worksheet (0 = first sheet).
 * @param range          A‑style range string, e.g. "A1:G20".
 * @param outputPath     Full path where the image will be saved.
 * @param imageFormat    Desired image format (PNG, JPEG, BMP, etc.).
 * @throws Exception if the file cannot be read or written.
 */
public static void exportRangeAsImage(
        String workbookPath,
        int sheetIndex,
        String range,
        String outputPath,
        ImageFormat imageFormat) throws Exception {

    // Load the workbook
    Workbook wb = new Workbook(workbookPath);

    // Obtain the requested worksheet
    Worksheet ws = wb.getWorksheets().get(sheetIndex);

    // Configure image export options
    ImageOrPrintOptions options = new ImageOrPrintOptions();
    options.setImageFormat(imageFormat);
    // Optional: increase DPI for higher‑resolution output
    options.setHorizontalResolution(300);
    options.setVerticalResolution(300);

    // Export the defined range as an image file
    ws.getCells().exportRangeAsImage(range, outputPath, options);
}
```

### Pourquoi cette méthode est importante

* **Séparation des préoccupations :** Le chargement, la configuration des options et l’exportation sont clairement séparés.
* **Flexibilité :** Vous pouvez changer le format d’image ou le DPI sans toucher à la logique principale.
* **Gestion des erreurs :** Lever une `Exception` permet à l’appelant de décider s’il faut consigner, réessayer ou abandonner.

## Étape 3 : Appeler la méthode avec des paramètres réels

Voici une méthode `main` minimale qui montre comment **exporter des cellules sélectionnées en image** et également comment **enregistrer une feuille de calcul Excel en image** en utilisant la plage complète de la feuille.

```java
public class ExcelImageExporter {
    public static void main(String[] args) {
        try {
            String inputFile   = "C:/Data/input.xlsx";
            String outputFile1 = "C:/Data/range.png";
            String outputFile2 = "C:/Data/full_sheet.png";

            // Export a specific range (A1:G20)
            exportRangeAsImage(
                    inputFile,
                    0,                  // first worksheet
                    "A1:G20",
                    outputFile1,
                    ImageFormat.PNG);   // primary format for lossless quality

            // Export the entire first worksheet – effectively saving the worksheet as picture
            exportRangeAsImage(
                    inputFile,
                    0,
                    "A1:" + getLastCellAddress(inputFile, 0), // compute last used cell
                    outputFile2,
                    ImageFormat.PNG);

            System.out.println("Images generated successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Helper that returns the address of the last used cell in a worksheet.
     */
    private static String getLastCellAddress(String workbookPath, int sheetIdx) throws Exception {
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.getWorksheets().get(sheetIdx);
        // Find the maximum row and column that contain data
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();
        // Convert column index to A‑style letter (0 -> A)
        String colLetter = CellReference.convertNumToColString(maxCol);
        return colLetter + (maxRow + 1);
    }
}
```

#### Résultat attendu

L’exécution du programme crée deux fichiers PNG :

* `range.png` – une image qui ne contient que les cellules **A1 : G20**.
* `full_sheet.png` – une image de toute la zone utilisée de la première feuille de calcul, ce qui équivaut à **enregistrer une feuille de calcul Excel en image**.

Vous pouvez ouvrir les fichiers avec n’importe quel visualiseur d’image pour vérifier que la mise en page visuelle correspond à la vue Excel, y compris les bordures de cellules, les couleurs et les cellules fusionnées.

## Étape 4 : Gérer les cas particuliers courants

### 1. Cellules fusionnées

Aspose.Cells préserve automatiquement l’apparence des cellules fusionnées, mais si vous devez contrôler le rendu, définissez `options.setOnePagePerSheet(true)` pour forcer toute la feuille sur une seule page avant l’exportation.

### 2. Lignes ou colonnes masquées

Par défaut, les lignes/colonnes masquées ne sont pas rendues. Pour les inclure, activez :

```java
options.setSkipEmptyRows(false);
options.setSkipEmptyColumns(false);
```

### 3. Grandes plages et consommation de mémoire

Exporter des plages très grandes peut consommer beaucoup de mémoire. Si vous rencontrez `OutOfMemoryError`, envisagez :

* Réduire le DPI (`options.setHorizontalResolution(150)`).
* Exporter la plage en morceaux plus petits et assembler les images avec une bibliothèque graphique.

## Étape 5 : Vérifier le résultat programmatique (optionnel)

Si votre processus en aval doit confirmer que l’image a été générée correctement, vous pouvez charger le PNG avec `javax.imageio.ImageIO` et vérifier ses dimensions :

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File(outputFile1));
System.out.println("Image width: " + img.getWidth() + " px");
System.out.println("Image height: " + img.getHeight() + " px");
```

Une largeur et une hauteur non nulles indiquent un export réussi.

## Conclusion

Vous savez maintenant comment **exporter une plage Excel en image** en Java, comment **exporter des cellules sélectionnées en image**, et comment **enregistrer une feuille de calcul Excel en image** en utilisant Aspose.Cells. La méthode réutilisable `exportRangeAsImage` abstrait la complexité, vous permet de contrôler la qualité de l’image, et fonctionne avec n’importe quel index de feuille ou plage de cellules.

Les étapes suivantes que vous pourriez explorer :

* Convertir le PNG en PDF avec Aspose.PDF pour le reporting.
* Traiter par lots plusieurs classeurs dans un répertoire.
* Intégrer l’exportation d’image dans un endpoint REST Spring Boot afin que les clients puissent demander des images à la demande.

N’hésitez pas à expérimenter différents formats d’image (`ImageFormat.JPEG`, `ImageFormat.BMP`) et réglages DPI pour répondre aux exigences visuelles de votre projet. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Exporter un classeur Excel en image avec Aspose.Cells pour Java : guide étape par étape](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Comment créer un graphique Excel avec ligne de tendance et l’exporter en image avec Aspose.Cells pour Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Exporter des cellules Excel en image avec Aspose.Cells .NET : guide étape par étape](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}