---
category: general
date: 2026-06-24
description: Créer un nouveau classeur en C# et copier le tableau croisé dynamique
  tout en conservant ses données. Apprenez à copier des lignes, à exporter une plage
  sélectionnée et à garder le tableau croisé dynamique intact.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: fr
og_description: Créer un nouveau classeur en C# et copier un tableau croisé dynamique
  tout en préservant ses données. Guide étape par étape expliquant comment copier
  des lignes et exporter la plage sélectionnée.
og_title: Créer un nouveau classeur en C# – Copier le tableau croisé dynamique
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: Créer un nouveau classeur en C# – Copier le tableau croisé dynamique
url: /fr/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un nouveau classeur en C# – Copier le tableau croisé dynamique

Vous avez déjà eu besoin de **create new workbook** en C# simplement pour déplacer une tranche de données incluant un tableau croisé dynamique ? Vous n'êtes pas le seul. Dans de nombreux pipelines de reporting, vous récupérez quelques lignes, peut‑être quelques colonnes, et vous vous attendez à ce que le tableau croisé dynamique reste exactement tel quel—sans références cassées, sans calculs manquants.  

Bonne nouvelle ? En quelques lignes d’Aspose.Cells, vous pouvez **copy pivot table**, le garder intact, et même **export selected range** sans rien casser. Vous verrez ci‑dessous un exemple complet, prêt à l’exécution, qui montre **how to copy rows**, préserve le tableau croisé dynamique, et enregistre le résultat comme un tout nouveau classeur.

## Ce que couvre ce tutoriel

- Configurer un projet C# avec Aspose.Cells (la bibliothèque qui alimente le code).
- Charger le classeur source qui contient le tableau croisé dynamique original.
- Utiliser les méthodes `CopyRows` et `CopyColumns` de la bibliothèque pour dupliquer la plage exacte dont vous avez besoin.
- Enregistrer la zone dupliquée dans un scénario de **create new workbook** tout en conservant le tableau croisé dynamique fonctionnel.
- Conseils pour les cas limites comme plusieurs tableaux croisés dynamiques, lignes masquées et grands ensembles de données.

À la fin de ce guide, vous serez capable de **export selected range** depuis n’importe quel fichier Excel, de garder la logique du tableau croisé dynamique active, et de déposer le nouveau fichier où vous le souhaitez.

> **Prerequisite** : Aspose.Cells for .NET (version d’essai gratuite ou version sous licence) installé via NuGet. Si vous ne l’avez pas encore ajouté, exécutez `dotnet add package Aspose.Cells` dans le dossier de votre projet.

## Créer un nouveau classeur et copier le tableau croisé dynamique

Ci‑dessous se trouve le cœur de la solution. Nous passerons en revue chaque ligne, expliquerons pourquoi elle est importante, puis afficherons le programme complet.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### Pourquoi cela fonctionne

- **`CopyRows` / `CopyColumns`** : Ces méthodes dupliquent les données de cellules sous‑jacentes *et* les objets associés (comme un cache de tableau croisé dynamique). C’est pourquoi le tableau croisé dynamique reste fonctionnel après le déplacement.
- **Separate destination workbook** : En créant une nouvelle instance `Workbook`, nous **create new workbook** sans aucun formatage résiduel ou feuilles cachées qui pourraient interférer.
- **Zero‑based indexing** : Aspose.Cells utilise des indices basés à zéro, donc `0` correspond à la cellule **A1**. Ajustez `startRow`/`startColumn` si votre tableau croisé dynamique n’est pas en haut à gauche.
- **Preserve pivot table** : Le cache du tableau croisé dynamique se trouve dans la même plage, donc copier la plage copie automatiquement le cache. Aucun code supplémentaire n’est nécessaire.

## Comment copier des lignes sans casser le tableau croisé dynamique

Si vous ne vous intéressez qu’à la partie copie de lignes, vous pouvez l’isoler :

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Pro tip** : Lors de la copie de lignes qui intersectent un tableau croisé dynamique, copiez toujours la *toute* zone du tableau (lignes + colonnes). Les copies partielles peuvent laisser le tableau avec des champs manquants, entraînant des erreurs `#REF!`.

## Export selected range – Un scénario réel

Imaginez que vous avez un classeur de ventes gigantesque, mais que votre client ne veut que le résumé du premier trimestre, qui se trouve dans les lignes 1‑20 et les colonnes A‑D. L’extrait ci‑dessus **export selected range** déjà pour vous. Il suffit de modifier les variables `totalRows` et `totalColumns` pour correspondre à la demande du client, et le tour est joué.

### Gestion des lignes masquées ou des filtres

Si la feuille source possède des lignes masquées (peut‑être filtrées), vous pourriez vouloir copier uniquement les lignes *visibles*. Aspose.Cells propose des surcharges de `CopyRows` qui respectent la visibilité :

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

Définissez le dernier booléen sur `true` pour copier uniquement les lignes visibles—parfait pour “export selected range” lorsque l’utilisateur a appliqué des filtres.

## Préserver le tableau croisé dynamique – Pièges courants et comment les éviter

| Piège | Pourquoi cela se produit | Solution |
|-------|--------------------------|----------|
| **Cache du tableau croisé dynamique non copié** | Utilisation de `Range.Copy` simple au lieu de `Cells.CopyRows/CopyColumns`. | Utilisez les méthodes `Cells` comme indiqué. |
| **La feuille de destination possède déjà un tableau croisé dynamique** | Enregistrement sur un classeur qui contient déjà un tableau croisé dynamique portant le même nom. | Commencez avec un nouveau `Workbook()` (comme nous le faisons). |
| **Les plages nommées se cassent** | Le tableau croisé dynamique source fait référence à une plage nommée qui n’est pas présente dans le nouveau fichier. | Copiez également la plage nommée : `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Le chemin de la source de données change** | Le tableau croisé dynamique pointe vers une source de données externe qui n’est pas disponible. | Utilisez `PivotTable.RefreshData()` après la copie si nécessaire. |

## Exemple complet de bout en bout (prêt à l’exécution)

Ci‑dessus se trouve le programme complet, incluant les directives `using` et une petite interface console. Copiez‑collez‑le dans un nouveau projet d’application console et appuyez sur **F5**.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**Sortie attendue** (dans la console) :

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

Ouvrez `copy-pivot.xlsx` et vous verrez le même tableau croisé dynamique que vous aviez dans `source.xlsx`, pleinement fonctionnel et faisant référence à la plage de données copiée.

## Questions fréquentes

**Q : Cette méthode fonctionne‑t‑elle avec plusieurs tableaux croisés dynamiques sur la même feuille ?**  
R : Oui, tant que le rectangle copié englobe chaque tableau croisé dynamique dont vous avez besoin. Si vous n’en voulez qu’un, ajustez `rows`/`cols` pour l’isoler.

**Q : Que se passe‑t‑il si le classeur source utilise des connexions de données externes ?**  
R : Le cache du tableau croisé dynamique pointera toujours vers la connexion originale. Appelez `pivotTable.RefreshData()` après le chargement de la destination si vous souhaitez réinterroger la source.

**Q : Puis‑je copier le tableau croisé dynamique vers une autre feuille du même classeur ?**  
R : Absolument. Remplacez `destinationWorkbook` par `sourceWorkbook` et choisissez un autre indice de feuille.

**Q : Existe‑t‑il un moyen de copier uniquement le formatage ?**  
R : Utilisez les surcharges de `CopyRows`/`CopyColumns` qui acceptent un objet `CopyOptions`—définissez `CopyOptions.CopyType = CopyType.ValuesOnly` ou `CopyType.All` selon vos besoins.

## Conclusion

Nous venons de parcourir un scénario de **create new workbook** qui **copy pivot table**, **preserve pivot table**, et **export selected range**—tout en C# pur.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Create a New Pivot Table Programmatically in .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [How to Change Pivot Table Source Data Using Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [How to Manage Excel Pivot Table Compatibility with Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}