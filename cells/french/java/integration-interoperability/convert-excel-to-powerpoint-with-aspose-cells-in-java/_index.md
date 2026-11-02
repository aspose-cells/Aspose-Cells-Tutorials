---
category: general
date: 2026-09-21
description: Convertir Excel en PowerPoint avec Aspose.Cells en Java – apprenez comment
  exporter un graphique au format PPTX et enregistrer le classeur au format PPTX en
  quelques lignes de code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- save workbook as pptx
- how to export chart to pptx
- create powerpoint from excel chart
language: fr
lastmod: 2026-09-21
og_description: Convertir Excel en PowerPoint avec Aspose.Cells en Java. Ce tutoriel
  montre comment exporter un graphique au format PPTX et enregistrer le classeur au
  format PPTX avec des zones de texte modifiables.
og_image_alt: Screenshot of Java code converting an Excel workbook to a PowerPoint
  presentation
og_title: Convertir Excel en PowerPoint avec Aspose.Cells – Guide Java
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Convert Excel to PowerPoint with Aspose.Cells in Java – learn how to
    export chart to PPTX and save workbook as PPTX in just a few lines of code.
  headline: Convert Excel to PowerPoint with Aspose.Cells in Java
  type: TechArticle
- questions:
  - answer: Yes. Loop through each worksheet, export its chart to a new slide using
      `PdfSaveOptions`, and then save the workbook once after processing all sheets.
    question: Can I convert multiple worksheets into separate PowerPoint slides?
  - answer: Only chart and textbox objects are transferred to PowerPoint. Cell formatting
      stays in the Excel file; it does not appear in the PPTX.
    question: Does this method preserve cell formatting?
  - answer: 'Use `SaveFormat.PDF` and the same `PdfSaveOptions`. The `setExportEditableTextBoxes`
      flag works for PDF as well. ## Next steps Now that you know how to **save workbook
      as PPTX** and **export chart to PPTX**, you might explore: * Adding multiple
      charts to different slides (`create powerpoint from exc'
    question: What if I need to export to PDF instead of PPTX?
  type: FAQPage
tags:
- Excel
- PowerPoint
- Aspose.Cells
- Java
title: Convertir Excel en PowerPoint avec Aspose.Cells en Java
url: /fr/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir Excel en PowerPoint avec Aspose.Cells en Java

Si vous devez **convertir Excel en PowerPoint**, ce guide vous montre une méthode concise et prête pour la production. Vous verrez comment exporter un graphique vers PPTX, garder les zones de texte éditables, et **enregistrer le classeur au format PPTX** en seulement trois lignes de code Java.

De nombreux développeurs exportent des données vers des PDF, mais PowerPoint est souvent plus adapté aux présentations qui nécessitent des graphiques dynamiques et des éléments éditables. Ce tutoriel couvre tout ce dont vous avez besoin — de la configuration du projet à la gestion des problèmes courants — afin de créer un PowerPoint à partir d’un graphique Excel sans quitter votre IDE Java.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* Java 17 ou version ultérieure installé.
* Maven (ou Gradle) pour gérer les dépendances.
* Une licence Aspose.Cells for Java (l’essai gratuit fonctionne pour l’évaluation).
* Un fichier Excel (`ChartAndTextbox.xlsx`) contenant au moins un graphique et une zone de texte.

## Étape 1 : Ajouter Aspose.Cells à votre projet

La première étape consiste à inclure la bibliothèque Aspose.Cells. Avec Maven, ajoutez la dépendance suivante à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Conseil pro :** Si vous utilisez Gradle, l’équivalent est :
> ```groovy
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Inclure la bibliothèque vous donne accès aux classes `Workbook`, `PdfSaveOptions` et à l’énumération `SaveFormat` nécessaires à la conversion.

## Étape 2 : Charger le classeur contenant le graphique et la zone de texte

Chargez maintenant le fichier Excel. La classe `Workbook` lit l’ensemble du classeur en mémoire, en préservant les graphiques, les formules et les zones de texte.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Adjust the path to point to your Excel file
        String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";

        // Load the workbook
        Workbook workbook = new Workbook(sourcePath);
        
        // Continue with conversion...
    }
}
```

**Pourquoi c’est important :** Charger le classeur en premier assure que tous les objets incorporés (graphiques, images, zones de texte) sont disponibles pour le processus d’exportation. Si le fichier est introuvable, Aspose.Cells lève une `FileNotFoundException` claire, que vous pouvez intercepter pour offrir une meilleure expérience utilisateur.

## Étape 3 : Configurer les options d’exportation pour garder les zones de texte éditables

Aspose.Cells utilise `PdfSaveOptions` pour contrôler la façon dont les objets sont écrits lorsque le format cible est PowerPoint. En activant `setExportEditableTextBoxes(true)`, toute zone de texte dans la feuille Excel reste éditable après la conversion.

```java
import com.aspose.cells.PdfSaveOptions;

PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.setExportEditableTextBoxes(true); // Text boxes stay editable in the PPTX
```

> **Pourquoi utiliser `PdfSaveOptions` pour PPTX ?**  
> En interne, Aspose.Cells réutilise le pipeline de rendu PDF pour la sortie PowerPoint, ce qui permet un contrôle fin des éléments éditables. Activer ce drapeau est la méthode recommandée pour préserver l’éditabilité des zones de texte.

## Étape 4 : Enregistrer le classeur en tant que présentation PowerPoint

Enfin, appelez `workbook.save` avec `SaveFormat.PPTX`. Cette étape finalise le flux **créer PowerPoint à partir d’un graphique Excel**.

```java
import com.aspose.cells.SaveFormat;

String targetPath = "YOUR_DIRECTORY/Result.pptx";
workbook.save(targetPath, SaveFormat.PPTX, saveOptions);
System.out.println("Conversion successful! PPTX saved to " + targetPath);
```

En réunissant le tout, le programme complet ressemble à ceci :

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.PdfSaveOptions;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook containing the chart and textbox
            String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2. Create PDF save options and enable editable text boxes for PPTX output
            PdfSaveOptions saveOptions = new PdfSaveOptions();
            saveOptions.setExportEditableTextBoxes(true); // text boxes will remain editable in the PPTX

            // 3. Save the workbook as a PowerPoint presentation using the configured options
            String targetPath = "YOUR_DIRECTORY/Result.pptx";
            workbook.save(targetPath, SaveFormat.PPTX, saveOptions);

            System.out.println("Conversion successful! PPTX saved to " + targetPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Sortie attendue

L’exécution du programme affiche :

```
Conversion successful! PPTX saved to YOUR_DIRECTORY/Result.pptx
```

Lorsque vous ouvrez `Result.pptx` dans Microsoft PowerPoint, vous verrez :

* Le graphique Excel d’origine rendu comme un graphique PowerPoint natif (modifiable dans l’éditeur de graphiques de PowerPoint).
* La zone de texte provenant d’Excel apparaît comme une forme éditable, vous permettant de changer son texte directement sur la diapositive.

## Gestion des cas limites courants

| Situation | Approche recommandée |
|-----------|----------------------|
| **File not found** | Enveloppez le constructeur `Workbook` dans un bloc `try‑catch` et affichez un message clair. |
| **Workbook has no chart** | Vérifiez que la feuille contient un graphique (`worksheet.getCharts().getCount() > 0`) avant la conversion ; sinon, sautez l’étape ou ajoutez un espace réservé. |
| **Large Excel files** | Augmentez la taille du tas JVM (`-Xmx2g`) pour éviter `OutOfMemoryError` pendant le rendu. |
| **License not set** | Appelez `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` avant de charger le classeur pour supprimer le filigrane d’évaluation. |

## Questions fréquentes

**Q : Puis‑je convertir plusieurs feuilles de calcul en diapositives PowerPoint distinctes ?**  
R : Oui. Parcourez chaque feuille, exportez son graphique vers une nouvelle diapositive à l’aide de `PdfSaveOptions`, puis enregistrez le classeur une fois toutes les feuilles traitées.

**Q : Cette méthode préserve‑t‑elle le formatage des cellules ?**  
R : Seuls les objets graphiques et les zones de texte sont transférés vers PowerPoint. Le formatage des cellules reste dans le fichier Excel ; il n’apparaît pas dans le PPTX.

**Q : Et si je dois exporter en PDF plutôt qu’en PPTX ?**  
R : Utilisez `SaveFormat.PDF` avec les mêmes `PdfSaveOptions`. Le drapeau `setExportEditableTextBoxes` fonctionne également pour le PDF.

## Prochaines étapes

Maintenant que vous savez comment **enregistrer le classeur au format PPTX** et **exporter un graphique au format PPTX**, vous pouvez explorer :

* Ajouter plusieurs graphiques à différentes diapositives (`create powerpoint from excel chart` avec une boucle).
* Personnaliser les mises en page des diapositives en utilisant Aspose.Slides for Java pour un style de présentation plus riche.
* Intégrer des images provenant des cellules Excel dans PowerPoint en utilisant la classe `Picture`.

Ces extensions vous permettent de créer des pipelines de reporting entièrement automatisés qui génèrent des présentations soignées directement à partir des données Excel.

---

**Résumé :** Ce tutoriel a démontré une méthode fiable pour **convertir Excel en PowerPoint** avec Aspose.Cells pour Java. En chargeant le classeur, en configurant `PdfSaveOptions` pour garder les zones de texte éditables, et en enregistrant avec `SaveFormat.PPTX`, vous obtenez un fichier PowerPoint contenant des graphiques dynamiques et des formes éditables — idéal pour des présentations d’affaires dynamiques. N’hésitez pas à adapter le code pour le traitement par lots ou à l’intégrer à des solutions de reporting plus larges.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos projets.

- [Comment créer un graphique Excel avec ligne de tendance et l'exporter en image avec Aspose.Cells pour Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Comment convertir des graphiques Excel en SVG avec Aspose.Cells en Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)
- [Comment convertir Excel en PDF en Java avec Aspose.Cells&#58; guide étape par étape](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}