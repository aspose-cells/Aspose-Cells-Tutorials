---
category: general
date: 2026-06-27
description: Jak formatować kolumny w Excelu w C# z naprzemiennymi kolorami. Dowiedz
  się, jak tworzyć skoroszyt Excel w C#, importować DataTable do Excela i eksportować
  jako .xlsx.
draft: false
keywords:
- how to format excel columns
- create excel workbook c#
- import datatable to excel
- apply alternating column colors
- export datatable as xlsx
language: pl
og_description: Jak formatować kolumny Excela w C# z naprzemiennymi kolorami. Postępuj
  zgodnie z tym samouczkiem krok po kroku, aby stworzyć skoroszyt Excela w C#, zaimportować
  DataTable i wyeksportować jako .xlsx.
og_title: Jak formatować kolumny Excela w C# – Kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to format Excel columns in C# with alternating colors. Learn to
    create Excel workbook C#, import DataTable to Excel, and export as .xlsx.
  headline: How to Format Excel Columns in C# – Complete Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: Jak formatować kolumny Excela w C# – Kompletny przewodnik
url: /pl/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak formatować kolumny w Excelu w C# – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak formatować kolumny w Excelu** w C# bez tracenia włosów? Nie jesteś sam. Niezależnie od tego, czy generujesz raport sprzedaży, czy zrzucasz dump bazy danych do arkusza, uporządkowane kolumny mogą zrobić różnicę między „meh” a „wow”.

W tym tutorialu przejdziemy przez **kompletny, gotowy do uruchomienia przykład**, który pokaże Ci, jak **utworzyć skoroszyt Excel w C#**, **zaimportować DataTable do Excela** oraz **zastosować naprzemienne kolory kolumn**, aby każda kolumna wyróżniała się. Na koniec dowiesz się, jak **wyeksportować DataTable jako xlsx** jedną linijką kodu. Bez zbędnego gadania, tylko praktyczny kod, który możesz skopiować‑wkleić.

> **Czego będziesz potrzebować**  
> - .NET 6 lub nowszy (dowolna aktualna wersja)  
> - Pakiet NuGet **Aspose.Cells** (lub inny podobny) – użyjemy go, ponieważ jest czystym C# i nie wymaga zainstalowanego Excela.  
> - Proste źródło `DataTable` – wygenerujemy je „na żywo” na potrzeby demonstracji.

Zanurzmy się.

![How to format Excel columns in C# example](excel-columns.png "How to format Excel columns in C#")

## Krok 1: Utwórz skoroszyt Excel w C#  

Pierwszą rzeczą, którą musisz zrobić, jest uruchomienie nowego skoroszytu. Pomyśl o tym jak o otwarciu zupełnie nowego notesu, w którym później zapiszesz dane.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class ExcelDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – this is the container for all sheets.
        Workbook workbook = new Workbook();

        // 2️⃣ Grab the first worksheet (index 0) – it’s already there.
        Worksheet worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this sheet with data and styling.
        // …
    }
}
```

**Dlaczego to ważne:** `Workbook` jest punktem wejścia dla każdej operacji na Excelu. Utworzenie go **tworzy excel workbook c#** – nie potrzebujesz żadnego COM interopu, a obiekt istnieje wyłącznie w pamięci, dopóki nie zdecydujesz się go zapisać.

> **Pro tip:** Jeśli tworzysz aplikację serwerową, wybierz bibliotekę, która nie wymaga zainstalowanego Microsoft Office. Aspose.Cells, EPPlus lub ClosedXML spełniają to kryterium.

## Krok 2: Przygotuj style – zastosuj naprzemienne kolory kolumn  

Teraz przychodzi zabawna część: nadanie co drugiej kolumnie innego odcienia. Ten wizualny sygnał pomaga czytelnikom szybciej przeglądać duże tabele.

```csharp
// Assume we already have a DataTable called dataTable (we’ll create it later).
int columnCount = dataTable.Columns.Count;

// Create an array to hold a style per column.
Style[] columnStyles = new Style[columnCount];

for (int i = 0; i < columnCount; i++)
{
    // Each column gets its own Style object.
    columnStyles[i] = workbook.CreateStyle();

    // Alternate between blue and green fonts.
    columnStyles[i].Font.Color = (i % 2 == 0) ? Color.Blue : Color.Green;

    // Optional: make the header bold for extra clarity.
    if (i == 0) // just an example, you could set this for all headers.
        columnStyles[i].Font.IsBold = true;
}
```

**Co się dzieje?**  
- `workbook.CreateStyle()` daje nam czyste płótno dla każdej kolumny.  
- Operator trójargumentowy `(i % 2 == 0) ? Color.Blue : Color.Green` jest sercem **apply alternating column colors** – kolumny o parzystych indeksach stają się niebieskie, nieparzyste zielone.  
- Ten blok możesz rozbudować, aby ustawić wypełnienia tła, obramowania lub formaty liczb, nie zmieniając reszty kodu.

> **Edge case:** Jeśli Twoja tabela ma więcej niż kilkadziesiąt kolumn, tworzenie stylu dla każdej z nich może pochłonąć pamięć. W takim scenariuszu użyj dwóch obiektów stylu (blueStyle, greenStyle) i przypisuj je w zależności od indeksu kolumny.

## Krok 3: Zbuduj przykładowy DataTable (lub użyj własnego)  

Dla samodzielnego demo wygenerujemy `DataTable` z kilkoma wierszami. W prawdziwych projektach zamienisz `GetSampleData()` na własną logikę pobierania danych.

```csharp
static DataTable GetSampleData()
{
    DataTable dt = new DataTable();

    // Define columns.
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));
    dt.Columns.Add("Date", typeof(DateTime));

    // Populate rows.
    for (int i = 1; i <= 5; i++)
    {
        dt.Rows.Add(i, $"Student {i}", 75 + i * 2, DateTime.Today.AddDays(-i));
    }

    return dt;
}
```

Teraz podłącz to do naszego głównego przepływu:

```csharp
DataTable dataTable = GetSampleData();   // <-- import datatable to excel
```

## Krok 4: Zaimportuj DataTable do arkusza z zastosowaniem stylów  

Aspose.Cells umożliwia import jedną linijką. Przeciążenie, którego używamy, pozwala przekazać tablicę stylów, którą zbudowaliśmy wcześniej.

```csharp
// 0️⃣ Row and column offsets – start at A1 (0,0).
int startRow = 0;
int startColumn = 0;

// The 'true' flag tells the method that the first row in the DataTable
// contains column headers, which will be written to the sheet.
worksheet.Cells.ImportDataTable(dataTable, true, startRow, startColumn, columnStyles);
```

**Dlaczego warto używać tego przeciążenia?**  
- Respektuje wiersz nagłówka, więc nie musisz ręcznie wpisywać nazw kolumn.  
- Stosuje tablicę **columnStyles** kolumna po kolumnie, dając nam naprzemienne kolory bez dodatkowych pętli.  
- Jest szybkie – cała tabela trafia do pamięci w jednym wywołaniu.

## Krok 5: Zapisz skoroszyt – wyeksportuj DataTable jako .xlsx  

Na koniec zapisujemy skoroszyt na dysku. To właśnie miejsce, w którym zachodzi **export datatable as xlsx**.

```csharp
// Choose a folder that exists on your machine.
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");

// Save in the modern Office Open XML format.
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to: {outputPath}");
```

Po otwarciu `output.xlsx` zobaczysz:

| **ID** | **Name**      | **Score** | **Date**    |
|--------|---------------|-----------|-------------|
| *1* (niebieski) | *Student 1* (zielony) | *77* (niebieski) | *2026‑06‑26* (zielony) |
| *2* (zielony) | *Student 2* (niebieski) | *79* (zielony) | *2026‑06‑25* (niebieski) |
| …      | …             | …         | …           |

*Kolory czcionki (niebieski i zielony) naprzemiennie zmieniają się w każdej kolumnie, dokładnie tak, jak zaprogramowaliśmy.*

## Krok 6: Typowe pułapki i jak ich unikać  

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| **Style nie są stosowane** | Przekazanie `null` lub tablicy o niepasującej długości do `ImportDataTable`. | Upewnij się, że `columnStyles.Length == dataTable.Columns.Count`. |
| **Plik zablokowany po zapisie** | Inny proces (np. Excel) ma otwarty plik. | Zamknij wszystkie przeglądarki przed uruchomieniem, albo zapisz do ścieżki tymczasowej i przenieś plik później. |
| **Wzrost pamięci przy ogromnych tabelach** | Tworzenie stylu dla każdej kolumny przy tysiącach kolumn. | Ponownie używaj dwóch obiektów stylu i przypisuj je w zależności od `(col % 2)`. |
| **Niepoprawny format daty** | Excel interpretuje `DateTime` jako liczbę. | Ustaw `columnStyles[i].Number = 14; // wbudowany format daty` dla kolumn z datami. |

## Krok 7: Co dalej – wyjście poza proste formatowanie  

Teraz, gdy opanowałeś **jak formatować kolumny w Excelu** przy użyciu naprzemiennych czcionek, możesz eksperymentować z:

- **Conditional formatting** – podświetlanie komórek spełniających reguły biznesowe.  
- **Table objects** – przekształcenie zakresu w tabelę Excela z automatycznymi filtrami.  
- **Chart generation** – wizualizacja danych bezpośrednio z skoroszytu.  
- **Streaming dużych eksportów** – użycie `SaveOptions`, aby zapisywać ogromne pliki bez ładowania wszystkiego do RAM.

Wszystko to opiera się na tych samych podstawowych koncepcjach, które omówiliśmy: tworzenie skoroszytu, stylowanie komórek, import danych i zapis.

---

### Zakończenie  

Właśnie nauczyłeś się **jak formatować kolumny w Excelu** w C# od początku do końca: utworzyć skoroszyt Excel w C#, zastosować naprzemienne kolory kolumn, zaimportować DataTable do Excela i w końcu wyeksportować DataTable jako plik .xlsx. Pełny, gotowy do skopiowania kod powyżej działa od razu, a wyjaśnienia odpowiadają na pytanie „dlaczego” stojące za każdą linijką.

Śmiało modyfikuj kolory, dodawaj obramowania lub przełącz się na inną bibliotekę, jeśli wolisz. Wzorzec pozostaje ten sam, a rezultat zawsze będzie czystym, profesjonalnym arkuszem gotowym dla interesariuszy.

Masz pytania lub chcesz podzielić się własnymi trikami stylizacji? zostaw komentarz poniżej i kontynuujmy dyskusję. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Style Excel Tables Using Aspose.Cells for .NET | Step‑By‑Step Guide](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}