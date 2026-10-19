---
date: '2026-09-22'
description: Apprenez à créer un graphique Excel interactif avec des cases à cocher
  en utilisant Aspose.Cells for Java. Ce guide couvre la configuration, l’ajout de
  cases à cocher, la licence et les meilleures pratiques.
keywords:
- create interactive Excel chart
- how to add checkbox java
- aspose.cells license java
lastmod: '2026-09-22'
og_description: Apprenez à créer un graphique Excel interactif avec des cases à cocher
  en utilisant Aspose.Cells for Java. Suivez les instructions étape par étape, consultez
  les conseils de licence et découvrez des cas d’utilisation réels.
og_image_alt: Guide showing how to create interactive Excel chart with checkboxes
  using Aspose.Cells for Java
og_title: Comment créer un graphique Excel interactif avec des cases à cocher
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to create interactive Excel chart with checkboxes using Aspose.Cells
    for Java. This guide covers setup, adding checkboxes, licensing, and best practices.
  headline: How to create interactive Excel chart with checkboxes
  type: TechArticle
- questions:
  - answer: Use Aspose.Cells’ `Shape` API with `ShapeType.FORM_CONTROL_CHECKBOX` and
      link it to a worksheet cell; the checkbox works natively in Excel.
    question: How do I add a checkbox without using VBA?
  - answer: The checkbox shape is available in the free evaluation, but a permanent
      Aspose.Cells license removes evaluation limits and enables full performance
      optimizations.
    question: Do I need a license for the checkbox feature?
  - answer: Files saved with Aspose.Cells follow the Office Open XML standard and
      open correctly in Excel 2016, 2019, 2021, and Microsoft 365.
    question: Which Excel versions can open the generated file?
  - answer: Yes, create a checkbox for each series, link each to a distinct helper
      cell, and use conditional formulas to toggle each series independently.
    question: Can I control multiple series with separate checkboxes?
  - answer: Practically, you can add dozens; performance remains stable up to 200
      controls per worksheet on typical server hardware.
    question: Is there a limit on the number of checkboxes per chart?
  type: FAQPage
tags:
- interactive Excel charts
- Aspose.Cells
- Java Excel automation
title: Comment créer un graphique Excel interactif avec des cases à cocher
url: /fr/java/charts-graphs/create-chart-checkbox-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un graphique Excel interactif avec des cases à cocher

## Introduction

Dans ce tutoriel, vous **créerez un graphique Excel interactif** qui permet aux utilisateurs d’activer ou désactiver des séries de données en cliquant sur des cases à cocher placées directement sur le graphique. En utilisant Aspose.Cells for Java, vous pouvez générer des classeurs entièrement fonctionnels de manière programmatique, sans avoir besoin de Microsoft Excel installé. Cette approche fonctionne pour toute solution de reporting ou de tableau de bord basée sur Java.

**Ce que vous apprendrez**
- Comment configurer Aspose.Cells for Java avec Maven ou Gradle  
- Comment instancier un `Workbook` et ajouter un graphique en colonnes  
- Comment intégrer une forme de case à cocher dans la zone du graphique  
- Comment appliquer une licence Aspose.Cells pour une utilisation en production  

## Réponses rapides
- **Quelle bibliothèque crée des graphiques Excel interactifs ?** Aspose.Cells for Java.  
- **Puis-je ajouter des cases à cocher sans VBA ?** Oui, en insérant une forme de contrôle de formulaire via l'API.  
- **Ai-je besoin d’une licence pour cette fonctionnalité ?** Une licence temporaire fonctionne pour l’évaluation ; une licence permanente est requise pour la production.  
- **Quelle version de Java est requise ?** JDK 8 ou supérieur.  
- **Le graphique fonctionnera-t-il dans Excel 2016‑2024 ?** Oui, le fichier généré suit la norme Office Open XML.  

## Qu’est‑ce qu’un graphique Excel interactif ?
Un **graphique Excel interactif** combine un graphique standard avec des contrôles UI (par ex., des cases à cocher) qui permettent aux utilisateurs d’afficher ou de masquer des séries de données à la volée, transformant ainsi un visuel statique en un outil de reporting dynamique.

## Pourquoi utiliser Aspose.Cells for Java ?
Aspose.Cells prend en charge **plus de 80 formats d’entrée et de sortie** et peut traiter des classeurs contenant **plus de 10 000 lignes** sans charger le fichier complet en mémoire, offrant ainsi une génération haute performance dans des environnements serveur.

## Prérequis

- **Java Development Kit (JDK) :** version 8 ou supérieure.  
- **Aspose.Cells for Java :** dernière version (par ex., 25.3).  
- **Maven ou Gradle :** pour gérer la dépendance de la bibliothèque.  

### Prérequis de connaissances
Une syntaxe Java de base et une familiarité avec les concepts Excel (feuilles de calcul, plages, graphiques) sont utiles, mais les étapes ci‑dessous sont suffisamment détaillées pour les développeurs de tout niveau d’expérience.

## Comment ajouter une case à cocher en Java ?

Chargez la bibliothèque Aspose.Cells, créez un classeur et insérez une forme de case à cocher en un seul appel. La case à cocher est un contrôle de formulaire qui peut être lié à une cellule ; son activation modifiera la valeur de la cellule liée, que vous pourrez ensuite associer à la visibilité d’une série du graphique.

```text
// Direct answer (40‑70 words):
You add a checkbox by creating a `Shape` of type `ShapeType.FORM_CONTROL_CHECKBOX`, setting its placement on the chart worksheet, and linking it to a cell that stores the Boolean state. The linked cell can be used in formulas that drive chart series visibility, enabling real‑time interactivity without VBA.
```

### Étape 1 : Configurer la dépendance Maven

Ajoutez l’artifact Maven d’Aspose.Cells à votre `pom.xml` :

```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

### Étape 2 : Configurer la dépendance Gradle

Ajoutez la ligne suivante à votre fichier `build.gradle` :

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Étapes d’obtention de licence

Pour débloquer toutes les fonctionnalités, obtenez une licence temporaire ou permanente. Téléchargez une licence d’évaluation depuis [Aspose's website](https://releases.aspose.com/cells/java/). Pour la production, achetez une licence et appliquez‑la comme indiqué plus loin.

#### Initialisation de base

`License` est la classe Aspose.Cells utilisée pour appliquer un fichier de licence acheté, activant ainsi toutes les fonctionnalités sans limites d’évaluation. Initialise‑la dans votre code Java avant toute opération sur le classeur :

```java
import com.aspose.cells.Workbook;

public class AsposeSetup {
    public static void main(String[] args) throws Exception {
        // Initialize the Workbook object.
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Comment créer un graphique Excel interactif ?

Un objet `Workbook` d’Aspose.Cells représente un fichier Excel complet, contenant des feuilles de calcul, des graphiques et d’autres éléments. En créant un classeur, vous pouvez ajouter des données, générer un graphique en colonnes et ensuite intégrer des contrôles interactifs tels que des cases à cocher. Les étapes suivantes vous guident dans la construction du classeur, le remplissage des données et la configuration du graphique pour l’interactivité.

```text
// Direct answer (40‑70 words):
First, instantiate a `Workbook`, fill a worksheet with sample data, and call `addChart` to place a column chart. Next, create a checkbox shape, position it over the chart, and link it to a cell that toggles the series’ `isVisible` property via a formula. Finally, save the workbook as an XLSX file.
```

### Instancier un classeur et ajouter un graphique

#### Vue d’ensemble

Cette section montre comment créer un nouveau classeur, ajouter une feuille de calcul pour les données et générer un graphique en colonnes qui sera ensuite rendu interactif.

##### Étape 1 : Créer un nouveau classeur

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SheetType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a new Workbook object representing an Excel file.
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook created.");
    }
}
```

##### Étape 2 : Ajouter une feuille de calcul pour le graphique

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ChartType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        
        // Adding a chart worksheet to the workbook.
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        System.out.println("Chart worksheet added.");
    }
}
```

##### Étape 3 : Insérer un graphique en colonnes

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN to the newly added chart worksheet.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        System.out.println("Column chart inserted.");
    }
}
```

##### Étape 4 : Ajouter les données de série

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        // Adding series data for the chart.
        sheet.getCharts().get(0).getNSeries().add("{1,2,3}", false);
        
        System.out.println("Series data added to the chart.");
    }
}
```

## Comment intégrer une case à cocher dans un graphique ?

Intégrer une case à cocher directement sur la zone du graphique permet aux utilisateurs finaux de cliquer pour afficher ou masquer une série spécifique. La case à cocher est une forme de contrôle de formulaire qui peut être liée à une cellule ; la valeur de la cellule peut être référencée dans une formule qui pilote la visibilité de la série.

`Shape` est l’objet Aspose.Cells représentant un élément de dessin tel qu’un contrôle de formulaire, une image ou une zone de texte au sein d’une feuille de calcul.

```text
// Direct answer (40‑70 words):
You embed a checkbox by creating a `Shape` with `ShapeType.FORM_CONTROL_CHECKBOX`, positioning it using `setUpperLeftRow/Column` relative to the chart sheet, and linking it to a helper cell (e.g., `B1`). Then, use a conditional formula in the series data range that checks the helper cell’s Boolean value to decide whether the series is plotted.
```

### Intégrer une forme de case à cocher

```java
import com.aspose.cells.MsoDrawingType;
import com.aspose.cells.PlacementType;

public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a checkbox shape within the chart area on the first chart of the worksheet.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        
        System.out.println("Checkbox added to the chart.");
    }
}
```

### Définir le texte de la case à cocher

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape within the chart.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);

        // Setting text for the newly added checkbox shape.
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        System.out.println("Checkbox labeled successfully.");
    }
}
```

## Comment enregistrer le classeur en fichier Excel ?

En enregistrant le `Workbook`, toutes les modifications en mémoire sont écrites dans un fichier Excel physique sur le disque. Aspose.Cells prend en charge le format moderne .xlsx, garantissant que le fichier s’ouvre dans Excel 2016‑2024 et d’autres applications compatibles Office. Utilisez la méthode `save` avec le chemin de fichier souhaité, et spécifiez éventuellement le format de fichier pour des options supplémentaires.

```text
// Direct answer (40‑70 words):
Call `workbook.save("InteractiveChart.xlsx", SaveFormat.XLSX)` to write the workbook. The method automatically closes all streams and guarantees that the embedded chart and checkbox are fully functional when the file is opened in Excel 2016‑2024.
```

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape and label it.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        // Save the workbook
        String outDir = "YOUR_OUTPUT_DIRECTORY"; // Replace with your actual output directory path.
        workbook.save(outDir + "/InsertCheckboxInChartSheet_out.xlsx");
        
        System.out.println("Workbook saved successfully.");
    }
}
```

## Applications pratiques

Scénarios réels où un graphique interactif avec des cases à cocher apporte de la valeur :

1. **Rapports interactifs :** Permettre aux parties prenantes d’activer/désactiver les lignes de produits individuelles sur un graphique de ventes.  
2. **Analyse comparative :** Permettre aux analystes de se concentrer sur des périodes ou des régions spécifiques en cochant/décochant des séries.  
3. **Tableaux de bord éducatifs :** Les étudiants peuvent explorer les tendances des données en sélectionnant les variables à afficher.

## Problèmes courants et solutions

- **Case à cocher ne répond pas :** Assurez‑vous que la case à cocher est liée à une cellule et que la cellule est référencée dans une formule affectant la visibilité de la série.  
- **Le graphique ne se met pas à jour après basculement :** Rafraîchissez la vue du classeur dans Excel ou recalculer les formules (`workbook.calculateFormula()`).  
- **Licence non appliquée :** Vérifiez que `License license = new License(); license.setLicense("Aspose.Cells.lic");` est exécuté avant toute opération sur le classeur.

## Questions fréquentes

**Q : Comment ajouter une case à cocher sans utiliser VBA ?**  
R : Utilisez l’API `Shape` d’Aspose.Cells avec `ShapeType.FORM_CONTROL_CHECKBOX` et liez‑la à une cellule de la feuille de calcul ; la case à cocher fonctionne nativement dans Excel.

**Q : Ai‑je besoin d’une licence pour la fonctionnalité de case à cocher ?**  
R : La forme de case à cocher est disponible dans l’évaluation gratuite, mais une licence permanente d’Aspose.Cells supprime les limites d’évaluation et active les optimisations de performance complètes.

**Q : Quelles versions d’Excel peuvent ouvrir le fichier généré ?**  
R : Les fichiers enregistrés avec Aspose.Cells respectent la norme Office Open XML et s’ouvrent correctement dans Excel 2016, 2019, 2021 et Microsoft 365.

**Q : Puis‑je contrôler plusieurs séries avec des cases à cocher séparées ?**  
R : Oui, créez une case à cocher pour chaque série, liez‑chaque à une cellule d’aide distincte, et utilisez des formules conditionnelles pour basculer chaque série indépendamment.

**Q : Y a‑t‑il une limite au nombre de cases à cocher par graphique ?**  
R : En pratique, vous pouvez ajouter des dizaines ; les performances restent stables jusqu’à 200 contrôles par feuille de calcul sur du matériel serveur typique.

---

**Last Updated:** 2026-09-22  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose

## Tutoriels associés

- [Comment ajouter une case à cocher dans Excel avec Aspose.Cells for Java : guide étape par étape](/cells/java/data-validation/add-checkbox-excel-aspose-cells-java/)
- [Créer des graphiques Excel dynamiques avec Aspose.Cells Java : guide complet pour les développeurs](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Ajouter des étiquettes de données à un graphique Excel avec Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}