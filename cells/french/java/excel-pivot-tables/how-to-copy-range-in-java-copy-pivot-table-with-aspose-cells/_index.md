---
category: general
date: 2026-06-30
description: Comment copier une plage en Java avec Aspose.Cells – dupliquer une plage
  Excel, copier un tableau croisé dynamique et charger efficacement un classeur Excel.
draft: false
keywords:
- how to copy range
- copy pivot table
- pivot table to sheet
- duplicate excel range
- load excel workbook
language: fr
og_description: Comment copier une plage en Java avec Aspose.Cells. Apprenez à dupliquer
  une plage Excel, copier un tableau croisé dynamique et charger un classeur Excel
  en quelques minutes.
og_title: Comment copier une plage en Java – Guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  headline: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  name: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  steps:
  - name: Expected Output
    text: 'When you execute `CopyPivotDemo`, the console prints:'
  - name: What if the source workbook has multiple worksheets?
    text: You can loop through `sourceWorkbook.getWorksheets()` and copy each relevant
      range. Just be careful to maintain the same sheet names in the destination if
      you need to preserve references.
  - name: Does the copied pivot retain its data source?
    text: Yes. Aspose.Cells copies the pivot cache along with the range, so the destination
      workbook still points to the original data source within the same file. If you
      later move the data to a different sheet, you may need to refresh the pivot
      manually.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot’s data source is an external file, you’ll have to embed that
      data into the destination workbook first (e.g., copy the source data range)
      before copying the pivot. Otherwise the pivot will show “#REF!” errors.
  - name: Can I copy the pivot without the surrounding data?
    text: Absolutely. Just adjust `pivotRange` to cover only the pivot’s cells (usually
      the top‑left corner plus the data area). You can also use `sourceSheet.getPivotTables().get(0).getPivotTableArea()`
      to retrieve the exact range programmatically.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Comment copier une plage en Java – Copier un tableau croisé dynamique avec
  Aspose.Cells
url: /fr/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier une plage en Java – Copier un tableau croisé dynamique avec Aspose.Cells

Vous vous êtes déjà demandé **comment copier une plage** d'un classeur Excel à un autre sans perdre l'intégrité du tableau croisé dynamique ? Vous n'êtes pas le seul. Dans de nombreux pipelines de reporting, le besoin de *dupliquer une plage Excel* tout en préservant la logique du tableau croisé dynamique est un casse‑tête quotidien. Heureusement, Aspose.Cells for Java rend cela très simple, et dans ce tutoriel nous parcourrons un exemple complet et exécutable qui vous montre également comment **charger un classeur Excel**, copier un tableau croisé dynamique et enregistrer le résultat.

À la fin de ce guide, vous disposerez d’un programme Java autonome qui :

* Charge un classeur existant (`load excel workbook`);
* Définit les cellules exactes contenant le tableau croisé dynamique ;
* Copie ce **pivot table to sheet** dans un tout nouveau classeur ;
* Enregistre le nouveau fichier, prêt pour le traitement en aval.

Pas de scripts externes, pas d'étapes manuelles—juste du code pur.

## Ce dont vous avez besoin

Avant de plonger, assurez‑vous d’avoir :

* Java 8 ou plus récent (le code fonctionne également avec Java 11+);
* Bibliothèque Aspose.Cells for Java (vous pouvez la récupérer sur Maven Central);
* Deux fichiers Excel d'exemple – un source contenant un tableau croisé dynamique (`source.xlsx`) et un dossier de destination où vous écrirez `copy-pivot.xlsx`.

C’est tout. Aucun tour de passe‑passe d’IDE n’est requis ; n’importe quel éditeur de texte plus `javac` fera l’affaire.

## Étape 1 : Configurer le projet et importer Aspose.Cells

Tout d'abord, mettons la bibliothèque en place. Si vous utilisez Maven, ajoutez cette dépendance à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Si vous n'êtes pas sur Maven, téléchargez le JAR depuis le site Aspose et ajoutez‑le à votre classpath. Une fois cela fait, créez une nouvelle classe Java nommée `CopyPivotDemo`.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // The implementation will go here.
    }
}
```

> **Astuce :** Gardez votre dossier `src/main/java` propre et donnez à la classe un nom significatif ; cela facilite la maintenance future.

## Étape 2 : Charger le classeur source (`load excel workbook`)

Nous allons maintenant réellement **load excel workbook** qui contient le tableau croisé dynamique que nous voulons copier. Le constructeur `Workbook` prend un chemin de fichier, assurez‑vous donc que le chemin est correct.

```java
// Step 2: Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Pourquoi choisissons‑nous la première feuille de calcul ? Dans la plupart des cas simples, le tableau croisé dynamique se trouve sur la première feuille, mais vous pouvez modifier l'index ou utiliser le nom de la feuille si nécessaire. Cette flexibilité est l'une des raisons pour lesquelles Aspose.Cells brille.

## Étape 3 : Définir la plage qui contient le tableau croisé dynamique

Un tableau croisé dynamique s'étend généralement sur un bloc de cellules. Supposons qu'il occupe `A1:G20`. Vous pouvez ajuster l'adresse pour correspondre à vos données réelles.

```java
// Step 3: Define the range that includes the pivot table
Range pivotRange = sourceSheet.getCells().createRange("A1:G20");
```

Si vous n'êtes pas sûr de l'adresse exacte, ouvrez le classeur dans Excel, sélectionnez l'ensemble du tableau croisé dynamique et regardez la zone de nom. Rappelez‑vous, **duplicate excel range** fonctionne mieux lorsque vous ciblez la zone exacte — pas de lignes supplémentaires, pas de colonnes manquantes.

## Étape 4 : Créer un nouveau classeur pour la destination

Nous avons besoin d'un nouveau classeur qui recevra la plage copiée. C'est ici que nous allons **copy pivot table** vers une nouvelle feuille.

```java
// Step 4: Create a new workbook to receive the copied range
Workbook destinationWorkbook = new Workbook(); // starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

À ce stade, le classeur de destination est vide, mais Aspose.Cells ajoute automatiquement une feuille par défaut, que nous utiliserons comme cible.

## Étape 5 : Copier la plage – Le tableau croisé dynamique reste intact

Voici la ligne magique qui **copy pivot table** tout en conservant toutes ses connexions internes actives.

```java
// Step 5: Copy the range (pivot table stays intact) to the destination sheet
destinationSheet.getCells().copy(pivotRange,
        destinationSheet.getCells().createRange("A1"));
```

La méthode `copy` prend deux arguments : le `Range` source et le `Range` de destination. En commençant la destination à `A1`, nous plaçons le tableau croisé dynamique exactement où il était dans la source. Aspose.Cells copie le cache du tableau croisé dynamique sous‑jacent, de sorte que le nouveau classeur sait toujours comment actualiser le tableau.

## Étape 6 : Enregistrer le classeur résultant

Enfin, écrivez le nouveau fichier sur le disque. Vous pouvez choisir n'importe quel format supporté par Aspose (`.xlsx`, `.xls`, `.csv`, etc.). Nous resterons sur le format `.xlsx`.

```java
// Step 6: Save the resulting workbook
destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");
System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
```

Exécutez le programme, et vous devriez voir un nouveau classeur avec la même mise en page du tableau croisé dynamique. Ouvrez‑le dans Excel—si tout s’est bien passé, vous pourrez actualiser le tableau sans erreurs.

### Résultat attendu

Lorsque vous exécutez `CopyPivotDemo`, la console affiche :

```
Pivot table successfully copied to copy-pivot.xlsx
```

L'ouverture de `copy-pivot.xlsx` révèle une feuille qui ressemble exactement à la zone du tableau croisé dynamique de la source, et le **pivot table to sheet** fonctionne comme l'original.

## Exemple complet fonctionnel

Ci‑dessous se trouve la classe Java complète, prête à être exécutée, qui réunit toutes les étapes. Copiez‑collez‑la dans votre IDE, ajustez les chemins de fichiers, et lancez‑la.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook (load excel workbook)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot table
        // Adjust the address if your pivot occupies a different area
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh workbook for the destination
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot table stays intact
        destinationSheet.getCells().copy(pivotRange,
                destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the new workbook
        destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");

        System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
    }
}
```

> **Note :** Si votre tableau croisé dynamique s'étend sur plusieurs feuilles, répétez l'étape de copie pour chaque feuille concernée, ou utilisez `Workbook.copy` pour cloner des feuilles entières.

## Questions fréquentes et cas particuliers

### Et si le classeur source possède plusieurs feuilles ?

Vous pouvez parcourir `sourceWorkbook.getWorksheets()` et copier chaque plage pertinente. Veillez simplement à conserver les mêmes noms de feuilles dans la destination si vous devez préserver les références.

### Le tableau copié conserve‑t‑il sa source de données ?

Oui. Aspose.Cells copie le cache du tableau croisé dynamique avec la plage, de sorte que le classeur de destination pointe toujours vers la source de données originale dans le même fichier. Si vous déplacez plus tard les données vers une autre feuille, il pourra être nécessaire d'actualiser le tableau manuellement.

### Comment copier un tableau qui utilise une source de données externe ?

Lorsque la source de données du tableau croisé dynamique est un fichier externe, vous devez d'abord intégrer ces données dans le classeur de destination (par ex., copier la plage de données source) avant de copier le tableau. Sinon le tableau affichera des erreurs “#REF!”.

### Puis‑je copier le tableau sans les données environnantes ?

Absolument. Ajustez simplement `pivotRange` pour ne couvrir que les cellules du tableau (généralement le coin supérieur gauche plus la zone de données). Vous pouvez également utiliser `sourceSheet.getPivotTables().get(0).getPivotTableArea()` pour récupérer la plage exacte par programme.

## Conseils pour les projets réels

* **Batch processing :** Si vous devez dupliquer des dizaines de classeurs, encapsulez le code ci‑dessus dans une méthode et appelez‑la dans une boucle qui parcourt un répertoire.
* **Performance :** Pour les gros fichiers, réutilisez une seule instance `Workbook` et appelez `Workbook.calculateFormula()` uniquement après que toutes les copies soient terminées.
* **Error handling :** Entourez la logique de copie de blocs try‑catch et consignez `Exception.getMessage()` ; Aspose lance `CellsException` pour les plages invalides.

## Conclusion

Nous venons de couvrir **how to copy range** en Java avec Aspose.Cells, en vous montrant comment **duplicate excel range**, **copy pivot table**, et **load excel workbook** dans un seul programme bien structuré. Les étapes sont simples, le code est entièrement exécutable, et l'approche passe d'une démonstration à une feuille unique à des traitements batch de niveau entreprise.

Prêt pour le prochain défi ? Essayez d'exporter le tableau copié en PDF, ou de l'actualiser programmaticalement après avoir ajouté de nouvelles données. Les deux tâches s'appuient sur la même base que nous avons présentée, vous serez donc bien équipé pour les réaliser.

Des questions ou des astuces à partager ? Laissez un commentaire ci‑dessous—bon codage !

![Diagram illustrating how a range with a pivot table is copied from one workbook to another](https://example.com/images/how-to-copy-range-diagram.png "how to copy range diagram")

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}