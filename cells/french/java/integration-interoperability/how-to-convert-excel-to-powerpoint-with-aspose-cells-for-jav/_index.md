---
category: general
date: 2026-11-22
description: Apprenez comment convertir Excel en PowerPoint en utilisant Aspose.Cells
  pour Java, y compris les étapes pour exporter un graphique Excel vers PowerPoint
  dans un flux de travail unique.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- export excel chart to powerpoint
- Aspose.Cells Java
- Excel to PPTX conversion
- Java file format conversion
language: fr
lastmod: 2026-11-22
og_description: Convertissez Excel en PowerPoint avec Aspose.Cells pour Java. Suivez
  ce tutoriel complet étape par étape pour également exporter le graphique Excel vers
  PowerPoint.
og_image_alt: Diagram showing conversion of Excel to PowerPoint using Aspose.Cells
og_title: Convertir Excel en PowerPoint avec Aspose.Cells – Guide Java
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to convert Excel to PowerPoint using Aspose.Cells for Java,
    including steps to export Excel chart to PowerPoint in a single workflow.
  headline: How to convert Excel to PowerPoint with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to convert Excel to PowerPoint using Aspose.Cells for Java,
    including steps to export Excel chart to PowerPoint in a single workflow.
  name: How to convert Excel to PowerPoint with Aspose.Cells for Java
  steps:
  - name: Open `withShapes.pptx` in PowerPoint.
    text: Open `withShapes.pptx` in PowerPoint.
  - name: Confirm that each Excel sheet appears as a separate slide.
    text: Confirm that each Excel sheet appears as a separate slide.
  - name: Check that charts retain their colors, legends, and data labels.
    text: Check that charts retain their colors, legends, and data labels.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- File conversion
title: Comment convertir Excel en PowerPoint avec Aspose.Cells pour Java
url: /fr/java/integration-interoperability/how-to-convert-excel-to-powerpoint-with-aspose-cells-for-jav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment convertir Excel en PowerPoint avec Aspose.Cells pour Java

Si vous devez **convertir Excel en PowerPoint**, ce guide vous montre une méthode simple avec Aspose.Cells pour Java. Vous verrez également comment **exporter un graphique Excel vers PowerPoint** dans le même processus, afin de pouvoir intégrer les graphiques directement dans une présentation sans copier‑coller manuel.

Convertir des feuilles de calcul en présentations est courant lorsque vous souhaitez partager des analyses basées sur des données avec un public non technique. Au lieu de recréer les graphiques dans PowerPoint, vous pouvez automatiser tout le pipeline, conserver le formatage intact et gagner des heures de travail.

Dans ce tutoriel vous allez :

* Configurer Aspose.Cells dans un projet Maven ou Gradle.  
* Charger un classeur existant contenant des données et des graphiques.  
* Configurer `ImageOrPrintOptions` pour cibler le format PPTX.  
* Enregistrer le classeur en tant que présentation PowerPoint.  
* Vérifier le résultat et gérer les cas limites typiques.

> **Pré-requis** – Vous avez besoin d’une licence valide d’Aspose.Cells pour Java (ou vous pouvez travailler avec la version d’évaluation). Le code fonctionne avec Java 8+ et tout IDE qui prend en charge Maven/Gradle.

![Diagram showing conversion of Excel to PowerPoint using Aspose.Cells](convert_excel_to_powerpoint.png)

## Ce dont vous avez besoin

| Item | Reason |
|------|--------|
| **Java Development Kit (JDK) 8 or newer** | Nécessaire pour compiler et exécuter l'exemple. |
| **Maven or Gradle** | Simplifie la gestion des dépendances pour Aspose.Cells. |
| **Aspose.Cells for Java** | Fournit les API `Workbook` et `ImageOrPrintOptions` utilisées pour la conversion. |
| **An Excel file (`shapes.xlsx`) containing at least one chart** | Illustre le scénario *exporter un graphique Excel vers PowerPoint*. |

## Étape 1 : Ajouter Aspose.Cells à votre projet

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest version -->
</dependency>
```

### Gradle

```gradle
implementation 'com.aspose:aspose-cells:24.10' // latest version as of 2026
```

> **Pourquoi cette étape est importante** – Ajouter la bibliothèque rend les classes `Workbook`, `ImageOrPrintOptions` et `SaveFormat` disponibles. Sans la dépendance correcte, le code ne compilera pas.

## Étape 2 : Charger le classeur contenant le(s) graphique(s)

```java
import com.aspose.cells.Workbook;

// Load the Excel file. Replace the path with your actual location.
Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
```

**Explication :**  
`Workbook` est le point d’entrée pour toutes les opérations Excel. En chargeant `shapes.xlsx`, vous chargez à la fois les tableaux de données et les graphiques intégrés en mémoire, ce qui permet la conversion suivante.

## Étape 3 : Créer les options de conversion et définir le format cible sur PPTX

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.SaveFormat;

// Configure options for image/print conversion.
ImageOrPrintOptions options = new ImageOrPrintOptions();
// The SaveFormat.PPTX constant tells Aspose.Cells to generate a PowerPoint file.
options.setSaveFormat(SaveFormat.PPTX);
```

**Pourquoi utiliser `ImageOrPrintOptions` ?**  
Ces options contrôlent la façon dont chaque feuille de calcul ou graphique est rendu. Définir `SaveFormat.PPTX` indique à la bibliothèque de placer chaque feuille (ou graphique) sur une diapositive distincte, en préservant la fidélité visuelle.

## Étape 4 : Enregistrer le classeur en tant que présentation PowerPoint

```java
// The second argument is the options object we just configured.
workbook.save("YOUR_DIRECTORY/withShapes.pptx", options);
```

**Que se passe-t-il ici ?**  
Aspose.Cells parcourt les feuilles de calcul et les graphiques du classeur, les rasterise en graphiques compatibles avec les diapositives, et écrit un paquet `.pptx` à l’emplacement spécifié. Le fichier résultant peut être ouvert dans Microsoft PowerPoint, Google Slides ou tout visualiseur compatible PPTX.

## Étape 5 : Vérifier la conversion

1. Ouvrez `withShapes.pptx` dans PowerPoint.  
2. Vérifiez que chaque feuille Excel apparaît comme une diapositive distincte.  
3. Assurez‑vous que les graphiques conservent leurs couleurs, légendes et étiquettes de données.  

Si un graphique apparaît déformé, vous devrez peut‑être ajuster le DPI de `ImageOrPrintOptions` :

```java
options.setResolution(300); // 300 DPI gives higher quality for complex charts
```

## Exporter un graphique Excel vers PowerPoint – une variante ciblée

Parfois vous n’avez besoin de déplacer qu’un seul graphique plutôt que l’ensemble du classeur. Vous pouvez y parvenir en convertissant d’abord le graphique en image puis en l’insérant manuellement dans une diapositive PowerPoint, mais Aspose.Cells simplifie le processus :

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;
import com.aspose.cells.SaveOptions;

// Assume the chart is on the first worksheet, first chart object.
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);

// Create options for converting the chart to an image.
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions();
chartOptions.setImageFormat(ImageFormat.PNG);
chartOptions.setSaveFormat(SaveFormat.PPTX);

// Save only the chart as a PPTX slide.
chart.save("YOUR_DIRECTORY/singleChart.pptx", chartOptions);
```

**Pourquoi c’est important :**  
Le fragment isole un seul graphique, réduit la taille du fichier et vous donne un contrôle plus fin sur les visuels qui deviennent des diapositives. C’est la façon la plus directe d’**exporter un graphique Excel vers PowerPoint** lorsque vous n’avez pas besoin du classeur complet.

## Problèmes courants et comment les éviter

| Issue | Cause | Fix |
|-------|-------|-----|
| **Diapositives vides** | La feuille de calcul ne contient aucune donnée visible ou le graphique est masqué. | Assurez‑vous que le graphique est visible et que la feuille de calcul contient des données avant l’enregistrement. |
| **Images à basse résolution** | Le DPI par défaut est 96, ce qui peut être insuffisant pour des diapositives imprimées. | Appelez `options.setResolution(200‑300)` avant `workbook.save`. |
| **Types de graphiques non pris en charge** | Des types de graphiques très récents ou personnalisés peuvent ne pas être rendus parfaitement. | Exportez le graphique en tant qu’image (`ImageFormat.PNG`) puis insérez‑le manuellement. |
| **Erreurs de chemin de fichier** | Chemin relatif incorrect sur différents systèmes d’exploitation. | Utilisez `Paths.get("YOUR_DIRECTORY", "file.xlsx").toString()` pour des chemins indépendants de la plateforme. |

## Astuces pro pour des conversions de niveau production

* **Traitement par lots :** Parcourez un répertoire de fichiers Excel et appelez la même logique de conversion.  
* **Gestion de la mémoire :** Pour les classeurs volumineux, invoquez `workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` afin de réduire l’utilisation du tas.  
* **Activation de licence :** Placez votre fichier de licence (`Aspose.Cells.lic`) dans le classpath et appelez `License license = new License(); license.setLicense("Aspose.Cells.lic");` avant toute utilisation de l’API Aspose.  
* **Sécurité des threads :** Chaque thread doit travailler avec sa propre instance `Workbook` ; les objets Aspose.Cells ne sont pas thread‑safe.

## Exemple complet fonctionnel

```java
import com.aspose.cells.*;

public class ExcelToPowerPointDemo {
    public static void main(String[] args) throws Exception {
        // 1. Optional: activate your Aspose.Cells license.
        // License license = new License();
        // license.setLicense("Aspose.Cells.lic");

        // 2. Load the workbook that contains charts.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");

        // 3. Set conversion options – target PPTX format.
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.PPTX);
        // Increase resolution for sharper charts (optional).
        options.setResolution(300);

        // 4. Save the workbook as a PowerPoint presentation.
        workbook.save("YOUR_DIRECTORY/withShapes.pptx", options);

        // 5. (Optional) Export only the first chart to its own PPTX.
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        ImageOrPrintOptions chartOpts = new ImageOrPrintOptions();
        chartOpts.setSaveFormat(SaveFormat.PPTX);
        chart.save("YOUR_DIRECTORY/singleChart.pptx", chartOpts);

        System.out.println("Conversion completed successfully.");
    }
}
```

**Sortie attendue :**  

L’exécution du programme affiche `Conversion completed successfully.` et crée deux fichiers :

* `withShapes.pptx` – un jeu de diapositives où chaque feuille (et ses graphiques) apparaît sur une diapositive distincte.  
* `singleChart.pptx` – une présentation à une seule diapositive contenant uniquement le premier graphique du classeur.

Ouvrez ces fichiers dans PowerPoint pour vérifier que les graphiques conservent leur style original et leurs étiquettes de données.

## Conclusion

Vous savez maintenant comment **convertir Excel en PowerPoint** en utilisant Aspose.Cells pour Java, et vous avez également découvert la façon la plus efficace d’**exporter un graphique Excel vers PowerPoint** lorsqu’un visuel spécifique est requis. En configurant `ImageOrPrintOptions` et en définissant le `SaveFormat` sur `PPTX`, la bibliothèque se charge du rendu lourd des feuilles et des graphiques en graphiques compatibles avec les diapositives.

À partir d’ici, vous pouvez :

* Automatiser les conversions par lots pour les pipelines de reporting.  
* Combiner le PPTX généré avec d’autres éléments de diapositives en utilisant l’API Apache POI `XSLF`.  
* Explorer des formats d’exportation supplémentaires tels que PDF ou HTML pour une distribution multicanal.

N’hésitez pas à expérimenter avec les réglages DPI, les mises en page de diapositives personnalisées, ou à intégrer le PPTX généré dans des flux de travail d’e‑mail. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment exporter une feuille Excel vers PowerPoint avec Aspose.Cells en Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [Comment convertir Excel en PDF en Java en utilisant Aspose.Cells : guide étape par étape](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Comment exporter un graphique vers docx depuis Excel en utilisant Aspose.Cells pour Java](/cells/english/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}