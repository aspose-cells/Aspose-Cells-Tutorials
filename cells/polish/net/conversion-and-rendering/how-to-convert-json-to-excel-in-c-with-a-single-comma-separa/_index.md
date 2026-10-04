---
category: general
date: 2026-10-04
description: Konwertuj JSON na Excel w C#, ładując plik JSON, deserializując tablicę
  ciągów znaków i zapisując ją jako pojedynczą komórkę Excela z wartościami oddzielonymi
  przecinkami.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert json to excel
- load json file c#
- deserialize json string array
- save json as excel
- comma separated excel cell
language: pl
lastmod: 2026-10-04
og_description: Szybko konwertuj JSON na Excel w C#. Wczytaj plik JSON, zdeserializuj
  tablicę stringów i zapisz ją jako jedną komórkę Excel z wartościami oddzielonymi
  przecinkami.
og_image_alt: Result of convert JSON to Excel showing a single comma‑separated Excel
  cell
og_title: Konwertuj JSON do Excela w C# – przewodnik po jednej komórce z wartościami
  oddzielonymi przecinkami
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Convert JSON to Excel in C# by loading a JSON file, deserializing a
    string array, and saving it as a single comma‑separated Excel cell.
  headline: How to convert JSON to Excel in C# with a single comma‑separated cell
  type: TechArticle
- questions:
  - answer: Yes. Aspose.Cells and Newtonsoft.Json are both .NET Standard libraries,
      so the same code runs on .NET Core, .NET 5/6, and .NET Framework.
    question: Does this work with .NET Core?
  - answer: A trial license works for development and testing. For production you’ll
      need a valid license to remove evaluation watermarks.
    question: Do I need a license for Aspose.Cells?
  - answer: 'Absolutely. Replace `workbook.Save(outPath);` with `using var ms = new
      MemoryStream(); workbook.Save(ms, SaveFormat.Xlsx);` and then return the byte
      array from a web API. ## Conclusion You now know how to **convert JSON to Excel**
      in C# by loading a JSON file, **deserializing a JSON string array**, '
    question: Can I write directly to a `MemoryStream` instead of a file?
  type: FAQPage
tags:
- JSON
- Excel
- C#
- Aspose.Cells
title: Jak przekonwertować JSON na Excel w C# z jedną komórką zawierającą wartości
  oddzielone przecinkami
url: /pl/net/conversion-and-rendering/how-to-convert-json-to-excel-in-c-with-a-single-comma-separa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przekonwertować JSON do Excela w C# przy użyciu jednej komórki z wartościami oddzielonymi przecinkami

Jeśli potrzebujesz **konwertować JSON do Excela** w projekcie C#, ten przewodnik pokaże Ci kompletne, gotowe‑do‑uruchomienia rozwiązanie. Nauczysz się, jak **wczytać plik JSON w C#**, **zdeserializować tablicę łańcuchów JSON**, oraz **zapisać JSON jako Excel**, gdzie cała tablica pojawia się jako **komórka Excela z wartościami oddzielonymi przecinkami**. Podejście wykorzystuje funkcję Smart Marker w Aspose.Cells, która eliminuje ręczne pętle i utrzymuje kod zwięzły.

Po zakończeniu tego samouczka będziesz mieć działający plik `.xlsx`, który zawiera całą tablicę JSON w komórce `A1` jako pojedynczą, przecinkowo‑oddzieloną wartość. Bez zewnętrznych skryptów, bez tymczasowych plików CSV — tylko czysty C#.

## Czego będziesz potrzebować

- .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7+)
- **Aspose.Cells for .NET** (wersja 23.10 lub nowsza) – biblioteka obsługująca Smart Markery
- **Newtonsoft.Json** (Json.NET) do deserializacji JSON
- Plik JSON zawierający prostą tablicę łańcuchów, np.:

```json
["Apple","Banana","Cherry","Date"]
```

> **Pro tip:** Jeśli wolisz rozwiązanie wyłącznie z NuGet, możesz zastąpić Aspose.Cells biblioteką ClosedXML i ręcznie zapisać ciąg znaków oddzielony przecinkami. Podejście Smart Marker jednak dobrze skalowalne jest przy dodawaniu bardziej złożonych struktur danych.

## Konwersja JSON do Excela – przygotowanie skoroszytu i smart markera

Pierwszym krokiem jest utworzenie pustego skoroszytu i umieszczenie Smart Markera w komórce, która ma otrzymać tablicę. Smart Markery działają jak znaczniki zastępcze, które Aspose.Cells wypełnia automatycznie podczas przetwarzania.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Create a new workbook with a single worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];

// Put a Smart Marker in A1 that tells the processor to write the whole array
sheet.Cells["A1"].PutValue("&=fruitsArray, ArrayAsSingle");
```

**Dlaczego to ważne:**  
`ArrayAsSingle` informuje procesor, aby traktował całą kolekcję jako jedną wartość zamiast rozwijać ją na wiele wierszy. To klucz do uzyskania **komórki Excela z wartościami oddzielonymi przecinkami**.

## Wczytaj plik JSON w C# i zdeserializuj tablicę łańcuchów JSON

Następnie odczytaj plik JSON z dysku i przekształć go w tablicę łańcuchów C#. Newtonsoft.Json upraszcza to zadanie.

```csharp
using System.IO;
using Newtonsoft.Json;

// Step 1: Load the JSON array from a file
string json = File.ReadAllText(@"C:\Data\fruits.json");

// Step 2: Deserialize the JSON into a string array
string[] fruitsArray = JsonConvert.DeserializeObject<string[]>(json);
```

**Dlaczego to ważne:**  
Deserializacja przekształca surowy tekst JSON w silnie typowaną `string[]`. Powstała zmienna (`fruitsArray`) odpowiada nazwie użytej w Smart Markerze (`fruitsArray`), co pozwala procesorowi automatycznie powiązać dane.

## Włącz ArrayAsSingle i przetwórz dane

Teraz skonfiguruj `SmartMarkerProcessor`, aby globalnie używał opcji `ArrayAsSingle` i przekaż obiekt danych do procesora.

```csharp
using Aspose.Cells.SmartMarkers;

// Create the processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();

// Enable the ArrayAsSingle option (applies to all markers)
processor.Options.ArrayAsSingle = true;

// Wrap the array in an anonymous object whose property name matches the marker
var data = new { fruitsArray };

// Process the workbook – the Smart Marker in A1 is replaced with the comma‑separated list
processor.Process(workbook, data);
```

**Dlaczego to ważne:**  
Ustawienie `processor.Options.ArrayAsSingle = true` zapewnia, że *dowolny* znacznik używający flagi `ArrayAsSingle` zachowuje się spójnie. Obiekt anonimowy (`data`) umożliwia wygodne przekazywanie wielu źródeł danych później, bez konieczności tworzenia dedykowanej klasy DTO.

## Zapisz JSON jako Excel z komórką Excela zawierającą wartości oddzielone przecinkami

Na koniec zapisz skoroszyt na dysku. Powstały plik zawiera całą tablicę JSON w jednej komórce.

```csharp
// Step 5: Save the workbook – the array appears as a single, comma‑separated value in A1
workbook.Save(@"C:\Output\JsonSingleCell.xlsx");
```

Otwórz plik w Excelu i zobaczysz coś podobnego do:

```
Apple, Banana, Cherry, Date
```

Wszystkie wartości są zapisane w **komórce A1**, dokładnie tak jak wymagane.

## Pełny działający przykład

Połączenie wszystkich elementów daje kompaktowy program, który możesz wkleić do dowolnego projektu konsolowego lub serwisowego.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using Newtonsoft.Json;

class Program
{
    static void Main()
    {
        // 1️⃣ Load JSON from file
        string jsonPath = @"C:\Data\fruits.json";
        if (!File.Exists(jsonPath))
        {
            Console.WriteLine($"File not found: {jsonPath}");
            return;
        }
        string json = File.ReadAllText(jsonPath);

        // 2️⃣ Deserialize to string[]
        string[] fruitsArray = JsonConvert.DeserializeObject<string[]>(json);
        if (fruitsArray == null || fruitsArray.Length == 0)
        {
            Console.WriteLine("JSON array is empty or malformed.");
            return;
        }

        // 3️⃣ Create workbook & place Smart Marker
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("&=fruitsArray, ArrayAsSingle");

        // 4️⃣ Configure processor and process data
        SmartMarkerProcessor processor = new SmartMarkerProcessor
        {
            Options = { ArrayAsSingle = true }
        };
        var data = new { fruitsArray };
        processor.Process(workbook, data);

        // 5️⃣ Save the result
        string outPath = @"C:\Output\JsonSingleCell.xlsx";
        workbook.Save(outPath);
        Console.WriteLine($"Excel file created: {outPath}");
    }
}
```

### Oczekiwany wynik

Uruchomienie programu z przykładowym JSON powyżej generuje `JsonSingleCell.xlsx`. Otworzenie pliku pokazuje:

| A                               |
|---------------------------------|
| Apple, Banana, Cherry, Date     |

Nie dodano dodatkowych wierszy ani kolumn.

## Przypadki brzegowe i praktyczne wskazówki

| Sytuacja | Jak sobie radzić |
|-----------|-----------------|
| **Pusta tablica JSON** | Sprawdzenie `if (fruitsArray == null || fruitsArray.Length == 0)` zapobiega zapisywaniu pustej komórki i pozwala zalogować ostrzeżenie. |
| **Elementy nie‑łańcuchowe** | Zmień typ generyczny, aby pasował do struktury JSON, np. `DeserializeObject<int[]>` dla liczb, i odpowiednio dostosuj Smart Marker (`&=numbersArray, ArrayAsSingle`). |
| **Duże tablice (10 k+ elementów)** | Komórki Excela mają limit 32 767 znaków. Jeśli połączony ciąg przekracza ten limit, podziel dane na wiele komórek lub wierszy. |
| **Inny separator** | Zastąp domyślny przecinek przetwarzając ciąg po fakcie: `string.Join(";", fruitsArray)` i ustaw znacznik na `&=fruitsArray, ArrayAsSingle` (separator jest określany przez implementację `ToString` tablicy). |
| **Wiele tablic** | Umieść dodatkowe Smart Markery w innych komórkach (`B1`, `C1`, …) i dodaj odpowiadające właściwości do obiektu anonimowego (`var data = new { fruitsArray, colorsArray }`). |

## Najczęściej zadawane pytania

**P: Czy to działa z .NET Core?**  
O: Tak. Aspose.Cells i Newtonsoft.Json są bibliotekami .NET Standard, więc ten sam kod działa na .NET Core, .NET 5/6 oraz .NET Framework.

**P: Czy potrzebna jest licencja na Aspose.Cells?**  
O: Licencja próbna działa w fazie rozwoju i testów. W produkcji potrzebna będzie ważna licencja, aby usunąć znaki wodne oceny.

**P: Czy mogę zapisać bezpośrednio do `MemoryStream` zamiast pliku?**  
O: Oczywiście. Zamień `workbook.Save(outPath);` na `using var ms = new MemoryStream(); workbook.Save(ms, SaveFormat.Xlsx);` i zwróć tablicę bajtów z API webowego.

## Podsumowanie

Teraz wiesz, jak **konwertować JSON do Excela** w C# poprzez wczytanie pliku JSON, **zdeserializowanie tablicy łańcuchów JSON** oraz **zapisanie JSON jako Excel**, gdzie cała kolekcja pojawia się jako **komórka Excela z wartościami oddzielonymi przecinkami**. Podejście Smart Marker utrzymuje kod krótki, eliminuje ręczne pętle i skaluje się do bardziej złożonych struktur danych.

Next, explore these related topics:

- **Wczytaj plik JSON w C#** przy użyciu `System.Text.Json` dla mniejszego zestawu zależności.  
- **Zdeserializuj tablicę łańcuchów JSON** do własnych obiektów w celu eksportu do Excela w wielu kolumnach.  
- **Zapisz JSON jako Excel** używając szablonów do generowania sformatowanych raportów.  
- **Obsługa komórki Excela z wartościami oddzielonymi przecinkami** przy eksporcie kompatybilnym z CSV.

Śmiało eksperymentuj z różnymi separatorami, większymi zestawami danych lub wieloma Smart Markerami. Jeśli napotkasz jakiekolwiek problemy, przejrzyj powyższe sekcje obsługi błędów lub skonsultuj się z dokumentacją Aspose.Cells w celu poznania zaawansowanych funkcji Smart Marker.

Miłego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [dane JSON do Excela – Pełny przewodnik konwersji tablicy JSON do Excela](/cells/english/net/excel-data-import-export/json-data-to-excel-full-guide-to-convert-json-array-excel/)
- [Konwertuj JSON do Excela w C# – Przewodnik krok po kroku](/cells/english/net/smart-markers-dynamic-data/convert-json-to-excel-with-c-step-by-step-guide/)
- [Utwórz skoroszyt Excel w C# – Wstaw JSON i zapisz jako XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}