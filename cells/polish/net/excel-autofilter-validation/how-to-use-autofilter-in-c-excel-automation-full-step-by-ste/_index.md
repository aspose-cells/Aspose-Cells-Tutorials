---
category: general
date: 2026-05-30
description: Jak używać AutoFilter w automatyzacji Excela w C#. Dowiedz się, jak utworzyć
  skoroszyt Excela, filtrować wiersze według wartości i usprawnić swoje zadania w
  arkuszu kalkulacyjnym.
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: pl
og_description: Jak używać AutoFilter w automatyzacji Excel w C#. Opanuj tworzenie
  skoroszytu Excel, filtrowanie wierszy według wartości oraz automatyzację arkuszy
  kalkulacyjnych z łatwością.
og_title: Jak używać AutoFilter w automatyzacji Excel w C# – kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: Jak używać AutoFilter w automatyzacji Excela w C# – pełny przewodnik krok po
  kroku
url: /pl/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać AutoFilter w automatyzacji Excel w C# – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak używać AutoFilter**, gdy generujesz pliki Excel z kodu C#? Nie jesteś sam — wielu programistów napotyka ten problem, gdy muszą ukryć wiersze nie spełniające określonego kryterium.  

W tym tutorialu przejdziemy przez konkretny, gotowy do uruchomienia przykład, który **tworzy skoroszyt Excel**, dodaje tabelę i **filtruje wiersze według wartości** w kolumnie B. Na końcu będziesz mieć czysty, wielokrotnego użytku fragment kodu, który możesz wstawić do dowolnego projektu C# wymagającego automatyzacji Excel.

## Czego się nauczysz

- Konfiguracja projektu C# z biblioteką Aspose.Cells (lub Microsoft.Office.Interop).  
- **Tworzenie skoroszytu Excel** programowo i dodawanie stylizowanej tabeli.  
- Zastosowanie **AutoFilter**, aby wyświetlać tylko wiersze, w których **kolumna B** równa się określonemu ciągowi znaków.  
- Całkowite usunięcie filtru, przywracając pełny zestaw danych.  
- Wskazówki dotyczące obsługi przypadków brzegowych, takich jak brakujące kolumny czy wiele kryteriów filtracji.

Nie wymagana jest wcześniejsza znajomość VBA w Excelu; wystarczy podstawowa znajomość C# i pakietów NuGet.

---

## Wymagania wstępne

| Wymaganie | Dlaczego jest ważne |
|-----------|----------------------|
| .NET 6.0 lub nowszy (lub .NET Framework 4.7+) | Nowoczesne środowiska uruchomieniowe zapewniają lepszą wydajność i łatwiejsze zarządzanie pakietami. |
| Aspose.Cells for .NET (lub Microsoft.Office.Interop.Excel) zainstalowane przez NuGet | Biblioteka dostarcza obiekty `Workbook`, `Worksheet` i `Table` używane w kodzie. |
| Edytor kodu (Visual Studio, VS Code, Rider itp.) | Będziesz musiał skompilować i uruchomić przykład. |
| Podstawowa znajomość C# | Tutorial wyjaśnia *dlaczego* każda linia istnieje, a nie tylko *co* robi. |

Aspose.Cells możesz zainstalować za pomocą:

```bash
dotnet add package Aspose.Cells
```

---

## Jak używać AutoFilter z Aspose.Cells w C#

Poniżej znajduje się pełny, samodzielny program. Zapisz go jako `Program.cs` w projekcie konsolowym i uruchom — w folderze wyjściowym pojawi się plik `FilteredWorkbook.xlsx`.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### Jak działa kod

1. **Tworzenie skoroszytu** – `new Workbook()` tworzy pusty plik; `Worksheets[0]` pobiera domyślny arkusz.  
2. **Wypełnianie przykładowymi danymi** – Wpisujemy mały zestaw danych, aby można było zobaczyć filtr w akcji.  
3. **Dodawanie tabeli** – `ListObjects.Add` zamienia zakres w tabelę Excel, która automatycznie obsługuje filtrowanie i stylizację.  
4. **Zastosowanie AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` mówi silnikowi: „Pokaż tylko wiersze, w których druga kolumna (B) równa się *Apple*.”  
5. **Zapisywanie plików** – Zapisane są dwa pliki: jeden przefiltrowany, drugi z usuniętym filtrem, co dowodzi, że `RemoveAutoFilter()` działa zgodnie z oczekiwaniami.

> **Pro tip:** Jeśli potrzebujesz filtrować po wielu kryteriach (np. „Apple” *lub* „Banana”), użyj przeciążenia `Filter(int columnIndex, string criteria1, string criteria2)` lub przekaż tablicę ciągów znaków.

---

## Filtrowanie wierszy według wartości – Typowe warianty

Choć powyższy przykład koncentruje się na **filtrze kolumny B**, możesz chcieć filtrować inne kolumny lub używać kryteriów liczbowych. Oto szybka karta pomocy:

| Żądany filtr | Fragment kodu |
|--------------|---------------|
| Dopasowanie tekstu w kolumnie C | `table.AutoFilter.Filter(2, "Cherry");` |
| Liczby większe niż 10 w kolumnie C | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| Wiele wartości w kolumnie B | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**Przypadek brzegowy:** Jeśli nagłówek kolumny jest literówką lub indeks kolumny jest poza zakresem, Aspose.Cells zgłosi `ArgumentException`. Zapobiegaj temu, sprawdzając `table.ListColumns.Count` przed zastosowaniem filtru.

---

## Usuwanie AutoFilter – Kiedy zresetować

Czasami trzeba ponownie wyświetlić pełny zestaw danych (np. po wyczyszczeniu pola wyszukiwania przez użytkownika). Wywołanie `table.RemoveAutoFilter()` rozwiązuje problem w jednej linii. Jeśli używasz Microsoft.Office.Interop, wywołujesz `worksheet.AutoFilterMode = false;`.

---

## Pełny działający przykład – podsumowanie

Poniżej ponownie cały program, bez komentarzy, dla tych, którzy wolą zwięzły widok:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

Uruchomienie tego kodu wygeneruje dwa pliki:

- **FilteredWorkbook.xlsx** – widoczne tylko wiersze z *Apple*.  
- **UnfilteredWorkbook.xlsx** – przywrócone oryginalne dane.

---

## Najczęściej zadawane pytania

**P: Czy to działa ze starszymi plikami .xls?**  
O: Tak. Aspose.Cells może zapisywać zarówno do `.xlsx`, jak i `.xls`, zmieniając rozszerzenie pliku lub używając `SaveOptions`.

**P: Co zrobić, jeśli muszę filtrować *po* zapisaniu skoroszytu?**  
O: Wczytaj plik za pomocą `new Workbook("ścieżka.xlsx")`, zastosuj filtr, a następnie ponownie `Save`.

**P: Czy mogę zastosować filtr do *zakresu*, który nie jest tabelą?**  
O: Oczywiście. Użyj `worksheet.AutoFilter.Range = "A1:C5";`, a potem `worksheet.AutoFilter.ApplyFilter();`. Jednak tabele zapewniają wbudowaną stylizację i łatwiejsze odwoływanie się do kolumn.

---

## Obraz – wizualne potwierdzenie

![Zrzut ekranu pokazujący zastosowany AutoFilter w kolumnie B w skoroszycie Excel utworzonym w C#](/images/autofilter-column-b.png "AutoFilter w kolumnie B")

*(Obraz ilustruje przefiltrowany widok, w którym pozostają tylko wiersze zawierające „Apple”.)*

---

## Zakończenie

Właśnie omówiliśmy **jak używać AutoFilter** w scenariuszu automatyzacji Excel z C#, od **tworzenia skoroszytu Excel** po **filtrowanie wierszy według wartości** w **kolumnie B**, a na końcu **usuwanie filtru**, gdy nie jest już potrzebny. Podstawowe kroki — inicjalizacja, dodanie tabeli, zastosowanie filtru i sprzątanie — są wielokrotnego użytku w każdym projekcie wymagającym **excel automation c#**.

Gotowy na kolejny wyzwanie? Spróbuj:

- Dodać formatowanie warunkowe, aby podświetlić przefiltrowane wiersze.  
- Eksportować przefiltrowane dane do CSV w celu dalszego przetwarzania.  
- Połączyć wiele filtrów (np. „Apple” *i* ilość > 8).

Eksperymentuj, łam rzeczy, a potem je naprawiaj—

## Co powinieneś nauczyć się dalej?

- [Jak zaimplementować AutoFilter w Excel przy użyciu Aspose.Cells dla .NET (Przewodnik analizy danych)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [Jak używać Autofilter Not Contains w Aspose.Cells .NET dla analizy danych w Excel](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [Jak zaimplementować Excel Autofilter 'EndsWith' przy użyciu Aspose.Cells dla .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}