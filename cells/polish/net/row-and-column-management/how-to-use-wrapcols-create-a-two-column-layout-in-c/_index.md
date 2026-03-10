---
category: general
date: 2026-02-15
description: Jak używać WRAPCOLS do stworzenia układu dwukolumnowego, dodania formuły
  i wygenerowania tablicy sekwencji w arkuszach C# – przewodnik krok po kroku.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: pl
og_description: Jak używać WRAPCOLS do stworzenia układu dwukolumnowego, dodawania
  formuł i generowania tablicy sekwencji w arkuszu C# – kompletny przewodnik.
og_title: 'Jak używać WRAPCOLS: układ dwukolumnowy w C#'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'Jak używać WRAPCOLS: Tworzenie układu dwukolumnowego w C#'
url: /pl/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać WRAPCOLS: Tworzenie układu dwukolumnowego w C#

Zastanawiałeś się kiedyś **jak używać WRAPCOLS**, gdy potrzebujesz szybkiego widoku dwukolumnowego w arkuszu stylizowanym na Excel? Nie jesteś sam. Wielu programistów napotyka problem, gdy próbują podzielić wygenerowaną listę na schludne kolumny bez pisania pętli dla każdej komórki. Dobre wieści? Dzięki funkcji `WRAPCOLS` możesz wstawić jedną formułę do `A1` i pozwolić Excelowi (lub kompatybilnemu silnikowi) wykonać ciężką pracę.

W tym samouczku przejdziemy przez **jak dodać formułę**, która tworzy **układ dwukolumnowy**, pokażemy ci **jak dynamicznie tworzyć kolumny** oraz nawet **generować tablicę sekwencji** w locie. Po zakończeniu będziesz mieć w pełni działający fragment C#, który możesz wkleić do swojego projektu, uruchomić i od razu zobaczyć schludny dwukolumnowy blok.

## Czego się nauczysz

- Cel funkcji `WRAPCOLS` i dlaczego jest lepszą alternatywą niż ręczne pętle.  
- Jak **dodać formułę** do komórki arkusza przy użyciu C#.  
- Jak wygenerować tablicę sekwencji przy użyciu `SEQUENCE` i przekazać ją do `WRAPCOLS`.  
- Wskazówki dotyczące przeliczania arkusza, aby formuła została natychmiast rozwiązana.  
- Obsługa przypadków brzegowych (np. puste arkusze, niestandardowa liczba kolumn).

Nie są wymagane żadne zewnętrzne biblioteki poza standardowym pakietem do obsługi Excela – użyjemy **ClosedXML** ze względu na jego prosty interfejs API, ale koncepcje można zastosować w EPPlus, SpreadsheetGear lub nawet w Google Sheets poprzez jego API.

---

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod kompiluje się na .NET Core i .NET Framework).  
- Odwołanie do **ClosedXML** (`dotnet add package ClosedXML`).  
- Podstawowa znajomość C# – powinieneś być swobodny w używaniu instrukcji `using` i inicjalizacji obiektów.

Jeśli masz już otwarty skoroszyt, możesz pominąć część tworzenia pliku i od razu przejść do sekcji z formułą.

---

## Krok 1: Przygotowanie arkusza (Jak tworzyć kolumny)

Najpierw potrzebujemy obiektu `Worksheet`, z którym będziemy pracować. W ClosedXML uzyskujesz go z `XLWorkbook`. Poniższy fragment tworzy nowy skoroszyt, dodaje arkusz o nazwie *Demo* i pobiera referencję nazwaną `worksheet` dla przejrzystości.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **Dlaczego zmienić nazwę?**  
> Trzymanie krótkiej nazwy zmiennej (`worksheet`) ułatwia późniejsze czytanie kodu, szczególnie gdy łańcuchujesz wiele operacji. Odzwierciedla to także styl nazewnictwa, który spotkasz w większości dokumentacji, zmniejszając obciążenie poznawcze.

---

## Krok 2: Wpisanie formuły (Jak dodać formułę + generować tablicę sekwencji)

Teraz nadchodzi magiczna linia. Umieścimy formułę w komórce **A1**, która robi dwie rzeczy:

1. **Wygenerować tablicę sekwencji** sześciu liczb (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Zawinąć te liczby w dwie kolumny** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **Co się dzieje?**  
> `SEQUENCE(6)` tworzy pionową tablicę `{1;2;3;4;5;6}`. `WRAPCOLS` następnie przyjmuje tę tablicę i „zawija” ją do określonej liczby kolumn — w tym przypadku **2**. Wynikiem jest blok 3‑wiersz × 2‑kolumnowy, który wygląda tak:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Jeśli zmienisz drugi argument na **3**, otrzymasz układ trzech kolumn. To jest sedno **jak tworzyć kolumny** w locie bez ręcznych pętli.

---

## Krok 3: Przeliczenie arkusza (Zapewnienie oceny formuły)

ClosedXML nie oceni automatycznie formuł po ich zapisaniu. Musisz wywołać `Calculate()` na skoroszycie (lub na konkretnym arkuszu), aby wymusić ocenę.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Wskazówka:** Jeśli pracujesz z dużymi skoroszytami, wywołuj `Calculate()` tylko na arkuszach, które faktycznie się zmieniły. To oszczędza pamięć i przyspiesza przetwarzanie.

Kiedy otworzysz `WrapColsDemo.xlsx`, zobaczysz dwukolumnowy układ starannie wypełniony w **A1:B3**. Nie było potrzebne dodatkowe kodowanie pętli przez wiersze lub kolumny – `WRAPCOLS` obsłużyło wszystko.

---

## Krok 4: Weryfikacja wyniku (Czego oczekiwać)

Po uruchomieniu programu otwórz wygenerowany plik. Powinieneś zobaczyć:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Jeśli liczby pojawią się pionowo (czyli wszystkie w kolumnie A), sprawdź, czy wywołałeś `worksheet.Calculate()` **po** ustawieniu formuły. Niektóre silniki wymagają również `workbook.Calculate()`; powyższy fragment działa z wbudowanym ewaluatorem ClosedXML.

---

## Typowe warianty i przypadki brzegowe

### Zmiana liczby kolumn

Aby **utworzyć układ dwukolumnowy** z inną liczbą wierszy, po prostu dostosuj rozmiar `SEQUENCE` lub drugi argument `WRAPCOLS`:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

To generuje blok 4‑wiersz × 3‑kolumnowy (12 liczb podzielonych na trzy kolumny).

### Użycie dynamicznej liczby kolumn

Jeśli liczba kolumn pochodzi z zmiennej, wstaw ją przy użyciu interpolacji ciągu znaków:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Teraz masz **jak dodać formułę**, która dostosowuje się w czasie wykonywania.

### Puste arkusze

Jeśli arkusz jest pusty, `Calculate()` nadal działa – formuła wypełni komórki zaczynając od A1. Jednak jeśli później usuniesz wiersze/kolumny, które przecinają zakres wyjściowy, możesz zobaczyć błędy `#REF!`. Aby tego uniknąć, najpierw wyczyść docelowy zakres:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Zgodność

`WRAPCOLS` i `SEQUENCE` są częścią funkcji **Dynamic Array** Excela, wprowadzonych w Office 365. Jeśli celujesz w starsze wersje Excela, funkcje te nie będą dostępne i będziesz potrzebować ręcznej pętli. Ewaluator ClosedXML odzwierciedla najnowsze zachowanie Excela, więc jest bezpieczny w nowoczesnych środowiskach.

---

## Pełny działający przykład (Gotowy do kopiowania i wklejenia)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Oczekiwany wynik:** Otwierając *WrapColsDemo.xlsx* zobaczysz schludny układ dwukolumnowy z liczbami 1‑6 ułożonymi jak opisano wcześniej.

---

## Podsumowanie

Omówiliśmy **jak używać WRAPCOLS** do **tworzenia układu dwukolumnowego**, pokazaliśmy **jak dodać formułę** programowo oraz zobaczyliśmy, jak `SEQUENCE` pozwala **generować tablicę sekwencji** bez pętli. Wykorzystując dynamiczne funkcje tablicowe Excela w C#, możesz utrzymać kod zwięzły, czytelny i łatwy w utrzymaniu.

Następnie możesz zbadać:

- **Tworzenie dynamicznej liczby wierszy** przy użyciu `ROWS` lub `COUNTA`.  
- **Stylowanie wyniku** (obramowania, formaty liczb) przy użyciu API stylizacji ClosedXML.  
- **Eksport do CSV** po zbudowaniu układu, w celu dalszego przetwarzania.

Spróbuj, zmodyfikuj liczbę kolumn i zobacz, jak szybko możesz prototypować złożone arkusze kalkulacyjne. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}