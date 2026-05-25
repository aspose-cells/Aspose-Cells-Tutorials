---
category: general
date: 2026-03-18
description: Apprenez à générer un fichier Excel à partir de JSON avec C#, à autoriser
  les noms de feuilles dupliqués, à créer une feuille de détail et à enregistrer le
  classeur avec C# en quelques minutes.
draft: false
keywords:
- generate excel from json
- allow duplicate sheet names
- how to create detail sheet
- save workbook c#
- smartmarker options
- aspnet cells integration
language: fr
og_description: Générez un fichier Excel à partir de JSON avec C#. Ce guide montre
  comment autoriser les noms de feuilles en double, créer une feuille de détails et
  enregistrer le classeur C# avec Aspose.Cells.
og_title: Générer un Excel à partir de JSON en C# – Tutoriel complet
tags:
- C#
- Excel automation
- JSON
- Aspose.Cells
title: Générer un Excel à partir de JSON en C# – Guide étape par étape
url: /fr/net/excel-data-import-export/generate-excel-from-json-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Générer Excel à partir de JSON en C# – Guide étape par étape

Vous avez déjà eu besoin de **générer Excel à partir de JSON** mais vous n'étiez pas sûr de la bibliothèque capable de faire le gros du travail ? Vous n'êtes pas le seul. Dans de nombreuses applications d'entreprise, nous recevons des charges utiles au format JSON et devons les transférer dans des feuilles de calcul bien formatées — pensez aux rapports de ventes, aux exportations d'inventaire ou aux journaux d'audit. La bonne nouvelle ? Avec le moteur SmartMarker d'Aspose.Cells, vous pouvez transformer une chaîne JSON en un fichier Excel complet en quelques lignes seulement.

Dans ce tutoriel, nous parcourrons l'ensemble du processus : de la préparation de la charge JSON, à la configuration de SmartMarker pour **autoriser les noms de feuilles en double**, la création d'une **feuille de détail**, et enfin **l'enregistrement du classeur en C#**. À la fin, vous disposerez d'un extrait réutilisable que vous pourrez intégrer à n'importe quel projet .NET.

> **Récapitulatif rapide :**  
> • Objectif principal – générer Excel à partir de JSON.  
> • Objectifs secondaires – autoriser les noms de feuilles en double, créer une feuille de détail, enregistrer le classeur en C#.  

## Prérequis

- .NET 6.0 SDK (ou toute version récente de .NET).  
- Visual Studio 2022 ou VS Code avec l'extension C#.  
- Une licence active ou un essai gratuit de **Aspose.Cells for .NET** (le package NuGet est `Aspose.Cells`).  
- Un fichier modèle Excel (`template.xlsx`) contenant déjà des balises SmartMarker comme `&=Name` et un espace réservé pour le tableau de détail.

Si l'un de ces éléments vous est inconnu, ne paniquez pas — l'installation du package NuGet se fait en une seule commande, et le modèle peut être un classeur simple avec quelques cellules de substitution.

## Vue d'ensemble de la solution

À un niveau élevé, nous allons :

1. Définir une chaîne JSON qui reflète les données que nous voulons dans la feuille.  
2. Configurer `SmartMarkerOptions` afin que les noms de feuilles en double soient autorisés et qu'une **feuille de détail** obtienne un nom prévisible.  
3. Charger le modèle Excel contenant les balises SmartMarker.  
4. Exécuter le processeur SmartMarker pour fusionner les données JSON dans le classeur.  
5. Enregistrer le fichier final avec `workbook.Save(...)`.

Chaque étape est expliquée ci-dessous, avec des extraits de code complets et l'importance de chaque étape.

---

## Étape 1 – Préparer la charge JSON à fusionner

La première chose dont vous avez besoin est un document JSON qui correspond aux balises SmartMarker de votre modèle. Considérez le JSON comme la source de vérité ; chaque clé devient un espace réservé dans le fichier Excel.

```csharp
// Step 1: Define the JSON data that will be merged into the worksheet
string jsonData = @"{
    ""Name"": ""John"",
    ""Date"": ""2023-01-01"",
    ""Orders"": [
        { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
        { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
    ]
}";
```

**Pourquoi c'est important :**  
SmartMarker lit la hiérarchie JSON et développe automatiquement les tableaux pour les collections comme `Orders`. Si la structure de votre JSON ne correspond pas aux balises, la fusion produira silencieusement des lignes vides — un piège courant.

---

## Étape 2 – Configurer SmartMarker pour autoriser les noms de feuilles en double et nommer la feuille de détail

Par défaut, Aspose.Cells interdit les noms de feuilles en double, ce qui peut être un obstacle lorsque vous générez une feuille de détail pour chaque enregistrement principal. La classe `SmartMarkerOptions` vous permet de relâcher cette règle et également de spécifier un modèle de nommage pour les nouvelles feuilles de détail créées.

```csharp
// Step 2: Create SmartMarker options and allow duplicate base names for detail sheets
var smartMarkerOptions = new Aspose.Cells.SmartMarker.SmartMarkerOptions
{
    // When a detail sheet is generated, it will be named "Detail", "Detail (2)", etc.
    DetailSheetNewName = "Detail",

    // This flag tells the engine that duplicate sheet names are acceptable.
    // Useful when you generate multiple detail sheets from a loop.
    AllowDuplicateSheetNames = true
};
```

**Pourquoi c'est important :**  
Si vous parcourez plusieurs clients et que chaque itération crée une nouvelle feuille, le moteur lancerait normalement une exception. Définir `AllowDuplicateSheetNames` à `true` indique à Aspose.Cells d'ajouter automatiquement un suffixe numérique, assurant ainsi la fluidité du processus.

---

## Étape 3 – Charger le modèle Excel contenant les balises SmartMarker

Votre modèle est la toile sur laquelle SmartMarker peindra les données. Il peut contenir n'importe quel formatage — couleurs, formules, graphiques — de sorte que vous n'ayez pas à recréer cette logique par programmation.

```csharp
// Step 3: Load the workbook that contains SmartMarker tags
using var workbook = new Aspose.Cells.Workbook(@"C:\MyProjects\ExcelDemo\template.xlsx");
```

**Astuce :**  
Conservez le modèle dans un dossier faisant partie de la sortie de votre projet (par ex., `Content\Templates`). Ainsi, vous pouvez le référencer avec un chemin relatif et éviter de coder en dur des répertoires absolus.

---

## Étape 4 – Exécuter le processeur SmartMarker avec le JSON et les options

Maintenant, la magie opère. Le `SmartMarkerProcessor` lit le JSON, respecte les options que vous avez définies et remplit le classeur en conséquence.

```csharp
// Step 4: Process the SmartMarker tags using the JSON data and the configured options
workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);
```

**Que se passe-t-il en coulisses ?**  
- Le processeur parcourt chaque cellule à la recherche de marqueurs comme `&=Name` ou `&=Orders.Item`.  
- Il remplace les marqueurs simples par des valeurs scalaires (`Name`, `Date`).  
- Pour les collections (`Orders`), il crée une nouvelle feuille de détail (nommée « Detail ») et remplit une ligne de tableau pour chaque élément.  
- Comme nous avons autorisé les noms de feuilles en double, si le modèle possède déjà une feuille nommée « Detail », le moteur créera « Detail (2) ».

---

## Étape 5 – Enregistrer le classeur fusionné sur le disque

Enfin, écrivez le classeur rempli dans un fichier. Vous pouvez choisir n'importe quel format pris en charge par Aspose.Cells — XLSX, CSV, PDF, etc. Ici, nous resterons sur le format moderne XLSX.

```csharp
// Step 5: Save the workbook with the merged data
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

**Pourquoi c'est important :**  
L'enregistrement est l'étape où vous **enregistrez réellement le classeur en C#**. Si vous devez diffuser le fichier vers un client web, vous pouvez utiliser `workbook.Save(Stream, SaveFormat.Xlsx)` à la place.

---

## Exemple complet fonctionnel

En rassemblant tous les éléments, voici une application console complète, prête à être exécutée. Assurez-vous d'avoir installé le package NuGet `Aspose.Cells` (`dotnet add package Aspose.Cells`) avant de compiler.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace ExcelFromJsonDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Define the JSON payload
            string jsonData = @"{
                ""Name"": ""John"",
                ""Date"": ""2023-01-01"",
                ""Orders"": [
                    { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
                    { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
                ]
            }";

            // 2️⃣ Configure SmartMarker options – allow duplicate sheet names & set detail sheet name
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail",
                AllowDuplicateSheetNames = true
            };

            // 3️⃣ Load the template workbook (ensure the path is correct)
            var workbookPath = @"C:\MyProjects\ExcelDemo\template.xlsx";
            using var workbook = new Workbook(workbookPath);

            // 4️⃣ Merge JSON data into the workbook
            workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);

            // 5️⃣ Save the result
            var outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Excel file generated successfully at: {outputPath}");
        }
    }
}
```

### Résultat attendu

- **Feuille 1** (la feuille principale) affichera « John » dans la cellule `Name` et « 2023‑01‑01 » dans la cellule `Date`.  
- Une nouvelle feuille **Detail** apparaîtra, contenant un tableau avec deux lignes : une pour la commande Laptop et une pour la commande Mouse.  
- Si le modèle possède déjà une feuille nommée « Detail », la nouvelle feuille sera nommée « Detail (2) », grâce au drapeau `AllowDuplicateSheetNames`.

![Sortie Excel montrant la feuille principale avec le nom et la date, plus une feuille Detail avec les lignes de commande](excel-output.png "générer excel à partir de json résultat")

*Texte alternatif de l'image :* **générer excel à partir de json – classeur d'exemple avec feuilles principale et détail**

---

## Questions fréquentes & cas limites

### Que faire si mon JSON contient des collections imbriquées ?

SmartMarker peut gérer les tableaux imbriqués, mais vous devrez ajouter des feuilles de détail supplémentaires ou utiliser des marqueurs hiérarchiques. Par exemple, `&=Orders.SubItems.Product` générerait automatiquement une feuille de troisième niveau.

### Comment personnaliser le modèle de nommage pour les feuilles en double ?

Au lieu d'un `DetailSheetNewName` statique, vous pouvez assigner un rappel via `smartMarkerOptions.DetailSheetNameGenerator`. Cela vous permet d'intégrer des horodatages ou des identifiants uniques dans le nom de la feuille.

```csharp
smartMarkerOptions.DetailSheetNameGenerator = (baseName, index) =>
    $"{baseName}_{DateTime.Now:yyyyMMdd}_{index}";
```

### Puis-je générer du CSV au lieu de XLSX ?

Absolument. Remplacez l'appel final à `Save` par :

```csharp
workbook.Save(outputPath, SaveFormat.Csv);
```

Le reste du pipeline reste identique.

### Cela fonctionne-t-il dans ASP.NET Core ?

Oui. Le même code peut s'exécuter à l'intérieur d'une action de contrôleur. Il suffit de diffuser le classeur dans la réponse :

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0;
return File(ms, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "report.xlsx");
```

---

## Astuces pro & pièges

- **Astuce pro :** Conservez vos balises SmartMarker dans une feuille « Template » séparée. Ainsi, vous pouvez protéger la feuille contre les modifications accidentelles tout en permettant au processeur de la lire.  
- **Attention à :** Les clés JSON contenant des espaces ou des caractères spéciaux. Aspose.Cells attend des identifiants JavaScript valides ; renommez‑les ou utilisez l'attribut `JsonProperty` si vous désérialisez depuis un POCO.  
- **Astuce de performance :** Si vous traitez des milliers de lignes, définissez `smartMarkerOptions.EnableCache = true` pour réutiliser les marqueurs compilés.  
- **Vérification de version :** Le code ci‑dessus cible Aspose.Cells 23.9+. Les versions antérieures peuvent ne pas prendre en charge `AllowDuplicateSheetNames`.

---

## Conclusion

Vous disposez maintenant d'une recette complète, de bout en bout, pour **générer Excel à partir de JSON** en C#. En configurant `SmartMarkerOptions`, nous avons montré comment **autoriser les noms de feuilles en double**, contrôler le nommage de la **feuille de détail**, et enfin **enregistrer le classeur en C#**. L'approche est entièrement autonome — aucune dépendance externe, seulement un seul package NuGet.

Prochaines étapes ? Essayez de remplacer la source JSON par une API réelle

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}