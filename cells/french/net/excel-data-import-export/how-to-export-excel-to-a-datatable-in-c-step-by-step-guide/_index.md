---
category: general
date: 2026-03-18
description: Comment exporter des données Excel vers un DataTable en C# avec du code
  qui gère des cellules spécifiques, convertit Excel en DataTable et formate les nombres.
  Apprenez à exporter des cellules spécifiques et bien plus encore.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: fr
og_description: Comment exporter des données Excel vers un DataTable en C#. Ce tutoriel
  montre comment exporter des cellules spécifiques, convertir Excel en DataTable et
  formater les nombres facilement.
og_title: Comment exporter Excel vers un DataTable en C# – Guide complet
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Comment exporter Excel vers un DataTable en C# – Guide étape par étape
url: /fr/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter Excel vers un DataTable en C# – Guide étape par étape

Vous êtes-vous déjà demandé **comment exporter Excel** vers un `DataTable` sans perdre le formatage ? Vous n'êtes pas le seul — les développeurs ont constamment besoin d'extraire une partie d'une feuille de calcul en mémoire pour le reporting, la validation ou les opérations d’insertion en masse. Bonne nouvelle : avec quelques lignes de C# vous pouvez exporter une plage précise (par exemple *A1:F11*), forcer chaque cellule à être traitée comme une chaîne, et même appliquer un format numérique personnalisé.

Dans ce tutoriel, nous couvrirons tout ce que vous devez savoir : du chargement du classeur, à la configuration de **exporter des cellules spécifiques**, en passant par la conversion de la plage en `DataTable`, et la gestion des cas particuliers comme les lignes vides ou les nombres dépendants de la locale. À la fin, vous disposerez d’une méthode réutilisable qui fonctionne avec les scénarios **excel to datatable c#** en code de production.

> **Prérequis** – Vous aurez besoin de la bibliothèque Aspose.Cells for .NET (ou toute API similaire offrant `ExportDataTable`). L’exemple suppose .NET 6+, mais les concepts s’appliquent aussi aux versions antérieures.

---

## Ce que vous apprendrez

- Comment **convertir Excel en DataTable** avec Aspose.Cells.  
- Exporter une plage personnalisée (`excel range to datatable`) tout en traitant toutes les valeurs comme des chaînes.  
- Appliquer un format numérique à deux décimales (`#,#00.00`) lors de l’export.  
- Pièges courants (lignes nulles, colonnes masquées) et comment les éviter.  
- Un exemple de code prêt à copier, entièrement exécutable.

---

## Prérequis et configuration

Avant de plonger dans le code, assurez‑vous d'avoir :

1. **Aspose.Cells for .NET** installé via NuGet :

   ```bash
   dotnet add package Aspose.Cells
   ```

2. Un fichier Excel (`input.xlsx`) placé dans un dossier que vous pouvez référencer, par ex. `YOUR_DIRECTORY/input.xlsx`.  
3. Un projet ciblant .NET 6 ou supérieur (les instructions `using` ci‑dessous fonctionnent immédiatement).

> **Astuce pro** : Si vous utilisez une autre bibliothèque (par ex., EPPlus ou ClosedXML), le concept reste le même — chargez le classeur, sélectionnez une plage, et appelez une méthode qui renvoie un `DataTable`.

---

## Étape 1 : Charger le classeur et récupérer la première feuille de calcul

La première chose dont vous avez besoin est un objet `Workbook` qui représente votre fichier Excel. Une fois que vous l’avez, vous pouvez accéder à n’importe quelle feuille par index ou par nom.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Pourquoi c’est important** : charger le classeur dès le départ vous permet d’inspecter sa structure (feuilles masquées, protection) avant de décider quelles cellules exporter. Si le fichier est volumineux, envisagez d’utiliser `LoadOptions` pour ne diffuser que les parties nécessaires.

---

## Étape 2 : Configurer les options d’export – Traiter toutes les valeurs comme des chaînes

Lorsque vous exportez des données pour un traitement en aval (par ex., insertion en masse dans SQL), vous voulez souvent une **représentation de chaîne cohérente**. Cela évite les erreurs de type plus tard.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Explication** :  
- `ExportAsString = true` indique à Aspose.Cells d’ignorer le type natif de la cellule et de renvoyer le texte formaté.  
- `NumberFormat = "#,##0.00"` garantit que des nombres comme `1234.5` deviennent `"1,234.50"` — utile pour les rapports financiers.

Si vous avez besoin des types de données d’origine, réglez simplement `ExportAsString` sur `false` et gérez la conversion vous‑même.

---

## Étape 3 : Exporter une plage spécifique (A1:F11) vers un DataTable

Voici le cœur de **exporter des cellules spécifiques**. La méthode `ExportDataTable` prend les indices de ligne/colonne de début et de fin (base 0) ainsi qu’un indicateur d’inclusion des en‑têtes.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**Ce que vous obtenez** : un `DataTable` contenant 11 lignes (en‑tête incluse) et 6 colonnes (`A`‑`F`). Toutes les valeurs sont des chaînes formatées selon `exportOptions`.

---

## Étape 4 : Vérifier le résultat – Afficher dans la console

Il est toujours judicieux de vérifier la sortie avant de transmettre le tableau à un autre composant.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

Vous devriez voir quelque chose comme :

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Remarquez comment les colonnes numériques affichent deux décimales, exactement comme spécifié.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet qui assemble tous les éléments. Copiez‑le dans un nouveau projet console, ajustez le chemin du fichier, et lancez‑le — aucune configuration supplémentaire n’est requise.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Points clés du code** :

- L’objet `ExportTableOptions` est réutilisable ; vous pouvez le passer à plusieurs appels `ExportDataTable` si vous devez exporter plusieurs plages.  
- L’indexation commence à **0**, donc `A1` correspond à `(0,0)`.  
- Mettre `includeColumnNames` à `true` utilise automatiquement la première ligne comme en‑têtes de colonnes — pratique pour les opérations `DataTable` en aval.

---

## Gestion des cas particuliers & questions fréquentes

### Que faire si la feuille possède des lignes ou colonnes masquées ?

Aspose.Cells respecte la visibilité par défaut. Si vous devez exporter les données masquées, définissez `exportOptions.ExportHiddenRows = true` et `ExportHiddenColumns = true`.

### Mon fichier Excel contient des formules — obtiendra‑t‑je les valeurs calculées ?

Oui. Par défaut, `ExportDataTable` renvoie la **valeur affichée** (le résultat de la formule). Si vous voulez le texte brut de la formule, réglez `exportOptions.ExportFormulas = true`.

### Comment ignorer les lignes totalement vides ?

Après l’export, vous pouvez épurer le `DataTable` :

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Puis‑je exporter une plage non contiguë (par ex., A1:B5 et D1:E5) ?

Aspose.Cells ne prend pas en charge les plages disjointes en un seul appel. Exportez chaque bloc séparément, puis fusionnez manuellement les `DataTable` résultants.

---

## Conseils de performance

- **Réutilisez `ExportTableOptions`** pour plusieurs exportations ; créer une nouvelle instance à chaque fois ajoute un surcoût négligeable mais encombre le code.  
- **Diffusez les gros fichiers** avec `LoadOptions` pour éviter de charger tout le classeur en mémoire.  
- **Évitez `DataTable`** si vous avez seulement besoin d’un export CSV rapide — `ExportDataTable` est pratique mais n’est pas la solution la plus économique en mémoire pour des feuilles massives.

---

## Conclusion

Nous avons parcouru **comment exporter Excel** vers un `DataTable` tout en contrôlant le formatage, en gérant des plages de cellules spécifiques, et en veillant à ce que chaque valeur arrive sous forme de chaîne. L’exemple complet montre une approche propre et prête pour la production que vous pouvez adapter aux scénarios **convert excel to datatable**, **export specific cells**, ou tout **excel range to datatable** que vous rencontrez.

N’hésitez pas à expérimenter : modifiez la plage, basculez `ExportAsString`, ou transmettez directement le `DataTable` à Entity Framework pour des insertions en masse. Le ciel est la limite une fois que vous avez cette base solide.

### Prochaines étapes & sujets connexes

- **Importer un DataTable dans Excel** – apprenez l’opération inverse avec `ImportDataTable`.  
- **Insertion en masse d’un DataTable dans SQL Server** – utilisez `SqlBulkCopy` pour des chargements ultra‑rapides.  
- **Travailler avec EPPlus ou ClosedXML** – voyez comment la même tâche se présente avec des bibliothèques alternatives.  
- **Formater les cellules à l’export** – explorez davantage `ExportTableOptions` pour les formats de date, les paramètres culturels personnalisés, et plus encore.

Des questions ou un cas d’utilisation différent ? Laissez un commentaire, et continuons la discussion. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}