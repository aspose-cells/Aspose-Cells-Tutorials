---
category: general
date: 2026-10-23
description: Apprenez à dupliquer une feuille Excel en Java tout en préservant les
  tableaux croisés dynamiques. Ce guide montre également comment copier les tableaux
  croisés dynamiques, copier des plages Excel et copier une feuille contenant des
  données de tableau croisé dynamique.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: fr
lastmod: 2026-10-23
og_description: Dupliquer une feuille Excel en Java tout en conservant les tableaux
  croisés dynamiques. Suivez ce tutoriel complet pour copier les tableaux croisés
  dynamiques, copier les plages Excel et copier une feuille contenant des données
  de tableau croisé dynamique.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Dupliquer une feuille Excel avec des tableaux croisés dynamiques en Java
  – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Comment dupliquer une feuille Excel et garder les tableaux croisés dynamiques
  intacts en Java
url: /fr/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment dupliquer une feuille Excel tout en conservant les tableaux croisés dynamiques intacts en Java

Si vous devez **dupliquer une feuille Excel** tout en maintenant chaque tableau croisé dynamique actif, ce guide vous montre exactement comment faire. Vous verrez une solution concise qui copie une feuille, copie une plage spécifique, et même copie un tableau croisé dynamique vers un autre classeur — le tout en Java pur avec Aspose.Cells.

Dupliquer une feuille Excel est une tâche courante lorsque vous générez des rapports mensuels à partir d’un modèle ou lorsque vous avez besoin d’une copie sandbox pour les tests. Le code ci‑dessous fonctionne avec Aspose.Cells 25.11 ou ultérieur, qui a introduit l’option `setCopyPivotTable(true)`.

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d’avoir :

- Java 17 (ou tout JDK récent) installé
- Aspose.Cells for Java 25.11 ou plus récent dans votre projet (coordonnée Maven `com.aspose:aspose-cells:25.11`)
- Un classeur source (`SourceWithPivot.xlsx`) contenant déjà un tableau croisé dynamique
- Un IDE ou un outil de construction de votre choix (IntelliJ IDEA, Eclipse, Maven, Gradle, etc.)

## Étape 1 : Charger le classeur source qui contient le tableau croisé dynamique

La première opération consiste à ouvrir le classeur qui détient le tableau croisé dynamique que vous souhaitez préserver.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Pourquoi cette étape est importante :** Charger le classeur source vous donne accès aux objets de feuille, aux cellules et aux tableaux croisés dynamiques intégrés. Sans cela, vous ne pouvez pas référencer les données du tableau que vous prévoyez de copier.

## Étape 2 : Créer un classeur de destination vide (ou charger un existant)

Vous pouvez soit partir d’un classeur vierge, soit ouvrir un fichier existant qui recevra la feuille dupliquée.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **Astuce :** Si vous avez déjà un classeur de reporting, remplacez la ligne ci‑dessus par `new Workbook("ExistingReport.xlsx")` pour y ajouter la feuille dupliquée.

## Étape 3 : Copier la feuille entière – le tableau croisé dynamique est préservé automatiquement

Copier la feuille entière est la façon la plus simple de **copier une feuille avec tableau croisé dynamique**. Aspose.Cells copie la définition du tableau et son cache automatiquement.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Pourquoi cela fonctionne :** `addCopy` clone la structure de la feuille, les valeurs des cellules, les styles et tous les tableaux croisés dynamiques intégrés. La nouvelle feuille dans `dstWb` sera identique à l’originale, y compris le cache du tableau.

## Étape 4 : (Facultatif) Copier uniquement une plage spécifique qui inclut le tableau croisé dynamique

Parfois vous ne voulez pas toute la feuille — peut‑être avez‑vous seulement besoin d’une portion contenant le tableau. C’est là que vous **copiez une plage Excel** et demandez explicitement que le tableau soit copié.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **Comment cela aide :** `setCopyPivotTable(true)` force le moteur à dupliquer la définition du tableau même lorsque vous copiez une plage limitée. Sans ce drapeau, seules les données brutes seraient copiées et le tableau serait perdu.

## Étape 5 : Enregistrer le classeur de destination

Enfin, écrivez le contenu dupliqué dans un nouveau fichier.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Résultat attendu

L’exécution du programme crée `DuplicatedWithPivot.xlsx` dans le répertoire cible. Ouvrez le fichier dans Excel et vous verrez :

- Une nouvelle feuille nommée `Sheet1 (Copy)` (ou le nom original avec « Copy » ajouté)
- Le tableau croisé dynamique apparaît exactement comme dans la feuille source, pleinement fonctionnel
- Si vous avez utilisé la copie de plage optionnelle, seules les cellules A1:G30 sont présentes, mais le tableau fonctionne toujours car son cache a été copié

## Questions fréquentes et cas particuliers

### Comment copier un tableau croisé dynamique vers un autre classeur sans copier toute la feuille ?

Si vous avez seulement besoin du tableau et de ses données sous‑jacentes, copiez la plage qui contient à la fois les données sources et le tableau, puis utilisez `setCopyPivotTable(true)`. Le même code de **l’Étape 4** s’applique ; assurez‑vous simplement que la plage couvre la source de données.

### Que faire si le classeur source possède plusieurs feuilles avec des tableaux croisés dynamiques ?

Répétez **l’Étape 3** pour chaque feuille que vous souhaitez dupliquer :

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### Cela fonctionne‑t‑il avec des feuilles protégées ?

Aspose.Cells peut copier des feuilles protégées, mais vous devez les déprotéger d’abord si vous avez besoin de modifier le tableau après la copie :

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### Puis‑je copier un tableau croisé dynamique dans un classeur existant qui contient déjà une feuille du même nom ?

Oui. Utilisez `addCopy` avec un nom unique :

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Astuce pro : vérifier le cache du tableau croisé dynamique

Après la copie, vous pouvez confirmer programmatique que le cache du tableau existe :

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

Si l’ID du cache affiche un nombre non négatif, le tableau a été dupliqué avec succès.

## Conclusion

Vous savez maintenant comment **dupliquer une feuille Excel** en Java tout en préservant chaque tableau croisé dynamique, comment **copier directement des tableaux croisés dynamiques**, comment **copier une plage Excel** qui inclut un tableau, et comment **copier une feuille avec tableau** ou **copier un tableau vers un classeur** en utilisant Aspose.Cells 25.11+. Appliquez ces modèles pour automatiser la génération de rapports, créer des clones de modèles, ou bâtir des environnements de test nécessitant des analyses pilotées par des tableaux croisés dynamiques identiques.

Prêt à explorer davantage ? Essayez d’exporter le classeur dupliqué en PDF, ou rafraîchissez programmatique le cache du tableau après la copie afin de garantir que les dernières données soient reflétées. Bon codage !

## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to duplicate worksheet and preserve pivot tables in Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}