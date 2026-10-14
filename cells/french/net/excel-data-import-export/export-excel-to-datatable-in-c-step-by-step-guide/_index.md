---
category: general
date: 2026-03-25
description: Apprenez à exporter Excel vers DataTable en C# rapidement. Ce tutoriel
  couvre l'exportation d'Excel avec les noms de colonnes et l'exportation des données
  Excel en tant que chaîne pour une gestion fiable des données.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: fr
og_description: Exportez Excel vers DataTable en C# avec les noms de colonnes et la
  conversion en chaîne. Suivez ce tutoriel concis pour une solution prête à l'emploi.
og_title: Exporter Excel vers DataTable en C# – Guide complet
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: Exporter Excel vers DataTable en C# – Guide étape par étape
url: /fr/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter Excel vers DataTable en C# – Guide étape par étape

Vous avez déjà eu besoin d'**exporter Excel vers DataTable** mais vous ne saviez pas quels indicateurs activer ? Vous n'êtes pas seul—de nombreux développeurs rencontrent le même obstacle lorsqu'ils essaient pour la première fois d'extraire les données d'une feuille de calcul dans un `DataTable`.  

Bonne nouvelle ? En quelques lignes de code, vous pouvez **exporter Excel avec les noms de colonnes** et même **exporter les données Excel en tant que chaîne** pour éviter les maux de tête liés aux incompatibilités de type. Vous trouverez ci‑dessous un exemple complet et exécutable ainsi que le « pourquoi » de chaque paramètre, afin que vous puissiez l'adapter à n'importe quel projet sans conjecture.

## Ce que couvre ce tutoriel

* Comment créer un classeur en mémoire (pas de fichier physique nécessaire).  
* Remplir quelques lignes d'exemple afin de voir le résultat immédiatement.  
* Configurer `ExportTableOptions` pour que chaque cellule soit traitée comme une chaîne.  
* Exporter une plage rectangulaire vers un `DataTable` tout en conservant la première ligne comme en‑têtes de colonnes.  
* Vérifier le résultat et afficher la première ligne dans la console.  

Aucun lien vers une documentation externe n'est requis—tout ce dont vous avez besoin se trouve ici. Si vous avez déjà un fichier Excel sur le disque, remplacez simplement la ligne de création du classeur par `new Workbook("path/to/file.xlsx")` et le tour est joué.

---

## Étape 1 : Configurer le projet et ajouter le package NuGet Aspose.Cells

Avant d'écrire du code, assurez‑vous que votre projet référence **Aspose.Cells for .NET** (la bibliothèque qui fournit la classe `Workbook`). Vous pouvez l'ajouter via le gestionnaire de packages NuGet :

```bash
dotnet add package Aspose.Cells
```

> **Astuce :** Utilisez la dernière version stable (en mars 2026, c’est la 22.12) pour obtenir les dernières corrections de bugs et améliorations de performances.

## Étape 2 : Créer un classeur et le remplir avec des données d'exemple

Nous commencerons avec un tout nouveau `Workbook` et écrirons quelques lignes afin que vous puissiez voir l'exportation en action. Cette étape montre également **comment exporter excel vers datatable** lorsque les données source n'existent qu'en mémoire.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*Pourquoi c’est important :* En insérant d'abord la ligne d’en‑tête (`A1` & `B1`), nous pouvons ensuite indiquer à l'exportateur de considérer la première ligne comme les noms de colonnes—c’est exactement ce que signifie **exporter excel avec les noms de colonnes**.

## Étape 3 : Indiquer à Aspose.Cells de traiter chaque cellule comme une chaîne

Lorsque vous exportez des cellules numériques ou de date, Aspose tente d’inférer le type .NET. Cela peut engendrer des bugs subtils si votre code en aval attend des chaînes. Le drapeau `ExportTableOptions.ExportAsString` force une conversion uniforme en chaîne.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*Pourquoi l’utiliser ?* Imaginez une colonne qui contient parfois des nombres et parfois du texte (par ex., « 00123 » vs. « ABC »). En exportant tout en tant que chaîne, vous évitez de perdre les zéros initiaux ou de déclencher des exceptions de conversion de type.

## Étape 4 : Exporter la plage souhaitée vers un DataTable

Nous allons maintenant réellement **exporter excel to datatable**. La méthode `ExportDataTable` prend la ligne/colonne de départ, le nombre de lignes/colonnes, un drapeau pour l'extraction des noms de colonnes, ainsi que les options que nous venons de créer.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*Ce qui se passe en coulisses :*  
- `startRow: 0` pointe sur la première ligne Excel (la ligne d’en‑tête).  
- `exportColumnNames: true` indique à Aspose de transférer « Name » et « Age » dans la collection de colonnes du `DataTable`.  
- `totalRows`/`totalColumns` peuvent être supérieurs aux données réelles ; les cellules excédentaires deviennent des chaînes vides grâce à `ExportAsString`.

## Étape 5 : Vérifier le résultat – Afficher la première ligne

Un affichage rapide dans la console prouve que la conversion a réussi et que les noms de colonnes sont intacts.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Sortie attendue**

```
First row: Alice, 30
```

Si vous modifiez les données d'exemple, la console reflétera automatiquement ces changements—aucun code supplémentaire n'est nécessaire.

## Questions fréquentes & cas limites

| Question | Réponse |
|----------|--------|
| **Puis-je exporter une feuille qui existe déjà sur le disque ?** | Oui—remplacez `new Workbook()` par `new Workbook("myFile.xlsx")`. Le reste des étapes reste identique. |
| **Que se passe-t-il si mon fichier Excel contient des cellules fusionnées ?** | Les cellules fusionnées sont déroulées ; la valeur de la cellule en haut à gauche est utilisée pour toute la plage fusionnée. |
| **Dois‑je me soucier des formats numériques spécifiques à une culture ?** | Pas lorsque `ExportAsString = true` ; tout arrive sous forme de chaîne brute affichée dans Excel. |
| **Combien de lignes puis‑je exporter en une fois ?** | Aspose.Cells peut gérer des millions de lignes, mais la consommation de mémoire augmente avec la taille du `DataTable`. Envisagez la pagination si vous atteignez les limites. |
| **Qu’en est‑il des colonnes masquées ?** | Les colonnes masquées sont exportées sauf si vous définissez `ExportHiddenColumns = false` dans `ExportTableOptions`. |

## Bonus : Exporter vers un CSV au lieu d'un DataTable

Parfois vous pouvez préférer un fichier plat. Les mêmes `ExportTableOptions` peuvent être réutilisés avec `ExportDataTableToCSV` :

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

Cette ligne unique vous fournit un CSV prêt à l'importation tout en **exporting excel data as string**.

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

Exécutez le programme (`dotnet run`) et vous verrez le résultat de **export excel to datatable** affiché dans la console. Remplacez les données d'exemple, modifiez `totalRows`/`totalColumns`, ou pointez le classeur vers un vrai fichier—tout s'adapte.

## Conclusion

Vous disposez maintenant d’une **solution complète et autonome pour exporter Excel vers DataTable** en C#. En configurant `ExportTableOptions.ExportAsString`, vous garantissez que **export excel data as string**, et en définissant `exportColumnNames: true`, vous obtenez les en‑têtes de colonnes familières que vous attendez lorsque vous **export excel with column names**.  

À partir de là, vous pouvez :

* Alimenter le `DataTable` dans Entity Framework ou Dapper pour des insertions en masse.  
* Le transmettre à un moteur de reporting comme **FastReport** ou **RDLC**.  
* Le convertir en JSON pour une réponse d'API (`JsonConvert.SerializeObject(table)`).

N'hésitez pas à expérimenter—essayez peut‑être d'exporter une feuille plus grande, ou combinez cela avec **how to export excel to datatable** depuis un partage réseau. Le modèle reste le même, et le code est prêt pour la production.

![Diagramme du flux de conversion Excel → DataTable – export excel to datatable](https://example.com/placeholder.png "diagramme export excel to datatable")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}