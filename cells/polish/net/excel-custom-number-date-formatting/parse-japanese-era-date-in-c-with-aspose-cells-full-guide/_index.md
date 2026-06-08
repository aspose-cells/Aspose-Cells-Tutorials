---
category: general
date: 2026-06-08
description: Parsuj datę w japońskim erze w C# przy użyciu Aspose.Cells. Dowiedz się,
  jak CultureInfo ja‑JP i format japońskiej ery umożliwiają dokładną konwersję dat
  w Excelu.
draft: false
keywords:
- parse japanese era date
- Aspose.Cells
- CultureInfo ja-JP
- Japanese era format
- Excel date conversion
- C# DateTime parsing
language: pl
og_description: Szybko parsuj japońską datę ery w C#. Ten samouczek pokazuje, jak
  CultureInfo ja-JP i Aspose.Cells zamieniają ciągi z erą na prawidłowe obiekty DateTime.
og_title: Parsowanie japońskiej daty ery w C# – przewodnik Aspose.Cells
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
title: Parsowanie japońskiej daty ery w C# z Aspose.Cells – pełny przewodnik
url: /pl/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parsowanie daty japońskiej ery w C# przy użyciu Aspose.Cells – Pełny przewodnik

Kiedykolwiek potrzebowałeś **parse japanese era date** ciągów bezpośrednio z arkusza Excel? Być może pobierasz dane ze starszego systemu, który wciąż używa „令和3年5月12日” i chcesz czysty `DateTime` do generowania raportów. W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który zamienia te ciągi w stylu ery na prawidłowe daty C# — bez zgadywania.

Użyjemy **Aspose.Cells**, potężnej biblioteki .NET do manipulacji Excel, wraz z ustawieniem **CultureInfo ja-JP**, które potrafi odczytywać japońskie ery. Po zakończeniu będziesz mieć wielokrotnego użytku fragment kodu, który obsługuje „令和”, „平成” i nawet starsze ery bez problemu.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.6+)
- Aspose.Cells dla .NET (możesz pobrać darmowy pakiet próbny NuGet: `Install-Package Aspose.Cells`)
- Podstawowa znajomość C# — nic skomplikowanego, wystarczy aplikacja konsolowa
- IDE według własnego wyboru (Visual Studio, Rider, VS Code, itp.)

To wszystko. Bez dodatkowych usług, bez niejasnych parserów firm trzecich.

## Krok 1: Utwórz projekt i dodaj Aspose.Cells

Najpierw utwórz nowy projekt konsolowy:

```bash
dotnet new console -n JapaneseEraParser
cd JapaneseEraParser
dotnet add package Aspose.Cells
```

Teraz otwórz **Program.cs** i dodaj wymagane przestrzenie nazw:

```csharp
using System;
using System.Globalization;
using Aspose.Cells;
```

> **Wskazówka:** Jeśli używasz Visual Studio, IDE zasugeruje automatyczne dodanie instrukcji `using` po wpisaniu nazw klas.

## Krok 2: Utwórz skoroszyt i zastosuj japońską kulturę

Kluczem do poprawnego **parse japanese era date** jest poinformowanie Aspose.Cells, której kultury użyć. Ustawienie `CultureInfo` na `ja-JP` aktywuje parsowanie świadome ery.

```csharp
// Step 2: Initialize a new workbook and set Japanese culture
Workbook workbook = new Workbook();
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

Dlaczego to ważne? Japoński kalendarz ma wiele er (np. *Reiwa* (令和), *Heisei* (平成)). Obiekt `CultureInfo` zawiera `JapaneseCalendar`, który zna daty rozpoczęcia każdej ery, więc każdy ciąg w formacie japońskiej ery może być poprawnie zinterpretowany.

## Krok 3: Zapisz ciąg daty japońskiej ery w komórce

Wstawmy przykładową datę ery do komórki **A1**. Śmiało zmień ciąg, aby przetestować różne ery.

```csharp
// Step 3: Put a Japanese era date string into A1
string japaneseDate = "令和3年5月12日"; // Reiwa 3, May 12, 2021
workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);
```

Jeśli wolisz pracować z istniejącym skoroszytem, możesz go załadować przy użyciu `new Workbook("path/to/file.xlsx")` i pominąć krok tworzenia.

## Krok 4: Pobierz wartość jako obiekt C# DateTime

Teraz dzieje się magia. Wywołując `GetDateTime()`, Aspose.Cells odczytuje komórkę przy użyciu wcześniej ustawionego `CultureInfo` i zwraca prawidłowy `DateTime`.

```csharp
// Step 4: Parse the cell value into a DateTime
DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

**Oczekiwany wynik**

```
Parsed DateTime: 2021-05-12
```

To cały przepływ **parse japanese era date** — cztery zwięzłe linie kodu.

## Krok 5: Obsługa przypadków brzegowych i alternatywnych er

Dane w rzeczywistym świecie nie zawsze są czyste. Oto kilka scenariuszy, z którymi możesz się spotkać i jak je obsłużyć.

### 5.1 Nieprawidłowe lub puste ciągi

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

### 5.2 Starsze ery (Showa, Taisho)

To samo `CultureInfo ja-JP` działa automatycznie dla starszych er:

```csharp
string showaDate = "昭和45年12月31日"; // Showa 45 = 1970-12-31
DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
Console.WriteLine(showaParsed.ToString("yyyy-MM-dd")); // 1970-12-31
```

### 5.3 Użycie `DateTime.ParseExact` do ścisłej walidacji

Jeśli chcesz wymusić dokładny wzorzec japońskiej ery, użyj własnego ciągu formatowego:

```csharp
string pattern = "ggggy年M月d日"; // gggg = era name, y = year in era
DateTime strictDate = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
Console.WriteLine(strictDate); // 2021-05-12 00:00:00
```

To podejście rzuca `FormatException`, gdy ciąg odbiega od wzorca, co może być przydatne przy kontroli jakości danych.

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do **Program.cs**, a następnie uruchomić.

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

Uruchom go poleceniem `dotnet run`, a powinieneś zobaczyć:

```
Parsed DateTime: 2021-05-12
Showa parsed: 1970-12-31
Strict parse: 2021-05-12
```

Boom — **parse japanese era date** zakończone, masz szablon dla każdej ery, którą możesz napotkać.

![Przebieg parsowania daty japońskiej ery – pokazuje tworzenie skoroszytu, ustawienie kultury, zapis do komórki i wywołanie GetDateTime](parse-japanese-era-date.png "Diagram ilustrujący, jak parsować datę japońskiej ery przy użyciu Aspose.Cells i CultureInfo ja-JP")

## Często zadawane pytania – odpowiedzi

- **Czy to działa z plikami .xlsx, które już zawierają daty w erze?**  
  Tak. Pod warunkiem, że `Settings.CultureInfo` skoroszytu jest ustawione na `ja-JP` *przed* wywołaniem `GetDateTime()`, Aspose.Cells poprawnie zinterpretuje istniejące ciągi.

- **A co z strefami czasowymi?**  
  Parsowanie zwraca `DateTime` z `Kind = Unspecified`. Jeśli potrzebujesz czasu UTC lub lokalnego, użyj `DateTime.SpecifyKind` lub dokonaj konwersji po parsowaniu.

- **Czy mogę parsować wiele komórek jednocześnie?**  
  Oczywiście. Przejdź pętlą po wybranym zakresie i wywołaj `GetDateTime()` dla każdej komórki — pamiętaj tylko o obsłudze wyjątków dla nieprawidłowych wpisów.

## Zakończenie

Omówiliśmy wszystko, co potrzebne do **parse japanese era date** ciągów w C# przy użyciu Aspose.Cells i wbudowanego `CultureInfo ja-JP`. Od konfiguracji skoroszytu, zapisu ciągów w formacie ery, pobrania czystego `DateTime`, po obsługę przypadków brzegowych, takich jak starsze ery i ścisła walidacja — ten przewodnik dostarcza gotowe do produkcji rozwiązanie.

Następnie możesz zbadać **konwersję dat Excel** dla numerycznych dat seryjnych lub zagłębić się w **parsowanie DateTime w C#** z własnymi kalendarzami dla innych regionów. Ten sam wzorzec działa dla tajskiego kalendarza buddyjskiego, kalendarza hebrajskiego i innych — wystarczy zamienić `CultureInfo`.

Masz nietypowy problem? Dodaj komentarz, a wspólnie go rozwiążemy. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak wdrożyć walidację dat w .NET przy użyciu Aspose.Cells: Kompletny przewodnik](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Zmień system dat Excel na 1904 używając Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Efektywne konwertowanie Excel do PDF z niestandardowymi formatami dat przy użyciu Aspose.Cells dla Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}