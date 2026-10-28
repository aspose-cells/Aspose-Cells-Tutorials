---
category: general
date: 2026-07-23
description: Créez un nouveau classeur en Java et apprenez à copier un tableau croisé
  dynamique, copier une plage Excel et exporter le tableau croisé dynamique avec Aspose.Cells
  en quelques minutes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: fr
lastmod: 2026-07-23
og_description: Créez un nouveau classeur en Java et copiez instantanément le tableau
  croisé dynamique, copiez une plage Excel, puis exportez le tableau croisé dynamique
  à l’aide d’Aspose.Cells. Suivez ce tutoriel complet.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: Créer un nouveau classeur en Java – Copier le tableau croisé dynamique étape
  par étape
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Créer un nouveau classeur en Java – Guide complet pour copier un tableau croisé
  dynamique
url: /fr/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un nouveau classeur en Java – Guide complet pour copier un tableau croisé dynamique

Vous êtes‑vous déjà demandé comment **create new workbook** en Java tout en conservant un tableau croisé dynamique complexe ? Vous n'êtes pas le seul à vous creuser la tête à ce sujet. Dans de nombreuses applications de reporting, vous devez déplacer un tableau croisé dynamique d'un fichier source vers un nouveau classeur, peut‑être pour l'envoyer à un client ou pour effectuer d'autres calculs. La bonne nouvelle ? En quelques lignes, vous pouvez faire exactement cela—sans aucun copier‑coller manuel.

Dans ce tutoriel, nous parcourrons l'ensemble du processus : charger le fichier source, définir la plage qui contient le tableau croisé dynamique, **copying the Excel range**, créer un **new workbook**, et enfin **exporting the pivot table** vers un nouveau fichier. À la fin, vous disposerez d'un programme Java autonome et exécutable qui répond à la question « **how to copy pivot** » sans aucune conjecture.

## Prérequis

- Java 17 ou ultérieur (le code fonctionne avec n'importe quel JDK récent)
- Bibliothèque Aspose.Cells for Java (version d'essai gratuite ou version sous licence)
- Un exemple `source.xlsx` contenant un tableau croisé dynamique dans la plage `A1:G20`
- Un IDE ou un outil de construction (Maven/Gradle) pour gérer le JAR Aspose.Cells

Vous les avez ? Super—commençons.

## Étape 1 : Configurer le projet et importer Aspose.Cells

Tout d'abord, vous devez ajouter Aspose.Cells à votre projet. Si vous utilisez Maven, insérez cette dépendance dans votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

Si vous préférez Gradle, l'équivalent est :

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

Une fois la bibliothèque sur le classpath, importez les classes dont vous aurez besoin :

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Astuce :** Aspose.Cells est une bibliothèque commerciale, mais elle propose une évaluation pleinement fonctionnelle de 30 jours qui ajoute un filigrane sur le résultat—parfait pour tester.

## Étape 2 : Charger le classeur source

Nous allons maintenant **create new workbook** des objets, mais d'abord nous avons besoin du source qui contient le tableau croisé dynamique. Cette étape est la base de toute opération **copy excel range** car l'objet plage sait exactement quelles cellules (y compris le cache du tableau croisé dynamique) transférer.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Pourquoi ne pas simplement lire la plage directement ? Parce que les métadonnées du tableau croisé dynamique résident dans le cache de pivot de la feuille de calcul, et Aspose.Cells les regroupe automatiquement lors de la copie de la plage.

## Étape 3 : Définir la plage qui contient le tableau croisé dynamique

Dans de nombreux fichiers réels, le tableau croisé dynamique occupe un bloc rectangulaire. Pour cet exemple, nous supposerons qu'il se trouve dans `A1:G20`. Vous pouvez bien sûr ajuster l'adresse pour correspondre à votre disposition réelle.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

Si vous n'êtes pas sûr de l'adresse exacte, vous pouvez utiliser `sourceSheet.getCells().getMaxDataRow()` et `getMaxDataColumn()` pour calculer dynamiquement les limites. C'est une astuce pratique lorsque la taille du tableau croisé dynamique change avec le temps.

## Étape 4 : **Create New Workbook** et feuille de destination

Voici le moment où nous **create new workbook** réellement qui recevra le contenu copié. Considérez cela comme la toile vierge sur laquelle vous collerez le tableau croisé dynamique.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Pourquoi commencer avec un classeur vide ? Cela garantit qu'aucun style caché ou tableau croisé dynamique précédent n'interfère avec la copie, vous offrant un résultat propre prêt pour **export pivot table**.

## Étape 5 : Copier le tableau croisé dynamique (et sa plage sous‑jacente)

Voici le cœur du tutoriel : **copy pivot table**. Aspose.Cells traite la copie d'une plage comme une copie profonde, ce qui signifie que le cache du tableau croisé dynamique se déplace avec les cellules. C’est pourquoi cette ligne unique effectue le travail lourd.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

Si vous vous êtes déjà demandé **how to copy pivot** sans perdre sa fonctionnalité, voici la réponse. La feuille de destination contient désormais un tableau croisé dynamique entièrement fonctionnel que vous pouvez actualiser, modifier ou simplement exporter.

### Cas particulier : Conserver les paramètres d'actualisation

Parfois, le tableau croisé dynamique source est configuré pour s'actualiser à l'ouverture. Pour conserver ce comportement, vous pouvez copier explicitement les options du tableau croisé dynamique :

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

## Étape 6 : Enregistrer le classeur de destination – **Export Pivot Table**

Enfin, nous **export pivot table** en enregistrant le nouveau classeur sur le disque. Vous pouvez choisir n'importe quel format supporté par Aspose : XLSX, XLS, CSV, PDF, etc. Pour ce guide, nous resterons sur le format XLSX.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

Si vous devez envoyer le fichier via un service web, vous pouvez l'écrire dans un `ByteArrayOutputStream` au lieu d'un chemin de fichier—Aspose rend cela trivial.

## Exemple complet fonctionnel

En rassemblant le tout, voici un programme complet, prêt à être exécuté. N'hésitez pas à le copier, le coller et l'exécuter dans votre IDE.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### Sortie attendue

Lorsque vous exécutez le programme, la console affiche :

```
Pivot table copied successfully!
```

## Questions fréquentes & dépannage

- **What if the source pivot spans more than one worksheet?**  
  Vous devrez copier chaque plage pertinente séparément, puis recréer le tableau croisé dynamique sur la feuille de destination en utilisant les API `PivotTable`.

- **Can I copy only the pivot layout without the data?**  
  Définissez `sourceRange.setCopyDataOnly(false)` avant la copie. Cela indique à Aspose de conserver le cache mais pas les données sources sous‑jacentes.

- **Is there a way to copy the pivot to a CSV file?**  
  Le CSV ne prend pas en charge les tableaux croisés dynamiques, mais vous pouvez exporter le *résultat* du tableau croisé dynamique en appelant `pivotTable.calculate()` puis en enregistrant la feuille au format CSV.

- **Why does the copied pivot lose its formatting?**  
  Le formatage réside dans la collection de styles. Après la copie, vous pouvez appeler `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())` pour transférer les styles.

## Conclusion

Nous venons de vous montrer comment **create new workbook** en Java, **copy pivot table**, et **export pivot table**—le tout avec un exemple de code propre et reproductible. En définissant la **copy excel range** exacte, en tirant parti des sémantiques de copie profonde d'Aspose.Cells, et en conservant les paramètres optionnels, vous pouvez automatiser pratiquement toute tâche de migration de tableau croisé dynamique.

Prêt pour l'étape suivante ? Essayez de changer le format de sortie en PDF, ou parcourez plusieurs fichiers source pour traiter par lots des dizaines de tableaux croisés dynamiques. Le même schéma s'applique—il suffit d'ajuster les chemins de fichiers et les adresses de plage.

Si vous rencontrez un problème, laissez un commentaire ci‑dessous ou consultez la documentation d'Aspose.Cells pour la manipulation avancée des tableaux croisés dynamiques. Bon codage, et profitez du temps gagné en automatisant ces fastidieuses tâches de copier‑coller !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}