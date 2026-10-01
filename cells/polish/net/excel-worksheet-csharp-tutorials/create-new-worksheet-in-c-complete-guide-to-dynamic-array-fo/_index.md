---
category: general
date: 2026-05-23
description: Utwórz nowy arkusz w C# z instrukcją krok po kroku. Dowiedz się, jak
  stworzyć skoroszyt, używać formuły dynamicznej tablicy, eksportować posortowane
  dane i zapisać skoroszyt.
draft: false
keywords:
- create new worksheet
- how to create workbook
- how to save workbook
- export sorted data
- dynamic array formula
language: pl
og_description: Utwórz nowy arkusz w C# przy użyciu Aspose.Cells. Ten przewodnik pokazuje,
  jak stworzyć skoroszyt, zastosować dynamiczną formułę tablicową, wyeksportować posortowane
  dane i zapisać skoroszyt.
og_title: Utwórz nowy arkusz w C# – pełny przewodnik programistyczny
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create new worksheet in C# with a step‑by‑step tutorial. Learn how
    to create workbook, use a dynamic array formula, export sorted data and save workbook.
  headline: Create New Worksheet in C# – Complete Guide to Dynamic Array Formulas
  type: TechArticle
- questions:
  - answer: The file will open, but the `SORT` formula will appear as text and show
      a `#NAME?` error. For backward compatibility, generate the sorted list in code
      and write the values directly.
    question: Does this work on older Excel versions that don’t support dynamic arrays?
  - answer: Absolutely. Use `=SORT(A2:C10, {1,2}, {1,-1})` where the second argument
      specifies the column indices and the third the sort order.
    question: Can I sort by multiple columns?
  - answer: 'After saving the workbook, load it again and call `worksheet.Cells.ExportDataTableAsString`
      or use `CsvSaveOptions` if your library provides one. --- ## Next Steps - **Explore
      other dynamic array functions** such as `FILTER`, `UNIQUE`, and `SEQUENCE`.
      - **Automate chart creation** on the same worksh'
    question: What if I need to export the sorted data to CSV?
  type: FAQPage
tags:
- C#
- Excel Automation
- Aspose.Cells
- Spreadsheet
title: Utwórz nowy arkusz w C# – Kompletny przewodnik po dynamicznych formułach tablicowych
url: /pl/net/excel-worksheet-csharp-tutorials/create-new-worksheet-in-c-complete-guide-to-dynamic-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie nowego arkusza w C# – Kompletny przewodnik po dynamicznych formułach tablicowych

Zastanawiałeś się kiedyś, jak **utworzyć nowy arkusz** w C# bez ręcznego otwierania Excela? Nie jesteś sam. Wielu programistów musi generować raporty, sortować dane w locie i udostępniać wynik jako plik .xlsx – wszystko z poziomu kodu.  

W tym tutorialu przejdziemy krok po kroku przez to właśnie: pokażemy **jak utworzyć skoroszyt**, wstawimy **dynamiczną formułę tablicową** do zupełnie nowego arkusza, **wyeksportujemy posortowane dane**, a na koniec **zapiszemy skoroszyt**, aby móc go udostępnić. Bez zbędnych wstępów, tylko solidny, gotowy do uruchomienia przykład, który możesz skopiować i wkleić już dziś.

## Czego się nauczysz

- Wymagania wstępne do użycia Aspose.Cells (lub dowolnej porównywalnej biblioteki .NET do Excela).  
- Jak **utworzyć nowy arkusz**, zapisać formułę `SORT` i pozwolić Excelowi automatycznie rozlać wynik.  
- Wskazówki dotyczące obsługi przypadków brzegowych, takich jak puste zakresy źródłowe czy duże zestawy danych.  
- Jak **wyeksportować posortowane dane** do nowego pliku i zweryfikować wynik.  
- Krótkie spojrzenie na alternatywne podejścia, jeśli wolisz `OpenXML` lub `EPPlus`.  

Po zakończeniu tego przewodnika będziesz mieć samodzielny program, który generuje posortowaną listę w nowym arkuszu, gotową do dalszego przetwarzania.

---

## Krok 1: Konfiguracja projektu – Jak utworzyć skoroszyt

Najpierw przygotujmy środowisko. Skorzystamy z **Aspose.Cells for .NET**, ponieważ obsługuje pełny silnik obliczeniowy Excela, w tym najnowsze **dynamiczne formuły tablicowe** takie jak `SORT`. Jeśli używasz innej biblioteki, koncepcje pozostają takie same – wystarczy zamienić przestrzeń nazw.

```csharp
// Add the Aspose.Cells NuGet package
//   dotnet add package Aspose.Cells
using Aspose.Cells;

namespace WorksheetDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or load an existing one)
            Workbook workbook = new Workbook();   // <-- this is how we **how to create workbook**
```

**Dlaczego to ważne:**  
Utworzenie obiektu `Workbook` uruchamia w pamięci reprezentację pliku Excel. Bez COM interop, bez wymogu instalacji Excela. Dzięki temu rozwiązanie jest przenośne na Windows, Linux i kontenery Docker.

> **Pro tip:** Jeśli masz już plik szablonu, przekaż jego ścieżkę do `new Workbook("template.xlsx")` zamiast zaczynać od zera.

---

## Krok 2: Dodaj nowy arkusz – Create New Worksheet

Mając już skoroszyt, potrzebujemy miejsca na nasze dane. Domyślnie Aspose tworzy pojedynczy arkusz o nazwie „Sheet1”. Dodamy kolejny, aby przykład był przejrzysty.

```csharp
            // Step 2: Add a new worksheet to hold the sorted output
            int newSheetIndex = workbook.Worksheets.Add();
            Worksheet sheet = workbook.Worksheets[newSheetIndex];   // <-- **create new worksheet**
```

**Co się dzieje w tle?**  
`Worksheets.Add()` zwraca indeks (zerowy) nowo dodanego arkusza. Następnie pobieramy obiekt `Worksheet`, aby móc bezpośrednio manipulować komórkami.

> **Uwaga:** Jeśli wywołujesz `Add()` wielokrotnie bez przechowywania indeksu, możesz stracić kontrolę, do którego arkusza zapisujesz. Zawsze zachowuj referencję.

---

## Krok 3: Wstaw przykładowe dane (opcjonalnie)

Aby formuła `SORT` miała na czym działać, potrzebujemy zakresu źródłowego. Wypełnijmy `A2:A6` kilkoma nieposortowanymi wartościami.

```csharp
            // Populate source data (A2:A6) – this mimics a raw data table
            string[] rawValues = { "Delta", "Alpha", "Echo", "Bravo", "Charlie" };
            for (int i = 0; i < rawValues.Length; i++)
            {
                sheet.Cells[i + 1, 0].PutValue(rawValues[i]); // Row i+1, Column 0 (A column)
            }
```

Dlaczego dane umieszczamy w *tym samym* arkuszu? Ponieważ funkcja `SORT` może odwoływać się do zakresu w tym samym arkuszu; dzięki temu demo jest kompaktowe. W rzeczywistych scenariuszach możesz odczytywać dane z bazy, pliku CSV lub innego arkusza.

---

## Krok 4: Zapisz dynamiczną formułę tablicową – Export Sorted Data

Oto serce tutorialu: wstawimy **dynamiczną formułę tablicową**, która automatycznie rozleje posortowaną listę do sąsiednich komórek.

```csharp
            // Step 4: Write a SORT formula into cell A1 (row 0, column 0)
            sheet.Cells[0, 0].Formula = "=SORT(A2:A6)";   // <-- **dynamic array formula**
```

Gdy Excel oceni `=SORT(A2:A6)`, zwróci pionową tablicę wartości w kolejności alfabetycznej. Dzięki zachowaniu spill wprowadzonego w Excel 365, wyniki automatycznie zajmą zakres `A1:A5`.

> **Częste pytanie:** *Co jeśli zakres źródłowy jest pusty?*  
> Formuła zwróci błąd `#SPILL!`. Zabezpiecz się, sprawdzając `rawValues.Length` przed zapisaniem formuły lub owiń ją w `IFERROR(SORT(...), "")`.

---

## Krok 5: Wymuś obliczenia – Niech formuła się wykona

Aspose.Cells nie przelicza formuł automatycznie po ich ustawieniu, więc musimy nakazać silnikowi wykonanie obliczeń.

```csharp
            // Recalculate the workbook so the spill range is populated
            workbook.CalculateFormula();   // <-- triggers **export sorted data**
```

**Co się dzieje w tle:** Silnik obliczeniowy parsuje drzewo formuły, rozwiązuje odwołania do komórek i zapisuje wynikową tablicę z powrotem do arkusza. Ten krok jest niezbędny; w przeciwnym razie w pliku zobaczysz surowy tekst `=SORT(A2:A6)`.

---

## Krok 6: Zapisz plik – How to Save Workbook

Na koniec zapisujemy skoroszyt na dysku. Wybierz dowolny folder, ale upewnij się, że proces ma prawo zapisu.

```csharp
            // Step 6: Save the workbook to view the result
            string outputPath = @"YOUR_DIRECTORY\sorted_output.xlsx";
            workbook.Save(outputPath);   // <-- **how to save workbook**
            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Dlaczego używamy `Save` zamiast `SaveCopyAs`?**  
`Save` nadpisuje docelowy plik, co jest w porządku przy jednorazowym eksporcie. Jeśli potrzebujesz zachować oryginał, najpierw wywołaj `workbook.SaveCopyAs("backup.xlsx")`.

---

## Pełny działający przykład

Łącząc wszystkie elementy, oto kompletny program, który możesz skompilować od razu:

```csharp
using Aspose.Cells;
using System;

namespace WorksheetDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Add a fresh worksheet
            int sheetIdx = workbook.Worksheets.Add();
            Worksheet sheet = workbook.Worksheets[sheetIdx];

            // 3️⃣ Seed unsorted data (A2:A6)
            string[] values = { "Delta", "Alpha", "Echo", "Bravo", "Charlie" };
            for (int i = 0; i < values.Length; i++)
                sheet.Cells[i + 1, 0].PutValue(values[i]);

            // 4️⃣ Insert the SORT dynamic array formula in A1
            sheet.Cells[0, 0].Formula = "=SORT(A2:A6)";

            // 5️⃣ Calculate so the spill range fills
            workbook.CalculateFormula();

            // 6️⃣ Save the workbook
            string outFile = @"C:\Temp\sorted_output.xlsx";
            workbook.Save(outFile);
            Console.WriteLine($"✅ Workbook saved – open {outFile} to see the sorted list.");
        }
    }
}
```

### Oczekiwany wynik

Po otwarciu `sorted_output.xlsx` komórka **A1** będzie zawierała „Alpha”, **A2** „Bravo”, **A3** „Charlie”, **A4** „Delta”, a **A5** „Echo”. Nieposortowana lista pozostaje w **A2:A6** (zakres źródłowy), co dowodzi, że **dynamiczna formuła tablicowa** poprawnie wyeksportowała posortowane dane.

---

## Obsługa przypadków brzegowych i wariantów

| Sytuacja | Co zrobić |
|-----------|------------|
| **Zakres źródłowy większy niż 1 048 576 wierszy** | Ograniczenie liczby wierszy Excela obowiązuje; podziel dane na kilka arkuszy lub użyj bazy danych do dużych obciążeń. |
| **Mieszane typy danych (liczby + tekst)** | `SORT` domyślnie umieszcza liczby przed tekstem. Użyj `SORTBY` z własnym kluczem sortowania, jeśli potrzebujesz innej kolejności. |
| **Potrzebujesz statycznego zakresu posortowanych wartości** | Po obliczeniu skopiuj zakres spill i wklej tylko wartości (`PasteSpecial`), a następnie usuń formułę. |
| **Używasz OpenXML/EPPlus zamiast Aspose** | Kroki są identyczne; zamień `Workbook`/`Worksheet` na odpowiedniki biblioteki i wywołaj `Package.Save()`. |

---

## Najczęściej zadawane pytania

**P: Czy to działa w starszych wersjach Excela, które nie obsługują dynamicznych tablic?**  
O: Plik otworzy się, ale formuła `SORT` pojawi się jako tekst i wyświetli błąd `#NAME?`. Dla kompatybilności wstecznej wygeneruj posortowaną listę w kodzie i zapisz wartości bezpośrednio.

**P: Czy mogę sortować po kilku kolumnach?**  
O: Oczywiście. Użyj `=SORT(A2:C10, {1,2}, {1,-1})`, gdzie drugi argument określa indeksy kolumn, a trzeci kolejność sortowania.

**P: Co zrobić, jeśli muszę wyeksportować posortowane dane do CSV?**  
O: Po zapisaniu skoroszytu wczytaj go ponownie i wywołaj `worksheet.Cells.ExportDataTableAsString` lub użyj `CsvSaveOptions`, jeśli twoja biblioteka taką opcję oferuje.

---

## Kolejne kroki

- **Poznaj inne dynamiczne funkcje tablicowe** takie jak `FILTER`, `UNIQUE` i `SEQUENCE`.  
- **Zautomatyzuj tworzenie wykresów** w tym samym arkuszu, aby wizualizować posortowane wyniki.  
- **Zintegruj z ASP.NET Core**, aby użytkownicy mogli pobierać wygenerowany plik bezpośrednio z API webowego.  

Każdy z tych tematów opiera się na fundamentach omówionych tutaj – tworzeniu skoroszytu, dodawaniu arkusza, stosowaniu formuł i zapisywaniu pliku.

---

## Zakończenie

Pokazaliśmy, jak **utworzyć nowy arkusz** w C#, wstawić **dynamiczną formułę tablicową**, **wyeksportować posortowane dane** i w końcu **zapisz skoroszyt**. Podejście jest proste, wymaga tylko kilku linii kodu i działa niezawodnie na różnych platformach.  

Wypróbuj, zmodyfikuj zakres źródłowy, zamień `SORT` na `FILTER` lub podłącz wynik do usługi raportowej. Gdy opanujesz podstawy programowego manipulowania Excelem, możliwości są nieograniczone.

Powodzenia w kodowaniu i niech twoje arkusze zawsze będą posortowane!

## Powiązane tutoriale

- [Jak utworzyć i zapisać skoroszyt Excel jako ODS przy użyciu Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Utwórz i zapisz skoroszyt Excel jako PDF w ASP.NET przy użyciu Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Jak utworzyć i stylizować tabele Excel przy użyciu Aspose.Cells for .NET | Przewodnik krok po kroku](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}