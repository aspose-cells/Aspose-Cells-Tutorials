---
category: general
date: 2026-02-26
description: Eksportuj wykres do PowerPointa z Excela przy użyciu C#. Dowiedz się,
  jak konwertować Excel na PowerPoint, zapisać Excel jako PowerPoint i zachować edytowalność
  kształtów.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: pl
og_description: Eksportuj wykres do PowerPointa z Excela przy użyciu C#. Ten przewodnik
  pokazuje, jak przekonwertować Excel na PowerPoint, zapisać skoroszyt jako PPTX i
  zachować edytowalne kształty.
og_title: Eksport wykresu do PowerPointa w C# – Pełny samouczek programistyczny
tags:
- Aspose.Cells
- C#
- Office Automation
title: Eksport wykresu do PowerPointa przy użyciu C# – Kompletny przewodnik krok po
  kroku
url: /pl/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksport wykresu do PowerPoint – Kompletny samouczek programistyczny

Zastanawiałeś się kiedyś, jak **wyeksportować wykres do PowerPoint** bez utraty możliwości edycji? W wielu scenariuszach raportowych potrzebny jest żywy wykres w prezentacji, a ręczne kopiowanie i wklejanie jest uciążliwe. Dobra wiadomość: możesz to zrobić programowo, używając kilku linijek C#.

W tym przewodniku przejdziemy krok po kroku przez cały proces: od wczytania skoroszytu Excel zawierającego wykres z polem tekstowym, przez skonfigurowanie eksportu tak, aby pola tekstowe i kształty pozostały edytowalne, aż po zapis wyniku jako plik **PowerPoint**. Na koniec dowiesz się, jak **konwertować Excel do PowerPoint**, **zapisać Excel jako PowerPoint**, a także jak dostosować opcje w sytuacjach brzegowych.

## Czego będziesz potrzebować

- **Aspose.Cells for .NET** (wersja 23.10 lub nowsza). To biblioteka, która sprawia, że konwersja jest bezproblemowa.
- **.NET 6+** runtime – dowolny aktualny SDK.
- Prosty plik Excel (`ChartWithTextbox.xlsx`) zawierający przynajmniej jeden wykres i pole tekstowe.
- Visual Studio lub ulubione IDE.

Nie są wymagane dodatkowe pakiety NuGet poza Aspose.Cells, ale podstawowa znajomość składni C# na pewno pomoże.

## Eksport wykresu do PowerPoint – Krok po kroku

Poniżej dzielimy rozwiązanie na dyskretne, łatwe do śledzenia kroki. Każdy krok zawiera dokładny kod, którego potrzebujesz, oraz krótki akapit „dlaczego”, wyjaśniający logikę.

### Krok 1: Wczytaj skoroszyt Excel zawierający wykres

Najpierw musimy wczytać plik źródłowy do pamięci. Użycie klasy `Workbook` z Aspose.Cells odczytuje cały arkusz, w tym wykresy, obrazy i osadzone obiekty.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Dlaczego to ważne:* Jeśli skoroszyt zostanie otwarty bez poprawnego podania ścieżki, otrzymasz `FileNotFoundException`. Szybka weryfikacja zapobiega późniejszemu eksportowi pustego slajdu.

### Krok 2: Przygotuj opcje prezentacji, aby kształty pozostały edytowalne

Aspose.Cells pozwala zdecydować, czy pola tekstowe, kształty i sam wykres pozostaną **edytowalne** po eksporcie. Ustawienie `ExportTextBoxes` i `ExportShapes` na `true` zachowuje te obiekty jako natywne elementy PowerPoint, a nie spłaszczone obrazy.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Dlaczego to ważne:* Jeśli pozostawisz te flagi w domyślnych wartościach (`false`), otrzymany slajd będzie zawierał bitmapę wykresu, co uniemożliwi późniejszą edycję serii lub zmianę podpisu. Włączenie obu opcji daje prawdziwy wykres PowerPoint, zachowujący się tak, jakby został narysowany ręcznie.

### Krok 3: Konwertuj Excel do PowerPoint i zapisz plik

Teraz wywołujemy metodę `Save`, przekazując enum `SaveFormat.Pptx` oraz skonfigurowane wcześniej opcje. Biblioteka zajmuje się przetłumaczeniem obiektu wykresu Excel na kształt wykresu PowerPoint.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Dlaczego to ważne:* Wywołanie `Save` wykonuje całą ciężką pracę – mapowanie serii Excel na serie PowerPoint, zachowanie formatowania osi oraz kopiowanie powiązanych pól tekstowych. Po wykonaniu tej linii będziesz mieć w pełni edytowalny plik `.pptx`, gotowy do otwarcia w Microsoft PowerPoint.

### Zweryfikuj wynik

Otwórz `Result.pptx` w PowerPoint. Powinieneś zobaczyć slajd zawierający:

- Oryginalny wykres, nadal połączony z danymi (możesz dwukrotnie kliknąć, aby edytować serie).
- Każde pole tekstowe, które znajdowało się w arkuszu Excel, teraz jako natywne pole tekstowe PowerPoint.
- Układ slajdu jest wybierany automatycznie (zwykle pusty slajd).

Jeśli zauważysz brakujące elementy, sprawdź, czy źródłowy skoroszyt faktycznie zawierał widoczne obiekty oraz czy `ExportTextBoxes` / `ExportShapes` zostały ustawione na `true`.

### Konwertuj Excel do PowerPoint: Obsługa wielu arkuszy

Często skoroszyt zawiera więcej niż jeden arkusz, każdy z własnym wykresem. Domyślnie Aspose.Cells wyeksportuje **wszystkie** wykresy z **wszystkich** arkuszy do osobnych slajdów. Jeśli potrzebujesz tylko wybranej części, możesz je odfiltrować przed zapisem:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Wskazówka:* Ustawienie `chart.IsVisible = false` jest tańsze niż całkowite usunięcie wykresu i pozwala na włączanie/wyłączanie go bez modyfikacji pliku źródłowego.

### Zapisz Excel jako PowerPoint – Dostosowanie rozmiaru slajdu

Domyślny rozmiar slajdu w PowerPoint to 10 cali na 5,63 cala. Jeśli wykres wygląda na zbyt ciasny, możesz zmienić wymiary slajdu za pomocą obiektu `PresentationOptions`:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

Teraz wyeksportowany wykres będzie miał więcej przestrzeni, a pola tekstowe zachowają pierwotny układ.

### Jak konwertować Excel do PPT: Radzenie sobie z ukrytymi obiektami

Ukryte wiersze, kolumny lub kształty mogą czasem przedostać się do eksportu. Aby je usunąć, wykonaj szybkie czyszczenie przed zapisem:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

Ten krok nie zawsze jest konieczny, ale zapobiega nieoczekiwanym lukom w finalnej prezentacji.

### Zapisz skoroszyt jako PPTX – Pełny działający przykład

Łącząc wszystko razem, oto gotowy do uruchomienia program konsolowy demonstrujący cały przepływ:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

Uruchomienie tego programu utworzy `Result.pptx` z edytowalnym wykresem i polem tekstowym – dokładnie to, czego oczekujesz przy ręcznym **zapisaniu skoroszytu jako pptx**.

![Export chart to PowerPoint example](/images/export-chart-to-powerpoint.png "Export chart to PowerPoint – edytowalny slajd")

## Często zadawane pytania i przypadki brzegowe

**Co zrobić, gdy plik Excel zawiera wykres z zewnętrznym źródłem danych?**  
Aspose.Cells kopiuje *obecne* wartości danych do wykresu PowerPoint. Nie zachowuje **zewnętrznego** połączenia, ponieważ PowerPoint nie może odwoływać się do połączenia danych Excel w ten sam sposób. Jeśli potrzebujesz aktualizacji na żywo, rozważ osadzenie oryginalnego pliku Excel w PPTX jako obiekt OLE.

**Czy mogę wyeksportować wykres używający własnego motywu?**  
Tak. Biblioteka stara się mapować kolory motywu Excel na sloty motywu PowerPoint. W przypadku bardzo niestandardowych palet może być konieczna korekta kolorów po eksporcie przy użyciu własnego API PowerPoint (np. Aspose.Slides).

**Czy istnieje limit liczby wykresów?**  
Praktycznie brak – Aspose.Cells strumieniuje dane, więc nawet skoroszyt z dziesiątkami wykresów zostanie wyeksportowany, choć rozmiar pliku PPTX rośnie liniowo.

**Czy potrzebna jest licencja na Aspose.Cells?**  
Darmowa wersja ewaluacyjna działa, ale dodaje znak wodny na pierwszym slajdzie. Do użytku produkcyjnego należy uzyskać pełną licencję, aby usunąć znak wodny i odblokować pełną wydajność.

## Podsumowanie

Omówiliśmy, jak **wyeksportować wykres do PowerPoint** przy użyciu C#, przedstawiliśmy dokładny kod do wczytania skoroszytu Excel, skonfigurowania `PresentationOptions` tak, aby pola tekstowe i kształty pozostały edytowalne, oraz zapisania wyniku jako `.pptx`. Dowiedziałeś się także, jak **konwertować Excel do PowerPoint**, **zapisać Excel jako PowerPoint**, oraz jak odpowiedzieć na pytanie „**jak przekonwertować Excel do ppt**” przy pomocy kompletnego, uruchamialnego przykładu.

## Co dalej?

- **Zapisz skoroszyt jako PPTX** z wieloma slajdami: iteruj po każdym arkuszu i wywołuj `Save` z `PresentationOptions` dla każdego.
- Poznaj **Aspose.Slides**, jeśli potrzebujesz programowo modyfikować wygenerowany PPTX (dodawać przejścia, notatki prelegenta itp.).
- Spróbuj wyeksportować **wykresy przestawne** lub **wykresy 3‑D** – te same opcje działają, choć może być konieczna dodatkowa korekta formatowania osi.

Jeśli napotkasz jakiekolwiek problemy, zostaw komentarz poniżej lub sprawdź oficjalną dokumentację Aspose.Cells pod kątem najnowszych zmian API. Powodzenia w kodowaniu i ciesz się przekształcaniem wykresów Excel w eleganckie prezentacje PowerPoint za pomocą kilku linijek C#!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}