---
date: 2026-09-02
description: Apprenez à créer un graphique en cascade Excel en Java avec Aspose.Cells,
  à définir la plage de données du graphique, à personnaliser les libellés et à exporter
  vers XLSX.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: Graphiques en cascade
og_description: Créez un graphique en cascade Excel avec Aspose.Cells pour Java –
  définissez la plage de données du graphique, ajoutez des libellés de données et
  exportez vers XLSX en quelques étapes.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Créer un graphique en cascade Excel avec Aspose.Cells pour Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Créer un graphique en cascade Excel avec Aspose.Cells pour Java
url: /fr/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Graphiques en cascade

## Introduction aux graphiques en cascade avec Aspose.Cells pour Java

Dans ce tutoriel, vous apprendrez à **créer un graphique en cascade Excel** et à **définir la plage de données du graphique** avec Aspose.Cells pour Java. Les graphiques en cascade transforment une série de nombres positifs et négatifs en une histoire visuelle claire, les rendant idéaux pour les états financiers, les revues de performance des ventes, et tout scénario où vous devez voir comment chaque élément contribue à un total.

## Réponses rapides
- **Qu'est‑ce qu'un graphique en cascade ?** Un visuel qui montre comment une valeur initiale est augmentée et diminuée par une série de valeurs intermédiaires, se terminant par un total final.  
- **Quelle bibliothèque est utilisée ?** Aspose.Cells for Java.  
- **Ai‑je besoin d'une licence ?** Un essai gratuit suffit pour le développement ; une licence commerciale est requise pour la production.  
- **Puis‑je enregistrer le fichier au format XLSX ?** Oui – utilisez `workbook.save("FileName.xlsx")`.  
- **Est‑il adapté à la visualisation de données Java ?** Absolument ; Aspose.Cells offre des fonctionnalités de graphiques riches sans besoin d'Office installé.

## Qu'est‑ce qu'un graphique en cascade ?
Un graphique en cascade affiche les contributions positives et négatives séquentielles à une valeur de départ, vous aidant à comprendre comment chaque composant impacte le résultat global. En visualisant gains et pertes côte à côte, il rend les flux financiers complexes immédiatement lisibles.

## Pourquoi utiliser Aspose.Cells pour Java pour ajouter un graphique en cascade ?
Aspose.Cells vous permet de générer des graphiques Excel sur n'importe quel serveur, pipeline CI ou poste de travail sans nécessiter Microsoft Excel. Il prend en charge **plus de 15 formats de sortie** (XLSX, PDF, HTML, CSV, et plus), traite des classeurs contenant **plus de 500 lignes** en moins d'une seconde, et offre un contrôle programmatique sur chaque élément du graphique — des couleurs aux étiquettes de données.

## Prérequis

Avant de plonger dans le code, assurez‑vous d'avoir les prérequis suivants en place :

- Aspose.Cells pour Java : Vous devez disposer d'Aspose.Cells pour Java installé. Vous pouvez le télécharger depuis la page de version d'Aspose.Cells pour Java : [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Environnement de développement Java : Assurez‑vous d'avoir Java installé sur votre système et un outil de construction (Maven/Gradle) prêt.

Maintenant, commençons à créer le graphique en cascade étape par étape.

## Comment définir la plage de données d'un graphique en cascade en Java
Chargez un nouveau classeur, remplissez‑le avec des données, ajoutez un objet `Chart`, définissez la plage de la série, puis enregistrez le fichier. Ce processus est simple : vous créez un classeur, remplissez les cellules avec des catégories et des valeurs, créez un graphique, liez les plages de données, puis exportez le classeur. Le résultat est un graphique en cascade entièrement fonctionnel prêt à être utilisé dans des rapports ou des tableaux de bord.

### Étape 1 : importer Aspose.Cells
Le package `com.aspose.cells` contient toutes les classes requises pour la manipulation d'Excel, y compris la création de classeurs, la gestion de feuilles de calcul et la génération de graphiques.

### Étape 2 : initialiser le classeur et la feuille de calcul
Un **Workbook** représente un fichier Excel, et une **Worksheet** est une feuille unique à l'intérieur de ce fichier. Créer ces objets fournit la toile pour les données brutes et le graphique.

### Étape 3 : saisir les données
La colonne A contient les libellés de catégorie, tandis que la colonne B contient les valeurs numériques du graphique en cascade. Cette disposition correspond au flux typique de profit‑et‑perte utilisé dans l'analyse financière.

### Étape 4 : créer le graphique en cascade
L'objet **Chart** crée une représentation visuelle ; définir son type sur `ChartType.WATERFALL` le configure comme un graphique en cascade. Utilisez la méthode `add` pour définir la plage de données du graphique pour la série (`"B2:B6"`), et liez l'axe des catégories à `"A2:A6"`.

### Étape 5 : enregistrer le classeur
En enregistrant le classeur, le graphique et les données sont écrits dans le format de fichier spécifié. Appelez `workbook.save("WaterfallChart.xlsx")` pour générer un fichier XLSX, ou modifiez le paramètre de format pour exporter en PDF, CSV ou HTML.

## Problèmes courants et solutions

- **Le graphique apparaît vide** – Vérifiez que les références de plage de données (`B2:B6` et `A2:A6`) correspondent aux cellules réelles contenant vos valeurs et catégories.  
- **Les valeurs négatives ne s'affichent pas correctement** – Assurez‑vous que le type de série est défini sur `ChartType.WATERFALL` ; les autres types de graphiques traitent les négatifs différemment.  
- **Le fichier ne s'ouvre pas dans Excel** – Utilisez la dernière version d'Aspose.Cells et assurez‑vous que l'extension du fichier correspond au format (`.xlsx` pour Excel).

## Questions fréquentes

### Comment puis‑je personnaliser l'apparence de mon graphique en cascade ?
Vous pouvez modifier des propriétés telles que `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` pour changer la couleur des barres, activer les étiquettes de données avec `setShowDataLabels(true)`, et ajuster les titres des axes via `getCategoryAxis().setTitle("Stage")`. La référence API Aspose.Cells fournit une liste complète des options personnalisables.

### Puis‑je créer plusieurs graphiques en cascade dans la même feuille de calcul ?
Oui. Après avoir ajouté le premier graphique, répétez les étapes de création du graphique avec une plage de données différente et un nouvel objet `Chart`. Chaque graphique est indépendant et peut être positionné n'importe où sur la feuille.

### Aspose.Cells est‑il compatible avec différents environnements de développement Java ?
Absolument. La bibliothèque fonctionne avec Eclipse, IntelliJ IDEA, NetBeans, et tout système de construction supportant Maven ou Gradle. Aucun plugin supplémentaire n'est requis.

### Puis‑je ajouter des séries de données supplémentaires à mon graphique en cascade ?
Vous pouvez ajouter plus de séries en appelant `chart.getNSeries().add("C2:C6", true)` et en configurant chaque série séparément. Cela vous permet de comparer plusieurs scénarios côte à côte.

### Où puis‑je trouver plus de ressources et d'exemples pour Aspose.Cells pour Java ?
Explorez la documentation complète à la référence API Java d'Aspose.Cells : [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## FAQ

**Q : Comment définir la plage de données du graphique pour un graphique en cascade financier ?**  
R : Utilisez la méthode `add` sur la série du graphique, en passant la plage de cellules contenant vos valeurs, par ex., `"B2:B6"`.

**Q : Puis‑je exporter le classeur en PDF au lieu de XLSX ?**  
R : Oui, appelez `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` pour générer une version PDF.

**Q : Que faire si je dois créer un graphique en cascade avec plus de catégories ?**  
R : Étendez la plage de données dans les colonnes de valeurs et de catégories, puis mettez à jour les appels `add` et `setCategoryData` en conséquence.

**Q : Existe‑t‑il un moyen de formater automatiquement les barres positives et négatives ?**  
R : Parcourez la collection `Series` et définissez la couleur `FillFormat` en fonction du signe de chaque valeur ; Aspose.Cells vous permet d'appliquer un format conditionnel par programme.

**Q : Aspose.Cells prend‑il en charge les mises à jour dynamiques des données pour les graphiques ?**  
R : Oui. Après avoir modifié les valeurs des cellules, il suffit de ré‑enregistrer le classeur — le graphique reflétera automatiquement les nouvelles données.

---

**Dernière mise à jour :** 2026-09-02  
**Testé avec :** Aspose.Cells for Java (latest)  
**Auteur :** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## Tutoriels associés

- [Personnaliser les étiquettes de données d'un graphique Excel avec Aspose.Cells pour Java : guide étape par étape](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Ajouter des étiquettes de données à un graphique Excel avec Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Comment créer et exporter des graphiques en Java avec Aspose.Cells : guide complet](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}