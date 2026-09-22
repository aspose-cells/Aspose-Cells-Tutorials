---
category: general
date: 2026-03-01
description: Szybko konwertuj Excel na PowerPoint przy użyciu C#. Dowiedz się, jak
  wygenerować prezentację PowerPoint z skoroszytu Excel przy użyciu Aspose.Cells w
  zaledwie kilku linijkach kodu.
draft: false
keywords:
- convert excel to powerpoint
- generate powerpoint from excel
- convert xlsx to pptx
- how to convert excel
- create pptx from excel
language: pl
og_description: Konwertuj Excel na PowerPoint w C#. Ten przewodnik pokazuje, jak wygenerować
  prezentację PowerPoint z pliku Excel przy użyciu Aspose.Cells, zawierając pełny
  kod i wskazówki.
og_title: Konwertuj Excel do PowerPoint – Kompletny samouczek C#
tags:
- C#
- Aspose.Cells
- Excel
- PowerPoint
title: Konwertuj Excel do PowerPoint – Przewodnik krok po kroku w C#
url: /pl/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwersja Excel do PowerPoint – Przewodnik krok po kroku w C#

Kiedykolwiek potrzebowałeś **konwertować Excel do PowerPoint**, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam — wielu programistów napotyka ten problem, gdy próbują przekształcić bogate w dane arkusze kalkulacyjne w gotowe do prezentacji slajdy.  

Dobra wiadomość jest taka, że kilka linii C# pozwala **automatycznie generować PowerPoint z Excela**, bez ręcznego kopiowania i wklejania. W tym samouczku przeprowadzimy Cię przez cały proces, od wczytania pliku `.xlsx` po zapisanie dopracowanego pliku `.pptx`, który możesz otworzyć w Microsoft PowerPoint lub dowolnym kompatybilnym przeglądarce.

> **Co otrzymasz:** działający program, który wczytuje skoroszyt Excel, konfiguruje opcje zapisu PowerPoint i zapisuje plik PowerPoint — wszystko przy użyciu biblioteki Aspose.Cells.

## Czego będziesz potrzebować

- **.NET 6.0** lub nowszy (kod działa również na .NET Framework 4.7+)  
- **Aspose.Cells for .NET** – możesz go pobrać z NuGet (`Install-Package Aspose.Cells`)  
- Podstawowa znajomość C# (nic skomplikowanego, tylko standardowe dyrektywy `using`)  
- Plik Excel (`input.xlsx`), który chcesz przekształcić w zestaw slajdów  

To wszystko. Bez dodatkowych narzędzi firm trzecich, bez interfejsu COM, bez skomplikowanej automatyzacji PowerPoint. Zanurzmy się.

![Diagram przepływu konwersji Excel do PowerPoint](convert-excel-to-powerpoint.png "Konwersja Excel do PowerPoint")

*Tekst alternatywny: Diagram przepływu konwersji Excel do PowerPoint*

## Konwersja Excel do PowerPoint przy użyciu Aspose.Cells

### Krok 1 – Wczytaj skoroszyt Excel

Pierwszą rzeczą, którą musimy zrobić, jest załadowanie arkusza kalkulacyjnego do pamięci. Aspose.Cells upraszcza to do wywołania konstruktora `Workbook` i przekazania ścieżki do pliku.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the Excel workbook
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
```

**Dlaczego to ważne:** Wczytanie skoroszytu daje dostęp do każdego arkusza, wykresu, a nawet osadzonych obrazów. Dzięki temu możemy zdecydować, co zachować, a co odrzucić przed konwersją.

### Krok 2 – Skonfiguruj opcje zapisu prezentacji

Aspose.Cells obsługuje wiele formatów wyjściowych, a dla PowerPoint używamy `PresentationSaveOptions`. Ten obiekt pozwala określić docelowy `SaveFormat.Pptx` oraz dostosować kilka przydatnych ustawień, takich jak osadzanie makr czy zachowanie oryginalnych szerokości kolumn.

```csharp
            // Step 2: Set up presentation save options for PowerPoint format
            PresentationSaveOptions saveOptions = new PresentationSaveOptions(SaveFormat.Pptx)
            {
                // Optional: keep the original Excel formatting as much as possible
                // (true by default, but we set it explicitly for clarity)
                KeepOriginalFormatting = true
            };
```

**Dlaczego to ważne:** Bez odpowiednich opcji uzyskane slajdy mogą wyglądać ściśnięcie lub stracić stylizację. Informując Aspose.Cells, że chcemy prawdziwy plik PPTX, zapewniamy, że konwersja zachowa układ Excela.

### Krok 3 – Zapisz skoroszyt jako prezentację PowerPoint

Teraz dzieje się magia. Jedno wywołanie `Save` zapisuje plik `.pptx`, który odzwierciedla pierwszy arkusz skoroszytu (lub wszystkie arkusze, w zależności od wersji biblioteki). W większości przypadków pierwszy arkusz wystarczy, ale później możesz eksperymentować.

```csharp
            // Step 3: Save the workbook as a PowerPoint presentation
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            workbook.Save(outputPath, saveOptions);

            Console.WriteLine($"Success! '{outputPath}' has been created.");
        }
    }
}
```

**Co zobaczysz:** Otwórz `output.pptx` w PowerPoint i zobaczysz, że każdy arkusz został przekształcony w slajd. Komórki tekstowe stają się polami tekstowymi, wykresy zamieniają się w natywne wykresy PowerPoint, a obrazy zachowują swoją pierwotną rozdzielczość.

## Generowanie PowerPoint z Excela – wskazówki dotyczące konfiguracji projektu

- **Instalacja NuGet:** Uruchom `dotnet add package Aspose.Cells` w folderze projektu. Pobierze to najnowszą stabilną wersję (stan na marzec 2026, wersja 23.10).  
- **Platforma docelowa:** Jeśli używasz .NET Core, upewnij się, że Twój plik `csproj` zawiera `<TargetFramework>net6.0</TargetFramework>`.  
- **Ścieżki plików:** Używaj `Path.Combine` dla bezpieczeństwa wieloplatformowego, szczególnie jeśli kod działa w kontenerach Linux.  

```csharp
using System.IO;

// Example of safe path building
string baseDir = AppDomain.CurrentDomain.BaseDirectory;
string inputPath = Path.Combine(baseDir, "input.xlsx");
string outputPath = Path.Combine(baseDir, "output.pptx");
```

## Konwersja Xlsx do Pptx – obsługa wielu arkuszy

Domyślnie Aspose.Cells konwertuje **tylko aktywny arkusz**. Jeśli potrzebujesz slajdu na każdy arkusz, możesz przeiterować kolekcję i zapisać każdy z osobna:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet sheet = workbook.Worksheets[i];
    sheet.IsSelected = true; // Make this sheet the active one
    string slidePath = Path.Combine(baseDir, $"Slide_{i + 1}.pptx");
    workbook.Save(slidePath, saveOptions);
}
```

**Wskazówka:** Po każdej iteracji wywołaj `workbook.Worksheets[i].IsSelected = false`, jeśli planujesz ponowne użycie tego samego obiektu `Workbook` w innych operacjach.

## Jak konwertować Excel – radzenie sobie z dużymi plikami

Duże skoroszyty (setki megabajtów) mogą obciążać pamięć. Kilka sztuczek utrzyma proces płynnym:

1. **Włącz strumieniowanie:** `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` zmusza Aspose.Cells do używania plików tymczasowych zamiast ładowania wszystkiego do RAM.  
2. **Pomiń puste wiersze/kolumny:** Ustaw `saveOptions.IgnoreEmptyRows = true`, aby zmniejszyć bałagan na slajdach.  
3. **Zmień rozmiar obrazów:** Jeśli Twój Excel zawiera obrazy wysokiej rozdzielczości, możesz je zmniejszyć przed konwersją przy użyciu `ImageResizeOptions`.  

```csharp
workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;
saveOptions.IgnoreEmptyRows = true;
saveOptions.ImageResizeOptions = new ImageResizeOptions
{
    Width = 1024,
    Height = 768,
    ResizeMode = ResizeMode.Proportional
};
```

## Tworzenie Pptx z Excela – weryfikacja wyniku

Po zakończeniu wywołania `Save` będziesz chciał potwierdzić, że plik jest użyteczny:

```csharp
if (File.Exists(outputPath))
{
    var fileInfo = new FileInfo(outputPath);
    Console.WriteLine($"File size: {fileInfo.Length / 1024} KB");
    // Optionally launch PowerPoint automatically (Windows only)
    System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
    {
        FileName = outputPath,
        UseShellExecute = true
    });
}
else
{
    Console.Error.WriteLine("Something went wrong – the PPTX was not created.");
}
```

Otwarcie pliku powinno pokazać zestaw slajdów odzwierciedlający układ oryginalnego arkusza, wraz z wykresami, tabelami i wszelkimi osadzonymi obrazami.

## Częste pytania i przypadki brzegowe

| Pytanie | Odpowiedź |
|----------|--------|
| *Czy mogę zachować makra Excel?* | Nie. PowerPoint nie obsługuje makr VBA z Excela. Będziesz musiał odtworzyć wszelką automatyzację bezpośrednio w PowerPoint. |
| *A co z komentarzami komórek?* | Stają się oddzielnymi polami tekstowymi na slajdzie, ale możesz je ukryć, ustawiając `saveOptions.IncludeCellComments = false`. |
| *Czy formuły są obliczane?* | Tak — Aspose.Cells oblicza formuły przed konwersją, więc slajd pokazuje wartości obliczone, a nie same formuły. |
| *Czy istnieje sposób na dostosowanie projektu slajdu?* | Po konwersji możesz zastosować szablon PowerPoint przy użyciu klasy `Presentation` z Aspose.Slides, a następnie skopiować wygenerowane slajdy do niego. |

## Pełny działający przykład (wszystki kod w jednym miejscu)

```csharp
using Aspose.Cells;
using System;
using System.IO;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Build safe file paths
            string baseDir = AppDomain.CurrentDomain.BaseDirectory;
            string inputPath = Path.Combine(baseDir, "input.xlsx");
            string outputPath = Path.Combine(baseDir, "output.pptx");

            // Load the Excel workbook
            Workbook workbook = new Workbook(inputPath);

            // Optional: improve memory usage for huge files
            workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;

            // Configure PowerPoint save options
            PresentationSaveOptions saveOptions = new PresentationSaveOptions(SaveFormat.Pptx)
            {
                KeepOriginalFormatting = true,
                IgnoreEmptyRows = true,
                ImageResizeOptions = new ImageResizeOptions
                {
                    Width = 1024,
                    Height = 768,
                    ResizeMode = ResizeMode.Proportional
                }
            };

            // Save as PowerPoint
            workbook.Save(outputPath, saveOptions);

            // Verify the result
            if (File.Exists(outputPath))
            {
                Console.WriteLine($"Success! '{outputPath}' created ({new FileInfo(outputPath).Length / 1024} KB).");
                // Open the file automatically (Windows only)
                System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            else
            {
                Console.Error.WriteLine("Failed to create the PowerPoint file.");
            }
        }
    }
}
```

Uruchom program, a otrzymasz nowy plik `.pptx` gotowy na kolejne spotkanie z klientem, prezentację w sali konferencyjnej lub wewnętrzne briefing.

## Podsumowanie

Teraz wiesz **jak konwertować Excel do PowerPoint** przy użyciu C# i Aspose.Cells. Główne kroki — wczytanie skoroszytu, ustawienie `PresentationSaveOptions` i wywołanie `Save` — są proste, a jednocześnie samouczek omówił niuanse **generowania PowerPoint z Excela**, takie jak zarządzanie pamięcią, 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}