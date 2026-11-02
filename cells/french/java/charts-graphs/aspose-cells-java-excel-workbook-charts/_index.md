---
date: '2026-04-11'
description: Apprenez l'automatisation d'Excel en Java avec Aspose.Cells. Ce tutoriel
  montre comment créer un classeur Excel en Java, remplir des données Excel en Java
  et enregistrer un fichier Excel en Java avec des graphiques.
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: 'Automatisation Excel Java : Créer des classeurs et des graphiques avec Aspose'
url: /fr/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatisation Excel Java : Créer des classeurs et des graphiques avec Aspose

## Introduction

L'automatisation des tâches Excel avec Java peut faire gagner des heures de travail manuel, surtout lorsque vous devez générer des rapports, des tableaux de bord ou des graphiques basés sur les données à la volée. **Excel automation java** avec Aspose.Cells vous offre une API propre et haute performance qui gère tout, de la création de classeur au style sophistiqué des graphiques. Dans ce tutoriel, vous apprendrez comment configurer Aspose.Cells, **create an Excel workbook java**, le remplir avec des données, ajouter un graphique, appliquer un formatage 3D, et enfin **save the Excel file java**.

### Réponses rapides
- **Quelle bibliothèque simplifie l'automatisation Excel en Java ?** Aspose.Cells for Java.  
- **Puis-je ajouter des graphiques 3D programmaticalement ?** Yes – the API supports 3‑D formatting and lighting effects.  
- **Ai-je besoin d'une licence pour le développement ?** A free trial license is available; a commercial license is required for production.  
- **Quels outils de construction Java sont pris en charge ?** Maven and Gradle are both fully supported.  
- **Quels formats de fichiers puis-je exporter ?** XLS, XLSX, CSV, PDF and many more.

## Qu'est-ce que l'automatisation Excel java ?

L'automatisation Excel java désigne le processus de génération, de modification et d'enregistrement de classeurs Excel de manière programmatique à l'aide de code Java. Elle élimine la modification manuelle des feuilles de calcul, assure la cohérence et permet l'intégration avec d'autres systèmes tels que les bases de données ou les services web.

## Pourquoi utiliser Aspose.Cells pour Java ?

- **Rich feature set** – des valeurs de cellules simples aux graphiques complexes, tableaux croisés dynamiques et mise en forme conditionnelle.  
- **No Microsoft Office dependency** – fonctionne dans tout environnement côté serveur.  
- **High performance** – optimisé pour de grands ensembles de données et les scénarios multi‑thread.  
- **Broad format support** – lecture/écriture XLS, XLSX, ODS, CSV, PDF, HTML, et plus.

## Prérequis

- **Java Development Kit (JDK) 8+**  
- **Maven or Gradle** for dependency management  
- **Aspose.Cells for Java 25.3 or later** (trial or licensed)  

## Configuration d'Aspose.Cells pour Java

Ajoutez la bibliothèque à votre projet en utilisant l'une des configurations suivantes.

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Acquisition de licence

Demandez une licence d'essai gratuite sur le site Aspose, ou achetez une licence complète pour une utilisation en production. Placez le fichier de licence dans votre projet et chargez‑le à l'exécution.

## Initialisation et configuration de base

Une fois la dépendance résolue, vous pouvez commencer à coder.

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## Guide étape par étape

### Étape 1 : Comment créer un classeur excel java

Créez une nouvelle instance de classeur qui contiendra toutes vos feuilles de calcul.

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### Étape 2 : Ajouter des feuilles de calcul (y compris une feuille de graphique)

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### Étape 3 : Comment remplir les données excel java

Insérez des données d'exemple que le graphique utilisera comme référence.

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### Étape 4 : Ajouter un graphique en colonnes au classeur

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### Étape 5 : Appliquer le format de couleur à la zone du graphique

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### Étape 6 : Configurer la légende et les séries de données

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### Étape 7 : Appliquer le format 3D aux séries

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### Étape 8 : Définir les couleurs des séries pour une meilleure distinction visuelle

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### Étape 9 : Comment enregistrer le fichier excel java

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## Applications pratiques

- **Financial Reporting** – Générer des états trimestriels avec des graphiques dynamiques.  
- **Data‑Analysis Dashboards** – Créer des tableaux de bord interactifs qui se rafraîchissent automatiquement.  
- **Inventory Management** – Exporter les niveaux de stock et les tendances vers Excel pour la révision des parties prenantes.  
- **Project Planning** – Créer des graphiques de type Gantt directement à partir de systèmes de planification basés sur Java.

## Conseils de performance pour l'automatisation Excel Java

- **Reuse Workbook Objects** lors du traitement de plusieurs feuilles afin de réduire la consommation de mémoire.  
- **Batch Cell Updates** en utilisant `Cells.importArray` pour de grands ensembles de données au lieu d'appels individuels à `putValue`.  
- **Dispose Resources** en appelant `book.dispose()` après l'enregistrement de gros fichiers.

## Questions fréquemment posées

**Q : Puis-je générer un XLSX au lieu d'un XLS ?**  
A : Oui – il suffit de changer l'extension du fichier dans `book.save("output.xlsx")` ; Aspose sélectionne automatiquement le format correct.

**Q : Une licence est‑elle requise pour le développement ?**  
A : Une licence d'essai gratuite fonctionne pour le développement et les tests. Les déploiements en production nécessitent une licence achetée.

**Q : Comment ajouter d'autres types de graphiques ?**  
A : Utilisez l'énumération `ChartType` (par ex., `ChartType.PIE`, `ChartType.LINE`) lors de l'appel à `charts.add(...)`.

**Q : Que faire si je dois protéger le classeur ?**  
A : Appelez `book.getSettings().setPassword("yourPassword")` avant d'enregistrer.

**Q : Aspose.Cells prend‑il en charge les fichiers avec macros ?**  
A : Oui – vous pouvez créer ou conserver des macros VBA dans les classeurs XLSM.

---

**Last Updated:** 2026-04-11  
**Tested With:** Aspose.Cells 25.3 (Java)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}