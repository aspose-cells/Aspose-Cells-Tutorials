---
date: 2026-02-16
description: Apprenez à définir la plage de données d’un graphique et à créer un graphique
  en cascade en Java avec Aspose.Cells. Guide étape par étape pour ajouter une série
  de données au graphique, le personnaliser et l’exporter au format XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Définir la plage de données du graphique – Diagramme en cascade Aspose.Cells
  pour Java
url: /fr/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Graphiques en cascade

## Introduction aux graphiques en cascade avec Aspose.Cells pour Java

Dans ce tutoriel, vous apprendrez à **set chart data range** et à créer un **waterfall chart** avec Aspose.Cells pour Java. Les graphiques en cascade sont un outil essentiel de visualisation de données car ils permettent de voir l'effet cumulé d'une série de valeurs positives et négatives. Que vous prépariez un état financier, un rapport de performance des ventes ou toute autre analyse basée sur les données, un graphique en cascade peut transformer des chiffres bruts en informations claires et exploitables.

## Réponses rapides
- **What is a waterfall chart?** Un visuel qui montre comment une valeur initiale est augmentée et diminuée par une série de valeurs intermédiaires, se terminant par un total final.  
- **Which library is used?** Aspose.Cells for Java.  
- **Do I need a license?** Un essai gratuit suffit pour le développement ; une licence commerciale est requise pour la production.  
- **Can I save the file as XLSX?** Oui – utilisez `workbook.save("FileName.xlsx")`.  
- **Is it suitable for Java data visualization?** Absolument ; Aspose.Cells offre des fonctionnalités de création de graphiques riches sans besoin d'Office installé.

## Qu'est-ce qu'un graphique en cascade ?

Un graphique en cascade affiche les contributions positives et négatives séquentielles à une valeur de départ, vous aidant à comprendre comment chaque composant influence le résultat global.

## Pourquoi utiliser Aspose.Cells pour Java pour ajouter un graphique en cascade ?

- **No Microsoft Excel required** – générez des graphiques sur n'importe quel serveur ou pipeline CI.  
- **Full control over formatting** – les couleurs, les étiquettes de données et les axes peuvent être personnalisés par programme.  
- **Supports multiple output formats** – XLSX, PDF, HTML, et plus.  
- **High performance** – idéal pour les classeurs volumineux et les rapports automatisés.

## Prérequis

Avant de plonger dans le code, assurez-vous d'avoir les prérequis suivants en place :

- Aspose.Cells for Java : Vous devez avoir Aspose.Cells for Java installé. Vous pouvez le télécharger depuis [here](https://releases.aspose.com/cells/java/).
- Environnement de développement Java : Assurez-vous d'avoir Java installé sur votre système.

Maintenant, commençons à créer le graphique en cascade étape par étape.

## Comment définir la plage de données du graphique pour un graphique en cascade en Java

### Étape 1 : Importer Aspose.Cells

```java
import com.aspose.cells.*;
```

Tout d'abord, vous devez importer la bibliothèque Aspose.Cells dans votre projet Java. Cette bibliothèque offre une fonctionnalité étendue pour travailler avec les fichiers Excel, y compris la création de graphiques.

### Étape 2 : Initialiser le classeur et la feuille de calcul

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Créez un nouveau classeur et ajoutez-y une feuille de calcul. Nous utiliserons cette feuille pour saisir nos données et **add chart to worksheet**.

### Étape 3 : Saisir les données

Maintenant, remplissons la feuille de calcul avec les données que nous souhaitons représenter dans le graphique en cascade.

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

Dans cet exemple, nous avons des catégories dans la colonne A et les valeurs correspondantes dans la colonne B. Vous pouvez remplacer ces données par votre propre jeu de données.

### Étape 4 : Créer le graphique en cascade

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Nous avons ajouté un graphique en cascade à notre feuille, spécifié la série de données et les données de catégorie. C'est l'étape principale qui **adds waterfall chart** à votre feuille. Notez comment la méthode `add` utilise la plage `"B2:B6"` – c'est ici que nous **set chart data range** pour la série. Vous pouvez personnaliser davantage l'apparence du graphique (couleurs, étiquettes de données, etc.) en utilisant les propriétés de l'objet `Chart`.

### Étape 5 : Enregistrer le classeur

```java
workbook.save("WaterfallChart.xlsx");
```

Enregistrez le classeur dans un fichier. L'exemple utilise le format XLSX, mais Aspose.Cells vous permet également de **export excel pdf java**‑compatible files tels que PDF, CSV, et de nombreux autres formats. Cela satisfait l'exigence **save workbook xlsx**.

## Problèmes courants et solutions

- **Chart appears blank** – Vérifiez que les références de plage de données (`B2:B6` et `A2:A6`) correspondent aux cellules réelles contenant vos valeurs et catégories.  
- **Negative values not displayed correctly** – Assurez-vous que le type de série est défini sur `ChartType.WATERFALL` ; les autres types de graphiques traitent les valeurs négatives différemment.  
- **File not opening in Excel** – Assurez-vous d'utiliser une version récente d'Aspose.Cells (la dernière version) et que l'extension du fichier correspond au format (`.xlsx` pour Excel).

## Questions fréquemment posées

### Comment puis‑je personnaliser l'apparence de mon graphique en cascade ?

Vous pouvez personnaliser l'apparence de votre graphique en cascade en modifiant des propriétés telles que les couleurs, les étiquettes de données et les étiquettes d'axes. Consultez la documentation d'Aspose.Cells pour des instructions détaillées.

### Puis‑je créer plusieurs graphiques en cascade dans la même feuille ?

Oui, vous pouvez créer plusieurs graphiques en cascade dans la même feuille en suivant les mêmes étapes avec des plages de données différentes.

### Aspose.Cells est‑il compatible avec différents environnements de développement Java ?

Oui, Aspose.Cells pour Java est compatible avec divers environnements de développement Java, y compris Eclipse, IntelliJ IDEA et NetBeans.

### Puis‑je ajouter des séries de données supplémentaires à mon graphique en cascade ?

Bien sûr, vous pouvez ajouter d'autres séries de données à votre graphique en cascade pour représenter efficacement des scénarios de données complexes. Voici un exemple de la façon dont vous pouvez **add data series chart** programmatically.

### Où puis‑je trouver plus de ressources et d'exemples pour Aspose.Cells pour Java ?

Vous pouvez explorer la documentation d'Aspose.Cells pour Java sur [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) pour des informations détaillées et des exemples de code.

## FAQ

**Q : Comment définir la plage de données du graphique pour un graphique en cascade financier ?**  
R : Utilisez la méthode `add` sur la série du graphique, en passant la plage de cellules contenant vos valeurs, par ex., `"B2:B6"`.

**Q : Puis‑je exporter le classeur en PDF au lieu de XLSX ?**  
R : Oui, appelez `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` pour une sortie **export excel pdf java**‑compatible.

**Q : Que faire si je dois créer un graphique en cascade financier avec plus de catégories ?**  
R : Étendez la plage de données dans la colonne des valeurs et la colonne des catégories, puis mettez à jour les appels `add` et `setCategoryData` en conséquence.

**Q : Existe‑t‑il un moyen de formater automatiquement les barres positives et négatives ?**  
R : Vous pouvez parcourir la collection `Series` et définir la couleur `FillFormat` en fonction du signe de chaque valeur.

**Q : Aspose.Cells prend‑il en charge les mises à jour dynamiques des données pour les graphiques ?**  
R : Oui, vous pouvez modifier les valeurs des cellules après la création du graphique ; le graphique reflétera les changements lors de l'enregistrement du classeur.

---

**Dernière mise à jour :** 2026-02-16  
**Testé avec :** Aspose.Cells pour Java (dernière version)  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}