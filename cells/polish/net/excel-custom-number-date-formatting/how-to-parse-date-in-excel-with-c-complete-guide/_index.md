---
category: general
date: 2026-05-23
description: Jak odczytać datę z komórki Excel przy użyciu C#. Poznaj triki z niestandardowymi
  formatami liczb w Excelu, odczytaj datę z komórki i zastosuj niestandardowy format
  dla dokładnych wyników.
draft: false
keywords:
- how to parse date
- custom number format excel
- read date from cell
- format excel cell date
- apply custom format
language: pl
og_description: Jak odczytać datę z komórki Excela przy użyciu C#. Ten samouczek pokazuje,
  jak zastosować niestandardowy format liczbowy w Excelu, odczytać datę z komórki
  oraz poprawnie sformatować datę w komórce Excela.
og_title: Jak parsować datę w Excelu przy użyciu C# – Kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  headline: How to Parse Date in Excel with C# – Complete Guide
  type: TechArticle
- description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  name: How to Parse Date in Excel with C# – Complete Guide
  steps:
  - name: Why a Custom Format Works
    text: Excel stores dates as serial numbers internally. By applying a locale‑aware
      format, Excel attempts to *interpret* the underlying text according to the pattern.
      The `[$-ja-JP]` prefix forces the Japanese calendar rules, while the rest of
      the pattern maps the characters to year, month, and day.
  - name: 1. Parsing European Dates (e.g., “12/05/2021” in French)
    text: '```csharp firstCell.PutValue("12/05/2021"); // day/month/year Style frStyle
      = workbook.CreateStyle(); frStyle.Custom = "[$-fr-FR]dd/mm/yyyy"; firstCell.SetStyle(frStyle);
      DateTime frDate = firstCell.DateTimeValue; // 2021-05-12 ```'
  - name: 2. When the Cell Already Contains a Serial Date
    text: 'If the source Excel file already stores a true date value, you can skip
      the custom format entirely:'
  - name: 3. Fallback to Manual Parsing
    text: 'Sometimes data is messy (extra spaces, hidden characters). A safe fallback
      is:'
  type: HowTo
tags:
- Excel
- C#
- Date Parsing
title: Jak parsować datę w Excelu przy użyciu C# – Kompletny przewodnik
url: /pl/net/excel-custom-number-date-formatting/how-to-parse-date-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak parsować datę w Excelu przy użyciu C# – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak parsować datę** przechowywaną w arkuszu Excel bez ręcznego manipulowania konwersjami łańcuchów? Nie jesteś jedyny. Niezależnie od tego, czy pobierasz japońskie daty fiskalne, europejskie kombinacje miesiąc‑dzień, czy dowolny łańcuch specyficzny dla lokalizacji, uzyskanie niezawodnego `DateTime` w C# może przypominać gonitwę za poruszającym się celem.  

W tym samouczku przeprowadzimy Cię przez konkretny, kompleksowy przykład, który **zastosowuje niestandardowy format liczbowy Excel** do komórki tekstowej, a następnie **odczytuje datę z komórki** jako prawidłowy `DateTime`. Po zakończeniu dokładnie będziesz wiedział, jak **formatować datę w komórce Excel**, **zastosować niestandardowy format** i unikać typowych pułapek, które potykają większość programistów.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa z .NET Core, .NET Framework i .NET 5+)
- Odwołanie do biblioteki arkuszy kalkulacyjnych obsługującej manipulację stylami – w przykładzie użyto **Aspose.Cells**, ale koncepcje można zastosować w EPPlus, ClosedXML lub NPOI.
- Podstawowa znajomość C# (dasz radę, prawda?)

> **Pro tip:** Jeśli nie masz jeszcze Aspose.Cells, możesz pobrać darmową wersję próbną z ich strony i dodać ją przez NuGet: `dotnet add package Aspose.Cells`.

## Przegląd rozwiązania

1. **Utwórz skoroszyt** i wskaż pierwszą komórkę pierwszego arkusza.  
2. **Wstaw łańcuch daty specyficzny dla lokalizacji** (w naszym przypadku japoński).  
3. **Zastosuj niestandardowy format liczbowy**, który instruuje Excel, aby traktował łańcuch jako datę.  
4. **Odczytaj wartość komórki** jako obiekt `DateTime`.  

To cały przepływ – bez ręcznego parsowania, bez akrobacji `DateTime.ParseExact`. Zanurzmy się.

---

## Krok 1: Przygotowanie skoroszytu i docelowej komórki

Najpierw utwórz nowy skoroszyt i pobierz komórkę, z którą będziemy pracować. Odzwierciedla to scenariusz „nowy skoroszyt”, od którego zaczynają większość zadań przetwarzania wsadowego.

```csharp
using Aspose.Cells;

// Create a new workbook
Workbook workbook = new Workbook();

// Get the first worksheet's first cell (A1)
Cell firstCell = workbook.Worksheets[0].Cells[0, 0];
```

> **Dlaczego to ważne:** Inicjalizacja skoroszytu programowo zapewnia kontrolę nad każdym aspektem pliku – brak ukrytych niespodzianek formatowania. Obiekt `Cell` jest naszym punktem wejścia zarówno dla treści, jak i stylu.

---

## Krok 2: Wstawienie japońskiego łańcucha daty

Excel często otrzymuje daty jako zwykły tekst, szczególnie gdy dane pochodzą z systemów legacy. Tutaj symulujemy to, wstawiając japońską datę ery bezpośrednio do komórki.

```csharp
// Insert a Japanese date string (令和3年5月12日 = May 12, 2021)
firstCell.PutValue("令和3年5月12日");
```

> **Uwaga dotycząca przypadków brzegowych:** Jeśli komórka już zawierała prawdziwą datę Excel (liczbę seryjną), można pominąć krok z niestandardowym formatem. Ten przewodnik koncentruje się na ścieżce konwersji *tekst‑do‑daty*.

---

## Krok 3: Zastosowanie niestandardowego formatu liczbowego, który interpretuje tekst jako datę

Teraz następuje magia: instruujemy Excel, aby traktował łańcuch przy użyciu **niestandardowego formatu liczbowego Excel** dopasowanego do japońskiej lokalizacji. Łańcuch formatu `[$-ja-JP]yyyy` wyodrębnia komponent roku, ale można go rozbudować o miesiąc i dzień w razie potrzeby.

```csharp
// Define a style with a custom number format for Japanese locale
Style style = workbook.CreateStyle();
style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";

// Apply the style to the cell
firstCell.SetStyle(style);
```

### Dlaczego działa niestandardowy format

Excel przechowuje daty wewnętrznie jako liczby seryjne. Stosując format zależny od lokalizacji, Excel próbuje *zinterpretować* podstawowy tekst zgodnie z wzorcem. Prefiks `[$-ja-JP]` wymusza zasady japońskiego kalendarza, a reszta wzorca mapuje znaki na rok, miesiąc i dzień.

> **Alternatywa:** Jeśli potrzebujesz bardziej ogólnego podejścia, możesz użyć `[$-en-US]mm/dd/yyyy` dla dat w stylu amerykańskim lub dowolnego innego kodu kultury obsługiwanego przez Windows.

---

## Krok 4: Pobranie sparsowanej daty jako obiektu `DateTime`

Na koniec pytamy komórkę o jej `DateTimeValue`. Aspose.Cells automatycznie konwertuje sformatowany tekst na prawidłowy obiekt `DateTime`.

```csharp
// Retrieve the cell value as a DateTime
DateTime parsedDate = firstCell.DateTimeValue;

// Output to console for verification
Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
```

**Oczekiwany wynik w konsoli**

```
Parsed date: 2021-05-12
```

> **Co jeśli zwróci `DateTime.MinValue`?** To zazwyczaj oznacza, że format nie pasuje do zawartości komórki. Sprawdź ponownie łańcuch niestandardowego formatu i upewnij się, że kod lokalizacji odpowiada językowi źródłowemu.

---

## Bonus: Obsługa innych lokalizacji i rzeczywistych wariacji

### 1. Parsowanie europejskich dat (np. „12/05/2021” po francusku)

```csharp
firstCell.PutValue("12/05/2021"); // day/month/year
Style frStyle = workbook.CreateStyle();
frStyle.Custom = "[$-fr-FR]dd/mm/yyyy";
firstCell.SetStyle(frStyle);
DateTime frDate = firstCell.DateTimeValue; // 2021-05-12
```

### 2. Gdy komórka już zawiera datę seryjną

Jeśli źródłowy plik Excel już przechowuje prawdziwą wartość daty, możesz całkowicie pominąć niestandardowy format:

```csharp
DateTime existingDate = firstCell.DateTimeValue; // works out‑of‑the‑box
```

### 3. Alternatywa: ręczne parsowanie

Czasami dane są nieporządne (dodatkowe spacje, ukryte znaki). Bezpieczną alternatywą jest:

```csharp
string raw = firstCell.StringValue?.Trim();
if (DateTime.TryParseExact(raw, "yyyy/MM/dd", CultureInfo.InvariantCulture,
                           DateTimeStyles.None, out DateTime fallback))
{
    // use fallback
}
```

Jednak podejście **zastosowania niestandardowego formatu** jest zazwyczaj szybsze i mniej podatne na błędy, ponieważ wykorzystuje własny silnik parsowania Excela.

---

## Typowe pułapki i jak ich unikać

| Pułapka | Objaw | Rozwiązanie |
|---------|-------|-------------|
| Nieprawidłowy kod lokalizacji (`[$-ja-JP]` vs `[$-ja]`) | `DateTimeValue` pozostaje na `1/1/1900` | Sprawdź dokładny ciąg LCID; użyj `CultureInfo.GetCultureInfo("ja-JP").LCID`, aby mieć pewność. |
| Brak cudzysłowów wokół statycznego tekstu | Excel traktuje `"年"` jako symbol formatu i nie działa | Umieść statyczne znaki w podwójnych cudzysłowach, np. `\"年\"`. |
| Komórka już sformatowana jako *Tekst* | Niestandardowy format ignorowany | Wyczyść najpierw `NumberFormat` komórki: `firstCell.SetStyle(workbook.CreateStyle());` |
| Używanie biblioteki, która nie obsługuje właściwości `Custom` | Błąd kompilacji | Przejdź na bibliotekę, która udostępnia niestandardowe formaty liczbowe (Aspose.Cells, EPPlus, ClosedXML). |

---

## Pełny działający przykład (gotowy do kopiowania i wklejania)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get target cell
        Workbook workbook = new Workbook();
        Cell firstCell = workbook.Worksheets[0].Cells[0, 0];

        // 2️⃣ Insert Japanese date string
        firstCell.PutValue("令和3年5月12日");

        // 3️⃣ Apply custom number format for Japanese locale
        Style style = workbook.CreateStyle();
        style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";
        firstCell.SetStyle(style);

        // 4️⃣ Retrieve parsed DateTime
        DateTime parsedDate = firstCell.DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Expected: Parsed date: 2021-05-12

        // Optional: Save the workbook to see the formatted cell in Excel
        workbook.Save("ParsedDateExample.xlsx");
    }
}
```

Uruchom program, otwórz `ParsedDateExample.xlsx`, a zobaczysz, że komórka **A1** wyświetla `2021年5月12日`, podczas gdy ukryta wartość jest prawidłową datą Excel.

---

## Zakończenie

Omówiliśmy **jak parsować łańcuchy dat** w Excelu przy użyciu C# poprzez **zastosowanie niestandardowego formatu liczbowego Excel** i następnie **odczyt daty z komórki** jako natywnego `DateTime`. Kluczowe wnioski:

- Używaj niestandardowego formatu zależnego od lokalizacji (`[$-ja-JP]…`), aby Excel wykonał ciężką pracę.  
- Uzyskaj `Cell.DateTimeValue`, aby otrzymać czysty `DateTime` bez ręcznego parsowania.  
- Dostosuj łańcuch formatu dla innych kultur i zawsze weryfikuj szybkim wyświetleniem w konsoli.  

Od tego momentu możesz **formatować datę w komórce Excel** do raportów, wprowadzać `DateTime` do baz danych lub wykonywać obliczenia bezpośrednio w aplikacji C#. Eksperymentuj z różnymi lokalizacjami, łącz wiele komórek lub nawet przetwarzaj wsadowo całe arkusze – te same zasady mają zastosowanie.

Masz dziwny format daty, którego nie możesz rozgryźć? Dodaj komentarz, a wspólnie znajdziemy rozwiązanie. Szczęśliwego kodowania!

## Powiązane samouczki

- [Excel Custom Number and Date Formatting](/cells/english/net/excel-custom-number-date-formatting/)
- [Mastering Data Presentation in Excel: Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Excel Custom Number Date Formatting](/cells/german/net/excel-custom-number-date-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}