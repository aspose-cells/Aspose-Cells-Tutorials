---
category: general
date: 2026-09-18
description: Comment dupliquer un tableau croisé dynamique en Java avec Aspose.Cells
  – copier un tableau croisé dynamique entre classeurs rapidement et de manière fiable.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: fr
lastmod: 2026-09-18
og_description: Comment dupliquer un tableau croisé dynamique en Java à l'aide d'Aspose.Cells.
  Suivez ce tutoriel complet pour copier un tableau croisé dynamique entre classeurs
  avec un code Java propre.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Dupliquer un tableau croisé dynamique en Java – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Comment dupliquer un tableau croisé dynamique en Java avec Aspose.Cells
url: /fr/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment dupliquer un pivot en Java avec Aspose.Cells

Si vous avez besoin de **comment dupliquer un pivot** dans une application Java, ce guide vous montre les étapes exactes. En chargeant un classeur Excel, en définissant la zone de cellules du pivot, et en copiant cette plage dans un nouveau classeur, vous pouvez déplacer un tableau croisé dynamique sans perdre sa définition ni ses données.

Copier un tableau croisé dynamique est une exigence courante lorsque vous générez des rapports, archivez des analyses ou divisez un grand classeur en morceaux modulaires. Dans ce tutoriel, vous apprendrez comment **copier une plage entre classeurs**, comment **charger un classeur Excel en Java**, et les nuances de **comment copier un pivot** en toute sécurité.

Vous terminerez avec un programme Java prêt à l'exécution qui duplique un tableau croisé dynamique de `Source.xlsx` vers `PivotCopied.xlsx` en utilisant Aspose.Cells pour Java.

## Prérequis

* JDK 8 ou version plus récente installé.
* Maven (ou un autre outil de construction) pour gérer les dépendances.
* Aspose.Cells for Java version 23.10 ou ultérieure. Ajoutez la dépendance Maven suivante à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* Un classeur source (`Source.xlsx`) contenant un tableau croisé dynamique dans la plage **A1:H30**.

## Comment dupliquer un pivot en Java

L'idée principale est simple :

1. **Charger le classeur source** – cela vous donne accès à la feuille qui contient le pivot.
2. **Définir la zone de cellules** qui englobe le pivot.
3. **Créer un classeur de destination** – un fichier vide qui recevra la plage copiée.
4. **Copier la plage** – Aspose.Cells duplique automatiquement la définition du pivot.
5. **Enregistrer le classeur de destination** – vous avez maintenant un fichier séparé avec le même pivot.

Voici un programme Java complet et exécutable qui suit ces étapes.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Pourquoi cela fonctionne

* **Aspose.Cells** considère un tableau croisé dynamique comme faisant partie de la collection de cellules de la feuille. Lorsque vous invoquez `copyRange`, la bibliothèque copie non seulement les valeurs des cellules mais aussi le cache et la définition du pivot sous-jacents, de sorte que le nouveau classeur contient un duplicata pleinement fonctionnel.
* L'objet `CopyOptions` préserve par défaut les formules, les formats et les objets incorporés. Vous pouvez le personnaliser (par ex., `setCopyColumnWidths(true)`) si vous avez besoin d'un contrôle supplémentaire.

## Copier une plage entre classeurs – examen approfondi

Bien que l'exemple ci‑dessus copie un seul bloc contigu, `copyRange` peut gérer n'importe quelle zone rectangulaire. Si votre pivot s'étend sur des plages non adjacentes, vous pouvez appeler `copyRange` plusieurs fois ou utiliser `Worksheet.copy` pour dupliquer la feuille entière.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Astuce :** Lors de la copie de grands classeurs, activez `CopyOptions.setPreserveCellStyle(true)` pour éviter la duplication inutile de styles, ce qui peut améliorer les performances.

## Comment copier un pivot vers un classeur – gestion de plusieurs pivots

Si la feuille source contient plus d'un pivot, vous pouvez parcourir les tableaux croisés dynamiques de la feuille et copier chacun individuellement :

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

Cette approche garantit que chaque pivot conserve son nom et sa source de données d'origine.

## Charger un classeur Excel en Java – pièges courants

* **Séparateurs de chemin de fichier :** Utilisez des barres obliques (`/`) ou `File.separator` pour rendre le code indépendant de la plateforme.
* **Licence manquante :** Aspose.Cells fonctionne en mode d'évaluation, mais la sortie contiendra un filigrane. Enregistrez une licence avec `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` avant de charger le classeur pour supprimer le filigrane.
* **Fichiers volumineux :** Pour les classeurs de plus de 100 Mo, envisagez d'utiliser `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` avec des options de streaming afin de réduire la consommation de mémoire.

## Récapitulatif complet de l'exemple de bout en bout

En rassemblant tous les éléments, voici le programme final que vous pouvez copier‑coller dans votre IDE :

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Sortie attendue :** Après exécution, `PivotCopied.xlsx` apparaît dans le répertoire spécifié. L'ouvrir dans Excel montre la même mise en page du tableau croisé dynamique, les filtres et les données que dans `Source.xlsx`. Tous les champs calculés et le formatage sont conservés.

## Questions fréquemment posées

* **Cela fonctionne-t-il avec les anciens formats Excel (.xls) ?**  
  Oui. Aspose.Cells détecte automatiquement le format. Utilisez `new Workbook("file.xls")` et la même logique de copie s'applique.

* **Que se passe-t-il si le pivot fait référence à des sources de données externes ?**  
  La copie conserve la référence à la source de données d'origine. Si l'environnement de destination ne peut pas accéder à cette source, le pivot affichera des erreurs `#REF!`. Pour éviter cela, actualisez le pivot après la copie ou modifiez sa source de données via `PivotTable.setDataSource(...)`.

* **Puis-je copier un pivot vers un nom de feuille spécifique ?**  
  Absolument. Après avoir créé la feuille de destination, renommez‑la :

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Conclusion

Vous savez maintenant **comment dupliquer des pivots** en Java avec Aspose.Cells, comment **copier une plage entre classeurs**, et les meilleures pratiques pour **charger un classeur Excel en Java**. En suivant le processus en cinq étapes — charger, définir, créer la destination, copier et enregistrer — vous pouvez automatiser la génération de rapports, archiver des analyses ou diviser des classeurs complexes sans perdre la fonctionnalité du pivot.

Ensuite, explorez des sujets connexes tels que **copier un pivot vers un classeur** avec plusieurs feuilles, ou intégrez le pivot dupliqué dans un pipeline de traitement de données plus vaste en utilisant Apache POI pour les scénarios non‑Aspose. Expérimentez avec différents paramètres `CopyOptions` pour affiner les performances sur des classeurs massifs.

Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment créer des tableaux croisés dynamiques dans Excel avec Aspose.Cells pour Java : Guide complet](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Comment mettre à jour la source d'un tableau croisé dynamique Excel avec Aspose.Cells pour Java : Guide complet](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Regrouper les champs d'un tableau croisé dynamique dans les classeurs Excel avec Aspose.Cells pour Java – Guide complet](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}