---
"date": "2025-04-08"
"description": "Apprenez à créer et personnaliser des graphiques à secteurs avec Aspose.Cells pour Java. Un guide étape par étape avec des exemples de code pour les développeurs."
"title": "Maîtriser Aspose.Cells &#58; Créer et personnaliser des graphiques à secteurs en Java"
"url": "/fr/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Maîtriser Aspose.Cells : créer et personnaliser des graphiques à secteurs en Java

## Introduction
Créer des graphiques attrayants est une exigence courante pour la visualisation de données dans Excel. Qu'il s'agisse de présenter des informations démographiques ou d'analyser les tendances du marché, les graphiques à secteurs offrent un moyen clair de représenter des données proportionnelles. Cependant, la configuration de ces graphiques par programmation peut s'avérer complexe. Ce tutoriel vous guide dans la création et la personnalisation d'un graphique à secteurs Aspose.Cells avec Java, simplifiant ainsi le processus pour les développeurs.

**Ce que vous apprendrez :**
- Configurez votre environnement avec Aspose.Cells pour Java.
- Créez un nouveau classeur et accédez aux cellules de la feuille de calcul.
- Remplissez les données dans des cellules spécifiques pour préparer la création du graphique.
- Générez un graphique à secteurs à partir de ces données.
- Personnalisez l’apparence de votre graphique à secteurs, y compris les couleurs, les titres et les légendes.

Avant de vous lancer, assurez-vous d'avoir quelques notions de programmation Java et de gestion des dépendances Maven ou Gradle. Configurez notre environnement !

## Prérequis
Pour suivre ce tutoriel, vous aurez besoin de :
- **Kit de développement Java (JDK)**:Version 8 ou supérieure.
- **Environnement de développement intégré (IDE)**:Comme IntelliJ IDEA ou Eclipse.
- **Gestion des dépendances**:Utilisez Maven ou Gradle pour gérer vos dépendances.

### Bibliothèques et dépendances requises
Assurez-vous d'inclure Aspose.Cells pour Java dans votre projet en utilisant Maven ou Gradle.

**Maven**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Étapes d'acquisition de licence
Aspose.Cells pour Java est une bibliothèque commerciale, mais vous pouvez commencer par un essai gratuit ou demander une licence temporaire. Visitez le [page d'achat](https://purchase.aspose.com/buy) pour explorer les options de licence.

## Configuration d'Aspose.Cells pour Java
Tout d'abord, assurez-vous que l'environnement de votre projet inclut les bibliothèques nécessaires en les ajoutant via Maven ou Gradle, comme indiqué ci-dessus. Une fois incluses, vous pouvez initialiser Aspose.Cells :

```java
import com.aspose.cells.Workbook;

// Initialiser une nouvelle instance de classeur
Workbook workbook = new Workbook();
```

## Guide de mise en œuvre

### Créer et configurer un classeur
La création d’un classeur est la première étape au cours de laquelle vous configurerez vos données.

#### Importer des bibliothèques
Assurez-vous que ces importations sont incluses en haut de votre fichier :

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Étape 1 : Créer une instance de classeur
```java
// Crée une instance de classeur vide avec laquelle travailler.
Workbook workbook = new Workbook();
```
Cette étape initialise votre fichier Excel par programmation, vous permettant de le manipuler à l'aide des fonctionnalités d'Aspose.Cells.

### Accéder ou modifier les cellules de la feuille de calcul
Ensuite, remplissez les données dans les cellules de la feuille de calcul qui seront utilisées pour le graphique à secteurs.

#### Étape 2 : Accéder à une feuille de calcul et à ses cellules
```java
// Accédez à la première feuille de calcul du classeur.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Placez les valeurs d’échantillon utilisées pour un graphique à secteurs dans des cellules spécifiques.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Placez les valeurs de pourcentage d’un graphique à secteurs dans des cellules spécifiques.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
Ici, vous remplissez la feuille de calcul avec des données qui représenteront différents segments d’un graphique à secteurs.

### Créer un graphique à secteurs

#### Étape 3 : Ajouter un graphique à secteurs à la feuille de calcul
```java
// Créez un graphique à secteurs dans la feuille de calcul.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
Cette étape ajoute un nouveau graphique à secteurs à votre feuille de calcul à des positions et des dimensions spécifiées.

### Configurer les séries et les données du graphique à secteurs

#### Étape 4 : Définir la série du graphique
```java
// Configurez la plage de données de la série pour le graphique.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Liez le titre du graphique à secteurs à une cellule contenant le texte du titre.
pie.getTitle().setLinkedSource("D2");
```
Ce code lie votre plage de données et configure la série pour le graphique à secteurs.

### Configurer la légende du graphique et l'apparence du titre

#### Étape 5 : Personnaliser la légende et le titre du graphique
```java
// Définissez la position de la légende en bas du graphique.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Définir les propriétés de police pour le titre du graphique.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
La personnalisation de l’apparence améliore la lisibilité et l’attrait visuel.

### Personnaliser les couleurs des séries de graphiques

#### Étape 6 : Modifier les couleurs des segments du graphique à secteurs
```java
import com.aspose.cells.Color;

// Accédez et personnalisez les couleurs des segments individuels du graphique à secteurs.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
Ces paramètres personnalisent votre graphique pour l'adapter à des schémas de couleurs spécifiques.

### Ajuster automatiquement les colonnes et enregistrer le classeur

#### Étape 7 : Ajustez la largeur des colonnes et enregistrez le fichier
```java
// Ajuster automatiquement toutes les colonnes.
worksheet.autoFitColumns();

// Définissez le chemin d'accès réservé au répertoire de sortie pour enregistrer le classeur.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Enregistrez le classeur modifié dans un fichier Excel dans le répertoire spécifié.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
Enfin, ajustez automatiquement les colonnes et enregistrez votre classeur.

## Applications pratiques
1. **Analyse démographique**:Utilisez des graphiques à secteurs pour afficher la répartition de la population dans différents pays ou régions.
2. **Rapports sur les parts de marché**:Illustrer la part de marché de différentes entreprises dans un secteur.
3. **Allocation budgétaire**:Visualisez comment les budgets sont répartis entre les différents départements d’une organisation.

Ces applications démontrent la polyvalence et l’utilité d’Aspose.Cells dans des scénarios réels.

## Considérations relatives aux performances
Pour optimiser les performances lors de l'utilisation d'Aspose.Cells :
- Minimisez l’utilisation de la mémoire en supprimant les objets dont vous n’avez plus besoin.
- Utilisez des structures de données efficaces pour traiter de grands ensembles de données.
- Profilez votre application pour identifier les goulots d’étranglement.

Le respect des meilleures pratiques garantit des applications fluides et réactives.

## Conclusion
Ce tutoriel vous a présenté les étapes de création et de personnalisation d'un graphique à secteurs avec Aspose.Cells en Java. Grâce à ces connaissances, vous pouvez désormais appliquer ces techniques à diverses tâches de visualisation de données dans vos projets. Pour approfondir votre exploration, découvrez les autres types de graphiques et les options de personnalisation avancées disponibles avec Aspose.Cells.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}