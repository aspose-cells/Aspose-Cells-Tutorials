---
category: general
date: 2026-03-30
description: Szybko utwórz skoroszyt Excel w C# poprzez wstawienie danych JSON i zapisanie
  go jako plik XLSX. Dowiedz się, jak generować Excel z JSON, zapisywać JSON do Excela
  i wstawiać JSON do Excela.
draft: false
keywords:
- create excel workbook c#
- save workbook as xlsx
- generate excel from json
- write json to excel
- insert json into excel
language: pl
og_description: Szybko utwórz skoroszyt Excel w C# poprzez wstawienie danych JSON
  i zapisanie go jako XLSX. Postępuj zgodnie z tym przewodnikiem krok po kroku, aby
  wygenerować Excel z JSON.
og_title: Utwórz skoroszyt Excel w C# – Wstaw JSON i zapisz jako XLSX
tags:
- Aspose.Cells
- C#
- Excel automation
title: Utwórz skoroszyt Excel w C# – wstaw JSON i zapisz jako XLSX
url: /pl/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt Excel w C# – Wstaw JSON i zapisz jako XLSX

Czy kiedykolwiek potrzebowałeś **create Excel workbook C#** i wrzucić jakiś JSON prosto do komórki? Nie jesteś jedyny — programiści często napotykają ten sam problem, gdy mają ładunki API lub pliki konfiguracyjne, które muszą trafić do arkusza kalkulacyjnego w celu raportowania lub udostępniania.  

Dobre wieści są takie, że z Aspose.Cells możesz zrobić to w kilku linijkach, **save workbook as XLSX**, i zachować cały proces typowo‑bezpieczny. W tym poradniku **generate Excel from JSON**, **write JSON to Excel**, oraz pokażemy dokładne kroki, aby **insert JSON into Excel** bez uciążliwych konkatenacji łańcuchów.

## Co obejmuje ten przewodnik

Przejdziemy przez:

1. Utworzenie nowego skoroszytu.  
2. Dodanie Smart Marker, który oczekuje JSON.  
3. Przekazanie tablicy JSON do markera.  
4. Dostosowanie `SmartMarkerOptions`, aby JSON pozostał w jednej komórce.  
5. Zapisanie pliku jako skoroszyt XLSX.  

Po zakończeniu będziesz mieć gotowy do użycia plik `JsonSingleCell.xlsx` oraz solidny wzorzec, który możesz ponownie wykorzystać w dowolnym scenariuszu JSON‑to‑Excel. Bez zewnętrznych usług, tylko czysty C# i biblioteka Aspose.Cells.

**Wymagania wstępne**

- .NET 6+ (lub .NET Framework 4.6+).  
- Visual Studio 2022 lub dowolne IDE kompatybilne z C#.  
- Pakiet NuGet `Aspose.Cells` (bezpłatna wersja próbna lub licencjonowana).  

Jeśli masz te elementy, zanurzmy się — bez dodatkowej konfiguracji.

---

## Krok 1: Utwórz nowy skoroszyt w C#

Pierwszą rzeczą, której potrzebujesz, jest pusty obiekt workbook. Pomyśl o nim jak o nowym pliku Excel czekającym na dane.

```csharp
using Aspose.Cells;

// Initialize a new workbook – this is your empty Excel file
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

**Dlaczego to ważne:**  
`Workbook` jest punktem wejścia dla wszystkich operacji Excel. Tworząc go najpierw, zapewniasz, że późniejsze wywołanie **save workbook as xlsx** ma konkretny obiekt do serializacji.

> **Wskazówka:** Jeśli planujesz pracować z wieloma arkuszami, możesz dodać je teraz za pomocą `workbook.Worksheets.Add()`.

---

## Krok 2: Umieść Smart Marker, który oczekuje JSON

Smart Markery są symbolami zastępczymi, które Aspose.Cells zamienia w czasie wykonywania. Tutaj informujemy go, aby szukał ciągu JSON o nazwie `data`.

```csharp
// Put a Smart Marker in cell A1 – {{data:json}} tells Aspose to expect JSON
worksheet.Cells["A1"].PutValue("{{data:json}}");
```

**Dlaczego to ważne:**  
Sufiks `:json` informuje silnik, że przychodząca wartość jest JSON, a nie zwykłym tekstem. To klucz do **write json to excel** bez ręcznego parsowania.

---

## Krok 3: Zdefiniuj tablicę JSON

Teraz tworzymy JSON, który chcemy wstawić. Dla demonstracji użyjemy prostej listy osób.

```csharp
// Sample JSON array – could come from an API, file, or DB
string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Jane\",\"Age\":28}]";
```

**Przypadek brzegowy:**  
Jeśli Twój JSON zawiera podwójne cudzysłowy, upewnij się, że są one escapowane (jak pokazano) lub użyj łańcucha dosłownego (`@"..."`), aby uniknąć błędów kompilacji.

---

## Krok 4: Skonfiguruj opcje Smart Marker – zachowaj całą tablicę

Domyślnie Aspose próbowałby rozwinąć tablicę na wiele wierszy. Chcemy, aby cały ciąg JSON pozostał w jednej komórce, co jest idealne w scenariuszach **insert json into excel**, gdzie odbiorca później sparsuje JSON.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Treat the whole array as a single cell value
    ArrayAsSingle = true
};
```

**Dlaczego to ważne:**  
`ArrayAsSingle = true` zapobiega rozciąganiu na wiersze, dając czysty, jednowierszowy JSON w jednej komórce. To kluczowe, gdy arkusz jest formatem transportowym, a nie raportem.

---

## Krok 5: Przetwórz Smart Marker z danymi JSON

Teraz wiążemy JSON z markerem i pozwalamy Aspose wykonać ciężką pracę.

```csharp
// Process the marker – the anonymous object maps "data" to our JSON string
worksheet.SmartMarkers.Process(new { data = jsonData }, smartMarkerOptions);
```

**Co się dzieje w tle:**  
Aspose ocenia placeholder `{{data:json}}`, serializuje ciąg `jsonData` i zapisuje go w komórce A1, respektując ustawione opcje.

---

## Krok 6: Zapisz skoroszyt jako plik XLSX

Na koniec zapisujemy skoroszyt na dysku. To właśnie moment, w którym wkracza **save workbook as xlsx**.

```csharp
// Save the workbook – the extension determines the format (XLSX here)
workbook.Save("JsonSingleCell.xlsx");
```

**Wynik:**  
Otwórz `JsonSingleCell.xlsx` w Excelu, a zobaczysz tablicę JSON dokładnie tak, jak ją zdefiniowaliśmy, ładnie umieszczoną w komórce A1.

---

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do aplikacji konsolowej. Zawiera wszystkie powyższe kroki i działa od razu (zakładając, że pakiet NuGet Aspose.Cells jest zainstalowany).

```csharp
using System;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Add a Smart Marker that expects JSON
            worksheet.Cells["A1"].PutValue("{{data:json}}");

            // 3️⃣ Define the JSON array
            string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Jane\",\"Age\":28}]";

            // 4️⃣ Configure options – keep array as a single cell value
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 5️⃣ Process the marker with the JSON payload
            worksheet.SmartMarkers.Process(new { data = jsonData }, smartMarkerOptions);

            // 6️⃣ Save the workbook as XLSX
            workbook.Save("JsonSingleCell.xlsx");

            Console.WriteLine("Excel file created successfully! Check JsonSingleCell.xlsx.");
        }
    }
}
```

**Oczekiwany wynik w Excelu**

| A |
|---|
| `[{"Name":"John","Age":30},{"Name":"Jane","Age":28}]` |

Ta pojedyncza komórka teraz zawiera w pełni prawidłową tablicę JSON gotową do dalszego przetwarzania.

---

## Częste pytania i przypadki brzegowe

### Co zrobić, jeśli potrzebuję rozłożyć JSON na wiersze?

Ustaw `ArrayAsSingle = false` (wartość domyślna). Aspose utworzy wiersz dla każdego elementu tablicy, mapując właściwości obiektu na kolumny. To przydatne, gdy chcesz widok tabelaryczny zamiast surowego ciągu JSON.

### Czy mogę użyć pliku JSON zamiast łańcucha zakodowanego na sztywno?

Oczywiście. Odczytaj plik do łańcucha:

```csharp
string jsonData = File.ReadAllText("people.json");
```

Następnie przekaż `jsonData` do tego samego wywołania `Process`. Reszta potoku pozostaje niezmieniona.

### Czy to działa z dużymi ładunkami JSON?

Tak, ale obserwuj zużycie pamięci. Przy ogromnych tablicach rozważ strumieniowanie danych lub bezpośrednie zapisywanie do wierszy (`ArrayAsSingle = false`), aby uniknąć jednej gigantycznej komórki, z którą Excel może mieć problemy.

### Czy wygenerowany XLSX jest kompatybilny ze starszymi wersjami Excela?

Format `.xlsx` oparty jest na Office Open XML i działa od Excela 2007 wzwyż. Jeśli potrzebujesz starszego formatu `.xls`, zmień wywołanie zapisu:

```csharp
workbook.Save("JsonSingleCell.xls", SaveFormat.Excel97To2003);
```

---

## Pro tipy do pracy z JSON i Excelem

- **Validate JSON first** – użyj `System.Text.Json.JsonDocument.Parse(jsonData)`, aby wcześnie wykryć nieprawidłowe dane.  
- **Escape special characters** – jeśli Twój JSON zawiera znaki nowej linii, pojawią się jako dosłowne `\n` w komórce; możesz je zamienić na `Environment.NewLine` przed przetwarzaniem.  
- **Reuse Smart Markers** – możesz umieścić wiele markerów w tym samym arkuszu, każdy wskazujący na inną właściwość JSON.  
- **Combine with formulas** – po umieszczeniu JSON w komórce możesz użyć funkcji Excel `FILTERXML` (w nowszych wersjach), aby parsować go na bieżąco.

---

## Podsumowanie

Teraz wiesz, jak **create excel workbook c#**, osadzić ładunek JSON i **save workbook as xlsx** przy użyciu Aspose.Cells. Ten wzorzec pozwala **generate excel from json**, **write json to excel** i **insert json into excel** za pomocą kilku linijek kodu, ułatwiając wymianę danych między usługami a analitykami.  

Gotowy na kolejny krok? Spróbuj przekonwertować tablicę JSON na właściwą tabelę (ustaw `ArrayAsSingle = false`) lub zbadaj stylizację arkusza po wstawieniu. To samo podejście działa dla CSV, XML lub nawet własnych obiektów — wystarczy dostosować typ Smart Marker.  

Miłego kodowania i śmiało eksperymentuj! Jeśli napotkasz problemy, zostaw komentarz poniżej lub zajrzyj do oficjalnej dokumentacji Aspose, aby głębiej zagłębić się w Smart Markery.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}