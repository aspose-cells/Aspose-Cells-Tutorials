---
category: general
date: 2026-11-25
description: Apprenez à supprimer des lignes d’un tableau Excel en C# et à supprimer
  également plusieurs lignes d’une feuille Excel efficacement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- delete multiple rows from excel sheet
language: fr
lastmod: 2026-11-25
og_description: Supprimez des lignes d’un tableau Excel en C# et apprenez à supprimer
  plusieurs lignes d’une feuille Excel avec un code propre.
og_image_alt: Screenshot of C# code deleting rows from an Excel table
og_title: Supprimer des lignes d'un tableau Excel en C# – guide complet
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  headline: How to delete rows from Excel table with C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  name: How to delete rows from Excel table with C#
  steps:
  - name: Add Aspose.Cells to your project
    text: 'Open the **Package Manager Console** and run:'
  - name: Load the workbook and locate the table
    text: '```csharp using Aspose.Cells;'
  - name: Delete the desired data rows
    text: The `DeleteRows` method expects a **zero‑based** row index relative to the
      table, **including** the header row. Because the header cannot be removed, you
      must start at index 1 for the first data row.
  - name: Save the modified workbook
    text: '```csharp // Save the workbook to a new file to preserve the original workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
      } } ```'
  - name: Full working example
    text: '```csharp using Aspose.Cells;'
  - name: Edge cases and best practices
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Deleting rows beyond the last row | Check `worksheet.Rows.Count` before calling
      `RemoveAt`. | | Removing all rows except the header | Delete data rows in a
      loop or use `DeleteRows(1, table.DataRa'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
- data manipulation
title: Comment supprimer des lignes d'un tableau Excel avec C#
url: /fr/net/row-and-column-management/how-to-delete-rows-from-excel-table-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment supprimer des lignes d'un tableau Excel avec C#

Si vous devez supprimer des lignes d'un tableau Excel en utilisant C#, ce guide vous montre exactement comment le faire. Vous verrez également comment supprimer plusieurs lignes d'une feuille Excel sans affecter les autres données.

Travailler avec Excel de manière programmatique nécessite souvent de supprimer des enregistrements obsolètes ou invalides. Supprimer des lignes directement dans une feuille de calcul peut être risqué car la ligne d'en-tête d'un tableau structuré doit rester intacte. Ce tutoriel vous guide à travers une approche sûre qui respecte l'en-tête du tableau et vous permet de supprimer n'importe quel nombre de lignes de données en un seul appel.

## Prérequis

* .NET 6.0 ou version ultérieure installé  
* Visual Studio 2022 (ou tout IDE compatible)  
* Le package NuGet **Aspose.Cells** (version 23.10 ou plus récente) – cette bibliothèque fournit les classes `Workbook`, `Worksheet` et `ListObject` utilisées dans les exemples  

Vous n'avez pas besoin d'installer Microsoft Office sur la machine de développement car Aspose.Cells travaille directement avec le format de fichier.

## Supprimer des lignes d'un tableau Excel – étape par étape

Les sections suivantes décrivent chaque étape nécessaire pour supprimer des lignes d'un tableau Excel en toute sécurité. Le mot‑clé principal apparaît dans ce titre pour répondre aux exigences SEO.

### Étape 1 : Ajouter Aspose.Cells à votre projet

Ouvrez la **Package Manager Console** et exécutez :

```powershell
Install-Package Aspose.Cells
```

Le package ajoute les assemblages nécessaires et résout les types `Workbook`, `Worksheet` et `ListObject`.

### Étape 2 : Charger le classeur et localiser le tableau

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Load the workbook that contains the table
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // Access the first worksheet (index 0)
        var worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (structured table) on the sheet
        var table = worksheet.ListObjects[0];
```

*Pourquoi c'est important* : le `ListObject` représente un vrai tableau Excel, qui conserve sa propre ligne d'en-tête. En travaillant avec le `ListObject`, vous évitez la suppression accidentelle de l'en-tête.

### Étape 3 : Supprimer les lignes de données souhaitées

La méthode `DeleteRows` attend un indice de ligne **à base zéro** relatif au tableau, **incluant** la ligne d'en-tête. Comme l'en-tête ne peut pas être supprimé, vous devez commencer à l'indice 1 pour la première ligne de données.

```csharp
        // Delete two data rows starting after the header (index 1)
        // Parameters: startRow (relative to the table), numberOfRows
        table.DeleteRows(1, 2);
```

Si vous essayez `table.DeleteRows(0, 2)`, Aspose.Cells lèvera une exception car la ligne d'en-tête (indice 0) est protégée. Commencer à l'indice 1 garantit que seules les lignes de données sont supprimées.

### Étape 4 : Enregistrer le classeur modifié

```csharp
        // Save the workbook to a new file to preserve the original
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

L'exécution du programme supprime les deux lignes situées immédiatement sous l'en-tête tout en laissant la structure du tableau intacte.

### Exemple complet fonctionnel

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // 1. Load workbook
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // 2. Access first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3. Get the first table (ListObject)
        var table = worksheet.ListObjects[0];

        // 4. Delete two rows after the header (cannot delete header itself)
        table.DeleteRows(1, 2);

        // 5. Save the result
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

**Sortie attendue** : le fichier `table_with_header_modified.xlsx` contient l'en-tête du tableau original, suivi de toutes les lignes sauf les deux qui ont été supprimées. Aucune autre feuille de calcul n'est modifiée.

## Supprimer plusieurs lignes d'une feuille Excel

Parfois, vous devez supprimer des lignes qui **n'appartiennent pas** à un tableau structuré. Le mot‑clé secondaire apparaît dans ce titre. L'approche diffère légèrement car vous travaillez avec la collection `Rows` de la feuille de calcul plutôt qu'avec un `ListObject`.

```csharp
using Aspose.Cells;

class SheetRowDeletion
{
    static void Main()
    {
        var workbook = new Workbook(@"C:\Data\plain_sheet.xlsx");
        var worksheet = workbook.Worksheets[0];

        // Delete rows 5 through 9 (inclusive) – zero‑based index
        // The second argument is the count of rows to remove
        worksheet.Rows.RemoveAt(4, 5);

        workbook.Save(@"C:\Data\plain_sheet_modified.xlsx");
    }
}
```

**Pourquoi cela fonctionne** : `Rows.RemoveAt(startIndex, count)` supprime un bloc contigu de lignes directement de la feuille de calcul. Il n'y a pas de protection d'en-tête, vous pouvez donc commencer à n'importe quel indice. La méthode est efficace car elle met à jour les structures de données internes en une seule opération, ce qui est idéal lorsque vous devez supprimer plusieurs lignes d'une feuille Excel.

### Cas limites et bonnes pratiques

| Situation                               | Recommandation |
|----------------------------------------|----------------|
| Supprimer des lignes au‑delà de la dernière ligne | Vérifier `worksheet.Rows.Count` avant d'appeler `RemoveAt`. |
| Supprimer toutes les lignes sauf l'en‑tête | Supprimer les lignes de données dans une boucle ou utiliser `DeleteRows(1, table.DataRange.RowCount - 1)`. |
| Conserver le format des cellules | La suppression via `ListObject` décale automatiquement le format ; pour les feuilles brutes, copier le format avant la suppression si nécessaire. |
| Grandes feuilles de calcul (> 10 000 lignes) | Effectuer les suppressions dans l'ordre décroissant pour éviter le décalage d'indices, ou utiliser `DeleteRows` sur le tableau si possible. |

**Astuce** : lorsque vous devez supprimer des lignes en fonction d'une condition (par ex., les lignes où la valeur d'une colonne est vide), parcourez le `DataRange` du tableau à l'envers et appelez `DeleteRows` pour chaque ligne correspondante. La suppression en sens inverse évite le désalignement des indices.

## Questions fréquentes

*Cette méthode fonctionne‑t‑elle avec les fichiers .xlsx créés par Excel 365 ?*  
Oui. Aspose.Cells prend en charge la spécification complète Office Open XML, donc le même code fonctionne avec n'importe quel fichier `.xlsx` moderne.

*Que faire si le classeur contient plusieurs tableaux ?*  
Récupérez le tableau souhaité par son nom : `var table = worksheet.ListObjects["MyTable"];` puis appliquez `DeleteRows` comme indiqué.

*Puis‑je supprimer des lignes sans utiliser de bibliothèque tierce ?*  
Vous pourriez utiliser l’interop COM Microsoft.Office.Interop.Excel, mais cela nécessite qu'Excel soit installé sur le serveur et introduit une surcharge liée à COM. Aspose.Cells offre une alternative légère et sûre pour le serveur.

## Conclusion

Vous savez maintenant comment supprimer des lignes d'un tableau Excel en toute sécurité et comment supprimer plusieurs lignes d'une feuille Excel en utilisant C#. La technique principale repose sur la méthode `ListObject.DeleteRows`, qui respecte l'en‑tête du tableau, tandis que la technique secondaire utilise `Rows.RemoveAt` pour les feuilles simples. Appliquez ces modèles pour nettoyer les données, automatiser la génération de rapports ou implémenter des fonctionnalités de modification en masse dans vos applications.

**Étapes suivantes**

* Explorez d'autres fonctionnalités d'Aspose.Cells telles que l'insertion de lignes, la copie de styles ou le filtrage de données.  
* Essayez les mêmes opérations avec **ClosedXML** si vous préférez une bibliothèque open‑source ; l'API est similaire mais utilise `IXLTable` et `IXLRows`.  
* Combinez la logique de suppression de lignes avec des requêtes LINQ pour créer des pipelines de nettoyage de données plus complexes.  

Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [comment supprimer des lignes dans Excel avec C# – protéger l'en‑tête du tableau](/cells/english/net/row-and-column-management/how-to-delete-rows-in-excel-with-c-protect-table-header/)
- [Comment utiliser Aspose.Cells pour supprimer des lignes d'un tableau Excel tout en conservant l'en‑tête](/cells/english/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/)
- [Charger un fichier Excel C# – Comment supprimer des lignes et enlever des lignes spécifiques](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}