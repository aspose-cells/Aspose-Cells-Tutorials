---
category: general
date: 2026-11-19
description: Jak wyeksportować wykres Excel jako obraz PNG przy użyciu Aspose.Cells.
  Dowiedz się, jak zapisać obraz wykresu Excel i ustawić format obrazu PNG w kilku
  prostych krokach.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: pl
lastmod: 2026-11-19
og_description: Jak wyeksportować wykres Excel jako obraz PNG przy użyciu Aspose.Cells.
  Postępuj zgodnie z tym przewodnikiem krok po kroku, aby zapisać obraz wykresu Excel
  i efektywnie ustawić format obrazu na PNG.
og_image_alt: How to export Excel chart as a PNG image
og_title: Jak wyeksportować wykres Excel jako obraz PNG – szybki przewodnik C#
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: Jak wyeksportować wykres Excela jako obraz PNG w C#
url: /pl/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyeksportować wykres Excel jako obraz PNG w C#

Jeśli potrzebujesz **how to export Excel chart** do przenośnego obrazu, ten przewodnik pokazuje kompletną, gotową do uruchomienia rozwiązanie. Korzystając z Aspose.Cells możesz **save Excel chart image** w formacie PNG za pomocą zaledwie trzech linii kodu, a tutorial wyjaśnia także, jak **set image format png** i **save Excel picture file** w bezpieczny sposób.

Na koniec tego artykułu otrzymasz działający program, który wczytuje skoroszyt, renderuje pierwszy wykres i zapisuje plik `pivot.png` na dysku. Bez dodatkowych narzędzi, bez ręcznego kopiowania‑wklejania — po prostu czysty kod C#, który możesz wkleić do dowolnego projektu .NET.

## Wymagania wstępne

Zanim zaczniesz, upewnij się, że masz:

* .NET 6.0 SDK lub nowszy (kod działa także z .NET Framework 4.6+)
* Visual Studio 2022 lub dowolny edytor C#
* Licencję Aspose.Cells for .NET (lub tymczasowy klucz ewaluacyjny)
* Plik Excel (`pivot.xlsx`) zawierający przynajmniej jeden wykres na pierwszym arkuszu

Są to jedyne zewnętrzne zależności; tutorial nie wymaga zainstalowanego Office na komputerze.

## Krok 1: Zainstaluj Aspose.Cells

Otwórz terminal w folderze projektu i uruchom:

```bash
dotnet add package Aspose.Cells
```

Pakiet dodaje przestrzeń nazw `Aspose.Cells`, która udostępnia klasy `Workbook`, `ImageOrPrintOptions` i inne niezbędne do **save Excel chart image**.

## Krok 2: Utwórz minimalny program konsolowy

Utwórz nową aplikację konsolową (`dotnet new console -n ExportChartDemo`) i zamień wygenerowany automatycznie plik `Program.cs` na poniższy kod. Program demonstruje **how to export Excel chart** i zawiera komentarze wyjaśniające każdą decyzję.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### Dlaczego każdy element ma znaczenie

* **Loading the workbook** – `Workbook` parsuje plik `.xlsx` bez potrzeby posiadania zainstalowanego Microsoft Excel.
* **ImageOrPrintOptions** – Ten obiekt kontroluje format wyjściowy. Ustawienie `ImageFormat = ImageFormat.Png` **sets image format png**, co jest bezstratne i szeroko wspierane.
* **RenderToImage** – Metoda `RenderToImage` konwertuje wykres (obiekt `Picture`) na plik obrazu. Metoda automatycznie obsługuje skalowanie, DPI i przezroczystość.
* **Error handling** – Sprawdzenie `sheet.Pictures.Count == 0` zapobiega wyjątkowi w czasie wykonywania, gdy arkusz nie zawiera wykresów – częsty przypadek, gdy użytkownik wskazuje niewłaściwy arkusz.

## Krok 3: Uruchom program i zweryfikuj wynik

1. Zbuduj projekt: `dotnet build`.
2. Uruchom go: `dotnet run --project ExportChartDemo`.

Jeśli wszystko jest poprawnie skonfigurowane, zobaczysz:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

Otwórz `pivot.png` w dowolnym przeglądarce obrazów. Powinieneś zobaczyć dokładną wizualizację wykresu Excel, co potwierdza, że udało Ci się **saved Excel picture file**.

### Oczekiwany wynik

Poniżej przykład, jak może wyglądać wyeksportowany PNG (rzeczywisty wykres zależy od Twojego pliku źródłowego).

![Exported Excel chart saved as PNG image](images/exported-chart.png){: .center alt="Jak wyeksportować wykres Excel jako obraz PNG"}

## Krok 4: Zaawansowane opcje – eksport wielu wykresów

Jeśli Twój skoroszyt zawiera więcej niż jeden wykres, możesz przeiterować kolekcję `Pictures`:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

Ten wzorzec pozwala **save Excel chart image** dla każdego wykresu na arkuszu, co jest przydatne w pipeline’ach raportowych.

## Typowe pułapki i jak ich unikać

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|-------|--------------------------|-------------|
| `ArgumentOutOfRangeException` przy `Pictures[0]` | Arkusz nie zawiera wykresu lub wykres znajduje się na innym arkuszu. | Sprawdź indeks arkusza (`Worksheets[0]`) i upewnij się, że wykres istnieje. W razie potrzeby użyj `Worksheets["SheetName"]`. |
| Wyeksportowany obraz jest rozmyty | DPI ustawione zbyt nisko (domyślnie 96). | Zwiększ `HorizontalResolution` i `VerticalResolution` w `ImageOrPrintOptions`. |
| Plik PNG jest pusty lub uszkodzony | Brak licencji powodujący ograniczenia wersji ewaluacyjnej. | Zastosuj ważną licencję Aspose.Cells przed wczytaniem skoroszytu (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| Błędy ścieżki pliku (`FileNotFoundException`) | Nieprawidłowy placeholder `YOUR_DIRECTORY`. | Użyj ścieżek bezwzględnych lub `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`. |

Rozwiązanie tych problemów zapewnia płynne doświadczenie **save excel picture file**.

## Pro tip: Eksport bezpośrednio do strumienia pamięci

Czasami potrzebujesz obrazu w pamięci (np. do wysłania do API internetowego) zamiast zapisywania go na dysku:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

Ta sama logika **set image format png** obowiązuje; jedynie zamieniasz ścieżkę pliku na strumień.

## Zakończenie

Teraz wiesz, **how to export Excel chart** jako plik PNG przy użyciu Aspose.Cells dla .NET. Tutorial obejmował:

* Instalację biblioteki
* Wczytanie skoroszytu
* **Setting image format png**
* **Saving Excel chart image** na dysku
* Obsługę wielu wykresów i typowe błędy

Dzięki tej bazie możesz zintegrować eksport wykresów z automatycznym raportowaniem, usługami webowymi lub aplikacjami desktopowymi. Następnie odkryj pokrewne tematy, takie jak **save excel picture file** jako JPEG (`ImageFormat.Jpeg`) lub konwersję wykresów do PDF w celu tworzenia raportów do druku.

Miłego kodowania!

## Co warto nauczyć się dalej?

Poniższe tutoriale dotyczą ściśle powiązanych zagadnień, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i wypróbować alternatywne podejścia w własnych projektach.

- [Convert Excel Pie Chart to Image Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}