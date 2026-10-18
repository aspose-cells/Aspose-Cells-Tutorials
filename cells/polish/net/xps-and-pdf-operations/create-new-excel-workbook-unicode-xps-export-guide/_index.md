---
category: general
date: 2026-05-30
description: Utwórz nowy skoroszyt Excel i dowiedz się, jak zapisywać Unicode w Excelu,
  eksportować Excel do XPS oraz wstawiać znaki specjalne w Excelu przy użyciu Aspose.Cells.
draft: false
keywords:
- create new excel workbook
- how to write unicode in excel
- export excel to xps
- write special character in excel
language: pl
og_description: Utwórz nowy skoroszyt Excela, wpisz znaki Unicode w Excelu i wyeksportuj
  go do formatu XPS, korzystając z pełnego, krok po kroku poradnika.
og_title: Utwórz nowy skoroszyt Excel – eksport Unicode i XPS
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Create new excel workbook and learn how to write unicode in excel,
    export excel to xps, and write special character in excel using Aspose.Cells.
  headline: Create New Excel Workbook – Unicode & XPS Export Guide
  type: TechArticle
- description: Create new excel workbook and learn how to write unicode in excel,
    export excel to xps, and write special character in excel using Aspose.Cells.
  name: Create New Excel Workbook – Unicode & XPS Export Guide
  steps:
  - name: Edge Cases & Tips
    text: '| Situation | How to Handle | |-----------|----------------| | The target
      font doesn’t support the variation selector | Set the cell style to a font that
      does (e.g., “Noto Sans CJK”). | | You need to write multiple Unicode strings
      quickly | Loop through an array of strings and call `PutValue` inside'
  - name: Verifying the Result
    text: "Open the generated `UnicodeDemo.out.xps` with Windows XPS Viewer. You should
      see the cell **A1** displaying the kanji **\U00020BB7** with the variant glyph
      (if your system font supports it). If the character looks like a box, double‑check
      that the font used in the worksheet supports the variation selector."
  - name: Expected Output
    text: 'When you run the program, the console prints something like:'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells writes the underlying file in the OpenXML format (`.xlsx`),
      which Excel 2007+ can read. The XPS export is independent of the Excel version.
    question: Does this work with older versions of Excel?
  - answer: "Emojis are also Unicode code points. Use the same `PutValue` method,
      e.g., `sheet.Cells[\"B2\"].PutValue(\"\U0001F600\")` for a grinning face."
    question: What if I need to write emojis?
  - answer: You can adjust the worksheet’s `PageSetup` properties before saving, such
      as `sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;`.
    question: Can I set the XPS page size?
  - answer: 'Minimal. Aspose.Cells processes strings efficiently, but if you’re handling
      millions of cells, consider batching writes or using `Cells.ImportDataTable`.
      ## Pro Tips for a Smooth Experience - **Font Embedding:** When you need the
      XPS to look identical on any machine, embed the font into the workbook'
    question: Is there a performance impact when writing many Unicode cells?
  type: FAQPage
tags:
- excel
- aspnet
- unicode
- xps
title: Utwórz nowy skoroszyt Excel – Przewodnik po eksporcie Unicode i XPS
url: /pl/net/xps-and-pdf-operations/create-new-excel-workbook-unicode-xps-export-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie nowego skoroszytu Excel – przewodnik po Unicode i eksporcie XPS

Zastanawiałeś się kiedyś, jak **utworzyć nowy skoroszyt Excel**, który poradzi sobie z ozdobnymi znakami i jednocześnie będzie możliwy do wydrukowania jako plik XPS? Nie jesteś sam. Wielu programistów napotyka problem, gdy muszą przechowywać znak Unicode — na przykład japoński kanji z selektorem wariacji — w komórce Excela, a następnie wyeksportować go jako wysokiej jakości dokument XPS.

W tym samouczku przejdziemy krok po kroku przez ten proces: **utworzymy nowy skoroszyt Excel**, pokażemy **jak zapisać Unicode w Excelu**, zademonstrujemy **eksport Excel do XPS** oraz omówimy niuanse **zapisu specjalnego znaku w Excelu**. Po zakończeniu będziesz mieć gotowy przykład kodu, jasne zrozumienie, dlaczego każdy krok ma znaczenie, oraz kilka profesjonalnych wskazówek, które pomogą uniknąć typowych pułapek.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.6+)
- Aspose.Cells for .NET (wersja trial lub licencjonowana)
- Proste IDE, takie jak Visual Studio lub VS Code
- Podstawowa znajomość C# — nic skomplikowanego, tylko standardowe instrukcje `using`

Jeśli już masz te elementy, świetnie — zaczynamy.

## Krok 1: Utworzenie nowego skoroszytu Excel przy użyciu Aspose.Cells

Pierwszą rzeczą, której potrzebujesz, jest świeży obiekt skoroszytu. Pomyśl o nim jak o czystym płótnie, na którym znajdują się wszystkie arkusze, komórki i style.

```csharp
using Aspose.Cells;

namespace ExcelUnicodeDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();

            // The workbook now contains one default worksheet (index 0)
            // You can add more sheets later if needed
        }
    }
}
```

> **Dlaczego to ważne:** Tworzenie instancji `Workbook` automatycznie dodaje domyślny arkusz, co oszczędza jedną linię kodu później. To podstawa operacji **create new excel workbook** — bez tego nic nie może się dalej wydarzyć.

## Krok 2: Dostęp do pierwszego arkusza

Gdy skoroszyt istnieje, potrzebujesz odwołania do arkusza, w którym umieścisz tekst Unicode.

```csharp
// Step 2: Get the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];
```

> **Wskazówka:** Jeśli planujesz generować wiele arkuszy, użyj `workbook.Worksheets.Add("MySheet")` i śledź indeks lub nazwę. Dla prostej demonstracji domyślny arkusz jest w zupełności wystarczający.

## Krok 3: Jak zapisać Unicode w komórkach Excel

Teraz przychodzi najciekawsza część — zapis specjalnego znaku. W tym przykładzie wstawimy znak `𠮷` z selektorem wariacji `U+FE00`. Ta kombinacja jest często używana, aby wymusić konkretną wariantę glifu.

```csharp
// Step 3: Write a character that includes a variation selector into cell A1
// The string literal uses an escaped Unicode sequence for the variation selector
sheet.Cells["A1"].PutValue("𠮷\uFE00");

// Optional: Adjust the column width so the character isn’t cut off
sheet.AutoFitColumn(0);
```

> **Co się dzieje?**  
> - `"𠮷"` to punkt kodowy Unicode spoza BMP (Basic Multilingual Plane), więc w UTF‑16 jest reprezentowany jako para surogatów.  
> - `\uFE00` to variation selector‑1. Po połączeniu wiele czcionek wyświetla nieco inny glif.  
> - `PutValue` automatycznie wykrywa typ łańcucha i zapisuje go jako wartość Unicode w komórce, spełniając wymaganie **write special character in excel**.

### Przypadki brzegowe i wskazówki

| Sytuacja | Jak postąpić |
|-----------|----------------|
| Docelowa czcionka nie obsługuje selektora wariacji | Ustaw styl komórki na czcionkę, która to robi (np. “Noto Sans CJK”). |
| Musisz szybko zapisać wiele ciągów Unicode | Przejdź pętlą po tablicy ciągów i wywołuj `PutValue` wewnątrz pętli. |
| Excel wyświetla znak � (znak zastępczy) | Sprawdź, czy plik jest zapisywany z kodowaniem UTF‑8 (Aspose.Cells robi to automatycznie). |

## Krok 4: Eksport Excel do XPS — docelowy format

Po bezpiecznym zapisaniu znaku Unicode, ostatnim elementem jest wygenerowanie dokumentu XPS. XPS zachowuje układ, czcionki i grafikę wektorową, co czyni go idealnym do drukowania lub archiwizacji.

```csharp
// Step 4: Save the workbook as an XPS document
string outputPath = @"C:\Temp\UnicodeDemo.out.xps";
workbook.Save(outputPath, SaveFormat.Xps);

// Inform the user
Console.WriteLine($"Workbook exported to XPS at: {outputPath}");
```

> **Dlaczego eksportować do XPS?** Opcja `SaveFormat.Xps` tworzy plik o stałym układzie, który odzwierciedla widok skoroszytu na ekranie. Jest to szczególnie przydatne, gdy trzeba udostępnić wersję tylko do odczytu, zachowującą dokładne formatowanie — idealne dla raportów, faktur czy dokumentów prawnych.

### Weryfikacja wyniku

Otwórz wygenerowany plik `UnicodeDemo.out.xps` w Windows XPS Viewer. Powinieneś zobaczyć komórkę **A1** wyświetlającą kanji **𠮷** z wariantem glifu (jeśli systemowa czcionka to obsługuje). Jeśli znak wygląda jak kwadrat, sprawdź, czy czcionka użyta w arkuszu obsługuje selektor wariacji.

## Pełny działający przykład

Oto cały program w jednym miejscu — skopiuj, wklej i uruchom.

```csharp
using System;
using Aspose.Cells;

namespace ExcelUnicodeDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new workbook (primary step for create new excel workbook)
            Workbook workbook = new Workbook();

            // Access the first worksheet
            Worksheet sheet = workbook.Worksheets[0];

            // Write a Unicode character with a variation selector into cell A1
            // This demonstrates how to write unicode in excel
            sheet.Cells["A1"].PutValue("𠮷\uFE00");
            sheet.AutoFitColumn(0); // Ensure the column is wide enough

            // Save as XPS (export excel to xps)
            string outputPath = @"C:\Temp\UnicodeDemo.out.xps";
            workbook.Save(outputPath, SaveFormat.Xps);

            Console.WriteLine($"Workbook exported to XPS at: {outputPath}");
            Console.WriteLine("Done! Check the XPS file to see the special character.");
        }
    }
}
```

### Oczekiwany wynik

Po uruchomieniu programu konsola wypisze coś w stylu:

```
Workbook exported to XPS at: C:\Temp\UnicodeDemo.out.xps
Done! Check the XPS file to see the special character.
```

Otwarcie pliku XPS pokaże **A1** zawierające specjalny znak **𠮷** z zastosowanym selektorem wariacji.

## Częste pytania i pułapki

**P: Czy to działa ze starszymi wersjami Excela?**  
O: Tak. Aspose.Cells zapisuje plik w formacie OpenXML (`.xlsx`), który od Excel 2007 wzwyż jest odczytywany. Eksport do XPS jest niezależny od wersji Excela.

**P: Co zrobić, jeśli muszę zapisać emoji?**  
O: Emoji to także punkty kodowe Unicode. Użyj tej samej metody `PutValue`, np. `sheet.Cells["B2"].PutValue("\U0001F600")` dla uśmiechniętej twarzy.

**P: Czy mogę ustawić rozmiar strony w XPS?**  
O: Tak, możesz dostosować właściwości `PageSetup` arkusza przed zapisem, np. `sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;`.

**P: Czy zapis wielu komórek Unicode wpływa na wydajność?**  
O: Minimalnie. Aspose.Cells efektywnie przetwarza łańcuchy, ale przy milionach komórek rozważ batchowanie zapisów lub użycie `Cells.ImportDataTable`.

## Profesjonalne wskazówki dla płynnej pracy

- **Osadzanie czcionek:** Gdy XPS ma wyglądać identycznie na każdej maszynie, osadź czcionkę w skoroszycie (`workbook.Fonts.AddFont("path/to/font.ttf")`).  
- **Zarządzanie pamięcią:** Dla dużych skoroszytów otocz `Workbook` blokiem `using` lub wywołaj `workbook.Dispose()` po zapisaniu, aby zwolnić zasoby niezarządzane.  
- **Testowanie Unicode:** Skorzystaj z internetowego eksploratora Unicode, aby kopiować‑wklejać znaki; unikniesz błędów przy ręcznym wpisywaniu par surogatów.  
- **Obsługa błędów:** Umieść wywołanie zapisu w bloku try‑catch, aby elegancko obsłużyć problemy z I/O (`DirectoryNotFoundException`, `UnauthorizedAccessException`).

## Zakończenie

Omówiliśmy wszystko, co potrzebne, aby **create new excel workbook**, **how to write unicode in excel**, **export excel to xps** oraz **write special character in excel** przy użyciu Aspose.Cells. Krok po kroku kod pokazuje pełny przepływ — od inicjalizacji skoroszytu, wstawienia glifu Unicode z selektorem wariacji, po wygenerowanie wiernego obrazu XPS.

Teraz możesz zastosować ten wzorzec do generowania wielojęzycznych raportów, zachowania dokładnego układu do archiwizacji lub po prostu zaimponować współpracownikom czystym obsługiwaniem Unicode. Chcesz iść dalej? Spróbuj dodać obrazy, stylizować komórki bogatymi czcionkami lub generować wiele arkuszy w jednym pliku XPS. Nie ma granic.

Masz pytanie lub ciekawy przypadek użycia? zostaw komentarz poniżej i powodzenia w kodowaniu!

![Screenshot of the XPS output showing the special Unicode character – create new excel workbook](/images/xps-unicode-output.png)


## Co warto nauczyć się dalej?

- [Jak utworzyć i wyeksportować Excel do HTML przy użyciu Aspose.Cells Java | Przewodnik po operacjach na skoroszycie](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Utwórz i zapisz skoroszyt Excel jako PDF w ASP.NET przy użyciu Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Eksportuj skoroszyt Excel jako obraz przy użyciu Aspose.Cells for Java: przewodnik krok po kroku](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}