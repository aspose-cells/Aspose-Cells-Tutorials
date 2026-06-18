---
category: general
date: 2026-06-18
description: Supprimer des lignes dans une feuille de calcul à l'aide d'Aspose.Cells
  pour Java. Apprenez comment supprimer la ligne d’en‑tête du tableau et supprimer
  des lignes d’un tableau Excel en toute sécurité.
draft: false
keywords:
- delete rows in worksheet
- remove table header row
- remove rows from excel table
language: fr
og_description: Supprimez des lignes dans une feuille de calcul avec Aspose.Cells
  pour Java. Ce guide montre comment supprimer la ligne d’en-tête du tableau et supprimer
  des lignes d’un tableau Excel de manière efficace.
og_title: Supprimer des lignes dans une feuille de calcul avec Java – Étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Delete rows in worksheet using Aspose.Cells for Java. Learn how to
    remove table header row and delete rows from Excel table safely.
  headline: Delete rows in worksheet with Java – Complete Guide
  type: TechArticle
- description: Delete rows in worksheet using Aspose.Cells for Java. Learn how to
    remove table header row and delete rows from Excel table safely.
  name: Delete rows in worksheet with Java – Complete Guide
  steps:
  - name: '`table.unlist()` strips the table metadata, turning the block into ordinary
      cells.'
    text: '`table.unlist()` strips the table metadata, turning the block into ordinary
      cells.'
  - name: With the header now a regular row, `deleteRows(0, …)` works without complaints.
    text: With the header now a regular row, `deleteRows(0, …)` works without complaints.
  - name: If you still need a table after the cleanup, you can recreate it using `ws.getTables().add(...)`.
    text: If you still need a table after the cleanup, you can recreate it using `ws.getTables().add(...)`.
  - name: Loads a workbook.
    text: Loads a workbook.
  - name: Checks if the first table exists.
    text: Checks if the first table exists.
  - name: Deletes **all** rows *including* the header safely.
    text: Deletes **all** rows *including* the header safely.
  - name: Re‑creates the table from the remaining rows (if any).
    text: Re‑creates the table from the remaining rows (if any).
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Worksheet
title: Supprimer des lignes dans une feuille de calcul avec Java – Guide complet
url: /fr/java/worksheet-management/delete-rows-in-worksheet-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Supprimer des lignes dans une feuille de calcul – Tutoriel complet Java

Vous avez déjà eu besoin de **supprimer des lignes dans une feuille de calcul** mais vous êtes tombé sur un mur parce que l’en‑tête du tableau refuse de bouger ? Vous n'êtes pas le seul. Dans de nombreux scénarios d’automatisation Excel, la première ligne appartient à un tableau structuré, et un appel naïf à `deleteRows` lève une exception ou laisse simplement l’en‑tête intact.

Dans ce tutoriel, nous allons voir exactement comment *supprimer la ligne d’en‑tête du tableau* et *supprimer des lignes d’un tableau Excel* sans endommager la feuille. À la fin, vous disposerez d’un extrait propre et exécutable qui fonctionne avec la dernière version d’Aspose.Cells for Java (v23.10 au moment de la rédaction).

Nous couvrirons les prérequis, trois approches pratiques, et une poignée d’astuces que vous voudrez mettre en signet. Pas de fioritures — juste le type de réponse que l’on attend d’un développeur chevronné autour d’un café.

## Prérequis

- Java 17 ou plus récent (le code se compile avec des versions antérieures, mais 17 est recommandé).
- Aspose.Cells for Java 23.10 ou ultérieur ajouté à votre Maven `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

- Un fichier Excel d’exemple (`Sample.xlsx`) contenant un tableau sur la première feuille de calcul. L’en‑tête du tableau se trouve à la ligne 0 (ligne 1 d’Excel).

C’est tout. Prêt ? Commençons.

## Supprimer des lignes dans une feuille de calcul – pourquoi la ligne d’en‑tête est importante

Lorsque vous appelez :

```java
ws.getCells().deleteRows(0, 2, true);
```

Aspose.Cells refuse de supprimer la ligne 0 car elle fait partie d’un **tableau**. L’API protège l’intégrité du tableau ; supprimer l’en‑tête laisserait les lignes de données orphelines. L’exception que vous verrez ressemble à *« The specified row belongs to a table and cannot be deleted. »*  

Comprendre cette protection est la première étape d’une solution réussie.

## Approche 1 – Supprimer les lignes **en dessous** de l’en‑tête (la plus courante)

Si vous souhaitez simplement effacer les données tout en conservant la structure du tableau, commencez à supprimer à partir de la ligne **après** l’en‑tête.

```java
import com.aspose.cells.*;

public class DeleteRowsBelowHeader {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Determine how many data rows the table currently has
        Table table = ws.getTables().get(0);
        int dataRowCount = table.getDataRange().getRowCount();

        // Delete all data rows (keep header)
        // startRow = 1 because row index 0 is the header
        ws.getCells().deleteRows(1, dataRowCount, true);

        // Save the result
        wb.save("Result_DeleteRowsBelowHeader.xlsx");
    }
}
```

**Pourquoi cela fonctionne  :** `deleteRows` reçoit un indice de départ de 1, donc l’en‑tête reste intact. Le drapeau `true` décale les lignes restantes vers le haut, préservant toutes les formules qui les référencent. Après l’exécution du code, vous verrez un tableau propre avec uniquement la ligne d’en‑tête restante.

### Astuce rapide

Si vous devez supprimer une plage *spécifique* de lignes (par ex., lignes 5‑10), ajustez simplement l’indice de départ et le nombre en conséquence. Le tableau sera automatiquement redimensionné pour correspondre à la nouvelle plage de données.

## Approche 2 – Convertir le tableau en plage simple, puis supprimer

Parfois, vous devez réellement **supprimer la ligne d’en‑tête du tableau** et traiter les données comme une plage ordinaire. L’astuce consiste d’abord à *unlist* le tableau.

```java
import com.aspose.cells.*;

public class RemoveHeaderAndDeleteRows {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Table table = ws.getTables().get(0);

        // 1️⃣ Unlist the table – it becomes a normal range
        table.unlist();

        // 2️⃣ Now you can delete the header row (row 0) and any other rows
        // Delete header + first two data rows (total 3 rows)
        ws.getCells().deleteRows(0, 3, true);

        // 3️⃣ (Optional) Re‑create a table from the remaining data
        // Assuming you still have data starting at row 0
        int firstDataRow = 0;
        int lastDataRow = ws.getCells().getMaxDataRow();
        int firstCol = ws.getCells().getMaxDataColumn();
        int lastCol = ws.getCells().getMaxDataColumn();

        String range = new CellArea(firstDataRow, 0, lastDataRow, firstCol).format();
        ws.getTables().add(range, true);
        ws.getTables().get(0).setName("NewTable");

        wb.save("Result_RemoveHeaderAndDeleteRows.xlsx");
    }
}
```

**Explication :**  

1. `table.unlist()` supprime les métadonnées du tableau, transformant le bloc en cellules ordinaires.  
2. Avec l’en‑tête maintenant une ligne normale, `deleteRows(0, …)` fonctionne sans problème.  
3. Si vous avez encore besoin d’un tableau après le nettoyage, vous pouvez le recréer en utilisant `ws.getTables().add(...)`.

Cette approche est pratique lorsque l’en‑tête lui‑même est incorrect ou que vous souhaitez remplacer toute la définition du tableau.

## Approche 3 – Utiliser l’API Table pour supprimer des lignes spécifiques

Aspose.Cells propose également une méthode **au niveau du tableau** pour supprimer des lignes, qui gère automatiquement la protection de l’en‑tête.

```java
import com.aspose.cells.*;

public class DeleteRowsViaTableAPI {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Table table = ws.getTables().get(0);

        // Delete the first two data rows (index 0 = first data row, not the header)
        // The Table API counts only data rows, so we don't touch the header.
        table.deleteRows(0, 2);

        wb.save("Result_DeleteRowsViaTableAPI.xlsx");
    }
}
```

**Pourquoi vous pourriez choisir celle‑ci  :** C’est la façon la plus *sémantique* — vous dites au tableau « supprimez mes lignes de données ». L’API met à jour automatiquement la plage du tableau, et vous n’avez jamais à manipuler les indices de lignes brutes.

## Cas limites & pièges courants

| Situation | À surveiller | Solution recommandée |
|-----------|--------------|----------------------|
| **Multiple tables on the same sheet** | `ws.getTables().get(0)` may target the wrong table. | Use `ws.getTables().stream().filter(t -> t.getName().equals("MyTable")).findFirst().orElse(null)` |
| **Merged cells in the header** | Deleting rows can split merged areas, causing layout glitches. | Unmerge before deletion: `ws.getCells().get("A1").getMergedRange().unmerge();` |
| **Formulas referencing the header** | Removing the header breaks external references. | Update formulas after deletion or keep a placeholder row. |
| **Large worksheets (>10 000 rows)** | `deleteRows` may be slower due to internal shifting. | Use `ws.getCells().clearRows(start, count)` if you don’t need to shift. |

## Exemple complet fonctionnel – Combiner le meilleur de tous les mondes

Voici un programme autonome qui :

1. Charge un classeur.
2. Vérifie si le premier tableau existe.
3. Supprime **toutes** les lignes *y compris* l’en‑tête en toute sécurité.
4. Re‑crée le tableau à partir des lignes restantes (le cas échéant).

```java
import com.aspose.cells.*;

public class DeleteRowsInWorksheetFullDemo {
    public static void main(String[] args) throws Exception {
        // ① Load the workbook
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // ② Guard: make sure a table is present
        if (ws.getTables().getCount() == 0) {
            System.out.println("No tables found – nothing to delete.");
            return;
        }

        // ③ Grab the first table (adjust if you have a named table)
        Table table = ws.getTables().get(0);

        // ④ Unlist so we can delete the header row
        table.unlist();

        // ⑤ Determine total rows to delete (header + data)
        int totalRows = table.getRange().getRowCount(); // includes header
        ws.getCells().deleteRows(0, totalRows, true);

        // ⑥ If there are still rows left, rebuild the table
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();

        if (maxRow >= 0) { // there is at least one row left
            String newRange = new CellArea(0, 0, maxRow, maxCol).format();
            Table newTable = ws.getTables().add(newRange, true);
            newTable.setName("RebuiltTable");
        }

        // ⑦ Save the result
        wb.save("Result_DeleteRowsInWorksheetFullDemo.xlsx");
        System.out.println("Rows deleted and table rebuilt successfully.");
    }
}
```

**Sortie attendue  :** Après exécution, vous trouverez `Result_DeleteRowsInWorksheetFullDemo.xlsx` avec le tableau original supprimé, et—si des données subsistent—un nouveau tableau nommé `RebuiltTable`. La console affiche un message de succès concis.

## Résumé visuel

![Excel worksheet before and after deleting rows](https://example.com/images/delete-rows-workbook.png "Before and after deleting rows in worksheet")

*Texte alternatif :* « Avant et après la suppression des lignes dans la feuille de calcul – en‑tête supprimé, lignes de données effacées. »

## Conclusion

Nous avons présenté trois méthodes fiables pour **supprimer des lignes dans une feuille de calcul** tout en gérant le scénario délicat de *suppression de la ligne d’en‑tête du tableau* et en **supprimant en toute sécurité des lignes d’un tableau Excel**. Que vous préfériez les opérations brutes sur les cellules, l’API Table, ou un cycle complet unlist‑relist, les extraits de code ci‑dessus sont prêts à être intégrés à votre projet.  

Prochaines étapes ? Essayez de combiner ces techniques avec une logique conditionnelle — supprimez les lignes uniquement lorsqu’une certaine colonne contient « Inactive », ou traitez par lots plusieurs

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Gestion efficace des lignes dans Excel avec Aspose.Cells for Java : insertion et suppression de lignes](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)
- [Comment supprimer les lignes vides des fichiers Excel avec Aspose.Cells for Java](/cells/english/java/data-manipulation/delete-blank-rows-aspose-cells-java/)
- [Comment supprimer des lignes dans Excel en utilisant Aspose.Cells for Java | Guide & Tutoriel](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}