---
category: general
date: 2026-03-22
description: Apprenez comment dupliquer un tableau croisé dynamique en C# à l’aide
  d’Aspose.Cells. Ce guide montre également comment copier des lignes et charger un
  classeur Excel en C# pour une automatisation fluide d’Excel lors de la copie de
  lignes.
draft: false
keywords:
- how to duplicate pivot
- how to copy rows
- load excel workbook c#
- excel automation copy rows
language: fr
og_description: Comment dupliquer un tableau croisé dynamique en C# ? Suivez ce tutoriel
  concis pour charger un classeur Excel en C#, copier des lignes et maîtriser l’automatisation
  Excel pour copier des lignes.
og_title: Comment dupliquer un pivot en C# – Guide complet
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Comment dupliquer le pivot en C# – Guide complet étape par étape
url: /fr/net/pivot-tables/how-to-duplicate-pivot-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment dupliquer un tableau croisé dynamique en C# – Guide complet étape par étape

Vous vous êtes déjà demandé **comment dupliquer un tableau croisé dynamique** de manière programmatique sans les faire glisser manuellement dans Excel ? Vous n'êtes pas le seul. Dans de nombreux pipelines de reporting, la même mise en page de tableau croisé dynamique est nécessaire sur un nouvel ensemble de lignes, et le faire à la main est une perte de temps.  

Bonne nouvelle ? En quelques lignes de C#, vous pouvez charger un classeur Excel, définir la zone qui contient le tableau croisé dynamique, et **comment copier des lignes** afin que le tableau croisé dynamique apparaisse à un nouvel emplacement — le tout en une exécution automatisée. Dans ce tutoriel, nous couvrirons également les bases de **load excel workbook c#** et vous fournirons une base solide pour les tâches de **excel automation copy rows**.

> **Ce que vous en retirerez**  
> • Un exemple complet et exécutable qui duplique un tableau croisé dynamique.  
> • Une explication de l'importance de chaque ligne.  
> • Des astuces pour gérer les cas particuliers comme les feuilles cachées ou plusieurs tableaux croisés dynamiques.

---

## Prérequis

Avant de commencer, assurez-vous d'avoir :

- **.NET 6.0** (ou toute version récente de .NET) installé.  
- **Aspose.Cells for .NET** – la bibliothèque que nous utiliserons pour manipuler les fichiers Excel. Vous pouvez l'obtenir via NuGet :

```bash
dotnet add package Aspose.Cells
```

- Un classeur source (`Source.xlsx`) qui contient déjà un tableau croisé dynamique dans la plage **A1:J20** (la plage que nous dupliquerons).  
- Une connaissance de base de la syntaxe C# – rien de compliqué, juste les déclarations `using` habituelles et la méthode `Main`.

Si l'un de ces éléments vous est inconnu, faites une pause et installez le package ; le reste du guide suppose que la bibliothèque est prête à l'emploi.

![Illustration of how to duplicate pivot in C# using Aspose.Cells](https://example.com/duplicate-pivot.png "illustration de comment dupliquer un tableau croisé dynamique en C#")
*Texte alternatif de l'image : « exemple de duplication d'un tableau croisé dynamique en C# montrant les lignes source et dupliquées ». *

## Étape 1 : Charger un classeur Excel C# – Ouverture du fichier

La toute première chose à faire lorsque vous voulez **load excel workbook c#** est de créer une instance `Workbook` pointant vers votre fichier. Cet objet vous donne accès à chaque feuille, cellule et tableau croisé dynamique du fichier.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Load the source workbook
        string sourcePath = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // From here on we can work with worksheets, ranges, and pivots.
```

**Pourquoi c’est important :**  
`Workbook` abstrait l’ensemble du fichier Excel en un modèle en mémoire. Sans le charger d’abord, vous ne pouvez pas inspecter l’emplacement du tableau croisé dynamique ni copier les lignes. De plus, le constructeur détecte automatiquement le format du fichier (XLS, XLSX, CSV, etc.), vous n’avez donc pas besoin de code supplémentaire pour la détection du format.

## Étape 2 : Comment copier des lignes – Définition de la zone du tableau croisé dynamique

Maintenant que le classeur est en mémoire, nous devons indiquer à Aspose.Cells quelles lignes contiennent le tableau croisé dynamique. Dans notre exemple, le tableau croisé dynamique se trouve dans **A1:J20**, ce qui correspond aux lignes **0‑19** (indexation à partir de zéro). Nous allons encapsuler cela dans une structure `CellArea`.

```csharp
        // Step 2: Define the cell area that contains the pivot table (A1:J20)
        // Row indices are zero‑based, column indices are also zero‑based.
        CellArea copyRange = new CellArea(startRow: 0, startColumn: 0, endRow: 19, endColumn: 9);
```

**Pourquoi nous utilisons `CellArea` :**  
C’est une façon légère de décrire un bloc rectangulaire. Lorsque vous appelez plus tard `CopyRows`, la méthode lit cet objet pour savoir exactement quelles lignes dupliquer. Si vous devez ajuster la plage (par exemple le tableau croisé dynamique s’étend à la colonne K), vous ne modifiez que la valeur `endColumn`.

## Étape 3 : Accéder à la feuille cible

La plupart des classeurs ont une seule feuille, mais l’API fonctionne de la même manière pour plusieurs feuilles. Récupérez la première feuille (index 0) – c’est là que se trouve le tableau croisé dynamique original.

```csharp
        // Step 3: Get the first worksheet from the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Astuce :**  
Si vous avez des feuilles nommées, vous pouvez également les récupérer par leur nom : `workbook.Worksheets["Sheet1"]`. Cela évite de coder en dur les indices lorsque la structure du classeur change.

## Étape 4 : Comment copier des lignes – Duplication du tableau croisé dynamique

Voici le cœur de **how to duplicate pivot** : nous copions les lignes contenant le tableau croisé dynamique vers un nouvel emplacement. Dans notre cas, nous commençons à la ligne 31 (index zéro 30). La méthode `CopyRows` copie *à la fois* les données et le cache du tableau croisé dynamique sous-jacent, de sorte que les nouvelles lignes se comportent exactement comme l’original.

```csharp
        // Step 4: Copy the rows of the defined range to a new location (starting at row 31)
        // The third argument is the destination start row (zero‑based).
        worksheet.Cells.CopyRows(copyRange.StartRow, copyRange.EndRow, destinationRow: 30);
```

**Que se passe-t-il en coulisses ?**  
`CopyRows` clone chaque ligne, en préservant les formules, les styles et les définitions du tableau croisé dynamique. Comme le cache du tableau croisé dynamique réside au niveau du classeur, le tableau dupliqué référence automatiquement la même source de données – aucune configuration supplémentaire n’est nécessaire.

**Cas particulier – lignes cachées :**  
Si l’une des lignes de la plage source est cachée, elle restera cachée après la copie. Si vous souhaitez les afficher, appelez `worksheet.Rows[destRow].IsHidden = false` après la copie.

## Étape 5 : Enregistrer le classeur – Vérifier la duplication

Enfin, écrivez les modifications sur le disque. Vous pouvez écraser le fichier original ou, plus prudent, enregistrer sous un nouveau nom afin de comparer avant/après.

```csharp
        // Step 5: Save the workbook – the pivot table is now duplicated in the new rows
        string outputPath = @"C:\Data\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine("Pivot duplicated successfully! Check " + outputPath);
    }
}
```

**Résultat attendu :**  
Ouvrez `CopyWithPivot.xlsx`. Vous trouverez le tableau croisé dynamique original à **A1:J20** et une copie identique commençant à **A31:J50**. Les deux tableaux peuvent être actualisés indépendamment, et tout segment (slicer) attaché à l’original fonctionnera toujours pour la copie car ils partagent le même cache.

## Questions fréquentes & variantes

### Puis-je dupliquer plusieurs tableaux croisés dynamiques à la fois ?

Absolument. Parcourez tous les tableaux croisés dynamiques (`worksheet.PivotTables`) et copiez la plage de chacun vers une destination différente. Veillez simplement à ce que les plages de destination ne se chevauchent pas.

### Et si le classeur source est protégé par mot de passe ?

Aspose.Cells vous permet d’ouvrir un fichier protégé en passant le mot de passe au constructeur `Workbook` :

```csharp
Workbook workbook = new Workbook(sourcePath, new LoadOptions { Password = "mySecret" });
```

### Comment copier des lignes sans affecter les formules ?

Si vous avez uniquement besoin des *valeurs* (pas de formules), utilisez `CopyRows` avec le drapeau `CopyOptions` :

```csharp
worksheet.Cells.CopyRows(sourceStart, sourceEnd, destStart, new CopyOptions { CopyValues = true });
```

### Existe-t-il un moyen de copier des lignes vers un classeur *différent* ?

Oui. Après avoir copié les lignes dans la feuille source, vous pouvez cloner la feuille dans une autre instance `Workbook` via `targetWorkbook.Worksheets.AddCopy(worksheet)`.

## Astuces pro pour une copie fiable de lignes en automatisation Excel

- **Validez la plage** avant de copier. Un simple `if (copyRange.EndRow >= worksheet.Cells.MaxDataRow)` évite les erreurs de dépassement de plage.  
- **Désactivez le calcul** pendant la copie de grandes plages : `workbook.Settings.CalcMode = CalcMode.Manual;` – cela accélère considérablement l’opération.  
- **Libérez les objets** (`workbook.Dispose()`) si vous traitez de nombreux fichiers dans une boucle afin de libérer les ressources natives.  
- **Enregistrez l’opération** – surtout dans les pipelines de production – afin de tracer quels fichiers ont été traités et de détecter les échecs rapidement.

## Conclusion

Vous savez maintenant **how to duplicate pivot** tables en C# avec Aspose.Cells, et vous avez vu le flux complet depuis **load excel workbook c#** jusqu’à **excel automation copy rows** et enfin l’enregistrement du résultat. L’exemple est autonome, fonctionne immédiatement, et peut être étendu pour gérer plusieurs tableaux croisés dynamiques, des fichiers protégés ou la copie entre classeurs.

Prochaines étapes ? Essayez d’adapter le script pour :

- Actualiser le tableau croisé dynamique dupliqué de façon programmatique (`pivotTable.RefreshData();`).  
- Exporter la zone dupliquée vers un CSV pour le traitement en aval.  
- Intégrer le code dans une API ASP.NET Core afin que les utilisateurs puissent télécharger un fichier et recevoir immédiatement une version dupliquée du tableau croisé dynamique.

Bonne programmation, et que votre automatisation Excel soit toujours fluide !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}