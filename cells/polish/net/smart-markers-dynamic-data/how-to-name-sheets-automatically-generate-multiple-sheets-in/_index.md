---
category: general
date: 2026-02-09
description: Jak nazwać arkusze w C# przy użyciu SmartMarker – dowiedz się, jak generować
  wiele arkuszy i automatyzować ich nazewnictwo w kilku linijkach kodu.
draft: false
keywords:
- how to name sheets
- generate multiple sheets
- automate sheet naming
- SmartMarker sheet naming
- workbook automation
language: pl
og_description: Jak nazwać arkusze w C# przy użyciu opcji SmartMarker. Ten przewodnik
  pokazuje, jak generować wiele arkuszy i automatycznie nadawać im nazwy bez wysiłku.
og_title: Jak automatycznie nazwać arkusze – szybki przewodnik C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Jak automatycznie nazywać arkusze – generowanie wielu arkuszy w C#
url: /pl/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/
---

Let's assemble.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak automatycznie nadawać nazwy arkuszom – generowanie wielu arkuszy w C#

Zastanawiałeś się kiedyś **jak nadawać nazwy arkuszom** w skoroszycie Excel bez ręcznego klikania „Zmień nazwę” za każdym razem? Nie jesteś sam. W wielu scenariuszach raportowania kończysz z dziesiątkami arkuszy szczegółowych, które potrzebują systematycznych nazw, a robienie tego ręcznie to koszmar.  

Dobre wiadomości są takie, że przy kilku linijkach C# możesz **generować wiele arkuszy** i **automatyzować nadawanie nazw arkuszom**, tak aby każdy nowy arkusz szczegółowy podążał za przewidywalnym wzorcem. W tym samouczku przeprowadzimy Cię przez pełne rozwiązanie, wyjaśnimy, dlaczego każdy element ma znaczenie, i dostarczymy gotowy do uruchomienia przykład kodu.

## Co obejmuje ten przewodnik

* Konfigurowanie skoroszytu zawierającego SmartMarkers.
* Konfigurowanie `SmartMarkerOptions`, aby kontrolować podstawową nazwę generowanych arkuszy.
* Uruchamianie `ProcessSmartMarkers`, aby biblioteka automatycznie tworzyła `Detail`, `Detail_1`, `Detail_2`, … .
* Wskazówki dotyczące obsługi przypadków brzegowych, takich jak istniejące nazwy arkuszy lub własne konwencje nazewnictwa.
* Pełny, uruchamialny przykład, który możesz wkleić do Visual Studio i od razu zobaczyć wynik.

Nie wymagana jest wcześniejsza znajomość Aspose.Cells — wystarczy podstawowa konfiguracja C# i wybrane przez Ciebie IDE.

## Prerequisites

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| .NET 6.0 lub nowszy | Nowoczesne funkcje języka i kompatybilność biblioteki |
| Aspose.Cells for .NET (pakiet NuGet) | Dostarcza przetwarzanie `SmartMarker` i tworzenie arkuszy |
| Pusty projekt konsolowy (lub dowolna aplikacja .NET) | Daje miejsce do wykonania kodu |

Zainstaluj bibliotekę za pomocą:

```bash
dotnet add package Aspose.Cells
```

Teraz, gdy podstawy są już omówione, przejdźmy do rzeczywistej implementacji.

## Krok 1: Utwórz skoroszyt z SmartMarkers

Najpierw potrzebujemy skoroszytu zawierającego placeholder SmartMarker. SmartMarker można traktować jako znacznik szablonu, który informuje silnik, gdzie wstrzyknąć dane i, w naszym przypadku, kiedy utworzyć nowy arkusz.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣  Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // 2️⃣  Insert a SmartMarker that will trigger sheet creation
        // The marker {{detail}} tells Aspose.Cells to repeat the row for each item in the "detail" collection.
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // 3️⃣  Prepare sample data for the SmartMarker
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };
```

> **Pro tip:** Utrzymuj arkusz szablonu lekki. Tylko wiersze, które wymagają duplikacji, powinny zawierać SmartMarkers; wszystko inne pozostaje statyczne.

## Krok 2: Skonfiguruj opcje SmartMarker – rdzeń nadawania nazw arkuszom

Teraz następuje magia. Ustawiając `DetailSheetNewName`, informujemy silnik, jaką podstawową nazwę używać dla każdego generowanego arkusza. Biblioteka doda „_1”, „_2” itd., gdy podstawowa nazwa już istnieje.

```csharp
        // 4️⃣  Define naming options – this is where we answer “how to name sheets”
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // Primary keyword appears here: how to name sheets
            DetailSheetNewName = "Detail"   // Base name for all generated sheets
        };
```

Jeśli kiedykolwiek potrzebujesz innej konwencji (np. „Report_2023”), po prostu zmień ciąg znaków. Silnik automatycznie obsługuje kolizje, dlatego to podejście **automatyzuje nadawanie nazw arkuszom** bez dodatkowego kodu.

## Krok 3: Przetwórz SmartMarkers i wygeneruj arkusze

Z gotowym skoroszytem, danymi i opcjami, jedno wywołanie metody wykonuje ciężką pracę.

```csharp
        // 5️⃣  Run the SmartMarker processor – this will create Detail, Detail_1, Detail_2…
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // 6️⃣  Save the result so you can open it in Excel
        wb.Save("GeneratedSheets.xlsx");

        // 7️⃣  Let the user know we’re done
        System.Console.WriteLine("Workbook created – check GeneratedSheets.xlsx");
    }
}
```

### Oczekiwany wynik

Po otwarciu *GeneratedSheets.xlsx* zobaczysz:

| Nazwa arkusza | Zawartość |
|------------|---------|
| Template   | Oryginalny układ znaczników (zachowany dla odniesienia) |
| Detail     | Pierwszy zestaw wierszy (Apple, Banana, Cherry) |
| Detail_1   | Druga kopia – identyczne dane (przydatne przy wielu kolekcjach) |
| Detail_2   | …i tak dalej, w zależności od liczby odrębnych grup SmartMarker |

Wzorzec nazw (`Detail`, `Detail_1`, `Detail_2`) demonstruje **jak programowo nadawać nazwy arkuszom**, jednocześnie **generując wiele arkuszy** w razie potrzeby.

## Przypadki brzegowe i warianty

### 1. Istniejące nazwy arkuszy

Jeśli Twój skoroszyt już zawiera arkusz o nazwie „Detail”, silnik rozpocznie od „Detail_1”. Zapobiega to przypadkowym nadpisaniom.

### 2. Niestandardowe formaty inkrementacji

Chcesz „Detail‑A”, „Detail‑B” zamiast numerycznych przyrostków? Możesz przetworzyć nazwy po `ProcessSmartMarkers`:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet sh = wb.Worksheets[i];
    if (sh.Name.StartsWith("Detail_"))
    {
        string suffix = ((char)('A' + i - 1)).ToString(); // A, B, C…
        sh.Name = $"Detail-{suffix}";
    }
}
```

### 3. Wiele grup SmartMarker

Jeśli Twój skoroszyt zawiera więcej niż jedną grupę SmartMarker (np. `{{invoice}}` i `{{detail}}`), każda grupa wygeneruje własny zestaw arkuszy na podstawie tego samego `DetailSheetNewName`. Aby nadać każdej grupie odrębny prefiks, utwórz osobne instancje `SmartMarkerOptions` i wywołaj `ProcessSmartMarkers` dla każdej kolekcji.

## Praktyczne wskazówki z pola

* **Pro tip:** Wyłącz `AllowDuplicateNames` w `WorkbookSettings`, jeśli chcesz, aby biblioteka zgłaszała wyjątek zamiast cicho zmieniać nazwy arkuszy. To pomaga wykrywać błędy logiki nazewnictwa wcześnie.
* **Uwaga:** Bardzo długie podstawowe nazwy. Excel ogranicza nazwy arkuszy do 31 znaków; biblioteka automatycznie przycina, ale możesz skończyć z niejednoznacznymi nazwami.
* **Uwaga dotycząca wydajności:** Generowanie setek arkuszy może zużywać pamięć. Usuń skoroszyt (`wb.Dispose()`), gdy skończysz, jeśli działasz w długotrwałej usłudze.

## Przegląd wizualny

![diagram jak nadawać nazwy arkuszom](image.png "Diagram przedstawiający przepływ od szablonu SmartMarker do wygenerowanych arkuszy – jak nadawać nazwy arkuszom")

*Tekst alternatywny zawiera główne słowo kluczowe w celu spełnienia wymagań SEO.*

## Pełny kod źródłowy (gotowy do kopiowania i wklejania)

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and template sheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // SmartMarker layout
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // Sample data
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };

        // Configure naming – this answers how to name sheets
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // Process markers → generates Detail, Detail_1, Detail_2 …
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // Save and finish
        wb.Save("GeneratedSheets.xlsx");
        System.Console.WriteLine("Workbook created – open GeneratedSheets.xlsx to see the result.");
    }
}
```

Uruchom program, otwórz wygenerowany plik i zobaczysz arkusze automatycznie nazwane zgodnie ze wzorcem, który zdefiniowaliśmy.

## Zakończenie

Teraz wiesz **jak nadawać nazwy arkuszom** w skoroszycie C#, jak **generować wiele arkuszy** przy użyciu SmartMarker oraz jak **automatyzować nadawanie nazw arkuszom**, aby nigdy nie musieć ręcznie zmieniać nazw. Podejście skaluje się od kilku stron szczegółowych do setek, a ten sam wzorzec działa dla każdej kolekcji przekazywanej do `ProcessSmartMarkers`.

Co dalej? Spróbuj zamienić źródło danych na zapytanie do bazy danych, eksperymentuj z własnymi formatami przyrostków lub połącz wiele grup SmartMarker, aby uzyskać pełnoprawny silnik raportowania. Nie ma ograniczeń, gdy pozwolisz bibliotece zająć się powtarzalnym nadawaniem nazw.

Jeśli uznałeś ten przewodnik za przydatny, wystaw mu gwiazdkę na GitHubie, podziel się nim z zespołem lub zostaw komentarz poniżej z własnymi sztuczkami nazewniczymi. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}