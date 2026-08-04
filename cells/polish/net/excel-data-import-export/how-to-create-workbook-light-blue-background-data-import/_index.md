---
category: general
date: 2026-02-09
description: Jak utworzyć skoroszyt w C# z jasnoniebieskim tłem i zaimportować dane
  z nagłówkami. Dowiedz się, jak dodać jasnoniebieskie tło, używać domyślnego stylu
  Excela i importować DataTable.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: pl
og_description: Jak stworzyć skoroszyt w C# z jasnoniebieskim tłem, zaimportować dane
  z nagłówkami i zastosować domyślny styl Excela — wszystko w jednym zwięzłym przewodniku.
og_title: Jak utworzyć skoroszyt – jasnoniebieskie tło, import danych
tags:
- C#
- Excel
- Aspose.Cells
title: Jak utworzyć skoroszyt – jasnoniebieskie tło, import danych
url: /pl/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć skoroszyt – jasnoniebieskie tło, import danych

Zastanawiałeś się kiedyś **how to create workbook** w C#, które wygląda nieco ładniej od razu po utworzeniu? Być może pobrałeś `DataTable` z bazy danych i masz dość nudnych, domyślnie białych komórek. W tym tutorialu przeprowadzimy Cię przez tworzenie nowego skoroszytu, dodawanie jasnoniebieskiego tła do kolumny oraz importowanie danych z nagłówkami — wszystko przy użyciu domyślnego stylu, jaki oferuje Excel.

Dodamy także kilka scenariuszy „co‑jeśli”, takich jak obsługa wartości null lub stylowanie więcej niż jednej kolumny. Po zakończeniu będziesz mieć w pełni wystylizowany plik Excel, który możesz przekazać interesariuszom bez dodatkowej obróbki.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

* **.NET 6+** (kod działa również na .NET Framework 4.6+)  
* **Aspose.Cells for .NET** – biblioteka obsługująca wywołania `Workbook`, `Style` i `ImportDataTable`. Zainstaluj ją przez NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* Źródło `DataTable` – w przykładzie stworzymy sztuczne, ale możesz podmienić je na dowolne zapytanie ADO.NET.

Masz wszystko? Świetnie, zaczynamy.

## Krok 1: Inicjalizacja nowego skoroszytu (Primary Keyword)

Pierwszą rzeczą, którą musisz zrobić, jest **how to create workbook** – dosłownie. Klasa `Workbook` reprezentuje cały plik Excel, a jej konstruktor daje czystą kartkę.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Dlaczego to ważne:** Rozpoczęcie od świeżego `Workbook` zapewnia pełną kontrolę nad każdym stylem od samego początku. Gdybyś otworzył istniejący plik, odziedziczyłbyś wszystkie style pozostawione przez pierwotnego autora, co może prowadzić do niespójnego formatowania.

## Krok 2: Przygotowanie DataTable, które zaimportujesz

Dla celów ilustracyjnych utwórzmy prosty `DataTable`. W rzeczywistych scenariuszach prawdopodobnie wywołasz procedurę składowaną lub metodę ORM.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Wskazówka:** Jeśli musisz zachować kolejność kolumn dokładnie taką, jaka występuje w bazie danych, ustaw parametr `importColumnNames` metody `ImportDataTable` na `true`. Spowoduje to, że Aspose.Cells zapisze dla Ciebie nagłówki kolumn.

## Krok 3: Definiowanie stylów kolumn – domyślny + jasnoniebieskie tło

Teraz odpowiadamy na część **add light blue background** zagadki. Aspose.Cells pozwala przekazać tablicę obiektów `Style`, które odpowiadają każdej importowanej kolumnie. Pierwszy element to styl dla kolumny 0, drugi dla kolumny 1 i tak dalej. Jeśli stylów jest mniej niż kolumn, pozostałe kolumny odziedziczą domyślny styl.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Dlaczego tylko dwa style?** W naszym przykładzie mamy cztery kolumny, ale chcemy wyróżnić jedynie drugą kolumnę (Name). Długość tablicy nie musi odpowiadać liczbie kolumn; brakujące pozycje automatycznie przyjmują domyślny styl skoroszytu.

## Krok 4: Import DataTable z nagłówkami i stylami

Tutaj łączymy **excel import datatable c#** i **import data with headers**. Metoda `ImportDataTable` wykonuje ciężką pracę: zapisuje nazwy kolumn, wiersze i stosuje wcześniej zbudowaną tablicę stylów.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Oczekiwany wynik

Po uruchomieniu programu `workbook` będzie zawierał jedną arkusz, który wygląda tak:

| **ID** | **Name** (light‑blue) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* Kolumna **Name** ma jasnoniebieskie tło, co potwierdza działanie tablicy stylów.  
* Nagłówki kolumn są generowane automatycznie, ponieważ przekazaliśmy `true` dla `importColumnNames`.  
* Wartości null pojawiają się jako puste komórki – jest to domyślne zachowanie Aspose.Cells.

## Krok 5: Zapis skoroszytu (Opcjonalnie, ale przydatne)

Prawdopodobnie będziesz chciał zapisać plik na dysku lub przesłać go strumieniowo do klienta webowego. Zapis jest prosty:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Pro tip:** Jeśli celujesz w starsze wersje Excela, zamień `SaveFormat.Xlsx` na `SaveFormat.Xls`. API zajmie się konwersją za Ciebie.

## Przypadki brzegowe i warianty

### Wielokrotne stylowane kolumny

Jeśli potrzebujesz więcej niż jednej stylowanej kolumny, po prostu rozszerz tablicę `columnStyles`:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Teraz zarówno **Name**, jak i **Salary** będą miały jasnoniebieskie tło.

### Formatowanie warunkowe zamiast stałych stylów

Czasami chcesz, aby kolumna zmieniała kolor na czerwony, gdy wartość przekroczy pewien próg. Wtedy **use default style excel** łączy się z formatowaniem warunkowym:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Import bez nagłówków

Jeśli Twój system docelowy dostarcza własne nagłówki, po prostu przekaż `false` dla argumentu `importColumnNames`. Dane rozpoczną się w komórce `A1`, a własne nagłówki możesz dodać później.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Pełny działający przykład (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}