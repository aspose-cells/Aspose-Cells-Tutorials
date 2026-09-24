---
category: general
date: 2026-09-24
description: Eksportuj zakres Excela jako obraz w C# przy użyciu Aspose.Cells – krok
  po kroku przewodnik, jak zapisać obszar arkusza jako PNG lub JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- Aspose.Cells export range
- C# Excel to PNG
- ImageOrPrintOptions usage
- export pivot table as image
language: pl
lastmod: 2026-09-24
og_description: Eksportuj zakres Excela jako obraz w C# z Aspose.Cells. Dowiedz się,
  jak w kilka minut przekształcić dowolny obszar arkusza, w tym tabele przestawne,
  na PNG lub JPEG.
og_image_alt: Screenshot of a C# program exporting an Excel range to a PNG image
og_title: Eksportuj zakres Excela jako obraz przy użyciu C# – kompletny przewodnik
  Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  headline: How to export excel range as image with C# and Aspose.Cells
  type: TechArticle
- description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  name: How to export excel range as image with C# and Aspose.Cells
  steps:
  - name: '**Load** the workbook from disk.'
    text: '**Load** the workbook from disk.'
  - name: '**Define** the cell area that will become the image (the *print area*).'
    text: '**Define** the cell area that will become the image (the *print area*).'
  - name: '**Export** the area using `ImageOrPrintOptions` and write the file.'
    text: '**Export** the area using `ImageOrPrintOptions` and write the file.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Image export
title: Jak wyeksportować zakres Excela jako obraz przy użyciu C# i Aspose.Cells
url: /pl/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyeksportować zakres Excela jako obraz przy użyciu C# i Aspose.Cells

Jeśli potrzebujesz **export excel range as image** w aplikacji .NET, ten przewodnik pokazuje kompletną, gotową do uruchomienia rozwiązanie. Niezależnie od tego, czy publikujesz pulpit nawigacyjny, osadzasz tabelę przestawną na stronie internetowej, czy generujesz miniaturkę raportu, możesz przekształcić dowolny obszar arkusza w PNG (lub JPEG) przy użyciu kilku linii kodu C#.

W tym samouczku dowiesz się, jak:

* Załadować istniejący skoroszyt (`Workbook` class)  
* Zdefiniować dokładny zakres komórek, który chcesz przechwycić (`PrintArea`)  
* Skonfigurować opcje eksportu obrazu (`ImageOrPrintOptions`)  
* Zapisz powstały obraz na dysku  

Wszystkie wymagania wstępne, przypadki brzegowe i typowe pułapki są omówione, abyś mógł dostosować kod do własnych projektów bez niespodzianek.

## Wymagania wstępne

| Wymaganie | Powód |
|-------------|--------|
| **Aspose.Cells for .NET** (latest version) | Udostępnia API `Workbook`, `Worksheet` i `ImageOrPrintOptions` używane w przykładzie. |
| **.NET 6.0 or later** | Przykład jest skierowany do .NET 6, ale każda wersja .NET Core/Framework obsługująca Aspose.Cells będzie działać. |
| **A valid Excel file** (e.g., `input.xlsx`) | Skoroszyt, który chcesz przekonwertować. |
| **Write permission to the output folder** | Wymagane, aby operacja `Save` zakończyła się sukcesem. |

You can install Aspose.Cells via NuGet:

```bash
dotnet add package Aspose.Cells
```

## Eksport zakresu Excela jako obrazu – przegląd procesu

The operation consists of three logical phases:

1. **Load** skoroszyt z dysku.  
2. **Define** obszar komórek, który stanie się obrazem (obszar *print area*).  
3. **Export** obszar przy użyciu `ImageOrPrintOptions` i zapisz plik.  

Poniżej każda faza jest rozbita na dedykowany krok z pełnym kodem źródłowym i wyjaśnieniem.

## Krok 1: Załaduj skoroszyt

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Path to the source Excel file
string inputPath = @"YOUR_DIRECTORY\input.xlsx";

// Create a Workbook object – this reads the file into memory
Workbook workbook = new Workbook(inputPath);
```

**Dlaczego to ważne:**  
`Workbook` jest punktem wejścia dla wszystkich operacji Excel. Załadowanie pliku raz utrzymuje niskie zużycie pamięci i pozwala później uzyskać dostęp do dowolnego arkusza.

## Krok 2: Uzyskaj dostęp do docelowego arkusza

```csharp
// Get the first worksheet (index 0). Change the index or use the sheet name as needed.
Worksheet sheet = workbook.Worksheets[0];
```

**Wskazówka:** Jeśli potrzebujesz konkretnego arkusza po nazwie, zamień indeks na `workbook.Worksheets["SheetName"]`. To zapobiega błędom, gdy układ skoroszytu się zmienia.

## Krok 3: Zdefiniuj zakres, który chcesz wyeksportować

```csharp
// Define the cell range that will be exported.
// Example: A1:G20 captures a typical pivot‑table area.
sheet.PageSetup.PrintArea = "A1:G20";
```

**Dlaczego ustawiać `PrintArea`?**  
Aspose.Cells renderuje *obszar wydruku* przy tworzeniu obrazu. Ograniczając go do dokładnego zakresu, unikasz dodatkowych pustych przestrzeni i zwiększasz wydajność.

### Alternatywa: Eksport całego arkusza

Jeśli chcesz cały arkusz, po prostu pomiń przypisanie `PrintArea`. Aspose.Cells domyślnie użyje używanego zakresu arkusza.

## Krok 4: Skonfiguruj opcje eksportu obrazu

```csharp
// Create an ImageOrPrintOptions object to control the output format.
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    // Choose PNG for lossless quality; change to Jpeg for smaller files.
    ImageFormat = ImageFormat.Png,

    // Optional: set the resolution (DPI). Higher DPI yields sharper images.
    HorizontalResolution = 300,
    VerticalResolution = 300,

    // Optional: set the page orientation if the range is wide.
    PageOrientation = PageOrientationType.Landscape
};
```

**Wyjaśnienie kluczowych właściwości:**

* `ImageFormat` – Określa typ pliku (`Png`, `Jpeg`, `Bmp` itp.). PNG jest idealny dla wykresów i tekstu, ponieważ zachowuje ostre krawędzie.  
* `HorizontalResolution` / `VerticalResolution` – Kontrolują gęstość pikseli. Dla miniatur internetowych 96 DPI wystarczy; dla grafik gotowych do druku zalecane jest 300 DPI.  
* `PageOrientation` – Pomaga, gdy wybrany zakres jest szerszy niż wyższy.  

## Krok 5: Wyeksportuj zakres do pliku obrazu

```csharp
// Define the output path for the image
string outputPath = @"YOUR_DIRECTORY\range.png";

// Save the first picture on the worksheet as an image.
// The Pictures collection is automatically populated after setting PrintArea.
sheet.Pictures[0].Save(outputPath, imgOptions);
```

**Co się dzieje w tle:**  
Gdy `PrintArea` jest ustawiony, Aspose.Cells generuje tymczasowy obraz reprezentujący ten obszar. Obiekt `Pictures[0]` jest następnie zapisywany przy użyciu podanych opcji.

### Obsługa arkuszy bez obrazów

Jeśli arkusz nie zawiera jeszcze obrazu (np. nowy plik), możesz go utworzyć w locie:

```csharp
// Create a picture from the defined range and add it to the sheet
Picture pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
pic.Save(outputPath, imgOptions);
```

## Pełny, uruchamialny przykład

Łącząc wszystko razem, oto samodzielna aplikacja konsolowa, którą możesz skopiować, wkleić i uruchomić:

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Define the range to export (e.g., a pivot table)
        sheet.PageSetup.PrintArea = "A1:G20";

        // 4️⃣ Set image export options (PNG, 300 DPI, landscape)
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300,
            PageOrientation = PageOrientationType.Landscape
        };

        // 5️⃣ Save the picture as an image file
        string outputPath = @"YOUR_DIRECTORY\range.png";

        // Ensure a picture exists; create one if necessary
        Picture pic;
        if (sheet.Pictures.Count == 0)
        {
            pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
        }
        else
        {
            pic = sheet.Pictures[0];
        }

        pic.Save(outputPath, imgOptions);

        System.Console.WriteLine($"Export completed: {outputPath}");
    }
}
```

**Oczekiwany wynik:**  
Plik o nazwie `range.png` pojawia się w `YOUR_DIRECTORY`. Po otwarciu pokazuje dokładne komórki od **A1 do G20** wyrenderowane jako wyraźny obraz PNG.

## Typowe warianty i obsługa przypadków brzegowych

| Scenariusz | Dostosowanie |
|----------|------------|
| **Export to JPEG** | Zmień `ImageFormat = ImageFormat.Jpeg` i opcjonalnie ustaw `Quality = 90` (zakres 0‑100). |
| **Multiple ranges** | Wywołaj `sheet.Pictures.Add` dla każdego zakresu i zapisz każdy obraz pod inną nazwą pliku. |
| **Large worksheets** | Zwiększ `HorizontalResolution`/`VerticalResolution` tylko dla potrzebnego zakresu, aby uniknąć skoków pamięci. |
| **No picture generated** | Sprawdź, czy `PrintArea` jest poprawnie sformatowany (`"A1:G20"`). Nieprawidłowy adres skutkuje pustą kolekcją `Pictures`. |
| **Saving to a stream** | Użyj `pic.Save(Stream, imgOptions)` gdy potrzebujesz obrazu w pamięci (np. w odpowiedzi ASP.NET). |

## Profesjonalne wskazówki dla niezawodnego eksportu obrazu

* **Validate the print area** – Użyj parsowania `CellArea` (`CellArea area = CellArea.CreateCellArea("A1", "G20")`) aby programowo budować zakresy i unikać literówek.  
* **Dispose of resources** – Otocz `Workbook` blokiem `using`, jeśli przetwarzasz wiele plików, aby szybko zwolnić zasoby natywne.  
* **Batch processing** – Przy eksportowaniu dziesiątek zakresów, ponownie używaj jednej instancji `ImageOrPrintOptions`, aby zmniejszyć narzut alokacji obiektów.  
* **Thread safety** – Obiekty Aspose.Cells nie są **bezpieczne wątkowo**. Utwórz osobny `Workbook` dla każdego wątku lub synchronizuj dostęp.  

## Zakończenie

Masz teraz kompletną, gotową do produkcji metodę **export excel range as image** przy użyciu C# i Aspose.Cells. Kroki — ładowanie skoroszytu, ustawianie obszaru wydruku, konfigurowanie `ImageOrPrintOptions` i zapisywanie obrazu — obejmują zarówno „jak”, jak i „dlaczego”, zapewniając możliwość dostosowania kodu do tabel przestawnych, wykresów lub dowolnego niestandardowego bloku komórek.

Next, you might explore:

* **Export excel range as image** w innych formatach (SVG, BMP) – kolejny drugorzędny słowo kluczowe do wypróbowania.  
* **Embedding the PNG in a PDF** przy użyciu Aspose.PDF do generowania raportów end‑to‑end.  
* **Automating batch exports** w wielu skoroszytach przy użyciu prostego pętli konsolowej.  

Śmiało eksperymentuj z różnymi rozdzielczościami, orientacjami i katalogami wyjściowymi. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Eksportowanie komórek Excel do obrazu przy użyciu Aspose.Cells .NET: przewodnik krok po kroku](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Eksportowanie skoroszytu Excel jako obrazu przy użyciu Aspose.Cells dla Java](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Jak wyeksportować arkusz Excel do PNG przy użyciu Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}