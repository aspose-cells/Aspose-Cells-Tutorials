---
category: general
date: 2026-04-07
description: Dowiedz się, jak odświeżyć tabelę przestawną, wstawić obraz do Excela
  i zapisać skoroszyt Excela z miejscem na obraz w kilku prostych krokach.
draft: false
keywords:
- how to refresh pivot
- insert image into excel
- save excel workbook
- add picture placeholder
- refresh pivot table
language: pl
og_description: Jak odświeżyć tabelę przestawną w Excelu, wstawić obraz do Excela
  i zapisać skoroszyt Excel przy użyciu C# z miejscem na obraz. Przykład kodu krok
  po kroku.
og_title: Jak odświeżyć tabelę przestawną i wstawić obraz w Excelu – Kompletny przewodnik
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak odświeżyć tabelę przestawną i wstawić obraz do Excela – Kompletny przewodnik
url: /pl/net/pivot-tables/how-to-refresh-pivot-and-insert-image-into-excel-complete-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak odświeżyć tabelę przestawną i wstawić obraz do Excela – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak odświeżyć tabelę przestawną**, gdy źródłowe dane się zmieniają, a następnie wkleić świeży wykres lub obraz tabeli bezpośrednio do tego samego arkusza? Nie jesteś jedyny. W wielu procesach raportowania dane znajdują się w bazie danych, tabela przestawna pobiera je, a końcowy plik Excel musi wyświetlać najnowsze liczby jako obraz — aby użytkownicy końcowi nie mogli przypadkowo edytować źródła.  

W tym samouczku przejdziemy krok po kroku przez to: **jak odświeżyć tabelę przestawną**, **wstawić obraz do Excela**, a na koniec **zapisać skoroszyt Excel** przy użyciu **placeholdera obrazu**. Po zakończeniu będziesz mieć pojedynczy, uruchamialny program w C#, który robi wszystko, i zrozumiesz, dlaczego każda linijka ma znaczenie.

> **Pro tip:** Podejście działa z Aspose.Cells 2024 lub nowszym, co oznacza, że nie musisz mieć zainstalowanego Excela na serwerze.

---

## Co będzie potrzebne

- **Aspose.Cells for .NET** (pakiet NuGet `Aspose.Cells`).  
- .NET 6.0 SDK lub nowszy (kod kompiluje się również z .NET 8).  
- Podstawowy plik Excel (`input.xlsx`), który już zawiera tabelę przestawną i placeholder obrazu (pierwszy obiekt obrazu w arkuszu).  
- Trochę ciekawości dotyczącej modeli obiektów Excela.

Bez dodatkowego COM interop, bez instalacji Office, tylko czysty C#.

---

## Jak odświeżyć tabelę przestawną i przechwycić najnowsze dane

Pierwszą rzeczą, którą musisz zrobić, jest poinformowanie Excela (a właściwie Aspose.Cells), że tabela przestawna ma przeliczyć się na podstawie najnowszego zakresu źródłowego. Pominięcie tego kroku pozostawi Cię z przestarzałymi liczbami, co podważa cały cel automatyzacji.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// 1️⃣ Load the workbook and grab the first worksheet
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelDemo\input.xlsx");
Worksheet worksheet = workbook.Worksheets[0];

// 2️⃣ Refresh the first pivot table so it reflects the latest data
worksheet.PivotTables[0].Refresh();
```

**Dlaczego to ważne:**  
Gdy wywołujesz `Refresh()`, silnik tabeli przestawnej ponownie uruchamia logikę agregacji. Jeśli później wyeksportujesz tabelę przestawną jako obraz, obraz pokaże *aktualne* sumy, a nie te z momentu ostatniego zapisu pliku.

---

## Wstawianie obrazu do Excela przy użyciu placeholdera obrazu

Teraz, gdy tabela przestawna jest odświeżona, musimy przekształcić ją w statyczny obraz. Jest to przydatne, gdy chcesz zamrozić wizualizację do dystrybucji lub później osadzić ją w slajdzie PowerPointa.

```csharp
// 3️⃣ Set up image options – we want a PNG image
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png
};

// 4️⃣ Render the refreshed pivot table to an image using the options
Image pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

Obiekt `ImageOrPrintOptions` pozwala kontrolować rozdzielczość, tło i format. PNG jest bezstratny i świetnie sprawdza się w większości raportów biznesowych.

---

## Dodawanie placeholdera obrazu do arkusza

Większość szablonów Excel już zawiera kształt lub obraz, który pełni rolę „gniazda” dla dynamicznych grafik. Jeśli go nie masz, po prostu wstaw pusty obraz w Excelu i zapisz szablon — Aspose.Cells udostępni go jako `Pictures[0]`.

```csharp
// 5️⃣ Place the rendered image into the first picture placeholder on the sheet
worksheet.Pictures[0].Image = pivotImage;
```

**Co zrobić, jeśli masz wiele placeholderów?**  
Wystarczy zmienić indeks (`Pictures[1]`, `Pictures[2]`, …) lub przeiterować `worksheet.Pictures`, aby znaleźć odpowiedni po nazwie.

---

## Zapis skoroszytu Excel po modyfikacjach

Na koniec utrwalamy zmiany. Skoroszyt zawiera teraz odświeżoną tabelę przestawną, świeżo wygenerowany PNG oraz zaktualizowany placeholder obrazu.

```csharp
// 6️⃣ Save the workbook to see the result
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

Gdy otworzysz `output.xlsx`, zobaczysz wypełnione miejsce obrazu najnowszym zrzutem tabeli przestawnej. Żadne ręczne kroki nie są wymagane.

---

## Pełny działający przykład (wszystkie kroki razem)

Poniżej znajduje się kompletny, gotowy do skopiowania i wklejenia program. Zawiera niezbędne instrukcje `using`, obsługę błędów oraz komentarze wyjaśniające każdą nieoczywistą linię.

```csharp
using Aspose.Cells;
using System;
using System.Drawing.Imaging;

namespace ExcelPivotImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\MyProjects\ExcelDemo\input.xlsx";
            string outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";

            try
            {
                // Load workbook
                Workbook workbook = new Workbook(inputPath);
                Worksheet sheet = workbook.Worksheets[0];

                // -------------------------------------------------
                // Refresh pivot table – this is the core of "how to refresh pivot"
                // -------------------------------------------------
                if (sheet.PivotTables.Count == 0)
                {
                    Console.WriteLine("No pivot tables found on the first worksheet.");
                    return;
                }
                sheet.PivotTables[0].Refresh();

                // -------------------------------------------------
                // Convert refreshed pivot to PNG image
                // -------------------------------------------------
                ImageOrPrintOptions imgOpts = new ImageOrPrintOptions
                {
                    ImageFormat = ImageFormat.Png,
                    // Optional: higher DPI for sharper images
                    HorizontalResolution = 150,
                    VerticalResolution = 150
                };
                Image pivotImg = sheet.PivotTables[0].ToImage(imgOpts);

                // -------------------------------------------------
                // Insert the image into the first picture placeholder
                // -------------------------------------------------
                if (sheet.Pictures.Count == 0)
                {
                    // If the template lacks a placeholder, we create one on the fly
                    int picIdx = sheet.Pictures.Add(0, 0, pivotImg);
                    sheet.Pictures[picIdx].Name = "PivotSnapshot";
                }
                else
                {
                    sheet.Pictures[0].Image = pivotImg;
                }

                // -------------------------------------------------
                // Save the updated workbook – this fulfills "save excel workbook"
                // -------------------------------------------------
                workbook.Save(outputPath);
                Console.WriteLine($"Workbook saved successfully to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
                // In production you might log the stack trace or rethrow
            }
        }
    }
}
```

**Oczekiwany rezultat:**  
Otwórz `output.xlsx`. Pierwszy obiekt obrazu teraz pokazuje PNG odświeżonej tabeli przestawnej. Jeśli zmienisz dane źródłowe w `input.xlsx` i ponownie uruchomisz program, obraz zostanie automatycznie zaktualizowany — bez ręcznego kopiowania i wklejania.

---

## Typowe warianty i przypadki brzegowe

| Sytuacja | Co zmienić |
|-----------|------------|
| **Wiele tabel przestawnych** | Przejdź przez `sheet.PivotTables` i odśwież każdą, a następnie wybierz tę, której potrzebujesz do obrazu. |
| **Inny format obrazu** | Ustaw `ImageFormat = ImageFormat.Jpeg` (lub `Bmp`) w `ImageOrPrintOptions`. |
| **Dynamiczny wybór placeholdera** | Użyj `sheet.Pictures["MyPlaceholderName"]` zamiast indeksu. |
| **Duże skoroszyty** | Zwiększ `Workbook.Settings.CalculateFormulaEngine` do `EngineType.Fast`, aby przyspieszyć odświeżanie. |
| **Uruchamianie na serwerze bez interfejsu** | Aspose.Cells działa w pełni bez UI, więc nie wymaga dodatkowej konfiguracji. |

---

## Najczęściej zadawane pytania

**Q: Czy to działa z skoroszytami z włączonymi makrami (`.xlsm`)?**  
A: Tak. Aspose.Cells traktuje je jak każdy inny skoroszyt; makra są zachowane, ale nie są wykonywane podczas odświeżania.

**Q: Co zrobić, jeśli tabela przestawna korzysta z zewnętrznego źródła danych?**  
A: Musisz upewnić się, że łańcuch połączenia jest prawidłowy na maszynie, na której uruchamiany jest kod. Wywołaj `pivotTable.CacheDefinition.ConnectionInfo`, aby dostosować go programowo.

**Q: Czy mogę umieścić obraz w określonym zakresie komórek zamiast w placeholderze?**  
A: Oczywiście. Użyj `sheet.Pictures.Add(row, column, pivotImg)`, gdzie `row` i `column` są indeksami zerowymi.

---

## Podsumowanie

Omówiliśmy **jak odświeżyć tabelę przestawną**, **wstawić obraz do Excela**, **dodać placeholder obrazu**, a na koniec **zapisać skoroszyt Excel** — wszystko w schludnym fragmencie C#. Odświeżając najpierw tabelę przestawną, zapewniasz, że obraz odzwierciedla najnowsze liczby, a użycie placeholdera utrzymuje szablony w czystości i umożliwia ich ponowne wykorzystanie.

Następnie możesz rozważyć:

- Eksport tego samego obrazu do raportu PDF (`PdfSaveOptions`).  
- Automatyzację wsadu plików z różnymi danymi źródłowymi.  
- Użycie Aspose.Slides do wklejenia PNG bezpośrednio do slajdu PowerPoint.

Śmiało eksperymentuj — zamień PNG na JPEG, zmień DPI lub dodaj wiele obrazów. Główna idea pozostaje niezmienna: utrzymuj dane aktualne, przechwyć je jako obraz i osadź tam, gdzie potrzebujesz.

Miłego kodowania! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}