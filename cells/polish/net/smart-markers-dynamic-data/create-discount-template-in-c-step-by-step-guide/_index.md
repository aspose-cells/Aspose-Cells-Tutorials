---
category: general
date: 2026-02-14
description: Szybko utwórz szablon rabatu i dowiedz się, jak zastosować rabat w arkuszu
  kalkulacyjnym, wstrzyknąć dane do szablonu oraz zdefiniować zmienny prefiks dla
  inteligentnych znaczników.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: pl
og_description: Utwórz szablon rabatu w C#. Dowiedz się, jak zastosować rabat w arkuszu
  kalkulacyjnym, wstrzyknąć dane do szablonu i zdefiniować zmienny prefiks dla inteligentnych
  znaczników.
og_title: Utwórz szablon rabatu – Pełny przewodnik C#
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Utwórz szablon rabatu w C# – Przewodnik krok po kroku
url: /pl/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

translated content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Discount Template – Full C# Walkthrough

Kiedykolwiek potrzebowałeś **create discount template** dla raportu sprzedaży, ale nie wiedziałeś, jak automatycznie wprowadzić liczby do arkusza kalkulacyjnego? Nie jesteś sam. W tym samouczku pokażemy dokładnie, jak **create discount template**, następnie **apply discount in spreadsheet** w komórkach, **inject data into template** oraz nawet **define variable prefix** dla twoich smart markers — wszystko przy użyciu czystego kodu C#.

Zaczniemy od nakreślenia problemu, a potem od razu przejdziemy do działającego rozwiązania, które możesz skopiować i wkleić. Po zakończeniu będziesz mieć wielokrotnego użytku wzorzec, który działa niezależnie od tego, czy generujesz faktury, cenniki, czy jakikolwiek arkusz kalkulacyjny wymagający dynamicznych rabatów.

---

## Czego się nauczysz

- Jak zaprojektować szablon arkusza kalkulacyjnego uwzględniający rabaty.
- Jak skonfigurować własny `VariablePrefix` / `VariableSuffix`, aby znaczniki były łatwe do zauważenia.
- Jak przekazać anonimowy obiekt (`discountData`) do `SmartMarkerProcessor`.
- Jak wynikowa formuła (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) automatycznie oblicza ostateczną cenę.
- Wskazówki dotyczące obsługi przypadków brzegowych, takich jak wiersze bez rabatu lub wielopoziomowe rabaty.

**Prerequisites** – aktualny środowisko uruchomieniowe .NET (≥ .NET 6), odwołanie do biblioteki `Aspose.Cells` (lub podobnej), która udostępnia `SmartMarkerProcessor`, oraz podstawowa znajomość składni C#. Nic egzotycznego.

---

## Krok 1: Utwórz Szablon Rabatu w Twoim Arkuszu

Najpierw otwórz nowy skoroszyt (lub użyj istniejącego) i umieść placeholder, w którym zostanie zastosowany rabat. Traktuj szablon jako zwykły plik Excel z „smart markers”, które procesor zamieni.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Dlaczego to ma znaczenie:** Poprzez osadzenie `#Discount#` w formule informujemy procesor, gdzie dokładnie ma się znaleźć wartość rabatu. `SmartMarkerProcessor` zastąpi `#Discount#` podaną później liczbą, pozostawiając resztę formuły niezmienioną.

## Krok 2: Zdefiniuj Prefiks Zmiennej dla Smart Markers

Domyślnie wiele bibliotek szuka `${Variable}` lub `{{Variable}}`. W naszym przypadku chcemy czysty, czytelny dla człowieka znacznik, więc **define variable prefix** i suffix definiujemy explicite.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro tip:** Użycie `#` utrzymuje znaczniki krótkie i łatwe do zauważenia w pasku formuły Excela. Jeśli kiedykolwiek będziesz musiał uniknąć konfliktów z istniejącymi funkcjami Excela, wybierz inny zestaw (np. `[[` i `]]`).

## Krok 3: Wstrzyknij Dane do Szablonu przy użyciu SmartMarkerProcessor

Teraz podajemy rzeczywistą wartość rabatu. Procesor przeszuka arkusz, znajdzie każde `#Discount#` i zastąpi je wartością z anonimowego obiektu, który przekazujemy.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

Po tym wywołaniu formuła w `B2` staje się:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

Gdy skoroszyt zostanie obliczony, `B2` wyświetla **90**, czyli 10 % rabatu zastosowanego do pierwotnej ceny 100.

**Dlaczego to działa:** `StartSmartMarkerProcessing` przegląda każdą komórkę, szuka tokenu `#Discount#` i podmienia go na wartość liczbową. Ponieważ token znajduje się wewnątrz instrukcji `IF`, arkusz nadal obsługuje przypadki, gdy rabat może wynosić zero.

## Krok 4: Zastosuj Rabat w Arkuszu – Zweryfikuj Wynik

Uruchommy obliczenia i wypiszmy ostateczną cenę na konsolę. Ten krok dowodzi, że przepływ **apply discount in spreadsheet** zakończył się sukcesem.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Oczekiwany wynik**

```
Original: 100
Discounted (10%): 90
```

Jeśli zmienisz `discountData.Discount` na `0.25` i ponownie uruchomisz procesor, wynik automatycznie odzwierciedli 25 % rabatu — bez dodatkowego kodu.

## Krok 5: Obsługa Przypadków Brzegowych i Wielokrotnych Rabatów

### Wiersze Bez Rabatu

Czasami produkt nie jest w promocji. Aby formuła była odporna, `IF` umieszczony wcześniej już obejmuje ten scenariusz: gdy `#Discount#` wynosi `0`, pierwotna cena przechodzi niezmieniona.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Wielokrotne Kolumny Rabatów

Jeśli potrzebujesz oddzielnych rabatów dla każdego wiersza, nadaj każdemu wierszowi własny znacznik, np. `#Discount1#`, `#Discount2#`, i przekaż kolekcję:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

Procesor dopasowuje znaczniki kolejno, więc każdy wiersz otrzymuje właściwą wartość.

## Pełny Działający Przykład

Poniżej znajduje się kompletny, gotowy do skopiowania program, który zawiera wszystkie powyższe kroki. Zapisz go jako `Program.cs`, dodaj odwołanie do `Aspose.Cells` i uruchom.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

Uruchomienie tego wypisze oczekiwane liczby i wygeneruje plik `DiscountedPricing.xlsx`, który możesz otworzyć w Excelu, aby zobaczyć już rozwiązane formuły.

## Zakończenie

Teraz wiesz, jak **create discount template**, **apply discount in spreadsheet**, **inject data into template** i **define variable prefix** dla smart markers — wszystko przy użyciu kilku zwięzłych linii C#. Wzorzec jest skalowalny — wystarczy zmienić anonimowy obiekt lub przekazać kolekcję do masowych aktualizacji, a ten sam szablon poradzi sobie z każdym scenariuszem rabatu, który mu przedstawisz.

Gotowy na kolejny poziom? Spróbuj:

- Dodawanie obliczeń podatku wraz z rabatami.
- Pobieranie procentów rabatu z bazy danych zamiast ich zakodowania na stałe.
- Używanie formatowania warunkowego do podświetlania wierszy z wysokimi rabatami.

Te rozszerzenia zachowują podstawową koncepcję, jednocześnie zwiększając użyteczność twojego szablonu rabatu.

Masz pytania lub ciekawy przypadek użycia? zostaw komentarz poniżej i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}