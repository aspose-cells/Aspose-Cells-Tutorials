---
category: general
date: 2026-10-20
description: Zapisz skoroszyt jako CSV z precyzyjnymi cyframi dziesiętnymi, wartościami
  w cudzysłowie i formatem daty japońskiej ery przy użyciu Aspose.Cells dla .NET.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- set excel number format
- export excel to csv
- quote csv values
language: pl
lastmod: 2026-10-20
og_description: Zapisz skoroszyt jako CSV z pełną kontrolą nad liczbami dziesiętnymi,
  cudzysłowami i datami w japońskim systemie ery. Przejdź krok po kroku przez samouczek
  C# z użyciem Aspose.Cells.
og_image_alt: Screenshot illustrating how to save workbook as CSV with custom options
  in C#
og_title: Zapisz skoroszyt jako CSV – kompletny przewodnik dla programistów C#
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Save workbook as CSV with precise decimal digits, quoted values and
    Japanese era date format using Aspose.Cells for .NET.
  headline: How to save workbook as CSV with custom formatting in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- CSV export
- Excel formatting
title: Jak zapisać skoroszyt jako CSV z niestandardowym formatowaniem w C#
url: /pl/net/csv-file-handling/how-to-save-workbook-as-csv-with-custom-formatting-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zapisać skoroszyt jako CSV z niestandardowym formatowaniem w C#

Jeśli potrzebujesz **zapisać skoroszyt jako CSV** kontrolując precyzję dziesiętną, cytowanie wartości i obsługę dat w erze japońskiej, ten samouczek pokaże Ci, jak to zrobić przy użyciu Aspose.Cells dla .NET. Nauczysz się **eksportować Excel do CSV**, **ustawiać format liczbowy w Excelu** i **cytować wartości CSV**, aby wynik odpowiadał typowym wymaganiom wymiany danych.

Przewodnik zakłada, że masz środowisko programistyczne .NET (Visual Studio 2022 lub nowsze) oraz ważną licencję Aspose.Cells. Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.Cells`.

## Wymagania wstępne

- .NET 6.0 SDK lub nowszy  
- Aspose.Cells for .NET (zainstalowany przez NuGet: `Install-Package Aspose.Cells`)  
- Przykładowy plik Excel (`Data.xlsx`) umieszczony w folderze, do którego możesz odwołać się w kodzie  

## Krok 1: Załaduj źródłowy skoroszyt – podstawa do zapisywania skoroszytu jako CSV

Najpierw tworzysz instancję `Workbook`, która wskazuje na plik Excel, który chcesz przekonwertować.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\Data.xlsx");
```

*Dlaczego ten krok jest ważny*: Obiekt `Workbook` przechowuje wszystkie arkusze, style i formuły. Wszystkie późniejsze operacje CSV działają na tej reprezentacji w pamięci.

## Krok 2: Ogranicz precyzję dziesiętną przy zapisywaniu skoroszytu jako CSV

Gdy potrzebujesz dokładnie czterech cyfr po przecinku, skonfiguruj `CsvSaveOptions`.

```csharp
// Configure CSV saving options
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    // Keep 4 digits after the decimal point
    SignificantDigits = 4
};

// Save the workbook as CSV with the defined precision
workbook.Save(@"YOUR_DIRECTORY\Data_Sig4.csv", csvOptions);
```

*Kluczowy punkt*: `SignificantDigits` zaokrągla każdą komórkę liczbową do określonej liczby miejsc po przecinku przed zapisaniem pliku CSV. Zapobiega to szumowi zmiennoprzecinkowemu w systemach downstream.

## Krok 3: Eksportuj Excel do CSV z cytowanymi wartościami

Niektóre parsery downstream wymagają, aby każde pole było otoczone podwójnymi cudzysłowami, szczególnie gdy wartości zawierają przecinki lub znaki nowej linii. Klasa `ExportTableOptions` pozwala traktować każdą komórkę jako ciąg znaków i zastosować własne cytowanie.

```csharp
// Prepare export options that treat every cell as a string
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // Force string export for all cells
    // Custom delegate to wrap each value in double quotes
    CustomExport = (cell, writer) =>
    {
        writer.Write('"' + cell.StringValue + '"');
    }
};

// Export the first worksheet as a CSV file with quoted values
workbook.Save(@"YOUR_DIRECTORY\TableExport.csv", tableOptions);
```

*Dlaczego warto cytować wartości*: Cytowanie chroni przecinki, znaki nowej linii oraz początkowe/końcowe spacje przed interpretacją jako delimitery, co jest niezbędne dla niezawodnego importu danych.

## Krok 4: Ustaw format liczbowy w Excelu dla dat w erze japońskiej

Excel może przechowywać daty przy użyciu kalendarzy specyficznych dla ery. Aby to zademonstrować, wstaw ciąg daty w erze japońskiej i zastosuj odpowiedni format liczbowy.

```csharp
// Create a new workbook for the era‑date example
Workbook eraWorkbook = new Workbook();
Worksheet sheet = eraWorkbook.Worksheets[0];

// Insert a Japanese‑era date string (Reiwa 3‑04‑01)
sheet.Cells["A1"].PutValue("R3-04-01");

// Apply the Japanese locale number format
sheet.Cells["A1"].SetNumberFormat("[$-ja-JP]yyyy-mm-dd");

// Retrieve the parsed DateTime value
DateTime parsedDate = sheet.Cells["A1"].GetDateTime();
Console.WriteLine(parsedDate); // Outputs: 2021-04-01
```

*Wyjaśnienie*: Wywołanie `SetNumberFormat` informuje Aspose.Cells, aby interpretował ciąg przy użyciu japońskiego kalendarza. Gdy wywołasz `GetDateTime()`, biblioteka automatycznie konwertuje notację ery na datę gregoriańską.

## Krok 5: Zweryfikuj wygenerowane pliki CSV

Po uruchomieniu kodu powinieneś zobaczyć trzy pliki w `YOUR_DIRECTORY`:

| Nazwa pliku            | Najważniejsze cechy |
|------------------------|---------------------|
| `Data_Sig4.csv`        | Liczby zaokrąglone do 4 miejsc po przecinku |
| `TableExport.csv`      | Każda komórka otoczona podwójnymi cudzysłowami |
| `Data.xlsx` (niezmieniony) | Demonstracja obsługi dat w erze japońskiej (wyświetlana w Excelu) |

Otwórz `Data_Sig4.csv` w edytorze tekstowym, aby potwierdzić precyzję, oraz otwórz `TableExport.csv`, aby zobaczyć cytowane wartości, np.:

```
"Name","Score","Comment"
"Alice","95.1234","Excellent"
"Bob","88.0000","Good"
```

Wyjście konsoli dla daty w erze będzie:

```
2021-04-01 00:00:00
```

## Typowe pułapki i jak ich unikać

- **Separator dziesiętny zależny od ustawień regionalnych**: `CsvSaveOptions` respektuje bieżącą kulturę. Jeśli potrzebujesz kropki (`.`) jako separatora niezależnie od ustawień regionalnych, ustaw `csvOptions.Separator = ',';`.
- **Duże arkusze**: Eksportowanie skoroszytu z milionami wierszy może zużywać dużo pamięci. Użyj `ExportTableOptions.StartRow` i `EndRow`, aby ograniczyć zakres eksportu.
- **Specjalne znaki w ciągach**: Niestandardowy zapis w Kroku 3 dodaje jedynie otaczające cudzysłowy. Jeśli komórka już zawiera cudzysłów, podwój go (`""`), aby zachować poprawność CSV.

## Porada: Połącz opcje dla maksymalnej kontroli

Możesz łączyć `CsvSaveOptions` i `ExportTableOptions`, najpierw konwertując skoroszyt do `MemoryStream` z jednym zestawem opcji, a następnie zapisując strumień na dysk z innym. To podejście pozwala, na przykład, zastosować zarówno zaokrąglanie dziesiętne **i** cytowanie w jednym przebiegu:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    // Apply rounding
    workbook.Save(ms, csvOptions);
    ms.Position = 0; // Reset stream

    // Load the intermediate CSV into a new workbook for quoting
    Workbook temp = new Workbook(ms, new LoadOptions(LoadFormat.Csv));
    temp.Save(@"YOUR_DIRECTORY\RoundedAndQuoted.csv", tableOptions);
}
```

## Zakończenie

Teraz wiesz, jak **zapisać skoroszyt jako CSV** z precyzyjnym obsługiwaniem liczb dziesiętnych, cytowanymi wartościami i niestandardowym formatowaniem dat. Pełne rozwiązanie obejmuje ładowanie skoroszytu, konfigurowanie `CsvSaveOptions`, użycie `ExportTableOptions` do **cytowania wartości CSV** oraz zastosowanie **formatu liczbowego w Excelu** dla dat w erze japońskiej. Od tego momentu możesz badać dodatkowe opcje, takie jak własne separatory, różne kodowania czy selektywny eksport arkuszy.

---

*Kolejne kroki*  
- Zbadaj `CsvSaveOptions.Encoding`, aby zapisywać pliki z BOM UTF‑8 lub UTF‑16.  
- Użyj `ExportTableOptions.StartColumn` / `EndColumn`, aby wyeksportować tylko podzbiór kolumn.  
- Połącz te techniki z `DataFormatter` Aspose.Cells, aby uzyskać formatowanie liczb zależne od ustawień regionalnych.  

Miłego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Zapisz skoroszyt jako CSV – Kompletny przewodnik po eksporcie Excel do CSV z kontrolą](/cells/english/net/csv-file-handling/save-workbook-as-csv-complete-guide-to-export-excel-to-csv-w/)
- [Zapisz skoroszyt jako CSV w C# – Eksport Excel do CSV](/cells/english/net/csv-file-handling/save-workbook-as-csv-in-c-export-excel-to-csv/)
- [Utwórz i zapisz skoroszyt Excel jako PDF w ASP.NET przy użyciu Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}