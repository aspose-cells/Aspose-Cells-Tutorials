---
category: general
date: 2026-02-09
description: Effacez l'interface de filtre dans Excel avec C# en supprimant le bouton
  AutoFilter. Apprenez à masquer le bouton de filtre, afficher la ligne d’en-tête
  et garder vos feuilles bien rangées.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: fr
og_description: Interface de filtre claire dans Excel avec C#. Ce guide montre comment
  masquer le bouton de filtre, afficher la ligne d’en-tête et garder les feuilles
  de calcul propres.
og_title: Effacer l'interface utilisateur du filtre dans Excel avec C# – Supprimer
  le bouton AutoFilter
tags:
- excel
- csharp
- epplus
- automation
title: Effacer l'interface de filtrage dans Excel avec C# – Supprimer le bouton AutoFilter
url: /fr/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effacer l'interface de filtre dans Excel avec C# – Supprimer le bouton AutoFilter

Vous avez déjà eu besoin d'**effacer l'interface de filtre** dans une feuille Excel mais vous ne saviez pas quelle ligne de code masque réellement cette petite flèche déroulante ? Vous n'êtes pas le seul. Le bouton de filtre peut être disgracieux lorsque vous livrez un rapport à des utilisateurs finaux qui n'ont jamais besoin de modifier la vue.  

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui **supprime le bouton AutoFilter** d'un tableau, s'assure que la ligne d'en-tête reste visible, et aborde même comment *masquer le bouton de filtre* de façon permanente. À la fin, vous saurez exactement **comment supprimer AutoFilter** en C# et pourquoi chaque étape est importante.

## Ce dont vous avez besoin

- .NET 6+ (ou .NET Framework 4.7.2+) – n'importe quel runtime récent fonctionne.
- Le package NuGet **EPPlus** (version 6.x ou ultérieure) – il nous fournit `ExcelWorksheet`, `ExcelTable`, etc.
- Un fichier Excel simple contenant un tableau nommé **SalesTable** (n'hésitez pas à en créer un en quelques clics).

C’est tout. Pas d’interop COM, pas de DLL supplémentaires, juste quelques instructions `using` et quelques lignes de code.

## Effacer l'interface de filtre : suppression du bouton AutoFilter

Le cœur de la solution réside dans trois petites instructions. Décomposons‑les afin que vous compreniez *pourquoi* elles sont nécessaires, et pas seulement *ce qu'elles font*.

### Étape 1 – Obtenir une référence au tableau

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

Pourquoi c’est important : EPPlus travaille avec des **tables** (`ExcelTable`), pas avec des plages brutes. En récupérant l’objet tableau, nous accédons à la propriété `AutoFilter`, qui contrôle l'élément UI que vous voyez sur la feuille. Si vous essayez de manipuler directement la feuille de calcul, vous n'affecterez que les valeurs, pas le bouton de filtre.

### Étape 2 – Supprimer la ligne du bouton AutoFilter

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

Définir `AutoFilter` à `null` indique à EPPlus de supprimer la ligne de filtre sous‑jacente. C’est l'opération *effacer l'interface de filtre* que la plupart des développeurs recherchent lorsqu'ils demandent « **comment supprimer autofilter** ». C’est une approche propre, en une seule ligne, qui fonctionne avec toutes les versions d'Excel prises en charge par EPPlus.

### Étape 3 – Conserver la ligne d'en-tête visible

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

Lorsque vous supprimez l'interface de filtre, Excel peut parfois masquer la ligne d'en-tête si le drapeau `ShowHeader` du tableau est à false. En le définissant explicitement à `true`, nous garantissons que les titres de colonnes restent à l'écran – un détail subtil mais important pour un rapport final soigné.

### Exemple complet et exécutable

Voici une application console minimale qui ouvre un classeur existant, exécute les trois étapes, puis enregistre le résultat. Copiez‑collez, appuyez sur **F5**, et observez le bouton de filtre disparaître.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Résultat attendu :** Ouvrez *SalesReport_NoFilter.xlsx* – les flèches de filtre ont disparu, mais les en‑têtes de colonnes restent. Plus de désordre d'interface « cliquer‑pour‑filtrer ».

> **Astuce :** Si vous avez **plusieurs tables** et que vous souhaitez masquer le bouton de filtre pour toutes, parcourez `worksheet.Tables` et appliquez les mêmes trois lignes à l'intérieur de la boucle.

## Comment supprimer AutoFilter dans Excel avec C# – une analyse approfondie

Vous vous demandez peut‑être : « Et si le classeur a déjà un filtre appliqué ? Le fait de définir `AutoFilter = null` supprime également les lignes filtrées ? » La réponse est **oui**. EPPlus supprime à la fois l'UI et les critères de filtre sous‑jacents, laissant les données dans leur ordre d'origine.

Si vous ne souhaitez que *masquer* le bouton tout en gardant le filtre actif, vous pouvez à la place définir la propriété `AutoFilter` à un **nouveau filtre vide** :

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

Cette variante est pratique lorsque vous voulez *masquer le bouton de filtre* pour un rendu soigné tout en permettant aux utilisateurs avancés de basculer les filtres via VBA ou le ruban.

### Cas limite : tables sans ligne d'en‑tête

Certains rapports hérités utilisent des plages simples au lieu de tables. Dans ce cas, EPPlus n'exposera pas d'objet `ExcelTable`, donc le code ci‑dessus générera une exception. La solution consiste à **convertir la plage en table** d'abord :

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

Vous avez maintenant *supprimé l'interface de type autofilter excel* même sur une plage qui ne commençait pas comme une table formelle.

## Afficher la ligne d'en‑tête après avoir masqué le bouton de filtre – pourquoi c’est important

Une plainte fréquente est que, après avoir masqué l'interface de filtre, la ligne d'en‑tête disparaît parfois, surtout si le classeur a été créé initialement avec « Masquer l’en‑tête » activé. En définissant explicitement `salesTable.ShowHeader = true;`, nous évitons cette surprise.

Si vous avez besoin de **masquer le bouton de filtre** tout en gardant l’en‑tête masquée (peut‑être que vous générez un vidage de données brut), définissez simplement `salesTable.ShowHeader = false;` après avoir supprimé le filtre. Le code est symétrique, ce qui le rend facile à basculer selon un drapeau de configuration.

## Masquer le bouton de filtre – conseils pratiques et pièges

- **Compatibilité des versions :** EPPlus 6+ ne fonctionne qu'avec les fichiers `.xlsx`. Si vous travaillez avec le format plus ancien `.xls`, vous aurez besoin d'une bibliothèque différente (par ex., NPOI) car l'API *clear filter UI* n'est pas disponible.
- **Performance :** Charger un classeur volumineux juste pour masquer un bouton peut être lent. Envisagez d'utiliser `ExcelPackage.Load(stream, true)` pour l'ouvrir en mode **lecture‑seule**, appliquer le changement, puis enregistrer.
- **Tests :** Validez toujours le fichier de sortie manuellement la première fois. Les tests UI automatisés peuvent vérifier que les flèches de filtre ont réellement disparu (`worksheet.Tables[0].AutoFilter == null`).
- **Licence :** EPPlus est passé à une double licence à partir de la version 5. Pour les projets commerciaux, vous aurez besoin d'une licence payante ou de passer à une bibliothèque alternative.

## Fichier source complet à copier‑coller

Voici le fichier exact que vous pouvez placer dans un nouveau projet console. Aucun dépendance cachée, tout est autonome.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

Exécutez `dotnet add package EPPlus --version 6.0.8` (ou la dernière version) avant de compiler, et vous disposerez d’une feuille propre prête à être distribuée.

## Conclusion

Nous venons de vous montrer **comment supprimer AutoFilter** et **effacer l'interface de filtre** dans un classeur Excel en utilisant C#. Le cœur de trois lignes (`AutoFilter = null;`, `ShowHeader = true;`) fait le gros du travail, tandis que le code d'accompagnement rend la solution

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}