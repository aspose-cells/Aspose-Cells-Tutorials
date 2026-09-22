---
category: general
date: 2026-03-22
description: Créer un classeur Excel, ajouter des propriétés personnalisées, définir
  le nom de la feuille de calcul et enregistrer en tant que fichier binaire XLSB en
  utilisant C#.
draft: false
keywords:
- create excel workbook
- add custom properties
- save as xlsb
- set worksheet name
- write binary excel file
language: fr
og_description: Créer un classeur Excel, ajouter des propriétés personnalisées, définir
  le nom de la feuille et enregistrer en tant que fichier binaire XLSB avec C#.
og_title: Créer un classeur Excel – Ajouter des propriétés personnalisées et enregistrer
  au format XLSB
tags:
- C#
- Aspose.Cells
- Excel automation
title: Créer un classeur Excel – Ajouter des propriétés personnalisées et enregistrer
  au format XLSB
url: /fr/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel – Ajouter des propriétés personnalisées et enregistrer au format XLSB

Vous avez déjà eu besoin de **create Excel workbook** de façon programmatique tout en conservant des métadonnées associées ? Peut‑être construisez‑vous un moteur de reporting qui associe à chaque fichier un ID de rapport, le nom de l’auteur ou le numéro de version. Dans ce cas, apprendre à **add custom properties** tout en **set worksheet name** et enfin **save as XLSB** vous évitera beaucoup de post‑traitement manuel.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui montre exactement comment **write binary Excel file** avec C#. Vous verrez pourquoi le format XLSB est le bon choix pour transporter des propriétés personnalisées, comment éviter les pièges les plus courants, et quoi faire si vous devez prendre en charge d’anciennes versions d’Excel.

---

## Ce dont vous avez besoin

- **.NET 6+** (ou .NET Framework 4.6+). Le code fonctionne sur n’importe quel runtime récent.
- **Aspose.Cells for .NET** (version d’essai gratuite ou sous licence). Il fournit les classes `Workbook`, `Worksheet` et `CustomProperties` utilisées ci‑dessous.
- Un IDE avec lequel vous êtes à l’aise – Visual Studio, Rider, ou même VS Code conviendra.
- Un accès en écriture à un dossier où le fichier généré sera enregistré.

Aucune autre bibliothèque tierce n’est requise.

---

## Étape 1 : Installer Aspose.Cells

Pour commencer, ajoutez le package NuGet Aspose.Cells à votre projet :

```bash
dotnet add package Aspose.Cells
```

> **Astuce :** Si vous êtes sur un serveur CI, stockez la clé de licence dans une variable d’environnement et chargez‑la à l’exécution – cela empêche le filigrane « evaluation » de s’infiltrer dans votre sortie.

---

## Étape 2 : Créer un classeur Excel – Vue d’ensemble

La première vraie action consiste à **create Excel workbook**. Cet objet représente le fichier complet en mémoire et vous donne accès aux feuilles de calcul, aux styles et aux propriétés personnalisées.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2.1: Instantiate a new workbook (empty by default)
            Workbook workbook = new Workbook();

            // The rest of the steps follow...
```

Pourquoi instancier un nouveau `Workbook` au lieu de charger un modèle ? Un classeur vierge garantit l’absence de styles cachés ou de propriétés personnalisées résiduelles, ce qui est particulièrement important lorsque vous avez l’intention de **write binary excel file** pour des systèmes en aval qui attendent une ardoise propre.

---

## Étape 3 : Définir le nom de la feuille de calcul (et pourquoi c’est important)

Les feuilles Excel portent par défaut les noms « Sheet1 », « Sheet2 », etc. Donner à une feuille un nom significatif facilite grandement la lecture du traitement en aval—comme Power Query ou les macros VBA.

```csharp
            // Step 3.1: Grab the first worksheet (index 0) and rename it
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data"; // clear, concise, and self‑describing
```

Si vous essayez d’attribuer un nom dupliqué, Aspose.Cells lèvera une `ArgumentException`. Pour être prudent, vous pouvez vérifier `Worksheets.Exists("Data")` avant de renommer.

---

## Étape 4 : Ajouter des propriétés personnalisées

Les propriétés personnalisées sont stockées dans le XML interne du classeur et voyagent avec le fichier quel que soit le format. Elles sont idéales pour intégrer des éléments comme `ReportId` ou `GeneratedBy`.

```csharp
            // Step 4.1: Add a numeric property
            workbook.CustomProperties.Add("ReportId", 12345);

            // Step 4.2: Add a string property
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");
```

> **Pourquoi utiliser les propriétés personnalisées ?**  
> • Elles sont accessibles via le panneau « File → Info → Properties » d’Excel.  
> • Le code qui consomme le classeur peut les lire sans analyser le contenu des cellules.  
> • Elles survivent aux conversions de format (XLSX ↔ XLSB) car elles font partie des métadonnées du fichier.

Vous pouvez également stocker des dates, des booléens ou même des blobs binaires, mais gardez la charge utile petite — Excel n’est pas une base de données.

---

## Étape 5 : Enregistrer au format XLSB (Write Binary Excel File)

Le format XLSB stocke les données dans une structure binaire, ce qui rend le fichier plus petit et plus rapide à ouvrir. Plus important pour ce tutoriel, **custom properties are baked into the binary stream**, garantissant qu’elles voyagent avec le fichier.

```csharp
            // Step 5.1: Define the output path
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // Step 5.2: Save the workbook as a binary XLSB file
            workbook.Save(outputPath, SaveFormat.Xlsb);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

### Résultat attendu

Après avoir exécuté le programme, vous trouverez `WithCustomProps.xlsb` sur votre bureau. Ouvrez‑le dans Excel, allez dans **File → Info → Properties**, et vous verrez `ReportId` et `GeneratedBy` listés sous *Custom*.

---

## Étape 6 : Cas limites et questions fréquentes

### Que faire si le dossier cible est en lecture‑seule ?

Enveloppez l’appel `Save` dans un bloc `try/catch` et revenez à un emplacement accessible en écriture par l’utilisateur, comme `%TEMP%`. Cela empêche l’application de planter en cas d’erreurs de permission.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsb);
}
catch (UnauthorizedAccessException)
{
    string fallback = Path.GetTempFileName().Replace(".tmp", ".xlsb");
    workbook.Save(fallback, SaveFormat.Xlsb);
    Console.WriteLine($"Saved to fallback location: {fallback}");
}
```

### Puis‑je **save as XLSX** et conserver les propriétés personnalisées ?

Oui—il suffit de remplacer `SaveFormat.Xlsb` par `SaveFormat.Xlsx`. Les propriétés sont stockées dans la même partie XML, elles survivent donc au changement de format. Cependant, les fichiers XLSX sont plus volumineux car ils sont du XML compressé, tandis que le XLSB offre de meilleures performances pour de grands ensembles de données.

### Comment lire les propriétés personnalisées plus tard ?

```csharp
Workbook loaded = new Workbook(outputPath);
foreach (CustomProperty prop in loaded.CustomProperties)
{
    Console.WriteLine($"{prop.Name} = {prop.Value}");
}
```

Cet extrait affiche chaque propriété personnalisée, ce qui rend trivial pour les services en aval de vérifier la provenance du fichier.

---

## Exemple complet fonctionnel

Ci‑dessous se trouve le programme complet que vous pouvez copier‑coller dans un nouveau projet console. Aucun morceau ne manque — tout, des instructions `using` jusqu’au dernier `Console.WriteLine`, est inclus.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook instance
            Workbook workbook = new Workbook();

            // 2️⃣ Access the first worksheet and give it a meaningful name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Add custom properties (they travel with the file)
            workbook.CustomProperties.Add("ReportId", 12345);
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");

            // 4️⃣ Define where to save the binary XLSB file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // 5️⃣ Save the workbook as a binary XLSB file
            try
            {
                workbook.Save(outputPath, SaveFormat.Xlsb);
                Console.WriteLine($"✅ Workbook saved to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ Failed to save workbook: {ex.Message}");
            }
        }
    }
}
```

Exécutez le programme, ouvrez le fichier résultant et vérifiez les propriétés personnalisées. C’est l’ensemble du processus de **create excel workbook**, **add custom properties**, **set worksheet name**, et **save as xlsb** en un flux bien ordonné.

---

## Conclusion

Vous savez maintenant exactement comment **create Excel workbook**, donner à sa feuille un **set worksheet name** clair, intégrer des métadonnées utiles avec **add custom properties**, et enfin **save as XLSB** pour produire un fichier Excel compact et binaire. Ce flux de travail est fiable, fonctionne sur toutes les versions de .NET, et s’adapte bien que vous génériez un rapport ou mille.

Et après ? Essayez d’ajouter un tableau de données à la feuille « Data », expérimentez différents types de propriétés (dates, booléens), ou changez la sortie en **save as xlsb** pour des ensembles de données massifs. Vous pouvez également explorer la protection du classeur par mot de passe—Aspose.Cells rend cela possible en une seule ligne.

N’hésitez pas à laisser un commentaire si vous rencontrez des problèmes, ou à partager comment vous avez étendu ce modèle dans vos propres projets. Bon codage !  

---  

![Create Excel workbook screenshot](image.png){alt="Créer un classeur Excel avec des propriétés personnalisées"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}