---
category: general
date: 2026-04-07
description: Zastosuj własny format liczbowy do komórki arkusza kalkulacyjnego i dowiedz
  się, jak formatować liczbę w arkuszu przy eksportowaniu wartości komórki w C#. Szybki,
  kompletny przewodnik.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: pl
og_description: Zastosuj niestandardowy format liczby do komórki arkusza kalkulacyjnego
  i wyeksportuj ją jako sformatowany ciąg znaków. Dowiedz się, jak formatować liczby
  w arkuszu kalkulacyjnym i eksportować wartość komórki.
og_title: Zastosuj własny format liczby – Kompletny samouczek eksportu w C#
tags:
- C#
- Spreadsheet
- Number Formatting
title: Zastosuj niestandardowy format liczbowy w eksporcie arkusza kalkulacyjnego
  C# – Przewodnik krok po kroku
url: /pl/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zastosuj własny format liczbowy w eksporcie arkusza C# – Kompletny tutorial

Czy kiedykolwiek musiałeś **zastosować własny format liczbowy** do komórki, a potem wyciągnąć sformatowany ciąg znaków z arkusza? Nie jesteś sam. Wielu programistów napotyka problem, gdy zamiast ładnego, zależnego od lokalizacji ciągu otrzymuje surową wartość. W tym przewodniku pokażemy dokładnie, jak formatować liczby w komórkach arkusza oraz jak wyeksportować wartość komórki jako sformatowany ciąg znaków przy użyciu popularnej biblioteki arkuszy w C#.

Po zakończeniu tego tutorialu będziesz w stanie **zastosować własny format liczbowy** do dowolnej komórki numerycznej, wyeksportować wynik przy pomocy `ExportTable` i zobaczyć dokładny wynik, jaki powinien pojawić się w interfejsie użytkownika lub raporcie. Nie potrzebujesz zewnętrznej dokumentacji — wszystko znajduje się tutaj.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa także na .NET Framework 4.7+)
- Odwołanie do biblioteki arkuszy, która udostępnia `Workbook`, `Worksheet` i `ExportTableOptions` (np. **Aspose.Cells** lub **GemBox.Spreadsheet**; przedstawione API odpowiada Aspose.Cells)
- Podstawowa znajomość C# — jeśli potrafisz napisać `Console.WriteLine`, jesteś gotowy

> **Pro tip:** Jeśli używasz innej biblioteki, nazwy właściwości są zazwyczaj podobne (`NumberFormat`, `ExportAsString`). Po prostu dopasuj je odpowiednio.

## Co obejmuje tutorial

1. Tworzenie skoroszytu i wybór pierwszego arkusza.  
2. Wstawienie wartości numerycznej do komórki.  
3. Konfiguracja `ExportTableOptions`, aby **zastosować własny format liczbowy** i zwrócić ciąg znaków.  
4. Eksportowanie komórki i wypisanie sformatowanego wyniku.  
5. Obsługa przypadków brzegowych – co zrobić, gdy komórka zawiera formułę lub wartość null?

Zaczynajmy.

![przykład zastosowania własnego formatu liczbowego](https://example.com/image.png "zastosowanie własnego formatu liczbowego")

## Krok 1 – Utwórz skoroszyt i pobierz pierwszy arkusz

Pierwszą rzeczą, której potrzebujesz, jest obiekt workbook. Myśl o nim jak o pliku Excel, który otwierasz w aplikacji Office. Gdy już go masz, pobierz pierwszy arkusz — większość tutoriali zaczyna właśnie tak, aby przykład był zwięzły.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Dlaczego to ważne:** Świeży skoroszyt daje czystą kartę, zapewniając, że żadne ukryte formatowanie nie zakłóci naszego własnego formatu liczbowego później.

## Krok 2 – Wstaw wartość numeryczną do komórki B2 (komórka, którą wyeksportujemy)

Teraz potrzebujemy czegoś do sformatowania. Komórka **B2** jest wygodnym miejscem — łatwo ją odwołać i jest wystarczająco oddalona od domyślnego rogu A1, aby uniknąć przypadkowych nadpisań.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**Co jeśli wartość jest formułą?**  
Jeśli później zamienisz surową wartość na formułę (np. `=SUM(A1:A10)`), procedura eksportu nadal będzie respektować format liczbowy, który zastosujemy w następnym kroku, ponieważ formatowanie jest przypisane do komórki, a nie do typu wartości.

## Krok 3 – Skonfiguruj opcje eksportu, aby otrzymać wartość jako sformatowany ciąg znaków

Oto serce tutorialu: informujemy bibliotekę, aby **zastosowała własny format liczbowy** podczas eksportu. Ciąg `NumberFormat` używa tego samego wzorca, co kategoria „Niestandardowe” w Excelu.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` zapewnia, że metoda zwróci `string` zamiast surowej liczby typu double.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` odzwierciedla wzorzec Excela: przecinki jako separator tysięcy, dwie cyfry po przecinku oraz nawiasy dla liczb ujemnych.

> **Dlaczego używać własnego formatu?** Gwarantuje to spójność między kulturami (np. separatory liczb w USA vs. Europie) i pozwala wstawić specyficzne dla biznesu formatowanie, takie jak nawiasy księgowe.

## Krok 4 – Eksportuj komórkę przy użyciu skonfigurowanych opcji

Teraz faktycznie pobieramy wartość z arkusza, pozwalając bibliotece wykonać ciężką pracę polegającą na zastosowaniu zdefiniowanego formatu.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Przypadek brzegowy – pusta komórka:** Jeśli `B2` byłaby pusta, `formattedResult` byłby `null`. Możesz zabezpieczyć się przed tym prostym sprawdzeniem null przed wypisaniem.

## Krok 5 – Wyświetl sformatowany ciąg znaków

Na koniec zapisujemy wynik do konsoli. W prawdziwej aplikacji możesz przekazać ten ciąg do PDF, e‑maila lub etykiety UI.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Oczekiwany wynik**

```
1,234.56
```

Jeśli zmienisz surową wartość na `-9876.54`, ten sam format da Ci `(9,876.54)` — dokładnie to, czego wymaga wiele raportów księgowych.

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się kompletny program, który możesz skopiować‑wkleić do nowego projektu konsolowego. Kompiluje się i działa od razu, pod warunkiem, że dodałeś odpowiedni pakiet NuGet dla biblioteki arkuszy.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Szybka kontrola poprawności

- **Czy się kompiluje?** Tak — wystarczy, że odwołasz bibliotekę `Aspose.Cells` (lub równoważną).
- **Czy zadziała w innych kulturach?** Ciąg formatu jest niezależny od kultury; biblioteka respektuje podany wzorzec. Jeśli potrzebujesz separatorów specyficznych dla lokalizacji, możesz przed eksportem dodać obsługę `CultureInfo`.

## Częste pytania i warianty

### Jak **formatować liczbę w arkuszu** używając innego wzorca?

Zastąp ciąg `NumberFormat`. Na przykład, aby wyświetlić procent z jedną cyfrą po przecinku:

```csharp
NumberFormat = "0.0%";
```

### Co zrobić, aby **wyeksportować wartość komórki** jako HTML zamiast zwykłego tekstu?

Większość bibliotek ma przeciążenie przyjmujące typ eksportu. Ustawisz `ExportAsString = true` i dodasz `ExportHtml = true` (lub podobnie). Zasada pozostaje ta sama: definiujesz format, a potem wybierasz reprezentację wyjściową.

### Czy mogę zastosować format do całego zakresu, a nie tylko jednej komórki?

Oczywiście. Możesz przypisać `NumberFormat` do obiektu `Style`, a następnie zastosować ten styl do `Range`. Wywołanie eksportu pozostaje niezmienione; automatycznie pobierze styl.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### Co się stanie, gdy komórka zawiera formułę?

Procedura eksportu najpierw oceni formułę, a potem sformatuje uzyskany wynik liczbowy. Nie potrzeba dodatkowego kodu — wystarczy upewnić się, że wywołano `Calculate`, jeśli wyłączyłeś automatyczne obliczenia.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Podsumowanie

Teraz wiesz, jak **zastosować własny format liczbowy** do komórki arkusza, **formatować liczbę w arkuszu** oraz **wyeksportować wartość komórki** jako gotowy do wyświetlenia ciąg znaków. Zwięzły przykład kodu powyżej obejmuje każdy krok — od tworzenia skoroszytu po ostateczny wynik — więc możesz go od razu wstawić do projektu produkcyjnego.

Gotowy na kolejny wyzwanie? Spróbuj połączyć tę technikę z **formatowaniem komórek liczbowych** dla dat, symboli walut lub formatowania warunkowego. Albo zbadaj eksport wielu komórek jako CSV przy zachowaniu ich własnych formatów. Nie ma granic, a dzięki tym podstawom masz solidne fundamenty.

Miłego kodowania i nie zapominaj eksperymentować — czasem najlepsze odpowiedzi pojawiają się, gdy nieco zmodyfikujesz ciąg formatu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}