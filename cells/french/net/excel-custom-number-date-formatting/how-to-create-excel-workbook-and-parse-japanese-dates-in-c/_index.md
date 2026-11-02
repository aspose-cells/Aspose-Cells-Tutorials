---
category: general
date: 2026-10-10
description: Créer un classeur Excel en C# et définir la valeur d’une cellule avec
  une date d’ère japonaise, puis appliquer un format personnalisé et lire la cellule
  de date à l’aide d’Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell value
- apply custom format
- read date cell
- excel date parsing
language: fr
lastmod: 2026-10-10
og_description: Créer un classeur Excel en C# et analyser les dates d’ère japonaise.
  Apprenez à définir la valeur d’une cellule, appliquer un format personnalisé et
  lire une cellule de date avec Aspose.Cells.
og_image_alt: Screenshot showing a C# program that creates an Excel workbook and parses
  a Japanese era date
og_title: Créer un classeur Excel en C# – guide complet de l'analyse des dates
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and set cell value with a Japanese era
    date, then apply custom format and read date cell using Aspose.Cells.
  headline: How to create Excel workbook and parse Japanese dates in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Comment créer un classeur Excel et analyser les dates japonaises en C#
url: /fr/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un classeur Excel et analyser les dates japonaises en C#

Si vous devez **create Excel workbook** à partir de zéro, ce guide vous montre exactement comment faire. Vous apprendrez à **set cell value** avec une chaîne de date d'ère japonaise, **apply custom format** qui comprend l'ère, et enfin **read date cell** pour obtenir un .NET `DateTime`. L'exemple complet fonctionne avec la dernière version d'Aspose.Cells pour .NET, vous pouvez donc copier‑coller le code dans n'importe quel projet C#.

Travailler avec des dates incluant des ères japonaises peut être délicat car l'analyseur Excel par défaut ne reconnaît pas les symboles d'ère. En utilisant un format numérique personnalisé (`[ja-JP-Era]`) vous indiquez à Excel comment interpréter la chaîne, permettant une **excel date parsing** fiable. Les étapes ci‑dessous couvrent l'ensemble du flux de travail, de la création du classeur à l'extraction de la date.

## Prérequis

- .NET 6.0 ou ultérieur (le code fonctionne également sur .NET Framework 4.7+)
- Aspose.Cells pour .NET (package NuGet `Aspose.Cells`)
- Familiarité de base avec C# et Visual Studio ou tout IDE de votre choix

## Étape 1 : Créer un classeur Excel et ajouter une feuille de calcul

La première opération consiste à **create Excel workbook** en mémoire. Aspose.Cells crée automatiquement une feuille de calcul par défaut, mais vous pouvez en ajouter d'autres si nécessaire.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Optional: rename the default worksheet for clarity
        workbook.Worksheets[0].Name = "Dates";
```

La création du classeur alloue les structures internes qui contiendront ensuite les cellules, les styles et les formules. Aucun fichier n'est écrit à ce stade, ce qui rend l'opération rapide et testable.

## Étape 2 : Définir la valeur d'une cellule avec une chaîne de date d'ère japonaise

Ensuite, **set cell value** à la représentation d'ère japonaise `"R5-04-01"` (Reiwa 5, 1 avril). La chaîne suit le modèle `EraYear-MM-DD`.

```csharp
        // Step 2: Reference cell A1 on the first worksheet
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Put the Japanese era date string into the cell
        dateCell.PutValue("R5-04-01");
```

L'utilisation de `PutValue` stocke le texte brut. Excel le traitera comme une chaîne jusqu'à ce qu'un format numérique indique le contraire. Cette approche fonctionne pour toute représentation de calendrier personnalisé, pas seulement les ères japonaises.

## Étape 3 : Appliquer un format numérique personnalisé qui comprend l'ère japonaise

Maintenant **apply custom format** afin qu'Excel puisse traduire la chaîne d'ère en une vraie date sérielle. Le format `[ja-JP-Era]yyyy/MM/dd` indique au moteur d'interpréter le caractère d'ère initial (`R` pour Reiwa) et de calculer la date grégorienne.

```csharp
        // Step 3: Apply a custom number format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";
```

Le format personnalisé est stocké dans l'objet de style de la cellule. Aspose.Cells respecte ce format lors du rendu et de la conversion de valeur, permettant une **excel date parsing** fiable plus tard dans le pipeline.

## Étape 4 : Récupérer la valeur DateTime analysée depuis la cellule

Enfin, **read date cell** pour obtenir un `DateTime` .NET. La propriété `DateTimeValue` renvoie la valeur convertie en fonction du format personnalisé appliqué précédemment.

```csharp
        // Step 4: Retrieve the parsed DateTime value
        DateTime parsedDate = dateCell.DateTimeValue;

        // Output the result to the console for verification
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
```

Lorsque le programme s'exécute, la console affiche :

```
Parsed Gregorian date: 2023-04-01
```

La sortie confirme que la chaîne d'ère japonaise `"R5-04-01"` a été correctement interprétée comme le 1 avril 2023.

## Exemple complet et exécutable

Assembler les éléments donne un programme autonome que vous pouvez compiler et exécuter immédiatement.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Reference cell A1
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Insert Japanese era date string
        dateCell.PutValue("R5-04-01");

        // Apply custom format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";

        // Retrieve the parsed DateTime
        DateTime parsedDate = dateCell.DateTimeValue;

        // Show the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");

        // (Optional) Save the workbook to verify the visual format
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

L'exécution du programme crée `JapaneseEraDate.xlsx` avec la cellule A1 affichant `2023/04/01` tandis que la console montre la même date grégorienne. Le fichier peut être ouvert dans Excel pour voir la valeur formatée.

## Pourquoi cette approche fonctionne

- **create excel workbook** – L'instanciation de `Workbook` construit la structure complète du fichier Excel en mémoire sans toucher le disque.
- **set cell value** – `PutValue` stocke le texte brut, ce qui est nécessaire avant d'appliquer un format spécifique à la culture.
- **apply custom format** – Le jeton `[ja-JP-Era]` comble le fossé entre la notation d'ère et le système de dates sérielles interne d'Excel.
- **read date cell** – `DateTimeValue` utilise automatiquement le style de la cellule pour effectuer la conversion, vous fournissant un `DateTime` natif.
- **excel date parsing** – En déléguant l'analyse au style de la cellule, vous évitez la manipulation manuelle de chaînes, réduisant les bugs et améliorant la prise en charge des paramètres régionaux.

## Cas limites et conseils pratiques

- **Different eras** – Utilisez `S` pour Showa, `H` pour Heisei, `R` pour Reiwa. La même chaîne de format fonctionne pour toutes les ères.
- **Invalid strings** – Si la cellule contient une date d'ère malformée, `DateTimeValue` renvoie `DateTime.MinValue`. Vérifiez `dateCell.IsDate` avant de lire.
- **Multiple cells** – Appliquez le format personnalisé à toute une plage (`range.ApplyStyle(style)`) lorsque vous devez analyser de nombreuses dates.
- **Performance** – Définir le style une fois par colonne est plus rapide que par cellule pour de grandes feuilles.
- **Saving options** – Aspose.Cells peut exporter en XLSX, XLS, CSV ou PDF. Choisissez le format qui correspond au traitement en aval.

## Questions fréquemment posées

**Can I use the built‑in .NET culture instead of a custom format?**  
La classe .NET `CultureInfo` ne comprend pas les symboles d'ère japonais de la même façon qu'Excel. Utiliser un format numérique personnalisé est la méthode la plus fiable pour le **excel date parsing** des chaînes d'ère.

**What if I need to write the date back to Excel in era format?**  
Attribuez à la cellule une valeur `DateTime` et appliquez le même format personnalisé. Excel affichera automatiquement l'ère.

**Does this work on older versions of Excel?**  
Le jeton `[ja-JP-Era]` est pris en charge par Excel 2010 et versions ultérieures. Aspose.Cells émule ce comportement, de sorte que le classeur s'affiche correctement même lorsqu'il est ouvert dans des versions plus anciennes d'Excel qui ne disposent pas du support natif des ères.

## Conclusion

Vous savez maintenant comment **create Excel workbook**, **set cell value** avec une chaîne d'ère japonaise, **apply custom format**, et **read date cell** pour obtenir un `DateTime`. Ce modèle fournit un **excel date parsing** robuste sans manipulation manuelle de chaînes, rendant votre code d'automatisation C# à la fois concis et fiable.

Ensuite, explorez des sujets connexes tels que **formatting multiple date columns**, **working with other cultural calendars**, ou **exporting the workbook to PDF**. Chaque extension s'appuie sur les mêmes principes présentés ici, vous permettant d'adapter la solution à un large éventail de scénarios de localisation. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Create Excel Workbook in C# – Apply Custom Number Format](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/)
- [Create Excel Workbook with Custom Format – C# Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-custom-format-c-guide/)
- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}