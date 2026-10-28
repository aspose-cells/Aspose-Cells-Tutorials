---
category: general
date: 2026-09-24
description: Parsuj DateTime z użyciem panowania japońskiego cesarza przy użyciu Aspose.Cells
  w C#. Włącz japoński kalendarz ery, zapisz ciągi ery i pobierz dokładne wartości
  DateTime.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: pl
lastmod: 2026-09-24
og_description: Parsuj DateTime z użyciem panowania japońskiego cesarza przy użyciu
  Aspose.Cells w C#. Ten samouczek pokazuje, jak włączyć japoński kalendarz ery, zapisywać
  ciągi ery i odczytywać poprawny DateTime.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: Parsowanie DateTime z okresem panowania japońskiego cesarza przy użyciu
  Aspose.Cells – przewodnik C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Parsowanie daty i godziny z uwzględnieniem panowania japońskiego cesarza przy
  użyciu Aspose.Cells
url: /pl/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parsowanie DateTime z użyciem panowania japońskiego cesarza przy użyciu Aspose.Cells

Jeśli potrzebujesz **parsować DateTime z użyciem panowania japońskiego cesarza** w aplikacji .NET, ten przewodnik pokaże Ci dokładnie, jak to zrobić za pomocą Aspose.Cells. Włączając kalendarz japońskich er, zapisując ciąg oparty na erze i odczytując otrzymaną wartość `DateTime`, uzyskasz wiarygodne, kulturowo‑świadome daty bez ręcznej manipulacji ciągami znaków.

Praca z datami w erze japońskiej jest powszechna w finansach, administracji i starszych systemach, które nadal przechowują daty w formacie „令和3年5月10日”. Ten tutorial obejmuje kompletny przepływ pracy, od konfiguracji projektu po uzyskanie obiektu `DateTime`, którego możesz używać w obliczeniach, logowaniu lub wyświetlaniu w interfejsie użytkownika.

## Czego się nauczysz

- Jak dodać pakiet NuGet Aspose.Cells do projektu C#.  
- Jak włączyć **japoński kalendarz er** za pomocą `Workbook.Settings`.  
- Jak zapisać ciąg daty w erze japońskiej do komórki i pozwolić Aspose.Cells automatycznie go sparsować.  
- Jak odczytać sparsowany `DateTime` przy użyciu właściwości `DateTimeValue`.  

**Wymagania wstępne**  
- .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7+).  
- Podstawowa znajomość C# i Visual Studio (lub dowolnego IDE).  
- Dostęp do Internetu w celu pobrania pakietu Aspose.Cells.

---

## Krok 1: Zainstaluj Aspose.Cells

Otwórz folder projektu w terminalu lub w konsoli Menedżera Pakietów NuGet i uruchom:

```bash
dotnet add package Aspose.Cells
```

Lub w Visual Studio, kliknij prawym przyciskiem myszy projekt → **Manage NuGet Packages** → wyszukaj **Aspose.Cells** i kliknij **Install**.  
Spowoduje to dodanie zestawu `Aspose.Cells`, który udostępnia klasy `Workbook`, `Worksheet` oraz funkcje parsowania, których potrzebujemy.

## Krok 2: Włącz japoński kalendarz er

Aspose.Cells domyślnie wyłącza parsowanie japońskich er. Musisz je włączyć poprzez flagę `Workbook.Settings.UseJapaneseEraCalendar`.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

Ustawienie `UseJapaneseEraCalendar` na `true` informuje bibliotekę, aby interpretowała ciągi zawierające nazwy er (`令和`, `平成`, `昭和` itp.) zgodnie z oficjalnymi zasadami japońskiego kalendarza.

## Krok 3: Zapisz ciąg daty w erze japońskiej do komórki

Następnie pobierz pierwszy arkusz i umieść ciąg daty w erze japońskiej w komórce **A1**.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**Dlaczego to działa:**  
Gdy `UseJapaneseEraCalendar` jest aktywne, metoda `PutValue` analizuje ciąg, wykrywa prefiks ery (`令和`) i wewnętrznie konwertuje go na odpowiadający rok gregoriański (2021). Biblioteka zapisuje wtedy wartość jako prawdziwy obiekt `DateTime`, a nie jako zwykły tekst.

## Krok 4: Odczytaj sparsowaną wartość `DateTime`

Teraz odczytaj właściwość `DateTimeValue` komórki. Aspose.Cells automatycznie zwróci datę gregoriańską.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

Uruchomienie programu wypisze:

```
Parsed Gregorian date: 2021-05-10
```

Wynik potwierdza, że **Parse DateTime with Japanese Emperor Reign** poprawnie przekształciło „令和3年5月10日” na 10 maja 2021 r.

## Krok 5: Obsługa przypadków brzegowych i typowych wariacji

### Różne formaty er
Aspose.Cells rozpoznaje kilka reprezentacji er:

| Era (Japanese) | Zakres lat gregoriańskich |
|----------------|--------------------------|
| 明治 (Meiji)   | 1868‑1912                |
| 大正 (Taishō)  | 1912‑1926                |
| 昭和 (Shōwa)   | 1926‑1989                |
| 平成 (Heisei)  | 1989‑2019                |
| 令和 (Reiwa)   | 2019‑obecnie             |

Jeśli Twoje dane źródłowe mieszają znaki pełnej szerokości, spacje lub używają kanji „年”, „月”, „日”, parser i tak zadziała. Na przykład, `"平成31年4月30日"` zostanie przekształcone na `2019-04-30`.

### Nieprawidłowe ciągi
Gdy ciąg nie może zostać sparsowany (np. `"令和99年13月40日"`), `DateTimeValue` zwraca `DateTime.MinValue`. Możesz sprawdzić tę sytuację:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### Wyłączanie funkcji
Jeśli później potrzebujesz przechowywać surowe ciągi er bez konwersji, ustaw flagę z powrotem na `false`:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### Wskazówka dotycząca wydajności
Włączenie kalendarza er dodaje niewielki narzut do każdego wywołania `PutValue`, które dotyczy ciągów. Jeśli parsujesz tylko kilka komórek, włącz flagę tuż przed operacją i wyłącz ją po zakończeniu, aby zminimalizować wpływ na wydajność.

## Kompletny, gotowy do uruchomienia przykład

Poniżej znajduje się pełny program, który możesz skopiować, wkleić i od razu uruchomić.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**Oczekiwany wynik**

```
Parsed Gregorian date: 2021-05-10
```

Program demonstruje pełny przepływ **Parse DateTime with Japanese Emperor Reign** przy użyciu Aspose.Cells, od utworzenia skoroszytu po uzyskanie użytecznego obiektu `DateTime`.

---

## Podsumowanie

Teraz wiesz, jak **parsować DateTime z użyciem panowania japońskiego cesarza** w C# poprzez:

1. Instalację **Aspose.Cells**.  
2. Włączenie **japońskiego kalendarza er** za pomocą `Workbook.Settings`.  
3. Zapis ciągów opartych na erze do komórek.  
4. Odczyt właściwości `DateTimeValue`.  

To podejście eliminuje ręczną logikę parsowania, respektuje oficjalne granice er i integruje się płynnie z istniejącym kodem obsługującym daty w .NET.  

**Kolejne kroki**  
- Zbadaj inne funkcje kulturowe Aspose.Cells, takie jak **C# date parsing** dla kalendarzy hijri lub tajskiego buddyjskiego.  
- Połącz tę technikę z ustawieniami skoroszytu, takimi jak `CalcEngine`, aby oceniać formuły odwołujące się do dat w erze.  
- Używaj sparsowanego `DateTime` w raportach, przechowywaniu w bazie danych lub komponentach UI wymagających dat gregoriańskich.

Śmiało eksperymentuj z różnymi ciągami er, obsługuj nieprawidłowe dane i integruj rozwiązanie w większych pipeline’ach importu danych. Powodzenia w kodowaniu!


## Co powinieneś nauczyć się dalej?


Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz krok‑po‑kroku wyjaśnienia, pomagające opanować dodatkowe funkcje API i poznać alternatywne podejścia implementacyjne w własnych projektach.

- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to Parse Japanese Dates in C# – Complete Guide](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}