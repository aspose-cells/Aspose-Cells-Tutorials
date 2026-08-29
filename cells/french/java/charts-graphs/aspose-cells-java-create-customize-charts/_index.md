---
date: '2026-04-08'
description: Apprenez à générer un diagramme à colonnes en Java avec Aspose.Cells,
  en couvrant la création de graphique Java, l’ajout d’une feuille de graphique et
  l’exportation du classeur Excel.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Générer un graphique à colonnes avec le tutoriel Aspose.Cells Java
url: /fr/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Générer un diagramme à colonnes avec Aspose.Cells Java

Dans les applications d'aujourd'hui axées sur les données, **générer un diagramme à colonnes** rapidement et de façon programmatique peut transformer des nombres bruts en informations visuelles claires. Que vous construisiez un tableau de bord de reporting, un outil d'analyse ou une simple fonctionnalité d'exportation, Aspose.Cells for Java vous offre une API fluide pour **create chart java** projets sans passer par l'interface Excel. Dans ce tutoriel, vous apprendrez comment configurer la bibliothèque, **populate Excel cells**, ajouter une **chart sheet**, personnaliser le **chart title**, et enfin **export workbook excel** vers un fichier.

## Réponses rapides
- **What does “generate column chart” mean?** Il crée une visualisation de type barre verticale à partir de données tabulaires.  
- **Which library is required?** Aspose.Cells for Java (essai gratuit disponible).  
- **Do I need an Excel installation?** Non, la bibliothèque fonctionne indépendamment de Microsoft Excel.  
- **Can I export to formats other than XLS?** Oui – PDF, PNG, SVG, etc., via `workbook.save()`.  
- **Is a license mandatory for production?** Oui, une licence achetée ou temporaire est requise.

## Qu'est-ce qu'un diagramme à colonnes ?
Un diagramme à colonnes affiche les séries de données sous forme de barres verticales, facilitant la comparaison des valeurs entre différentes catégories telles que les régions, les mois ou les lignes de produits. Aspose.Cells vous permet de créer ce diagramme entièrement par code, vous donnant un contrôle total sur les données, le style et le format de sortie.

## Pourquoi utiliser Aspose.Cells pour créer chart java ?
- **No COM interop** – fonctionne sur tout OS avec une JVM.  
- **Rich styling options** – images, dégradés, légendes et polices personnalisées.  
- **High performance** – adapté aux grands ensembles de données.  
- **Multiple export formats** – XLS, XLSX, PDF, PNG, et plus encore.

## Prérequis
- **Java Development Kit (JDK) 8+** installé.  
- Connaissances de base en Java et familiarité avec les concepts Excel.  

### Bibliothèques requises
Ajoutez Aspose.Cells à votre projet en utilisant l'un des extraits ci‑dessous.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Acquisition de licence
Aspose propose un essai gratuit et une licence temporaire pour des tests approfondis.

- **Essai gratuit** : [Download Free](https://releases.aspose.com/cells/java/)  
- **Licence temporaire** : [Request Here](https://purchase.aspose.com/temporary-license/)

## Configuration d'Aspose.Cells pour Java

Tout d'abord, créez une instance `Workbook` – ce sera le canevas pour nos données et notre diagramme.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## Guide étape par étape

### 1. Créer et nommer une feuille de calcul
Nous stockerons les données brutes dans une feuille appelée **Data**.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Remplir les cellules Excel
Insérez les noms de régions et les chiffres de ventes que le diagramme à colonnes visualisera.

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Ajouter une feuille de graphique
Séparer le graphique des données brutes maintient le classeur ordonné.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. Créer un diagramme à colonnes
Nous créons maintenant réellement des objets **generate column chart**.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Définir une image comme remplissage d'arrière‑plan dans la zone de tracé
Une image d'arrière‑plan peut faire ressortir le graphique.

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. Définir le titre du graphique
Personnaliser le **set chart title** améliore la lisibilité.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. Configurer les données de série et la légende
Liez la plage de données au graphique et positionnez la légende.

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. Exporter le classeur Excel
Enfin, **export workbook excel** vers un fichier XLS (ou tout autre format supporté).

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Applications pratiques
- **Rapports d'entreprise** – Générer automatiquement des graphiques de ventes pour des PDF mensuels.  
- **Outils d'analyse de données** – Intégrer des graphiques dynamiques dans des tableaux de bord d'analyse personnalisés.  
- **Tableaux de bord d'entreprise** – Rafraîchir les images de graphiques à la volée pour une surveillance en temps réel.

## Considérations de performance
- Effectuez des mises à jour de cellules par lots lorsque vous travaillez avec de grands ensembles de données afin de réduire la surcharge.  
- Libérez les ressources (`workbook.dispose()`) si vous traitez de nombreux classeurs dans une boucle.  

## Problèmes courants et solutions
- **Image non affichée** – Vérifiez le chemin du fichier et que le format d'image (PNG, JPEG) est pris en charge.  
- **Graphique vide** – Assurez‑vous que les références de plage de données (`Data!B2:B8`) correspondent aux cellules remplies.  
- **Erreurs de mémoire insuffisante** – Traitez les données par morceaux et appelez `System.gc()` après de gros enregistrements.

## Questions fréquemment posées

**Q : Comment ajouter plusieurs séries à un diagramme à colonnes ?**  
R : Appelez `chart.getNSeries().add()` à plusieurs reprises avec différentes plages de données, par ex., `"Data!C2:C8"` pour une deuxième série.

**Q : Puis‑je modifier les libellés des axes ?**  
R : Oui. Utilisez `chart.getCategoryAxis().setTitle("Regions")` et `chart.getValueAxis().setTitle("Sales")`.

**Q : Quels formats puis‑je exporter en plus de XLS ?**  
R : Utilisez `workbook.save("chart.pdf")`, `workbook.save("chart.png")` ou `workbook.save("chart.xlsx")` pour PDF, PNG et XLSX respectivement.

**Q : Une licence est‑elle requise pour les builds de développement ?**  
R : Un essai gratuit suffit pour l'évaluation, mais une licence permanente ou temporaire est nécessaire pour les déploiements en production.

**Q : Comment améliorer la vitesse de rendu pour des milliers de lignes ?**  
R : Remplissez les cellules avec `cells.importArray()` et minimisez les rafraîchissements du graphique en créant le graphique après le chargement complet des données.

---

**Dernière mise à jour :** 2026-04-08  
**Testé avec :** Aspose.Cells 25.3 for Java  
**Auteur :** Aspose  

## Ressources

- [Documentation Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Télécharger Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Acheter une licence](https://purchase.aspose.com/buy)
- [Essai gratuit](https://releases.aspose.com/cells/java/)
- [Demande de licence temporaire](https://purchase.aspose.com/temporary-license/)
- [Forum de support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}