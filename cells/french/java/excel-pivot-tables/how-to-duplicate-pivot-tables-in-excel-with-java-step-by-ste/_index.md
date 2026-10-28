---
category: general
date: 2026-10-07
description: Apprenez à dupliquer des tableaux croisés dynamiques dans Excel en utilisant
  Java et Aspose.Cells. Copiez un tableau croisé dynamique en copiant sa plage entre
  les classeurs rapidement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: fr
lastmod: 2026-10-07
og_description: Comment dupliquer des tableaux croisés dynamiques dans Excel en utilisant
  Java et Aspose.Cells. Suivez ce guide pour copier un tableau croisé dynamique en
  copiant sa plage entre les classeurs.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Comment dupliquer des tableaux croisés dynamiques dans Excel avec Java –
  tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: Comment dupliquer des tableaux croisés dynamiques dans Excel avec Java – guide
  étape par étape
url: /fr/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment dupliquer des tableaux croisés dynamiques dans Excel avec Java – guide étape par étape

Si vous devez **dupliquer des tableaux croisés dynamiques** dans un classeur Excel, ce tutoriel vous montre une solution complète, prête à l'emploi. En utilisant Aspose.Cells for Java, vous pouvez copier un tableau croisé dynamique avec ses données source en copiant la plage sous‑jacente, puis enregistrer le résultat dans un nouveau classeur.

Dupliquer un tableau croisé dynamique semble souvent difficile parce que le cache du tableau est caché dans la feuille. En copiant toute la plage qui contient le tableau, Aspose.Cells recrée automatiquement le cache dans le classeur de destination, de sorte que vous obtenez une copie pleinement fonctionnelle sans manipulation manuelle du XML.

Dans ce guide, vous allez :

* Charger un classeur source qui contient un tableau croisé dynamique.  
* Définir la plage exacte qui contient le tableau.  
* Copier cette plage dans un nouveau classeur, en préservant la définition du tableau.  
* Enregistrer le nouveau fichier et vérifier que le tableau fonctionne.  

Les étapes fonctionnent avec n'importe quelle version d'Excel prise en charge par Aspose.Cells (2007‑2024) et ne nécessitent que quelques lignes de code Java.

## Prérequis

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| **Java 8 ou plus récent** | Aspose.Cells est conçu pour Java 8+. |
| **Aspose.Cells for Java** (dernière version) | Fournit les API `Workbook`, `Range` et `CopyRange` utilisées dans l'exemple. |
| **Classeur source** avec un tableau croisé dynamique (par ex., `Source.xlsx`) | Le tableau que vous souhaitez dupliquer. |
| **Permission d'écriture** dans le répertoire cible | Nécessaire pour enregistrer `CopyWithPivot.xlsx`. |

Ajoutez la dépendance Maven Aspose.Cells à votre `pom.xml` (ou téléchargez le JAR manuellement) :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## Comment dupliquer des tableaux croisés dynamiques – implémentation complète

Ci‑dessous se trouve un programme Java autonome qui montre **comment dupliquer des tableaux croisés dynamiques** en copiant la plage qui les contient. Le code inclut la gestion des erreurs, des commentaires et une étape de vérification.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### Explication de chaque étape

| Étape | Ce que fait le code | Pourquoi c'est important pour **copy pivot table** |
|-------|----------------------|----------------------------------------------------|
| **1️⃣ Load source workbook** | `new Workbook(srcPath)` lit `Source.xlsx`. | Le fichier source est le seul endroit où le tableau croisé dynamique original existe. |
| **2️⃣ Define the range** | `createRange("A1:G20")` crée un objet `Range` qui couvre le tableau et ses données. | Un tableau croisé dynamique est stocké avec son cache ; copier la plage entière garantit que le cache est déplacé également. |
| **3️⃣ Copy the range** | `copyRange(srcRange, "A1")` écrit la plage dans la feuille de destination. | Ceci est le cœur de **copy range between workbooks** – l'API gère automatiquement les objets cachés. |
| **4️⃣ Refresh pivot** | `pivotTable.refresh()` force le tableau à se recalculer. | Assure que le tableau croisé dynamique dupliqué affiche les mêmes valeurs que l'original, surtout après des modifications. |
| **5️⃣ Save workbook** | `destWb.save(destPath)` écrit le fichier sur le disque. | Produit le résultat final **copy excel range** que vous pouvez ouvrir dans Excel. |

#### Résultat attendu

Après avoir exécuté le programme, ouvrez `CopyWithPivot.xlsx`. Vous verrez une feuille de calcul qui ressemble exactement à la feuille source, et le tableau croisé dynamique fonctionne exactement comme l'original — vous pouvez développer les lignes, filtrer les champs et actualiser les données sans erreurs.

## Variations courantes et cas limites

### 1️⃣ Copier un tableau croisé dynamique qui s'étend sur plusieurs feuilles

Si les données source du tableau se trouvent sur une feuille différente de celle du tableau lui‑même, incluez les deux feuilles dans l'opération de copie. L'approche la plus simple consiste à copier d'abord la feuille source entière, puis à copier la feuille du tableau :

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Gérer les plages nommées

Aspose.Cells préserve les plages nommées lorsque vous copiez une plage. Cependant, si le classeur de destination contient déjà un nom avec le même identifiant, une `CellsException` est levée. Résolvez ce problème en renommant le nom en conflit avant la copie :

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Gros classeurs et performances

Copier des plages très grandes (des centaines de milliers de lignes) peut être gourmand en mémoire. Activez **memory optimization** :

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Conserver les formules intactes

Si la plage source contient des formules qui font référence à des cellules en dehors de la zone copiée, ces références seront cassées après la copie. Pour éviter cela, étendez la plage afin d'inclure toutes les cellules dépendantes, ou utilisez `copyRange` avec le drapeau `CopyOptions` `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Astuces professionnelles pour un **copy range between workbooks** fiable

* **Utilisez toujours des adresses absolues** (`$A$1:$G$20`) lorsque la feuille source peut être renommée.  
* **Actualisez après la copie** – même si Aspose.Cells reconstruit le cache, appeler `refresh()` élimine les avertissements occasionnels de cache obsolète dans Excel.  
* **Validez le tableau** : après l’enregistrement, ouvrez le fichier par programme et appelez `pivotTable.validate()` pour vous assurer qu'aucune référence n’est cassée.  
* **Compatibilité des versions** : le code fonctionne avec les fichiers Excel 2007‑2024 (`.xlsx`, `.xlsm`). Pour les fichiers `.xls` anciens, définissez `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## Listing complet du code source (prêt à compiler)

```java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // --------------------------------------------------------------------
        // 1️⃣ Load source workbook
        // --------------------------------------------------------------------
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 2️⃣ Define the range that contains the pivot table
        // --------------------------------------------------------------------
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        String pivotRangeAddress = "A1:G20"; // adjust to your pivot's actual area
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // --------------------------------------------------------------------
        // 3️⃣ Copy the range (including the pivot) to a new workbook
        // --------------------------------------------------------------------
        Workbook destWb = new Workbook(); // blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 4️⃣ Refresh the duplicated pivot (ensures correct values)
        // --------------------------------------------------------------------
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet


## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment copier un tableau croisé dynamique en Java – Guide complet Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Comment créer des tableaux croisés dynamiques dans Excel avec Aspose.Cells pour Java : guide complet](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Comment mettre à jour la source d'un tableau croisé dynamique Excel avec Aspose.Cells pour Java : guide complet](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}