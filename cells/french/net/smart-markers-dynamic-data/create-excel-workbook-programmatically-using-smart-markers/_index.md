---
category: general
date: 2026-09-24
description: Créer un classeur Excel de façon programmatique, apprendre à créer plusieurs
  feuilles détaillées, puis enregistrer le classeur au format xlsx avec un exemple
  C# clair.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook programmatically
- how to create multiple detail sheets
- save workbook as xlsx file
language: fr
lastmod: 2026-09-24
og_description: Créer un classeur Excel par programmation, voir comment créer plusieurs
  feuilles de détail et enregistrer le classeur au format xlsx dans un exemple unique
  et exécutable.
og_image_alt: Screenshot of an Excel workbook created programmatically in C#
og_title: Créer un classeur Excel par programmation – guide complet C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Create Excel workbook programmatically and learn how to create multiple
    detail sheets, then save workbook as xlsx file with a clear C# example.
  headline: Create Excel workbook programmatically using Smart Markers
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Créer un classeur Excel de manière programmatique à l'aide des Smart Markers
url: /fr/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel programmé à l'aide de Smart Markers

Si vous devez **créer un classeur Excel programmé**, ce guide vous montre exactement comment le faire avec Aspose.Cells .NET. Vous découvrirez également **comment créer plusieurs feuilles de détail** à partir d'une source de données unique et enfin **enregistrer le classeur au format xlsx** sans aucune étape manuelle.  

La solution est autonome : nous parcourons chaque ligne de code, expliquons pourquoi chaque paramètre est important et couvrons les pièges courants tels que les noms de feuilles en double. À la fin, vous disposerez d’une application console prête à l’exécution qui génère un classeur avec une feuille maître et un ensemble de feuilles de détail.

## Ce dont vous aurez besoin

| Prérequis | Raison |
|--------------|--------|
| .NET 6.0 SDK or later | Fournit le runtime pour l'application console C# |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Fournit les classes `Workbook`, `SmartMarkerProcessor` et `SmartMarkerOptions` |
| A simple data source (e.g., `DataTable` or a list of objects) | Fournit les valeurs que les Smart Markers développeront |
| Visual Studio 2022 or any editor that supports .NET | Facilite la compilation et l'exécution du code |

> **Astuce** : Installez le package Aspose.Cells via la CLI avant de commencer :  
> `dotnet add package Aspose.Cells`

## Étape 1 : Configurer le projet et importer les espaces de noms

Créez un nouveau projet console et importez les espaces de noms requis.

```csharp
using System;
using System.Data;               // For DataTable (sample data source)
using Aspose.Cells;              // Core Excel API
using Aspose.Cells.SmartMarkers; // Smart Marker processing
```

*Pourquoi c'est important* : `Aspose.Cells` gère le cycle de vie du classeur, tandis que `Aspose.Cells.SmartMarkers` vous fournit le puissant moteur Smart Marker capable de générer de nombreuses feuilles à partir d'un seul modèle.

## Étape 2 : Créer le classeur Excel programmé

La première action concrète consiste à instancier un `Workbook`. Cet objet représente l'intégralité du fichier Excel en mémoire.

```csharp
// Step 2: Create a new workbook (or load an existing template)
Workbook workbook = new Workbook(); // an empty workbook with one default sheet
```

Si vous préférez démarrer à partir d'un modèle contenant déjà des lignes d'en-tête ou du formatage, remplacez `new Workbook()` par `new Workbook("Template.xlsx")`. Le reste du processus fonctionne de la même manière.

## Étape 3 : Préparer un modèle Smart Marker

Les Smart Markers fonctionnent sur le contenu des cellules contenant des espaces réservés comme `&=Employees.Name`. Pour ce tutoriel, nous ajouterons un modèle simple directement via le code, mais vous pouvez également modifier la feuille manuellement dans Excel.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Write a header row
sheet.Cells["A1"].PutValue("Employee Report");

// Insert a Smart Marker that will generate a detail sheet for each employee
sheet.Cells["A3"].PutValue("&=Employees.Name");

// Optional: add column titles for the detail sheet
sheet.Cells["A4"].PutValue("Name");
sheet.Cells["B4"].PutValue("Department");
sheet.Cells["C4"].PutValue("Salary");
```

*Pourquoi c'est important* : L'espace réservé `&=Employees.Name` indique au processeur Smart Marker d'itérer sur la collection `Employees`. Chaque itération générera une nouvelle feuille de calcul car nous configurerons le processeur pour créer une **feuille de détail** pour chaque ligne.

## Étape 4 : Construire une source de données contenant plusieurs lignes

Nous utiliserons un `DataTable` comme moyen rapide de simuler une collection d'enregistrements d'employés.

```csharp
// Step 4: Create a DataTable with sample employee data
DataTable employees = new DataTable("Employees");
employees.Columns.Add("Name", typeof(string));
employees.Columns.Add("Department", typeof(string));
employees.Columns.Add("Salary", typeof(decimal));

employees.Rows.Add("Alice Johnson", "Finance", 72000);
employees.Rows.Add("Bob Smith", "Engineering", 95000);
employees.Rows.Add("Carol Lee", "Marketing", 63000);
```

Vous pouvez remplacer cela par n'importe quel `IEnumerable` (par ex., `List<Employee>`) – les Smart Markers acceptent toute source de données implémentant `IEnumerable`.

## Étape 5 : Configurer les options Smart Marker – comment créer plusieurs feuilles de détail

Par défaut, les Smart Markers écrivent les données dans la même feuille. Pour générer **plusieurs feuilles de détail**, vous devez définir la propriété `DetailSheetNewName`. Cela montre également **comment créer plusieurs feuilles de détail** sans conflits de noms.

```csharp
// Step 5: Configure Smart Marker options
SmartMarkerOptions smOptions = new SmartMarkerOptions
{
    // Each iteration will create a new sheet named "Detail"
    DetailSheetNewName = "Detail"
};
```

Si la source de données contient des noms en double, le processeur ajoute automatiquement un suffixe numérique (par ex., `Detail_1`, `Detail_2`). Cela évite les erreurs d'exécution et garantit que toutes les feuilles de détail sont enregistrées.

## Étape 6 : Traiter les Smart Markers

Nous invoquons maintenant le processeur, en passant la source de données et les options que nous venons de définir.

```csharp
// Step 6: Process Smart Markers
workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);
```

*Pourquoi c'est important* : Le processeur lit l'espace réservé `&=Employees.Name`, itère sur chaque ligne de `employees`, crée une nouvelle feuille nommée « Detail », et écrit les données de la ligne dans cette feuille. La feuille originale reste comme feuille de synthèse ou maître.

## Étape 7 : Enregistrer le classeur au format xlsx

Enfin, persistez le classeur sur le disque en utilisant le modèle **enregistrer le classeur au format xlsx**.

```csharp
// Step 7: Save the resulting workbook
string outputPath = @"./output/detail.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

L'énumération `SaveFormat.Xlsx` garantit que le fichier est stocké au format moderne Office Open XML, compatible avec Excel 2007+ et la plupart des services cloud.

## Exemple complet et exécutable

Copiez le code suivant dans `Program.cs` d'un projet console .NET et exécutez-le. Le programme générera `detail.xlsx` dans le dossier `output`, contenant une feuille maître et trois feuilles de détail (une par employé).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create an empty workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Build a simple template with a Smart Marker
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Employee Report");
            sheet.Cells["A3"].PutValue("&=Employees.Name");
            sheet.Cells["A4"].PutValue("Name");
            sheet.Cells["B4"].PutValue("Department");
            sheet.Cells["C4"].PutValue("Salary");

            // 3️⃣ Prepare the data source
            DataTable employees = new DataTable("Employees");
            employees.Columns.Add("Name", typeof(string));
            employees.Columns.Add("Department", typeof(string));
            employees.Columns.Add("Salary", typeof(decimal));

            employees.Rows.Add("Alice Johnson", "Finance", 72000);
            employees.Rows.Add("Bob Smith", "Engineering", 95000);
            employees.Rows.Add("Carol Lee", "Marketing", 63000);

            // 4️⃣ Configure Smart Marker options (how to create multiple detail sheets)
            SmartMarkerOptions smOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail"
            };

            // 5️⃣ Process the markers
            workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);

            // 6️⃣ Save workbook as xlsx file
            string outPath = "./output/detail.xlsx";
            workbook.Save(outPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outPath}");
        }
    }
}
```

**Sortie attendue**

- `output/detail.xlsx` contains:
  - **Sheet1** – le modèle original avec l'en-tête « Employee Report ».
  - **Detail** – première feuille de détail avec l’enregistrement d’Alice.
  - **Detail_1** – deuxième feuille de détail avec l’enregistrement de Bob.
  - **Detail_2** – troisième feuille de détail avec l’enregistrement de Carol.

Ouvrez le fichier dans Excel et vous verrez chaque employé sur sa propre feuille, prouvant que nous avons réussi à **créer plusieurs feuilles de détail** et à **enregistrer le classeur au format xlsx**.

## Questions fréquentes & gestion des cas limites

| Question | Réponse |
|----------|--------|
| *Et si j’ai besoin d’un nom personnalisé pour chaque feuille de détail ?* | Définissez `DetailSheetNewName = "Employee_"` et incluez une colonne nommée `SheetName` dans la source de données. Le processeur ajoutera la valeur de `SheetName` au nom de base. |
| *Puis-je conserver la feuille originale comme résumé de tous les détails ?* | Oui. La feuille maître reste intacte ; vous pouvez ajouter des formules qui référencent les feuilles de détail générées. |
| *Que se passe-t-il lorsque la source de données est vide ?* | Aucune feuille de détail n’est créée, mais le classeur est tout de même enregistré. Envisagez de vérifier `employees.Rows.Count` avant le traitement si vous avez besoin d’une gestion spéciale. |
| *Est-il possible d’utiliser un fichier de modèle existant ?* | Remplacez `new Workbook()` par `new Workbook("Template.xlsx")`. Toute la logique Smart Marker fonctionne de la même manière. |

## Conclusion

Vous savez maintenant **comment créer un classeur Excel programmé**, comment **créer plusieurs feuilles de détail** à l'aide des Smart Markers, et comment **enregistrer le classeur au format xlsx** avec Aspose.Cells. L'exemple complet peut être adapté pour des factures, des rapports ou tout scénario nécessitant une sortie Excel maître‑détail.

### Prochaines étapes

- Explorez d'autres fonctionnalités des Smart Markers telles que les **group markers** et le **conditional formatting**.
- Remplacez le `DataTable` par une vraie requête de base de données pour générer des rapports à grande échelle.
- Utilisez `Workbook.Save("output.pdf", SaveFormat.Pdf)` pour exporter les mêmes données en PDF à des fins de distribution.

N'hésitez pas à expérimenter différents schémas de nommage, styles ou feuilles supplémentaires — vos nouvelles compétences en génération programmatique d'Excel sont prêtes pour une utilisation en production. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Créer un classeur Excel C# – Ajouter un commentaire et enregistrer en XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Créer un nouveau classeur en C# – Ajouter une formule et enregistrer le fichier Excel](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Créer un classeur Excel C# – Insérer du JSON et enregistrer en XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}