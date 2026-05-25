---
category: general
date: 2026-05-04
description: Jak odświeżyć tabelę przestawną w C# i wyeksportować ją jako PNG, a następnie
  wstawić obraz do arkusza. Postępuj zgodnie z tym przewodnikiem krok po kroku z pełnym
  kodem.
draft: false
keywords:
- how to refresh pivot
- how to export pivot
- insert image into worksheet
- refresh pivot table code
- load excel workbook c#
language: pl
og_description: Jak odświeżyć tabelę przestawną w C#? Dowiedz się, jak wyeksportować
  tabelę przestawną jako obraz i wstawić ją do arkusza, z pełnymi przykładami kodu.
og_title: Jak odświeżyć tabelę przestawną w C# – eksport i wstawienie jako obraz
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Jak odświeżyć Pivot w C# – eksport i wstawienie jako obraz
url: /pl/net/pivot-tables/how-to-refresh-pivot-in-c-export-and-insert-as-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak odświeżyć tabelę przestawną w C# – eksport i wstawienie jako obrazu

Odświeżanie tabeli przestawnej w C# to częsta przeszkoda przy automatyzacji raportów Excel. W tym przewodniku zobaczysz dokładnie **jak odświeżyć tabelę przestawną**, wyeksportować ją jako PNG i umieścić ten obraz w miejscu przeznaczonym w arkuszu – wszystko w jednym, gotowym do uruchomienia programie.

Jeśli zastanawiasz się *jak wyeksportować tabelę przestawną* lub potrzebujesz **wstawić obraz do arkusza**, trafiłeś we właściwe miejsce. Przejdziemy przez każdy wiersz kodu, wyjaśnimy, dlaczego jest ważny, i omówimy kilka przypadków brzegowych, które mogą pojawić się w rzeczywistych projektach.

---

## Czego będziesz potrzebować

Zanim zaczniemy, upewnij się, że masz:

- **Aspose.Cells for .NET** (biblioteka udostępniająca `Workbook`, `Worksheet`, `ImageOrPrintOptions` itp.). Pobierz ją z NuGet: `Install-Package Aspose.Cells`.
- .NET 6 lub nowszy (kod poniżej jest skierowany do .NET 6, ale działa również w każdej nowszej wersji).
- Podstawową znajomość C# i operacji I/O – nic skomplikowanego.

To wszystko. Nie potrzebujesz dodatkowych DLL‑ów, COM‑interop, po prostu czysta aplikacja konsolowa w C#.

---

## Krok 1 – Załaduj skoroszyt Excel w stylu C#

Najpierw musimy otworzyć plik źródłowy. To miejsce, w którym pojawia się **load excel workbook c#**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Dlaczego?**  
> Załadowanie skoroszytu daje dostęp do jego arkuszy, tabel przestawnych i miejsc na obrazy. Jeśli plik nie zostanie znaleziony, Aspose zgłosi czytelny `FileNotFoundException`, który możesz przechwycić, aby wyświetlić przyjaźniejszy komunikat.

---

## Krok 2 – Przygotuj opcje obrazu do eksportu tabeli przestawnej

Teraz mówimy Aspose, jak ma wyglądać wyeksportowany obraz. To serce **how to export pivot**.

```csharp
        // Step 2: Set up image export options – PNG is lossless and widely supported
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            // Optional: tweak resolution for sharper images
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

> **Pro tip:**  
> Jeśli potrzebujesz JPEG o mniejszym rozmiarze pliku, zamień `SaveFormat.Png` na `SaveFormat.Jpeg` i odpowiednio dostosuj `Quality`.

---

## Krok 3 – Kod odświeżania tabeli przestawnej

Przestarzała tabela przestawna pokazuje stare dane. Odświeżenie zapewnia, że obraz odzwierciedla najnowsze liczby.

```csharp
        // Step 3: Refresh the first pivot table in the worksheet
        if (worksheet.PivotTables.Count > 0)
        {
            worksheet.PivotTables[0].Refresh();
        }
        else
        {
            Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }
```

> **Dlaczego odświeżać?**  
> Tabele przestawne buforują dane źródłowe w momencie ich utworzenia. Jeśli podlegający arkusz ulegnie zmianie (np. dodano nowe wiersze), bufor staje się nieaktualny. Wywołanie `Refresh()` zmusza Aspose do ponownego odczytania zakresu źródłowego, zapewniając, że wyeksportowany obraz nie będzie „zablokowany” na przestarzałych sumach.

---

## Krok 4 – Konwersja odświeżonej tabeli przestawnej na obraz

Oto magiczna linia, która faktycznie **export pivot** do tablicy bajtów.

```csharp
        // Step 4: Export the refreshed pivot table as an image
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

> **Co otrzymujesz:**  
> `pivotImage` zawiera teraz obraz tabeli przestawnej zakodowany jako PNG, gotowy do zapisania na dysku lub osadzenia w innym miejscu.

---

## Krok 5 – Wstaw obraz do arkusza

To miejsce, w którym **insert image into worksheet**. Umieścimy obraz w pierwszym miejscu na obraz (jeśli takie istnieje).

```csharp
        // Step 5: Insert the image into the first picture placeholder
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            // If no placeholder exists, add a new picture at cell A1
            int pictureIndex = worksheet.Pictures.Add(0, 0, pivotImage).Index;
            Console.WriteLine($"Added new picture at index {pictureIndex}.");
        }
```

> **Dlaczego używać miejsca na obraz?**  
> Wiele szablonów Excel dostarcza wstępnie sformatowany kształt obrazu (rozmiar, obramowanie, pozycję). Kierując się do `Pictures[0]`, zachowujemy układ. Jeśli szablon nie ma takiego miejsca, mechanizm awaryjny tworzy nowy obraz zakotwiczony w komórce A1.

---

## Krok 6 – Zapisz skoroszyt (opcjonalnie)

Na koniec utrwal zmiany. Możesz nadpisać oryginał lub zapisać do nowego pliku.

```csharp
        // Step 6: Save the updated workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **Oczekiwany rezultat:**  
> Otwórz `output.xlsx` i zobaczysz odświeżoną tabelę przestawną, wyeksportowaną jako wyraźny PNG i wyświetloną w pierwszym miejscu na obraz. Reszta skoroszytu pozostaje niezmieniona.

---

## Pełny działający przykład (gotowy do kopiowania)

Poniżej znajduje się kompletny blok kodu, który możesz wkleić do nowego projektu konsolowego. Żadne fragmenty nie brakuje.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);
        Worksheet worksheet = workbook.Worksheets[0];

        // Configure image export options (PNG, 300 DPI)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // Refresh the first pivot table
        if (worksheet.PivotTables.Count == 0)
        {
            Console.WriteLine("No pivot tables found.");
            return;
        }
        worksheet.PivotTables[0].Refresh();

        // Export pivot to PNG byte array
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);

        // Insert the image into a picture placeholder or add a new picture
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            worksheet.Pictures.Add(0, 0, pivotImage);
        }

        // Save the workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Uruchom program, otwórz wygenerowany plik i sprawdź, czy tabela przestawna odzwierciedla najnowsze dane i wyświetla się jako obraz wysokiej rozdzielczości.

---

## Najczęściej zadawane pytania i przypadki brzegowe

| Pytanie | Odpowiedź |
|----------|--------|
| **Co zrobić, gdy skoroszyt ma wiele arkuszy?** | Zmodyfikuj `workbook.Worksheets[0]` na odpowiedni indeks lub nazwę (`workbook.Worksheets["Sheet2"]`). |
| **Czy mogę wyeksportować wiele tabel przestawnych?** | Przejdź pętlą po `worksheet.PivotTables` i powtórz kroki 3‑4 dla każdej. Przechowuj każdy obraz w osobnym miejscu na obraz lub łącz je na jednym arkuszu. |
| **Co z dużymi tabelami przestawnymi powodującymi obciążenie pamięci?** | Użyj `ImageOrPrintOptions` z niższym DPI lub eksportuj do JPEG, aby zmniejszyć rozmiar tablicy bajtów. |
| **Czy muszę coś zwalniać?** | Obiekty Aspose są zarządzane; instrukcja `using` nie jest wymagana, ale możesz objąć `Workbook` w `using`, jeśli chcesz deterministyczne czyszczenie. |
| **Czy to działa z .NET Core?** | Tak. Aspose.Cells obsługuje .NET Core, .NET 5/6 oraz .NET Framework. Wystarczy odwołać odpowiedni pakiet NuGet. |

---

## Wskazówki i dobre praktyki

- **Waliduj ścieżki**: Używaj `Path.Combine` i `Environment.GetFolderPath`, aby uniknąć twardo zakodowanych separatorów.
- **Obsługa błędów**: Owiń całą zawartość `Main` w `try/catch` i loguj `Exception.Message` w skryptach produkcyjnych.
- **Projekt szablonu**: Umieść przezroczysty kształt obrazu tam, gdzie ma się pojawić obraz tabeli przestawnej; zachowuje to szerokości kolumn i wysokości wierszy.
- **Wydajność**: Jeśli potrzebujesz jedynie obrazu, możesz pominąć zapisywanie skoroszytu i zapisać `pivotImage` do osobnego pliku PNG.

---

## Zakończenie

Teraz wiesz **jak odświeżyć tabelę przestawną** w C#, wyeksportować odświeżony widok jako obraz oraz **wstawić obraz do arkusza** bezproblemowo. Kompletny proces – ładowanie skoroszytu, ustawianie opcji eksportu, odświeżanie tabeli, konwersja do PNG i zapisywanie pliku – obejmuje cały przepływ, o który pytałeś.

Gotowy na kolejny krok? Spróbuj połączyć **how to export pivot** z przetwarzaniem wsadowym wielu plików lub zbadaj **refresh pivot table code** dla dynamicznych źródeł danych, takich jak bazy danych czy pliki CSV. Ten sam wzorzec się sprawdza: ładowanie, odświeżanie, eksport, wstawianie, zapisywanie.

Miłego kodowania i niech Twoje automatyzacje Excel pozostaną świeże i idealnie przedstawione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}