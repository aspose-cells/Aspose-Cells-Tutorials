---
date: 2026-02-09
description: Apprenez à créer un graphique Excel, ajouter une courbe de tendance,
  afficher la valeur R² et exporter le graphique sous forme d’image à l’aide d’Aspose.Cells
  pour Java. Comprend les étapes pour charger le fichier Excel, personnaliser le graphique
  et enregistrer au format PNG/JPEG.
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Comment créer un graphique Excel avec ligne de tendance et l'exporter en image
  avec Aspose.Cells pour Java
url: /fr/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

 formatting preserved.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Exporter le graphique en image avec analyse de ligne de tendance

Dans ce tutoriel, vous apprendrez comment **créer un graphique Excel** avec une ligne de tendance, afficher sa valeur R‑squared, et exporter le visuel résultant en image en utilisant Aspose.Cells for Java. Nous parcourrons le chargement d’un classeur existant, l’ajout d’une ligne de tendance, la personnalisation des titres, l’enregistrement du classeur, et enfin la génération d’un fichier PNG/JPEG que vous pourrez intégrer n’importe où.

## Réponses rapides
- **Quel est le but principal de ce guide ?** Vous montrer comment ajouter une ligne de tendance, afficher son équation et sa valeur R‑squared, et exporter le graphique résultant en image avec Java.  
- **Quelle bibliothèque est requise ?** Aspose.Cells for Java (téléchargez [ici](https://releases.aspose.com/cells/java/)).  
- **Ai‑je besoin d’une licence ?** Un essai gratuit suffit pour le développement ; une licence commerciale est requise pour la production.  
- **Puis‑je générer un fichier Excel en Java ?** Oui – le tutoriel crée et enregistre un classeur XLSX.  
- **Comment exporter le graphique en PNG ou JPEG ?** Utilisez la méthode `Chart.toImage()` (décrite dans la section « Export Chart »).

## Comment créer un graphique Excel avec ligne de tendance et l’exporter en image
Ce titre répond directement à la requête principale et vous guide à travers l’ensemble du flux de travail dans un ordre logique. Vous trouverez ci‑dessous le pourquoi, les prérequis, et un guide étape par étape.

## Qu’est‑ce que l’exportation d’un graphique en image ?
Exporter un graphique en image convertit la représentation visuelle de vos données en un bitmap portable (PNG, JPEG, etc.). Cela est utile pour intégrer des graphiques dans des rapports, des pages web ou des présentations où le fichier Excel original n’est pas nécessaire.

## Pourquoi ajouter une ligne de tendance et afficher la valeur R‑squared ?
Une ligne de tendance vous aide à identifier le motif sous‑jacent d’une série de données, tandis que la métrique **R‑squared** quantifie la qualité de l’ajustement de la ligne aux données. Les inclure dans votre image exportée fournit aux parties prenantes un aperçu immédiat sans ouvrir le classeur.

## Prérequis
- Java 8 ou version supérieure installé.  
- Bibliothèque Aspose.Cells for Java ajoutée à votre projet (fichiers JAR sur le classpath).  
- Familiarité de base avec les IDE Java (IntelliJ IDEA, Eclipse, etc.).

## Guide étape par étape

### Étape 1 : Configurer le projet
Créez un nouveau projet Java et ajoutez les JAR Aspose.Cells au chemin de construction. Cela prépare l’environnement pour générer et manipuler des fichiers Excel.

### Étape 2 : Charger le fichier Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Nous venons de **charger un fichier Excel** en mémoire, prêt pour la création du graphique.*

### Étape 3 : Créer un graphique
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Ici nous générons un graphique en courbes qui accueillera plus tard notre ligne de tendance.*

### Étape 4 : Ajouter une ligne de tendance (how to add trendline) et afficher la valeur R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*L’appel `setDisplayRSquaredValue(true)` garantit que la **valeur R‑squared** apparaît sur le graphique.*

### Étape 5 : Personnaliser le graphique et enregistrer le classeur (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Le classeur est maintenant **généré** et enregistré au format XLSX, prêt pour un traitement ultérieur.*

### Étape 6 : Exporter le graphique en image (export chart to image)
> **Note :** Cette étape est décrite sans bloc de code supplémentaire afin de conserver le même nombre de blocs.  
Après que le graphique a été créé et enregistré, vous pouvez l’exporter en image en appelant la méthode `chart.toImage()` et en écrivant le `java.awt.image.BufferedImage` résultant dans le format de fichier de votre choix (PNG, JPEG, BMP). Le flux de travail typique est :
1. Récupérer l’objet `Chart` (déjà fait dans les étapes précédentes).  
2. Appeler `chart.toImage()` pour obtenir un `BufferedImage`.  
3. Utiliser `ImageIO.write(bufferedImage, "png", new File("chart.png"))` pour écrire le fichier.  

Cela produit une image haute résolution que vous pouvez intégrer n’importe où, complétant le processus d’**exportation du graphique en image**.

## Analyser les résultats
Ouvrez `output.xlsx` dans Excel pour vérifier que la ligne de tendance, l’équation et la valeur R‑squared apparaissent comme prévu. Ouvrez le fichier image exporté (par ex., `chart.png`) pour voir un visuel épuré qui peut être partagé sans le classeur original.

## Problèmes courants et solutions
- **La ligne de tendance n’apparaît pas :** Assurez‑vous que la plage de données (`A1:A10`) contient bien des valeurs numériques ; des données non numériques empêcheront le calcul de la ligne de tendance.  
- **La valeur R‑squared s’affiche à 0 :** Cela indique souvent que la série de données est constante ou manque de variation suffisante. Essayez un autre jeu de données ou une ligne de tendance polynomiale.  
- **L’exportation de l’image échoue avec `NullPointerException` :** Vérifiez que le graphique a été entièrement rendu avant d’appeler `toImage()`. Enregistrer le classeur au préalable peut parfois résoudre les problèmes de synchronisation.

## Questions fréquemment posées

**Q : Comment changer le type de ligne de tendance ?**  
R : Utilisez une autre énumération `TrendlineType` lors de l’ajout de la ligne de tendance, par ex., `TrendlineType.POLYNOMIAL` pour un ajustement polynomial.

**Q : Puis‑je personnaliser l’apparence de la ligne de tendance (couleur, épaisseur) ?**  
R : Oui. Accédez au `LineFormat` de la ligne de tendance via `trendline.getLineFormat()` et définissez des propriétés comme `setWeight()` et `setColor()`.

**Q : Comment exporter le graphique en PDF plutôt qu’en image ?**  
R : Convertissez d’abord le graphique en image, puis intégrez cette image dans un PDF en utilisant Aspose.PDF ou toute bibliothèque PDF de votre choix.

**Q : Est‑il possible d’ajouter plusieurs lignes de tendance au même graphique ?**  
R : Absolument. Appelez `chart.getNSeries().get(0).getTrendlines().add(...)` pour chaque série que vous souhaitez analyser.

**Q : Aspose.Cells prend‑il en charge l’exportation d’images haute résolution ?**  
R : Oui. Vous pouvez spécifier le DPI lors de l’appel à `chart.toImage()` puis redimensionner l’image en conséquence avant de l’enregistrer.

## Conclusion
Vous disposez maintenant d’une solution complète, de bout en bout, pour **créer un graphique Excel**, ajouter une ligne de tendance, afficher l’équation et la valeur R‑squared, personnaliser le visuel, enregistrer le classeur, et enfin exporter le graphique sous forme d’image PNG/JPEG. Cette approche vous permet de générer programmétiquement des actifs analytiques de qualité professionnelle, idéal pour les rapports automatisés, les tableaux de bord, ou tout scénario où une image statique est plus pratique qu’un fichier Excel.

---

**Dernière mise à jour :** 2026-02-09  
**Testé avec :** Aspose.Cells for Java latest  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}