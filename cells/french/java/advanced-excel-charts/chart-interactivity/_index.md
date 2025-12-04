---
date: 2025-12-04
description: Apprenez à créer des graphiques interactifs en Java avec Aspose.Cells,
  ajoutez des info-bulles au graphique et ajoutez un graphique à approfondissement
  pour une visualisation de données plus riche.
language: fr
linktitle: Create Interactive Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Créer un graphique interactif Java avec Aspose.Cells
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Créer un graphique interactif Java

## Introduction

Les graphiques interactifs offrent à vos utilisateurs la possibilité d’explorer les points de données, de voir les détails au survol, et même de plonger dans des ensembles de données plus profonds — le tout sans quitter la feuille de calcul. Dans ce tutoriel, vous apprendrez **comment créer des graphiques interactifs Java** à l’aide d’Aspose.Cells. Nous verrons comment ajouter des info-bulles, des étiquettes de données, et implémenter une expérience de forage, afin que vos graphiques deviennent plus engageants et informatifs.

## Réponses rapides
- **Quelle bibliothèque est utilisée ?** Aspose.Cells for Java  
- **Puis‑je ajouter des info‑bulles au graphique ?** Oui, en utilisant l’API de data‑label NSeries  
- **Le forage est‑il pris en charge ?** Oui, en attachant des hyperliens aux points de données  
- **Quel format de fichier est produit ?** Classeur XLSX standard avec graphiques intégrés  
- **Ai‑je besoin d’une licence ?** Une version d’essai gratuite suffit pour l’évaluation ; une licence commerciale est requise pour la production  

## Pré‑requis

Avant de commencer, assurez‑vous d’avoir :

- Un environnement de développement Java (JDK 8+ recommandé)  
- La bibliothèque Aspose.Cells for Java (téléchargez‑la depuis la page officielle [Aspose release page](https://releases.aspose.com/cells/java/))  
- Un fichier Excel d’exemple nommé **data.xlsx** contenant les données que vous souhaitez visualiser  

## Étape 1 : Configurer votre projet Java

1. Créez un nouveau projet Java dans votre IDE préféré (IntelliJ IDEA, Eclipse, VS Code, etc.).  
2. Ajoutez le JAR Aspose.Cells à votre classpath — soit en plaçant le JAR dans le dossier `libs`, soit en ajoutant la dépendance Maven/Gradle.

## Étape 2 : Charger les données

Pour créer un graphique interactif, vous avez d’abord besoin d’une feuille de calcul contenant les données. L’extrait ci‑dessous ouvre un classeur existant et récupère la première feuille.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Astuce :** Assurez‑vous que la plage de données que vous comptez représenter est contiguë ; Aspose.Cells détectera automatiquement la plage lorsque vous lierez la série.

## Étape 3 : Créer un graphique

Nous créons maintenant un graphique en colonnes et le plaçons sur la feuille. Vous pouvez remplacer `ChartType.COLUMN` par tout autre type (par ex. `ChartType.LINE`) si vous préférez un style visuel différent.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Pourquoi c’est important :** Créer le graphique par programme vous donne un contrôle total sur sa taille, sa position et sa source de données, ce qui est essentiel pour concevoir des expériences interactives.

## Étape 4 : Ajouter de l’interactivité

### Comment ajouter des info‑bulles au graphique

Les info‑bulles (ou étiquettes de données affichant les valeurs) permettent aux utilisateurs de voir instantanément la valeur exacte derrière chaque barre. Le code suivant active les étiquettes de données et les configure pour afficher la valeur.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### Comment ajouter des étiquettes de données (callouts)

Si vous souhaitez que les étiquettes apparaissent sous forme de callouts plutôt que de texte simple, activez la propriété `ShowLabelAsDataCallout`.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### Comment ajouter un graphique à forage

Le forage permet à l’utilisateur de cliquer sur un point de données et d’accéder à une vue détaillée associée — généralement implémenté avec un hyperlien. Ci‑dessous, nous attachons une URL au premier point de la série.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Piège fréquent :** N’oubliez pas de définir la cible de l’hyperlien vers une page capable de rendre les données détaillées (par ex. un rapport web ou une autre feuille Excel). Sinon le clic mènera à un lien mort.

## Étape 5 : Enregistrer le classeur

Après avoir configuré le graphique, persistez le classeur. Le fichier résultant contient le graphique interactif prêt à être ouvert dans Excel ou tout visualiseur compatible.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Conclusion

Dans ce guide, vous avez appris **comment créer des graphiques interactifs Java** avec Aspose.Cells, en couvrant :

- Le chargement des données depuis un classeur existant  
- La création d’un graphique en colonnes par programme  
- L’ajout d’info‑bulles et d’étiquettes de données sous forme de callouts  
- L’implémentation du forage via des hyperliens  
- L’enregistrement du classeur final  

Ces techniques transforment des feuilles de calcul statiques en tableaux de bord dynamiques et conviviaux, améliorant la compréhension des données et la prise de décision.

## Questions fréquentes

**Q : Comment changer le type de graphique ?**  
R : Modifiez l’énumération `ChartType` dans la méthode `add` (par ex. `ChartType.LINE` pour un graphique linéaire).

**Q : Puis‑je personnaliser l’apparence des info‑bulles ?**  
R : Oui, vous pouvez ajuster la taille de police, la couleur, l’arrière‑plan et d’autres propriétés de style via l’objet `DataLabels`.

**Q : Comment gérer l’interactivité du graphique dans une application web ?**  
R : Exportez le classeur au format XLSX, puis utilisez une bibliothèque de graphiques JavaScript (par ex. Highcharts) pour rendre les données côté client, ou intégrez le fichier Excel dans un Office Web Viewer qui respecte les hyperliens.

**Q : Où trouver plus d’exemples ?**  
R : Consultez la [Référence API Aspose.Cells Java](https://reference.aspose.com/cells/java/) officielle pour la liste complète des classes et méthodes liées aux graphiques.

**Q : Ai‑je besoin d’une licence pour une utilisation en production ?**  
R : Oui, une licence commerciale est requise pour le déploiement ; une licence d’évaluation gratuite est disponible pour les tests.

---

**Dernière mise à jour :** 2025-12-04  
**Testé avec :** Aspose.Cells for Java 24.12 (dernière version au moment de la rédaction)  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}