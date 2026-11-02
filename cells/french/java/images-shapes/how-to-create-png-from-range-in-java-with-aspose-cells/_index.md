---
category: general
date: 2026-10-07
description: Apprenez à créer un PNG à partir d’une plage et à exporter les données
  au format PNG en Java. Ce guide vous montre comment enregistrer l’image d’une plage
  Excel à l’aide d’Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: fr
lastmod: 2026-10-07
og_description: Créez un PNG à partir d’une plage en Java et exportez les données
  au format PNG avec Aspose.Cells. Suivez ce tutoriel complet pour enregistrer instantanément
  l’image d’une plage Excel.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Créer un PNG à partir d’une plage en Java – guide Aspose.Cells étape par
  étape
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Comment créer un PNG à partir d’une plage en Java avec Aspose.Cells
url: /fr/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un PNG à partir d'une plage en Java avec Aspose.Cells

Si vous devez **créer un PNG à partir d'une plage** dans un classeur Excel, ce tutoriel vous montre exactement comment le faire. À la fin du guide, vous serez capable de **exporter des données en PNG**, d'enregistrer une image de plage Excel et de réutiliser le fichier dans des rapports ou des pages web.

Vous verrez un programme Java complet et exécutable qui charge un classeur, sélectionne les cellules souhaitées, les rend en PNG et enregistre le résultat sur le disque. Aucun outil externe n'est requis—Aspose.Cells gère tout en interne.

## Ce que couvre ce tutoriel

* Prérequis et configuration Maven pour Aspose.Cells
* Chargement d'un classeur contenant un tableau croisé dynamique ou toute plage de données
* Définition de la plage de cellules exacte que vous souhaitez convertir
* Configuration des options d'image pour la sortie PNG
* Rendu de la plage et sauvegarde du fichier PNG
* Pièges courants et astuces pour des images de haute qualité

Après avoir suivi ces étapes, vous pourrez **convertir une feuille de calcul en PNG** pour n'importe quelle plage, qu'il s'agisse d'un tableau simple ou d'un graphique croisé dynamique complexe.

## Prérequis

* Java 17 ou ultérieur (le code se compile avec JDK 11+)
* Maven 3.6+ (ou Gradle si vous préférez)
* Aspose.Cells for Java 23.12 ou plus récent – ajoutez la dépendance indiquée ci-dessous
* Un fichier Excel existant (`PivotWithStyle.xlsx`) qui contient la plage que vous souhaitez capturer

> **Astuce :** Si vous n'avez pas de licence, vous pouvez demander une clé d'évaluation temporaire auprès d'Aspose. La bibliothèque fonctionne en mode évaluation sans configuration supplémentaire.

### Dépendance Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Étape 1 : Charger le classeur qui contient la plage cible

La première opération consiste à ouvrir le fichier Excel. Aspose.Cells lit le fichier en mémoire sans nécessiter Microsoft Office.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Pourquoi c'est important* : Charger le classeur vous donne accès aux feuilles de calcul, aux cellules et aux propriétés de mise en page nécessaires au rendu.

## Étape 2 : Accéder à la feuille de calcul qui contient la plage

La plupart des classeurs ont une feuille par défaut à l'index 0, mais vous pouvez également utiliser le nom de la feuille.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Si vos données se trouvent sur une autre feuille, remplacez `0` par l'index approprié ou utilisez `workbook.getWorksheets().get("SheetName")`.

## Étape 3 : Définir la plage de cellules que vous souhaitez convertir

Vous pouvez spécifier n'importe quelle zone rectangulaire en utilisant la notation A1. Dans cet exemple, nous capturons `A1:D15`, qui peut être un tableau croisé dynamique ou un bloc de données ordinaire.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Cas particulier* : Lorsque la plage comprend des cellules fusionnées, Aspose.Cells agrandit automatiquement l'image pour inclure la zone fusionnée.

## Étape 4 : Préparer les options d'image PNG

`ImageOrPrintOptions` vous permet de contrôler le format, la résolution et d'autres détails de rendu. Définir le format d'enregistrement sur PNG garantit une qualité sans perte.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Augmenter le DPI est utile lorsque les cellules source contiennent de petites polices ou des graphiques détaillés.

## Étape 5 : Limiter la zone de rendu à la plage sélectionnée

En assignant la plage comme zone d'impression, Aspose.Cells ne rend que ces cellules et ignore le reste de la feuille.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Si vous sautez cette étape, toute la feuille de calcul sera rasterisée, ce qui peut gaspiller de la mémoire et produire une image plus grande.

## Étape 6 : Rendre la plage et ajouter l'image à la feuille de calcul (optionnel)

Si vous souhaitez intégrer le PNG généré dans le classeur (à des fins d'aperçu), vous pouvez l'ajouter comme image. Cette étape est optionnelle pour les scénarios d'exportation pure.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Pourquoi vous pourriez faire cela* : Certains flux de travail nécessitent que l'image fasse partie du classeur avant la distribution, par exemple la création d'un rapport imprimable qui mélange cellules natives et images.

## Étape 7 : Enregistrer le fichier PNG sur le disque

Enfin, écrivez l'image dans un fichier. La méthode `save` respecte le format spécifié dans `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Lorsque le programme se termine, `PivotImage.png` contiendra une capture pixel‑parfait des cellules `A1:D15`.

### Résultat attendu

* Un fichier nommé `PivotImage.png` situé dans `YOUR_DIRECTORY`.
* L'image montre la mise en page exacte, les polices, les couleurs et les bordures de la plage sélectionnée.
* Si la plage source contient un tableau croisé dynamique, l'image rendue inclut le même style et les mêmes valeurs calculées que celles affichées dans Excel.

## Gestion des scénarios courants

### Exporter une plage non contiguë

Aspose.Cells ne rend pas les plages disjointes dans une seule image. Pour exporter plusieurs zones, créez des images séparées pour chaque plage et combinez‑les ensuite avec une bibliothèque de traitement d'images (par ex., ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Enregistrer une grande feuille de calcul en PNG

Rendre une feuille entière qui s'étend sur des milliers de lignes peut consommer beaucoup de mémoire. Atténuez cela en :

* Réduisant le DPI (`imageOptions.setResolution(72)`) pour un fichier plus petit.
* Utilisant `setPageCount` pour limiter le nombre de pages rendues.
* Exportant une page imprimable à la fois via `worksheet.getPageSetup().setPrintArea(...)`.

### Conserver les formules des cellules

Une image PNG est un format raster ; les formules ne sont pas conservées. Si les consommateurs en aval ont besoin des données brutes, exportez également la plage en CSV ou JSON en utilisant `Range.exportDataTable()`.

## Exemple complet et exécutable

Ci-dessous se trouve la classe Java complète que vous pouvez copier‑coller dans votre IDE. Remplacez `YOUR_DIRECTORY` par un chemin absolu ou relatif sur votre machine.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Exécutez le programme avec `mvn compile exec:java` (ou votre outil de construction préféré). Après l'exécution, ouvrez `PivotImage.png` pour vérifier le résultat.

## Conclusion

Vous savez maintenant comment **créer un PNG à partir d'une plage** en Java avec Aspose.Cells, et ainsi **exporter des données en PNG** et **enregistrer l'image d'une plage Excel** pour tout scénario de reporting ou de partage. Les étapes—chargement du classeur, définition de la plage, configuration des options d'image, définition de la zone d'impression et sauvegarde du fichier—couvrent l'ensemble du flux de travail pour **convertir une feuille de calcul en PNG** et **enregistrer des cellules en PNG**.

### Prochaines étapes

* Expérimentez avec différentes valeurs de `Resolution` pour équilibrer qualité et taille du fichier.
* Utilisez `ImageOrPrintOptions.setTransparent(true)` si vous avez besoin d'un PNG avec un arrière‑plan transparent.
* Combinez plusieurs images de plages en un seul PDF en utilisant `PdfSaveOptions` pour des rapports multi‑pages.
* Explorez l'exportation vers d'autres formats raster (JPEG, BMP) en modifiant `setSaveFormat`.

N'hésitez pas à adapter ce modèle aux graphiques, tableaux ou même à des feuilles de calcul entières. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et à explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment exporter une feuille de calcul Excel en PNG avec Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convertir Excel en PNG avec Aspose.Cells pour Java : guide étape par étape](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Créer une plage d'union dans Excel avec Aspose.Cells Java : guide complet](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}