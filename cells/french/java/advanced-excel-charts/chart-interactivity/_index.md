---
date: 2025-12-01
description: Apprenez à modifier le type de graphique Excel et à ajouter des fonctionnalités
  interactives comme les info-bulles, les étiquettes de données et le drill‑down à
  l'aide d'Aspose.Cells pour Java.
language: fr
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Modifier le type de graphique Excel et ajouter de l’interactivité – Aspose.Cells
  Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Modifier le type de graphique Excel et ajouter de l'interactivité

## Introduction

Les graphiques interactifs permettent à votre audience d'explorer les données en temps réel, tandis que la possibilité de **modifier le type de graphique Excel** vous offre la flexibilité de présenter l'information sous le format visuel le plus efficace. Dans ce tutoriel, vous apprendrez à utiliser Aspose.Cells for Java pour changer le type d’un graphique, ajouter des infobulles, intégrer des étiquettes de données, et même créer des liens de drill‑down — le tout sans quitter votre code Java. À la fin, vous disposerez d’un classeur Excel entièrement interactif que vous pourrez intégrer dans des rapports, des tableaux de bord ou des applications web.

## Réponses rapides
- **Puis‑je changer le type de graphique par programme ?** Oui – utilisez l’énumération `ChartType` lors de la création ou de la mise à jour d’un graphique.  
- **Comment ajouter des infobulles à un graphique ?** Activez les étiquettes de données et définissez `ShowValue` sur true.  
- **Quelle est la façon la plus simple d’ajouter des liens de drill‑down ?** Attachez un hyperlien à un point de données via `getHyperlinks().add(url)`.  
- **Ai‑je besoin d’une licence pour Aspose.Cells ?** Une version d’essai gratuite suffit pour le développement ; une licence est requise en production.  
- **Quelle version de Java est prise en charge ?** Java 8 et supérieures sont entièrement supportées.

## Qu’est‑ce que « modifier le type de graphique Excel » ?

Modifier le type de graphique consiste à remplacer la représentation visuelle (par ex. d’un graphique en colonnes à un graphique en lignes) tout en conservant les données sous‑jacentes. Cela est utile lorsqu’on découvre qu’un autre type de graphique communique mieux les tendances, les comparaisons ou les distributions.

## Pourquoi ajouter de l’interactivité aux graphiques Excel ?

- **Meilleure compréhension des données :** Les infobulles et les étiquettes de données permettent aux utilisateurs de voir les valeurs exactes sans faire défiler.  
- **Présentations engageantes :** Les éléments interactifs retiennent l’attention des spectateurs.  
- **Capacité de drill‑down :** Les hyperliens permettent aux utilisateurs de passer à des feuilles détaillées ou à des ressources externes.  
- **Actifs réutilisables :** Un même classeur peut servir à plusieurs scénarios de reporting en changeant simplement le type de graphique.

## Prérequis

- Environnement de développement Java (JDK 8+)  
- Bibliothèque Aspose.Cells for Java (téléchargez‑la depuis [here](https://releases.aspose.com/cells/java/))  
- Un fichier Excel d’exemple (`data.xlsx`) contenant les données que vous souhaitez visualiser

## Guide étape par étape

### Étape 1 : Configurer votre projet Java

1. Créez un nouveau projet Java dans votre IDE préféré (IntelliJ IDEA, Eclipse, VS Code, etc.).  
2. Ajoutez le JAR Aspose.Cells au classpath de votre projet.

### Étape 2 : Charger le classeur source

Nous commençons par charger un classeur existant qui contient les données pour notre graphique.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Étape 3 : Créer un graphique et **modifier son type**

Ci‑dessous, nous créons un graphique en colonnes, puis montrons immédiatement comment le basculer en graphique en lignes si besoin.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **Astuce :** Modifier le type de graphique après sa création est aussi simple que d’appeler `setChartType(...)`. Cela répond au mot‑clé principal **modifier le type de graphique Excel** sans nécessiter la création d’un nouveau graphique.

### Étape 4 : Ajouter de l’interactivité

#### 4.1 Ajouter des infobulles au graphique

Les infobulles s’affichent lorsqu’un utilisateur survole un point de données. Dans Aspose.Cells, elles sont implémentées via les étiquettes de données.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2 Ajouter des étiquettes de données (**add data labels chart**)

Les étiquettes de données peuvent afficher la valeur exacte, le nom de la catégorie, ou les deux. Ici nous utilisons un style d’appel.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3 Implémenter le drill‑down (**add drill down excel**)

Un lien de drill‑down permet aux utilisateurs de cliquer sur un point et d’accéder à une vue détaillée, que ce soit dans le classeur ou sur une page web.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### Étape 5 : Enregistrer le classeur

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problèmes courants et solutions

| Problème | Raison | Solution |
|----------|--------|----------|
| Les infobulles ne s’affichent pas | `HasDataLabels` non activé | Assurez‑vous d’appeler `setHasDataLabels(true)` avant de configurer `ShowValue`. |
| Le lien de drill‑down ne fonctionne pas | URL de l’hyperlien mal formée | Vérifiez que l’URL commence par `http://` ou `https://`. |
| Le type de graphique ne change pas | Utilisation d’une version ancienne d’Aspose.Cells | Mettez à jour vers la dernière version (testée avec 24.12). |

## FAQ

**Q : Comment puis‑je changer le type de graphique après sa création ?**  
R : Appelez `chart.setChartType(ChartType.YOUR_CHOICE)` sur l’objet `Chart` existant. Cela répond directement à la demande de **modifier le type de graphique Excel**.

**Q : Puis‑je personnaliser l’apparence des infobulles ?**  
R : Oui. Utilisez `chart.getNSeries().get(0).getPoints().getDataLabels()` pour définir la taille de police, la couleur et le fond.

**Q : Est‑il possible d’ajouter plusieurs liens de drill‑down dans un même graphique ?**  
R : Absolument. Parcourez les points et appelez `getHyperlinks().add(url)` pour chaque point que vous souhaitez lier.

**Q : Aspose.Cells prend‑il en charge d’autres types de graphiques comme le secteur ou le radar ?**  
R : Tous les types de graphiques définis dans l’énumération `ChartType` sont supportés, y compris `PIE`, `RADAR`, `AREA`, etc.

**Q : Où puis‑je trouver plus d’exemples ?**  
R : Consultez la référence officielle [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) pour une liste complète des méthodes liées aux graphiques.

## Conclusion

Vous savez maintenant comment **modifier le type de graphique Excel**, intégrer des **infobulles**, ajouter des **étiquettes de données**, et créer des liens de **drill‑down** en utilisant Aspose.Cells for Java. Ces fonctionnalités interactives transforment les feuilles de calcul statiques en outils dynamiques d’exploration de données, idéaux pour les tableaux de bord, les rapports et l’analyse web.

---

**Dernière mise à jour :** 2025-12-01  
**Testé avec :** Aspose.Cells 24.12 for Java  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}