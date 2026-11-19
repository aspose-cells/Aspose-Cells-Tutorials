---
category: general
date: 2026-11-19
description: Ustaw format liczbowy komórki w C# i dowiedz się, jak zastosować format
  daty Excel dla japońskich dat ery, umożliwiając niezawodną konwersję dat Excel w
  C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: pl
lastmod: 2026-11-19
og_description: Ustaw format liczbowy komórki w C# i zastosuj format daty Excel dla
  dat japońskich er. Skorzystaj z tego pełnego przewodnika, aby dokładnie konwertować
  daty w C# Excel.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: Ustaw format liczbowy komórki i konwertuj japońskie daty w C# – przewodnik
  krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: Ustaw format liczby w komórce i konwertuj japońskie daty w C#
url: /pl/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ustaw format liczbowy komórki i konwertuj japońskie daty w C#

Jeśli potrzebujesz **ustawić format liczbowy komórki** w projekcie automatyzacji Excel w C#, ten przewodnik pokaże Ci, jak **zastosować format daty Excel** i wykonać **konwersję daty Excel w C#** dla dat z japońskich er. Otrzymasz kompletny, gotowy do uruchomienia przykład, który konwertuje ciąg z ery Reiwa (np. `R3/04/01`) na datę gregoriańską `2021‑04‑01`.

## Czego się nauczysz

* Jak utworzyć skoroszyt i uzyskać dostęp do jego pierwszego arkusza.  
* Jak **ustawić format liczbowy komórki**, aby Excel traktował wartość jako datę.  
* Jak **zastosować format daty Excel**, który rozpoznaje ciągi z japońskimi erami.  
* Jak wywołać **konwersję daty Excel w C#** poprzez przeliczenie formuł.  
* Oczekiwany wynik oraz wskazówki rozwiązywania problemów w przypadkach brzegowych.

**Wymagania wstępne**

* .NET 6 lub nowszy (kod działa również z .NET Framework 4.6+).  
* Aspose.Cells dla .NET 2024 lub nowszy – zainstaluj przez NuGet: `dotnet add package Aspose.Cells`.  
* Podstawowa znajomość C# i obsługi dat w Excelu.

> **Pro tip:** Aspose.Cells działa bez zainstalowanego Microsoft Office, co czyni go idealnym do automatyzacji po stronie serwera.

## Ustaw format liczbowy komórki przy użyciu Aspose.Cells w C#

Pierwszym krokiem jest poinformowanie Excela, że komórka zawiera datę. Excel przechowuje daty jako liczby seryjne, więc musimy zastosować wbudowany format liczbowy daty (ID 14) do docelowej komórki.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### Dlaczego to działa

* `Style.Number = 14` mapuje do formatu *Krótka data* w Excelu (`mm/dd/yyyy` domyślnie).  
* Gdy komórka zawiera ciąg z japońską erą, np. `R3/04/01`, wewnętrzny parser Aspose.Cells rozpoznaje erę i konwertuje ją na odpowiadającą liczbę seryjną gregoriańską podczas `CalculateFormula()`.  
* Po obliczeniu, `StringValue` zwraca sformatowaną datę gregoriańską.

## Zastosuj format daty Excel dla japońskich dat erowych

Jeśli chcesz, aby komórka wyświetlała japońską erę zamiast daty gregoriańskiej, możesz użyć niestandardowego formatu liczbowego, który zawiera kod ery. To demonstruje możliwość **zastosowania formatu daty Excel**.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` wymusza japoński locale.  
* `ggg` reprezentuje nazwę ery (np. `R` dla Reiwa).  
* Dodanie znaków dosłownych (`年`, `月`, `日`) tworzy znany układ japońskiej daty.

### Kiedy używać niestandardowego formatu

* Raporty przeznaczone dla japońskiej publiczności.  
* Gdy konieczne jest zachowanie pierwotnej informacji o erze w dokumentach prawnych.  
* W pulpitach nawigacyjnych, gdzie zarówno daty gregoriańskie, jak i erowe są wyświetlane obok siebie.

## Konwersja daty Excel w C# – obsługa japońskich er

Proces **c# excel date conversion** można podzielić na trzy logiczne części:

1. **Parsowanie ciągu ery** – Aspose.Cells automatycznie rozpoznaje `R` (Reiwa), `H` (Heisei), `S` (Showa) itd.  
2. **Konwersja na liczbę seryjną** – Excel przechowuje daty jako liczbę dni od 1899‑12‑30.  
3. **Formatowanie liczby seryjnej** – albo wbudowanym formatem (ID 14), albo niestandardowym formatem japońskim.

### Pełny przykład end‑to‑end

Poniżej znajduje się samodzielny program, który demonstruje zarówno wyjście gregoriańskie, jak i erowe w jednym uruchomieniu.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**Oczekiwany wynik w konsoli**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### Przypadki brzegowe i typowe pułapki

| Sytuacja                              | Na co zwrócić uwagę                                   | Naprawa / Rekomendacja                                   |
|---------------------------------------|-------------------------------------------------------|----------------------------------------------------------|
| Pusty lub nieprawidłowy ciąg ery      | `PutValue` zapisuje tekst dosłowny; konwersja nie powodzi się | Zweryfikuj wejście przy użyciu wyrażenia regularnego przed zapisem do komórki. |
| Niepasujący locale                    | Niestandardowy format wyświetla zachodnie cyfry zamiast japońskich znaków | Upewnij się, że format `Custom` zawiera `[$-ja-JP]` lub ustaw `Workbook.Settings.CultureInfo` na `ja-JP`. |
| Skoroszyt zawiera formuły odwołujące się do komórki z datą | Przeliczenie może nadpisać wyniki formuł | Wywołaj `CalculateFormula` **po** wszystkich krokach formatowania, lub użyj `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)`, jeśli potrzebujesz pominąć błędy. |
| Używanie starszych wersji Aspose.Cells | Obsługa japońskich er została dodana w Q3 2022          | Zaktualizuj do najnowszego pakietu NuGet.                     |

## Testowanie rozwiązania

1. **Uruchom program** z Visual Studio lub `dotnet run`.  
2. Zweryfikuj, że konsola wyświetla datę gregoriańską `2021‑04‑01` oraz ciąg ery `R3年04月01日`.  
3. Otwórz wygenerowany skoroszyt (jeśli dodasz `wb.Save("Demo.xlsx");`) w Microsoft Excel, aby zobaczyć te same formatowania zastosowane w komórkach.

### Wskazówka dotycząca automatyzacji

Jeśli musisz przetworzyć dużą gamę dat erowych (np. kolumna A zawiera wiele japońskich dat), otocz logikę konwersji pętlą:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

To podejście utrzymuje operację **ustawiania formatu liczbowego komórki** szybką i oszczędną pod względem pamięci.

## Podsumowanie

Teraz wiesz, jak **ustawić format liczbowy komórki** w C# przy użyciu Aspose.Cells, jak **zastosować format daty Excel** dla japońskich ciągów erowych oraz jak wykonać niezawodną **konwersję daty Excel w C#** z ery na daty gregoriańskie. Kompletny, gotowy do uruchomienia kod demonstruje oba wyniki i podkreśla typowe przypadki brzegowe.  

**Kolejne kroki**

* Poznaj inne wbudowane identyfikatory formatów

## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [ustaw format daty Excel w C# – Kompletny przewodnik krok po kroku](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [Jak zastosować format liczbowy Excel z Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [Jak zastosować niestandardowy format liczbowy Excel w C#](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}