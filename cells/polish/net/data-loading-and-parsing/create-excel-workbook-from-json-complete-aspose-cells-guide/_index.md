---
category: general
date: 2026-02-14
description: Utwórz skoroszyt Excel przy użyciu Aspose.Cells i dowiedz się, jak przetwarzać
  JSON, konwertować JSON do Excela oraz ładować JSON do Excela w kilku prostych krokach.
draft: false
keywords:
- create excel workbook
- how to process json
- convert json to excel
- load json into excel
- aspose cells json
language: pl
og_description: Utwórz skoroszyt Excel przy użyciu Aspose.Cells, dowiedz się, jak
  przetwarzać JSON, konwertować JSON do Excela oraz ładować JSON do Excela szybko
  i niezawodnie.
og_title: Utwórz skoroszyt Excel z JSON – krok po kroku tutorial Aspose.Cells
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Utwórz skoroszyt Excel z JSON – Kompletny przewodnik Aspose.Cells
url: /pl/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie skoroszytu Excel z JSON – Kompletny przewodnik Aspose.Cells

Czy kiedykolwiek potrzebowałeś **utworzyć skoroszyt Excel** z fragmentu JSON, ale nie wiedziałeś od czego zacząć? Nie jesteś sam. Wielu programistów napotyka ten sam problem, gdy mają ładunek JSON i potrzebują uporządkowanego arkusza kalkulacyjnego do raportowania lub wymiany danych.  

Dobra wiadomość? Dzięki **Aspose.Cells** możesz zamienić ten JSON w w pełni funkcjonalny plik Excel w zaledwie kilku linijkach kodu. W tym tutorialu przejdziemy przez **przetwarzanie JSON**, **konwersję JSON do Excel** oraz **ładowanie JSON do Excel** przy użyciu potężnego `SmartMarkerProcessor`. Na końcu będziesz mieć gotowy do zapisania skoroszyt oraz jasny obraz dostępnych opcji konfiguracyjnych.

## Co się nauczysz

- Jak skonfigurować projekt Aspose.Cells do obsługi JSON.  
- Dokładny kod potrzebny do **utworzenia skoroszytu Excel** z tablicy JSON.  
- Dlaczego opcja `ArrayAsSingle` ma znaczenie i kiedy warto ją zmienić.  
- Wskazówki dotyczące obsługi większych struktur JSON, obsługi błędów i zapisywania pliku.  

> **Wymagania wstępne:** .NET 6+ (lub .NET Framework 4.6+), pakiet NuGet Aspose.Cells for .NET oraz podstawowa znajomość C#. Nie są potrzebne żadne inne biblioteki.

---

## Krok 1: Zainstaluj Aspose.Cells i dodaj wymaganą przestrzeń nazw

Zanim uruchomisz jakikolwiek kod, musisz mieć bibliotekę Aspose.Cells dodaną do swojego projektu.

```bash
dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;   // Core namespace for workbook manipulation
```

> **Pro tip:** Jeśli używasz Visual Studio, interfejs menedżera pakietów NuGet robi to samo – po prostu wyszukaj *Aspose.Cells* i kliknij **Install**.

---

## Krok 2: Przygotuj dane JSON, które chcesz przekonwertować

`SmartMarkerProcessor` działa z dowolnym ciągiem JSON, ale musisz określić, jak biblioteka ma interpretować tablice. W tym przykładzie potraktujemy prostą tablicę liczb jako **pojedynczy rekord**, co jest przydatne, gdy potrzebujesz płaskiej listy wartości.

```csharp
// Step 2: Define the JSON payload – an array of three numbers
string jsonData = "[1,2,3]";   // You could also load this from a file or API response
```

> **Dlaczego to ważne:** Domyślnie Aspose.Cells traktuje każdy element tablicy jako oddzielny rekord. Ustawienie `ArrayAsSingle = true` scala całą tablicę w jeden rekord, co pasuje do wielu scenariuszy raportowych.

---

## Krok 3: Utwórz nową instancję Workbook

Teraz faktycznie **tworzymy skoroszyt Excel** w pamięci. Żaden plik nie jest jeszcze zapisywany; przygotowujemy jedynie kontener.

```csharp
// Step 3: Initialise a fresh workbook – starts with a single empty worksheet
Workbook workbook = new Workbook();
```

W tym momencie `workbook.Worksheets[0]` to pusty arkusz o nazwie *Sheet1*. Możesz zmienić jego nazwę później, jeśli chcesz.

---

## Krok 4: Skonfiguruj opcje SmartMarker dla przetwarzania JSON

Klasa `SmartMarkerOptions` daje precyzyjną kontrolę nad tym, jak JSON jest interpretowany. Kluczową flagą w naszym scenariuszu jest `ArrayAsSingle`.

```csharp
// Step 4: Set SmartMarker options – treat the JSON array as a single record
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // Important when your JSON is a simple list
};
```

> **Kiedy to zmienić:** Jeśli Twój JSON reprezentuje kolekcję wierszy (np. tablicę obiektów), pozostaw `ArrayAsSingle` jako `false`. Każdy obiekt automatycznie stanie się nowym wierszem.

---

## Krok 5: Uruchom przetwarzanie Smart Marker na arkuszu

Mając gotowy skoroszyt i opcje, przekazujemy JSON do procesora. Procesor skanuje arkusz w poszukiwaniu smart markerów (znaczników) i zastępuje je danymi z JSON. Ponieważ nie mamy wyraźnych znaczników, procesor po prostu tworzy domyślny układ.

```csharp
// Step 5: Execute Smart Marker processing on the first worksheet
workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);
```

Jeśli chcesz kontrolować dokładną komórkę, od której zaczynają się dane, możesz dodać znacznik `"${Array}"` do komórki **A1** przed uruchomieniem procesora. W tym tutorialu polegamy na zachowaniu domyślnym, które zapisuje wartości tablicy w kolejnych komórkach zaczynając od **A1**.

---

## Krok 6: Zapisz skoroszyt na dysku (lub w strumieniu)

Ostatni krok to utrwalenie skoroszytu. Możesz zapisać go do pliku, strumienia pamięci lub nawet zwrócić bezpośrednio z API webowego.

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

Uruchomienie pełnego programu generuje plik Excel z liczbami **1**, **2** i **3** umieszczonymi w komórkach **A1**, **A2** i **A3** odpowiednio.

---

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do uruchomienia program konsolowy, który łączy wszystkie kroki. Skopiuj‑wklej go do nowego projektu C# typu console i naciśnij **F5**.

```csharp
// ---------------------------------------------------------------
// Complete example: Create Excel workbook from JSON using Aspose.Cells
// ---------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare JSON data
        string jsonData = "[1,2,3]";

        // 2️⃣ Create a new workbook (empty Excel file)
        Workbook workbook = new Workbook();

        // 3️⃣ Configure SmartMarker options – treat the array as a single record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Process the JSON on the first worksheet
        workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);

        // 5️⃣ Optionally, add a header for clarity
        workbook.Worksheets[0].Cells["A1"].PutValue("Numbers");
        // Shift data down one row so the header stays on top
        workbook.Worksheets[0].Cells.InsertRows(1, 1);

        // 6️⃣ Save the workbook
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Excel workbook created at: {outputPath}");
    }
}
```

**Oczekiwany wynik w Excelu**

| Numbers |
|---------|
| 1       |
| 2       |
| 3       |

Wiersz nagłówka („Numbers”) jest opcjonalny, ale pokazuje, jak można mieszać ręczne edycje komórek z przetwarzaniem smart‑markerów.

---

## Częste pytania i przypadki brzegowe

### Co zrobić, gdy mój JSON jest obiektem, a nie tablicą?

```json
{
  "Name": "Alice",
  "Age": 30,
  "Country": "USA"
}
```

Wciąż możesz używać `SmartMarkerProcessor`. Umieść znaczniki takie jak `${Name}`, `${Age}`, `${Country}` w arkuszu, a następnie wywołaj `StartSmartMarkerProcessing`. Procesor zastąpi każdy znacznik odpowiednią wartością.

### Jak obsłużyć duże pliki JSON (megabajty)?

- **Strumieniowanie JSON**: Zamiast wczytywać cały ciąg, odczytaj plik przy pomocy `StreamReader` i przekaż tekst do `StartSmartMarkerProcessing`.  
- **Zwiększ limit pamięci**: Ustaw `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` jeśli napotkasz `OutOfMemoryException`.  
- **Przetwarzanie w partiach**: Podziel JSON na mniejsze tablice i przetwarzaj każdą część w osobnym arkuszu.

### Czy mogę wyeksportować do CSV zamiast XLSX?

Oczywiście. Po przetworzeniu po prostu wywołaj:

```csharp
workbook.Save("output.csv", SaveFormat.Csv);
```

Układ danych pozostaje taki sam; zmienia się jedynie format pliku.

### Co zrobić, gdy muszę sformatować komórki (czcionki, kolory) po załadowaniu JSON?

Możesz zastosować formatowanie po kroku smart‑marker:

```csharp
Style style = workbook.CreateStyle();
style.Font.IsBold = true;
workbook.Worksheets[0].Cells["A1"].SetStyle(style);
```

Ponieważ procesor uruchamia się jako pierwszy, wszelkie formatowanie dodane później nie zostanie nadpisane.

---

## Wskazówki i dobre praktyki

- **Zawsze ustawiaj `ArrayAsSingle` świadomie** – zapomnienie tej flagi jest częstą przyczyną nieoczekiwanego duplikowania wierszy.  
- **Waliduj JSON przed przetworzeniem** – niepoprawny ciąg wywoła `JsonParseException`. Owiń wywołanie w blok `try/catch`, aby obsłużyć błąd elegancko.  
- **Używaj nazwanych smart markerów** (`${Orders}`) dla czytelności, szczególnie przy zagnieżdżonych obiektach JSON.  
- **Trzymaj skoroszyt w pamięci**, jeśli zwracasz go z API webowego; przesyłanie `MemoryStream` eliminuje niepotrzebny dostęp do dysku.  
- **Kompatybilność wersji**: Powyższy kod działa z Aspose.Cells 23.12 i nowszymi. Sprawdź notatki wydania, jeśli używasz starszej wersji.

---

## Podsumowanie

Pokazaliśmy, jak **utworzyć skoroszyt Excel** z JSON przy użyciu Aspose.Cells, od instalacji biblioteki po zapisanie finalnego pliku. Opanowując `SmartMarkerProcessor` i jego opcje, możesz **ładować JSON do Excel**, **konwertować JSON do Excel** i nawet dostosowywać wyjście dla złożonych scenariuszy raportowych.  

Gotowy na kolejny krok? Spróbuj przetworzyć zagnieżdżoną tablicę obiektów, dodaj formatowanie warunkowe lub wyeksportuj wynik jako PDF – wszystko przy użyciu tego samego API Aspose.Cells. Twoje potoki danych‑do‑Excel są teraz tylko kilka linii kodu od gotowości.

Jeśli masz pytania lub napotkasz problem, zostaw komentarz poniżej. Szczęśliwego kodowania i przyjemności z zamieniania JSON w piękne arkusze kalkulacyjne! 

![Create Excel workbook with JSON data](/images/create-excel-workbook-json.png "Illustration of a JSON array being transformed into an Excel sheet")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}