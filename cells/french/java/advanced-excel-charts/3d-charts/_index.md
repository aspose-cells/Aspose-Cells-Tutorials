---
date: 2026-08-21
description: Apprenez à exporter un graphique en image et à créer des diagrammes circulaires
  3D en Java avec Aspose.Cells. Générez des graphiques à barres 3D, ajoutez des graphiques
  3D à Excel et enregistrez les classeurs au format XLSX.
keywords:
- export chart as image
- 3d pie chart java
- 3d bar chart java
- save workbook as xlsx
- add 3d chart excel
lastmod: 2026-08-21
linktitle: Créer un diagramme circulaire 3D en Java
og_description: Exportez un graphique en image et créez des diagrammes circulaires
  3D en Java avec Aspose.Cells. Guide étape par étape pour générer des graphiques
  à barres et des diagrammes circulaires 3D, les personnaliser et enregistrer les
  classeurs au format XLSX.
og_image_alt: Developer guide showing how to export a 3D chart as an image with Aspose.Cells
  for Java
og_title: Exporter un graphique en image et créer un diagramme circulaire 3D en Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to export chart as image and create 3D pie charts in Java
    with Aspose.Cells. Generate 3D bar charts, add 3D charts to Excel, and save workbooks
    as XLSX.
  headline: How to export chart as image and create 3D pie chart in Java
  type: TechArticle
- questions:
  - answer: Use `chart.getNSeries().add()` for each series range and ensure the chart
      type remains 3‑D (e.g., `ChartType.BAR_3_D` or `ChartType.PIE_3_D`).
    question: How can I add multiple data series to a 3D chart?
  - answer: Yes, you can save the chart as PNG, JPEG, or PDF by calling the appropriate
      `chart.toImage()` overload or `workbook.save()` with an image or PDF format,
      satisfying the **convert chart png** requirement.
    question: Can I export 3D charts created with Aspose.Cells for Java to other formats?
  - answer: Aspose.Cells focuses on static Excel charts. For interactive web‑based
      3‑D visualizations, consider coupling Excel data with JavaScript libraries such
      as Three.js.
    question: Is it possible to create interactive 3D charts with Aspose.Cells for
      Java?
  - answer: Absolutely. Load new data into the worksheet programmatically and refresh
      the chart range; the next time the workbook is opened, the chart reflects the
      updated values.
    question: Can I automate the process of updating data in my 3D charts?
  - answer: 'You can find comprehensive documentation and resources for Aspose.Cells
      for Java at the website: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more resources and documentation for Aspose.Cells for
      Java?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart as image
- 3d pie chart
- Aspose.Cells Java
- Excel chart automation
title: Comment exporter un graphique en image et créer un diagramme circulaire 3D
  en Java
url: /fr/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Créer un graphique circulaire 3D Java

## Introduction aux graphiques 3D

Aspose.Cells for Java est une API Java puissante pour travailler avec des fichiers Excel, et elle simplifie la **create 3d pie chart** projets ainsi que les visualisations classiques de barres 3‑D. Dans ce tutoriel, vous verrez exactement comment **export chart as image**, générer un diagramme à barres 3‑D, adapter la même approche pour un diagramme circulaire 3‑D, personnaliser les apparences, et enfin **add 3d chart excel** fichiers à vos rapports. Que vous construisiez un tableau de bord financier, une feuille de performance des ventes, ou que vous visualisiez des données scientifiques, les étapes ci‑dessous vous fourniront une base solide.

## Réponses rapides

- **Quelle bibliothèque dois‑je utiliser ?** Aspose.Cells for Java (latest version)  
- **Puis‑je générer un diagramme à barres 3D ?** Oui – use `ChartType.BAR_3_D`  
- **Ai‑je besoin d’une licence ?** Une licence valide supprime les limites d'évaluation  
- **Quelles versions d’Excel sont prises en charge ?** Toutes les versions majeures de 2003 à 2023  
- **Est‑il possible d’exporter le graphique en image ?** Oui – call `chart.toImage()` after the chart is created  

## Qu’est‑ce que les graphiques 3D ?

Les graphiques 3D ajoutent de la profondeur aux visualisations 2D traditionnelles, aidant les spectateurs à saisir les relations multidimensionnelles de manière plus intuitive. Ils sont particulièrement utiles lorsqu’il faut comparer plusieurs catégories côte à côte tout en conservant une hiérarchie visuelle claire. En ajoutant une troisième dimension, ces graphiques peuvent mettre en évidence des différences d’amplitude qui seraient moins évidentes dans des représentations plates, rendant les données complexes plus faciles à interpréter pour les parties prenantes commerciales.

## Pourquoi utiliser Aspose.Cells for Java pour générer un diagramme à barres 3D ?

Aspose.Cells for Java offre plus de 150 types de graphiques intégrés et prend en charge plus de 100 fonctions Excel, vous fournissant un moteur complet qui fonctionne sur toutes les versions d’Excel de 2003 à 2023 sans nécessiter Microsoft Office. Cela signifie que vous pouvez **generate 3d bar chart** des objets de façon programmatique avec des résultats prévisibles et une surcharge minimale.

## Configuration d’Aspose.Cells for Java

### Téléchargement et installation

Vous pouvez télécharger la bibliothèque Aspose.Cells for Java depuis le site officiel. Suivez les instructions Maven/Gradle fournies ou ajoutez le JAR directement au classpath de votre projet.

### Initialisation de la licence

La classe `License` est utilisée pour appliquer votre licence Aspose.Cells et débloquer toutes les fonctionnalités.  
```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Création d’un graphique 3D de base

### Importation des bibliothèques nécessaires

Tout d’abord, importez les classes requises :  
```java
import com.aspose.cells.*;
```

### Initialisation d’un classeur

Créez un nouveau classeur qui hébergera le graphique :  
```java
Workbook workbook = new Workbook();
```

### Ajout de données au graphique

Remplissez la feuille de calcul avec des données d’exemple que le graphique utilisera :  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

## Comment générer un diagramme à barres 3D en Java

Pour créer un diagramme à barres 3D, vous ajoutez un objet graphique à la feuille, définissez son type sur `ChartType.BAR_3_D`, puis liez les séries de données aux cellules contenant vos valeurs. Après avoir configuré l’apparence du graphique, vous pouvez le rendre ou l’exporter selon les besoins.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

## Enregistrement du graphique dans un fichier

Enfin, écrivez le classeur (qui contient maintenant le graphique 3‑D) sur le disque. Cela **save workbook xlsx** également au format Excel standard :  
```java
workbook.save("3D_Chart.xlsx");
```

## Comment créer un diagramme circulaire 3D avec Aspose.Cells for Java

Si vous avez besoin d’une visualisation de type circulaire, le flux de travail est presque identique — seul l’énuméré `ChartType` change. Remplacez `ChartType.BAR_3_D` par `ChartType.PIE_3_D` lors de l’ajout du graphique, et pointez les séries vers la même plage de données. Après la création du graphique, vous pouvez définir un titre descriptif, ajuster les couleurs des parts et exporter le résultat en image. Cette approche vous permet de réutiliser le même code de préparation des données tout en offrant une perspective visuelle différente.

## Comment exporter le graphique en image en Java

La méthode `toImage` de l’objet `Chart` enregistre le graphique sous forme de fichier image. Vous pouvez exporter n’importe quel graphique 3D vers une image raster avec un appel unique : `chart.toImage("myChart.png", ImageFormat.getPng())`. Cette méthode rend le graphique exactement tel qu’il apparaît dans Excel, en préservant la profondeur 3‑D, les couleurs et les légendes, et écrit le résultat dans le chemin de fichier spécifié. Utilisez PNG pour une qualité sans perte ou JPEG pour des tailles de fichier plus petites lors de l’intégration de l’image dans des rapports web.

## Différents types de graphiques 3D

Aspose.Cells for Java prend en charge plusieurs variantes de graphiques 3D que vous pouvez **add 3d chart excel** fichiers avec :

- **Diagrammes à barres** – idéal pour comparer des catégories.  
- **Diagrammes circulaires** – montrent les contributions proportionnelles (y compris le circulaire 3D).  
- **Diagrammes en ligne** – illustrent les tendances au fil du temps.  
- **Diagrammes de zone** – mettent en évidence l’ampleur du changement.

Vous pouvez changer l’énumération `ChartType` pour l’une de celles‑ci tout en conservant le même modèle de création.

## Personnalisation avancée du graphique

### Ajout de titres et d’étiquettes

Donnez du contexte à votre graphique en définissant un titre descriptif et des libellés d’axes.

### Ajustement des couleurs et des styles

Utilisez la méthode `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` pour correspondre à l’identité visuelle de l’entreprise.

### Travail avec les axes du graphique

Affinez les échelles, intervalles et marques d’échelle des axes pour améliorer la lisibilité.

### Ajout de légendes

Activez les légendes avec `chart.getLegend().setVisible(true)` afin que les spectateurs puissent identifier chaque série de données.

### Exportation des graphiques en images

Lorsque vous avez besoin d’une image statique pour un rapport web, appelez `chart.toImage("chart.png", ImageFormat.getPng())`. Cela répond au cas d’utilisation **convert chart png** sans quitter le classeur.

## Intégration des données

Aspose.Cells for Java peut extraire des données depuis des bases de données, des fichiers CSV ou des API en direct. Remplissez simplement les cellules de la feuille avec les données récupérées avant de lier la plage au graphique. Cela maintient votre flux de travail **add 3d chart excel** dynamique et à jour.

## Conclusion

Dans ce guide, nous avons parcouru la façon de **create 3d pie chart** et **create 3d bar chart** projets de bout en bout — configuration de la bibliothèque, ajout de données, génération d’un diagramme à barres 3‑D, adaptation des mêmes étapes pour un diagramme circulaire 3‑D, et application de styles avancés. Avec Aspose.Cells for Java, vous disposez d’une méthode fiable et indépendante de version pour intégrer des visualisations 3‑D riches directement dans les classeurs Excel et même **export chart as image** pour les utiliser dans des tableaux de bord ou des rapports.

## Questions fréquentes

**Q : Comment puis‑je ajouter plusieurs séries de données à un graphique 3D ?**  
A: Utilisez `chart.getNSeries().add()` pour chaque plage de séries et assurez‑vous que le type de graphique reste 3‑D (par ex., `ChartType.BAR_3_D` ou `ChartType.PIE_3_D`).

**Q : Puis‑je exporter les graphiques 3D créés avec Aspose.Cells for Java vers d’autres formats ?**  
A: Oui, vous pouvez enregistrer le graphique au format PNG, JPEG ou PDF en appelant la surcharge appropriée de `chart.toImage()` ou `workbook.save()` avec un format image ou PDF, répondant à l’exigence **convert chart png**.

**Q : Est‑il possible de créer des graphiques 3D interactifs avec Aspose.Cells for Java ?**  
A: Aspose.Cells se concentre sur les graphiques Excel statiques. Pour des visualisations 3D interactives basées sur le web, envisagez de coupler les données Excel avec des bibliothèques JavaScript telles que Three.js.

**Q : Puis‑je automatiser le processus de mise à jour des données dans mes graphiques 3D ?**  
A: Absolument. Chargez de nouvelles données dans la feuille de calcul de façon programmatique et rafraîchissez la plage du graphique ; la prochaine fois que le classeur sera ouvert, le graphique reflétera les valeurs mises à jour.

**Q : Où puis‑je trouver davantage de ressources et de documentation pour Aspose.Cells for Java ?**  
A: Vous pouvez trouver une documentation complète et des ressources pour Aspose.Cells for Java sur le site : [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**Dernière mise à jour :** 2026-08-21  
**Testé avec :** Aspose.Cells for Java 24.12 (latest)  
**Auteur :** Aspose

## Tutoriels associés

- [Créer des graphiques circulaires dans Excel avec Aspose.Cells for Java : guide complet](/cells/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/)
- [aspose cells java – Créer un graphique Excel avec des annotations](/cells/java/advanced-excel-charts/chart-annotations/)
- [Ajouter des étiquettes de données à un graphique Excel avec Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}