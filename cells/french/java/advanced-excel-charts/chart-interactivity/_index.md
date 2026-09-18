---
date: 2026-02-09
description: Apprenez à ajouter des étiquettes de données à un graphique Excel et
  à modifier le type de graphique à l'aide d'Aspose.Cells pour Java, ainsi que les
  info-bulles et l'interactivité drill‑down.
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Ajouter des étiquettes de données à un graphique Excel avec Aspose.Cells Java
url: /fr/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter des étiquettes de données à un graphique Excel et changer le type de graphique – Aspose.Cells Java

Les graphiques interactifs donnent à vos rapports Excel un nouveau niveau d’analyse, et **ajouter des étiquettes de données à un graphique Excel** rend l’information immédiatement lisible. Dans ce tutoriel, vous apprendrez comment **ajouter des étiquettes de données à un graphique Excel**, changer le type de graphique, et créer des solutions Java interactives avec Aspose.Cells. Nous vous montrerons également comment ajouter des info-bulles et un hyperlien de drill‑down simple afin que votre audience puisse explorer les données en profondeur.

## Réponses rapides
- **Quelle bibliothèque est utilisée ?** Aspose.Cells for Java  
- **Puis‑je changer le type de graphique ?** Oui – il suffit de modifier l’énumération `ChartType` lors de la création du graphique.  
- **Comment ajouter des info‑bulles à un graphique ?** Utilisez l’API des étiquettes de données (`setHasDataLabels(true)`) et activez l’affichage de la valeur.  
- **Le drill‑down est‑il pris en charge ?** Vous pouvez attacher des hyperliens aux points de données pour un comportement de drill‑down basique.  
- **Prérequis ?** IDE Java, JAR Aspose.Cells, et un fichier Excel contenant des données d’exemple.

## Prérequis

Avant de commencer, assurez‑vous de disposer de :

- Environnement de développement Java (JDK 8+ recommandé)  
- Bibliothèque Aspose.Cells for Java (téléchargez‑la [ici](https://releases.aspose.com/cells/java/))  
- Un classeur d’exemple (`data.xlsx`) contenant les données que vous souhaitez visualiser  

## Étape 1 : Configuration de votre projet Java

1. Créez un nouveau projet Java dans votre IDE préféré (IntelliJ IDEA, Eclipse, etc.).  
2. Ajoutez le JAR Aspose.Cells à votre chemin de construction ou à vos dépendances Maven/Gradle.

## Étape 2 : Chargement des données

Pour travailler avec des graphiques, vous devez d’abord charger un classeur en mémoire.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Étape 3 : Création d’un graphique (et changement de son type)

Vous pouvez choisir n’importe quel type de graphique qui correspond à votre analyse. Ci‑dessous, nous créons un **graphique en colonnes**, mais vous pouvez facilement passer à un graphique en ligne, en secteur ou en barres en modifiant l’énumération `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Astuce :** Pour **changer le type de graphique Excel**, remplacez `ChartType.COLUMN` par `ChartType.LINE`, `ChartType.PIE`, etc.

## Étape 4 : Ajout d’interactivité

### 4.1. Ajout d’info‑bulles (Add Tooltips to Chart)

Les info‑bulles apparaissent lorsque l’utilisateur survole un point de données. Le code suivant active les étiquettes de données et affiche la valeur comme info‑bulle.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Ajout d’étiquettes de données – **add data labels to excel chart**

Les étiquettes de données offrent un repère visuel permanent directement sur le graphique. Vous pouvez les afficher sous forme de bulles d’appel pour une meilleure lisibilité.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **Pourquoi ajouter des étiquettes de données ?** Les placer directement sur le graphique élimine le besoin pour les utilisateurs de survoler ou deviner les valeurs, améliorant ainsi la clarté du rapport.

### 4.3. Implémentation du drill‑down (hyperlien sur un point de données)

Une façon simple d’ajouter la capacité de drill‑down consiste à attacher un hyperlien à un point spécifique. Un clic sur le point ouvre une page Web contenant des informations détaillées.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Étape 5 : Enregistrement du classeur

Après avoir configuré le graphique, enregistrez le classeur afin que les fonctionnalités interactives soient conservées dans le fichier de sortie.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problèmes courants & solutions

| Problème | Solution |
|----------|----------|
| **Les info‑bulles ne s’affichent pas** | Assurez‑vous d’appeler `setHasDataLabels(true)` avant de configurer `setShowValue(true)`. |
| **L’hyperlien n’est pas cliquable** | Vérifiez que le format de sortie prend en charge les hyperliens (par ex., XLSX, pas CSV). |
| **Le type de graphique ne change pas** | Revérifiez que vous avez bien modifié la bonne énumération `ChartType` lors de l’ajout du graphique. |

## Foire aux questions

**Q : Comment changer le type de graphique après sa création ?**  
R : Vous devez créer un nouveau graphique avec le `ChartType` souhaité. Aspose.Cells ne propose pas de conversion de type en‑place, il faut donc supprimer l’ancien graphique et en ajouter un nouveau.

**Q : Puis‑je personnaliser l’apparence des info‑bulles ?**  
R : Oui. Utilisez les propriétés de `DataLabel` telles que `setFontSize`, `setFontColor` et `setBackgroundColor` pour styliser le texte de l’info‑bulle.

**Q : Comment gérer les interactions utilisateur dans une application Web ?**  
R : Exportez le classeur au format HTML ou XLSX et utilisez JavaScript côté client pour capturer les événements de clic sur les éléments du graphique.

**Q : Où trouver plus d’exemples et de documentation ?**  
R : Consultez la [Référence API Aspose.Cells Java](https://reference.aspose.com/cells/java/) pour obtenir la liste complète des classes et méthodes liées aux graphiques.

## Conclusion

Vous savez maintenant comment **ajouter des étiquettes de données à un graphique Excel**, **changer le type de graphique Excel**, **créer des solutions Java de graphiques interactifs**, et les enrichir avec des info‑bulles, des étiquettes de données et des hyperliens de drill‑down grâce à Aspose.Cells for Java. Ces améliorations rendent vos rapports Excel beaucoup plus engageants et instructifs pour les utilisateurs finaux.

---

**Dernière mise à jour :** 2026-02-09  
**Testé avec :** Aspose.Cells for Java 24.12  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}