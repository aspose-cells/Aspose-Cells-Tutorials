---
"date": "2025-04-07"
"description": "Apprenez à créer et personnaliser des graphiques à secteurs dans Excel avec Aspose.Cells pour Java. Suivez ce guide étape par étape pour améliorer vos compétences en visualisation de données."
"title": "Créer des graphiques à secteurs dans Excel à l'aide d'Aspose.Cells pour Java - Un guide complet"
"url": "/fr/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Créer des graphiques à secteurs dans Excel avec Aspose.Cells pour Java
## Introduction
Créer des graphiques à secteurs attrayants et informatifs dans Excel peut transformer des données brutes en informations précieuses, vous permettant ainsi de prendre rapidement des décisions éclairées. Vous rencontrez des difficultés avec les fonctionnalités intégrées de Microsoft Excel ou recherchez une solution évolutive qui s'intègre parfaitement à vos applications Java ? Aspose.Cells pour Java est là pour vous aider.

Ce tutoriel vous guide dans la création et la personnalisation de graphiques à secteurs dans Excel avec Aspose.Cells pour Java. Découvrez comment ajouter efficacement des données, configurer des éléments de graphique et finaliser votre classeur, le tout avec simplicité et précision.

**Ce que vous apprendrez :**
- Configuration et utilisation d'Aspose.Cells pour Java
- Créer un nouveau classeur et le remplir avec des exemples de données
- Ajout et personnalisation de graphiques à secteurs dans une feuille de calcul Excel
- Meilleures pratiques pour la configuration et l'optimisation des graphiques

Commençons par aborder les prérequis.
## Prérequis
Avant de commencer, assurez-vous de disposer des éléments suivants :
### Bibliothèques, versions et dépendances requises
Assurez-vous qu'Aspose.Cells pour Java version 25.3 ou ultérieure est inclus dans votre projet à l'aide de Maven ou Gradle.
**Expert :**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```
**Gradle :**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```
### Configuration requise pour l'environnement
- Un kit de développement Java (JDK) installé sur votre système.
- Un environnement de développement intégré (IDE) tel qu'IntelliJ IDEA, Eclipse ou NetBeans.
### Prérequis en matière de connaissances
Une compréhension de base de la programmation Java et une familiarité avec les structures de fichiers Excel seront bénéfiques.
## Configuration d'Aspose.Cells pour Java
Aspose.Cells est une bibliothèque puissante qui permet aux développeurs de créer, modifier et afficher des feuilles de calcul Excel dans des applications Java. Voici comment la configurer :
1. **Installation**: Ajoutez la dépendance Maven ou Gradle comme indiqué ci-dessus.
2. **Acquisition de licence**:
   - Obtenez une licence d'essai gratuite pour les tests initiaux auprès de [Essai gratuit d'Aspose](https://releases.aspose.com/cells/java/).
   - Demandez une licence temporaire pour tester toutes les fonctionnalités sans limitations via [Permis temporaire](https://purchase.aspose.com/temporary-license/).
3. **Initialisation de base**: Commencez par créer une instance du `Workbook` classe, qui représente votre fichier Excel.
```java
import com.aspose.cells.Workbook;
// Créer et initialiser un nouveau classeur
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook();
```
## Guide de mise en œuvre
Maintenant, implémentons chaque fonctionnalité étape par étape pour créer un classeur Excel avec un graphique à secteurs.
### 1. Création et initialisation du classeur
**Aperçu**:Nous commençons par initialiser notre `Workbook` objet et accéder à sa première feuille de calcul où nous ajouterons des données et des graphiques.
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorksheetCollection;

String dataDir = "YOUR_DATA_DIRECTORY";
// Créer une nouvelle instance de classeur
Workbook workbook = new Workbook();
// Accéder à la première feuille de calcul du classeur
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
```
### 2. Ajout d'échantillons de données aux cellules
**Aperçu**: Remplissez votre feuille de calcul avec des exemples de données qui seront représentées dans le graphique à secteurs.
```java
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

Cells cells = sheet.getCells();
// Ajouter les noms de pays dans la colonne A
Cell cell = cells.get("A1");
cell.setValue("Italy");
cell = cells.get("A2");
cell.setValue("Germany");
// Continuer pour les autres pays...
// Ajoutez les données de vente correspondantes dans la colonne B
cell = cells.get("B1");
cell.setValue(10000);
cell = cells.get("B2");
cell.setValue(20000);
// Continuez pour le reste des données...
```
### 3. Ajout d'un graphique à secteurs à la feuille de calcul
**Aperçu**:Insérez un graphique à secteurs dans la feuille de calcul à l’aide de plages de données prédéfinies.
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;

ChartCollection charts = sheet.getCharts();
// Ajouter un graphique à secteurs à l'emplacement et à la taille spécifiés
int chartIndex = charts.add(ChartType.PIE, 15, 4, 40, 15);
Chart chart = charts.get(chartIndex);
```
### 4. Configuration de la série de graphiques
**Aperçu**: Définissez la plage de données pour les données de vente et de catégorie (noms de pays) pour garantir que le graphique à secteurs représente avec précision votre ensemble de données.
```java
import com.aspose.cells.SeriesCollection;

SeriesCollection serieses = chart.getNSeries();
// Définir les données de vente comme source de données du graphique
serieses.add("B1:B8", true);
// Spécifier les données de catégorie (noms de pays)
serieses.setCategoryData("A1:A8");
// Activer des couleurs variées pour chaque tranche de tarte
serieses.setColorVaried(true);

// Afficher un tableau de données sur le graphique pour plus de clarté
chart.setShowDataTable(true);
```
### 5. Définition du titre et du style du graphique
**Aperçu**:Personnalisez le titre de votre graphique pour améliorer la lisibilité et la présentation.
```java
import com.aspose.cells.Color;

// Définissez le titre du graphique avec les options de style
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```
### 6. Configuration des étiquettes de données pour les séries de graphiques
**Aperçu**: Ajoutez des étiquettes de données à chaque tranche de graphique, fournissant une répartition claire des valeurs.
```java
import com.aspose.cells.DataLabels;
import com.aspose.cells.LabelPositionType;

for (int i = 0; i < serieses.getCount(); i++) {
    DataLabels datalabels = serieses.get(i).getDataLabels();
    // Positionnez les étiquettes à l'intérieur de la base de chaque part de tarte
    datalabels.setPosition(LabelPositionType.INSIDE_BASE);
    // Configurer les options d'affichage des étiquettes
    datalabels.setShowCategoryName(true);
    datalabels.setShowValue(true);
    datalabels.setShowPercentage(false);
    datalabels.setShowLegendKey(true);
}
```
### 7. Enregistrer le classeur
**Aperçu**:Finalisez votre fichier Excel avec toutes les données et tous les graphiques enregistrés sur le disque.
```java
import com.aspose.cells.SaveFormat;

String outDir = "YOUR_OUTPUT_DIRECTORY";
// Enregistrer le classeur dans un fichier Excel
workbook.save(outDir + "/HTCPChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
## Applications pratiques
- **Analyse commerciale**:Utilisez des graphiques à secteurs dans les rapports de vente pour visualiser la part de marché ou la répartition des revenus entre les régions.
- **Outils pédagogiques**: Créez des modules d’apprentissage interactifs affichant des distributions de données statistiques.
- **Gestion de projet**:Représenter visuellement l’allocation des ressources et l’utilisation du budget aux parties prenantes.
## Considérations relatives aux performances
Pour optimiser les performances :
- Réduisez l’utilisation de la mémoire en gérant efficacement la taille du classeur.
- Utilisez les fonctionnalités d'Aspose.Cells telles que la diffusion de fichiers volumineux si vous traitez de vastes ensembles de données.
- Suivez les meilleures pratiques de Java en matière de gestion de la mémoire, en vous assurant que les ressources sont correctement libérées après utilisation.
## Conclusion
En suivant ce guide, vous avez appris à créer, configurer et personnaliser des graphiques à secteurs dans Excel avec Aspose.Cells pour Java. Cette puissante bibliothèque permet aux développeurs d'intégrer facilement des fonctionnalités avancées de tableur à leurs applications Java.
Pour une exploration plus approfondie, envisagez d'explorer d'autres types de graphiques ou d'étendre vos capacités de manipulation de données avec des fonctionnalités supplémentaires offertes par Aspose.Cells.
## Section FAQ
1. **Puis-je utiliser Aspose.Cells gratuitement ?**
   - Oui, un essai gratuit est disponible. Pour accéder à toutes les fonctionnalités sans limitation, vous pouvez demander une licence temporaire.
2. **Est-il possible de créer d’autres types de graphiques à l’aide d’Aspose.Cells ?**
   - Absolument ! Vous pouvez créer des graphiques à barres, des graphiques linéaires et bien plus encore en ajustant `ChartType`.
3. **Comment gérer de grands ensembles de données dans Excel avec Java ?**
   - Utilisez des techniques de chargement de données efficaces et envisagez le streaming pour les fichiers très volumineux.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}