---
category: general
date: 2026-03-29
description: Comment analyser les dates japonaises en C# avec DateTimeParser et CultureInfo.
  Apprenez le parsing des dates d’ère japonaise, les astuces de parsing de dates en
  C# et la gestion des cas limites.
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: fr
og_description: Comment analyser les dates japonaises en C# avec DateTimeParser et
  CultureInfo. Obtenez une solution étape par étape pour l’analyse des dates d’ère
  japonaise.
og_title: Comment analyser les dates japonaises en C# – Guide complet
tags:
- C#
- .NET
- DateTime
- Localization
title: Comment analyser les dates japonaises en C# – Guide complet
url: /fr/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment analyser les dates japonaises en C# – Guide complet

Vous vous êtes déjà demandé **comment analyser les dates japonaises** dans une application .NET ? Peut‑être travaillez‑vous sur un système financier qui reçoit des dates comme « 令和3年5月12日 » d’un client japonais, et vous devez les convertir en un `DateTime` standard. Vous n’êtes pas seul — les problèmes de localisation surgissent tout le temps.  

Bonne nouvelle : avec les bons paramètres de culture et une petite classe d’aide, **comment analyser les dates japonaises** devient un jeu d’enfant. Dans ce tutoriel, nous passerons en revue chaque étape, de la configuration de `CultureInfo` pour *ja‑JP* à la gestion des cas limites comme les ères historiques. À la fin, vous disposerez d’un `DateTimeParser` réutilisable qui fonctionne pour toute date moderne au format japonais.

> **Ce que vous obtiendrez** – un exemple complet et exécutable, des explications du *pourquoi* de chaque ligne, des astuces pour les ères plus anciennes, et une petite checklist pour ne jamais oublier une étape.

## Prérequis

- .NET 6+ (ou .NET Framework 4.7 + — l’API que nous utilisons n’a pas changé)
- Connaissances de base en C# (vous devez être à l’aise avec les instructions `using` et `Console.WriteLine`)
- Aucun package NuGet externe — tout se trouve dans `System` et `System.Globalization`

Si vous avez déjà un projet ouvert, super — déposez simplement le code. Sinon, créez une nouvelle application console avec `dotnet new console -n JapaneseDateDemo` et vous êtes prêt.

## Étape 1 : Comprendre le système de calendrier japonais

Avant de plonger dans le code, répondons au « pourquoi ». Les dates japonaises sont exprimées au format **ère** (元号), où le numéro d’année se réinitialise à l’avènement d’un nouvel empereur. Par exemple :

- **令和** (Reiwa) a commencé le 01‑05‑2019.  
- **平成** (Heisei) a couvert 1989‑2019.  
- **昭和** (Showa) s’est déroulé de 1926‑1989.

La classe .NET `JapaneseCalendar` connaît déjà ces ères, mais il faut indiquer au parseur quelle culture utiliser. C’est là qu’intervient **cultureinfo ja‑jp** — elle associe le calendrier à la locale japonaise.

## Étape 2 : Créer un petit wrapper – `DateTimeParser`

Au lieu d’éparpiller `CultureInfo` partout, nous allons encapsuler la logique dans une petite classe d’aide. Cela rend le code réutilisable et garde le reste de votre application propre.

```csharp
// File: DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        // Ensure the supplied culture uses the Japanese calendar.
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    /// <summary>
    /// Parses a Japanese era date string (e.g., "令和3年5月12日") into a Gregorian DateTime.
    /// </summary>
    /// <param name="japaneseDate">The era‑based date string.</param>
    /// <returns>A DateTime representing the same day in the Gregorian calendar.</returns>
    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        // The standard pattern for Japanese era dates.
        // "gggy年M月d日" -> era name (ggg), year (y), month (M), day (d)
        const string pattern = "gggy年M月d日";

        // TryParseExact respects the culture's calendar (JapaneseCalendar here).
        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        // If parsing fails, give a helpful exception.
        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }
}
```

**Pourquoi ce helper ?**  
- **Responsabilité unique** – tout le parsing dépendant de la locale vit en un seul endroit.  
- **Gestion des erreurs** – nous affichons des messages clairs lorsque le format est incorrect.  
- **Préparé pour le futur** – si vous devez plus tard prendre en charge les ères *Taisho* ou *Meiji*, il suffit d’ajuster le motif ou d’ajouter un fallback.

## Étape 3 : Brancher le tout dans `Program.cs`

Nous allons maintenant utiliser le wrapper pour analyser réellement une chaîne d’exemple. Notez comment nous récupérons la culture japonaise avec `CultureInfo.GetCultureInfo("ja-JP")`. Cela satisfait l’exigence **cultureinfo ja‑jp** et active le `JapaneseCalendar`.

```csharp
// File: Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 3‑1: Grab the Japanese culture (ja-JP) which uses JapaneseCalendar.
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");

        // Step 3‑2: Initialise our DateTimeParser with that culture.
        var parser = new DateTimeParser(japaneseCulture);

        // Step 3‑3: The era string we want to convert.
        string eraDate = "令和3年5月12日";

        try
        {
            // Step 3‑4: Parse it.
            DateTime gregorian = parser.Parse(eraDate);

            // Step 3‑5: Show the result – expected: 2021‑05‑12.
            Console.WriteLine($"Japanese: {eraDate} → Gregorian: {gregorian:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            // Friendly error output – useful in real‑world apps.
            Console.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

Lorsque vous lancez `dotnet run`, vous verrez :

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

C’est le cœur de **comment analyser les dates japonaises**. Simple, non ?

## Étape 4 : Gestion des cas limites & ères anciennes

### 4.1 Dates historiques avant 1912

Le `JapaneseCalendar` intégré ne prend en charge que les ères modernes (Meiji et suivantes). Si vous devez analyser des dates de la période *Taisho* (1912‑1926) ou *Meiji* (1868‑1912), le même motif fonctionne — il suffit que la chaîne contienne le nom d’ère correct (« 大正 », « 明治 »). Le parseur renverra toujours un `DateTime` grégorien correct.

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 Ère manquante (entrée ambiguë)

Si un client envoie « 2021年5月12日 » sans ère, le parseur échouera parce que le motif attend une ère (`ggg`). Vous avez deux options :

1. **Supposer le calendrier grégorien** – retomber sur `CultureInfo.InvariantCulture` avec un autre motif.  
2. **Rejeter l’entrée** – informer l’appelant que l’ère est requise.

Voici une adaptation rapide :

```csharp
public DateTime ParseFlexible(string input)
{
    // Try era‑based first.
    try { return Parse(input); } catch { /* ignore */ }

    // Fallback to plain Gregorian pattern.
    const string gregPattern = "yyyy年M月d日";
    if (DateTime.TryParseExact(
            input,
            gregPattern,
            _culture,
            DateTimeStyles.None,
            out DateTime gResult))
    {
        return gResult;
    }

    throw new FormatException("Unable to parse the provided date string.");
}
```

### 4.3 Note sur la sécurité des threads

Les objets `CultureInfo` sont en lecture‑seule après création, vous pouvez donc réutiliser la même instance entre plusieurs threads. Le `DateTimeParser` lui‑même ne possède aucun état mutable, ce qui le rend **thread‑safe** – un atout pour les API web à fort débit.

## Étape 5 : Tout assembler – Un exemple prêt à copier

Voici le code complet que vous pouvez coller dans un nouveau projet console. Aucun package externe, aucune dépendance cachée.

```csharp
// DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        const string pattern = "gggy年M月d日";

        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }

    // Optional flexible parser for non‑era inputs.
    public DateTime ParseFlexible(string input)
    {
        try { return Parse(input); } catch { /* fall through */ }

        const string gregPattern = "yyyy年M月d日";
        if (DateTime.TryParseExact(
                input,
                gregPattern,
                _culture,
                DateTimeStyles.None,
                out DateTime gResult))
        {
            return gResult;
        }

        throw new FormatException("Unable to parse the provided date string.");
    }
}
```

```csharp
// Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");
        var parser = new DateTimeParser(japaneseCulture);

        string[] samples = {
            "令和3年5月12日",   // 2021‑05‑12
            "平成31年4月30日", // 2019‑04‑30 (dernier jour de Heisei)
            "大正5年12月31日", // 1916‑12‑31 (historique)
            "2022年1月1日"      // ambiguë – pas d’ère
        };

        foreach (var s in samples)
        {
            try
            {
                DateTime dt = parser.ParseFlexible(s);
                Console.WriteLine($"{s} → {dt:yyyy-MM-dd}");

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}