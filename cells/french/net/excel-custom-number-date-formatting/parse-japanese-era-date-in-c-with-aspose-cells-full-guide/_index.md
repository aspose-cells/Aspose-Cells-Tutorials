---
category: general
date: 2026-06-08
description: Analyser une date d’ère japonaise en C# avec Aspose.Cells. Découvrez
  comment CultureInfo ja-JP et le format d’ère japonaise permettent une conversion
  précise des dates Excel.
draft: false
keywords:
- parse japanese era date
- Aspose.Cells
- CultureInfo ja-JP
- Japanese era format
- Excel date conversion
- C# DateTime parsing
language: fr
og_description: Analysez rapidement les dates d'ère japonaise en C#. Ce tutoriel montre
  comment CultureInfo ja-JP et Aspose.Cells transforment les chaînes d'ère en objets
  DateTime appropriés.
og_title: Analyser la date de l’ère japonaise en C# – Guide Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  headline: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  type: TechArticle
- description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  name: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  steps:
  - name: 5.1 Invalid or Empty Strings
    text: '```csharp string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString();
      // could be empty if (string.IsNullOrWhiteSpace(maybeDate)) { Console.WriteLine("Cell
      B1 is empty – skipping."); } else { // Attempt to parse; catch format exceptions
      try { DateTime dt = DateTime.Parse(maybeDate, new Cultur'
  - name: 5.2 Older Eras (Showa, Taisho)
    text: 'The same `CultureInfo ja-JP` works for older eras automatically:'
  - name: 5.3 Using `DateTime.ParseExact` for Strict Validation
    text: 'If you want to enforce the exact Japanese era pattern, use a custom format
      string:'
  type: HowTo
- questions:
  - answer: Yes. As long as the workbook’s `Settings.CultureInfo` is set to `ja-JP`
      *before* you call `GetDateTime()`, Aspose.Cells will interpret the existing
      strings correctly.
    question: Does this work with .xlsx files that already contain era dates?
  - answer: The parsing returns a `DateTime` with `Kind = Unspecified`. If you need
      UTC or local time, apply `DateTime.SpecifyKind` or convert after parsing.
    question: What about time zones?
  - answer: Absolutely. Loop through the desired range and call `GetDateTime()` on
      each cell—just remember to handle exceptions for malformed entries.
    question: Can I parse multiple cells at once?
  type: FAQPage
tags:
- C#
- Excel
- DateTime
- Localization
title: Analyser les dates d’ère japonaise en C# avec Aspose.Cells – Guide complet
url: /fr/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analyser les dates d’ère japonaise en C# avec Aspose.Cells – Guide complet

Vous avez déjà eu besoin d’**analyser des dates d’ère japonaise** directement depuis une feuille Excel ? Peut‑être que vous extrayez des données d’un système hérité qui utilise encore « 令和3年5月12日 » et que vous voulez un `DateTime` propre pour vos rapports. Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l’emploi, qui transforme ces chaînes au format d’ère en dates C# correctes—sans deviner.

Nous utiliserons **Aspose.Cells**, la puissante bibliothèque .NET pour la manipulation d’Excel, conjointement avec le paramètre **CultureInfo ja-JP** qui sait lire les ères japonaises. À la fin, vous disposerez d’un extrait réutilisable qui gère « 令和 », « 平成 » et même les ères plus anciennes sans le moindre effort.

## Prérequis

- .NET 6.0 ou supérieur (le code fonctionne également sur .NET Framework 4.6+)
- Aspose.Cells pour .NET (vous pouvez obtenir le package NuGet d’essai gratuit : `Install-Package Aspose.Cells`)
- Connaissances de base en C#—rien de sophistiqué, une simple application console suffit
- Un IDE de votre choix (Visual Studio, Rider, VS Code, etc.)

C’est tout. Aucun service supplémentaire, aucun parseur tiers obscur.

## Étape 1 : Configurer le projet et ajouter Aspose.Cells

Tout d’abord, créez un nouveau projet console :

```bash
dotnet new console -n JapaneseEraParser
cd JapaneseEraParser
dotnet add package Aspose.Cells
```

Ouvrez maintenant **Program.cs** et ajoutez les espaces de noms requis :

```csharp
using System;
using System.Globalization;
using Aspose.Cells;
```

> **Astuce :** Si vous utilisez Visual Studio, l’IDE proposera d’ajouter automatiquement les instructions `using` après que vous ayez tapé les noms de classe.

## Étape 2 : Créer un classeur et appliquer la culture japonaise

Le secret pour **analyser des dates d’ère japonaise** correctement est d’indiquer à Aspose.Cells quelle culture utiliser. Le réglage de `CultureInfo` à `ja-JP` active l’analyse sensible aux ères.

```csharp
// Step 2: Initialize a new workbook and set Japanese culture
Workbook workbook = new Workbook();
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

Pourquoi est‑ce important ? Le calendrier japonais comporte plusieurs ères (par ex., *Reiwa* (令和), *Heisei* (平成)). L’objet `CultureInfo` contient un `JapaneseCalendar` qui connaît les dates de début de chaque ère, de sorte que toute chaîne suivant le format d’ère japonaise peut être interprétée correctement.

## Étape 3 : Écrire une chaîne de date d’ère japonaise dans une cellule

Insérons un exemple de date d’ère dans la cellule **A1**. N’hésitez pas à modifier la chaîne pour tester d’autres ères.

```csharp
// Step 3: Put a Japanese era date string into A1
string japaneseDate = "令和3年5月12日"; // Reiwa 3, May 12, 2021
workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);
```

Si vous préférez travailler avec un classeur existant, vous pouvez le charger avec `new Workbook("path/to/file.xlsx")` et ignorer l’étape de création.

## Étape 4 : Récupérer la valeur sous forme d’objet C# DateTime

Maintenant, la magie opère. En appelant `GetDateTime()`, Aspose.Cells lit la cellule en utilisant le `CultureInfo` défini précédemment et renvoie un `DateTime` correct.

```csharp
// Step 4: Parse the cell value into a DateTime
DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

**Sortie attendue**

```
Parsed DateTime: 2021-05-12
```

Voilà le flux complet d’**analyse de dates d’ère japonaise**—quatre lignes de code concises.

## Étape 5 : Gestion des cas limites et des ères alternatives

Les données du monde réel ne sont pas toujours propres. Voici quelques scénarios que vous pourriez rencontrer et comment les gérer.

### 5.1 Chaînes invalides ou vides

```csharp
string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString(); // could be empty
if (string.IsNullOrWhiteSpace(maybeDate))
{
    Console.WriteLine("Cell B1 is empty – skipping.");
}
else
{
    // Attempt to parse; catch format exceptions
    try
    {
        DateTime dt = DateTime.Parse(maybeDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"B1 parsed as {dt:yyyy-MM-dd}");
    }
    catch (FormatException)
    {
        Console.WriteLine($"Unable to parse '{maybeDate}' as a Japanese era date.");
    }
}
```

### 5.2 Ères plus anciennes (Showa, Taisho)

Le même `CultureInfo ja-JP` fonctionne automatiquement pour les ères plus anciennes :

```csharp
string showaDate = "昭和45年12月31日"; // Showa 45 = 1970-12-31
DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
Console.WriteLine(showaParsed.ToString("yyyy-MM-dd")); // 1970-12-31
```

### 5.3 Utilisation de `DateTime.ParseExact` pour une validation stricte

Si vous souhaitez imposer le motif exact de l’ère japonaise, utilisez une chaîne de format personnalisée :

```csharp
string pattern = "ggggy年M月d日"; // gggg = era name, y = year in era
DateTime strictDate = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
Console.WriteLine(strictDate); // 2021-05-12 00:00:00
```

Cette approche lève une `FormatException` lorsque la chaîne diffère, ce qui peut être utile pour les contrôles de qualité des données.

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier‑coller dans **Program.cs** et exécuter.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and set Japanese culture
        Workbook workbook = new Workbook();
        workbook.Settings.CultureInfo = new CultureInfo("ja-JP");

        // 2️⃣ Insert a Japanese era date string
        string japaneseDate = "令和3年5月12日";
        workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);

        // 3️⃣ Parse the cell value into DateTime
        DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");

        // 4️⃣ Demonstrate handling an older era
        string showaDate = "昭和45年12月31日";
        DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"Showa parsed: {showaParsed:yyyy-MM-dd}");

        // 5️⃣ Strict parsing with ParseExact
        string pattern = "gggy年M月d日";
        try
        {
            DateTime strict = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
            Console.WriteLine($"Strict parse: {strict:yyyy-MM-dd}");
        }
        catch (FormatException ex)
        {
            Console.WriteLine($"Strict parse failed: {ex.Message}");
        }
    }
}
```

Exécutez‑le avec `dotnet run` et vous devriez voir :

```
Parsed DateTime: 2021-05-12
Showa parsed: 1970-12-31
Strict parse: 2021-05-12
```

Boom—**analyse de dates d’ère japonaise** terminée, et vous avez maintenant un modèle pour toute ère que vous pourriez rencontrer.

![Flux de travail d’analyse de dates d’ère japonaise – montre la création du classeur, le réglage de la culture, l’écriture dans la cellule et l’appel GetDateTime](parse-japanese-era-date.png "Diagramme illustrant comment analyser une date d’ère japonaise avec Aspose.Cells et CultureInfo ja-JP")

## Questions fréquentes

- **Cela fonctionne‑t‑il avec des fichiers .xlsx contenant déjà des dates d’ère ?**  
  Oui. Tant que le `Settings.CultureInfo` du classeur est défini sur `ja-JP` *avant* d’appeler `GetDateTime()`, Aspose.Cells interprétera correctement les chaînes existantes.

- **Qu’en est‑il des fuseaux horaires ?**  
  L’analyse renvoie un `DateTime` avec `Kind = Unspecified`. Si vous avez besoin d’un UTC ou d’une heure locale, appliquez `DateTime.SpecifyKind` ou convertissez après l’analyse.

- **Puis‑je analyser plusieurs cellules en même temps ?**  
  Absolument. Parcourez la plage souhaitée et appelez `GetDateTime()` sur chaque cellule—n’oubliez pas de gérer les exceptions pour les entrées mal formées.

## Conclusion

Nous avons couvert tout ce qu’il faut pour **analyser des dates d’ère japonaise** en C# avec Aspose.Cells et le `CultureInfo ja-JP` intégré. De la configuration du classeur, l’écriture de chaînes au format d’ère, la récupération d’un `DateTime` propre, à la gestion des cas limites comme les ères anciennes et la validation stricte—ce guide vous fournit une solution prête pour la production.

Ensuite, vous pourriez explorer la **conversion de dates Excel** pour les dates numériques sérielles, ou plonger dans le **parsing DateTime en C#** avec des calendriers personnalisés pour d’autres locales. Le même schéma fonctionne pour le calendrier bouddhiste thaï, le calendrier hébraïque, etc.—il suffit de changer le `CultureInfo`.

Vous avez un cas particulier qui vous pose problème ? Laissez un commentaire, et résolvons-le ensemble. Bon codage !

## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Change Excel Date System to 1904 using Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}