---
category: general
date: 2026-01-14
description: Jak skopiować tabelę przestawną przy użyciu Aspose.Cells oraz nauczyć
  się konwertować Excel na PPTX, kopiować zakres do innego skoroszytu i uczynić pole
  tekstowe edytowalne w PPTX w jednym samouczku.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: pl
og_description: Jak skopiować tabelę przestawną, a następnie przekonwertować Excel
  na PPTX, skopiować zakres do innego skoroszytu i uczynić pole tekstowe edytowalne
  w PPTX — wszystko przy użyciu Aspose.Cells.
og_title: Jak skopiować tabelę przestawną w C# – Kompletny przewodnik od Excela do
  PPTX
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Jak skopiować tabelę przestawną w C# – konwertować Excel na PPTX, kopiować
  zakres i uczynić pole tekstowe edytowalnym
url: /pl/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skopiować tabelę przestawną w C# – Kompletny przewodnik Excel do PPTX

Kopiowanie tabeli przestawnej z jednego skoroszytu do drugiego jest częstym pytaniem, gdy automatyzujesz raporty oparte na Excelu. W tym samouczku przeprowadzimy trzy scenariusze z życia wzięte przy użyciu **Aspose.Cells for .NET**: kopiowanie zakresu tabeli przestawnej, eksportowanie arkusza do pliku PPTX z edytowalnym polem tekstowym oraz wypełnianie pojedynczej komórki tablicą JSON za pomocą Smart Markers.  

Zobaczysz także, jak **konwertować Excel do PPTX**, **kopiować zakres do innego skoroszytu** i **tworzyć edytowalne pole tekstowe w PPTX** bez uszkadzania formatowania. Po zakończeniu będziesz mieć gotowy kod, który możesz wkleić do dowolnego projektu .NET.

> **Pro tip:** Wszystkie przykłady dotyczą Aspose.Cells 23.12, ale te same koncepcje mają zastosowanie do wcześniejszych wersji z niewielkimi zmianami w API.

![Diagram przedstawiający, jak kopiowana jest tabela przestawna, arkusz eksportowany do PPTX oraz wstawiana tablica JSON – przepływ pracy kopiowania tabeli przestawnej](how-to-copy-pivot-table-diagram.png)

---

## Czego będziesz potrzebować

- Visual Studio 2022 (lub dowolne IDE C#)
- .NET 6.0 lub nowszy runtime
- Aspose.Cells for .NET NuGet package  
  ```bash
  dotnet add package Aspose.Cells
  ```
- Dwa przykładowe pliki Excel (`source.xlsx`, `chartWithTextbox.xlsx`) umieszczone w folderze, którym zarządzasz (zamień `YOUR_DIRECTORY` na swoją rzeczywistą ścieżkę).

Nie są wymagane dodatkowe biblioteki; ta sama biblioteka `Aspose.Cells` obsługuje Excel, PPTX i Smart Markery.

## Jak skopiować tabelę przestawną i zachować jej dane

Kiedy kopiujesz zakres zawierający tabelę przestawną, domyślne zachowanie to wklejenie tylko **wartości**. Aby zachować definicję przestawnej, musisz włączyć flagę `CopyPivotTable`.

### Krok po kroku

1. **Załaduj skoroszyt źródłowy**, który zawiera tabelę przestawną.  
2. **Utwórz pusty skoroszyt docelowy** – będzie on odbierał skopiowany zakres.  
3. **Użyj `CopyRange` z `CopyPivotTable = true`**, aby definicja przestawnej przeszła wraz z danymi.  
4. **Zapisz plik docelowy** w dowolnym miejscu.

#### Pełny przykład kodu

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Dlaczego to działa:**  
`CopyOptions.CopyPivotTable` instruuje Aspose.Cells, aby sklonował podstawowy obiekt `PivotTable`, a nie tylko jego wyrenderowane wartości. Skoroszyt docelowy zawiera teraz w pełni funkcjonalną przestawną, którą możesz odświeżać lub modyfikować programowo.

**Przypadek brzegowy:** Jeśli skoroszyt źródłowy używa zewnętrznych źródeł danych, może być konieczne osadzenie danych lub dostosowanie ciągów połączeń po skopiowaniu, w przeciwnym razie przestawna wyświetli „#REF!”.

## Konwertowanie Excel do PPTX i tworzenie edytowalnego pola tekstowego

Eksportowanie arkusza do PowerPointu jest przydatne do tworzenia prezentacji bezpośrednio z danych. Domyślnie wyeksportowane pole tekstowe staje się statycznym kształtem, ale ustawienie `IsTextBoxEditable` odwraca to zachowanie.

### Krok po kroku

1. **Otwórz skoroszyt**, który zawiera wykres i pole tekstowe, które chcesz wyeksportować.  
2. **Skonfiguruj `ImageOrPrintOptions`** z `SaveFormat = SaveFormat.Pptx`.  
3. **Zdefiniuj obszar drukowania**, który obejmuje pole tekstowe.  
4. **Włącz `IsTextBoxEditable`**, aby tekst można było edytować po otwarciu pliku PPTX.  
5. **Zapisz plik PPTX**.

#### Pełny przykład kodu

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Rezultat:** Otwórz `result.pptx` w PowerPoint – pole tekstowe umieszczone w Excelu będzie teraz zwykłym polem tekstowym, w które możesz wpisywać. Nie ma potrzeby ręcznego odtwarzania go.

**Częsty błąd:** Jeśli arkusz zawiera scalone komórki, które przecinają obszar drukowania, wynikowy slajd może się przesunąć. Dostosuj obszar drukowania lub rozłącz scalone komórki przed eksportem.

## Kopiowanie zakresu do innego skoroszytu przy użyciu Smart Markers (JSON → pojedyncza komórka)

Czasami trzeba osadzić tablicę JSON w jednej komórce Excela, na przykład przy przekazywaniu danych do systemów downstream, które oczekują ciągu JSON. Smart Markery Aspose.Cells mogą serializować tablicę jako pojedynczą komórkę, gdy ustawisz `ArrayAsSingle = true`.

### Krok po kroku

1. **Załaduj skoroszyt szablonu**, który zawiera placeholder Smart Marker (np. `&=Items.Name`).  
2. **Przygotuj obiekt danych** – anonimowy typ z tablicą `Items`.  
3. **Utwórz `SmartMarkerProcessor`** i zastosuj dane z `ArrayAsSingle`.  
4. **Zapisz wypełniony skoroszyt**.

#### Pełny przykład kodu

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Wyjaśnienie:**  
Gdy `ArrayAsSingle` jest true, Aspose.Cells konkatenatuje każdy element `Items.Name` w ciąg w stylu JSON (`["A","B"]`) i zapisuje go w komórce, w której znajdował się smart marker. To zapobiega tworzeniu osobnego wiersza dla każdego elementu tablicy.

**Kiedy używać:** Idealne do eksportowania tabel konfiguracyjnych, ładunków API lub dowolnego scenariusza, w którym odbiorca oczekuje zwartego ciągu JSON zamiast układu tabelarycznego.

## Dodatkowe wskazówki i obsługa przypadków brzegowych

| Scenario | What to Watch For | Suggested Fix |
|----------|-------------------|---------------|
| **Duże tabele przestawne** | Wzrost zużycia pamięci przy kopiowaniu ogromnych pamięci podręcznych przestawnych. | Use `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` before loading. |
| **Eksportowanie do PPTX z obrazami** | Obrazy mogą być rasteryzowane przy niskim DPI. | Set `pptxOptions.ImageResolution = 300` for sharper slides. |
| **Formatowanie JSON w Smart Marker** | Znaki specjalne (`"` , `\`) psują JSON. | Escape them manually or use `JsonSerializer` to pre‑serialize before feeding Smart Markers. |
| **Kopiowanie zakresu między różnymi wersjami Excel** | Starsze pliki `.xls` mogą tracić formatowanie. | Save the destination as `.xlsx` to preserve modern features. |

## Podsumowanie – Jak skopiować tabelę przestawną i zrobić znacznie więcej

Zaczęliśmy od odpowiedzi na pytanie **jak skopiować tabelę przestawną**, zachowując jej funkcjonalność, następnie pokazaliśmy, jak **konwertować Excel do PPTX**, **tworzyć edytowalne pole tekstowe w PPTX**, a w końcu jak **skopiować zakres do innego skoroszytu** przy użyciu Smart Markers, aby osadzić tablicę JSON w jednej komórce.  

Wszystkie trzy fragmenty kodu są samodzielne; możesz wkleić je do nowej aplikacji konsolowej, dostosować ścieżki plików i uruchomić już dziś.

## Co dalej?

- **Zbadaj inne formaty eksportu** – Aspose.Cells obsługuje także PDF, XPS i HTML.  
- **Odświeżaj tabele przestawne programowo** używając `PivotTable.RefreshData()` po skopiowaniu.  
- **Łącz Smart Markery z wykresami**, aby generować dynamiczne pulpity nawigacyjne, które aktualizują się automatycznie.  

Jeśli jesteś zainteresowany **zapisywaniem skoroszytu jako PPTX** z niestandardowymi układami slajdów, zapoznaj się z dokumentacją Aspose.Cells dotyczącą `SlideOptions`.  

Śmiało eksperymentuj — zmień obszar drukowania, wypróbuj różne `CopyOptions` lub podaj bardziej złożony ładunek JSON. API jest wystarczająco elastyczne dla większości potoków raportowania.

### Najczęściej zadawane pytania

**Q: Czy `CopyPivotTable` kopiuje także segmentatory?**  
A: Nie bezpośrednio. Segmentatory są oddzielnymi obiektami; po skopiowaniu trzeba je odtworzyć lub skopiować za pomocą kolekcji `Worksheet.Shapes`.

**Q: Czy mogę wyeksportować wiele arkuszy do jednej prezentacji PPTX?**  
A: Tak. Przejdź pętlą po każdym arkuszu, wywołaj `Save` z tymi samymi `ImageOrPrintOptions` i ustaw `pptxOptions.StartSlideNumber`, aby kontynuować numerację.

**Q: Co jeśli moja tablica JSON zawiera zagnieżdżone obiekty?**  
A: Ustaw `ArrayAsSingle = false` i użyj niestandardowego szablonu, który iteruje po

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}