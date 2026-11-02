---
category: general
date: 2026-09-24
description: Utwórz skoroszyt Excela programowo i dowiedz się, jak tworzyć wiele arkuszy
  szczegółowych, a następnie zapisz skoroszyt jako plik xlsx z przejrzystym przykładem
  w C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook programmatically
- how to create multiple detail sheets
- save workbook as xlsx file
language: pl
lastmod: 2026-09-24
og_description: Utwórz skoroszyt Excela programowo, zobacz, jak stworzyć wiele arkuszy
  szczegółowych i zapisać skoroszyt jako plik xlsx w jednym, gotowym do uruchomienia
  przykładzie.
og_image_alt: Screenshot of an Excel workbook created programmatically in C#
og_title: Tworzenie skoroszytu Excel programowo – pełny przewodnik C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Create Excel workbook programmatically and learn how to create multiple
    detail sheets, then save workbook as xlsx file with a clear C# example.
  headline: Create Excel workbook programmatically using Smart Markers
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Tworzenie skoroszytu Excel programowo przy użyciu Smart Markers
url: /pl/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt Excel programowo przy użyciu Smart Markers

Jeśli potrzebujesz **utworzyć skoroszyt Excel programowo**, ten przewodnik pokaże Ci dokładnie, jak to zrobić przy użyciu Aspose.Cells .NET. Odkryjesz także **jak utworzyć wiele arkuszy szczegółowych** z jednego źródła danych i w końcu **zapisać skoroszyt jako plik xlsx** bez żadnych ręcznych kroków.  

Rozwiązanie jest samodzielne: przechodzimy przez każdy wiersz kodu, wyjaśniamy, dlaczego każde ustawienie ma znaczenie, i omawiamy typowe pułapki, takie jak duplikaty nazw arkuszy. Po zakończeniu będziesz mieć gotową do uruchomienia aplikację konsolową, która generuje skoroszyt z arkuszem głównym i zestawem arkuszy szczegółowych.

## Czego będziesz potrzebować

| Wymaganie | Powód |
|--------------|--------|
| .NET 6.0 SDK lub nowszy | Zapewnia środowisko uruchomieniowe dla aplikacji konsolowej C# |
| Aspose.Cells dla .NET (pakiet NuGet `Aspose.Cells`) | Dostarcza klasy `Workbook`, `SmartMarkerProcessor` i `SmartMarkerOptions` |
| Proste źródło danych (np. `DataTable` lub lista obiektów) | Dostarcza wartości, które zostaną rozwinięte przez Smart Markers |
| Visual Studio 2022 lub dowolny edytor obsługujący .NET | Ułatwia kompilację i uruchamianie kodu |

> **Wskazówka:** Zainstaluj pakiet Aspose.Cells za pomocą CLI przed rozpoczęciem:  
> `dotnet add package Aspose.Cells`

## Krok 1: Skonfiguruj projekt i zaimportuj przestrzenie nazw

Utwórz nowy projekt konsolowy i wprowadź wymagane przestrzenie nazw do zasięgu.

```csharp
using System;
using System.Data;               // For DataTable (sample data source)
using Aspose.Cells;              // Core Excel API
using Aspose.Cells.SmartMarkers; // Smart Marker processing
```

*Dlaczego to ważne*: `Aspose.Cells` obsługuje cykl życia skoroszytu, natomiast `Aspose.Cells.SmartMarkers` zapewnia potężny silnik Smart Marker, który może generować wiele arkuszy z jednego szablonu.

## Krok 2: Utwórz skoroszyt Excel programowo

Pierwszym konkretnym działaniem jest utworzenie instancji `Workbook`. Ten obiekt reprezentuje cały plik Excel w pamięci.

```csharp
// Step 2: Create a new workbook (or load an existing template)
Workbook workbook = new Workbook(); // an empty workbook with one default sheet
```

Jeśli wolisz rozpocząć od szablonu, który już zawiera wiersze nagłówka lub formatowanie, zamień `new Workbook()` na `new Workbook("Template.xlsx")`. Reszta procesu działa identycznie.

## Krok 3: Przygotuj szablon Smart Marker

Smart Markery działają na zawartości komórek, które zawierają znaczniki takie jak `&=Employees.Name`. W tym samouczku dodamy prosty szablon bezpośrednio w kodzie, ale możesz również edytować arkusz ręcznie w Excelu.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Write a header row
sheet.Cells["A1"].PutValue("Employee Report");

// Insert a Smart Marker that will generate a detail sheet for each employee
sheet.Cells["A3"].PutValue("&=Employees.Name");

// Optional: add column titles for the detail sheet
sheet.Cells["A4"].PutValue("Name");
sheet.Cells["B4"].PutValue("Department");
sheet.Cells["C4"].PutValue("Salary");
```

*Dlaczego to ważne*: Znacznik `&=Employees.Name` informuje procesor Smart Marker, aby iterował po kolekcji `Employees`. Każda iteracja utworzy nowy arkusz, ponieważ skonfigurujemy procesor tak, aby tworzył **arkusz szczegółowy** dla każdego wiersza.

## Krok 4: Zbuduj źródło danych zawierające wiele wierszy

Użyjemy `DataTable` jako szybkiego sposobu symulacji kolekcji rekordów pracowników.

```csharp
// Step 4: Create a DataTable with sample employee data
DataTable employees = new DataTable("Employees");
employees.Columns.Add("Name", typeof(string));
employees.Columns.Add("Department", typeof(string));
employees.Columns.Add("Salary", typeof(decimal));

employees.Rows.Add("Alice Johnson", "Finance", 72000);
employees.Rows.Add("Bob Smith", "Engineering", 95000);
employees.Rows.Add("Carol Lee", "Marketing", 63000);
```

Możesz zamienić to na dowolny `IEnumerable` (np. `List<Employee>`) – Smart Markery akceptują każde źródło danych implementujące `IEnumerable`.

## Krok 5: Skonfiguruj opcje Smart Marker – jak utworzyć wiele arkuszy szczegółowych

Domyślnie Smart Markery zapisują dane w tym samym arkuszu. Aby wygenerować **wiele arkuszy szczegółowych**, musisz ustawić właściwość `DetailSheetNewName`. To także pokazuje **jak utworzyć wiele arkuszy szczegółowych** bez konfliktów nazw.

```csharp
// Step 5: Configure Smart Marker options
SmartMarkerOptions smOptions = new SmartMarkerOptions
{
    // Each iteration will create a new sheet named "Detail"
    DetailSheetNewName = "Detail"
};
```

Jeśli źródło danych zawiera duplikujące się nazwy, procesor automatycznie dodaje numeryczny sufiks (np. `Detail_1`, `Detail_2`). Zapobiega to błędom w czasie wykonywania i zapewnia zapis wszystkich arkuszy szczegółowych.

## Krok 6: Przetwórz Smart Markery

Teraz wywołujemy procesor, przekazując źródło danych oraz opcje, które właśnie zdefiniowaliśmy.

```csharp
// Step 6: Process Smart Markers
workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);
```

*Dlaczego to ważne*: Procesor odczytuje znacznik `&=Employees.Name`, iteruje po każdym wierszu `employees`, tworzy nowy arkusz o nazwie „Detail” i zapisuje dane wiersza w tym arkuszu. Oryginalny arkusz pozostaje jako podsumowanie lub arkusz główny.

## Krok 7: Zapisz skoroszyt jako plik xlsx

Na koniec zapisz skoroszyt na dysku, używając wzorca **zapisz skoroszyt jako plik xlsx**.

```csharp
// Step 7: Save the resulting workbook
string outputPath = @"./output/detail.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

`SaveFormat.Xlsx` enum zapewnia, że plik jest przechowywany w nowoczesnym formacie Office Open XML, który jest kompatybilny z Excel 2007+ oraz większością usług w chmurze.

## Pełny, działający przykład

Skopiuj poniższy kod do pliku `Program.cs` w projekcie konsolowym .NET i uruchom go. Program wygeneruje `detail.xlsx` w folderze `output`, zawierający jeden arkusz główny i trzy arkusze szczegółowe (po jednym dla każdego pracownika).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create an empty workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Build a simple template with a Smart Marker
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Employee Report");
            sheet.Cells["A3"].PutValue("&=Employees.Name");
            sheet.Cells["A4"].PutValue("Name");
            sheet.Cells["B4"].PutValue("Department");
            sheet.Cells["C4"].PutValue("Salary");

            // 3️⃣ Prepare the data source
            DataTable employees = new DataTable("Employees");
            employees.Columns.Add("Name", typeof(string));
            employees.Columns.Add("Department", typeof(string));
            employees.Columns.Add("Salary", typeof(decimal));

            employees.Rows.Add("Alice Johnson", "Finance", 72000);
            employees.Rows.Add("Bob Smith", "Engineering", 95000);
            employees.Rows.Add("Carol Lee", "Marketing", 63000);

            // 4️⃣ Configure Smart Marker options (how to create multiple detail sheets)
            SmartMarkerOptions smOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail"
            };

            // 5️⃣ Process the markers
            workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);

            // 6️⃣ Save workbook as xlsx file
            string outPath = "./output/detail.xlsx";
            workbook.Save(outPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outPath}");
        }
    }
}
```

**Oczekiwany wynik**

- `output/detail.xlsx` zawiera:
  - **Sheet1** – oryginalny szablon z nagłówkiem „Employee Report”.
  - **Detail** – pierwszy arkusz szczegółowy z rekordem Alice.
  - **Detail_1** – drugi arkusz szczegółowy z rekordem Bob.
  - **Detail_2** – trzeci arkusz szczegółowy z rekordem Carol.

Otwórz plik w Excelu, a zobaczysz każdego pracownika na osobnym arkuszu, co potwierdza, że pomyślnie **utworzyliśmy wiele arkuszy szczegółowych** i **zapisaliśmy skoroszyt jako plik xlsx**.

## Częste pytania i obsługa przypadków brzegowych

| Pytanie | Odpowiedź |
|----------|--------|
| *Co zrobić, jeśli potrzebuję niestandardowej nazwy dla każdego arkusza szczegółowego?* | Ustaw `DetailSheetNewName = "Employee_"` i dodaj kolumnę o nazwie `SheetName` w źródle danych. Procesor dopisze wartość `SheetName` do nazwy bazowej. |
| *Czy mogę zachować oryginalny arkusz jako podsumowanie wszystkich szczegółów?* | Tak. Arkusz główny pozostaje niezmieniony; możesz dodać formuły odwołujące się do wygenerowanych arkuszy szczegółowych. |
| *Co się stanie, gdy źródło danych jest puste?* | Żadne arkusze szczegółowe nie zostaną utworzone, ale skoroszyt nadal zostanie zapisany. Rozważ sprawdzenie `employees.Rows.Count` przed przetwarzaniem, jeśli potrzebujesz specjalnej obsługi. |
| *Czy można użyć istniejącego pliku szablonu?* | Zamień `new Workbook()` na `new Workbook("Template.xlsx")`. Cała logika Smart Marker działa w ten sam sposób. |

## Podsumowanie

Teraz wiesz **jak utworzyć skoroszyt Excel programowo**, jak **utworzyć wiele arkuszy szczegółowych** przy użyciu Smart Markers oraz jak **zapisać skoroszyt jako plik xlsx** przy użyciu Aspose.Cells. Pełny przykład można dostosować do faktur, raportów lub dowolnego scenariusza, w którym wymagany jest wyjściowy Excel w układzie master‑detail.

### Kolejne kroki

- Zbadaj inne funkcje Smart Marker, takie jak **group markers** i **conditional formatting**.
- Zastąp `DataTable` rzeczywistym zapytaniem do bazy danych, aby generować raporty na dużą skalę.
- Użyj `Workbook.Save("output.pdf", SaveFormat.Pdf)`, aby wyeksportować te same dane do PDF w celu dystrybucji.

Śmiało eksperymentuj z różnymi schematami nazewnictwa, stylizacją lub dodatkowymi arkuszami — Twoje nowe umiejętności programowego generowania Excel są gotowe do użycia w produkcji. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz skoroszyt Excel C# – Dodaj komentarz i zapisz jako XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Utwórz nowy skoroszyt w C# – Dodaj formułę i zapisz plik Excel](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Utwórz skoroszyt Excel C# – Wstaw JSON i zapisz jako XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}