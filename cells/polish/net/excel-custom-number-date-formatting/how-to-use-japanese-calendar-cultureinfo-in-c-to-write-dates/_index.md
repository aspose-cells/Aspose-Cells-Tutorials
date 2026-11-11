---
category: general
date: 2026-10-26
description: Dowiedz się, jak używać CultureInfo japońskiego kalendarza w C# przy
  parsowaniu dat z erą i wstawianiu ich do arkusza Excel przy użyciu NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: pl
lastmod: 2026-10-26
og_description: Użyj CultureInfo kalendarza japońskiego w C#, aby parsować daty z
  ery Reiwa i zapisać je w arkuszu Excel. Pełny, działający kod z wyjaśnieniami.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Użyj japońskiego kalendarza CultureInfo w C# – pełny przykład Excel
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: Jak używać CultureInfo japońskiego kalendarza w C# do zapisywania dat w Excelu
url: /pl/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać CultureInfo kalendarza japońskiego w C# do zapisywania dat w Excelu

Jeśli potrzebujesz **używać CultureInfo kalendarza japońskiego** podczas pracy z datami w C#, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Nauczysz się parsować ciąg daty zawierający japońską nazwę ery (na przykład *Reiwa 2/5/1*) i następnie zapisać otrzymany `DateTime` w pierwszej komórce arkusza Excel przy użyciu biblioteki NPOI.

Parsowanie dat opartych na erze bez odpowiedniego `CultureInfo` prowadzi do `FormatException` lub niepoprawnych wartości miesiąca/dnia. Konfigurując `CultureInfo` na kalendarz japoński, zapewniasz, że środowisko .NET prawidłowo interpretuje erę i że wartość zapisana w Excelu odpowiada oryginalnej japońskiej notacji.

W tym samouczku:

* Utworzysz obiekt `CultureInfo` używający kalendarza japońskiego.
* Zparsujesz japoński ciąg daty z erą przy użyciu `DateTime.Parse`.
* Wstawisz sparsowany `DateTime` do komórki arkusza NPOI.
* Zobaczysz kompletny, uruchamialny program oraz oczekiwany wynik.

> **Wymagania wstępne** – .NET 6.0+ (lub .NET Core 3.1+), pakiet **NPOI** NuGet oraz podstawowa znajomość C# i obsługi plików Excel.

---

## Czego będziesz potrzebować

| Element | Powód |
|------|--------|
| **.NET SDK** (6.0 lub nowszy) | Dostarcza środowisko uruchomieniowe i biblioteki dla `CultureInfo`. |
| **NPOI** (`NPOI` pakiet NuGet) | Umożliwia tworzenie i manipulowanie plikami Excel bez zainstalowanego Office. |
| **Visual Studio Code**, **Visual Studio** lub dowolne IDE C# | Do kompilacji i uruchomienia przykładu. |
| **Japoński ciąg daty z erą** (np. `"Reiwa 2/5/1"`) | Demonstruje użycie kalendarza japońskiego. |

---

## Krok 1: Zainstaluj NPOI

Otwórz terminal w folderze projektu i uruchom:

```bash
dotnet add package NPOI --version 2.6.1
```

Pakiet dostarcza typy `IWorkbook`, `ISheet` i `ICell` używane później.

---

## Krok 2: Utwórz CultureInfo używający kalendarza japońskiego

Kalendarz japoński jest kalendarzem opartym na erze. Musisz poprosić o wariant *Japanese* lokalizacji `ja-JP` i jawnie ustawić kalendarz na `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Dlaczego to ważne** – Domyślna kultura `ja-JP` używa kalendarza gregoriańskiego. Przypisanie właściwości `Calendar` zapewnia, że nazwy er, takie jak *Reiwa*, są rozpoznawane podczas parsowania.

---

## Krok 3: Parsuj japoński ciąg daty z erą

Teraz, gdy `CultureInfo` jest skonfigurowane, możesz bezpiecznie parsować ciąg zawierający nazwę ery.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Wyjście**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

Metoda `Parse` interpretuje *Reiwa 2* jako rok gregoriański 2020, miesiąc 5, dzień 1.

### Przypadek brzegowy: obsługa nieprawidłowych er

Jeśli użytkownik poda nieobsługiwaną erę (np. `"Heisei 31/4/30"` po zakończeniu ery Heisei), `DateTime.Parse` zgłasza `FormatException`. Owiń wywołanie w blok try‑catch, aby zwrócić przyjazny komunikat o błędzie:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## Krok 4: Zapisz sparsowany DateTime w arkuszu Excel

Gdy obiekt `DateTime` jest gotowy, możesz umieścić go w komórce Excela. NPOI automatycznie formatuje wartości `DateTime` jako daty Excel.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Wynik** – Otwarcie *JapaneseEraDate.xlsx* pokazuje datę **2020‑05‑01** w komórce A1.

### Dlaczego warto używać NPOI?

*Działa na każdej platformie* (Windows, Linux, macOS) i **nie** wymaga Microsoft Office. Dzięki temu rozwiązanie nadaje się do potoków CI, kontenerów Docker czy przetwarzania po stronie serwera.

---

## Krok 5: Pełny, uruchamialny program

Łącząc wszystko razem, oto kompletny program konsolowy demonstrujący cały przepływ:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**Jak uruchomić**

```bash
dotnet run
```

Po wykonaniu znajdziesz plik `JapaneseEraDate.xlsx` w folderze projektu z prawidłowo sparsowaną datą.

---

## Typowe pułapki i wskazówki najlepszych praktyk

| Pułapka | Rozwiązanie / Rekomendacja |
|---------|----------------------------|
| Zapomnienie o ustawieniu `japaneseCulture.DateTimeFormat.Calendar` | Zawsze przypisuj instancję `JapaneseCalendar`; w przeciwnym razie nazwa ery nie zostanie rozpoznana. |
| Użycie `DateTime.TryParse` bez własnego `CultureInfo` | Przekaż tę samą `japaneseCulture` do `TryParse`, aby zachować spójne zachowanie. |
| Oczekiwanie, że Excel wyświetli nazwę ery | Wbudowane formaty dat w Excelu są wyłącznie gregoriańskie. Jeśli potrzebujesz wyświetlić erę, zapisz oryginalny ciąg w osobnej kolumnie lub utwórz własny format tekstowy. |
| Niezwalnianie `FileStream` | Użyj bloku `using` (jak pokazano), aby zapewnić szybkie zwolnienie uchwytu pliku. |
| Mieszanie obiektów `CultureInfo` między wątkami | `CultureInfo` jest bezpieczne wątkowo dla operacji tylko do odczytu, ale unikaj modyfikowania jego właściwości `Calendar` po początkowej konfiguracji. |

---

## Zakończenie

Teraz wiesz, jak **używać CultureInfo kalendarza japońskiego** w C#, aby dokładnie parsować daty z japońską erą i zapisywać otrzymany `DateTime` w arkuszu Excel przy pomocy NPOI. Pełny przykład obejmuje konfigurację, parsowanie, obsługę błędów i wyjście do Excela, dając solidne podstawy dla każdego zglobalizowanego raportowania lub scenariusza wymiany danych.

Następnie możesz zgłębić:

* **Formatowanie dat przy użyciu własnego tekstu**, aby zachować nazwę ery w Excelu.
* **Odczytywanie dat z Excela** przy użyciu `cell.DateCellValue` z uwzględnieniem kalendarza japońskiego.
* **Stosowanie tej samej techniki** dla innych kalendarzy opartych na erze (np. tajski kalendarz buddyjski) poprzez zamianę `JapaneseCalendar` na odpowiednią podklasę `Calendar`.

Śmiało eksperymentuj z różnymi ciągami er, większymi zestawami danych lub integruj tę logikę w API ASP.NET Core generującym raporty Excel w locie. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Utwórz skoroszyt Excel z datami kalendarza japońskiego – pełny przewodnik](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Parsuj daty japońskiej ery w Excelu – pełny przewodnik dla programistów C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Jak utworzyć skoroszyt Excel i parsować japońskie daty w C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}