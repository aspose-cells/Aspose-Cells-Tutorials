---
category: general
date: 2026-08-07
description: Supprimer des lignes d’un tableau Excel avec C#. Apprenez à supprimer
  en toute sécurité les lignes de données d’Excel tout en protégeant la ligne d’en‑tête,
  en quelques étapes seulement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- remove data rows excel
- protect header row excel
language: fr
lastmod: 2026-08-07
og_description: Supprimer des lignes d’un tableau Excel par programmation. Ce guide
  vous montre comment supprimer en toute sécurité les lignes de données d’Excel et
  protéger la ligne d’en‑tête d’Excel avec Aspose.Cells.
og_image_alt: Screenshot of C# code that deletes rows from an Excel table while keeping
  the header intact
og_title: Supprimer des lignes d'un tableau Excel – solution C# rapide
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Delete rows from Excel table using C#. Learn how to remove data rows
    Excel safely while protecting header row Excel in just a few steps.
  headline: Delete rows from Excel table – complete C# guide
  type: TechArticle
- description: Delete rows from Excel table using C#. Learn how to remove data rows
    Excel safely while protecting header row Excel in just a few steps.
  name: Delete rows from Excel table – complete C# guide
  steps:
  - name: Run the program with a sample workbook that has at least five data rows.
    text: Run the program with a sample workbook that has at least five data rows.
  - name: Verify that the console prints “Rows deleted and workbook saved successfully.”
    text: Verify that the console prints “Rows deleted and workbook saved successfully.”
  - name: 'Open `TableHeaderProtected.xlsx` in Excel and confirm:'
    text: 'Open `TableHeaderProtected.xlsx` in Excel and confirm:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Data manipulation
title: Supprimer des lignes d'un tableau Excel – guide complet C#
url: /fr/net/row-and-column-management/delete-rows-from-excel-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Supprimer des lignes d'un tableau Excel – guide complet C# 

Si vous devez **delete rows from Excel table** dans un projet .NET, ce tutoriel vous montre une méthode fiable pour le faire. Que vous nettoyiez des données importées ou que vous réduisiez un rapport, vous verrez comment supprimer des lignes de données Excel tandis que l'API protège automatiquement **protect header row excel** contre la suppression accidentelle.

Dans les étapes ci‑dessous, vous apprendrez comment charger un classeur, supprimer des lignes en toute sécurité, puis enregistrer les modifications. Le guide couvre également l'erreur courante consistant à essayer de supprimer la ligne d'en‑tête et explique pourquoi la bibliothèque l'empêche. À la fin, vous pourrez **remove data rows excel** en toute confiance dans toute solution basée sur Aspose.Cells.

## Prérequis

- .NET 6.0 ou version ultérieure installé.  
- Le package NuGet **Aspose.Cells for .NET** (version 23.10 ou plus récente). Installez-le avec :

  ```bash
  dotnet add package Aspose.Cells
  ```

- Un fichier Excel (`TableWithHeader.xlsx`) contenant un tableau structuré avec une ligne d'en‑tête dans la première feuille.  
- Une connaissance de base du C# et de Visual Studio (ou tout autre IDE de votre choix).

## Étape 1 : Charger le classeur contenant un tableau avec une ligne d'en‑tête

La première opération consiste à ouvrir le classeur qui contient le tableau que vous souhaitez modifier. Aspose.Cells lit le fichier en mémoire sans nécessiter l'installation d'Excel.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the workbook from disk
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\TableWithHeader.xlsx");

        // Continue with the next steps...
```

**Pourquoi c’est important :** Le chargement du classeur crée un objet `Workbook` qui vous donne accès aux feuilles, aux tableaux et aux cellules. Sans cet objet, vous ne pouvez pas manipuler la structure Excel.

## Étape 2 : Accéder à la première feuille et à son premier tableau

La plupart des exemples simples conservent le tableau dans la première feuille et à l'index 0, mais vous pouvez ajuster les indices selon votre scénario.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (Excel table) on that worksheet
        ListObject table = worksheet.Tables[0];
```

**Pourquoi c’est important :** `ListObject` représente un tableau Excel, qui comprend la ligne d'en‑tête, les lignes de données et tout formatage. Travailler avec l'objet tableau garantit le respect de la sémantique des tableaux Excel, comme la protection de la ligne d'en‑tête.

## Étape 3 : Tenter de supprimer la ligne d'en‑tête (démonstration de la protection)

Aspose.Cells lève une exception si vous essayez de supprimer la ligne d'en‑tête parce que l'API **protect header row excel** par conception. Montrer ce comportement vous aide à comprendre pourquoi une suppression directe échoue.

```csharp
        try
        {
            // Attempt to delete the header row (index 0) and the row below it
            table.DeleteRows(0, 2);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Deletion prevented: " + ex.Message);
        }
```

**Sortie attendue**

```
Deletion prevented: Cannot delete the header row of a table.
```

**Explication :** La méthode `DeleteRows` reçoit un indice de départ basé sur zéro et un nombre. L'indice 0 pointe vers la ligne d'en‑tête, que la bibliothèque protège pour maintenir l'intégrité du tableau.

## Étape 4 : Supprimer uniquement les lignes de données – la bonne façon de **remove data rows excel**

Maintenant que vous savez que l'en‑tête est protégé, supprimez uniquement les lignes de données qui commencent après l'en‑tête. Dans la plupart des tableaux, la première ligne de données se trouve à l'indice 1.

```csharp
        // Delete three data rows starting after the header (index 1)
        table.DeleteRows(1, 3); // removes rows 2, 3, and 4 of the worksheet

        // Optionally, you can delete a single row:
        // table.DeleteRows(4, 1);
```

**Pourquoi cela fonctionne :** En commençant à l'indice 1, vous sautez l'en‑tête, donc l'opération respecte la règle **protect header row excel**. La méthode `DeleteRows` met à jour automatiquement la plage interne du tableau.

## Étape 5 : Enregistrer le classeur modifié

Enregistrez les modifications dans un nouveau fichier afin de conserver l'original intact.

```csharp
        // Save the workbook with the modified table
        workbook.Save(@"YOUR_DIRECTORY\TableHeaderProtected.xlsx");

        Console.WriteLine("Rows deleted and workbook saved successfully.");
    }
}
```

**Résultat :** Après l'exécution du programme, `TableHeaderProtected.xlsx` contient la même ligne d'en‑tête, mais les lignes de données spécifiées ont disparu. L'ouverture du fichier dans Excel montre un tableau propre sans les lignes supprimées.

## Pièges courants et comment les éviter

| Piège | Pourquoi cela se produit | Solution |
|-------|--------------------------|----------|
| Essayer de supprimer la ligne d'en‑tête | Aspose.Cells impose l'intégrité du tableau | Commencez toujours la suppression à l'indice 1 ou supérieur |
| Supprimer plus de lignes qu'il n'en existe | `DeleteRows` lève `ArgumentOutOfRangeException` | Vérifiez `table.DataRange.RowCount` avant d'appeler `DeleteRows` |
| Travailler avec une plage qui n'est pas un tableau | Les méthodes `ListObject` ne s'appliquent qu'aux tableaux structurés | Convertissez d'abord une plage en tableau (`worksheet.Tables.Add`) si nécessaire |

**Astuce :** Si vous devez effacer tout le tableau mais garder l'en‑tête, utilisez `table.DeleteRows(1, table.DataRange.RowCount - 1);`. Cela supprime chaque ligne de données quel que soit le nombre de lignes que le tableau possède actuellement.

## Alternative : Supprimer des lignes par adresse de cellule

Parfois, vous connaissez l'adresse exacte d'une cellule plutôt que l'indice de ligne. Vous pouvez convertir une adresse en indice de ligne avec la collection `Cells` :

```csharp
        // Example: delete rows that contain the value "Obsolete"
        for (int i = table.DataRange.FirstRow; i <= table.DataRange.LastRow; i++)
        {
            if (worksheet.Cells[i, table.DataRange.FirstColumn].StringValue == "Obsolete")
            {
                // Subtract one because DeleteRows expects a zero‑based index relative to the table
                table.DeleteRows(i - table.StartRow + 1, 1);
                i--; // Adjust loop counter after deletion
            }
        }
```

Cette approche est utile lorsque les lignes à supprimer sont identifiées par leur contenu plutôt que par un nombre fixe.

## Tester votre implémentation

1. Exécutez le programme avec un classeur d'exemple contenant au moins cinq lignes de données.  
2. Vérifiez que la console affiche « Rows deleted and workbook saved successfully. »  
3. Ouvrez `TableHeaderProtected.xlsx` dans Excel et confirmez :
   - La ligne d'en‑tête est toujours présente.  
   - Seules les lignes de données prévues sont manquantes.  

Si l'en‑tête disparaît, vous avez probablement commencé la suppression à l'indice 0 — revoyez **Étape 4**.

## Conclusion

Vous savez maintenant comment **delete rows from Excel table** en toute sécurité avec C#. Le guide a couvert le chargement d'un classeur, l'accès au tableau, le respect de la règle **protect header row excel**, la suppression correcte de **remove data rows excel**, et l'enregistrement du résultat. En suivant ces étapes, vous évitez les erreurs courantes et maintenez vos tableaux Excel bien structurés.

### Prochaines étapes

- Explorez les fonctionnalités d'**Aspose.Cells** comme l'insertion de lignes, l'application de styles ou le filtrage de données.  
- Combinez la suppression de lignes avec les **formules Excel** pour automatiser le nettoyage en fonction des résultats de calcul.  
- Découvrez des sujets connexes tels que **exporter Excel en CSV** ou **lire de grands classeurs efficacement**.

N'hésitez pas à expérimenter avec différents nombres de lignes, plusieurs tableaux ou des suppressions conditionnelles. Si vous rencontrez des cas particuliers, consultez à nouveau la gestion des erreurs présentée dans **Étape 3** — la bibliothèque protégera toujours la ligne d'en‑tête pour vous. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Supprimer plusieurs lignes dans Excel avec Aspose.Cells .NET : guide complet pour la manipulation de données](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [Comment insérer et supprimer des lignes dans Excel avec Aspose.Cells pour .NET : guide complet](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Comment supprimer les lignes vides dans Excel en utilisant Aspose.Cells .NET pour le nettoyage de données](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}