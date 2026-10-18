---
category: general
date: 2026-06-27
description: Apprenez à analyser les dates d’ère japonaise en C# puis à formater la
  date/heure au format yyyy‑mm‑dd pour une sortie ISO. Code pas à pas, cas limites
  et astuces.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: fr
og_description: Analysez les dates d’ère japonaise en C# et formatez les datetime
  au format yyyy‑mm‑dd sans effort. Exemple complet avec explications et pièges.
og_title: Analyser une date d’ère japonaise en C# – Guide complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  headline: Parse Japanese era date in C# – Complete Guide
  type: TechArticle
- description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  name: Parse Japanese era date in C# – Complete Guide
  steps:
  - name: Multiple Eras
    text: Japan has gone through several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa).
      The `JapaneseCalendar` automatically maps them, so `"H30-12-31"` (Heisei 30)
      becomes `2018-12-31`. Just keep the same parsing logic; the calendar does the
      heavy lifting.
  - name: Invalid Input
    text: 'If a string doesn’t match the expected pattern, `Parse` throws. Use `TryParseExact`
      as shown earlier, or pre‑validate with a regular expression:'
  - name: Time Zones
    text: '`DateTime` objects are “kind‑agnostic” by default. If you need a UTC timestamp,
      call:'
  type: HowTo
tags:
- C#
- .NET
- DateTime
- Localization
title: Analyser une date d’ère japonaise en C# – Guide complet
url: /fr/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analyser les dates d'ère japonaise en C# – Guide complet

Vous avez déjà eu besoin d'**analyser une date d'ère japonaise** dans une application .NET et vous vous êtes demandé pourquoi le résultat semblait incorrect ? Vous n'êtes pas seul. Dans de nombreux systèmes hérités, les dates sont présentées sous le format « R3‑04‑01 », et vous devez les convertir en une chaîne **format datetime yyyy-mm-dd** propre pour les API ou les bases de données.  

Dans ce tutoriel, nous parcourrons les étapes exactes pour y parvenir, expliquerons pourquoi chaque élément est important, et vous montrerons comment gérer les cas limites délicats qui posent souvent problème aux développeurs.

> **Note :** Tout le code est prêt à être copié‑collé dans une application console ciblant .NET 6 ou une version ultérieure.

## Ce dont vous avez besoin

- .NET 6 SDK (ou toute version récente)
- Familiarité de base avec C# et l'espace de noms `System.Globalization`
- Un IDE ou éditeur – Visual Studio, VS Code, Rider, ce que vous préférez

Aucun package NuGet externe requis ; tout se trouve dans le BCL.

## Étape 1 : Configurer la culture japonaise avec le calendrier impérial

Tout d'abord, nous avons besoin d'un `CultureInfo` qui connaît le calendrier impérial japonais. Par défaut, `ja-JP` utilise le calendrier grégorien, nous remplaçons donc son `DateTimeFormat.Calendar` par une instance de `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a Japanese culture and switch to the Japanese imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // (The rest of the code follows...)
```

> **Pourquoi c'est important :** Le `JapaneseCalendar` traduit les symboles d'ère (comme « R » pour Reiwa) en l'année grégorienne correcte. Sans cela, `DateTime.Parse` lancerait une `FormatException`.

## Étape 2 : Analyser la chaîne de date basée sur l'ère

Nous pouvons maintenant fournir une chaîne telle que "R3-04-01" à `DateTime.Parse`. La culture que nous venons de configurer indique à l'analyseur comment interpréter la partie « R3 ».

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Si vous préférez une approche plus sûre qui évite les exceptions en cas de mauvaise entrée, remplacez `Parse` par `TryParseExact` :

```csharp
        // Safer alternative with TryParseExact
        if (DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",               // ggy = era+year, MM = month, dd = day
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime safeDate))
        {
            parsedDate = safeDate;
        }
        else
        {
            Console.WriteLine("Unable to parse the Japanese era date.");
            return;
        }
```

> **Astuce :** La chaîne de format personnalisée "ggy-MM-dd" indique à l'analyseur exactement ce à quoi s'attendre. « gg » est le désignateur d'ère, « y » l'année au sein de cette ère.

## Étape 3 : Convertir le résultat en ISO 8601 (`format datetime yyyy-mm-dd`)

Enfin, nous affichons le `DateTime` dans un format ISO standard. Le spécificateur de format "yyyy-MM-dd" fait exactement cela.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

L'exécution du programme affiche :

```
2021-04-01
```

C'est le **format datetime yyyy-mm-dd** que vous recherchiez, prêt pour les charges JSON, les insertions SQL ou tout système en aval.

![parse japanese era date example](placeholder.png){alt="exemple d'analyse de date d'ère japonaise"}

## Gestion des autres ères et des cas limites

### Plusieurs ères

Le Japon a traversé plusieurs ères (Meiji, Taishō, Shōwa, Heisei, Reiwa). Le `JapaneseCalendar` les mappe automatiquement, ainsi `"H30-12-31"` (Heisei 30) devient `2018-12-31`. Conservez simplement la même logique d'analyse ; le calendrier effectue le travail lourd.

### Entrée invalide

Si une chaîne ne correspond pas au modèle attendu, `Parse` lève une exception. Utilisez `TryParseExact` comme montré précédemment, ou pré‑validez avec une expression régulière :

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Fuseaux horaires

Les objets `DateTime` sont « kind‑agnostic » par défaut. Si vous avez besoin d'un horodatage UTC, appelez :

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

Ou utilisez `DateTimeOffset` pour une prise en compte complète du fuseau.

## Exemple complet fonctionnel

Voici le fragment complet que vous pouvez insérer dans un nouveau projet console :

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Initialize Japanese culture with the imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // The era‑based date you want to convert
        string eraDate = "R3-04-01";

        // Try parsing – safer than Parse when input may be malformed
        if (!DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime parsedDate))
        {
            Console.WriteLine("Failed to parse the Japanese era date.");
            return;
        }

        // Convert to ISO 8601 (format datetime yyyy-mm-dd)
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine($"Original era date: {eraDate}");
        Console.WriteLine($"Converted ISO date: {isoDate}");
    }
}
```

**Sortie console attendue**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Récapitulatif

Nous avons vu comment **analyser des dates d'ère japonaise** en suivant :

1. Créer un `CultureInfo` pour `ja-JP` et remplacer le calendrier par `JapaneseCalendar`.
2. Utiliser `DateTime.Parse` ou le plus robuste `TryParseExact` avec un format personnalisé.
3. Formater le `DateTime` résultant avec `"yyyy-MM-dd"` pour obtenir le **format datetime yyyy-mm-dd** souhaité.

C’est tout ce dont vous avez besoin pour faire le pont entre les données d'ère japonaise héritées et les systèmes modernes conformes à ISO.

## Et après ?

- **Traitement par lots :** Parcourir un CSV de dates d'ère et écrire les chaînes ISO dans une base de données.
- **Localisation :** Convertir les dates ISO en format d'ère pour l'affichage UI (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Calendriers personnalisés :** Explorer `TaiwanCalendar` ou `HijriCalendar` pour d'autres besoins régionaux.

N'hésitez pas à expérimenter — changez la chaîne d'ère, testez les cas limites, ou intégrez cette logique dans des points de terminaison ASP.NET Core. Si vous rencontrez un problème, laissez un commentaire ci‑dessous ; bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment implémenter la validation de dates en .NET avec Aspose.Cells : Guide complet](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Modifier le système de dates Excel en 1904 avec Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Comment implémenter et formater les commentaires Excel avec Aspose.Cells pour .NET : Guide étape par étape](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}