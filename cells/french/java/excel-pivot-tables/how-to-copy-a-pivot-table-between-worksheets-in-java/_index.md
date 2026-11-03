---
category: general
date: 2026-10-16
description: Comment copier un tableau croisé dynamique en Java avec Aspose.Cells
  – apprenez à copier une plage vers une autre feuille et à copier une plage entre
  feuilles de calcul efficacement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: fr
lastmod: 2026-10-16
og_description: Comment copier un tableau croisé dynamique en Java avec Aspose.Cells.
  Ce tutoriel vous montre comment copier une plage vers une autre feuille et copier
  une plage entre des feuilles de calcul avec le code complet.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Comment copier un tableau croisé dynamique entre feuilles de calcul en Java
  – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Comment copier un tableau croisé dynamique entre feuilles de calcul en Java
url: /fr/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier un tableau croisé dynamique entre feuilles de calcul en Java

Si vous devez **copier un tableau croisé dynamique** d’une feuille à une autre dans le même classeur, ce guide fournit une solution complète, prête à l’emploi. Vous verrez comment copier la plage source contenant le tableau croisé dynamique, en préserver la fonctionnalité, et vérifier le résultat — le tout en utilisant Aspose.Cells pour Java.

Copier un tableau croisé dynamique est une tâche courante lorsque vous générez des rapports de manière programmatique, et le faire correctement évite de perdre le cache du tableau croisé dynamique ou de casser les formules. À la fin de ce tutoriel, vous serez capable de **copier une plage vers une autre feuille** et **copier une plage entre feuilles de calcul** sans aucune étape manuelle.

## Ce que vous apprendrez

* Charger un fichier Excel existant contenant un tableau croisé dynamique.  
* Définir la plage source qui contient le tableau croisé dynamique.  
* Définir une plage de destination sur une feuille différente.  
* Utiliser `CopyOptions` pour garder le tableau croisé dynamique intact.  
* Vérifier que le tableau croisé dynamique copié fonctionne comme prévu.

**Prérequis**

* Java 17 ou version ultérieure.  
* Aspose.Cells for Java (version 23.12 ou plus récente).  
* Un fichier Excel (`input.xlsx`) contenant un tableau croisé dynamique sur la première feuille.

---

## Comment copier un tableau croisé dynamique avec Aspose.Cells

Le cœur de l’opération est un processus en quatre étapes : charger le classeur, localiser la plage source, définir la plage de destination et effectuer la copie. Chaque étape est expliquée en détail ci‑dessous.

### Étape 1 : Charger le classeur

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*Pourquoi cette étape ?*  
Charger le classeur charge le fichier complet en mémoire, vous donnant accès aux feuilles de calcul, aux cellules et au cache du tableau croisé dynamique. Aspose.Cells lit automatiquement le format du fichier, vous n’avez donc pas à vous soucier de `.xls` vs `.xlsx`.

### Étape 2 : Localiser la plage source contenant le tableau croisé dynamique

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Pourquoi cette étape ?*  
Un tableau croisé dynamique est stocké dans un bloc de cellules qui référence également un cache caché. En sélectionnant la plage exacte (`A1:G20` dans cet exemple), vous vous assurez que le cache reste lié lors de la copie de la plage.

### Étape 3 : Définir la plage de destination sur une autre feuille

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*Pourquoi cette étape ?*  
Choisir une destination sur une feuille différente vous permet de **copier une plage vers une autre feuille**. La cellule en haut à gauche (`A1`) est un point de départ courant, mais vous pouvez la placer n’importe où en modifiant l’adresse.

### Étape 4 : Copier la plage source tout en préservant le tableau croisé dynamique

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*Pourquoi cette étape ?*  
`CopyOptions` contrôle ce qui est transféré. Utiliser `PasteType.PASTE_ALL` garantit que le tableau croisé dynamique, son formatage et les formules sous‑jacentes sont dupliqués. Sans ces options, seules les valeurs brutes pourraient être copiées, ce qui casserait la fonctionnalité du tableau croisé dynamique.

### Étape 5 : Enregistrer le classeur et vérifier le résultat

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Ouvrez `output.xlsx` dans Excel et confirmez que :

* La deuxième feuille contient un tableau croisé dynamique pleinement fonctionnel identique à l’original.  
* Actualiser le tableau croisé dynamique met à jour les données, prouvant que le cache est intact.

---

## Copier une plage vers une autre feuille avec Java

Si votre objectif est simplement de **copier une plage vers une autre feuille** sans tableau croisé dynamique, le même code fonctionne avec une plage de cellules ordinaire. Le seul changement est l’adresse source. La configuration de `CopyOptions` reste la même, garantissant que les formules et le formatage sont préservés.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

Cet extrait montre la flexibilité de l’API pour les scénarios avec ou sans tableau croisé dynamique.

---

## Copier une plage entre feuilles de calcul sans perdre les formules

Lorsque vous **copiez une plage entre feuilles de calcul**, les formules qui font référence à d’autres feuilles peuvent se casser si les références relatives changent. Pour éviter cela :

1. Utilisez `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` si vous ne avez besoin que des formules.  
2. Gardez la feuille de destination dans le même classeur afin que les références internes restent valides.  
3. Après la copie, appelez `workbook.calculateFormula();` pour forcer un recalcul.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

Ces étapes supplémentaires garantissent qu’une plage copiée se comporte exactement comme l’originale, même lorsqu’elle s’étend sur plusieurs feuilles.

---

## Conseils pro et pièges courants

| Situation | Conseil |
|-----------|---------|
| **Cache du tableau croisé dynamique ne se met pas à jour** | Après la copie, appelez `destSheet.getPivotTables().get(0).refresh();` pour rafraîchir le cache. |
| **Copier vers un classeur différent** | Utilisez `Workbook destWorkbook = new Workbook();` puis `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. N’oubliez pas de copier le cache du tableau croisé dynamique séparément si nécessaire. |
| **Grands tableaux croisés dynamiques** | Augmentez la taille du tas Java (`-Xmx2g`) pour éviter `OutOfMemoryError` pendant la copie. |
| **Préserver les styles** | Définissez `copyOptions.setPasteType(PasteType.PASTE_ALL)` ; sinon, seules les valeurs sont copiées. |

---

## Résultat attendu

L’exécution du programme complet produit `output.xlsx`. Lorsqu’il est ouvert dans Excel :

* **Sheet2!A1:G20** affiche le même tableau croisé dynamique que **Sheet1!A1:G20**.  
* La liste des champs du tableau, les libellés de lignes/colonnes et les valeurs de données correspondent à la source.  
* Actualiser le tableau met à jour les nombres, confirmant que le cache est fonctionnel.

La console affichera :

```
Pivot table copied successfully.
```

---

## Conclusion

Dans ce tutoriel, vous avez appris **comment copier un tableau croisé dynamique** d’une feuille de calcul à une autre en utilisant Aspose.Cells pour Java. En chargeant le classeur, en sélectionnant la bonne plage source, en définissant une destination et en configurant `CopyOptions`, vous pouvez de manière fiable **copier une plage vers une autre feuille** et **copier une plage entre feuilles de calcul** tout en préservant toutes les fonctionnalités du tableau croisé dynamique.  

Ensuite, vous pourriez explorer :

* Exporter le tableau croisé dynamique copié en PDF ou HTML.  
* Automatiser le rafraîchissement des tableaux croisés dynamiques à travers plusieurs classeurs.  
* Utiliser `CopyOptions` pour copier uniquement des éléments spécifiques (par ex., valeurs, formats).

N’hésitez pas à expérimenter avec différentes adresses de plage, structures de classeur, ou même des copies entre classeurs. Bon codage !

## Quoi apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos projets.

- [Comment copier une plage en Java – Copier un tableau croisé dynamique avec Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Comment copier un tableau croisé dynamique en Java – Guide complet Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Copier un tableau croisé dynamique Excel – Guide étape par étape avec Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}