---
category: general
date: 2026-11-22
description: Naucz się tworzyć pliki Excel z danych JSON w języku C# przy użyciu Aspose.Cells
  Smart Marker. Przewodnik krok po kroku obejmuje projektowanie szablonu, obsługę
  JSON oraz eksport pliku.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json data
- Aspose.Cells
- Smart Marker
- C# Excel generation
- JSON to Excel
- Excel template
language: pl
lastmod: 2026-11-22
og_description: Utwórz plik Excel z danych JSON przy użyciu Aspose.Cells Smart Marker.
  Skorzystaj z tego zwięzłego poradnika, aby wygenerować w pełni sformatowany skoroszyt
  z tablicy JSON.
og_image_alt: Screenshot showing Excel workbook created from JSON data using Aspose.Cells
og_title: Utwórz Excel z danych JSON w C# – kompletny przewodnik Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn to create Excel from JSON data in C# using Aspose.Cells Smart
    Marker. Step‑by‑step guide covers template design, JSON handling, and file export.
  headline: How to create Excel from JSON data with Aspose.Cells and Smart Marker
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak utworzyć plik Excel z danych JSON przy użyciu Aspose.Cells i Smart Marker
url: /pl/net/smart-markers-dynamic-data/how-to-create-excel-from-json-data-with-aspose-cells-and-sma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć Excel z danych JSON przy użyciu Aspose.Cells i Smart Marker

Jeśli potrzebujesz **utworzyć Excel z danych JSON** w aplikacji .NET, ten samouczek pokaże Ci kompletną, gotową do produkcji rozwiązanie. Zobaczysz, jak osadzić tablicę JSON w pojedynczej komórce, użyć funkcji **Smart Marker** w **Aspose.Cells** oraz wygenerować finalny skoroszyt bez ręcznego kodowania komórka po komórce.

Podejście działa dla dowolnego ładunku JSON — niezależnie od tego, czy eksportujesz wyniki API, serializujesz obiekty, czy tworzysz raporty. Po zakończeniu przewodnika będziesz mieć gotowy do uruchomienia projekt C#, który odczytuje ciąg JSON, stosuje go do **szablonu Excel**, i zapisuje wynik jako nowy plik.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.6+)
- Visual Studio 2022 (lub dowolne IDE obsługujące C#)
- **Aspose.Cells for .NET** pakiet NuGet (wersja 23.10 lub nowsza)
- Prosty plik szablonu Excel zawierający znacznik Smart Marker `<%=Fruits:ArrayAsSingle%>` w docelowej komórce

> **Wskazówka:** Przechowuj szablon w folderze, do którego Twoja aplikacja ma dostęp w czasie wykonywania (np. `Resources` lub konfigurowalna ścieżka).  

## Krok 1: Przygotuj ładunek JSON

Najpierw zdefiniuj tablicę JSON, którą chcesz wstawić do arkusza. W tym przykładzie używamy listy nazw owoców.

```csharp
// Step 1 – JSON array that will be placed in a single cell
string fruitsJson = "[\"Apple\",\"Banana\",\"Cherry\"]";
```

Ciąg JSON może być generowany dynamicznie (np. `JsonSerializer.Serialize(myList)`) lub odczytany z zewnętrznego źródła, takiego jak REST API. Kluczowe jest, aby ciąg był prawidłową tablicą JSON, ponieważ **Smart Marker** oczekuje reprezentacji JSON przy użyciu opcji `ArrayAsSingle`.

## Krok 2: Zbuduj źródło danych Smart Marker

Silnik Smart Marker w Aspose.Cells działa z dowolnym obiektem .NET. Tworzymy anonimowy obiekt, który zawiera ciąg JSON pod właściwością o nazwie `Fruits`. Nazwa właściwości musi odpowiadać nazwie znacznika użytej w szablonie.

```csharp
// Step 2 – Anonymous object serving as the Smart Marker data source
var dataSource = new
{
    Fruits = fruitsJson   // Property name "Fruits" matches the marker <%=Fruits...%>
};
```

> **Dlaczego anonimowy obiekt?** Pozwala on przekazać lekki kontener danych bez definiowania dedykowanej klasy, co przyspiesza prototypowanie. W większych projektach możesz zastąpić go silnie typowanym DTO.

## Krok 3: Zaprojektuj szablon Excel z miejscem na Smart Marker

Utwórz plik Excel (`SmartMarkerTemplate.xlsx`), który zawiera miejsce, w którym pojawi się JSON. Umieść następujący znacznik w wybranej komórce (np. **A1**):

```
<%=Fruits:ArrayAsSingle%>
```

- `Fruits` – odpowiada nazwie właściwości w źródle danych.
- `ArrayAsSingle` – instruuje Smart Marker, aby zapisał całą tablicę JSON jako pojedynczy ciąg, zachowując nawiasy i cudzysłowy.

![Excel template with Smart Marker placeholder](excel-template.png){alt="Szablon Excel zawierający <%=Fruits:ArrayAsSingle%> do tworzenia Excela z danych JSON"}

## Krok 4: Załaduj skoroszyt i zainicjuj procesor Smart Marker

Teraz załaduj plik szablonu do instancji `Aspose.Cells.Workbook` i utwórz `SmartMarkerProcessor`, który będzie obsługiwał zamianę.

```csharp
// Step 4 – Load the template workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

// Initialise the Smart Marker processor with the loaded workbook
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor(workbook);
```

Załadowanie skoroszytu raz i ponowne użycie tej samej instancji `SmartMarkerProcessor` jest bardziej wydajne niż tworzenie nowego procesora dla każdej komórki.

## Krok 5: Zastosuj źródło danych, aby zastąpić znacznik

Metoda `ApplyTemplate` przeszukuje skoroszyt w poszukiwaniu wszystkich znaczników i zastępuje je wartościami z dostarczonego obiektu.

```csharp
// Step 5 – Replace the Smart Marker with the JSON content
smartMarkerProcessor.ApplyTemplate(dataSource);
```

Ponieważ użyliśmy `ArrayAsSingle`, komórka teraz zawiera surowy ciąg JSON:

```
["Apple","Banana","Cherry"]
```

Jeśli potrzebujesz innego formatu (np. listy oddzielonej przecinkami), możesz użyć `ArrayAsCommaSeparated` zamiast `ArrayAsSingle`.

## Krok 6: Zapisz przetworzony skoroszyt

Na koniec zapisz zmodyfikowany skoroszyt do nowego pliku. Możesz wybrać dowolny obsługiwany format (`.xlsx`, `.xls`, `.csv` itp.).

```csharp
// Step 6 – Save the workbook with the JSON inserted
workbook.Save("YOUR_DIRECTORY/JsonExported.xlsx");
```

Powstały plik `JsonExported.xlsx` może być otwarty w Excelu, Google Sheets lub dowolnym kompatybilnym przeglądarce i wyświetli tablicę JSON dokładnie tak, jak została wstawiona.

## Pełny działający przykład

Połączenie wszystkich elementów daje Ci samodzielny program konsolowy:

```csharp
using Aspose.Cells;

class SmartMarkerJsonDemo
{
    static void Main()
    {
        // 1️⃣ Define the JSON array
        string fruitsJson = "[\"Apple\",\"Banana\",\"Cherry\"]";

        // 2️⃣ Create the data source object
        var dataSource = new
        {
            Fruits = fruitsJson
        };

        // 3️⃣ Load the Excel template that contains <%=Fruits:ArrayAsSingle%>
        Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

        // 4️⃣ Initialise the Smart Marker processor
        SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor(workbook);

        // 5️⃣ Apply the data source – the marker is replaced with the JSON string
        smartMarkerProcessor.ApplyTemplate(dataSource);

        // 6️⃣ Save the result
        workbook.Save("YOUR_DIRECTORY/JsonExported.xlsx");
    }
}
```

### Oczekiwany wynik

| A                                   |
|-------------------------------------|
| `["Apple","Banana","Cherry"]`       |

JSON pojawia się dokładnie jako ciąg znaków w komórce **A1** pliku `JsonExported.xlsx`.

## Obsługa typowych wariacji i przypadków brzegowych

| Sytuacja                                 | Zalecana modyfikacja |
|------------------------------------------|----------------------|
| **Duże obiekty JSON** (zagnieżdżone słowniki) | Użyj `ArrayAsJson`, aby osadzić całą hierarchię obiektów, lub zamapuj JSON na silnie typowany model i użyj zagnieżdżonych znaczników (`<%=Parent.Child%>`). |
| **Wiele tablic JSON** w różnych komórkach | Dodaj dodatkowe właściwości do anonimowego obiektu (np. `Vegetables = vegJson`) oraz odpowiadające znaczniki (`<%=Vegetables:ArrayAsSingle%>`). |
| **Potrzeba podzielenia tablicy na wiersze** | Zastąp `ArrayAsSingle` przez `Array` – Smart Marker utworzy nowy wiersz dla każdego elementu. |
| **Szablon przechowywany jako zasób osadzony** | Załaduj skoroszyt ze strumienia: `Assembly.GetExecutingAssembly().GetManifestResourceStream("Namespace.Template.xlsx")`. |
| **Uruchamianie w ASP.NET Core** | Użyj `IWebHostEnvironment.ContentRootPath`, aby zbudować pełną ścieżkę do szablonu i plików wyjściowych. |

## Rozważania dotyczące wydajności

- **Ponowne użycie obiektu `Workbook`** przy przetwarzaniu wielu rekordów w partii; utwórz procesor raz na skoroszyt.
- **Wyłącz obliczenia** (`workbook.CalculateFormula = false`), jeśli szablon zawiera ciężkie formuły, które nie są potrzebne w kroku wstawiania JSON.
- **Zapisywanie strumieniowe** (`workbook.Save(stream, SaveFormat.Xlsx)`) zmniejsza obciążenie I/O przy bezpośrednim wysyłaniu pliku w odpowiedzi do klienta.

## Podsumowanie

Teraz wiesz, jak **utworzyć Excel z danych JSON** w C# przy użyciu **Aspose.Cells** i funkcji **Smart Marker**. Samouczek obejmował przygotowanie JSON, tworzenie źródła danych, projektowanie szablonu, przetwarzanie znaczników oraz zapisywanie pliku — wszystko w jednym, uruchamialnym programie.

Z tego miejsca możesz:

- Rozszerzyć szablon o dodatkowe znaczniki **Smart Marker**, aby uzyskać bardziej rozbudowane raporty.
- Przejść na `Array` lub `ArrayAsJson`, aby wyświetlać JSON jako wiersze lub struktury zagnieżdżone.
- Połączyć tę technikę z bibliotekami **C# Excel generation** takimi jak EPPlus lub ClosedXML, jeśli potrzebujesz darmowej alternatywy.

Miłego kodowania i ciesz się przekształcaniem JSON w dopracowane skoroszyty Excel!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Importowanie danych JSON do Excela przy użyciu Aspose.Cells Java: Kompletny przewodnik](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Samouczek Aspose Cells GridJs – Eksport danych Excel do JSON z leniwym ładowaniem](/cells/english/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/)
- [Tworzenie Excela z JSON przy użyciu Smart Marker w Aspose.Cells](/cells/spanish/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}