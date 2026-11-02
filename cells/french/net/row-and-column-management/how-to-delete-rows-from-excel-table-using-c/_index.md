---
category: general
date: 2026-09-27
description: Apprenez à supprimer des lignes d’un tableau Excel en C# avec un guide
  étape par étape qui montre également comment charger rapidement un classeur Excel
  en C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: fr
lastmod: 2026-09-27
og_description: Supprimer des lignes d’un tableau Excel en C# avec un exemple clair.
  Ce tutoriel couvre également comment charger un classeur Excel en C# et gérer les
  cas limites courants.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: Supprimer des lignes d'un tableau Excel en C# – guide complet du code
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: Comment supprimer des lignes d'un tableau Excel en C#
url: /fr/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Supprimer des lignes d'un tableau Excel en C# – guide complet de programmation

Si vous devez **supprimer des lignes d'un tableau Excel** dans un fichier .xlsx, ce tutoriel vous montre exactement comment le faire avec C#. Vous verrez un exemple concis et exécutable qui charge un classeur Excel, supprime des lignes spécifiques du premier tableau et enregistre le résultat. L'approche fonctionne avec la bibliothèque populaire Aspose.Cells et peut être adaptée à d'autres API Excel .NET.

Supprimer des lignes d'un tableau est une tâche courante lors du nettoyage de données importées, de la réduction de sections de rapports ou de l'automatisation des mises à jour de feuilles de calcul. À la fin de ce guide, vous serez capable de **charger un classeur Excel C#**, localiser un tableau (ListObject), supprimer les lignes que vous choisissez et écrire le fichier modifié sur le disque.

## Prérequis

* .NET 6.0 ou ultérieur installé (le code fonctionne également avec .NET Framework 4.7+).
* Une référence au package NuGet **Aspose.Cells** (ou toute bibliothèque compatible exposant les types `Workbook`, `Worksheet` et `ListObject`).
* Un fichier d'entrée nommé `input.xlsx` placé dans un dossier que vous pouvez référencer depuis votre projet.
* Une connaissance de base de la syntaxe C# et de Visual Studio (ou votre IDE préféré).

> **Astuce :** Si vous préférez une alternative open‑source, la même logique peut être appliquée avec **ClosedXML** – il suffit de remplacer les classes spécifiques à Aspose par `XLWorkbook`, `IXLWorksheet` et `IXLTable`.

## Étape 1 : Charger le classeur Excel en C#

La première opération consiste à lire le fichier source en mémoire. Charger le classeur est peu coûteux pour des tailles de feuilles de calcul typiques et vous donne un accès complet aux feuilles, aux tableaux et aux valeurs des cellules.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Pourquoi c'est important :* `Workbook` analyse la structure Open XML du fichier .xlsx, exposant une collection d'objets `Worksheet`. Si le fichier est introuvable, Aspose lève une `FileNotFoundException`, assurez‑vous donc que le chemin est correct.

## Étape 2 : Accéder à la feuille cible

La plupart des feuilles de calcul contiennent plusieurs feuilles ; vous devez choisir celle qui contient le tableau que vous souhaitez modifier. Ici nous utilisons la première feuille (`Worksheets[0]`), qui est une valeur sûre pour les fichiers simples.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Pourquoi c'est important :* `Worksheet` est le conteneur des tableaux (`ListObjects`). Accéder à la bonne feuille évite des modifications accidentelles de données non liées.

## Étape 3 : Supprimer des lignes d'un tableau Excel

Les tableaux Excel sont représentés par des objets `ListObject`. Le premier tableau de la feuille est `ListObjects[0]`. La méthode `DeleteRows(startIndex, rowCount)` supprime des lignes **relatives à la zone de données du tableau**, et non aux numéros de lignes absolus de la feuille.  

Dans cet exemple, nous supprimons la deuxième et la troisième ligne du tableau (l'en-tête est la ligne 0, donc nous commençons à l'index 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### Et si le tableau a un nom ou une position différente ?

* **Table nommé :** Utilisez `ws.ListObjects["MyTableName"]` au lieu de l'index.  
* **Tables multiples :** Parcourez `ws.ListObjects` et choisissez celui qui correspond à une condition (par ex., les noms d'en‑tête de colonne).  
* **Nombre de lignes dynamique :** Vous pouvez calculer `rowCount` à l'exécution en inspectant `ws.ListObjects[0].DataRange.RowCount`.

### Gestion des cas limites

| Situation | Modification de code recommandée |
|----------------------------------------|--------------------------------------------------------------|
| Le tableau est vide ou contient moins de lignes | Check `ws.ListObjects[0].DataRange.RowCount` before deleting. |
| Les lignes à supprimer dépassent la taille du tableau | Clamp `rowCount` to `DataRange.RowCount - startIndex`. |
| Besoin de supprimer des lignes en fonction d'une condition (par ex., valeur dans la colonne C) | Iterate `DataRange.Rows` and collect matching indices, then delete in reverse order to keep indices stable. |

## Étape 4 : Enregistrer le classeur modifié

Après la suppression, écrivez le classeur dans un nouveau fichier (ou écrasez l'original si vous le préférez). L'enregistrement crée un nouveau .xlsx qui reflète le tableau mis à jour.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Pourquoi c'est important :* `Save` sérialise la représentation en mémoire sur le disque. Si vous devez conserver le fichier original, écrivez toujours vers un chemin différent.

## Exemple complet et exécutable

Assembler toutes les étapes vous donne un programme autonome que vous pouvez copier, coller et exécuter.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Sortie attendue** (console) :

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Ouvrez `output.xlsx` – le premier tableau ne contient plus les lignes que vous avez supprimées, tandis que la ligne d'en‑tête reste intacte.

## Questions fréquentes et variantes

### Comment supprimer des lignes de **tous** les tableaux d'un classeur ?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### Puis‑je supprimer des lignes en fonction d’une **valeur de cellule** ?

Oui. Parcourez le `DataRange` à la recherche de cellules correspondantes, collectez leurs indices zéro‑basés, puis supprimez-les dans l'ordre décroissant :

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### Et si je dois **conserver le formatage** ?

`DeleteRows` supprime la ligne entière du tableau mais conserve le style du tableau pour les lignes restantes. Si vous devez garder un formatage spécifique sur une ligne que vous supprimez, copiez le style sur une autre ligne avant la suppression.

### Cette méthode fonctionne‑t‑elle avec les fichiers **.xls** (Excel 97‑2003) ?

Oui. Aspose.Cells détecte automatiquement le format du fichier, donc le même code fonctionne avec `.xls`. Il suffit de changer l'extension du fichier dans le constructeur `Workbook`.

## Conseils de performance

* **Suppressions groupées :** Supprimer de nombreuses lignes une par une peut être plus lent. Utilisez un appel unique `DeleteRows(start, count)` lorsqu'il est possible.  
* **Éviter le blocage du thread UI :** Si vous intégrez cela dans une application de bureau, exécutez la manipulation du classeur sur un thread d'arrière‑plan pour garder l'interface réactive.  
* **Libérer correctement les ressources :** Bien qu'Aspose.Cells utilise la mémoire gérée, encapsulez le `Workbook` dans un bloc `using` si vous traitez de gros fichiers afin de libérer rapidement les ressources.

## Conclusion

Vous disposez maintenant d'un exemple complet et prêt pour la production qui **supprime des lignes d'un tableau Excel** en utilisant C#. Le guide a couvert comment **charger un classeur Excel C#**, localiser le `ListObject` souhaité, supprimer les lignes en toute sécurité et enregistrer le fichier mis à jour. Avec la gestion des cas limites et les conseils de performance inclus, vous pouvez adapter ce modèle à des scénarios plus complexes tels que les suppressions conditionnelles, les tableaux multiples ou les bibliothèques Excel .NET alternatives.

### Prochaines étapes

* Explorez **ClosedXML** ou **EPPlus** si vous préférez une pile entièrement open‑source.  
* Combinez la suppression de lignes avec la **validation des données** pour nettoyer les feuilles de calcul avant de les importer dans une base de données.  
* Automatisez le processus pour un dossier de classeurs en utilisant `Directory.GetFiles` et une boucle.

N'hésitez pas à expérimenter avec différentes plages de lignes, noms de tableaux et logiques conditionnelles. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Charger un fichier Excel C# – Comment supprimer des lignes et enlever des lignes spécifiques](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [Comment insérer et supprimer des lignes dans Excel avec Aspose.Cells pour .NET : Guide complet](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Comment supprimer les lignes vides dans Excel en utilisant Aspose.Cells .NET pour le nettoyage des données](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}