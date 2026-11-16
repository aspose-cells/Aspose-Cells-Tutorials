---
category: general
date: 2026-11-16
description: Apprenez à exporter une forme d’Excel vers PowerPoint en Java, à convertir
  un graphique Excel en fichier PPTX et à enregistrer la forme PPTX avec Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shape
- convert excel chart
- shape to powerpoint
- save shape pptx
- export shape from excel
language: fr
lastmod: 2026-11-16
og_description: Comment exporter une forme d’Excel vers PowerPoint en Java. Suivez
  ce tutoriel complet pour convertir un graphique Excel, enregistrer la forme au format
  PPTX et intégrer une forme dans un fichier PowerPoint.
og_image_alt: Diagram illustrating how to export shape from Excel to PowerPoint using
  Java
og_title: Comment exporter une forme d’Excel vers PowerPoint en Java – guide étape
  par étape
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  headline: How to export shape from Excel to PowerPoint using Java
  type: TechArticle
- description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  name: How to export shape from Excel to PowerPoint using Java
  steps:
  - name: '**Load the workbook** that contains the shape.'
    text: '**Load the workbook** that contains the shape.'
  - name: '**Locate the shape** on the first worksheet.'
    text: '**Locate the shape** on the first worksheet.'
  - name: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
    text: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
  - name: '**Save the shape as a PPTX file**.'
    text: '**Save the shape as a PPTX file**.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
- PowerPoint integration
title: Comment exporter une forme d’Excel vers PowerPoint à l’aide de Java
url: /fr/java/integration-interoperability/how-to-export-shape-from-excel-to-powerpoint-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter une forme d'Excel vers PowerPoint avec Java

Si vous avez besoin de **how to export shape** depuis un classeur Excel vers une diapositive PowerPoint, ce guide vous montre les étapes exactes. Vous verrez comment **convert Excel chart** des objets, les transformer en **shape to PowerPoint**, et enfin **save shape PPTX** avec les bonnes options d'exportation.

Exporter une forme est une exigence courante lorsque vous générez des rapports de façon programmatique. À la fin de ce tutoriel, vous disposerez d'un programme Java autonome qui crée un fichier `shape.pptx` prêt pour la présentation. Aucun script externe n'est requis, et le code fonctionne avec Aspose.Cells 2024‑R2 ou ultérieur.

## Prérequis

* Java 17 ou plus récent (le code se compile avec n'importe quel JDK 8+)
* Bibliothèque Aspose.Cells pour Java (téléchargez depuis le site Aspose ou ajoutez la dépendance Maven)
* Un fichier Excel (`chart.xls`) contenant au moins une forme (un graphique, une zone de texte ou un SmartArt)
* Familiarité de base avec la gestion des exceptions Java

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version>
</dependency>
```

## Comment exporter une forme d'Excel vers PowerPoint (flux global)

Le processus se compose de quatre sections logiques :

1. **Load the workbook** qui contient la forme.  
2. **Locate the shape** sur la première feuille de calcul.  
3. **Configure export options** afin que la forme devienne un objet PowerPoint éditable.  
4. **Save the shape as a PPTX file**.

Chaque section est expliquée en détail ci‑dessous, et le programme complet et exécutable suit les explications.

## Étape 1 : Charger le classeur qui contient la forme

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // Load the Excel workbook. Adjust the path to your environment.
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");
```

*Pourquoi cette étape ?*  
`Workbook` est le point d'entrée pour toutes les opérations Aspose.Cells. Charger le fichier vous donne accès aux feuilles de calcul, aux cellules et à la collection de formes. Si le fichier est introuvable, Aspose.Cells lève une `FileNotFoundException`, que nous interceptons plus tard.

## Étape 2 : Accéder à la première feuille de calcul et récupérer la forme cible

```java
            // Access the first worksheet (index 0)
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // Retrieve the first shape. In most examples the chart is the first shape.
            Shape shape = worksheet.getShapes().get(0);
```

*Pourquoi cette étape ?*  
Les feuilles de calcul sont stockées dans une collection indexée à partir de zéro, donc `get(0)` renvoie la première feuille. Les formes sont également indexées ; `get(0)` récupère la première forme, qui est généralement le graphique que vous souhaitez exporter. Si votre classeur contient plusieurs formes, vous pouvez parcourir la collection ou utiliser `shape.getName()` pour en sélectionner une spécifique.

## Étape 3 : Préparer les options d'exportation – nous voulons la forme comme objet PPTX éditable

```java
            // Create export options. Setting the save format to PPTX tells Aspose.Cells
            // to generate a PowerPoint file rather than an image.
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);
```

*Pourquoi cette étape ?*  
`ImageOrPrintOptions` contrôle la façon dont la forme est rendue. En choisissant `SaveFormat.PPTX`, la bibliothèque convertit le graphique Excel en une forme PowerPoint vectorielle qui reste éditable après l'importation. Ceci est essentiel pour une vraie conversion **shape to PowerPoint** ; utiliser PNG ou JPEG verrouillerait le graphique.

## Étape 4 : Exporter la forme vers un fichier PowerPoint

```java
            // Export the shape. The output file will contain a single slide with the shape.
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

*Pourquoi cette étape ?*  
La méthode `save` écrit la forme en utilisant les options définies précédemment. Le `shape.pptx` résultant contient une seule diapositive où la forme apparaît exactement comme dans Excel, mais vous pouvez maintenant la modifier dans PowerPoint (changer les couleurs, redimensionner, ajouter des animations, etc.). Cela satisfait l'exigence **save shape PPTX**.

## Exemple complet et exécutable

Copiez la classe entière dans un fichier nommé `ExportShapeDemo.java`, remplacez `YOUR_DIRECTORY` par un chemin absolu ou relatif, et exécutez `javac ExportShapeDemo.java && java ExportShapeDemo`. Après l'exécution, vous trouverez `shape.pptx` dans le dossier cible.

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook that contains the chart
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");

            // 2. Access the first worksheet
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // 3. Retrieve the first shape (assumed to be a chart or textbox)
            Shape shape = worksheet.getShapes().get(0);

            // 4. Prepare export options – we want the shape as an editable PPTX object
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);

            // 5. Export the shape to a PowerPoint file
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            System.err.println("An error occurred while exporting the shape:");
            e.printStackTrace();
        }
    }
}
```

### Résultat attendu

```
Export completed. File saved as shape.pptx
```

Ouvrez `shape.pptx` dans Microsoft PowerPoint. Vous verrez une seule diapositive contenant le graphique Excel original (ou la zone de texte) sous forme de forme PowerPoint entièrement éditable.

## Variations courantes et cas limites

| Situation | Ajustement recommandé |
|-----------|------------------------|
| **Multiple shapes** | Parcourir `worksheet.getShapes()` et appeler `save` pour chaque forme, ou sélectionner par `shape.getName()`. |
| **Shape is a chart with data series** | Utilisez `exportOptions.setExportChartAsEditable(true)` pour garder les séries éditables. |
| **Need a specific slide layout** | Après l'enregistrement, ouvrez le PPTX avec Aspose.Slides et insérez la forme dans une mise en page personnalisée. |
| **Large workbook** | Chargez uniquement la feuille de calcul requise en utilisant `Workbook(String, LoadOptions)` pour réduire la consommation de mémoire. |
| **Different output format (PDF, PNG)** | Modifiez `exportOptions.setSaveFormat(SaveFormat.PDF)` ou `SaveFormat.PNG`. Ceci est utile lorsque vous **convert Excel chart** en image statique au lieu d'une forme PowerPoint. |

**Pro tip :** Vérifiez toujours que l'index de la forme (`get(0)`) correspond à l'élément visuel que vous souhaitez exporter. L'ordre de la collection de formes reflète l'ordre d'insertion dans Excel, qui peut différer de l'ordre d'empilement visuel.

## Comment exporter une forme d'Excel vers PowerPoint – liste de contrôle de dépannage

* **File not found** – Assurez‑vous que le chemin dans `new Workbook()` pointe vers un fichier `.xls` ou `.xlsx` existant.  
* **No shapes returned** – Confirmez que la feuille de calcul contient réellement une forme ; vous pouvez appeler `worksheet.getShapes().getCount()` pour déboguer.  
* **Exported file is empty** – Vérifiez que `exportOptions.setSaveFormat(SaveFormat.PPTX)` est défini ; utiliser un format image produira une image au lieu d'une forme.  
* **Compatibility issues** – Aspose.Cells 24.9+ prend en charge l'exportation PPTX sur toutes les principales plateformes. Mettez à jour si vous rencontrez `UnsupportedOperationException`.

## Conclusion

Vous savez maintenant **how to export shape** depuis un classeur Excel et l'intégrer dans une présentation PowerPoint avec Java. Le tutoriel a couvert le chargement du classeur, la localisation de la forme, la configuration des options **export shape from Excel**, et enfin **save shape PPTX**. Avec cette base, vous pouvez automatiser la génération de rapports, créer des tableaux de bord, ou intégrer des visuels Excel dans des présentations sans copier‑coller manuellement.

### Prochaines étapes

* Explorez **convert Excel chart** vers d'autres formats Office tels que PDF ou DOCX.  
* Combinez cette technique avec Aspose.Slides pour placer plusieurs formes sur une même diapositive.  
* Expérimentez les propriétés de `ImageOrPrintOptions` (par ex., `setResolution`, `setTransparent`) pour affiner la qualité visuelle de la forme exportée.

N'hésitez pas à adapter le code pour un traitement par lots ou à l'intégrer dans un service de reporting plus large. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment exporter une forme avec ShapeExportOptions en Java](/cells/english/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/)
- [Comment exporter une feuille Excel vers PowerPoint avec Aspose.Cells en Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [Comment exporter des graphiques d'Excel vers PowerPoint – Guide complet Java](/cells/english/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}