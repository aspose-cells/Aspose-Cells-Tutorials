---
date: 2026-02-14
description: Apprenez à exporter un graphique au format PNG, ajouter une série de
  données, combiner un graphique en courbes et colonnes, enregistrer le classeur au
  format XLSX et ajouter une légende au graphique en utilisant Aspose.Cells pour Java.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: Exporter le graphique en PNG et ajouter des séries de données pour le graphique
  combiné
url: /fr/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Exporter le graphique au format PNG et ajouter une série de données pour un graphique combiné

Dans ce tutoriel, vous allez **ajouter une série de données** à un classeur Excel, **combiner des éléments de graphique ligne et colonne**, et apprendre comment **exporter le graphique au format PNG** en utilisant Aspose.Cells for Java. Nous parcourrons chaque étape — depuis la configuration du classeur, l'ajout du graphique à une feuille de calcul, la personnalisation de la légende, jusqu'à **enregistrer le classeur au format xlsx** et générer une image PNG du graphique. À la fin, vous disposerez d'un graphique combiné prêt à l'emploi que vous pourrez intégrer dans des rapports ou des tableaux de bord.

## Réponses rapides
- **Which library creates combined charts?** Quelle bibliothèque crée des graphiques combinés ? Aspose.Cells for Java  
- **How do I add a data series?** Comment ajouter une série de données ? Use `chart.getNSeries().add(...)`  
- **How can I export chart to png?** Comment exporter le graphique au format PNG ? Call `chart.toImage("file.png", ImageFormat.getPng())`  
- **What file format can I save the workbook as?** Quel format de fichier puis‑je enregistrer le classeur ? Standard `.xlsx` (save workbook as xlsx)  
- **Do I need a license for production?** Une licence est‑elle nécessaire pour la production ? A valid Aspose.Cells license is required  

## Qu’est‑ce que **export chart to PNG** dans Aspose.Cells ?
Exporter un graphique au format PNG crée une image raster du graphique Excel qui peut être affichée dans des pages web, des rapports ou des e‑mails sans nécessiter l’application Excel.

## Pourquoi créer un **combined line column chart** ?
Un graphique combiné vous permet d’afficher différents ensembles de données avec des représentations visuelles distinctes (par ex., une série ligne superposée à une série colonne) dans une même vue. C’est idéal pour comparer les tendances aux totaux, mettre en évidence des corrélations ou fournir des informations plus riches dans un format compact.

## Prérequis
- Java Development Kit (JDK) 8 ou supérieur  
- Bibliothèque Aspose.Cells for Java (téléchargement depuis le lien ci‑dessous)  
- Familiarité de base avec la syntaxe Java et les concepts Excel  

## Commencer

Tout d’abord, téléchargez la bibliothèque Aspose.Cells for Java depuis le site officiel :

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

### Étape 4 : Ajouter un objet de graphique combiné à la feuille de calcul  
Nous commencerons avec un graphique ligne et ajouterons plus tard une série colonne pour obtenir un effet de **combined line column chart**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Ajouter des données au graphique

Maintenant que le conteneur du graphique existe, nous devons le nourrir avec des données.

### Étape 5 : Définir les plages de données et **ajouter une série de données**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** Le premier paramètre (`"A1:A5"`) est la plage pour la première série, et le second (`"B1:B5"`) crée une deuxième série qui sera combinée avec la première.

### Étape 6 : Définir les données de catégorie (axe X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Personnaliser le graphique

Un bon graphique raconte une histoire. Donnons‑lui des titres, des libellés d’axes et une légende claire.

### Étape 7 : **Définir les libellés des axes du graphique** et le titre
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Étape 8 : **Ajouter la légende du graphique** et ajuster sa position
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Enregistrement et exportation du graphique

Après la personnalisation, vous voudrez **enregistrer le classeur au format xlsx** et également générer une image.

### Étape 9 : Enregistrer le classeur en tant que fichier Excel (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### Étape 10 : **Exporter le graphique au format PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> La méthode `chart.toImage` **génère des images de graphique Excel** qui peuvent être utilisées dans des pages web, des rapports ou des e‑mails.

## Problèmes courants & dépannage

| Problème | Solution |
|----------|----------|
| **Aucune donnée n’apparaît** | Vérifiez que les plages de cellules (`A1:A5`, `B1:B5`, `C1:C5`) contiennent réellement des données avant de créer le graphique. |
| **La légende chevauche le graphique** | Définissez `chart.getLegend().setOverlay(false)` ou déplacez la légende vers une autre position (par ex., `RIGHT`). |
| **Le fichier image est vide** | Assurez‑vous que le graphique possède au moins une série et que `chart.toImage` est appelé après toutes les personnalisations. |
| **L’enregistrement génère une exception** | Vérifiez que vous avez les droits d’écriture sur le répertoire cible et que le fichier n’est pas ouvert dans Excel. |

## Questions fréquemment posées

**Q : Comment installer Aspose.Cells for Java ?**  
R : Téléchargez le JAR depuis le site officiel et ajoutez‑le au classpath de votre projet. Le lien de téléchargement est : [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q : Puis‑je créer d’autres types de graphiques en plus des lignes et colonnes ?**  
R : Oui, Aspose.Cells prend en charge les graphiques à barres, secteurs, nuages de points, aires, et bien d’autres. Consultez la documentation API pour la liste complète.

**Q : Une licence est‑elle requise pour une utilisation en production ?**  
R : Une licence Aspose.Cells valide est nécessaire pour les déploiements en production. Un essai gratuit est disponible pour évaluation.

**Q : Comment changer les couleurs de chaque série ?**  
R : Utilisez `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (ou similaire) après avoir ajouté les séries.

**Q : Où puis‑je trouver plus d’exemples de code ?**  
R : Une documentation complète et des exemples supplémentaires sont disponibles sur le site de référence Aspose : [here](https://reference.aspose.com/cells/java/).

---

**Dernière mise à jour :** 2026-02-14  
**Testé avec :** Aspose.Cells for Java dernière version  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}