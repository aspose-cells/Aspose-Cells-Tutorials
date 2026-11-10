---
category: general
date: 2026-10-01
description: Apprenez à supprimer des lignes d’un tableau Excel et à modifier le nom
  du tableau Excel en utilisant C#. Guide étape par étape avec le code complet et
  les meilleures pratiques.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows excel table
- change excel table name
- load excel workbook c#
- remove rows from excel table
- update excel table name
language: fr
lastmod: 2026-10-01
og_description: Supprimez des lignes d’un tableau Excel et modifiez le nom du tableau
  Excel en C#. Suivez ce tutoriel complet pour charger un classeur, modifier le tableau
  et enregistrer le résultat.
og_image_alt: Screenshot showing C# code that deletes rows from an Excel table and
  updates the table name
og_title: Supprimer des lignes d’un tableau Excel et changer son nom en C# – guide
  complet
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn to delete rows from an Excel table and change the Excel table
    name using C#. Step‑by‑step guide with full code and best practices.
  headline: How to delete rows from an Excel table and change its name in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Comment supprimer des lignes d’un tableau Excel et changer son nom en C#
url: /fr/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment supprimer des lignes d'un tableau Excel et changer son nom en C#

Si vous devez **supprimer des lignes d'un tableau Excel** tout en travaillant avec C#, ce guide montre les étapes exactes requises. Vous verrez comment **charger un classeur Excel en C#**, supprimer des lignes spécifiques d'un tableau, puis **mettre à jour le nom du tableau Excel** afin que le fichier reste cohérent.

Le tutoriel couvre tout ce que vous devez savoir : les packages NuGet requis, du code complet et exécutable, ainsi que les pièges courants tels que les violations de la structure du tableau. À la fin de l'article, vous pourrez modifier n'importe quel tableau Excel de manière programmatique sans intervention manuelle.

## Prérequis

Avant de commencer, assurez‑vous d'avoir :

* .NET 6.0 SDK ou version ultérieure installé.
* Visual Studio 2022 (ou tout IDE C#) configuré pour le développement .NET.
* La bibliothèque **Aspose.Cells for .NET** ajoutée via NuGet (`Install-Package Aspose.Cells`).
* Un classeur Excel existant (`Table.xlsx`) contenant au moins une feuille avec un tableau.

Ces éléments fournissent l'environnement nécessaire pour le code **load Excel workbook c#** et exécuter les opérations de manière fiable.

## Étape 1 : Charger le classeur contenant le tableau

La première opération consiste à ouvrir le fichier du classeur. Aspose.Cells lit l'intégralité du classeur en mémoire, vous donnant un contrôle complet sur les feuilles, les tableaux et les données des cellules.

```csharp
using Aspose.Cells;

string inputPath = @"C:\Data\Table.xlsx";

// Load the workbook from disk
Workbook workbook = new Workbook(inputPath);
```

*Pourquoi c'est important* : charger le classeur constitue la base de toute manipulation de tableau ultérieure. L'objet `Workbook` expose la collection `Worksheets`, que vous utiliserez pour localiser le tableau cible.

## Étape 2 : Accéder à la première feuille et à son premier tableau

La plupart des fichiers Excel stockent les tableaux dans la première feuille, mais vous pouvez ajuster l'index si nécessaire. Le code suivant récupère le premier objet `Table`.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Retrieve the first table on that worksheet
Table table = sheet.Tables[0];
```

Si la feuille ne contient pas de tableau, `sheet.Tables.Count` sera zéro et vous devrez gérer ce cas. Tenter d'accéder à `sheet.Tables[0]` lorsqu'aucun tableau n'existe génère une exception, c'est pourquoi une clause de garde est recommandée dans le code de production.

## Étape 3 : Supprimer des lignes du tableau Excel

Pour **supprimer des lignes d'un tableau Excel**, appelez `DeleteRows(startRow, totalRows)`. Le paramètre `startRow` est indexé à zéro par rapport à la première ligne de données du tableau (la ligne après l'en-tête).

```csharp
// Delete two rows starting from the second data row (index 1)
int startRow = 1;   // second row within the table
int rowsToDelete = 2;

table.DeleteRows(startRow, rowsToDelete);
```

### Pourquoi utiliser `DeleteRows` au lieu de supprimer des lignes de la feuille ?

`DeleteRows` met à jour la plage interne du tableau, préservant les formules, les styles et les noms définis qui appartiennent au tableau. Supprimer directement des lignes de la feuille pourrait casser la structure du tableau et déclencher une exception.

**Cas limite** : si la suppression laisse le tableau sans lignes de données, Aspose.Cells lève une `ArgumentException`. Protégez‑vous en vérifiant `table.RowCount` avant la suppression.

```csharp
if (table.RowCount - rowsToDelete < 1)
{
    throw new InvalidOperationException("Cannot delete all data rows from the table.");
}
```

## Étape 4 : Modifier le nom du tableau Excel

Après la suppression des lignes, vous pouvez vouloir donner au tableau un identifiant plus descriptif. La propriété `Name` définit le nom du tableau, utilisé dans les formules et VBA.

```csharp
// Assign a new name to the table
string newTableName = "SalesData2026";

if (workbook.Worksheets.GetDefinedNames().Any(d => d.Text == newTableName))
{
    throw new InvalidOperationException($"The name '{newTableName}' already exists as a defined name.");
}

table.Name = newTableName;
```

*Pourquoi renommer ?* Un nom de tableau clair améliore la lisibilité dans les formules (`=SUM(SalesData2026[Amount])`) et évite les collisions de noms lorsque plusieurs tableaux partagent des objectifs similaires.

## Étape 5 : Enregistrer le classeur modifié (optionnel)

Conservez les modifications en enregistrant dans un nouveau fichier ou en écrasant l'original. Enregistrer à un nouvel emplacement est plus sûr pendant le développement.

```csharp
string outputPath = @"C:\Data\ModifiedTable.xlsx";
workbook.Save(outputPath);
```

La méthode `Save` écrit le classeur mis à jour, incluant la plage du tableau modifiée et le nouveau nom du tableau, sur le disque.

## Exemple complet fonctionnel

Assembler toutes les étapes donne un programme autonome que vous pouvez exécuter immédiatement.

```csharp
using System;
using System.Linq;
using Aspose.Cells;

class ExcelTableModifier
{
    static void Main()
    {
        // ----- Step 1: Load workbook -----
        string inputPath = @"C:\Data\Table.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // ----- Step 2: Access worksheet and table -----
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Tables.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        Table table = sheet.Tables[0];

        // ----- Step 3: Delete rows -----
        int startRow = 1;      // second data row (zero‑based)
        int rowsToDelete = 2;

        if (table.RowCount - rowsToDelete < 1)
        {
            Console.WriteLine("Deletion would remove all data rows; operation aborted.");
            return;
        }

        table.DeleteRows(startRow, rowsToDelete);
        Console.WriteLine($"{rowsToDelete} rows removed starting at index {startRow}.");

        // ----- Step 4: Change table name -----
        string newTableName = "SalesData2026";

        bool nameExists = workbook.Worksheets.GetDefinedNames()
                               .Any(d => d.Text.Equals(newTableName, StringComparison.OrdinalIgnoreCase));

        if (nameExists)
        {
            Console.WriteLine($"The name '{newTableName}' already exists. Choose a different name.");
            return;
        }

        table.Name = newTableName;
        Console.WriteLine($"Table renamed to '{newTableName}'.");

        // ----- Step 5: Save workbook -----
        string outputPath = @"C:\Data\ModifiedTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to '{outputPath}'.");
    }
}
```

**Sortie attendue** (en supposant que le fichier et le tableau existent) :

```
2 rows removed starting at index 1.
Table renamed to 'SalesData2026'.
Modified workbook saved to 'C:\Data\ModifiedTable.xlsx'.
```

L'exécution du programme met à jour le fichier Excel exactement comme décrit : les lignes sont supprimées, le nom du tableau change, et le résultat est enregistré sans édition manuelle.

## Questions fréquentes et dépannage

| Question | Réponse |
|----------|--------|
| *Que se passe-t-il si le tableau s'étend sur des cellules fusionnées ?* | `DeleteRows` respecte les plages fusionnées. Si une cellule fusionnée traverse la frontière de suppression, Aspose.Cells ajuste automatiquement la fusion. Vérifiez le résultat visuellement si vous comptez sur des fusions complexes. |
| *Puis-je supprimer des lignes d'un tableau qui fait partie d'un cache de tableau croisé dynamique ?* | Supprimer des lignes d'un tableau source qui alimente un tableau croisé dynamique ne **rafraîchit pas** automatiquement le cache du tableau croisé. Appelez `pivotTable.RefreshData()` après avoir modifié le tableau source. |
| *Est-il possible de supprimer des lignes en fonction d'une condition (par ex., valeur < 0) ?* | Oui. Parcourez `table.ListObjects` ou `table.Rows` pour localiser les lignes correspondantes, puis collectez leurs indices et appelez `DeleteRows` pour chaque plage. |
| *Dois‑je libérer l'objet `Workbook` ?* | `Workbook` implémente `IDisposable`. Enveloppez‑le dans un bloc `using` pour une libération déterministe des ressources, surtout lors du traitement de gros fichiers. |
| *En quoi cela diffère‑t‑il de l'utilisation d'EPPlus ?* | EPPlus prend également en charge la manipulation de tableaux mais utilise une API différente (`ExcelTable`). Les concepts de chargement d'un classeur, de suppression de lignes et de renommage du tableau sont analogues. Choisissez la bibliothèque qui correspond à vos exigences de licence. |

## Bonnes pratiques lors de la modification de tableaux Excel en C#

* **Valider les index** – Les index des lignes du tableau sont à zéro ; les erreurs d'offset d'une unité entraînent des suppressions inattendues.
* **Vérifier les collisions de noms** – Excel n'autorise pas les noms définis en double ; vérifiez toujours l'unicité avant d'attribuer un nouveau nom.
* **Sauvegarder les fichiers originaux** – Les scripts automatisés peuvent corrompre les données ; conservez une copie du classeur source.
* **Utiliser les instructions `using`** – Garantit que les poignées de fichiers sont libérées rapidement :

```csharp
using (Workbook wb = new Workbook(inputPath))
{
    // modify workbook
}
```

* **Tester avec des cas limites** – Les tableaux avec une seule ligne de données, les tableaux qui couvrent toute la feuille, et les tableaux liés à des graphiques doivent être vérifiés après les modifications.

## Conclusion

Vous savez maintenant comment **supprimer des lignes d'un tableau Excel** et **modifier le nom du tableau Excel** en utilisant C#. La solution complète charge le classeur, accède au tableau cible, supprime les lignes souhaitées, renomme le tableau et enregistre le résultat. Appliquez ces techniques pour automatiser la génération de rapports, le nettoyage de données ou tout flux de travail nécessitant une gestion programmatique des tableaux Excel.

Ensuite, explorez des sujets connexes tels que **mettre à jour les valeurs des cellules dans un tableau Excel**, **ajouter de nouvelles lignes programmatique** et **exporter les données du tableau vers CSV**. Maîtriser ces opérations vous donnera un contrôle complet sur les fichiers Excel depuis vos applications C#.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment renommer un tableau dans Excel avec C# – Guide étape par étape](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Créer un tableau Excel en C# – Guide étape par étape](/cells/english/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/)
- [Obtenir le premier tableau d'un classeur Excel en C# – Guide complet](/cells/english/net/excel-autofilter-validation/get-first-table-from-excel-workbook-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}