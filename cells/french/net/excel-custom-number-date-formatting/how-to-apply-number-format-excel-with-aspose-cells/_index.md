---
category: general
date: 2026-10-10
description: Appliquer rapidement le format numérique dans Excel en important un DataTable,
  en définissant les formats de date et de devise, et en conservant la ligne d’en‑tête
  Excel en une seule étape.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: fr
lastmod: 2026-10-10
og_description: Appliquer le format numérique Excel en C# avec Aspose.Cells. Apprenez
  à définir le format de date Excel, le format monétaire Excel et à conserver la ligne
  d’en‑tête Excel lors de l’importation d’un DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Appliquer le format de nombre Excel en C# – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Comment appliquer le format de nombre dans Excel avec Aspose.Cells
url: /fr/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment appliquer un format de nombre Excel avec Aspose.Cells

Si vous devez **appliquer un format de nombre Excel** lors du chargement de données depuis un `DataTable`, ce guide vous montre exactement comment faire. Vous apprendrez également à **définir le format de date Excel**, **définir le format de devise Excel**, et à **conserver la ligne d’en-tête Excel** pendant l’importation, de sorte que la feuille de calcul résultante ait un aspect professionnel sans traitement supplémentaire.

Nous couvrirons tout, de l’installation de la bibliothèque à l’écriture d’un extrait complet et exécutable. À la fin, vous pourrez importer n’importe quel `DataTable` dans un classeur Excel, formater automatiquement les colonnes numériques et garder la ligne d’en‑tête intacte — le tout en quelques lignes de C#.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.6+)
* Visual Studio 2022 (ou tout IDE C# de votre choix)
* **Aspose.Cells for .NET** – installer via NuGet :

```bash
dotnet add package Aspose.Cells
```

* Une source `DataTable` – l’exemple utilise une méthode d’aide `GetTable()` qui renvoie des données d’exemple.

> **Astuce :** Aspose.Cells est une bibliothèque commerciale, mais elle propose un mode d’évaluation gratuit qui désactive le filigrane pendant 30 jours maximum.

## Étape 1 : Créer un classeur et accéder à la première feuille

L’objet `Workbook` est le point d’entrée pour toutes les opérations Excel. Créer un nouveau classeur vous fournit une feuille par défaut à l’index 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Pourquoi cette étape ?*  
`Workbook` gère le format de fichier, le moteur de calcul et le référentiel de styles. Accéder à `Worksheet` dès le départ nous permet de passer la feuille cible à la méthode d’importation plus tard.

## Étape 2 : Récupérer les données source sous forme de DataTable

Dans les projets réels, les données proviennent souvent d’une requête de base de données, d’un parseur CSV ou d’une réponse d’API. À titre d’illustration, nous générons un `DataTable` simple avec trois colonnes : **Product**, **Price**, et **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Pourquoi cette étape ?*  
Un `DataTable` fournit une représentation tabulaire en mémoire que Aspose.Cells peut importer directement, en préservant l’ordre des colonnes et les types de données.

## Étape 3 : Préparer un tableau `Style` – un style par colonne

Aspose.Cells vous permet d’appliquer un style distinct à chaque colonne lors de l’importation en passant un tableau d’objets `Style`. La longueur du tableau doit correspondre au nombre de colonnes du tableau source.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Pourquoi cette étape ?*  
Si vous omettez la création explicite (`CreateStyle()`), tenter de définir `Number` déclenchera une `NullReferenceException`. Initialiser chaque `Style` garantit que les affectations ultérieures réussiront.

## Étape 4 : Attribuer les formats de nombre – devise et date

Excel identifie les formats de nombre intégrés par leur ID.  
* **14** – Devise (ex. : `$1,234.00`)  
* **22** – Date courte (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Remarque :** Si vous avez besoin d’un format personnalisé (ex. : `"¥#,##0.00"`), utilisez `Style.Custom = "¥#,##0.00"` à la place d’un ID intégré.

*Pourquoi cette étape ?*  
Appliquer le **format de nombre** correct au moment de l’importation élimine la nécessité d’un second passage qui parcourrait les cellules pour modifier le formatage. Cela garantit également que le **format excel des cellules date** et le **set currency format excel** restent cohérents sur toutes les lignes.

## Étape 5 : Importer le DataTable tout en conservant la ligne d’en‑tête

La méthode `ImportDataTable` peut copier les données, garder la première ligne comme en‑tête, et appliquer les styles de colonne que nous avons préparés.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Résultat attendu** – Ouvrez `FormattedReport.xlsx` et vous verrez :

| Produit | Prix (devise) | Date de sortie (date) |
|---------|----------------|-----------------------|
| Widget A| $12.99         | 05/01/2023            |
| Widget B| $23.50         | 06/15/2023            |
| Widget C| $7.75          | 07/30/2023            |

La ligne d’en‑tête est intacte, la colonne **Price** affiche le symbole de devise, et la colonne **ReleaseDate** montre un format de date courte — le tout sans aucun code de style supplémentaire.

### Gestion des cas limites courants

| Situation                               | Solution |
|----------------------------------------|----------|
| **Plus de colonnes que de styles**           | Assurez‑vous que `columnStyles.Length` soit égal à `sourceTable.Columns.Count`. Les entrées manquantes utilisent le style par défaut du classeur. |
| **Valeurs null dans les colonnes numériques**     | Excel traite `null` comme une cellule vide ; le format de nombre s’applique toujours lorsqu’une valeur est saisie ultérieurement. |
| **Devise locale personnalisée**    | Utilisez `columnStyles[i].Custom = "\"€\"#,##0.00"` et définissez `columnStyles[i].Number = -1` pour désactiver l’ID intégré. |
| **Tables volumineuses ( > 100 000 lignes )**    | Envisagez d’utiliser la surcharge `ImportDataTable` avec `ImportTableOptions` pour diffuser les données et réduire la pression mémoire. |
| **Appliquer le même style à plusieurs colonnes** | Réutilisez la même instance `Style` dans le tableau (ex. : `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bonus : Utiliser une chaîne de format personnalisée

Si les IDs intégrés ne répondent pas à vos besoins, vous pouvez définir un format de nombre personnalisé :

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

Cette approche vous donne un contrôle total sur le **format excel des cellules date** et le **set currency format excel** au‑delà des IDs prédéfinis.

## Conclusion

Vous savez maintenant comment **appliquer un format de nombre Excel** de façon efficace lors de l’importation d’un `DataTable` avec Aspose.Cells. En créant un tableau `Style` par colonne, en assignant des IDs de nombre intégrés ou personnalisés, et en utilisant la surcharge `ImportDataTable` qui **preserve header row excel**, vous pouvez générer des feuilles prêtes à publier en une seule opération.

### Et après ?

* Explorez le **set date format excel** avec des modèles personnalisés comme `"dddd, mmmm dd, yyyy"`.
* Combinez cette technique avec le **conditional formatting** pour mettre en évidence les valeurs hors plage.
* Utilisez le **format excel cells date** dans les tableaux croisés dynamiques ou les graphiques pour des rapports dynamiques.

N’hésitez pas à expérimenter avec différents IDs de nombre ou chaînes personnalisées afin de respecter le guide de style de votre organisation. Bon codage !

## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [apply number format excel – Guide étape par étape pour le formatage des colonnes](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Set date format in Excel with C# – Guide complet de formatage d’importation](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}