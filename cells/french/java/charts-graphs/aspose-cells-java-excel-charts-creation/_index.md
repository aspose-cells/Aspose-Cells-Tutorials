---
date: '2026-04-08'
description: Apprenez à créer un graphique en courbes avec des repères à l'aide d'Aspose.Cells
  pour Java, à ajouter le graphique à la feuille de calcul et à personnaliser les
  graphiques Excel pour les rapports automatisés.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Créer un graphique linéaire avec des marqueurs à l'aide d'Aspose.Cells pour
  Java
url: /fr/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Créer et styliser des graphiques Excel avec Aspose.Cells Java

## Introduction

Dans le monde actuel axé sur les données, un **line chart with markers** est l'une des méthodes les plus efficaces pour visualiser les tendances et les valeurs aberrantes. Que vous créiez des rapports automatisés ou un tableau de bord mis à jour quotidiennement, pouvoir ajouter de façon programmatique un line chart with markers à une feuille de calcul évite d'innombrables étapes manuelles. Ce tutoriel vous guide à travers l'utilisation d'Aspose.Cells pour Java afin de créer, styliser et exporter de tels graphiques, afin que vous puissiez vous concentrer sur les insights plutôt que sur la manipulation fastidieuse d'Excel.

**Ce que vous apprendrez**
- Initialisation d'un classeur et remplissage avec des données en utilisant Aspose.Cells.  
- **Comment ajouter un line chart with markers à une feuille de calcul** et configurer son apparence.  
- Personnalisation des couleurs des séries, des marqueurs et d'autres options de style.  
- Enregistrement du classeur au format Excel incluant votre graphique stylisé.

## Réponses rapides
- **Quelle est la classe principale pour commencer ?** `Workbook` initialise un nouveau fichier Excel.  
- **Quel type de graphique crée un line chart with markers ?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **Comment définir des couleurs personnalisées pour les points de série ?** Utilisez `chart.getNSeries().setColorVaried(true)` et définissez les couleurs de la zone des marqueurs.  
- **Ai-je besoin d'une licence pour la pleine fonctionnalité ?** Oui, une licence Aspose.Cells payante ou temporaire supprime les limites d'évaluation.  
- **Puis-je exporter le résultat au format XLSX ?** Absolument — `workbook.save("StyledChart.xlsx")` crée un fichier XLSX.

## Prérequis

Avant de créer et de styliser des graphiques avec Aspose.Cells pour Java, assurez‑vous d'avoir la configuration suivante :

### Bibliothèques requises
Incluez Aspose.Cells comme dépendance dans votre projet. Voici les instructions pour les utilisateurs de Maven et de Gradle :

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Exigences de configuration de l'environnement
- Kit de développement Java (JDK) installé sur votre système.  
- Un environnement de développement intégré (IDE) tel qu'IntelliJ IDEA ou Eclipse pour coder et tester.

### Prérequis de connaissances
Une compréhension de base de la programmation Java est requise, ainsi qu'une familiarité avec les classeurs Excel et les concepts de création de graphiques.

### Acquisition de licence
Aspose.Cells est un produit commercial qui nécessite une licence pour la pleine fonctionnalité. Vous pouvez obtenir un essai gratuit pour évaluer ses fonctionnalités, demander une licence temporaire pour des tests prolongés, ou acheter le produit pour une utilisation à long terme.

- **Essai gratuit :** [Télécharger l'essai gratuit](https://releases.aspose.com/cells/java/)  
- **Licence temporaire :** [Demander une licence temporaire](https://purchase.aspose.com/temporary-license/)  
- **Achat :** [Acheter Aspose.Cells](https://purchase.aspose.com/buy)

## Configuration d'Aspose.Cells pour Java

Une fois les dépendances nécessaires installées, configurez votre environnement de développement pour utiliser Aspose.Cells. Commencez par importer la bibliothèque et initialiser un objet `Workbook` dans votre application Java :

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Guide de mise en œuvre

Dans cette section, nous décomposerons la mise en œuvre en fonctionnalités distinctes : Initialisation du classeur et remplissage des données, Création et configuration du graphique, Personnalisation des séries et Enregistrement du classeur.

### Fonctionnalité 1 : Initialisation du classeur et remplissage des données

**Aperçu :** Cette fonctionnalité se concentre sur la création d'un nouveau classeur, l'accès à sa première feuille de calcul et le remplissage avec des données pour la création du graphique.

#### Étape 1 : Initialiser le classeur
Commencez par instancier un objet `Workbook` :

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Étape 2 : Définir les titres de colonnes et remplir les données
Définissez les en‑têtes de colonnes et remplissez les lignes avec des données d'exemple :

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Fonctionnalité 2 : Création et configuration du graphique

**Aperçu :** Cette fonctionnalité montre comment ajouter un graphique à la feuille de calcul du classeur, définir son style et configurer les propriétés de base.

#### Étape 3 : Ajouter un graphique à la feuille de calcul
Ajoutez un line chart with data markers :

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Fonctionnalité 3 : Configuration et personnalisation des séries

**Aperçu :** Améliorez l'aspect visuel de vos graphiques en personnalisant les paramètres des séries, comme les couleurs variées et les styles de marqueurs.

#### Étape 4 : Personnaliser les paramètres des séries
Configurez les données des séries, appliquez un formatage personnalisé et ajustez les marqueurs :

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Fonctionnalité 4 : Enregistrement du classeur

**Aperçu :** Enfin, enregistrez le classeur pour conserver vos modifications et vous assurer que le graphique est inclus dans le fichier Excel.

#### Étape 5 : Enregistrer le classeur
Enregistrez votre classeur avec les graphiques nouvellement créés :

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### Problèmes courants et dépannage
- **Le graphique apparaît vide :** Vérifiez que les plages de cellules utilisées dans `setXValues` et `setValues` font correctement référence aux cellules remplies.  
- **Les couleurs ne sont pas appliquées :** Assurez‑vous que `chart.getNSeries().setColorVaried(true)` est appelé avant de personnaliser les séries individuelles.  
- **Erreurs de licence :** Une licence d'essai peut limiter le nombre de graphiques ; installez une licence complète pour supprimer les restrictions.

## Questions fréquentes

**Q : Puis‑je créer d'autres types de graphiques (par ex., bar, pie) avec Aspose.Cells ?**  
R : Oui, Aspose.Cells prend en charge une large gamme de types de graphiques ; il suffit de remplacer `ChartType.LINE_WITH_DATA_MARKERS` par la valeur d'énumération souhaitée.

**Q : Dois‑je fermer le classeur ou libérer les ressources ?**  
R : La classe `Workbook` gère les ressources automatiquement, mais vous pouvez appeler `workbook.dispose()` dans les applications à long terme pour libérer la mémoire.

**Q : Est‑il possible d'ajouter plusieurs graphiques à la même feuille de calcul ?**  
R : Absolument — appelez `worksheet.getCharts().add(...)` pour chaque graphique que vous souhaitez insérer.

**Q : Comment exporter le fichier au format Excel plus ancien (XLS) ?**  
R : Utilisez `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`.

**Q : Le graphique conservera‑t‑il son style lorsqu'il sera ouvert dans Microsoft Excel ?**  
R : Oui, Aspose.Cells écrit des objets graphiques Excel natifs, ainsi tous les styles, couleurs et marqueurs apparaissent exactement comme définis.

---

**Dernière mise à jour :** 2026-04-08  
**Testé avec :** Aspose.Cells 25.3 for Java  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}