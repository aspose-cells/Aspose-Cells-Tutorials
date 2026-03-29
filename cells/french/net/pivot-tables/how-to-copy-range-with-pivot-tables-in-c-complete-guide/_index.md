---
category: general
date: 2026-03-29
description: Apprenez à copier une plage, à copier des tableaux croisés dynamiques,
  à enregistrer un classeur et à le charger en C#. Déplacez facilement les tableaux
  croisés dynamiques avec du code étape par étape.
draft: false
keywords:
- how to copy range
- copy pivot tables
- how to save workbook
- how to load workbook
- move pivot table
language: fr
og_description: Comment copier une plage, copier des tableaux croisés dynamiques,
  comment enregistrer un classeur et comment charger un classeur en C#. Déplacez les
  tableaux croisés dynamiques sans effort avec un code clair.
og_title: Comment copier une plage avec des tableaux croisés dynamiques en C# – Guide
  complet
tags:
- C#
- Aspose.Cells
- Excel automation
title: Comment copier une plage avec des tableaux croisés dynamiques en C# – Guide
  complet
url: /fr/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier une plage contenant des tableaux croisés dynamiques en C# – Guide complet

Vous vous êtes déjà demandé **comment copier une plage** contenant un tableau croisé dynamique sans rompre le lien avec ses données source ? Vous n'êtes pas le seul. Dans de nombreux projets réels, je suis tombé sur ce même problème — les fichiers Excel arrivent avec des tableaux croisés dynamiques sophistiqués, et il faut les repositionner ou dupliquer les données ailleurs.  

Bonne nouvelle ? La solution est assez simple une fois que vous savez **comment charger le classeur**, faire une copie, puis **comment enregistrer le classeur** à nouveau. Dans ce tutoriel, nous parcourrons l’ensemble du processus, y compris comment **copier des tableaux croisés dynamiques**, et même une astuce rapide sur **déplacer un tableau croisé dynamique** si vous devez le placer ailleurs dans la même feuille.

À la fin de ce guide, vous disposerez d’un extrait C# entièrement fonctionnel qui :

1. Charge un fichier Excel existant.  
2. Copie une plage (y compris le tableau croisé dynamique) vers un nouvel emplacement.  
3. Enregistre le classeur modifié dans un nouveau fichier.

Pas de scripts externes, pas de manipulations manuelles — juste du code propre et réutilisable.

---

## Prérequis

- **.NET 6+** (toute version récente fonctionne).  
- **Aspose.Cells for .NET** – la bibliothèque qui fournit `Workbook`, `WorksheetCopyOptions`, etc. Vous pouvez l’installer via NuGet :

```bash
dotnet add package Aspose.Cells
```

- Un classeur d’entrée (`input.xlsx`) contenant déjà un tableau croisé dynamique dans la plage `A1:G20`.  
- Une connaissance de base de C# et de Visual Studio (ou de votre IDE préféré).

> **Astuce pro :** Si vous utilisez une autre bibliothèque Excel (par ex., EPPlus), les concepts restent les mêmes — il suffit d’échanger les appels d’API.

---

## Étape 1 – Comment charger le classeur (Configuration principale)

Avant de pouvoir copier quoi que ce soit, nous devons charger le fichier Excel en mémoire.

```csharp
using Aspose.Cells;

// Step 1: Load the source workbook
var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Grab the first worksheet – this is where our pivot lives
var sourceWorksheet = sourceWorkbook.Worksheets[0];
```

**Pourquoi c’est important :**  
Le chargement du classeur vous fournit un modèle d’objet que vous pouvez manipuler. Sans **comment charger le classeur** correctement, toute opération de copie ultérieure déclencherait une exception *FileNotFound* ou *InvalidOperation*.  

> **Attention :** Si le fichier est volumineux, envisagez d’utiliser `LoadOptions` avec `MemorySetting` pour contrôler l’utilisation de la mémoire.

---

## Étape 2 – Comment copier une plage (y compris le tableau)

Voici le cœur du sujet : copier une plage qui contient un tableau croisé dynamique. La méthode `CopyRange`, combinée à `WorksheetCopyOptions`, effectue le travail lourd.

```csharp
// Step 2: Copy a range that includes a pivot table to a new location
sourceWorksheet.CopyRange(
    "A1:G20",                                   // Source range
    new WorksheetCopyOptions { CopyPivotTables = true }, // Ensure pivot tables travel with the data
    sourceWorksheet,                           // Destination worksheet (same sheet in this case)
    "A25");                                     // Upper‑left corner of the destination
```

**Pourquoi nous définissons `CopyPivotTables = true` :**  
Par défaut, copier une plage ne déplace que les cellules brutes. Le cache du tableau croisé dynamique reste en arrière‑plan, et le tableau copié devient une table statique. En définissant `CopyPivotTables`, on préserve la **connexion en direct**, de sorte que le tableau dupliqué se **rafraîchisse** lorsque ses données source changent.

**Cas limite :** Si la plage de destination chevauche la **source**, Aspose.Cells lèvera une `ArgumentException`. Choisissez toujours une cible qui ne se chevauche pas, ou créez d’abord une nouvelle feuille.

---

## Étape 3 – Comment enregistrer le classeur (Persister les modifications)

Après la copie, vous voudrez écrire les changements sur le disque. C’est ici que **comment enregistrer le classeur** entre en jeu.

```csharp
// Step 3: Save the modified workbook to a new file
sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

**Ce qui se passe en coulisses :**  
`Save` sérialise le classeur en mémoire, y compris le tableau croisé dynamique nouvellement copié, dans un package `.xlsx` standard. Si vous avez besoin d’un autre format (CSV, PDF, etc.), il suffit de changer l’extension du fichier ou d’utiliser la surcharge qui accepte `SaveFormat`.

> **Conseil :** Utilisez `Workbook.Save(string, SaveOptions)` si vous devez protéger le fichier avec un mot de passe ou définir d’autres options d’exportation.

---

## Exemple complet fonctionnel

En rassemblant le tout, voici le programme complet, prêt à être exécuté :

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ How to load workbook
        var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        var sourceWorksheet = sourceWorkbook.Worksheets[0];

        // 2️⃣ How to copy range (including pivot tables)
        sourceWorksheet.CopyRange(
            "A1:G20",
            new WorksheetCopyOptions { CopyPivotTables = true },
            sourceWorksheet,
            "A25");

        // 3️⃣ How to save workbook
        sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");

        Console.WriteLine("✅ Range copied and workbook saved successfully!");
    }
}
```

**Résultat attendu :**  
Ouvrez `output.xlsx`. Vous verrez le tableau croisé dynamique original toujours présent dans `A1:G20`, et une copie identique, pleinement fonctionnelle, à partir de `A25`. Les deux tableaux pointent vers les mêmes données source, de sorte que rafraîchir l’un met à jour l’autre.

---

## Questions fréquentes & Variantes

### Puis‑je **déplacer un tableau croisé dynamique** au lieu de le copier ?

Absolument. Après la copie, il suffit d’effacer la plage d’origine (ou d’utiliser `sourceWorksheet.Cells.ClearRange(0, 0, 19, 6)`) puis de renommer la plage de destination si nécessaire. Cela « déplace » effectivement le tableau.

### Et si le tableau utilise une source de données externe ?

`CopyPivotTables = true` ne copie que la définition du tableau, pas la connexion externe elle‑même. Assurez‑vous que le classeur cible a accès à la même source de données, ou recréez la connexion après la copie.

### Comment copier vers une **feuille différente** ?

Il suffit de passer l’objet de la feuille de destination à la place de `sourceWorksheet` :

```csharp
var destWorksheet = sourceWorkbook.Worksheets.Add("CopiedPivot");
sourceWorksheet.CopyRange("A1:G20", new WorksheetCopyOptions { CopyPivotTables = true }, destWorksheet, "A1");
```

### Existe‑t‑il un moyen de copier **plusieurs plages** en une fois ?

Vous pouvez appeler `CopyRange` à plusieurs reprises ou utiliser `CopyRows`/`CopyColumns` pour des blocs plus importants. Parcourir une liste de chaînes d’adresses est une approche propre.

---

## Pièges courants & Astuces pro

- **Taille du cache du tableau** : Les caches volumineux peuvent gonfler la taille du classeur. Si vous n’avez besoin que des données affichées, envisagez `CopyPivotTables = false` puis utilisez `PivotTable.RefreshData()` sur la destination.
- **Chemins de fichiers** : Utilisez `Path.Combine` pour éviter les séparateurs codés en dur, surtout en .NET multiplateforme.
- **Performance** : Pour les classeurs très lourds, encapsulez la copie dans un `using (var stream = new MemoryStream())` et enregistrez d’abord dans le flux, puis écrivez sur le disque. Cela réduit la surcharge d’E/S.

---

## Conclusion

Vous savez maintenant **comment copier une plage** contenant un tableau croisé dynamique, comment **copier des tableaux croisés dynamiques**, ainsi que les étapes exactes pour **comment charger le classeur** et **comment enregistrer le classeur** après l’opération. Que vous ayez besoin de **déplacer un tableau croisé dynamique** dans la même feuille ou vers une autre feuille, le schéma reste le même — charger, copier avec les bonnes options, puis enregistrer.

Essayez avec vos propres fichiers, ajustez l’adresse de destination et expérimentez avec différentes configurations de tableaux croisés dynamiques. Plus vous jouerez, plus vous serez à l’aise pour automatiser les tâches Excel en C#.

---

![Diagram showing the source range A1:G20 being copied to A25 in the same worksheet – how to copy range with pivot tables](/images/how-to-copy-range-diagram.png "how to copy range with pivot tables")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}