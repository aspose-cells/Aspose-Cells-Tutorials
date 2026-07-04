---
category: general
date: 2026-07-03
description: Dowiedz się, jak wyeksportować tabelę Excel do pliku .txt i zapisać tabelę
  Excel w pliku .txt przy użyciu C#. Wyeksportuj dane z Excela jako zwykły tekst z
  pełnym przykładem kodu.
draft: false
keywords:
- how to export excel table
- save excel table to .txt file
- export excel data as plain text
- Aspose.Cells export table
- C# Excel to text
language: pl
og_description: Jak wyeksportować tabelę Excel jako zwykły tekst. Ten przewodnik pokazuje,
  jak wyeksportować dane z Excela jako zwykły tekst i zapisać tabelę Excel w pliku
  .txt przy użyciu Aspose.Cells.
og_title: Jak wyeksportować tabelę Excel – Pełny tutorial C#
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to export Excel table to a .txt file and save Excel table
    to .txt file using C#. Export Excel data as plain text with full code example.
  headline: How to Export Excel Table – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- File I/O
title: Jak wyeksportować tabelę Excel – Kompletny przewodnik krok po kroku
url: /pl/net/excel-data-export-retrieval/how-to-export-excel-table-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyeksportować tabelę Excel – Kompletny przewodnik krok po kroku

Zastanawiałeś się kiedyś **jak wyeksportować tabelę Excel** bez wczytywania całego skoroszytu do pamięci? Nie jesteś sam. W wielu zadaniach automatyzacji system docelowy akceptuje jedynie prosty plik `.txt`, więc musisz **zapisać tabelę Excel do pliku .txt** szybko i niezawodnie.  

W tym tutorialu przejdziemy przez czyste rozwiązanie w C#, które **eksportuje dane z Excela jako zwykły tekst** przy użyciu Aspose.Cells. Po zakończeniu będziesz mieć gotowy do uruchomienia program, zrozumiesz, dlaczego każda linijka ma znaczenie, i zobaczysz, jak dostosować eksport do własnych przypadków brzegowych.

## Czego będziesz potrzebować

- **Aspose.Cells for .NET** (dowolna aktualna wersja, np. 23.12).  
- .NET 6 SDK lub nowszy – kod kompiluje się także z .NET Core.  
- Przykładowy plik `input.xlsx` zawierający przynajmniej jedną tabelę Excel.  
- Edytor tekstu lub IDE (Visual Studio, VS Code, Rider… wybór należy do Ciebie).

Nie są wymagane dodatkowe pakiety NuGet poza Aspose.Cells, a cały proces działa na Windows, Linux i macOS.

## Krok 1: Utworzenie projektu i importy

Najpierw utwórz aplikację konsolową i zaimportuj niezbędne przestrzenie nazw.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the export logic here.
        }
    }
}
```

> **Porada:** Jeśli używasz .NET CLI, uruchom `dotnet new console -n ExcelTableExport`, a następnie `dotnet add package Aspose.Cells` przed wklejeniem powyższego kodu.

## Krok 2: Załadowanie skoroszytu i pobranie pierwszego arkusza

Obiekt workbook reprezentuje cały plik Excel. Załadowanie go raz utrzymuje niskie zużycie pamięci.

```csharp
// Step 2: Load the workbook and get the first worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = wb.Worksheets[0];
```

Dlaczego wybieramy pierwszy arkusz? W wielu generowanych raportach dane znajdują się w pierwszym arkuszu, ale możesz zmienić indeks lub użyć `wb.Worksheets["SheetName"]` dla arkusza o nazwie.

## Krok 3: Pobranie pierwszej tabeli zdefiniowanej w arkuszu

Tabele Excel (ListObjects) dostarczają ustrukturyzowane dane, co czyni eksport przewidywalnym.

```csharp
// Step 3: Retrieve the first table defined on the worksheet
Table tbl = ws.Tables[0];
```

Jeśli Twój skoroszyt zawiera wiele tabel, po prostu iteruj `ws.Tables` lub wybierz po `tbl.Name`.

## Krok 4: Konfiguracja opcji eksportu – eksportuj każdą komórkę jako ciąg znaków

Aspose.Cells pozwala kontrolować format każdej komórki podczas eksportu. Ustawienie `ExportAsString` zapewnia, że liczby, daty i formuły zostaną zamienione na zwykły tekst.

```csharp
// Step 4: Set up export options – export every cell as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true
};
```

### Dodanie własnej akcji eksportu, aby przyciąć białe znaki

Często źródłowe dane zawierają wiodące lub końcowe spacje. Ich usunięcie sprawia, że końcowy plik `.txt` jest czystszy.

```csharp
// Define a custom export action to trim cell values before writing
exportOptions.CustomExport = (cell, writer) =>
{
    writer.Write(cell.StringValue.Trim());
};
```

Lambda otrzymuje obiekt `Cell` oraz `TextWriter`. Możesz tutaj dodać także logikę warunkową — np. zamienić przecinki na średniki dla wyjścia w stylu CSV.

## Krok 5: Eksport tabeli zaczynając od komórki A1 do pliku tekstowego

Teraz faktycznie zapisujemy tabelę na dysk. Metoda `ExportTable` przechodzi przez tabelę wiersz po wierszu, stosując wcześniej zdefiniowane opcje.

```csharp
// Step 5: Export the table starting at cell A1 to a text file
using (StreamWriter writer = new StreamWriter("YOUR_DIRECTORY/Table.txt"))
{
    ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
}
```

**Co zobaczysz:** Każdy wiersz tabeli Excel staje się linią w `Table.txt`. Kolumny są domyślnie oddzielone znakiem tabulacji (`\t`) — idealne do dalszego parsowania.

### Przykład oczekiwanego wyjścia

Zakładając, że `input.xlsx` zawiera tabelę z trzema kolumnami (`ID`, `Name`, `Score`) i dwoma wierszami danych, `Table.txt` będzie wyglądać tak:

```
1    Alice    85
2    Bob      92
```

Zauważ, że spacje zostały przycięte, a wszystko jest zwykłym tekstem — dokładnie to, czego wymaga **export excel data as plain text**.

## Obsługa typowych przypadków brzegowych

| Sytuacja | Co zrobić | Dlaczego |
|-----------|------------|-----|
| **Tabela ma puste komórki** | Lambda zapisuje `cell.StringValue.Trim()`, co zwraca pusty ciąg dla pustych pól. | Utrzymuje wyrównanie kolumn bez dodawania niechcianych znaków. |
| **Potrzebujesz własnego separatora** | Zamień `writer.Write(cell.StringValue.Trim());` na `writer.Write($"{cell.StringValue.Trim()},");` i usuń końcowy separator po każdym wierszu. | Niektóre systemy wolą przecinki lub pionowe kreski zamiast tabulacji. |
| **Duże arkusze ( > 100 k wierszy )** | Użyj `ExportTableOptions` z `ExportAsString = true` i strumieniuj plik jak pokazano; Aspose.Cells przetwarza wiersze w trybie strumieniowym, unikając błędów OOM. | Gwarantuje skalowalność. |
| **Wiele tabel w jednym arkuszu** | Iteruj `ws.Tables` i wywołuj `ExportTable` dla każdej, opcjonalnie dodając linię separatora między eksportami. | Pozwala **save Excel table to .txt file** dla każdej tabeli. |

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do `Program.cs`. Zamień `YOUR_DIRECTORY` na ścieżkę absolutną lub względną istniejącą na Twoim komputerze.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
            Worksheet ws = wb.Worksheets[0];

            // Get first table
            if (ws.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }
            Table tbl = ws.Tables[0];

            // Configure export options
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, writer) =>
                {
                    // Trim whitespace and write value
                    writer.Write(cell.StringValue.Trim());
                }
            };

            // Export to text file
            string outputPath = "YOUR_DIRECTORY/Table.txt";
            using (StreamWriter writer = new StreamWriter(outputPath))
            {
                ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
            }

            Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

Uruchom program poleceniem `dotnet run`. Jeśli wszystko jest poprawnie skonfigurowane, zobaczysz komunikat potwierdzający oraz nowo utworzony plik `Table.txt` zawierający **export excel data as plain text**.

## Bonus: Wizualne potwierdzenie (opcjonalnie)

Jeśli chcesz zobaczyć szybki zrzut ekranu powstałego pliku, otwórz go w dowolnym edytorze tekstu. Poniżej znajduje się przykładowy obrazek pokazujący oczekiwany układ.

![how to export excel table screenshot](https://example.com/images/export-excel-table.png "how to export excel table")

*Alt text:* **how to export excel table** – pokazuje wyjście w postaci zwykłego tekstu wyeksportowanej tabeli Excel.

## Podsumowanie i kolejne kroki

Omówiliśmy wszystko, co musisz wiedzieć **how to export Excel table** przy użyciu Aspose.Cells, od ładowania skoroszytu, przez przycinanie wartości komórek, aż po zapis czystego pliku `.txt`.  

- Teraz rozumiesz, jak **save Excel table to .txt file** z własną logiką.  
- Możesz dostosować lambdę do obsługi dat, liczb lub własnych separatorów.  
- W większych projektach rozważ opakowanie logiki w wielokrotnego użytku metodę lub klasę.

**Co dalej?** Spróbuj wyeksportować wiele tabel lub zmień format wyjściowy na CSV, zmieniając separator. Możesz także zbadać **export excel data as plain text** bezpośrednio do strumienia sieciowego dla integracji w czasie rzeczywistym.

Masz pytania lub napotkałeś problem? zostaw komentarz, i powodzenia w kodowaniu!

## Co powinieneś nauczyć się następnie?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [How to Export Excel Files in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Combine Excel Sheets into a Single Text File Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/combine-excel-sheets-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}