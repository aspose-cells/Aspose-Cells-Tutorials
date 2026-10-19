---
category: general
date: 2026-09-18
description: Apprenez à exporter Excel vers PowerPoint avec Aspose.Cells. Convertissez
  Excel en PPTX, créez un PowerPoint à partir d’Excel et enregistrez Excel en tant
  que PowerPoint en quelques minutes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- convert excel to pptx
- create powerpoint from excel
- save excel as powerpoint
- export excel to powerpoint
language: fr
lastmod: 2026-09-18
og_description: Comment exporter Excel vers PowerPoint avec Aspose.Cells. Suivez ce
  guide pour convertir Excel en PPTX, créer un PowerPoint à partir d'Excel et enregistrer
  Excel en tant que PowerPoint efficacement.
og_image_alt: Screenshot showing how to export Excel to PowerPoint with Aspose.Cells
og_title: Comment exporter Excel vers PowerPoint – tutoriel complet Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to export Excel to PowerPoint using Aspose.Cells. Convert
    Excel to PPTX, create PowerPoint from Excel, and save Excel as PowerPoint in minutes.
  headline: How to export Excel to PowerPoint with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to export Excel to PowerPoint using Aspose.Cells. Convert
    Excel to PPTX, create PowerPoint from Excel, and save Excel as PowerPoint in minutes.
  name: How to export Excel to PowerPoint with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that contains the shapes
    text: '```java import com.aspose.cells.*;'
  - name: Configure export options for PowerPoint conversion
    text: '```java /** * Creates ImageOrPrintOptions that control how Excel content
      is rendered * in the resulting PowerPoint file. * * @return a fully configured
      ImageOrPrintOptions object */ private static ImageOrPrintOptions createExportOptions()
      { ImageOrPrintOptions options = new ImageOrPrintOptions(); //'
  - name: Mark pictures (or charts) as editable
    text: '```java /** * Marks the first picture on the first worksheet as editable.
      * You can extend this loop to mark all pictures if needed. * * @param workbook
      the workbook that was loaded earlier */ private static void makeFirstPictureEditable(Workbook
      workbook) { // Navigate to the first worksheet (index'
  - name: Save the workbook as an editable PowerPoint presentation
    text: '```java /** * Performs the actual conversion and writes the PPTX file.
      * * @param workbook the workbook prepared in previous steps * @param exportOptions
      the options created in step 2 * @param outputPath full path for the resulting
      .pptx file * @throws Exception if saving fails */ private static voi'
  - name: Full runnable example
    text: '```java import com.aspose.cells.*;'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel‑to‑PowerPoint
- Document conversion
title: Comment exporter Excel vers PowerPoint avec Aspose.Cells – guide étape par
  étape
url: /fr/java/excel-import-export/how-to-export-excel-to-powerpoint-with-aspose-cells-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter Excel vers PowerPoint avec Aspose.Cells – guide étape par étape

Si vous avez besoin de **comment exporter Excel** vers une présentation PowerPoint, ce tutoriel montre une solution complète, prête à l’emploi. À la fin des deux premières phrases, vous connaîtrez exactement quels appels d’API transforment un fichier `.xlsx` en un `.pptx` modifiable. L’approche fonctionne pour tout classeur contenant des graphiques, des images ou d’autres formes, et elle ne nécessite que quelques lignes de code Java.

Dans ce guide, vous apprendrez à **convertir Excel en PPTX**, **créer PowerPoint à partir d’Excel**, et **enregistrer Excel en PowerPoint** tout en préservant la possibilité de modifier les graphiques et les images. Aucun outil supplémentaire au-delà d’Aspose.Cells n’est requis, et le code s’exécute sur Java 8+ et tout JDK récent.  

**Prérequis :**

* Java Development Kit (JDK) 8 ou version plus récente installé  
* Maven ou Gradle pour la gestion des dépendances (ou le JAR Aspose.Cells sur le classpath)  
* Un classeur (`WithShapes.xlsx`) contenant au moins une image ou un graphique  

---

![Diagramme illustrant comment exporter Excel vers PowerPoint](https://example.com/diagram.png "illustration de comment exporter excel vers powerpoint")

## Comment exporter Excel vers PowerPoint avec Aspose.Cells

Le cœur de la conversion se compose de quatre étapes concises. Chaque étape est encapsulée dans une méthode afin que vous puissiez réutiliser la logique dans des applications plus importantes.

### Étape 1 : Charger le classeur qui contient les formes

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {

    /**
     * Loads the source Excel workbook.
     *
     * @param path full path to the .xlsx file
     * @return a Workbook instance ready for manipulation
     * @throws Exception if the file cannot be read
     */
    private static Workbook loadWorkbook(String path) throws Exception {
        // The Workbook constructor reads the entire file into memory.
        return new Workbook(path);
    }
}
```

**Pourquoi c’est important :**  
Charger le classeur vous donne accès aux feuilles de calcul, aux images et aux graphiques. Aspose.Cells lit le fichier sans invoquer Microsoft Office, ce qui permet à l’opération de fonctionner sur des serveurs sans interface graphique.

### Étape 2 : Configurer les options d’exportation pour la conversion PowerPoint

```java
    /**
     * Creates ImageOrPrintOptions that control how Excel content is rendered
     * in the resulting PowerPoint file.
     *
     * @return a fully configured ImageOrPrintOptions object
     */
    private static ImageOrPrintOptions createExportOptions() {
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        // Do not include hidden worksheets – they usually contain metadata only.
        options.setExportHiddenWorksheet(false);
        // Export charts as editable shapes so the end‑user can modify them in PowerPoint.
        options.setExportChartAsEditable(true);
        return options;
    }
```

**Pourquoi c’est important :**  
`setExportChartAsEditable(true)` indique à Aspose.Cells de générer des formes vectorielles au lieu d’images raster. Cela permet à la sortie PowerPoint **de créer PowerPoint à partir d’Excel** avec des graphiques entièrement modifiables, répondant à la plupart des flux de travail de création de présentations.

### Étape 3 : Marquer les images (ou graphiques) comme modifiables

```java
    /**
     * Marks the first picture on the first worksheet as editable.
     * You can extend this loop to mark all pictures if needed.
     *
     * @param workbook the workbook that was loaded earlier
     */
    private static void makeFirstPictureEditable(Workbook workbook) {
        // Navigate to the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
        // Retrieve the first picture on that sheet
        Picture pic = sheet.getPictures().get(0);
        // Set the picture to be editable in the PowerPoint output
        pic.setEditable(true);
    }
```

**Pourquoi c’est important :**  
Lorsqu’une image est marquée comme modifiable, Aspose.Cells l’émet sous forme de forme EMF/WMF dans le fichier PPTX. C’est essentiel pour le cas d’utilisation **exporter excel vers powerpoint** où le destinataire doit ajuster l’image ultérieurement.

### Étape 4 : Enregistrer le classeur en tant que présentation PowerPoint modifiable

```java
    /**
     * Performs the actual conversion and writes the PPTX file.
     *
     * @param workbook      the workbook prepared in previous steps
     * @param exportOptions the options created in step 2
     * @param outputPath    full path for the resulting .pptx file
     * @throws Exception if saving fails
     */
    private static void saveAsPowerPoint(Workbook workbook,
                                          ImageOrPrintOptions exportOptions,
                                          String outputPath) throws Exception {
        // The SaveFormat.PPTX enum tells Aspose.Cells to generate a PowerPoint file.
        workbook.save(outputPath, SaveFormat.PPTX);
    }
```

**Pourquoi c’est important :**  
L’appel `save` regroupe toutes les modifications précédentes (images modifiables, paramètres des graphiques) dans une archive unique `.pptx`. Le fichier résultant peut être ouvert dans Microsoft PowerPoint, Google Slides ou tout visualiseur compatible PPTX.

### Exemple complet exécutable

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {

    public static void main(String[] args) {
        try {
            // Adjust these paths to match your environment.
            String sourcePath = "YOUR_DIRECTORY/WithShapes.xlsx";
            String destinationPath = "YOUR_DIRECTORY/Result.pptx";

            // Step 1 – load workbook
            Workbook workbook = loadWorkbook(sourcePath);

            // Step 2 – configure export options
            ImageOrPrintOptions exportOptions = createExportOptions();

            // Step 3 – make the first picture editable
            makeFirstPictureEditable(workbook);

            // Step 4 – save as PPTX
            saveAsPowerPoint(workbook, exportOptions, destinationPath);

            System.out.println("Conversion successful! File saved at: " + destinationPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }

    // ---- Helper methods from earlier steps ----

    private static Workbook loadWorkbook(String path) throws Exception {
        return new Workbook(path);
    }

    private static ImageOrPrintOptions createExportOptions() {
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setExportHiddenWorksheet(false);
        options.setExportChartAsEditable(true);
        return options;
    }

    private static void makeFirstPictureEditable(Workbook workbook) {
        Worksheet sheet = workbook.getWorksheets().get(0);
        if (!sheet.getPictures().isEmpty()) {
            sheet.getPictures().get(0).setEditable(true);
        }
    }

    private static void saveAsPowerPoint(Workbook workbook,
                                          ImageOrPrintOptions exportOptions,
                                          String outputPath) throws Exception {
        // Export options are automatically applied when saving to PPTX.
        workbook.save(outputPath, SaveFormat.PPTX);
    }
}
```

**Résultat attendu :**  
L’ouverture de `Result.pptx` dans PowerPoint affiche une diapositive qui reflète la première feuille de calcul de `WithShapes.xlsx`. Les graphiques apparaissent sous forme de formes vectorielles que vous pouvez double‑cliquer pour modifier les données, et la première image est un objet modifiable (vous pouvez le redimensionner, le recolorer ou le remplacer directement dans PowerPoint).

---

## Convertir Excel en PPTX – personnalisation avancée

Bien que le flux de base soit suffisant pour la plupart des scénarios, vous pourriez avoir besoin de :

* **Exporter plusieurs feuilles de calcul** – parcourir `workbook.getWorksheets()` et appeler `workbook.save` pour chacune, en passant un indice de diapositive différent via `ImageOrPrintOptions.setSlideNumber(int)`.  
* **Contrôler les dimensions des diapositives** – utilisez `exportOptions.setImageHeight(int)` et `setImageWidth(int)` pour correspondre à une taille de diapositive PowerPoint spécifique (par ex., 1024 × 768).  
* **Préserver les formules** – définissez `exportOptions.setExportFormulasAsValues(false)` si vous souhaitez que les formules Excel d’origine soient intégrées comme données cachées.  

Ces ajustements vous permettent de **créer PowerPoint à partir d’Excel** qui correspond à l’image de marque de l’entreprise ou aux normes de présentation.

---

## Enregistrer Excel en PowerPoint – pièges courants et comment les éviter

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| Les graphiques apparaissent comme des images raster | `setExportChartAsEditable(false)` (par défaut) | Activez les graphiques modifiables avec `setExportChartAsEditable(true)` |
| Aucune image n’apparaît sur la diapositive | Image non marquée comme modifiable ou indice d’image hors limites | Vérifiez que `sheet.getPictures().size() > 0` avant d’appeler `setEditable(true)` |
| Les feuilles cachées apparaissent dans le PPTX | `setExportHiddenWorksheet(true)` | Conservez la valeur par défaut `false` ou définissez explicitement `false` |
| Le fichier de sortie est corrompu | Utilisation d’une version obsolète d’Aspose.Cells (pré‑20.10) | Mettez à jour vers la dernière version d’Aspose.Cells pour Java (par ex., 23.12) |

---

## Exporter Excel vers PowerPoint : conseils de performance

* **Réutiliser le même objet `ImageOrPrintOptions`** pour plusieurs sauvegardes – cela évite des allocations répétées.  
* **Diffuser le classeur source** (`new Workbook(InputStream)`) lors du traitement de gros fichiers sur des serveurs à mémoire limitée.  
* **Paralléliser la conversion par feuille** si vous devez générer un diaporama contenant des centaines de diapositives ; chaque feuille peut être traitée dans son propre thread car les objets Aspose.Cells sont thread‑safe après construction.  

---

## Prochaines étapes

Vous savez maintenant **comment exporter Excel** vers un diaporama PowerPoint, **convertir Excel en PPTX**, et **enregistrer Excel en PowerPoint** avec du contenu modifiable. Pour approfondir vos connaissances, vous pourriez :

* Explorer **Aspose.Slides** pour ajouter des animations ou des dispositions de diapositive maître après la conversion.  
* Automatiser le flux de travail dans un pipeline CI/CD afin que chaque nouveau rapport Excel devienne automatiquement un diaporama PPTX.  
* Combiner cette approche avec **Apache POI** pour pré‑traiter les fichiers Excel avant de les transmettre à Aspose.Cells.  

---

## Conclusion

Ce tutoriel a démontré **comment exporter Excel** vers PowerPoint en utilisant Aspose.Cells, couvrant chaque étape depuis le chargement du classeur jusqu’à l’enregistrement d’un `.pptx` modifiable. Vous pouvez désormais **convertir Excel en PPTX**, **créer PowerPoint à partir d’Excel**, et **enregistrer Excel en PowerPoint** dans vos applications Java en toute confiance. Expérimentez les paramètres optionnels pour adapter la sortie à vos exigences précises de présentation. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment convertir Excel en PowerPoint avec Aspose.Cells pour .NET : guide complet](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Comment exporter Excel vers PowerPoint – guide étape par étape](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [Comment exporter Excel vers PowerPoint avec C# – guide complet](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}