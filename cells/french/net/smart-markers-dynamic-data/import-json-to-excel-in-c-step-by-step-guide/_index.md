---
category: general
date: 2026-08-11
description: Importer du JSON vers Excel en utilisant C# et Aspose.Cells. Charger
  le JSON dans un DataSet, traiter les smart markers et enregistrer au format xlsx
  en quelques minutes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- import json to excel
- convert json to xlsx
- export json data excel
- load json into dataset
- save workbook c#
language: fr
lastmod: 2026-08-11
og_description: Importer JSON dans Excel avec C# et Aspose.Cells. Ce guide montre
  comment charger le JSON dans un DataSet, traiter les smart markers et enregistrer
  le classeur au format xlsx, permettant une exportation de données fluide.
og_image_alt: Screenshot of C# code importing JSON into an Excel workbook using Aspose.Cells
og_title: Importer JSON vers Excel avec C# – guide complet étape par étape
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Import json to excel using C# and Aspose.Cells. Load JSON into a DataSet,
    process smart markers, and save as xlsx in minutes.
  headline: Import json to excel in C# – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: '`ReadJson` still creates an empty `DataTable`. The smart marker will
      produce only the header row, which is often the desired outcome for reporting
      templates.'
    question: What if the JSON array is empty?
  - answer: Yes. Load each array into its own `DataTable` within the same `DataSet`,
      then call `ProcessSmartMarkers` on each worksheet, referencing the appropriate
      table name in the marker (e.g., `&=Table(Orders)`).
    question: Can I import multiple JSON arrays into different sheets?
  - answer: After `ReadJson`, reorder columns by manipulating `dataSet.Tables[0].Columns`
      before processing the smart marker.
    question: How do I control column order?
  - answer: 'If you need the raw JSON string in a cell, skip the `DataSet` step and
      assign it directly: `worksheet.Cells["A1"].PutValue(jsonData);`'
    question: Is it possible to write JSON directly to a single cell as a string?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- JSON
- Excel automation
title: Importer JSON dans Excel en C# – guide étape par étape
url: /fr/net/smart-markers-dynamic-data/import-json-to-excel-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Importer du JSON vers Excel en C# – guide étape par étape

Si vous devez importer du JSON vers Excel avec C#, ce tutoriel vous guide à travers l’ensemble du processus. Vous apprendrez comment charger du JSON dans un DataSet, appliquer un smart marker et enregistrer le résultat sous forme de fichier xlsx. La même approche vous permet également de convertir du JSON en xlsx pour les pipelines de reporting ou les scripts de migration de données.

Le guide couvre chaque ligne de code requise, explique pourquoi chaque étape est importante et met en évidence les pièges courants. À la fin, vous pourrez exporter des données JSON vers Excel sans écrire de parseurs personnalisés, et vous comprendrez comment enregistrer un classeur C# de manière prête pour la production. Aucun outil externe autre qu’Aspose.Cells n’est nécessaire.

## Prérequis

- .NET 6.0 ou version ultérieure installé  
- Visual Studio 2022 (ou tout IDE supportant .NET)  
- Package NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
- Un fichier modèle Excel contenant un smart marker (par ex., `Template.xlsx`)  

Le modèle doit contenir une seule cellule avec le smart marker `&=Table(Data)` où `Data` correspond au nom du DataTable que vous passerez.

## Importer du JSON vers Excel – configurer le projet

Créez une nouvelle application console et ajoutez la référence Aspose.Cells :

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // The complete workflow is demonstrated in the following steps.
        }
    }
}
```

Ajouter les directives `using` en haut permet au compilateur de localiser `DataSet`, `Workbook` et les types associés. Cette base est requise pour chaque opération ultérieure.

## Convertir du JSON en xlsx – charger le JSON dans un DataSet

La première étape fonctionnelle consiste à transformer la chaîne JSON en un `DataSet`. Aspose.Cells fournit une extension pratique `ReadJson` qui analyse un tableau d’objets directement dans une table.

```csharp
// Step 1: Define the JSON source
string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

// Step 2: Load the JSON into a DataSet
DataSet dataSet = new DataSet();
dataSet.ReadJson(jsonData);
```

**Pourquoi c’est important :**  
`ReadJson` crée automatiquement un `DataTable` nommé `Table` (ou le nom de l’élément racine) et remplit les colonnes en fonction des clés JSON. Cela élimine les boucles manuelles et garantit que les types de données sont correctement inférés. Si votre JSON contient des objets imbriqués, Aspose.Cells les aplatit en tables séparées que vous pourrez référencer ultérieurement.

**Astuce :**  
Si la charge JSON est volumineuse, envisagez de la diffuser avec un `StringReader` afin d’éviter de charger toute la chaîne en mémoire.

## Exporter des données JSON vers Excel – ouvrir le modèle Excel avec un smart marker

Ensuite, ouvrez le classeur contenant le smart marker. Le smart marker indique à Aspose.Cells où insérer les données du `DataSet`.

```csharp
// Step 3: Open the Excel template that contains a smart marker
Workbook workbook = new Workbook("YOUR_DIRECTORY/Template.xlsx");
```

**Pourquoi c’est important :**  
Le modèle sépare le formatage du code. Vous pouvez concevoir l’apparence finale dans Excel (polices, bordures, mise en forme conditionnelle) et laisser la bibliothèque gérer l’insertion des données. La syntaxe du smart marker `&=Table(Data)` indique au moteur d’écrire le `DataTable` complet dans la cellule où se trouve le marqueur.

## Exporter des données JSON vers Excel – traiter le smart marker

Traitez maintenant le smart marker, en passant le `DataTable` créé à partir du JSON.

```csharp
// Step 4: Process the smart marker, writing the entire array into a single cell
workbook.Worksheets[0].ProcessSmartMarkers(dataSet.Tables[0]);
```

**Pourquoi c’est important :**  
`ProcessSmartMarkers` lit le marqueur, étend la table verticalement et conserve le formatage de la cellule d’origine. La méthode respecte également les largeurs de colonne et applique automatiquement les formats numériques en fonction des types .NET sous-jacents.

**Cas particulier :**  
Si la cellule cible contient déjà des données, la méthode les écrase. Pour préserver le contenu existant, placez le marqueur dans une zone dédiée du modèle.

## Enregistrer le classeur C# – écrire le fichier final

Enfin, enregistrez le classeur sous forme de fichier `.xlsx`. Vous pouvez choisir n’importe quel emplacement où votre application peut écrire.

```csharp
// Step 5: Save the resulting workbook
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx", SaveFormat.Xlsx);
```

**Pourquoi c’est important :**  
Spécifier `SaveFormat.Xlsx` garantit que la sortie respecte la norme Open XML, la rendant lisible par les applications de tableur modernes. Si vous avez besoin d’un fichier `.xls` hérité, remplacez `SaveFormat.Xlsx` par `SaveFormat.Excel97To2003`.

**Astuce pro :**  
Utilisez `SaveOptions` pour contrôler le niveau de compression des gros fichiers, par ex., `var opts = new XlsSaveOptions { CompressionLevel = CompressionLevel.Maximum }; workbook.Save("out.xls", opts);`

## Code source complet

Assembler toutes les étapes donne un programme exécutable :

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Define the JSON source
            string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

            // Load the JSON into a DataSet
            DataSet dataSet = new DataSet();
            dataSet.ReadJson(jsonData);

            // Open the Excel template that contains a smart marker
            Workbook workbook = new Workbook("YOUR_DIRECTORY/Template.xlsx");

            // Process the smart marker, writing the entire array into a single cell
            workbook.Worksheets[0].ProcessSmartMarkers(dataSet.Tables[0]);

            // Save the resulting workbook
            workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx", SaveFormat.Xlsx);

            Console.WriteLine("JSON has been imported to Excel successfully.");
        }
    }
}
```

**Sortie attendue :**  
L’exécution du programme crée `JsonSingleCell.xlsx`. L’ouverture du fichier montre les deux lignes (`John`, `30` et `Anna`, `25`) remplissant la zone sous la cellule du smart‑marker, en conservant tout format d’en‑tête que vous avez défini dans `Template.xlsx`.

![Exemple de code d’importation JSON vers Excel](image.png "Exemple de code d’importation JSON vers Excel")

## Questions fréquentes et comment les gérer

- **Que faire si le tableau JSON est vide ?**  
  `ReadJson` crée toujours un `DataTable` vide. Le smart marker ne produira que la ligne d’en‑tête, ce qui est souvent le résultat souhaité pour les modèles de reporting.

- **Puis‑je importer plusieurs tableaux JSON dans différentes feuilles ?**  
  Oui. Chargez chaque tableau dans son propre `DataTable` au sein du même `DataSet`, puis appelez `ProcessSmartMarkers` sur chaque feuille, en référant le nom de table approprié dans le marqueur (par ex., `&=Table(Orders)`).

- **Comment contrôler l’ordre des colonnes ?**  
  Après `ReadJson`, réordonnez les colonnes en manipulant `dataSet.Tables[0].Columns` avant de traiter le smart marker.

- **Est‑il possible d’écrire le JSON directement dans une seule cellule sous forme de chaîne ?**  
  Si vous avez besoin de la chaîne JSON brute dans une cellule, sautez l’étape `DataSet` et affectez‑la directement : `worksheet.Cells["A1"].PutValue(jsonData);`

## Conclusion

Vous savez maintenant comment importer du JSON vers Excel en C# avec Aspose.Cells, depuis le chargement du JSON dans un DataSet jusqu’au traitement d’un smart marker et l’enregistrement du classeur C#. Cette solution de bout en bout vous permet de convertir rapidement du JSON en xlsx, d’exporter des données JSON

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Importer facilement du JSON dans Excel avec Aspose.Cells pour .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)
- [Importer des données JSON dans Excel avec Aspose.Cells Java&#58; guide complet](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Importer efficacement du JSON vers Excel avec Aspose.Cells pour Java&#58; guide complet](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}