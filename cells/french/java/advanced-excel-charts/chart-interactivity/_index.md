---
date: 2026-08-21
description: Apprenez comment ajouter des tooltips, des data labels et modifier le
  type de graphique dans les graphiques Excel en utilisant Aspose.Cells for Java –
  guide étape par étape avec des exemples interactifs.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Modifier le type de graphique Excel
og_description: Apprenez comment ajouter des tooltips, des data labels et modifier
  le type de graphique dans les graphiques Excel en utilisant Aspose.Cells for Java
  – guide étape par étape avec des exemples interactifs.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Comment ajouter des tooltips et des data labels aux graphiques Excel en
  Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Comment ajouter des tooltips et des data labels aux graphiques Excel en Java
url: /fr/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter des étiquettes de données à un graphique Excel et changer le type de graphique – Aspose.Cells Java

Les graphiques interactifs donnent à vos rapports Excel un nouveau niveau d'analyse, et **how to add tooltips** rend l'information instantanément lisible. Dans ce tutoriel, vous apprendrez comment **add data labels to Excel chart**, **change the chart type**, et créer des solutions Java interactives avec Aspose.Cells. Nous vous montrerons également comment ajouter des info-bulles et un simple hyperlien de drill‑down afin que votre audience puisse explorer les données en profondeur.

## Réponses rapides
- **Quelle bibliothèque est utilisée ?** Aspose.Cells for Java  
- **Puis-je changer le type de graphique ?** Oui – il suffit de modifier l'énumération `ChartType` lors de la création du graphique.  
- **Comment ajouter des info-bulles à un graphique ?** Utilisez l'API des étiquettes de données (`setHasDataLabels(true)`) et activez l'affichage des valeurs.  
- **Le drill‑down est‑il pris en charge ?** Vous pouvez attacher des hyperliens aux points de données pour un comportement de drill‑down de base.  
- **Prérequis ?** IDE Java, JAR Aspose.Cells, et un fichier Excel avec des données d'exemple.

## Qu'est-ce que l'ajout d'info-bulles ?
**How to add tooltips** fait référence au processus d'activation du texte au survol qui affiche la valeur d'un point de données ou des informations personnalisées sur un graphique Excel. Dans Aspose.Cells, cela est réalisé via les paramètres des étiquettes de données du graphique. Les info-bulles aident les utilisateurs à comprendre rapidement les données sans encombrer le graphique, et elles peuvent être personnalisées en police, couleur et format.

## Pourquoi utiliser des graphiques interactifs avec Aspose.Cells ?
Aspose.Cells prend en charge **50+ formats d'entrée et de sortie** — y compris XLSX, CSV, PDF et HTML — et peut traiter des classeurs contenant **plus de 1 000 feuilles** sans charger le fichier complet en mémoire, offrant une génération rapide de graphiques côté serveur pour les rapports d'entreprise. Les graphiques interactifs permettent également d'intégrer des hyperliens, des mises à jour de données dynamiques et l'exportation vers des formats adaptés au web, ce qui les rend idéaux pour les tableaux de bord et les portails de reporting.

## Prérequis

Avant de commencer, assurez‑vous de disposer de :

- Environnement de développement Java (JDK 8+ recommandé)  
- Bibliothèque Aspose.Cells for Java (téléchargement depuis la [page de téléchargement Aspose.Cells for Java](https://releases.aspose.com/cells/java/))  
- Un classeur d'exemple (`data.xlsx`) contenant les données que vous souhaitez visualiser  

## Étape 1 : configuration de votre projet Java

1. Créez un nouveau projet Java dans votre IDE préféré (IntelliJ IDEA, Eclipse, etc.).  
2. Ajoutez le JAR Aspose.Cells au chemin de construction de votre projet ou aux dépendances Maven/Gradle.

## Étape 2 : chargement des données

Pour travailler avec les graphiques, vous devez d'abord charger un classeur en mémoire.

La classe `Workbook` représente un fichier Excel, et `Worksheet` représente une feuille unique dans ce fichier.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Comment changer le type de graphique dans Aspose.Cells ?

Créez un nouveau graphique avec l'énumération `ChartType` souhaitée ; Aspose.Cells ne modifie pas le type d'un graphique existant sur place, vous devez donc ajouter un nouveau graphique du type correct et, éventuellement, supprimer l'ancien. Cette approche garantit que toutes les séries et axes sont reconstruits correctement pour la nouvelle représentation visuelle.

## Étape 3 : création d'un graphique (et changement de son type)

Vous pouvez choisir n'importe quel type de graphique qui correspond à votre analyse. Ci-dessous, nous créons un **graphique en colonnes**, mais vous pouvez facilement passer à un graphique en lignes, en secteurs ou en barres en modifiant l'énumération `ChartType`.

L'objet `Chart` fournit des méthodes pour configurer la représentation visuelle des données dans la feuille de calcul.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Astuce :** Pour **change Excel chart type**, remplacez `ChartType.COLUMN` par `ChartType.LINE`, `ChartType.PIE`, etc.

## Comment ajouter des info-bulles à un graphique Excel ?

Chargez votre graphique, activez les étiquettes de données, et définissez le drapeau `showValue`. L'info-bulle affichera alors la valeur de la cellule sous-jacente chaque fois qu'un utilisateur survole un point de données dans le fichier Excel rendu ou la vue HTML. Vous pouvez également personnaliser la police, la couleur et l'arrière‑plan de l'info-bulle pour correspondre au style de votre rapport.

La classe `DataLabel` contrôle l'apparence et le contenu des étiquettes de données, qui servent également d'info-bulles.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## Étape 4 : ajout d'interactivité

### 4.1. Ajout d'info-bulles (add tooltips to chart)

Les info-bulles apparaissent lorsque l'utilisateur survole un point de données. Le code suivant active les étiquettes de données et affiche la valeur comme une info-bulle.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Ajout d'étiquettes de données – **add data labels to excel chart**

Les étiquettes de données offrent un repère visuel permanent sur le graphique lui‑même. Vous pouvez les afficher sous forme d'appels pour une meilleure lisibilité.

La classe `DataLabel` contrôle l'apparence des étiquettes sur chaque série. En appelant `setHasDataLabels(true)` et en configurant des propriétés telles que `setShowValue(true)`, vous intégrez la valeur numérique directement sur le graphique, la rendant instantanément visible sans aucune interaction. Des options supplémentaires vous permettent d'afficher les noms de séries, les pourcentages ou du texte personnalisé pour un contexte plus riche.

> **Pourquoi ajouter des étiquettes de données ?** Inclure des étiquettes de données directement sur le graphique élimine le besoin pour les utilisateurs de survoler ou deviner les valeurs, améliorant la clarté du rapport.

### 4.3. Mise en œuvre du drill‑down (hyperlien sur un point de données)

Une façon simple d'ajouter une capacité de drill‑down consiste à attacher un hyperlien à un point spécifique. Cliquer sur le point ouvre une page web avec des informations détaillées.

La classe `Hyperlink` attache un lien cliquable à un élément du graphique, permettant la navigation drill‑down.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Comment ajouter des étiquettes de données à un graphique Excel ?

La classe `DataLabel` contrôle l'apparence des étiquettes sur chaque série. En appelant `setHasDataLabels(true)` et en configurant des propriétés telles que `setShowValue(true)`, vous intégrez la valeur numérique directement sur le graphique, la rendant instantanément visible sans aucune interaction. Des options supplémentaires vous permettent d'afficher les noms de séries, les pourcentages ou du texte personnalisé pour un contexte plus riche.

## Étape 5 : sauvegarde du classeur

Après avoir configuré le graphique, persistez le classeur afin que les fonctionnalités interactives soient enregistrées dans le fichier de sortie.

Appeler `workbook.save` écrit le classeur modifié dans un fichier au format choisi.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problèmes courants & solutions

| Problème | Solution |
|----------|----------|
| **Info-bulles non affichées** | Assurez‑vous que `setHasDataLabels(true)` est appelé avant de configurer `setShowValue(true)`. |
| **Hyperlien non cliquable** | Vérifiez que le format de sortie prend en charge les hyperliens (par ex., XLSX, pas CSV). |
| **Le type de graphique ne change pas** | Vérifiez à nouveau que vous avez modifié la bonne énumération `ChartType` lors de l'ajout du graphique. |

## Questions fréquemment posées

**Q : Comment puis‑je changer le type de graphique après sa création ?**  
R : Vous devez créer un nouveau graphique avec le `ChartType` souhaité. Aspose.Cells ne propose pas de conversion de type sur place, il faut donc supprimer l'ancien graphique et en ajouter un nouveau.

**Q : Puis‑je personnaliser l'apparence des info-bulles ?**  
R : Oui. Utilisez les propriétés `DataLabel` telles que `setFontSize`, `setFontColor` et `setBackgroundColor` pour styliser le texte de l'info-bulle.

**Q : Comment gérer les interactions utilisateur dans une application web ?**  
R : Exportez le classeur vers un fichier HTML ou XLSX et utilisez JavaScript côté client pour capturer les événements de clic sur les éléments du graphique.

**Q : Où puis‑je trouver plus d'exemples et de documentation ?**  
R : Consultez la [Référence API Aspose.Cells Java](https://reference.aspose.com/cells/java/) pour une liste complète des classes et méthodes liées aux graphiques.

## Conclusion

Vous savez maintenant comment **add data labels to Excel chart**, **change Excel chart type**, **create interactive chart Java** solutions, et les enrichir avec des info-bulles, des étiquettes de données et des hyperliens de drill‑down en utilisant Aspose.Cells for Java. Ces améliorations rendent vos rapports Excel beaucoup plus attrayants et instructifs pour les utilisateurs finaux.

---

**Dernière mise à jour :** 2026-08-21  
**Testé avec :** Aspose.Cells for Java 24.12  
**Auteur :** Aspose

## Tutoriels associés

- [Comment modifier les graphiques Excel et les étiquettes de données avec Aspose.Cells for Java](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Extraire les étiquettes d'axe d'un graphique Excel avec Aspose.Cells Java : guide complet](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Créer des graphiques à bulles dans Excel avec Aspose.Cells for Java : guide étape par étape](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}