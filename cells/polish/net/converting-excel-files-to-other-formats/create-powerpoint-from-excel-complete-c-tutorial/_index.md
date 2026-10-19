---
category: general
date: 2026-02-21
description: Szybko twórz prezentacje PowerPoint z Excela. Dowiedz się, jak wyeksportować
  Excel do PowerPoint z edytowalnym tekstem i wykresami przy użyciu Aspose.Cells w
  zaledwie kilku linijkach C#.
draft: false
keywords:
- create powerpoint from excel
- export excel to powerpoint
- export editable text
- export excel chart powerpoint
- convert excel chart powerpoint
language: pl
og_description: Utwórz prezentację PowerPoint z Excela z edytowalnym tekstem i wykresami.
  Postępuj zgodnie z tym szczegółowym przewodnikiem, aby wyeksportować Excel do PowerPoint
  przy użyciu Aspose.Cells.
og_title: Utwórz PowerPoint z Excela – Przewodnik krok po kroku w C#
tags:
- C#
- Aspose.Cells
- PowerPoint
- Excel Automation
title: Utwórz PowerPoint z Excela – Kompletny samouczek C#
url: /pl/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-complete-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz PowerPoint z Excela – Kompletny samouczek C#

Czy kiedykolwiek potrzebowałeś **create PowerPoint from Excel**, ale nie wiedziałeś, którego API użyć? Nie jesteś sam. Wielu programistów napotyka problem, gdy chcą przekształcić arkusz pełen danych w elegancką prezentację, szczególnie gdy potrzebują, aby pola tekstowe pozostały edytowalne po konwersji.  

W tym przewodniku pokażemy, jak **export Excel to PowerPoint**, zachowując edytowalny tekst, wierność wykresów i układ — wszystko przy użyciu kilku linijek C#. Po zakończeniu będziesz mieć gotowy plik PPTX, który możesz dostosować w PowerPoint tak, jak każdą ręcznie stworzoną slajd.

## Czego się nauczysz

- Jak wczytać skoroszyt Excel zawierający wykresy i kształty.  
- Jak skonfigurować `PresentationExportOptions`, aby pola tekstowe pozostały edytowalne (`export editable text`).  
- Jak faktycznie **export Excel chart PowerPoint** i uzyskać czystą prezentację.  
- Małe wariacje, które możesz zastosować, gdy potrzebujesz **convert Excel chart PowerPoint** dla różnych ustawień strony lub wielu arkuszy.  

### Wymagania wstępne

- Środowisko programistyczne .NET (Visual Studio 2022 lub nowsze).  
- Aspose.Cells for .NET (bezpłatna wersja próbna lub licencjonowana).  
- Plik Excel (`ChartWithShape.xlsx`) zawierający przynajmniej jeden wykres i kształt, który chcesz zachować jako edytowalny.  

Jeśli masz te elementy, zanurzmy się — bez zbędnych wstępów, tylko praktyczne, działające rozwiązanie.

## Utwórz PowerPoint z Excela – Krok po kroku

Poniżej każdego kroku zamieścimy zwięzły fragment kodu, wyjaśnimy **dlaczego** to robimy i wskażemy typowe pułapki. Śmiało kopiuj‑wklej pełny przykład na końcu strony.

### Krok 1: Wczytaj skoroszyt Excel

Najpierw musimy załadować źródłowy skoroszyt do pamięci. Aspose.Cells odczytuje plik i buduje bogaty model obiektowy, którym możemy manipulować.

```csharp
// Step 1: Load the Excel workbook that contains the chart and shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");

// Quick sanity check – make sure the workbook actually loaded
if (workbook.Worksheets.Count == 0)
    throw new InvalidOperationException("The workbook appears to be empty.");
```

**Dlaczego to ważne:**  
Wczytanie skoroszytu jest fundamentem. Jeśli ścieżka do pliku jest nieprawidłowa lub skoroszyt jest uszkodzony, wszystkie kolejne kroki `export excel to powerpoint` zakończą się niepowodzeniem. Sprawdzenie poprawności daje wczesny feedback zamiast niejasnego „file not found” później.

### Krok 2: Przygotuj opcje eksportu

Aspose.Cells udostępnia obiekt `PresentationExportOptions`, który kontroluje wygląd PPTX. To tutaj decydujesz, czy tekst ma pozostać edytowalny.

```csharp
// Step 2: Create export options for PowerPoint conversion
PresentationExportOptions exportOptions = new PresentationExportOptions();

// Optional: tweak the slide size (default is 10in x 7.5in)
exportOptions.SlideSize = new SizeF(10, 7.5f);
```

**Dlaczego to ważne:**  
Bez konfiguracji `PresentationExportOptions` biblioteka używa domyślnych ustawień, które mogą nie pasować do Twojego szablonu slajdów firmowych. Ustawienie rozmiaru slajdu z góry eliminuje potrzebę ręcznego skalowania później.

### Krok 3: Włącz edytowalne pola tekstowe

Magiczna flaga `ExportEditableTextBoxes` mówi Aspose.Cells, aby zachował wszystkie kształty tekstowe jako pola tekstowe PowerPoint, a nie jako statyczne obrazy.

```csharp
// Step 3: Enable editability of text boxes in the resulting presentation
exportOptions.ExportEditableTextBoxes = true;
```

**Dlaczego to ważne:**  
Jeśli pominiesz tę linię, wynikowy PPTX będzie zawierał rasteryzowany tekst — nie będziesz mógł edytować etykiety ani podpisu w PowerPoint. Ustawienie `export editable text` jest kluczem do naprawdę wielokrotnego użytku prezentacji.

### Krok 4: Eksportuj arkusz do PPTX

Teraz faktycznie zapisujemy plik PPTX. Możesz wybrać dowolny arkusz; w przykładzie używamy pierwszego (`Worksheets[0]`).

```csharp
// Step 4: Export the first worksheet's page setup to a PPTX file
workbook.Worksheets[0].PageSetup.SaveToPptx("YOUR_DIRECTORY/Result.pptx", exportOptions);
```

**Dlaczego to ważne:**  
`SaveToPptx` respektuje ustawienia strony (marginesy, orientację) zdefiniowane w Excelu, więc slajd odzwierciedla układ, który już zaprojektowałeś. To sedno **export excel chart powerpoint**.

### Krok 5: Zweryfikuj wynik (opcjonalnie, ale zalecane)

Po konwersji otwórz wygenerowany `Result.pptx` w PowerPoint i sprawdź:

1. Czy wykresy są wyraźne i zachowują serie danych.  
2. Czy pola tekstowe są zaznaczalne i edytowalne.  
3. Czy rozmiar slajdu odpowiada Twoim oczekiwaniom.

Jeśli coś wygląda nie tak, wróć do `exportOptions` — na przykład możesz ustawić `exportOptions.IncludePrintArea = true`, aby uwzględnić nazwany obszar wydruku.

```csharp
// Optional: open the PPTX automatically (requires System.Diagnostics)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/Result.pptx",
    UseShellExecute = true
});
```

### Krok 6: Zaawansowane wariacje (eksport wielu arkuszy)

Często chcesz **convert excel chart powerpoint** dla kilku arkuszy jednocześnie. Przejdź pętlą po kolekcji i nadaj każdemu slajdowi unikalną nazwę:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outputPath = $"YOUR_DIRECTORY/Result_Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(outputPath, exportOptions);
}
```

**Pro tip:** Jeśli potrzebujesz wszystkich arkuszy w *jednym* PPTX, utwórz nowy obiekt `Presentation`, zaimportuj każdy slajd, a następnie zapisz raz. To nieco bardziej skomplikowane, ale pozwala uniknąć wielu plików.

## Pełny działający przykład

Oto cały program, który możesz wkleić do aplikacji konsolowej i od razu uruchomić.

```csharp
using System;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Export;

class Program
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");
        if (workbook.Worksheets.Count == 0)
        {
            Console.WriteLine("Workbook is empty – aborting.");
            return;
        }

        // 2️⃣ Set up export options
        PresentationExportOptions exportOptions = new PresentationExportOptions
        {
            SlideSize = new SizeF(10, 7.5f),          // optional custom size
            ExportEditableTextBoxes = true           // <‑‑ keep text boxes editable
        };

        // 3️⃣ Export first worksheet
        string outputPath = "YOUR_DIRECTORY/Result.pptx";
        workbook.Worksheets[0].PageSetup.SaveToPptx(outputPath, exportOptions);
        Console.WriteLine($"PowerPoint created at: {outputPath}");

        // 4️⃣ Open the result automatically (Windows only)
        try
        {
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = outputPath,
                UseShellExecute = true
            });
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not open PPTX automatically: {ex.Message}");
        }
    }
}
```

**Oczekiwany rezultat:**  
Po otwarciu `Result.pptx` zobaczysz slajd, który odzwierciedla układ arkusza Excel. Każdy wykres umieszczony w Excelu pojawia się jako natywny wykres PowerPoint, a podpis dodany jako kształt staje się w pełni edytowalnym polem tekstowym.

## Częste pytania i przypadki brzegowe

- **Czy to działa z skoroszytami zawierającymi makra (`.xlsm`)?**  
  Tak. Aspose.Cells odczytuje makra, ale ich nie wykonuje. Proces konwersji ignoruje VBA, więc nadal otrzymasz zawartość wizualną.

- **Co jeśli mój arkusz zawiera wiele wykresów?**  
  Wszystkie widoczne wykresy zostaną przeniesione na ten sam slajd. Jeśli potrzebujesz każdy wykres na osobnym slajdzie, podziel arkusz lub użyj pętli pokazanej w Kroku 6.

- **Czy mogę zachować własne motywy PowerPoint?**  
  Nie bezpośrednio podczas eksportu. Po konwersji możesz zastosować motyw w PowerPoint lub programowo za pomocą Aspose.Slides.

- **Czy istnieje sposób, aby wyeksportować tylko wybrany zakres?**  
  Ustaw nazwany obszar wydruku w Excelu (`Page Layout → Print Area`) i włącz `exportOptions.IncludePrintArea = true`.

## Zakończenie

Teraz wiesz, jak **create PowerPoint from Excel** przy użyciu Aspose.Cells, mając pełną kontrolę nad edytowalnym tekstem, wiernością wykresów i rozmiarem slajdów. Krótki fragment kodu, który udostępniliśmy, obsługuje najczęstszy scenariusz, a dodatkowe wskazówki dają elastyczność, gdy musisz **export excel to powerpoint** dla wielu arkuszy lub niestandardowych układów.  

Gotowy na kolejny krok? Spróbuj połączyć to podejście z **Aspose.Slides**, aby programowo dodać przejścia, notatki prelegenta lub nawet osadzić wygenerowane slajdy w większej prezentacji. Albo eksperymentuj z konwersją całego skoroszytu na wieloslajdową prezentację — idealną do zautomatyzowanych potoków raportowania.

Masz pytania lub odkryłeś sprytny trik? zostaw komentarz poniżej i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}