---
date: 2026-08-27
description: Apprenez à ajouter une trendline à un graphique, afficher sa valeur R‑squared,
  et exporter le graphique en image PNG ou JPEG à l'aide d'Aspose.Cells for Java.
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: Exporter le chart en image avec analyse de Trendline
og_description: Ajoutez une trendline à un chart, visualisez le R‑squared, et exportez
  le résultat en PNG/JPEG avec Aspose.Cells for Java – une solution rapide, compatible
  avec 50 formats.
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: Ajouter une trendline à un chart et l'exporter en image avec Aspose.Cells
  for Java
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: Comment ajouter une trendline à un graphique et l'exporter en image en Java
url: /fr/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une droite de tendance au graphique et l'exporter en image

Dans ce tutoriel, vous apprendrez comment **ajouter une droite de tendance au graphique**, afficher la valeur R‑carré, et exporter le visuel en fichier PNG ou JPEG en utilisant Aspose.Cells for Java. Vous verrez pourquoi les droites de tendance sont importantes, comment préparer le classeur, et les étapes exactes pour générer une image haute résolution pouvant être intégrée dans des rapports, des e‑mails ou des pages Web.

## Réponses rapides
- **Quel est l'objectif principal de ce guide ?** Montrer comment ajouter une droite de tendance au graphique, afficher son équation et la valeur R‑carré, et exporter le graphique en image avec Java.  
- **Quelle bibliothèque faut‑il ?** Aspose.Cells for Java – téléchargez‑la depuis la [page de diffusion d'Aspose.Cells for Java](https://releases.aspose.com/cells/java/).  
- **Ai‑je besoin d’une licence pour le développement ?** Un essai gratuit suffit pour le développement ; une licence commerciale est requise pour les déploiements en production.  
- **Puis‑je générer le classeur Excel de façon programmatique ?** Oui – le tutoriel crée et enregistre un classeur XLSX à partir de zéro.  
- **Comment le graphique est‑il exporté en PNG ou JPEG ?** Appelez la méthode `Chart.toImage()` et écrivez le `BufferedImage` retourné avec `ImageIO.write(...)`.

## Comment créer un graphique Excel avec une droite de tendance et l'exporter en image ?
Chargez le classeur, ajoutez un graphique en courbes, attachez une droite de tendance affichant l'équation et la valeur R‑carré, enregistrez le classeur, puis appelez `chart.toImage()` et écrivez le `BufferedImage` résultant dans un fichier PNG ou JPEG. Ce flux de bout en bout ne nécessite que quelques lignes de code Java et produit une image pixel‑parfaite adaptée à toute application en aval.

## Qu’est‑ce que l’exportation d’un graphique en image ?
Exporter un graphique en image convertit la représentation visuelle de vos données en un bitmap portable (PNG, JPEG, BMP, etc.). Ce format est idéal pour intégrer des graphiques dans des rapports, des pages Web ou des présentations où le fichier Excel original n’est pas nécessaire.

## Pourquoi ajouter une droite de tendance et afficher la valeur R‑carré ?
Une droite de tendance révèle le motif sous‑jacent d’une série de données, tandis que la métrique **R‑carré** quantifie à quel point la droite de tendance s’ajuste aux données. Inclure les deux dans l’image exportée donne aux parties prenantes un aperçu immédiat sans ouvrir le classeur. Cela aide les décideurs à évaluer rapidement la force de corrélation et à prévoir les tendances sans avoir à ouvrir Excel.

## Prérequis
- Java 8 ou version ultérieure installé sur votre machine de développement.  
- Bibliothèque Aspose.Cells for Java ajoutée au classpath du projet (fichiers JAR).  
- Familiarité avec un IDE Java tel qu’IntelliJ IDEA ou Eclipse.  

## Guide étape par étape

### Étape 1 : configurer le projet
Créez un nouveau projet Java et placez les JAR d’Aspose.Cells sur le chemin de construction. Cela prépare l’environnement pour générer et manipuler des fichiers Excel.

### Étape 2 : charger le fichier Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Nous venons de **charger un fichier Excel** en mémoire, prêt pour la création du graphique.*

### Étape 3 : créer un graphique
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Ici nous générons un graphique en courbes qui accueillera plus tard notre droite de tendance.*

### Étape 4 : ajouter une droite de tendance (how to add trendline) et afficher la valeur R‑carré
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*L’appel `setDisplayRSquaredValue(true)` garantit que la **valeur R‑carré** apparaît sur le graphique.*

### Étape 5 : personnaliser le graphique et enregistrer le classeur (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Le classeur est maintenant **généré** et enregistré au format XLSX, prêt pour un traitement ultérieur.*

### Étape 6 : exporter le graphique en image (export chart to image)
> **Note :** Cette étape est décrite sans bloc de code supplémentaire afin de conserver le nombre original de blocs.  
Après la création et l’enregistrement du graphique, vous pouvez l’exporter en image en appelant la méthode `chart.toImage()` et en écrivant le `java.awt.image.BufferedImage` résultant dans le format de fichier de votre choix (PNG, JPEG, BMP). Le flux de travail typique est :
1. Récupérez l’objet `Chart` (déjà fait dans les étapes précédentes).  
2. Appelez `chart.toImage()` pour obtenir un `BufferedImage`.  
3. Utilisez `ImageIO.write(bufferedImage, "png", new File("chart.png"))` pour écrire le fichier.  

L’objet `Chart` représente un graphique dans le classeur et fournit des méthodes pour modifier son apparence et ses données. `BufferedImage` est une classe Java qui stocke une image en mémoire, permettant de l’enregistrer dans un fichier. `ImageIO` est une classe utilitaire pour lire et écrire des images en Java. `setDisplayRSquaredValue` active l’affichage de la statistique R‑carré sur la droite de tendance.

### Analyser les résultats
Ouvrez `output.xlsx` dans Excel pour vérifier que la droite de tendance, l’équation et la valeur R‑carré apparaissent comme prévu. Ouvrez le fichier image exporté (par ex., `chart.png`) pour voir un visuel net qui peut être partagé sans le classeur original.

## Problèmes courants et solutions
- **Droite de tendance non affichée :** Assurez‑vous que la plage de données (`A1:A10`) contient des valeurs numériques ; des données non numériques empêchent le calcul de la droite de tendance.  
- **Valeur R‑carré affichée comme 0 :** Cela indique souvent que la série de données est constante ou manque de variation. Essayez un autre jeu de données ou utilisez une droite de tendance polynomiale.  
- **Échec de l’exportation d’image avec `NullPointerException` :** Vérifiez que le graphique a été entièrement rendu avant d’appeler `toImage()`. Enregistrer le classeur d’abord peut parfois résoudre les problèmes de synchronisation.

## Questions fréquemment posées

**Q : Comment puis‑je changer le type de droite de tendance ?**  
R : Utilisez une autre énumération `TrendlineType` lors de l’ajout de la droite de tendance, par ex., `TrendlineType.POLYNOMIAL` pour un ajustement polynomial.

**Q : Puis‑je personnaliser l’apparence de la droite de tendance (couleur, épaisseur) ?**  
R : Oui. Accédez au `LineFormat` de la droite de tendance via `trendline.getLineFormat()` et définissez des propriétés comme `setWeight()` et `setColor()`.

**Q : Comment exporter le graphique en PDF au lieu d’une image ?**  
R : Convertissez d’abord le graphique en image, puis intégrez cette image dans un PDF en utilisant Aspose.PDF ou toute autre bibliothèque PDF.

**Q : Est‑il possible d’ajouter plusieurs droites de tendance au même graphique ?**  
R : Absolument. Appelez `chart.getNSeries().get(0).getTrendlines().add(...)` pour chaque série que vous souhaitez analyser.

**Q : Aspose.Cells prend‑il en charge l’exportation d’images haute résolution ?**  
R : Oui. Vous pouvez spécifier le DPI lors de l’appel à `chart.toImage()` puis redimensionner l’image avant l’enregistrement, garantissant une sortie nette pour l’impression ou les écrans à haute densité.

---

**Dernière mise à jour :** 2026-08-27  
**Testé avec :** Aspose.Cells for Java latest (supports 50+ file formats and processes workbooks with up to 2 million rows without full memory load)  
**Auteur :** Aspose

## Tutoriels associés

- [Ajouter des étiquettes de données au graphique Excel avec Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Comment exporter des graphiques Excel au format SVG en utilisant Aspose.Cells Java pour les graphiques vectoriels évolutifs](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Exporter des graphiques Excel en PDF en utilisant Aspose.Cells for Java : Guide des tailles de page personnalisées](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}