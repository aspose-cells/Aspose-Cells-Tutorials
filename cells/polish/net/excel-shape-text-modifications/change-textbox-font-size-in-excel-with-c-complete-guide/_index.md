---
category: general
date: 2026-05-30
description: Zmień rozmiar czcionki pola tekstowego w Excelu przy użyciu C#. Dowiedz
  się, jak szybko modyfikować czcionkę pola tekstowego w Excelu, korzystając z kodu
  krok po kroku.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: pl
og_description: Zmień rozmiar czcionki pola tekstowego w Excelu przy użyciu C#. Ten
  przewodnik pokazuje, jak bezpiecznie i efektywnie modyfikować czcionkę pola tekstowego
  w Excelu.
og_title: Zmień rozmiar czcionki pola tekstowego w Excelu przy użyciu C# – Pełny poradnik
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: Zmiana rozmiaru czcionki w polu tekstowym w Excelu przy użyciu C# – Kompletny
  przewodnik
url: /pl/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zmienianie rozmiaru czcionki w polu tekstowym w Excelu przy użyciu C# – Kompletny przewodnik

Potrzebujesz **zmienić rozmiar czcionki w polu tekstowym** w arkuszu Excel przy użyciu C#? Jesteś we właściwym miejscu. Niezależnie od tego, czy generujesz raporty, tworzysz pulpit nawigacyjny, czy po prostu dopracowujesz szablon, dostosowanie wyglądu pola tekstowego może sprawić, że Twój arkusz będzie wyglądał znacznie bardziej profesjonalnie.

W tym samouczku pokażemy również, jak **modyfikować czcionkę pola tekstowego w Excelu** nie tylko pod kątem rozmiaru — pomyśl o rodzinie czcionek, pogrubieniu i obsłudze wielu kształtów. Po zakończeniu będziesz mieć gotowy fragment kodu, który obejmuje każdy etap procesu, od otwarcia skoroszytu po czyszczenie obiektów COM. Bez zbędnych wstępów, tylko praktyczny kod, który możesz od razu wkleić do swojego projektu.

## Wymagania wstępne — Czego będziesz potrzebować

Zanim zanurkujemy, upewnij się, że masz następujące elementy na swoim komputerze:

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| **.NET 6+** (or .NET Framework 4.7.2+) | Zapewnia kompilator C# i środowisko uruchomieniowe. |
| **Microsoft.Office.Interop.Excel** NuGet package | Dostarcza typy interfejsu COM potrzebne do komunikacji z Excelem. |
| **Excel installed** (any recent version) | Warstwa Interop działa tylko wtedy, gdy aplikacja Office jest zainstalowana. |
| **Basic C# knowledge** | Będziesz mógł łatwo podążać za instrukcją, ale wyjaśnimy każdy wiersz. |

Jeśli którekolwiek z nich brakuje, zatrzymaj się teraz i zainstaluj je; dalsza część przewodnika zakłada, że są dostępne.

## Krok 1: Konfiguracja projektu i importowanie przestrzeni nazw

Na początek—utwórz nową aplikację konsolową (lub zintegrować ją z istniejącą) i zaimportuj przestrzeń nazw interop.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Wskazówka:** Jeśli celujesz w .NET 6+, dodaj pakiet `Microsoft.Office.Interop.Excel` za pomocą `dotnet add package Microsoft.Office.Interop.Excel`. To zapewnia prawidłowe rozpoznanie aliasu `Excel`.

## Krok 2: Otwórz skoroszyt i pobierz docelowy arkusz

Teraz musimy uruchomić Excel, otworzyć plik i wskazać arkusz, który zawiera pole tekstowe. Umieszczenie tego w bloku `try/finally` zapewnia zwolnienie obiektów COM nawet w przypadku błędów.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Dlaczego to ważne

Otwieranie skoroszytu przez COM daje nam żywy model obiektowy — co oznacza, że każda wprowadzona zmiana od razu odzwierciedla się w pliku. Ustawienie `Visible = false` przyspiesza działanie i zapobiega pojawianiu się okien podczas automatyzacji.

## Krok 3: Pobierz kształt pola tekstowego

Excel traktuje pola tekstowe jako obiekty `Shape` w kolekcji `Shapes`, a nie jako dedykowaną kolekcję `TextBox`. Dlatego poniższy kod wygląda nieco inaczej niż fragment, który mogłeś zobaczyć w sieci.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Uwaga:** Kolekcja `Shapes` jest indeksowana od 1, więc dodajemy `+1` do zerowego indeksu `textboxIndex`, który podajesz. Zapomnienie tego prowadzi do błędów „index out of range”, które mogą być frustrujące w debugowaniu.

## Krok 4: Zmień rozmiar czcionki (i nazwę) pola tekstowego

Tutaj w końcu **zmieniamy rozmiar czcionki pola tekstowego**. Właściwość `TextFrame2` zapewnia dostęp do opcji formatowania tekstu sformatowanego, w tym `Font.Name` i `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Dlaczego używamy `TextFrame2`

`TextFrame2` to nowszy model obiektowy wprowadzony w Office 2007. Obsługuje zaawansowane funkcje typograficzne i jest zazwyczaj bardziej niezawodny niż starszy `TextFrame`. Użycie go zapewnia, że operacja **zmiany rozmiaru czcionki pola tekstowego** działa we wszystkich nowoczesnych wersjach Excela.

## Krok 5: Zapisz, wyczyść i zweryfikuj

Po dostosowaniu czcionki musimy zapisać zmiany i zwolnić wszystkie odwołania COM. Pominięcie czyszczenia może pozostawić osierocone procesy Excel działające w tle.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Wskazówka:** Jeśli musisz **modyfikować czcionkę pola tekstowego w Excelu** na wielu arkuszach, umieść wewnętrzną logikę w pętli iterującej po `Workbook.Worksheets`. Pamiętaj tylko, aby zresetować `textboxIndex` dla każdego arkusza.

## Obsługa przypadków brzegowych — Wiele pól tekstowych i brakujące kształty

W rzeczywistych arkuszach rzadko występuje tylko jedno pole tekstowe. Poniżej dwie szybkie strategie, które możesz zastosować bez przepisywania całej metody.

### 1. Zmień *wszystkie* pola tekstowe na arkuszu

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Zidentyfikuj pole tekstowe po jego **Nazwie** zamiast indeksu

Jeśli nadałeś swojemu polu tekstowemu znaczącą nazwę (np. „TitleBox”), możesz pobrać je bezpośrednio:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Oba podejścia pozwalają **modyfikować czcionkę pola tekstowego w Excelu** precyzyjnie, niezależnie od struktury skoroszytu.

## Przegląd wizualny (opcjonalnie)

Jeśli wolisz szybki podgląd wizualny, wyobraź sobie następujący diagram:

![Zrzut ekranu pokazujący arkusz Excel z podświetlonym polem tekstowym – demonstruje, jak zmienić rozmiar czcionki w polu tekstowym](change-textbox-font-size.png)

*Alt text:* *zmiana rozmiaru czcionki w polu tekstowym w Excelu – podświetlone pole tekstowe gotowe do modyfikacji czcionki.*

## Pełny działający przykład

Łącząc wszystko razem, oto pojedynczy plik, który możesz skopiować i wkleić do projektu konsolowego i uruchomić od razu (wystarczy zaktualizować ścieżkę do pliku i nazwę arkusza).

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these parameters for your environment.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // First textbox on the sheet.
            double newFontSize = 14;       // Desired font size.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

        static void ChangeTextboxFontSize(string workbookPath,
                                          string sheetName,
                                          int textboxIndex,
                                          double newSize,
                                          string fontName)
        {
            Excel.Application xlApp = null;
            Excel.Workbook xlWorkbook = null;
            Excel.Worksheet xlWorksheet = null;

            try
            {
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## Co warto się nauczyć dalej?

- [Zmiana rozmiaru czcionki w Excelu](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [Jak dostosować rozmiar czcionki w komórkach Excela przy użyciu Aspose.Cells .NET | Kompletny przewodnik](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [Jak ustawić style czcionki w Excelu przy użyciu Aspose.Cells dla .NET (przewodnik krok po kroku)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}