---
category: general
date: 2026-03-22
description: Aspose Cells supprime des lignes tout en protégeant la ligne d’en‑tête.
  Apprenez comment récupérer la première table et supprimer en toute sécurité les
  lignes d’une table Excel en C#.
draft: false
keywords:
- aspose cells delete rows
- protect header row
- delete excel table rows
- retrieve first table
language: fr
og_description: Aspose Cells supprime des lignes tout en protégeant la ligne d’en-tête.
  Apprenez à récupérer la première table et à supprimer en toute sécurité les lignes
  d’une table Excel en C#.
og_title: Aspose Cells Supprimer des lignes – Protéger la ligne d’en-tête dans Excel
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose Cells Supprimer des lignes – Protéger la ligne d’en-tête dans Excel
url: /fr/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells Delete Rows – Protéger la ligne d’en‑tête dans Excel

Vous avez déjà essayé de **aspose cells delete rows** d’un tableau pour découvrir que l’en‑tête avait disparu ? C’est un piège courant lors de la manipulation programmatique des feuilles Excel. Dans ce guide, nous parcourrons une solution complète et exécutable qui **protège la ligne d’en‑tête**, vous montre comment **retrieve first table**, et supprime en toute sécurité les **delete Excel table rows** sans casser la structure.

Nous couvrirons tout, du chargement du classeur à la gestion de l’exception qu’Aspose lance lorsque vous essayez d’abandonner l’en‑tête. À la fin, vous disposerez d’un modèle solide que vous pourrez intégrer à n’importe quel projet .NET utilisant Aspose.Cells.

---

## Ce dont vous avez besoin

- **Aspose.Cells for .NET** (v23.12 ou ultérieur) – la bibliothèque qui vous permet de travailler avec des fichiers Excel sans Office installé.  
- Un environnement de développement C# de base (Visual Studio, Rider ou le `dotnet` CLI).  
- Un fichier Excel (`TableWithHeader.xlsx`) contenant au moins un **ListObject** (tableau Excel) avec une ligne d’en‑tête dans la première ligne.

Aucun package NuGet supplémentaire n’est requis au-delà d’Aspose.Cells.

---

## Étape 1 : Charger le classeur et récupérer le premier tableau  

La première chose à faire est d’ouvrir le classeur et de récupérer le tableau que vous souhaitez modifier. C’est ici que le mot‑clé secondaire **retrieve first table** entre en jeu.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains a table with a header row
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\TableWithHeader.xlsx");

        // Access the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Retrieve the first table (ListObject) on the worksheet
        ListObject table = worksheet.ListObjects[0];

        // Continue with row deletion...
        DeleteRowsSafely(table);
    }
}
```

**Pourquoi c’est important :**  
- `Workbook` lit le fichier sans nécessiter Excel installé.  
- `worksheet.ListObjects[0]` est la façon la plus directe de **retrieve first table** ; si vous avez plusieurs tableaux, vous pouvez itérer ou utiliser le nom du tableau.

> **Astuce :** Si vous n’êtes pas sûr qu’une feuille de calcul contienne réellement un tableau, vérifiez d’abord `worksheet.ListObjects.Count` pour éviter une `IndexOutOfRangeException`.

---

## Étape 2 : Protéger la ligne d’en‑tête lors de la suppression des lignes  

Voici le cœur du problème : **aspose cells delete rows** sans effacer l’en‑tête. La méthode `DeleteRows` d’Aspose prend un indice de départ basé sur zéro et un nombre. Tenter de supprimer l’en‑tête (ligne 0) déclenche une exception, ce que nous voulons absolument éviter.

```csharp
static void DeleteRowsSafely(ListObject table)
{
    try
    {
        // Attempt to delete rows 2‑3 (the header is row 1 in Excel, index 0 in code)
        // Here we start at index 1 (second row) and delete 2 rows.
        table.DeleteRows(1, 2);
        Console.WriteLine("Rows deleted successfully.");
    }
    catch (Exception ex)
    {
        // The API throws an exception because the header would be removed
        Console.WriteLine("Operation blocked: " + ex.Message);
    }

    // Save the workbook to verify the result
    table.Worksheet.Workbook.Save(@"YOUR_DIRECTORY\Result.xlsx");
}
```

**Explication de la logique :**  

| Étape | Raison |
|------|--------|
| `table.DeleteRows(1, 2);` | L’indice 1 pointe sur la **deuxième** ligne (la première ligne de données). Supprimer deux lignes enlève les lignes 2‑3 en termes Excel, laissant l’en‑tête (ligne 1) intacte. |
| `catch (Exception ex)` | Aspose lance une exception **uniquement** lorsque l’opération isolerait l’en‑tête. La capturer vous permet d’enregistrer un message convivial au lieu de faire planter l’application. |
| `Save` | La persistance des modifications vous permet d’ouvrir `Result.xlsx` et de voir que l’en‑tête est toujours présent. |

> **Et si vous devez vraiment supprimer l’en‑tête ?**  
> Utilisez `table.ShowHeaders = false;` avant la suppression, ou supprimez le tableau entier et recréez‑le. Mais dans la plupart des scénarios métier, vous voudrez **protect header row**.

---

## Étape 3 : Vérifier le résultat – Sortie attendue  

Après avoir exécuté le programme, ouvrez `Result.xlsx`. Vous devriez voir :

- La première ligne contient toujours les titres de colonnes d’origine.  
- Les lignes 2‑3 (celles que nous avons ciblées) ont disparu, et les données restantes ont été décalées vers le haut.

La console affichera :

```
Rows deleted successfully.
```

Si vous avez accidentellement tenté de supprimer l’en‑tête (par ex., `table.DeleteRows(0, 1);`), la sortie serait :

```
Operation blocked: Cannot delete header row of the table.
```

Ce message confirme que la protection intégrée d’Aspose fonctionne comme prévu.

---

## Étape 4 : Méthodes alternatives pour **Delete Excel Table Rows**  

Parfois, vous avez besoin de plus de contrôle — par exemple supprimer des lignes selon une condition, ou enlever des lignes non contiguës. Voici deux modèles rapides qui préservent l’en‑tête.

### 4.1 Supprimer des lignes par filtre de données  

```csharp
static void DeleteRowsByCondition(ListObject table, string columnName, string valueToRemove)
{
    // Find the column index by name
    int colIndex = table.ListColumns[columnName].Index;

    // Iterate backwards to avoid messing up row indices
    for (int i = table.DataRange.RowCount - 1; i >= 0; i--)
    {
        var cell = table.DataRange[i, colIndex];
        if (cell.StringValue.Equals(valueToRemove, StringComparison.OrdinalIgnoreCase))
        {
            // Delete the row (add 1 because DataRange is zero‑based inside the table)
            table.DeleteRows(i + 1, 1);
        }
    }
}
```

### 4.2 Suppression en masse à l’aide d’une plage  

```csharp
// Delete rows 5‑10 (still preserving the header)
table.DeleteRows(4, 6);   // 4 = 5th row in Excel, 6 = number of rows to delete
```

Les deux extraits respectent la règle **protect header row** car l’indice de départ ne descend jamais en dessous de 1.

---

## Étape 5 : Pièges courants et comment les éviter  

| Piège | Pourquoi cela se produit | Solution |
|---------|----------------|-----|
| Suppression accidentelle de l’en‑tête | Utilisation de `0` comme indice de départ | Commencez toujours à `1` pour les lignes de données, ou vérifiez d’abord `table.ShowHeaders`. |
| `IndexOutOfRangeException` lorsque la feuille ne contient aucun tableau | Supposer qu’un tableau existe | Vérifiez que `worksheet.ListObjects.Count > 0` avant d’accéder à `[0]`. |
| Modifications non enregistrées | Oublier d’appeler `Save` | Appelez `workbook.Save` après les modifications. |
| Supprimer des lignes au milieu décale les indices, entraînant des sauts | Itération en avant lors de la suppression | Itérez **en arrière** ou collectez d’abord les lignes à supprimer. |

---

## Étape 6 : Assembler le tout – Exemple complet fonctionnel  

```csharp
using System;
using Aspose.Cells;

class AsposeDeleteRowsDemo
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\TableWithHeader.xlsx");
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Ensure a table exists
        if (sheet.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // 3️⃣ Retrieve the first table (retrieve first table)
        ListObject table = sheet.ListObjects[0];

        // 4️⃣ Delete rows safely (aspose cells delete rows while protecting header row)
        DeleteRowsSafely(table);

        // 5️⃣ (Optional) Delete rows by condition
        // DeleteRowsByCondition(table, "Status", "Closed");

        // 6️⃣ Save the result
        workbook.Save(@"YOUR_DIRECTORY\Result.xlsx");
        Console.WriteLine("Workbook saved as Result.xlsx");
    }

    static void DeleteRowsSafely(ListObject table)
    {
        try
        {
            // Delete rows 2‑3 (header stays intact)
            table.DeleteRows(1, 2);
            Console.WriteLine("Rows deleted successfully.");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Operation blocked: " + ex.Message);
        }
    }

    // Uncomment if you need conditional deletion
    /*
    static void DeleteRowsByCondition(ListObject table, string columnName, string valueToRemove)
    {
        int colIdx = table.ListColumns[columnName].Index;
        for (int i = table.DataRange.RowCount - 1; i >= 0; i--)
        {
            var cell = table.DataRange[i, colIdx];
            if (cell.StringValue.Equals(valueToRemove, StringComparison.OrdinalIgnoreCase))
            {
                table.DeleteRows(i + 1, 1);
            }
        }
    }
    */
}
```

Exécutez ce programme, ouvrez `Result.xlsx`, et vous verrez l’en‑tête intacte tandis que les lignes sélectionnées ont disparu. C’est la **solution complète et autonome** pour **aspose cells delete rows** sans sacrifier l’en‑tête.

---

## Conclusion  

Nous venons de démontrer comment **aspose cells delete rows** tout en **protecting the header row**, comment **retrieve first table**, et plusieurs méthodes pour **delete excel table rows** en toute sécurité. Les points clés sont :

- Commencez toujours les suppressions à l’indice 1 pour garder l’en‑tête intacte.  
- Utilisez `try/catch` pour gérer l’exception de protection intégrée d’Aspose.  
- Vérifiez l’existence du tableau avant d’opérer, et itérez en arrière lors de la suppression conditionnelle de lignes.

Prêt à passer à la vitesse supérieure ? Essayez de combiner cette approche avec les API de style d’**Aspose Cells** pour mettre en évidence les lignes supprimées avant la suppression, ou automatisez le processus sur plusieurs feuilles de calcul. Les possibilités sont infinies, et vous disposez maintenant d’un modèle fiable sur lequel construire.

Si vous avez trouvé ce tutoriel utile, donnez‑lui un pouce en l’air, partagez‑le avec vos collègues, ou laissez un commentaire avec vos propres solutions de cas limites. Bon codage !  

---

![Exemple de suppression de lignes Aspose Cells – En‑tête protégé](https://example.com/images/aspose-delete-rows.png "aspose cells delete rows")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}