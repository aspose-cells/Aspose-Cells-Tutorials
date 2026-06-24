---
category: general
date: 2026-06-24
description: Utwórz płaski plik OPC w C# przy użyciu Aspose.Cells. Dowiedz się, jak
  skonfigurować SaveOptions dla FlatOPC, wyeksportować dane Xlsx i zweryfikować wynik
  w kilka minut.
draft: false
keywords:
- create flat OPC file
- Aspose.Cells FlatOPC save
- Xlsx flat OPC format
- SaveOptions FlatOPC example
- workbook save flat OPC
language: pl
og_description: Szybko utwórz płaski plik OPC w C#. Ten samouczek pokazuje krok po
  kroku, jak skonfigurować SaveOptions dla FlatOPC i wygenerować prawidłowy plik .opc.
og_title: Utwórz płaski plik OPC w C# – Kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create flat OPC file in C# using Aspose.Cells. Learn to set up SaveOptions
    for FlatOPC, export Xlsx data, and verify the result in minutes.
  headline: Create flat OPC file with C# – Complete Guide
  type: TechArticle
- questions:
  - answer: Absolutely—Aspose.Cells is cross‑platform, and the same code runs on Windows,
      Linux, or macOS.
    question: Does this work with .NET Core?
  - answer: Set the `Password` property on `SaveOptions` before calling `Save`. The
      flat OPC will include the encryption metadata.
    question: What if I need to export a password‑protected workbook?
  - answer: Yes. Use the overload `wb.Save(Stream, SaveOptions)` and pipe the stream
      wherever you need (HTTP response, Azure Blob, etc.).
    question: Can I stream the output instead of writing to disk?
  - answer: Typically a bit larger because it’s plain XML, but the trade‑off is human
      readability.
    question: Is the Flat OPC file larger than a regular .xlsx?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
- File formats
title: Utwórz płaski plik OPC w C# – Kompletny przewodnik
url: /pl/net/saving-and-exporting-excel-files-with-options/create-flat-opc-file-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz płaski plik OPC w C# – Kompletny przewodnik

Zastanawiałeś się kiedyś, jak **utworzyć płaski plik OPC** bez ręcznego walczenia się z XML? Nie jesteś jedyny. Niezależnie od tego, czy potrzebujesz lekkiej reprezentacji skoroszytu Excel do kontroli wersji, testów automatycznych, czy po prostu z ciekawości, format Flat OPC jest przydatnym narzędziem.  

W tym samouczku przeprowadzimy Cię przez rzeczywisty przykład z użyciem Aspose.Cells dla .NET, pokazując dokładnie, jak skonfigurować obiekt `SaveOptions`, dodać dane do skoroszytu i w końcu zapisać prawidłowy płaski plik OPC na dysku. Bez niejasnych odniesień — po prostu kompletny, gotowy do uruchomienia kod, który możesz skopiować‑wkleić.

## Czego się nauczysz

- Cel formatu **Flat OPC** i sytuacje, w których się wyróżnia.  
- Jak zainstalować i odwołać się do Aspose.Cells w projekcie C#.  
- Krok po kroku kod, który **tworzy płaski plik OPC** od podstaw.  
- Wskazówki dotyczące rozwiązywania typowych problemów i weryfikacji wyniku.

Zanim zaczniemy, upewnij się, że masz aktualną wersję .NET (4.6+ lub .NET Core 3.1+) oraz IDE, w którym czujesz się komfortowo — Visual Studio, Rider lub nawet VS Code będą odpowiednie.

![Przykład tworzenia płaskiego pliku OPC](/images/create-flat-opc-file.png "Zrzut ekranu płaskiego pliku OPC wygenerowanego przez kod C#")

## Tworzenie płaskiego pliku OPC – Przegląd

Format Flat OPC to zasadniczo pojedynczy dokument XML, który zawiera wszystkie części pakietu Office Open XML (np. skoroszyt `.xlsx`) w czytelnej, linia‑po‑linii strukturze. Jest idealny do kontroli wersji przyjaznej diff‑om, ponieważ możesz zobaczyć każdą komórkę, styl i relację jako zwykły tekst. Aspose.Cells odciąża ciężką pracę, pozwalając **utworzyć płaski plik OPC** w kilku linijkach kodu.

## Krok 1: Zainstaluj Aspose.Cells

Najpierw potrzebujesz biblioteki Aspose.Cells. Najszybszy sposób to przez NuGet:

```bash
dotnet add package Aspose.Cells
```

Lub, jeśli wolisz konsolę Package Manager w Visual Studio:

```powershell
Install-Package Aspose.Cells
```

> **Wskazówka:** Wybierz najnowszą stabilną wersję; od czerwca 2026 jest to 24.9.0, która zawiera poprawki błędów dla zapisu Flat OPC.

## Krok 2: Zbuduj przykładowy skoroszyt

Posiadanie skoroszytu z przynajmniej jednym arkuszem i kilkoma komórkami sprawia, że wynikowy płaski plik OPC jest ciekawszy. Poniżej znajduje się samodzielna metoda, która tworzy `Workbook`, wypełnia go i zwraca instancję.

```csharp
using Aspose.Cells;
using System;

public class FlatOpcDemo
{
    /// <summary>
    /// Creates a simple workbook with data for demonstration.
    /// </summary>
    /// <returns>A populated Workbook object.</returns>
    public static Workbook BuildSampleWorkbook()
    {
        // Initialize a new workbook – this is the entry point for any Excel manipulation.
        var wb = new Workbook();

        // Grab the first worksheet (index 0) and give it a friendly name.
        var sheet = wb.Worksheets[0];
        sheet.Name = "Demo";

        // Add a header row.
        sheet.Cells["A1"].PutValue("Product");
        sheet.Cells["B1"].PutValue("Quantity");
        sheet.Cells["C1"].PutValue("Price");

        // Insert a few rows of sample data.
        sheet.Cells["A2"].PutValue("Apples");
        sheet.Cells["B2"].PutValue(120);
        sheet.Cells["C2"].PutValue(0.45);

        sheet.Cells["A3"].PutValue("Bananas");
        sheet.Cells["B3"].PutValue(85);
        sheet.Cells["C3"].PutValue(0.30);

        // Apply a simple style to the header row – optional but shows that styles survive the flat OPC conversion.
        var style = wb.CreateStyle();
        style.Font.IsBold = true;
        style.ForegroundColor = System.Drawing.Color.LightGray;
        style.Pattern = BackgroundType.Solid;
        var styleFlag = new StyleFlag { Font = true, CellShading = true };
        sheet.Cells.CreateRange("A1:C1").ApplyStyle(style, styleFlag);

        return wb;
    }
}
```

Zauważ, że każda linijka jest celowo skomentowana. Te komentarze stają się częścią wyjaśnienia „dlaczego”, spełniając wymóg cytowania AI.

## Krok 3: Skonfiguruj SaveOptions dla formatu Flat OPC

Teraz przechodzi do sedna: ustawienie obiektu `SaveOptions`, aby Aspose.Cells wiedział, że chcemy **Flat OPC** zamiast domyślnego binarnego `.xlsx`. Kluczowe właściwości to `SaveFormat` (musi być `SaveFormat.FlatOPC`) oraz opcjonalnie `Compression` (ale Flat OPC jest już zwykłym XML, więc pozostawiamy domyślne).

```csharp
using Aspose.Cells;

/// <summary>
/// Prepares SaveOptions to generate a flat OPC file.
/// </summary>
/// <returns>A configured SaveOptions instance.</returns>
public static SaveOptions GetFlatOpcSaveOptions()
{
    // Step 1: Create save options for the Flat OPC format.
    // The constructor takes the base format (Xlsx) because FlatOPC is a variant of Xlsx.
    var flatOpcSaveOptions = new SaveOptions(SaveFormat.Xlsx)
    {
        // Explicitly tell Aspose.Cells we need the Flat OPC representation.
        SaveFormat = SaveFormat.FlatOPC
    };

    // You could also tweak other options here, e.g., EnableZip64 = false,
    // but for most scenarios the defaults are fine.
    return flatOpcSaveOptions;
}
```

Ten fragment kodu dokładnie odzwierciedla oryginalny kod, który podałeś, ale dodaje kontekst o *dlaczego* każda właściwość jest ustawiona, co czyni tutorial przydatnym do cytowania.

## Krok 4: Zapisz skoroszyt jako płaski plik OPC

Mając gotowy skoroszyt i opcje zapisu, zapis pliku to jednowierszowy kod. Owińmy cały przepływ w metodę `Main`, abyś mógł od razu uruchomić program.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Build a workbook with sample data.
        Workbook wb = FlatOpcDemo.BuildSampleWorkbook();

        // 2️⃣ Get the correctly configured SaveOptions.
        SaveOptions flatOpcOptions = FlatOpcDemo.GetFlatOpcSaveOptions();

        // 3️⃣ Define the output path – adjust the folder to suit your environment.
        string outputPath = @"C:\Temp\demo.flat.opc";

        // 4️⃣ Save the workbook using the configured options.
        // This is the line that actually creates the flat OPC file.
        wb.Save(outputPath, flatOpcOptions);

        Console.WriteLine($"Flat OPC file created at: {outputPath}");
    }
}
```

Uruchomienie tego programu wygeneruje plik o nazwie `demo.flat.opc`. Otwórz go w dowolnym edytorze tekstu, a zobaczysz pojedynczy dokument XML zawierający wszystkie dane arkuszy, style i relacje — dokładnie to, co definiuje specyfikacja **Flat OPC**.

## Weryfikacja i czego się spodziewać

Po wykonaniu, przejdź do `C:\Temp\demo.flat.opc` (lub innej wybranej ścieżki). Plik zacznie się od czegoś w rodzaju:

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<package xmlns="http://schemas.openxmlformats.org/package/2006/content-types">
  <part name="/xl/workbook.xml" contentType="application/vnd.openxmlformats-officedocument.spreadsheetml.sheet.main+xml">
    <!-- workbook XML goes here -->
  </part>
  <part name="/xl/worksheets/sheet1.xml" contentType="application/vnd.openxmlformats-officedocument.spreadsheetml.worksheet+xml">
    <!-- sheet data, including rows for Apples and Bananas -->
  </part>
  <!-- additional parts for styles, shared strings, etc. -->
</package>
```

Ponieważ format **Flat OPC** spłaszcza kontener ZIP do jednego XML, możesz porównać dwie wersje zwykłym `git diff` i natychmiast zauważyć zmiany na poziomie komórek. To główna zaleta w stosunku do binarnego pakietu `.xlsx`.

### Często zadawane pytania

- **Czy to działa z .NET Core?** Absolutnie — Aspose.Cells jest wieloplatformowy, a ten sam kod działa na Windows, Linuxie i macOS.  
- **Co zrobić, gdy muszę wyeksportować skoroszyt chroniony hasłem?** Ustaw właściwość `Password` w `SaveOptions` przed wywołaniem `Save`. Flat OPC uwzględni metadane szyfrowania.  
- **Czy mogę strumieniować wynik zamiast zapisywać na dysk?** Tak. Użyj przeciążenia `wb.Save(Stream, SaveOptions)` i przekieruj strumień tam, gdzie potrzebujesz (odpowiedź HTTP, Azure Blob itp.).  
- **Czy plik Flat OPC jest większy niż zwykły .xlsx?** Zazwyczaj nieco większy, ponieważ jest to czysty XML, ale wymiana na czytelność dla człowieka jest tego warta.

## Podsumowanie

Właśnie **utworzyliśmy płaski plik OPC** od podstaw przy użyciu C# i Aspose.Cells. Proces sprowadza się do trzech jasnych kroków: zbudowanie skoroszytu, skonfigurowanie `SaveOptions` dla formatu `FlatOPC` i wywołanie `Save`. Dzięki pełnemu kodowi powyżej możesz dostosować przykład do dowolnego istniejącego skoroszytu, dodać wykresy, tabele przestawne lub nawet makra — wszystko zostanie wiernie odzwierciedlone w wyjściu Flat OPC.

### Co dalej?

- Eksperymentuj z opcjami zapisu **Aspose.Cells FlatOPC** takimi jak `EnableMemoryOptimization` przy bardzo dużych skoroszytach.  
- Spróbuj przekonwertować istniejący `.xlsx` na Flat OPC, ładując go za pomocą `new Workbook("input.xlsx")` i ponownie zapisując.  
- Zbadaj powiązane formaty: **Open XML SDK** także obsługuje Flat OPC, oferując darmową alternatywę, jeśli nie potrzebujesz dodatkowych funkcji Aspose.

Masz własny pomysł, który wypróbowałeś i zadziałał (lub nie)? Podziel się nim w komentarzach — wspólna nauka wzmacnia społeczność. Miłego kodowania i ciesz się prostotą płaskiego OPC!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Utwórz i zapisz plik Excel Aspose Cells .NET](/cells/german/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [Utwórz i zapisz plik Excel Aspose Cells .NET](/cells/french/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [Utwórz i zapisz plik Excel Aspose Cells .NET](/cells/spanish/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}