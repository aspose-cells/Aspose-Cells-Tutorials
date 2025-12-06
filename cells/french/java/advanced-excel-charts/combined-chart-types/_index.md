---
date: 2025-12-06
description: Apprenez comment ajouter des séries de données, créer des types de graphiques
  combinés, enregistrer le classeur Excel et exporter le graphique au format PNG avec
  Aspose.Cells pour Java.
language: fr
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Ajouter des séries de données pour créer un graphique combiné avec Aspose.Cells
url: /java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une série de données pour créer un graphique combiné avec Aspose.Cells

Dans ce tutoriel, vous allez **ajouter une série de données** à un classeur Excel et apprendre comment **créer des graphiques combinés** avec Aspose.Cells for Java. Nous parcourrons chaque étape — de la configuration du classeur, l'ajout de séries, la personnalisation de la légende, jusqu'à **enregistrer le classeur Excel** et exporter le **graphique au format PNG**. À la fin, vous disposerez d'un graphique combiné prêt à l'emploi que vous pourrez intégrer dans des rapports ou des tableaux de bord.

## Réponses rapides
- **Quelle bibliothèque crée des graphiques combinés ?** Aspose.Cells for Java  
- **Comment ajouter une série de données ?** Utilisez `chart.getNSeries().add(...)`  
- **Puis-je exporter le graphique sous forme d'image ?** Oui, avec `chart.toImage(...)` (PNG)  
- **Quel format de fichier puis‑je enregistrer le classeur ?** Standard `.xlsx` (Excel)  
- **Ai‑je besoin d'une licence pour la production ?** Une licence valide d'Aspose.Cells est requise  

## Qu'est-ce que **add data series** dans Aspose.Cells ?
Ajouter une série de données indique au graphique quelles cellules contiennent les valeurs que vous souhaitez tracer. Chaque série peut représenter une ligne, une colonne ou tout autre type de graphique, et vous pouvez les combiner pour créer un **graphique combiné**.

## Pourquoi créer un **graphique combiné** ?
Un graphique combiné vous permet d'afficher différents ensembles de données avec des représentations visuelles distinctes (par ex., une série en ligne superposée à une série en colonnes) dans une même vue. C'est idéal pour comparer des tendances avec des totaux, mettre en évidence des corrélations ou fournir des informations plus riches dans un format compact.

## Prérequis
- Java Development Kit (JDK) 8 ou supérieur  
- Bibliothèque Aspose.Cells for Java (téléchargez depuis le lien ci‑dessous)  
- Familiarité de base avec la syntaxe Java et les concepts Excel  

## Commencer

Tout d'abord, téléchargez la bibliothèque Aspose.Cells for Java depuis le site officiel :

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Une fois le JAR ajouté au classpath de votre projet, vous pouvez commencer à créer le graphique.

### Étape 1 : Importer les classes Aspose.Cells
```java
import com.aspose.cells.*;
```

### Étape 2 : Créer un nouveau classeur
```java
Workbook workbook = new Workbook();
```

### Étape 3 : Accéder à la première feuille de calcul
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Étape 4 : Ajouter un objet de graphique combiné  
Nous commencerons avec un graphique en ligne et ajouterons plus tard d'autres séries pour obtenir un effet de **graphique combiné**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Ajouter des données au graphique

Maintenant que le conteneur du graphique existe, nous devons le alimenter avec des données.

### Étape 5 : Définir les plages de données et **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Astuce :** Le premier paramètre (`"A1:A5"`) est la plage pour la première série, et le second (`"B1:B5"`) crée une deuxième série qui sera combinée avec la première.

### Étape 6 : Définir les données de catégorie (axe X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Personnaliser le graphique

Un bon graphique raconte une histoire. Donnons‑lui des titres, des libellés d'axes et une légende claire.

### Étape 7 : Définir le titre du graphique et les libellés des axes
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Étape 8 : **Add legend chart** et ajuster sa position
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Enregistrement et exportation du graphique

Après la personnalisation, vous voudrez **enregistrer le classeur Excel** et également générer une image.

### Étape 9 : Enregistrer le classeur au format Excel
```java
workbook.save("CombinedChart.xlsx");
```

### Étape 10 : Exporter le **chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> La méthode `chart.toImage` **génère des images de graphique Excel** qui peuvent être utilisées dans des pages web, des rapports ou des e‑mails.

## Problèmes courants & dépannage

| Problème | Solution |
|----------|----------|
| **Aucune donnée n'apparaît** | Vérifiez que les plages de cellules (`A1:A5`, `B1:B5`, `C1:C5`) contiennent réellement des données avant de créer le graphique. |
| **La légende chevauche le graphique** | Définissez `chart.getLegend().setOverlay(false)` ou déplacez la légende à une autre position (par ex., `RIGHT`). |
| **Le fichier image est vide** | Assurez‑vous que le graphique possède au moins une série et que `chart.toImage` est appelé après toutes les personnalisations. |
| **L'enregistrement génère une exception** | Vérifiez que vous avez les droits d'écriture sur le répertoire cible et que le fichier n'est pas ouvert dans Excel. |

## Questions fréquentes

**Q : Comment installer Aspose.Cells for Java ?**  
A : Téléchargez le JAR depuis le site officiel et ajoutez‑le au classpath de votre projet. Le lien de téléchargement est : [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q : Puis‑je créer d'autres types de graphiques en plus des lignes et des colonnes ?**  
A : Oui, Aspose.Cells prend en charge les graphiques à barres, secteurs, nuages de points, aires, et bien d’autres types de graphiques. Consultez la documentation de l'API pour la liste complète.

**Q : Une licence est‑elle requise pour une utilisation en production ?**  
A : Une licence valide d'Aspose.Cells est requise pour les déploiements en production. Un essai gratuit est disponible pour l'évaluation.

**Q : Comment changer les couleurs de chaque série ?**  
A : Utilisez `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (ou similaire) après avoir ajouté les séries.

**Q : Où puis‑je trouver plus d'exemples de code ?**  
A : Une documentation complète et des exemples supplémentaires sont disponibles sur le site de référence Aspose : [here](https://reference.aspose.com/cells/java/).

---

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.Cells for Java 24.12  
**Author:** Aspose  

---