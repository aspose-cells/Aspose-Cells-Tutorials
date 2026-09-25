---
category: general
date: 2026-03-18
description: Copier un tableau croisé dynamique en C# avec Aspose.Cells. Apprenez
  à copier une plage Excel, dupliquer un tableau croisé dynamique Excel, copier une
  plage vers une nouvelle feuille et copier le tableau croisé dynamique vers une feuille
  en quelques minutes.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: fr
og_description: Copier un tableau croisé dynamique en C# avec Aspose.Cells. Apprenez
  à dupliquer un tableau croisé dynamique Excel, à copier une plage Excel vers un
  nouvel emplacement, et à copier le tableau croisé dynamique vers une feuille avec
  des exemples de code complets.
og_title: Copier un tableau croisé dynamique en C# – Guide complet de programmation
tags:
- Aspose.Cells
- C#
- Excel automation
title: Copier un tableau croisé dynamique en C# – Guide étape par étape
url: /fr/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copier un tableau croisé dynamique en C# – Guide complet de programmation

Avez-vous déjà eu besoin de **copy pivot table** d'une partie d'un classeur à une autre, sans savoir comment le faire sans perdre les connexions de données sous-jacentes ? Vous n'êtes pas seul. De nombreux développeurs rencontrent ce problème lorsqu'ils automatisent des rapports Excel, surtout lorsque le tableau croisé dynamique se trouve à l'intérieur d'un bloc de données plus grand. Bonne nouvelle : avec Aspose.Cells, vous pouvez copier le tableau croisé dynamique **exactly as it appears**, et vous apprendrez également à **copy excel range**, **duplicate excel pivot**, et même **copy pivot to sheet** en quelques lignes de C#.

Dans ce tutoriel, nous parcourrons un scénario réel : déplacer un tableau croisé dynamique qui occupe *A1:J20* vers une nouvelle zone *M1:V20* dans la même feuille de calcul. À la fin, vous disposerez d'un programme exécutable, comprendrez pourquoi chaque étape est importante et saurez comment adapter le code à d'autres plages ou même à des feuilles de calcul distinctes. Aucun document externe n'est nécessaire — tout est ici.

---

## Prérequis

- **Aspose.Cells for .NET** (version 23.9 ou ultérieure). Vous pouvez l'obtenir via NuGet : `Install-Package Aspose.Cells`.
- Un environnement de développement C# de base (Visual Studio 2022, Rider, ou VS Code avec l'extension C#).
- Un fichier Excel (`source.xlsx`) contenant un tableau croisé dynamique dans la plage *A1:J20*.

C’est tout. Si vous êtes à l'aise pour créer une application console, vous êtes prêt à démarrer.

## Comment copier un tableau croisé dynamique avec Aspose.Cells

Le cœur de la solution repose sur un appel unique à `Worksheet.Cells.CopyRange`. Cette méthode copie non seulement les valeurs brutes des cellules, mais préserve également les tableaux croisés dynamiques, les graphiques et d'autres objets riches automatiquement. Décomposons cela.

### Étape 1 : Charger le classeur source

Tout d'abord, nous devons charger le classeur en mémoire.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Pourquoi c’est important** : charger le classeur crée une représentation en mémoire que Aspose.Cells peut manipuler sans lancer Excel. C’est rapide, sûr pour les threads et fonctionne sur les serveurs.

### Étape 2 : Récupérer la première feuille de calcul

La plupart des exemples utilisent la première feuille, mais vous pouvez cibler n'importe quel index ou nom.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Conseil** : si vous devez **copy pivot to sheet** au lieu de la même feuille, il suffit de changer la référence `worksheet` vers un autre objet `Worksheet`.

### Étape 3 : Définir les plages source et cible

Nous utiliserons les structures `CellArea` pour décrire les blocs que nous déplaçons.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Explication** : les indices de lignes et de colonnes commencent à zéro. Colonne 0 = **A**, colonne 12 = **M**, etc. Ajustez ces nombres si votre tableau croisé dynamique se trouve ailleurs.

### Étape 4 : Effectuer l’opération de copie

C’est maintenant que la magie opère. Mettre le dernier paramètre booléen à `true` indique à Aspose.Cells de copier tous les objets — y compris le tableau croisé dynamique.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Pourquoi `true`** ? Le drapeau indique « copier tous les objets ». Si vous le mettez à `false`, seules les valeurs brutes des cellules seraient déplacées, et le tableau croisé dynamique serait perdu.

### Étape 5 : Enregistrer le classeur

Enfin, écrivez le classeur modifié sur le disque.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Résultat** : `copy-pivot.xlsx` contient maintenant le tableau croisé dynamique original en *A1:J20* **et** une copie identique en *M1:V20*. Ouvrez le fichier dans Excel pour vérifier que les deux tableaux croisés dynamiques fonctionnent et conservent leurs connexions de données.

## Copier une plage Excel vers un nouvel emplacement – une variation rapide

Parfois, vous n’avez besoin que de **copy excel range** sans vous soucier des tableaux croisés dynamiques. La même méthode `CopyRange` fait l’affaire ; il suffit de mettre le dernier argument à `false`.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **Quand l’utiliser** : si vous déplacez des données brutes vers une feuille de calcul temporaire, désactiver la copie des objets économise de la mémoire et accélère l’opération.

## Dupliquer un tableau croisé dynamique Excel sur plusieurs feuilles

Et si vous souhaitez **duplicate excel pivot** sur une autre feuille de calcul ? Le même schéma s’applique ; il suffit de référencer un autre `Worksheet` pour la destination.

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Cas limite** : si le tableau croisé dynamique source utilise une table qui se trouve sur la feuille d’origine, Aspose.Cells copiera également la définition de la table sous‑jacente, garantissant que le nouveau tableau croisé dynamique fonctionne immédiatement.

## Écueils courants et comment les éviter

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| **Pivot loses its cache** | Utilisation de `CopyRange` avec `false` ou d’une routine de copie personnalisée qui ignore les objets. | Toujours passer `true` lorsque vous avez besoin du tableau croisé dynamique lui‑même. |
| **Target cells already contain data** | Écrase silencieusement, pouvant corrompre les formules existantes. | Effacez d’abord la zone cible : `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **Source range doesn’t include the whole pivot** | Les tableaux croisés dynamiques couvrent plus de lignes/colonnes que prévu (par ex., des lignes masquées). | Utilisez `worksheet.PivotTables[0].DataRange` pour récupérer programmatique les limites exactes. |
| **Copying between workbooks** | `CopyRange` ne fonctionne que dans le même classeur. | Utilisez `sourceWorksheet.Cells.CopyRange` vers une plage temporaire, puis `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

## Résultat attendu & vérification

Après l’exécution du programme :

1. Ouvrez `copy-pivot.xlsx`.
2. Vous verrez deux tableaux croisés dynamiques identiques — l’un en **A1:J20**, l’autre en **M1:V20**.
3. Rafraîchissez n’importe quel tableau croisé dynamique ; les deux doivent refléter les mêmes données sous‑jacentes.
4. Si vous avez dupliqué sur une autre feuille, la nouvelle feuille contiendra également une copie fonctionnelle.

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

## Astuce pro : automatiser la détection de la plage

Coder en dur le `CellArea` fonctionne pour les rapports statiques, mais le code de production doit souvent localiser le tableau croisé dynamique dynamiquement.

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **Pourquoi s’en soucier** ? Cela rend votre solution résiliente aux changements de mise en page — plus d’erreurs du type « Oups, le tableau croisé dynamique a bougé en B2 ».

![exemple de copie de tableau croisé dynamique](copy-pivot.png){alt="exemple de copie de tableau croisé dynamique"}

*La capture d’écran (espace réservé) montre le tableau croisé dynamique original à gauche et la copie dupliquée à droite.*

## Récapitulatif

Nous venons de couvrir comment **copy pivot table** en C# avec Aspose.Cells, explorer les méthodes pour **copy excel range**, **duplicate excel pivot**, et même **copy pivot to sheet** entre les feuilles. Les points clés sont :

- Utilisez `Worksheet.Cells.CopyRange` avec le drapeau `true` pour préserver les objets riches.
- Définissez les objets `CellArea` source et cible avec des indices basés à zéro.
- Ajustez la feuille de destination si vous devez **copy pivot to sheet**.
- Prenez en compte les cas limites comme les données existantes, les lignes masquées et les scénarios inter‑classeur.

## Et après ?

- **Dynamic pivot discovery** : Créez un assistant qui parcourt un classeur à la recherche de tous les tableaux croisés dynamiques et les réplique automatiquement.
- **Export to PDF/HTML** : Après la copie, vous pourriez vouloir rendre la feuille dans un format de rapport — Aspose.Cells le gère également.
- **Performance tuning** : Pour des classeurs volumineux, envisagez de désactiver le calcul avant la copie et de le réactiver ensuite.

N’hésitez pas à expérimenter : modifiez les coordonnées cibles, copiez vers un tout nouveau classeur, ou même bouclez sur plusieurs feuilles pour créer un rapport consolidé. Les possibilités sont infinies, et avec les bases que vous avez maintenant, vous pourrez adapter le code à pratiquement n’importe quelle tâche d’automatisation Excel.

Bon codage, et que vos tableaux croisés dynamiques restent toujours parfaitement synchronisés !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}