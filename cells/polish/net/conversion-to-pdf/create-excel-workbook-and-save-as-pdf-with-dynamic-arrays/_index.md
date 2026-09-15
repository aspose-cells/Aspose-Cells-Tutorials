---
category: general
date: 2026-09-15
description: Utwórz skoroszyt Excel w C# i dowiedz się, jak zapisać go jako PDF, jednocześnie
  rozlewając dynamiczne tablice przy użyciu funkcji EXPAND.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: pl
lastmod: 2026-09-15
og_description: Utwórz skoroszyt Excel w C# i szybko zapisz go jako PDF, używając
  funkcji EXPAND do rozlewania dynamicznej tablicy.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: Utwórz skoroszyt Excel i zapisz jako PDF z dynamicznymi tablicami
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Utwórz skoroszyt Excela i zapisz jako PDF z dynamicznymi tablicami
url: /pl/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt Excel i zapisz jako PDF z dynamicznymi tablicami

Jeśli potrzebujesz **utworzyć skoroszyt Excel** programowo, a następnie **zapisać skoroszyt jako PDF**, ten przewodnik pokaże Ci kompletną, kompleksową metodę w C#. Zobaczysz także, jak **rozlać wyniki dynamicznej tablicy** przy użyciu **funkcji EXPAND**, czyli nowoczesnego sposobu generowania tablic bez VBA.  

Niezależnie od tego, czy tworzysz usługę raportowania, funkcję eksportu dla systemu ERP, czy pulpit nawigacyjny oparty na danych, poniższe kroki pozwolą Ci wygenerować skoroszyt, wypełnić go danymi Smart‑Marker i wyprodukować PDF zachowujący zaawansowane cechy czcionek.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.8)
* Aktualną wersję **Aspose.Cells for .NET** (v25.8 lub nowszą) – udostępnia `Workbook`, `PdfSaveOptions` i `SmartMarkerProcessor`.
* IDE, np. Visual Studio 2022 (dowolny edytor zdolny kompilować C#).

Dodaj pakiet NuGet do swojego projektu:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Krok 1: Utwórz skoroszyt Excel i skonfiguruj pierwszy arkusz

Pierwszym zadaniem jest **utworzyć skoroszyt Excel** i uzyskać odwołanie do domyślnego arkusza. Ten arkusz będzie hostował dynamiczną tablicę oraz szablon Smart Marker.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Dlaczego to ważne*: Inicjalizacja `Workbook` alokuje wewnętrzną strukturę skoroszytu, a dostęp do `Worksheets[0]` daje gotowy arkusz bez konieczności ręcznego dodawania.

## Krok 2: Rozlać dynamiczną tablicę przy użyciu funkcji EXPAND

**Funkcja EXPAND** w Excelu może zamienić statyczny literał tablicowy w zakres rozlewający się o dowolnym rozmiarze. Tutaj prosimy Excel, aby rozlał `{1,2,3}` na zakres 5‑wierszy × 1‑kolumny zaczynający się od `A1`.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Dlaczego to ważne*: Użycie `EXPAND` eliminuje ręczne pętle w C#. Silnik oblicza zakres rozlewu i zapisuje wartości bezpośrednio w arkuszu, które później pojawią się w PDF.

## Krok 3: Zapisz skoroszyt jako PDF zachowując selektory wariantów czcionek

Gdy potrzebujesz **zapisać skoroszyt jako PDF**, możesz także włączyć zaawansowane funkcje typograficzne, takie jak selektory wariantów czcionek (dostępne od Aspose.Cells v25.8). Zapewnia to prawidłowe renderowanie skomplikowanych skryptów w PDF.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Dlaczego to ważne*: Ustawienie `FontVariationSelectors` na `true` jest niezbędne dla języków korzystających z wariacji glifów (np. chiński, japoński, emoji). Utworzony PDF odzwierciedla widok Excela na ekranie.

## Krok 4: Wstaw szablon Smart Marker odwołujący się do zagnieżdżonego źródła danych

Smart Markery pozwalają osadzać znaczniki bezpośrednio w arkuszu. Poniższy szablon wygeneruje listę zamówień i ich pozycje.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Dlaczego to ważne*: Umieszczając szablon w `A1`, informujesz Aspose.Cells, gdzie rozpocząć rozwijanie danych. Składnia `:` (`Items:ItemName`) mówi procesorowi, aby iterował po zagnieżdżonej kolekcji.

## Krok 5: Zdefiniuj zagnieżdżone źródło danych (zamówienia zawierające pozycje)

Tworzymy anonimową tablicę zamówień, z których każde zawiera własną kolekcję obiektów pozycji. To odzwierciedla typowy scenariusz master‑detail.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Dlaczego to ważne*: Struktura zagnieżdżona demonstruje **jak stworzyć dynamiczną tablicę w Excelu** przy użyciu Smart Markerów, bez pisania VBA ani ręcznych pętli komórek.

## Krok 6: Przetwórz Smart Markery i zapisz ostateczny plik Excel

Teraz przekazujemy skoroszyt i źródło danych do `SmartMarkerProcessor`. Po przetworzeniu znaczniki zostają zastąpione rzeczywistymi wierszami, a wynik zapisujemy jako zwykły plik `.xlsx`.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Dlaczego to ważne*: `SmartMarkerProcessor` automatycznie rozwija szablon, tworzy potrzebne wiersze i wypełnia je danymi. Gotowy skoroszyt można otworzyć w Excelu, aby zweryfikować poprawność wyświetlania każdego zamówienia i jego pozycji.

## Oczekiwany wynik

* **VarSelector.pdf** – plik PDF pokazujący liczby 1‑3 rozlewające się na pięć wierszy, renderowane z dowolnymi wariacjami OpenType, które włączyłeś.
* **NestedSmartMarker.xlsx** – plik Excel z następującymi wierszami (zaczynając od `A1`):

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

Wersja PDF zachowuje ten sam rozlew liczbowy, ponieważ stan arkusza został zapisany przed przetworzeniem Smart Marker; możesz powtórzyć zapis PDF po przetworzeniu, jeśli potrzebujesz finalnych danych w PDF.

## Porady i typowe pułapki

| Porada | Wyjaśnienie |
|-----|-------------|
| **Używaj tego samego obiektu `PdfSaveOptions`** | Utworzenie obiektu opcji raz i ponowne jego użycie eliminuje subtelne różnice w renderowaniu (np. brakujące selektory wariantów). |
| **Wywołaj `ws.Calculate()` po ustawieniu formuł** | Bez jawnego przeliczenia zakres rozlewu może pozostać pusty przy programowym przeglądaniu skoroszytu. |
| **Umieszczaj szablony Smart Marker na czystym arkuszu** | Mieszanie szablonów z istniejącymi danymi może powodować nieoczekiwane wstawianie wierszy. Jeśli to możliwe, użyj dedykowanego arkusza. |
| **Zwróć uwagę na ścieżki plików** | Używaj `Path.Combine(Environment.CurrentDirectory, "output.pdf")`, aby uniknąć twardo zakodowanych katalogów na różnych maszynach. |
| **Sprawdź wersję** | `FontVariationSelectors` jest dostępny dopiero od wersji 25.8; starsze wersje zignorują tę właściwość bez wyrzucania błędu. |

## Kolejne kroki

Teraz, gdy wiesz, jak **utworzyć skoroszyt Excel**, **rozlać dynamiczną tablicę** i **zapisać skoroszyt jako PDF**, możesz rozważyć:

* Dodanie wykresów lub obrazów przed konwersją do PDF.
* Eksport tego samego skoroszytu do innych formatów (np. HTML, CSV) przy użyciu przeciążeń `Save`.
* Korzystanie z **wyrażeń Smart Marker** (`${Orders.Total:SUM(Items.Price)}`) w celu obliczania agregatów w locie.
* Integrację tego kodu w API ASP.NET Core, aby użytkownicy mogli pobierać wygenerowany PDF bezpośrednio z endpointu webowego.

---

**Podsumowanie** – Ten tutorial pokazał, jak **utworzyć skoroszyt Excel**, użyć **funkcji EXPAND** do **rozlania dynamicznej tablicy**, osadzić **Smart Marker** współpracujący ze zagnieżdżonym źródłem danych oraz w końcu **zapisać skoroszyt jako PDF** zachowując zaawansowane cechy czcionek. Pełny, gotowy do uruchomienia przykład możesz skopiować do dowolnego projektu C# i dostosować do własnych struktur danych. Powodzenia w kodowaniu!


## Co powinieneś nauczyć się dalej?


Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu wraz z krok‑po‑kroku wyjaśnieniami, pomagając Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Utwórz i zapisz skoroszyt Excel jako PDF w ASP.NET przy użyciu Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Jak utworzyć i zapisać skoroszyt Excel jako ODS przy użyciu Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Jak utworzyć i zapisać skoroszyt Excel jako SVG przy użyciu Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}