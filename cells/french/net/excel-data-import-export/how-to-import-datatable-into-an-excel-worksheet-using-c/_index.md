---
category: general
date: 2026-10-26
description: Apprenez à importer un DataTable dans une feuille Excel avec C# et Aspose.Cells,
  en conservant les styles et les en‑têtes en quelques lignes de code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: fr
lastmod: 2026-10-26
og_description: Comment importer un DataTable dans une feuille Excel à l’aide de C#
  et Aspose.Cells. Suivez ce guide complet pour préserver les styles, les en-têtes
  et le formatage.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: Comment importer un DataTable dans une feuille Excel – Guide pas à pas en
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Comment importer un DataTable dans une feuille Excel à l'aide de C#
url: /fr/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment importer un DataTable dans une feuille Excel avec C#

Si vous avez besoin de **comment importer datatable** dans une feuille Excel, ce guide montre les étapes exactes en C#. Que vous construisiez un moteur de reporting ou que vous exportiez les données d’une grille, vous verrez comment conserver les en‑têtes de colonnes et les styles de cellules intacts avec Aspose.Cells. La solution fonctionne avec .NET 6+ et ne nécessite que quelques lignes de code.

Importer un DataTable est une tâche courante lorsqu’on travaille avec des feuilles de calcul, mais les développeurs oublient souvent d’activer le transfert de style ou de passer correctement le drapeau d’en‑tête. Dans ce tutoriel, vous apprendrez à configurer **ImportTableOptions**, activer **ImportDataTableStyle**, et appeler `ImportDataTable` en toute sécurité. À la fin, vous disposerez d’une méthode prête à l’emploi que vous pourrez intégrer dans n’importe quel projet C#.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6 SDK ou une version ultérieure installé.
* Une copie sous licence de **Aspose.Cells for .NET** (l’essai gratuit suffit pour les tests).
* Une connaissance de base de `DataTable` et des concepts Excel.
* Un IDE tel que Visual Studio 2022 (tout éditeur supportant C# convient).

Aucun package NuGet supplémentaire n’est requis au‑delà de `Aspose.Cells`.

## Étape 1 : Récupérer les données sources dans un DataTable

La première chose à faire lorsque vous répondez à **comment importer datatable** est d’avoir les données prêtes. Dans la plupart des scénarios réels, le `DataTable` provient d’une requête de base de données, d’un parseur CSV ou d’une collection en mémoire. Voici un exemple minimal qui crée une table avec quelques lignes :

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*Pourquoi c’est important* : En construisant d’abord le `DataTable`, vous contrôlez l’ordre des colonnes, les types de données et les noms d’en‑tête — tout cela est préservé lorsque vous importerez plus tard la table dans une feuille Excel.

## Étape 2 : Créer `ImportTableOptions` et activer l’importation du style

Lorsque vous répondez à **comment importer datatable**, la décision suivante est de savoir si vous voulez le style visuel (polices, couleurs, bordures) déjà défini sur le `DataTable` source. Aspose.Cells fournit la classe `ImportTableOptions` pour un contrôle fin. Définir `ImportDataTableStyle = true` copie les informations de style vers la feuille cible.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*Pourquoi c’est important* : Sans activer `ImportDataTableStyle`, les cellules importées utiliseraient le style par défaut de la feuille, perdant tout formatage personnalisé appliqué au `DataTable`. Ce drapeau est essentiel pour une exportation soignée.

## Étape 3 : Importer le DataTable dans la feuille, en incluant les en‑têtes

Vous avez maintenant tout ce qu’il faut pour répondre à **comment importer datatable** dans un fichier Excel. Vous créez un classeur, choisissez une feuille, et appelez `ImportDataTable`. Le deuxième argument de la méthode (`true`) indique à Aspose.Cells d’écrire les en‑têtes de colonnes en première ligne.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

L’exécution de `ExportDataTableToExcel("Employees.xlsx")` produit un fichier `Employees.xlsx` où la première ligne contient **Id**, **Name** et **Department**, et chaque cellule conserve le style défini dans le `DataTable` original.

### Exemple complet exécutable

Voici un programme console complet et autonome qui montre **comment importer datatable** et enregistre le résultat dans le répertoire courant. Copiez‑collez‑le dans un nouveau projet console et exécutez‑le.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**Résultat attendu**  
Lorsque vous ouvrez `Employees.xlsx`, vous verrez :

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

Toutes les cellules conservent le style par défaut du DataTable (police, alignement). Si vous avez appliqué des styles personnalisés au `DataTable` avant l’importation, ces styles apparaissent identiquement dans la feuille parce que `ImportDataTableStyle` est réglé sur `true`.

## Problèmes courants et bonnes pratiques

| Problème | Pourquoi cela se produit | Comment l’éviter |
|----------|--------------------------|------------------|
| **En‑têtes manquantes** | Passage de `false` comme deuxième argument à `ImportDataTable` qui saute les noms de colonnes. | Utilisez toujours `true` lorsque vous avez besoin des en‑têtes, ou écrivez‑les manuellement avant l’importation. |
| **Style non transféré** | Oubli d’activer `ImportDataTableStyle`. | Définissez `ImportDataTableStyle = true` dans `ImportTableOptions`. |
| **Grandes tables entraînant un ralentissement** | Importation de millions de lignes sans pagination. | Importez par lots ou utilisez la surcharge `ImportDataTable` avec le paramètre `startRow` pour diffuser les données. |
| **Référence de feuille incorrecte** | Utilisation de `workbook.Worksheets[1]` alors qu’une seule feuille existe. | Utilisez `workbook.Worksheets[0]` ou créez une nouvelle feuille avec `workbook.Worksheets.Add()`. |
| **Expiration de licence** | La version d’essai d’Aspose.Cells ajoute un filigrane après 30 jours. | Appliquez une licence valide avec `License license = new License(); license.SetLicense("Aspose.Cells.lic");`. |

**Astuce pro** : Si vous devez appliquer un thème personnalisé après l’importation, appelez `ws.Cells.ApplyStyle(style)` où `style` est un objet `Style` que vous configurez une fois et réutilisez sur les lignes.

## Extension de la solution

Maintenant que vous savez **comment importer datatable**, vous pouvez explorer des scénarios connexes :

* **Importer plusieurs tables** – répétez l’importation sur différentes feuilles.
* **Mise en forme conditionnelle** – après l’importation, ajoutez des règles avec `ws.Cells.ApplyConditionalFormatting`.
* **Exporter vers CSV** – utilisez `workbook.Save("file.csv", SaveFormat.Csv)` si un format texte brut est requis.
* **Lire à nouveau dans un DataTable** – utilisez `ws.Cells.ExportDataTable` pour vérifier l’intégrité du aller‑retour.

Toutes ces extensions s’appuient sur le modèle de base démontré ci‑dessus : récupérer les données, configurer les options d’importation, et appeler une seule méthode Aspose.Cells.

## Conclusion

Vous disposez maintenant d’une réponse complète et prête pour la production à **comment importer datatable** dans une feuille Excel avec C#. Le tutoriel a couvert la récupération des données sources, la configuration de `ImportTableOptions` avec `ImportDataTableStyle`, et l’exécution de l’importation via `ImportDataTable`. En suivant l’exemple de code, vous préserverez automatiquement les en‑têtes et les styles, et vous pourrez adapter le modèle à des ensembles de données plus volumineux, à plusieurs feuilles ou à des besoins de formatage supplémentaires.

Prêt à automatiser votre flux de reporting ? Essayez de remplacer le `DataTable` d’exemple par une vraie requête de base de données, expérimentez avec des styles de cellule personnalisés, et intégrez la méthode dans votre couche de service existante. Bon codage !


## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Import Arrays into Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [How to Import XML Data into Excel with Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [How to Import HTML-Formatted DataTables into Excel Using Aspose.Cells for .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}