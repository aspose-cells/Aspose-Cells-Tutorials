---
date: 2025-12-06
description: Apprenez à changer le type de graphique Excel et à créer des graphiques
  interactifs avec Java en utilisant Aspose.Cells. Ajoutez des infobulles au graphique,
  des étiquettes de données et un drill‑down pour une visualisation de données plus
  riche.
language: fr
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Modifier le type de graphique Excel avec Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Modifier le type de graphique Excel et ajouter de l'interactivité

## Introduction

Les graphiques interactifs donnent à vos rapports Excel un nouveau niveau d'analyse, permettant aux utilisateurs de survoler, cliquer et explorer les points de données directement. Dans ce tutoriel, vous **changerez le type de graphique Excel** et **créerez des solutions de graphiques interactifs Java** avec Aspose.Cells for Java. Nous verrons comment ajouter des info‑bulles au graphique, des étiquettes de données, et un simple hyperlien de forage afin que votre audience puisse approfondir les chiffres.

## Réponses rapides
- **Quelle bibliothèque est utilisée ?** Aspose.Cells for Java  
- **Puis-je changer le type de graphique ?** Oui – il suffit de modifier l'énumération `ChartType` lors de la création du graphique.  
- **Comment ajouter des info‑bulles à un graphique ?** Utilisez l'API des étiquettes de données (`setHasDataLabels(true)`) et activez l'affichage des valeurs.  
- **Le forage (drill‑down) est‑il pris en charge ?** Vous pouvez attacher des hyperliens aux points de données pour un comportement de forage de base.  
- **Prérequis ?** IDE Java, JAR Aspose.Cells, et un fichier Excel avec des données d'exemple.

## Prérequis

Avant de commencer, assurez‑vous de disposer de ce qui suit :

- Environnement de développement Java (JDK 8+ recommandé)  
- Bibliothèque Aspose.Cells for Java (télécharger depuis [here](https://releases.aspose.com/cells/java/))  
- Un classeur d'exemple (`data.xlsx`) contenant les données que vous souhaitez visualiser  

## Étape 1 : Configurer votre projet Java

1. Créez un nouveau projet Java dans votre IDE préféré (IntelliJ IDEA, Eclipse, etc.).  
2. Ajoutez le JAR Aspose.Cells au chemin de construction de votre projet ou aux dépendances Maven/Gradle.

## Étape 2 : Charger les données

Pour travailler avec les graphiques, vous devez d'abord charger un classeur en mémoire.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Étape 3 : Créer un graphique (et changer son type)

Vous pouvez choisir n'importe quel type de graphique qui correspond à votre analyse. Ci‑dessous, nous créons un **graphique en colonnes**, mais vous pouvez facilement passer à un graphique en ligne, en secteur ou en barres en modifiant l'énumération `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Astuce :** Pour **modifier le type de graphique Excel**, remplacez `ChartType.COLUMN` par `ChartType.LINE`, `ChartType.PIE`, etc.

## Étape 4 : Ajouter de l'interactivité

### 4.1. Ajouter des info‑bulles (Add Tooltips to Chart)

Les info‑bulles apparaissent lorsque l'utilisateur survole un point de données. Le code suivant active les étiquettes de données et affiche la valeur comme une info‑bulle.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Ajouter des étiquettes de données

Les étiquettes de données offrent un repère visuel permanent sur le graphique lui‑même. Vous pouvez les afficher sous forme d'appels pour une meilleure lisibilité.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Implémenter le forage (Hyperlink sur un point de données)

Une façon simple d'ajouter la capacité de forage consiste à attacher un hyperlien à un point spécifique. Cliquer sur le point ouvre une page Web avec des informations détaillées.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Étape 5 : Enregistrer le classeur

Après avoir configuré le graphique, persistez le classeur afin que les fonctionnalités interactives soient enregistrées dans le fichier de sortie.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problèmes courants & solutions

| Problème | Solution |
|----------|----------|
| **Info‑bulles non affichées** | Assurez‑vous que `setHasDataLabels(true)` est appelé avant de configurer `setShowValue(true)`. |
| **Hyperlien non cliquable** | Vérifiez que le format de sortie prend en charge les hyperliens (par ex., XLSX, pas CSV). |
| **Le type de graphique ne change pas** | Revérifiez que vous avez modifié la bonne énumération `ChartType` lors de l'ajout du graphique. |

## Questions fréquentes

**Q : Comment puis‑je changer le type de graphique après sa création ?**  
R : Vous devez créer un nouveau graphique avec le `ChartType` souhaité. Aspose.Cells ne propose pas de conversion de type en‑place, il faut donc supprimer l'ancien graphique et en ajouter un nouveau.

**Q : Puis‑je personnaliser l'apparence des info‑bulles ?**  
R : Oui. Utilisez les propriétés de `DataLabel` telles que `setFontSize`, `setFontColor` et `setBackgroundColor` pour styliser le texte de l'info‑bulle.

**Q : Comment gérer les interactions utilisateur dans une application web ?**  
R : Exportez le classeur vers un fichier HTML ou XLSX et utilisez JavaScript côté client pour capturer les événements de clic sur les éléments du graphique.

**Q : Où puis‑je trouver plus d’exemples et de documentation ?**  
R : Consultez la [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) pour une liste complète des classes et méthodes liées aux graphiques.

## Conclusion

Vous savez maintenant comment **modifier le type de graphique Excel**, **créer des solutions de graphiques interactifs Java**, et les enrichir avec des info‑bulles, des étiquettes de données et des hyperliens de forage en utilisant Aspose.Cells for Java. Ces améliorations rendent vos rapports Excel beaucoup plus engageants et instructifs pour les utilisateurs finaux.

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.Cells for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}