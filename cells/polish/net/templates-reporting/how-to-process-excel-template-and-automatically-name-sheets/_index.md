---
category: general
date: 2026-10-10
description: Dowiedz się, jak przetwarzać szablon Excela w C# i automatycznie nadawać
  nazwy arkuszom. Przewodnik krok po kroku z kodem SmartMarkerProcessor i najlepszymi
  praktykami.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- process excel template
- automatically name sheets
- SmartMarkerProcessor
- Excel automation C#
- worksheet data binding
language: pl
lastmod: 2026-10-10
og_description: Przetwarzaj szablon Excela w C# i automatycznie nazwij arkusze za
  pomocą SmartMarkerProcessor. Postępuj zgodnie z tym szczegółowym samouczkiem, aby
  generować dynamiczne skoroszyty.
og_image_alt: Screenshot showing process excel template with automatically named sheets
  in a C# application
og_title: Przetwarzaj szablon Excela i automatycznie nazwij arkusze w C# – kompletny
  przewodnik
schemas:
- author: GroupDocs
  dateModified: '2026-10-10'
  description: Learn how to process Excel template in C# while automatically name
    sheets. Step‑by‑step guide with SmartMarkerProcessor code and best practices.
  headline: How to process Excel template and automatically name sheets in C#
  type: TechArticle
- description: Learn how to process Excel template in C# while automatically name
    sheets. Step‑by‑step guide with SmartMarkerProcessor code and best practices.
  name: How to process Excel template and automatically name sheets in C#
  steps:
  - name: Large data sets
    text: 'When the data source contains hundreds of rows, the processor creates a
      separate sheet for each row by default. To keep the workbook from exploding,
      you can:'
  - name: Existing sheet name conflicts
    text: If the template already contains a sheet named `Detail`, the processor appends
      a numeric suffix to avoid collision (`Detail_0`, `Detail_1`, …). To enforce
      a custom conflict‑resolution strategy, inspect `Worksheet.Sheets` before processing
      and rename any conflicting sheets.
  - name: Non‑Excel templates
    text: The same `SmartMarkerProcessor` can process Word, PowerPoint, or PDF templates.
      The only change is the class you instantiate (`Document`, `Presentation`, etc.).
      The **process excel template** pattern stays identical, which means you can
      reuse the code with minimal adjustments.
  type: HowTo
tags:
- Excel
- C#
- SmartMarker
- Automation
title: Jak przetwarzać szablon Excela i automatycznie nadawać nazwy arkuszom w C#
url: /pl/net/templates-reporting/how-to-process-excel-template-and-automatically-name-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przetwarzać szablon Excel i automatycznie nazywać arkusze w C#

Jeśli potrzebujesz **przetwarzać szablon Excel** w aplikacji .NET, ten przewodnik pokaże Ci niezawodny sposób generowania skoroszytów i **automatycznego nazywania arkuszy**. Korzystając z `SmartMarkerProcessor` biblioteki GroupDocs.Parser, możesz powiązać dane z szablonem, tworzyć arkusze szczegółowe w locie i utrzymać porządek w skoroszycie bez ręcznego zmieniania nazw.

Zakończysz tutorial pełnym, gotowym do uruchomienia przykładem, który odczytuje szablon, stosuje źródło danych i tworzy arkusze o nazwach `Detail`, `Detail_1`, `Detail_2`, … Wszystkie wymagane przestrzenie nazw, kroki konfiguracji i typowe pułapki są omówione, dzięki czemu możesz śmiało skopiować kod do własnego projektu.

## Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz:

* .NET 6.0 lub nowszy (kod działa z .NET Core i .NET Framework)
* Odwołanie do pakietu NuGet **GroupDocs.Parser** (wersja 23.5 lub nowsza)
* Szablon Excel (`Template.xlsx`) zawierający znaczniki SmartMarker, takie jak `{{Table}}` dla danych master‑detail
* Prosty model danych (np. `DataTable` lub lista obiektów) pasujący do znaczników w szablonie

Jeśli którekolwiek z tych elementów brakuje, zainstaluj pakiet NuGet przy użyciu:

```bash
dotnet add package GroupDocs.Parser
```

## Przegląd rozwiązania

Rozwiązanie składa się z trzech logicznych faz:

1. **Utwórz instancję `SmartMarkerProcessor`** – ten obiekt steruje całym silnikiem szablonów.
2. **Skonfiguruj procesor, aby automatycznie nazywał arkusze szczegółowe** – opcja `DetailSheetNewName` definiuje nazwę bazową, a biblioteka dodaje kolejne przyrostki.
3. **Wykonaj `Process`** – metoda odczytuje szablon, łączy źródło danych i zapisuje wynik do nowego skoroszytu.

Każda faza jest wyjaśniona poniżej, wraz z dokładnym kodem, którego potrzebujesz.

## Krok 1: Utwórz instancję SmartMarkerProcessor

Procesor jest punktem wejścia dla wszystkich operacji SmartMarker. Nie wymaga żadnych argumentów konstruktora, ale możesz później przekazać własny obiekt `SmartMarkerOptions`, jeśli potrzebujesz zaawansowanych ustawień.

```csharp
using GroupDocs.Parser;
using GroupDocs.Parser.Options;

// ...

// Step 1: Instantiate the processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

*Dlaczego to ważne*: Tworzenie instancji procesora raz na operację utrzymuje niskie zużycie pamięci i pozwala ponownie używać tego samego obiektu dla wielu szablonów, jeśli to konieczne.

## Krok 2: Skonfiguruj automatyczne nazewnictwo arkuszy

Gdy tabela master‑detail rozdziela się na osobne arkusze, biblioteka automatycznie tworzy nowe arkusze. Ustawiając `DetailSheetNewName`, kontrolujesz nazwę bazową używaną przez silnik. Biblioteka dodaje podkreślenie i rosnący numer dla każdego dodatkowego arkusza.

```csharp
// Step 2: Define the base name for automatically created detail sheets
processor.Options.DetailSheetNewName = "Detail"; // Sheets become Detail, Detail_1, Detail_2, …
```

*Wskazówki*:

* Wybierz nazwę bazową, która nie koliduje z istniejącymi nazwami arkuszy w szablonie.
* Schemat nazewnictwa działa dla dowolnej liczby wierszy szczegółowych; biblioteka przestaje dodawać przyrostki, gdy zostanie utworzony ostatni arkusz.
* Jeśli potrzebujesz innego wzorca nazewnictwa (np. prefiks zamiast przyrostka), możesz modyfikować `processor.Options.DetailSheetNewName` przed każdym wywołaniem.

## Krok 3: Przetwórz arkusz przy użyciu źródła danych

Metoda `Process` przyjmuje trzy argumenty:

* **źródłowy arkusz** (`Worksheet` object) – uzyskujesz go, ładując plik szablonu.
* **strumień docelowy** – miejsce, w którym zostanie zapisany przetworzony skoroszyt.
* **źródło danych** – dowolny obiekt implementujący `IDataSource` (np. `DataTable`, `IEnumerable<T>`).

Poniżej znajduje się kompletny przykład, który ładuje `Template.xlsx`, wiąże `DataTable` i zapisuje wynik jako `Result.xlsx`.

```csharp
using System.Data;
using System.IO;
using GroupDocs.Parser;
using GroupDocs.Parser.Data;
using GroupDocs.Parser.Options;

// ...

// Load the Excel template into a Worksheet object
using (FileStream templateStream = File.OpenRead("Template.xlsx"))
{
    // Create a Worksheet instance from the template
    Worksheet ws = new Worksheet(templateStream);

    // Prepare a simple DataTable as the data source
    DataTable dt = new DataTable("Employees");
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    // Populate the table with sample rows
    dt.Rows.Add("Alice", "Engineering", 95000);
    dt.Rows.Add("Bob", "Marketing", 72000);
    dt.Rows.Add("Charlie", "Sales", 68000);

    // Wrap the DataTable in a DataSource object required by SmartMarker
    IDataSource dataSource = new DataTableSource(dt);

    // Step 1 and Step 2 have already been performed earlier
    // Now process the worksheet
    using (MemoryStream resultStream = new MemoryStream())
    {
        processor.Process(ws, dataSource, resultStream);

        // Write the processed workbook to a physical file
        File.WriteAllBytes("Result.xlsx", resultStream.ToArray());
    }
}
```

*Wyjaśnienie kluczowych linii*:

* `new Worksheet(templateStream)` odczytuje plik Excel i tworzy reprezentację w pamięci, którą SmartMarker może modyfikować.
* `DataTableSource` implementuje `IDataSource`, umożliwiając procesorowi iterację po wierszach i podstawianie znaczników takich jak `{{Employees.Name}}`.
* `processor.Process(ws, dataSource, resultStream)` łączy dane i zapisuje finalny skoroszyt do `resultStream`. Metoda automatycznie tworzy arkusze szczegółowe o nazwach `Detail`, `Detail_1` itd., dzięki opcji ustawionej w Kroku 2.
* Po przetworzeniu wynik jest zapisywany jako `Result.xlsx`. Otwórz plik w Excelu, aby zweryfikować, że istnieją trzy arkusze szczegółowe, każdy zawierający wiersze z tabeli `Employees`.

## Zweryfikuj wynik

Otwórz `Result.xlsx` i sprawdź następujące elementy:

| Nazwa arkusza | Oczekiwana zawartość |
|---------------|----------------------|
| Detail | Wiersz nagłówka (`Name`, `Department`, `Salary`) oraz pierwszy wiersz danych (`Alice`) |
| Detail_1 | Drugi wiersz danych (`Bob`) |
| Detail_2 | Trzeci wiersz danych (`Charlie`) |

Jeśli arkusze pojawią się z prawidłową nazwą bazową i przyrostkowymi sufiksami, przepływ pracy **process excel template** zakończył się sukcesem, a funkcja **automatically name sheets** działała zgodnie z oczekiwaniami.

## Obsługa przypadków brzegowych

### Duże zestawy danych

Gdy źródło danych zawiera setki wierszy, procesor domyślnie tworzy osobny arkusz dla każdego wiersza. Aby zapobiec nadmiernemu rozrostowi skoroszytu, możesz:

* **Grupowanie wierszy**: zmodyfikuj szablon, aby używać znacznika tabeli powtarzającego się w jednym arkuszu zamiast tworzyć nowy arkusz dla każdego wiersza.
* **Ograniczenie tworzenia arkuszy**: ustaw `processor.Options.MaxDetailSheets` na rozsądną liczbę (np. 50) i obsłuż przepełnienie ręcznie.

```csharp
processor.Options.MaxDetailSheets = 50; // Prevent more than 50 auto‑generated sheets
```

### Konflikty nazw istniejących arkuszy

Jeśli szablon już zawiera arkusz o nazwie `Detail`, procesor dodaje numeryczny sufiks, aby uniknąć kolizji (`Detail_0`, `Detail_1`, …). Aby wymusić własną strategię rozwiązywania konfliktów, sprawdź `Worksheet.Sheets` przed przetwarzaniem i zmień nazwę wszelkich kolidujących arkuszy.

```csharp
foreach (var sheet in ws.Sheets)
{
    if (sheet.Name.Equals("Detail", StringComparison.OrdinalIgnoreCase))
    {
        sheet.Name = "BaseDetail";
    }
}
```

### Szablony nie‑Excel

Ten sam `SmartMarkerProcessor` może przetwarzać szablony Word, PowerPoint lub PDF. Jedyną zmianą jest klasa, którą tworzysz (`Document`, `Presentation` itp.). Wzorzec **process excel template** pozostaje identyczny, co oznacza, że możesz ponownie użyć kodu przy minimalnych modyfikacjach.

## Profesjonalne wskazówki dla środowiska produkcyjnego

* **Ponowne użycie procesora**: Utwórz singleton `SmartMarkerProcessor`, jeśli przetwarzasz wiele szablonów w usłudze webowej. Redukuje to narzut alokacji.
* **Strumień zamiast pliku**: W scenariuszach o wysokiej przepustowości trzymaj zarówno szablon, jak i wynik w strumieniach pamięci, aby uniknąć operacji dyskowych.
* **Zwalnianie obiektów**: Wszystkie instancje `Worksheet`, `FileStream` i `MemoryStream` implementują `IDisposable`. Użycie bloków `using`, jak pokazano, zapewnia prawidłowe zwolnienie zasobów.
* **Logowanie**: Włącz `processor.Options.Logging`, aby przechwycić szczegółowe informacje o przetwarzaniu, co pomaga szybko diagnozować błędy szablonu.

## Pełny, uruchamialny przykład

Poniżej znajduje się cały program skompilowany w jednym pliku. Skopiuj go do projektu konsolowego i uruchom; wynikowy skoroszyt pojawi się w folderze projektu.

```csharp
using System;
using System.Data;
using System.IO;
using GroupDocs.Parser;
using GroupDocs.Parser.Data;
using GroupDocs.Parser.Options;

class ExcelTemplateProcessor
{
    static void Main()
    {
        // 1️⃣ Create the processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Set automatic sheet naming
        processor.Options.DetailSheetNewName = "Detail";

        // Load the template
        using (FileStream templateStream = File.OpenRead("Template.xlsx"))
        {
            Worksheet ws = new Worksheet(templateStream);

            // Build a sample data source
            DataTable dt = new DataTable("Employees");
            dt.Columns.Add("Name", typeof(string));
            dt.Columns.Add("Department", typeof(string));
            dt.Columns.Add("Salary", typeof(decimal));
            dt.Rows.Add("Alice", "Engineering", 95000);
            dt.Rows.Add("Bob", "Marketing", 72000);
            dt.Rows.Add("Charlie", "Sales", 68000);
            IDataSource dataSource = new DataTableSource(dt);

            // 3️⃣ Process the worksheet
            using (MemoryStream resultStream = new MemoryStream())
            {
                processor.Process(ws, dataSource, resultStream);
                File.WriteAllBytes("Result.xlsx", resultStream.ToArray());
            }
        }

        Console.WriteLine("Processing complete. Check Result.xlsx.");
    }
}
```

Uruchomienie programu wypisuje „Processing complete. Check Result.xlsx.” i tworzy plik Excel, który demonstruje przepływ pracy **process excel template** z **automatically name sheets**.

## Zakończenie

Teraz wiesz, jak **przetwarzać szablony Excel** w C#, pozwalając bibliotece **automatycznie nazywać arkusze** na podstawie własnej nazwy bazowej. Tutorial obejmował tworzenie procesora, konfigurację opcji, powiązanie danych i kroki weryfikacji, a także obsługę przypadków brzegowych i wskazówki produkcyjne. Zastosuj ten sam wzorzec w większych projektach, zintegrować go z API webowymi lub rozszerzyć na inne formaty Office.

**Kolejne kroki**, które możesz rozważyć:

* Użyj `processor.Options.DetailSheetNewName` z wartościami dynamicznymi (np. uwzględnij datę lub identyfikator użytkownika).
* Połącz wiele źródeł danych, aby generować hierarchie master‑detail w kilku arkuszach.
* Eksperymentuj ze stylizacją znaczników SmartMarker, aby kontrolować czcionki, kolory i formaty liczb bezpośrednio z szablonu.

Miłego kodowania i ciesz się usprawnioną automatyzacją Excel!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletny działający kod z przykładami oraz wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Create Excel from Template – Step‑by‑Step Guide for .NET Developers](/cells/english/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/)
- [How to Merge and Rename Excel Sheets Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/worksheet-management/merge-rename-excel-sheets-aspose-cells-net/)
- [How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide](/cells/english/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}