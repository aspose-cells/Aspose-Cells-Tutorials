---
category: general
date: 2026-10-01
description: Konwertuj datę w japońskiej erze na datę i czas gregoriański przy użyciu
  Aspose.Cells w C#. Dowiedz się, jak szybko konwertować japoński kalendarz.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: pl
lastmod: 2026-10-01
og_description: konwertuj japońską datę ery na datę i godzinę w kalendarzu gregoriańskim
  w C#. Ten tutorial wyjaśnia, jak dokładnie konwertować japoński kalendarz przy użyciu
  Aspose.Cells.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: Konwertuj japońską datę z ery na kalendarz gregoriański w C# – przewodnik
  krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: Jak przekonwertować japońską datę z erą na kalendarz gregoriański w C#
url: /pl/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przekonwertować japoński kalendarz era na datę gregoriańską w C#

Jeśli potrzebujesz **konwertować japońskie daty era** na daty gregoriańskie w C#, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Niezależnie od tego, czy przetwarzasz starsze dane, odczytujesz dane wejściowe od użytkownika, czy generujesz raporty, biblioteka Aspose.Cells ułatwia konwersję. Dodatkowo odkryjesz najlepszy sposób **jak konwertować japoński kalendarz** przy pracy z arkuszami kalkulacyjnymi.

Samouczek obejmuje każdy krok — od utworzenia skoroszytu po pobranie wartości `DateTime` — dzięki czemu możesz skopiować‑wkleić kompletny, działający program. Nie wymaga żadnej zewnętrznej dokumentacji; po prostu postępuj zgodnie z kodem i wyjaśnieniami poniżej.

## Wymagania wstępne

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.6+)
* Licencja na **Aspose.Cells** (darmowa wersja próbna działa do testów)
* Środowisko programistyczne, takie jak Visual Studio 2022 lub VS Code
* Podstawowa znajomość aplikacji konsolowych w C#

## Konwersja japońskiej daty era przy użyciu Aspose.Cells

Rdzeń konwersji opiera się na kilku prostych wywołaniach API. Aspose.Cells automatycznie interpretuje japońskie ciągi era (np. „Reiwa 2/04/01”) i udostępnia wynik jako obiekt `DateTime`, gdy arkusz zostanie przeliczony.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### Dlaczego każdy krok ma znaczenie

| Krok | Cel | Jak pomaga w konwersji |
|------|-----|------------------------|
| **Utwórz skoroszyt** | Zapewnia kontener rozumiejący formuły Excel i systemy dat. | Wewnętrzny silnik dat biblioteki jest aktywowany tylko wewnątrz skoroszytu. |
| **Wstaw ciąg era** | Dostarcza surowy tekst japońskiego kalendarza, który chcesz przetłumaczyć. | Aspose.Cells rozpoznaje nazwy era, takie jak *Reiwa*, *Heisei*, *Showa* itp. |
| **Ustaw styl** | Wymusza traktowanie komórki jako komórki wartości, a nie jako dosłownego ciągu. | Bez stylu metoda `Calculate` może zignorować komórkę, pozostawiając tekst niezmieniony. |
| **Oblicz** | Uruchamia parsowanie ciągu era i konwersję na wewnętrzny numer seryjny daty. | Biblioteka konwertuje „Reiwa 2/04/01” → numer seryjny → gregoriański `DateTime`. |
| **Odczytaj `DateTimeValue`** | Zwraca przekonwertowany obiekt .NET `DateTime`. | Masz teraz standardowy `DateTime`, którego możesz używać w dowolnym API .NET. |

## Jak konwertować japoński kalendarz w innych scenariuszach

To samo podejście działa dla każdej nazwy japońskiej era obsługiwanej przez Aspose.Cells:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### Obsługa nieprawidłowych lub niejednoznacznych ciągów

* **Nieprawidłowa nazwa era** – Aspose.Cells zgłasza `FormatException`. Owiń konwersję w `try/catch`, aby zapewnić przyjazny komunikat o błędzie.
* **Brak roku/miesiąca/dnia** – Biblioteka oczekuje pełnego wzorca „Era Rok/Miesiąc/Dzień”. Jeśli otrzymasz częściowe dane, dołącz brakujące części lub odrzuć wejście wczesniej.
* **Różne ustawienia regionalne** – Konwersja **nie** zależy od bieżącej kultury wątku; zawsze używa mapy japońskich era wbudowanej w Aspose.Cells. Dzięki temu metoda jest bezpieczna w przetwarzaniu po stronie serwera.

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## Praktyczne wskazówki i typowe pułapki

* **Zawsze wywołuj `SetStyle`** przed `Calculate`. Pominięcie tego kroku jest częstym źródłem błędów, ponieważ komórka pozostaje zwykłym holderem tekstu.
* **Używaj tego samego skoroszytu** jeśli musisz konwertować wiele dat. Tworzenie nowego skoroszytu dla każdej konwersji wprowadza niepotrzebne obciążenie.
* **Konwersja wsadowa** – Wypełnij kolumnę ciągami era, wywołaj `worksheet.Calculate()` raz, a następnie odczytaj całą kolumnę `DateTimeValue`. To znacznie wydajniejsze niż przeliczanie każdej komórki osobno.
* **Kompatybilność wersji** – Logika konwersji era została wprowadzona w Aspose.Cells 22.9. Upewnij się, że używasz tej wersji lub nowszej; starsze wydania traktują ciąg jako zwykły tekst.

## Pełny działający przykład (aplikacja konsolowa)

Poniżej znajduje się samodzielny program, który możesz od razu skompilować i uruchomić. Demonstruje konwersję zarówno Reiwa, jak i Heisei, obsługując błędy w sposób elegancki.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**Oczekiwany wynik w konsoli**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

Uruchomienie tego programu potwierdza, że biblioteka poprawnie **konwertuje japońskie daty era** i elegancko zgłasza nieobsługiwane wartości.

## Zakończenie

Teraz wiesz, jak **konwertować japońskie daty era** na standardowe obiekty `DateTime` w kalendarzu gregoriańskim przy użyciu Aspose.Cells w C#. Proces sprowadza się do wstawienia tekstu era, zastosowania stylu, przeliczenia arkusza i odczytania `DateTimeValue`. Postępując zgodnie z powyższymi krokami, możesz także odpowiedzieć na szersze pytanie **jak konwertować japoński kalendarz** w dużej ilości, obsługiwać błędy i optymalizować wydajność.

### Kolejne kroki

* Zbadaj **opcje formatowania**, aby zapisać datę gregoriańską z powrotem do arkusza przy użyciu własnego formatu liczbowego.
* Połącz tę konwersję z **pipeline'ami importu danych** (np. odczyt plików CSV zawierających daty era).
* Przejrzyj inne funkcje Aspose.Cells, takie jak **arytmetyka dat** i **ustawienia regionalne**, dla bardziej złożonych scenariuszy kalendarzowych.

Miłego kodowania, i śmiało dostosuj przykład do własnych przepływów przetwarzania danych!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Parse Japanese Era Date in C# with Aspose.Cells – Full Guide](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Enable Japanese Era Parsing in C# with Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [How to create workbook and convert string to date in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}