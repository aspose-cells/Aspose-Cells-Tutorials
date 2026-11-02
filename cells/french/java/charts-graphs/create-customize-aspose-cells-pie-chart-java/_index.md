---
date: '2026-09-27'
description: Apprenez à créer un pie chart java en utilisant Aspose.Cells. Guide étape
  par étape pour personnaliser le pie chart Excel, configurer la dépendance Maven
  et générer des graphiques professionnels.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Créez un pie chart java avec Aspose.Cells pour Java. Apprenez à personnaliser
  le pie chart Excel, ajouter la dépendance Maven et générer des graphiques professionnels
  en quelques minutes.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Créer un pie chart java avec Aspose.Cells – Guide complet Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Comment créer un pie chart java avec Aspose.Cells
url: /fr/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un diagramme circulaire java avec Aspose.Cells

## Introduction
Créer un **diagramme circulaire** de manière programmatique ressemble souvent à un puzzle, surtout lorsque vous avez besoin d'un contrôle fin sur les couleurs, les légendes et les titres. Dans ce guide, vous apprendrez comment **créer un diagramme circulaire java** avec Aspose.Cells, puis personnaliser le diagramme circulaire Excel pour qu'il corresponde à votre marque ou à votre style de reporting. Nous parcourrons la configuration de l'environnement, le remplissage des données, la génération du graphique et les ajustements visuels — le tout sans quitter votre IDE Java.

**Ce que vous allez apprendre**
- Ajouter la **dépendance Maven Aspose.Cells** à votre projet.
- Construire un classeur, remplir les cellules avec des données et générer un diagramme circulaire.
- Appliquer des couleurs, titres et légendes personnalisés au graphique.
- Exporter le classeur vers un fichier XLSX prêt à être partagé.

Avant de commencer, vous devez être à l'aise avec la syntaxe Java de base et disposer de Maven ou Gradle installé.

## Réponses rapides
- **Quelle bibliothèque crée des diagrammes circulaires en Java ?** Aspose.Cells for Java.
- **Ai-je besoin d'une licence ?** Un essai gratuit fonctionne pour le développement ; une licence payante est requise pour la production.
- **Quelles coordonnées Maven sont requises ?** `com.aspose:aspose-cells:24.10`.
- **Puis-je changer les couleurs des parts ?** Oui, via la méthode `setAreaColor` sur chaque série.
- **Le graphique est‑il exportable en XLSX ?** Absolument — il suffit d'appeler `workbook.save("output.xlsx")`.

## Qu'est‑ce qu'un diagramme circulaire dans Excel ?
Un diagramme circulaire visualise une série de données unique sous forme de parts proportionnelles d'un cercle, facilitant la comparaison des parties d'un tout. L'angle de chaque part correspond à sa valeur relative au total, offrant ainsi une vision rapide de la répartition entre les catégories telles que la part de marché, l'allocation budgétaire ou les pourcentages démographiques.

## Pourquoi utiliser Aspose.Cells pour créer un diagramme circulaire java ?
Aspose.Cells prend en charge plus de 50 types de graphiques et peut gérer des feuilles de calcul contenant jusqu'à un million de lignes sans charger l'intégralité du fichier en mémoire. Cette performance vous permet de générer de gros rapports sur du matériel modeste, tout en offrant un contrôle fin sur l'apparence du graphique, la liaison des données et les formats d'exportation, ce qui en fait un choix supérieur à de nombreuses bibliothèques open‑source.

## Prérequis
- **Java Development Kit (JDK)** 8 ou plus récent.
- **IDE** tel qu'IntelliJ IDEA ou Eclipse.
- **Maven** ou **Gradle** pour la gestion des dépendances.
- Une **licence Aspose.Cells d'essai ou achetée**.

### Bibliothèques et dépendances requises
Ajoutez l'artifact Maven Aspose.Cells à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Ou l'équivalent Gradle :

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Étapes d'obtention de licence
Aspose.Cells for Java est commercial, mais vous pouvez commencer avec un essai gratuit. Visitez la [page d'achat](https://purchase.aspose.com/buy) pour obtenir une clé de licence temporaire.

## Configuration d'Aspose.Cells pour Java
Tout d'abord, assurez-vous que la bibliothèque est sur votre classpath. Après avoir ajouté la dépendance, vous pouvez initialiser l'API comme indiqué ci‑dessous.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Guide d'implémentation

### Créer et configurer un classeur
La classe `Workbook` représente un fichier Excel complet en mémoire.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Étape 1 : instancier un classeur
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Cela crée un nouveau classeur vide que vous pouvez immédiatement commencer à remplir.

### Accéder ou modifier les cellules d'une feuille de calcul
Un `Worksheet` représente une seule feuille au sein du classeur, contenant des cellules, des lignes et des colonnes.  
Vous écrirez les données qui alimentent le diagramme circulaire dans une feuille.

#### Étape 2 : obtenir la première feuille de calcul et ses cellules
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Remplissez les cellules avec les noms de catégories et les valeurs que le graphique utilisera.

### Créer un diagramme circulaire
Les objets `Chart` visualisent les données d'une feuille et prennent en charge divers types tels que circulaire, colonne et ligne.

#### Étape 3 : ajouter un diagramme circulaire à la feuille de calcul
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Configurer les séries et les données du diagramme circulaire
`Series` définit la plage de données et le formatage d'un graphique, reliant les cellules de la feuille aux éléments visuels.

#### Étape 4 : définir les séries pour le graphique
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Configurer l'apparence de la légende et du titre du graphique
Une `Legend` de graphique affiche les noms des séries et les couleurs, aidant les lecteurs à identifier chaque part.

#### Étape 5 : personnaliser la légende et le titre du graphique
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Personnaliser les couleurs des séries du graphique
`setAreaColor` définit la couleur de remplissage d'une part de série de graphique à l'aide d'une valeur RVB.

#### Étape 6 : changer les couleurs des segments du diagramme circulaire
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Ajuster automatiquement les colonnes et enregistrer le classeur
`autoFitColumns` ajuste automatiquement la largeur des colonnes pour correspondre au contenu des cellules.

#### Étape 7 : ajuster la largeur des colonnes et enregistrer le fichier
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Cas d'utilisation courants
- **Analyse démographique :** Montrer la répartition de la population par région.
- **Rapport de part de marché :** Visualiser la part de chaque concurrent en un coup d'œil.
- **Allocation budgétaire :** Mettre en évidence la répartition des fonds entre les départements.

## Considérations de performance
- Libérez les objets (`workbook.dispose()`) lorsqu'ils ne sont plus nécessaires pour libérer la mémoire native.
- Pour des ensembles de données massifs, utilisez `WorkbookDesigner` pour diffuser les données au lieu de tout charger d'un coup.
- Profilez avec Java Flight Recorder pour repérer les goulets d'étranglement dans la génération du graphique.

## Questions fréquemment posées

**Q : Puis‑je générer plusieurs diagrammes circulaires dans le même classeur ?**  
R : Oui, répétez les étapes de création du graphique pour chaque plage de données ; chaque graphique est indépendant.

**Q : Aspose.Cells prend‑il en charge les diagrammes circulaires 3‑D ?**  
R : Oui ; définissez le type de graphique sur `ChartType.PIE_3D` lors de l'ajout du graphique.

**Q : Comment appliquer un thème personnalisé à tous les graphiques ?**  
R : Utilisez la méthode `Workbook.setDefaultTheme` avant de créer des graphiques.

**Q : Quels formats de fichier puis‑je exporter depuis le classeur ?**  
R : Plus de 30 formats, dont XLSX, CSV, PDF et HTML.

**Q : Une licence est‑elle requise pour le déploiement commercial ?**  
R : Oui, une licence valide supprime les filigranes d'évaluation et débloque toutes les fonctionnalités.

## Conclusion
Vous disposez maintenant d’une recette complète, de bout en bout, pour **créer un diagramme circulaire java** avec Aspose.Cells. En suivant les étapes ci‑dessus, vous pouvez générer des diagrammes circulaires Excel soignés, ajuster les couleurs et les titres, et les intégrer à n’importe quel pipeline de reporting. Explorez d’autres types de graphiques — colonnes, lignes, radars—pour élargir votre boîte à outils de visualisation de données.

---

**Dernière mise à jour :** 2026-09-27  
**Testé avec :** Aspose.Cells 24.10 for Java  
**Auteur :** Aspose

## Tutoriels associés

- [Personnaliser les étiquettes de données des graphiques Excel avec Aspose.Cells pour Java&#58; guide étape par étape](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Créer des graphiques Excel dynamiques avec Aspose.Cells Java&#58; guide complet pour les développeurs](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Créer et personnaliser des classeurs Excel avec Aspose.Cells Java&#58; guide étape par étape](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}