---
date: 2026-09-02
description: Apprenez comment exporter le chart au format PNG, ajouter data series,
  combiner un line column chart, enregistrer le workbook au format XLSX et ajouter
  legend chart en utilisant Aspose.Cells for Java.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Exporter le chart au format PNG et ajouter data series pour le combined
  chart
og_description: Exporter le chart au format PNG avec Aspose.Cells for Java, combiner
  un line and column chart, ajouter data series, et enregistrer le workbook au format
  XLSX dans un seul tutoriel.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Exporter le chart au format PNG et ajouter data series pour le combined
  chart
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: Exporter le chart au format PNG et ajouter data series pour le combined chart
url: /fr/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter le graphique au format PNG et ajouter des séries de données pour un graphique combiné

Dans ce tutoriel, vous allez **ajouter des séries de données** à un classeur Excel, **combiner des éléments de graphique ligne et colonne**, et apprendre comment **exporter le graphique au format PNG** en utilisant Aspose.Cells for Java. Nous parcourrons chaque étape — depuis la configuration du classeur, l'ajout du graphique à une feuille de calcul, la personnalisation de la légende, jusqu'à **enregistrer le classeur au format XLSX** et générer une image PNG du graphique. À la fin, vous disposerez d'un graphique combiné prêt à l'emploi que vous pourrez intégrer dans des rapports ou des tableaux de bord.

## Réponses rapides
- **Quelle bibliothèque crée des graphiques combinés ?** Aspose.Cells for Java.  
- **Comment ajouter une série de données ?** Call `chart.getNSeries().add(...)` with the appropriate range.  
- **Comment exporter le graphique au format PNG ?** Use `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **Quel format de fichier puis‑je enregistrer le classeur ?** Standard `.xlsx` (save workbook as XLSX).  
- **Ai‑je besoin d’une licence pour la production ?** Yes – a valid Aspose.Cells license is required for production deployments.

## Qu’est‑ce que l’exportation d’un graphique au format PNG dans Aspose.Cells ?
Exporter un graphique au format PNG crée une image raster du graphique Excel qui peut être affichée dans des pages web, des rapports ou des e‑mails sans nécessiter l’application Excel. Cette méthode capture la mise en page visuelle exacte, les couleurs et les marqueurs de données, produisant un fichier image portable.

## Pourquoi créer un graphique combiné ligne‑colonne ?
Un graphique combiné ligne‑colonne vous permet d’afficher différents ensembles de données avec des représentations visuelles distinctes (par ex., une série en ligne superposée à une série en colonne) dans une même vue. Cette approche est idéale pour comparer les tendances aux totaux, mettre en évidence des corrélations ou fournir des insights plus riches tout en conservant une empreinte visuelle réduite.

## Pré‑requis
- Java Development Kit (JDK) 8 ou supérieur  
- Bibliothèque Aspose.Cells for Java (télécharger depuis le lien ci‑dessous)  
- Familiarité de base avec la syntaxe Java et les concepts Excel  

## Commencer

Tout d’abord, téléchargez la bibliothèque Aspose.Cells for Java depuis le site officiel :

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Une fois le JAR ajouté au classpath de votre projet, vous pouvez commencer à créer le graphique.

### Étape 1 : importer les classes aspose.cells
`Workbook` est l’objet principal d’Aspose.Cells qui représente un fichier Excel complet en mémoire.  
```java
import com.aspose.cells.*;
```

### Étape 2 : créer un nouveau classeur
`Worksheet` représente une feuille unique à l’intérieur d’un `Workbook` et fournit l’accès aux cellules, lignes et graphiques.  
```java
Workbook workbook = new Workbook();
```

### Étape 3 : accéder à la première feuille de calcul
`Chart` est l’objet qui contient tous les paramètres liés au graphique, les séries et les options de rendu.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Étape 4 : ajouter un objet graphique combiné à la feuille de calcul  
Nous commencerons avec un graphique en ligne et ajouterons plus tard une série en colonne pour obtenir un effet de **graphique combiné ligne‑colonne**.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Ajouter des données au graphique

Maintenant que le conteneur du graphique existe, nous devons le alimenter en données.

### Étape 5 : définir les plages de données et ajouter des séries de données
`NSeries` est la collection qui stocke chaque série de données pour un graphique. Ajouter une série lie une plage de cellules au graphique.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Astuce :** Le premier paramètre (`"A1:A5"`) est la plage pour la première série, et le second (`"B1:B5"`) crée une deuxième série qui sera combinée avec la première.

### Étape 6 : définir les données de catégorie (axe X)
`CategoryAxis` représente l’axe horizontal du graphique, contrôlant les libellés affichés le long de l’axe X.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Personnaliser le graphique

Un bon graphique raconte une histoire. Donnons‑lui des titres, des libellés d’axes et une légende claire.

### Étape 7 : définir les libellés des axes du graphique et le titre
`Title` définit le titre principal du graphique, et les objets `Axis` représentent les axes X et Y.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Étape 8 : ajouter la légende du graphique et ajuster sa position
`Legend` contrôle le placement et l’apparence de la légende des séries dans le graphique.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Enregistrer et exporter le graphique

Après la personnalisation, vous voudrez **enregistrer le classeur au format XLSX** et également générer une image.

### Étape 9 : enregistrer le classeur en tant que fichier Excel (XLSX)
`Workbook.save` écrit le classeur en mémoire dans un fichier au format spécifié.  
```java
workbook.save("CombinedChart.xlsx");
```

### Étape 10 : exporter le graphique au format PNG
`Chart.toImage` rend le graphique sous forme de fichier image dans le format choisi.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> La méthode `chart.toImage` **génère des images de graphiques Excel** qui peuvent être utilisées dans des pages web, des rapports ou des e‑mails.

## Problèmes courants et dépannage

| Problème | Solution |
|----------|----------|
| **Aucune donnée n’apparaît** | Vérifiez que les plages de cellules (`A1:A5`, `B1:B5`, `C1:C5`) contiennent réellement des données avant de créer le graphique. |
| **La légende chevauche le graphique** | Définissez `chart.getLegend().setOverlay(false)` ou déplacez la légende à une autre position (par ex., `RIGHT`). |
| **Le fichier image est vide** | Assurez‑vous que le graphique possède au moins une série et que `chart.toImage` est appelé après toutes les personnalisations. |
| **L’enregistrement génère une exception** | Vérifiez que vous avez les droits d’écriture sur le répertoire cible et que le fichier n’est pas ouvert dans Excel. |

## Questions fréquentes

**Q :** Comment installer Aspose.Cells for Java ?  
**R :** Téléchargez le JAR depuis le site officiel et ajoutez‑le au classpath de votre projet. Le lien de téléchargement est : [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q :** Puis‑je créer d’autres types de graphiques en plus des lignes et colonnes ?  
**R :** Oui, Aspose.Cells prend en charge les graphiques à barres, secteurs, nuages de points, aires, et bien d’autres types. Consultez la documentation API pour la liste complète.

**Q :** Une licence est‑elle requise pour une utilisation en production ?  
**R :** Une licence Aspose.Cells valide est requise pour les déploiements en production. Un essai gratuit est disponible pour l’évaluation.

**Q :** Comment changer les couleurs de chaque série ?  
**R :** Utilisez `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (ou similaire) après avoir ajouté les séries.

**Q :** Où puis‑je trouver plus d’exemples de code ?  
**R :** Une documentation complète et des exemples supplémentaires sont disponibles sur le site de référence Aspose : [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

---

**Dernière mise à jour :** 2026-09-02  
**Testé avec :** Aspose.Cells for Java dernière version  
**Auteur :** Aspose

## Tutoriels associés

- [Comment ajouter des libellés aux graphiques Excel avec Aspose.Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Comment créer un graphique Excel avec ligne de tendance et l’exporter en image avec Aspose.Cells for Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Exporter des graphiques Excel en PDF avec Aspose.Cells for Java : guide des tailles de page personnalisées](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}