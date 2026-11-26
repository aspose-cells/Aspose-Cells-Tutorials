---
category: general
date: 2026-11-25
description: Exporter Excel vers SVG avec Aspose.Cells en Java – un guide étape par
  étape pour enregistrer Excel au format SVG et créer une image vectorielle.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to svg
- save excel as svg
- excel to vector image
- convert excel to svg
- export excel as svg
language: fr
lastmod: 2026-11-25
og_description: Exportez Excel en SVG avec Aspose.Cells en Java. Apprenez comment
  enregistrer Excel au format SVG et générer des images vectorielles de haute qualité
  en quelques lignes de code.
og_image_alt: Screenshot of an Excel worksheet exported to SVG format
og_title: Exporter Excel en SVG avec Java – tutoriel complet Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  headline: How to export Excel to SVG using Aspose.Cells in Java
  type: TechArticle
- description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  name: How to export Excel to SVG using Aspose.Cells in Java
  steps:
  - name: Load the workbook containing the data
    text: '```java import com.aspose.cells.Workbook;'
  - name: Set up image export options for SVG
    text: '```java import com.aspose.cells.ImageOrPrintOptions; import com.aspose.cells.ImageFormat;'
  - name: Save the workbook as an SVG file
    text: '```java import com.aspose.cells.SaveFormat;'
  - name: What to explore next
    text: '* **Export Excel as PNG or JPEG** – change `exportOptions.setImageFormat(ImageFormat.PNG)`
      for raster output. * **Convert Excel to PDF** – use `PdfSaveOptions` for printable
      documents. * **Batch processing** – combine the above code with a file‑system
      watcher to automatically **convert Excel to SVG*'
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
- Excel
title: Comment exporter Excel en SVG avec Aspose.Cells en Java
url: /fr/java/excel-import-export/how-to-export-excel-to-svg-using-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter Excel en SVG avec Aspose.Cells en Java

Si vous devez **exporter Excel en SVG**, ce guide vous montre comment le faire avec Aspose.Cells pour Java. Vous apprendrez à **enregistrer Excel en SVG** et à générer une **image vectorielle** de haute qualité en quelques lignes de code.

Exporter un classeur Excel au format SVG vous permet d’intégrer la feuille dans des pages web, des rapports ou tout environnement qui privilégie les graphiques évolutifs. Le format SVG préserve les polices, les couleurs et les bordures de cellules sans la pixellisation des images raster.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* Java 17 ou version ultérieure installé.
* Une licence active d’Aspose.Cells pour Java (ou une clé d’évaluation temporaire).
* Un projet Maven ou Gradle où vous pouvez ajouter la dépendance Aspose.Cells.

Ajoutez la bibliothèque Aspose.Cells à votre projet :

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.10'
```

## Exporter Excel en SVG – étape par étape

Le processus se compose de trois étapes simples : charger le classeur, configurer les options d’exportation SVG et enregistrer le résultat. Chaque étape est expliquée ci‑dessous.

### Étape 1 : Charger le classeur contenant les données

```java
import com.aspose.cells.Workbook;

public class ExcelToSvgDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel file you want to convert.
        Workbook workbook = new Workbook("C:/Data/Report.xlsx");
        // Continue with export options...
    }
}
```

**Pourquoi c’est important :**  
`Workbook` est l’objet central d’Aspose.Cells. Charger le fichier une fois vous donne accès à toutes les feuilles de calcul, styles et objets incorporés, que l’exportateur SVG rendra ensuite.

### Étape 2 : Configurer les options d’exportation d’image pour SVG

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;

ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setImageFormat(ImageFormat.SVG); // Guarantees a vector output
exportOptions.setOnePagePerSheet(true);       // Export each sheet as a single SVG page
exportOptions.setTransparent(true);           // Preserve transparent backgrounds
```

**Pourquoi c’est important :**  
`ImageOrPrintOptions` vous permet de contrôler le format de sortie. Sélectionner `ImageFormat.SVG` garantit que le résultat est une **image vectorielle** plutôt qu’un bitmap. Activer `OnePagePerSheet` évite les sauts de page à l’intérieur d’une feuille, ce qui est généralement souhaité lorsque le SVG sera affiché dans une vue web.

### Étape 3 : Enregistrer le classeur au format SVG

```java
import com.aspose.cells.SaveFormat;

workbook.save("C:/Output/Report.svg", exportOptions);
System.out.println("Excel workbook successfully exported to SVG.");
```

**Pourquoi c’est important :**  
La méthode `save` combine le classeur chargé avec les `exportOptions` configurées. L’appel écrit un fichier SVG pleinement conforme qui peut être ouvert dans les navigateurs, Inkscape ou tout éditeur compatible vecteurs.

## Exemple complet exécutable

Assembler les trois étapes vous fournit un programme autonome que vous pouvez compiler et exécuter immédiatement :

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("C:/Data/FontVariation.xlsx");

        // 2. Configure SVG export options
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setImageFormat(ImageFormat.SVG);
        exportOptions.setOnePagePerSheet(true);
        exportOptions.setTransparent(true);

        // 3. Export to SVG
        workbook.save("C:/Output/WithVariationSelectors.svg", exportOptions);
        System.out.println("Export complete: Excel saved as SVG.");
    }
}
```

**Sortie attendue**

L’exécution du programme affiche :

```
Export complete: Excel saved as SVG.
```

Vous trouverez `WithVariationSelectors.svg` dans `C:/Output`. L’ouverture du fichier dans un navigateur montre la feuille rendue comme des graphiques évolutifs, avec le texte, les bordures et les couleurs de cellules préservés.

## Variantes courantes et cas limites

| Situation | Ajustement recommandé |
|-----------|------------------------|
| **Plusieurs feuilles de calcul** | Parcourir `workbook.getWorksheets()` et appeler `save` pour chaque feuille, en ajoutant éventuellement le nom de la feuille au nom du fichier. |
| **Classeur volumineux** | Augmenter `exportOptions.setRenderThreadCount(int)` pour utiliser le rendu parallèle, réduisant ainsi le temps de conversion. |
| **DPI personnalisé** | Appeler `exportOptions.setHorizontalResolution(int)` et `exportOptions.setVerticalResolution(int)` pour contrôler le redimensionnement du viewBox du SVG. |
| **Incorporation des polices** | Définir `exportOptions.setExportFontAsSVG(true)` pour incorporer les définitions de police directement dans le SVG, garantissant la fidélité visuelle sur les machines ne disposant pas des polices d’origine. |
| **Fichiers protégés par mot de passe** | Fournir le mot de passe lors du chargement : `Workbook workbook = new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("pwd"); }});` |

## Astuces professionnelles

* **Éviter le recours au raster** – Si une feuille de calcul contient des graphiques complexes, vérifiez qu’ils apparaissent comme des éléments vectoriels dans le SVG. Sinon, activez `exportOptions.setExportChartAsSVG(true)`.
* **Performance** – Pour les conversions par lots, réutilisez une seule instance de `ImageOrPrintOptions` au lieu d’en créer une nouvelle pour chaque fichier.
* **Tests** – Validez le SVG généré avec un validateur en ligne (par ex., le W3C SVG Validator) pour détecter tôt toute balise malformée.

## Vérifier la conversion

Vous pouvez confirmer programmétiquement que le fichier de sortie est bien un SVG :

```java
import java.nio.file.Files;
import java.nio.file.Paths;

byte[] data = Files.readAllBytes(Paths.get("C:/Output/Report.svg"));
String content = new String(data, "UTF-8");
if (content.contains("<svg")) {
    System.out.println("File is a valid SVG.");
}
```

La présence de l’élément racine `<svg>` indique une opération réussie de **conversion d’Excel en SVG**.

## Conclusion

Ce tutoriel a démontré comment **exporter Excel en SVG** avec Aspose.Cells pour Java. En chargeant le classeur, en configurant `ImageOrPrintOptions` pour le SVG et en appelant `save`, vous pouvez **enregistrer Excel en SVG** et obtenir une conversion propre d’**Excel en image vectorielle**. À partir de là, vous pouvez intégrer le SVG dans des pages web, l’inclure dans la documentation ou le traiter davantage avec n’importe quel outil de graphisme vectoriel.

### Que explorer ensuite

* **Exporter Excel en PNG ou JPEG** – modifier `exportOptions.setImageFormat(ImageFormat.PNG)` pour une sortie raster.
* **Convertir Excel en PDF** – utiliser `PdfSaveOptions` pour des documents imprimables.
* **Traitement par lots** – combiner le code ci‑dessus avec un observateur de système de fichiers pour **convertir automatiquement Excel en SVG** pour chaque nouveau classeur dans un dossier.

N’hésitez pas à expérimenter avec les options, et laissez la flexibilité d’Aspose.Cells transformer vos données Excel en tout format visuel dont vous avez besoin. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment exporter les graphiques Excel en SVG avec Aspose.Cells Java pour des graphiques vectoriels évolutifs](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Comment créer et enregistrer un classeur Excel en SVG avec Aspose.Cells pour Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Comment exporter Excel en SVG – Guide Java étape par étape](/cells/english/java/excel-import-export/how-to-export-excel-to-svg-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}