---
category: general
date: 2026-03-22
description: Comment exporter Excel avec mise en forme et préserver le format des
  nombres. Apprenez à convertir une plage Excel, obtenir le résultat d’une formule
  et exporter Excel avec mise en forme en utilisant Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: fr
og_description: Comment exporter Excel avec mise en forme et préserver le format des
  nombres. Guide étape par étape pour convertir une plage Excel, obtenir le résultat
  d’une formule et exporter Excel avec mise en forme en C#.
og_title: Comment exporter Excel avec mise en forme – Conserver le format des nombres
tags:
- C#
- Aspose.Cells
- Excel automation
title: Comment exporter Excel avec mise en forme – Conserver le format des nombres
url: /fr/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter Excel avec mise en forme – Conserver le format des nombres

Vous êtes‑vous déjà demandé **comment exporter Excel** tout en conservant l’apparence exacte de chaque cellule telle qu’elle apparaît dans le classeur ? Peut‑être devez‑vous envoyer un rapport à un client, alimenter un contrôle de grille, ou simplement stocker les valeurs dans une base de données. Le problème habituel est la perte du format des nombres ou les formules qui se transforment en chaînes brutes.  

Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l’emploi en C#, qui **conserve le format des nombres**, **convertit une plage Excel** en `DataTable`, **obtient le résultat de la formule**, et enfin **exporte Excel avec mise en forme** en utilisant Aspose.Cells. À la fin, vous disposerez d’une méthode unique que vous pourrez intégrer à n’importe quel projet et appeler avec une référence de feuille de calcul.

> **Aperçu rapide :** le code crée un classeur, écrit une valeur et une formule, indique à Aspose.Cells d’exporter les cellules sous forme de chaînes formatées, et affiche `123.456 | 246.912` – exactement ce que vous vous attendez à voir dans Excel.

---

## Ce dont vous aurez besoin

- **Aspose.Cells for .NET** (l’essai gratuit suffit pour l’apprentissage)
- .NET 6.0 ou version ultérieure (l’API est identique sur .NET Framework)
- Un environnement de développement C# basique (Visual Studio, VS Code, Rider… à vous de choisir)

Aucun package NuGet supplémentaire au‑delà d’Aspose.Cells n’est requis. Si vous ne l’avez pas encore installé, exécutez :

```bash
dotnet add package Aspose.Cells
```

---

## Étape 1 – Créer un classeur et écrire des valeurs (y compris une formule)

Tout d’abord, nous créons un nouveau classeur et insérons une valeur numérique dans **A1**. Ensuite, nous ajoutons une formule simple dans **B1** qui multiplie la première cellule par deux. Cela prépare le terrain pour démontrer **obtenir le résultat de la formule** plus tard.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Pourquoi c’est important :**  
- `PutValue` stocke le nombre brut, tandis que `PutFormula` stocke le calcul.  
- Aspose.Cells garde la formule **active**, de sorte que lorsque nous demanderons plus tard la valeur de la cellule, nous obtiendrons réellement `246.912`, et non la chaîne `"=A1*2"`.

---

## Étape 2 – Indiquer à Aspose.Cells d’exporter les valeurs sous forme de chaînes formatées

Si vous appelez simplement `ExportDataTable` avec les paramètres par défaut, les cellules numériques seront renvoyées sous forme de leurs valeurs `double` sous‑jacentes. Cela supprime les séparateurs de milliers, les symboles monétaires ou les décimales personnalisées que vous avez éventuellement définis. La classe `ExportTableOptions` nous permet de **conserver le format des nombres** et **d’exporter sous forme de chaîne**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Point clé :** `ExportNumberFormat = true` est le drapeau qui rend **conserver le format des nombres** fonctionnel. Sans cela, vous verriez `"123.456"` et `"246.912"` comme nombres bruts, ce qui peut sembler correct dans le code mais pas lorsque vous collez les données dans une UI qui attend le même format qu’Excel.

---

## Étape 3 – Imprimer les données exportées (vérification)

Maintenant que nous disposons d’un `DataTable` rempli de chaînes formatées, affichons le contenu dans la console. Cela montre également que nous **obtenons le résultat de la formule** sans évaluer nous‑mêmes la formule.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Exécution du programme affiche :

```
123.456 | 246.912
```

Remarquez comment la deuxième colonne montre le **résultat de la formule**, et non le texte de la formule. C’est exactement ce dont vous avez besoin lorsque vous **exportez Excel avec mise en forme** pour un traitement en aval.

---

## Étape 4 – Convertir de plus grandes plages Excel (optionnel)

L’exemple ci‑dessus traite d’une petite tranche `A1:B1`, mais les scénarios réels nécessitent souvent l’exportation de tables complètes. La même méthode fonctionne pour n’importe quel bloc rectangulaire – il suffit d’ajuster les arguments `firstRow`, `firstColumn`, `totalRows` et `totalColumns`.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Astuce :** Si votre feuille possède déjà une ligne d’en‑tête, définissez `includeColumnNames` sur `true`. Aspose.Cells utilisera la première ligne de la plage comme noms de colonnes, ce qui est pratique lorsque vous liez ensuite le `DataTable` à une grille UI.

---

## Étape 5 – Pièges courants & comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Les nombres perdent les virgules ou les symboles monétaires** | `ExportAsString` est `false` ou `ExportNumberFormat` est omis | Définissez à la fois `ExportAsString = true` **et** `ExportNumberFormat = true`. |
| **Les cellules de formule renvoient le texte de la formule** | Vous n’avez pas appelé `CalculateFormula` avant l’exportation (nécessaire uniquement si le classeur n’est pas en auto‑calcul) | Activez le calcul automatique (`workbook.CalculateFormula()`) ou utilisez `ExportAsString` qui force l’évaluation. |
| **Les en‑têtes apparaissent comme des lignes de données** | `includeColumnNames` défini à `false` alors que votre plage inclut une ligne d’en‑tête | Définissez `includeColumnNames = true` pour traiter la première ligne comme noms de colonnes. |
| **Les grandes plages provoquent une pression mémoire** | Exporter la feuille entière en une fois charge tout en mémoire | Exportez par morceaux (par ex., 500 lignes à la fois) et fusionnez les `DataTable` si besoin. |

---

## Étape 6 – Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet, des déclarations `using` à `Main`. Collez‑le dans une application console et appuyez sur **F5** – vous verrez immédiatement la sortie formatée.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Sortie attendue**

```
123.456 | 246.912

Press any key to exit...
```

C’est l’ensemble du workflow **comment exporter Excel**, avec le format conservé, les résultats de formule évalués, et un `DataTable` propre prêt pour tout consommateur .NET.

---

## Conclusion

Nous avons couvert tout ce que vous devez savoir sur **comment exporter Excel** tout en **conservant le format des nombres**, **convertissant une plage Excel** en `DataTable`, et **obtenant les résultats de formule** sans analyse supplémentaire. La clé réside dans la configuration de `ExportTableOptions` : une fois que vous avez défini `ExportAsString` et `ExportNumberFormat` sur `true`, Aspose.Cells effectue le travail lourd pour vous.

À partir d’ici, vous pouvez :

- Brancher le `DataTable` dans un `DataGrid` WPF ou une vue ASP.NET MVC.  
- Écrire la table dans un fichier CSV tout en conservant la représentation visuelle exacte.  
- Étendre l’approche à plusieurs feuilles ou à des plages dynamiques.

N’hésitez pas à expérimenter avec différents formats (monétaire, pourcentage) et des blocs de données plus volumineux. Si vous rencontrez des particularités, revenez à la table **pièges courants** – elle couvre les difficultés les plus fréquentes lorsque vous **exportez Excel avec mise en forme**.

Bon codage, et que vos feuilles de calcul exportées soient toujours aussi soignées que les originales !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}