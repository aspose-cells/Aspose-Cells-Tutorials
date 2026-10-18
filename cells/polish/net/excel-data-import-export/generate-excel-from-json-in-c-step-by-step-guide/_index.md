---
category: general
date: 2026-03-18
description: Dowiedz się, jak generować plik Excel z JSON przy użyciu C#, zezwolić
  na duplikaty nazw arkuszy, utworzyć arkusz szczegółowy i zapisać skoroszyt w C#
  w kilka minut.
draft: false
keywords:
- generate excel from json
- allow duplicate sheet names
- how to create detail sheet
- save workbook c#
- smartmarker options
- aspnet cells integration
language: pl
og_description: Generuj plik Excel z JSON przy użyciu C#. Ten przewodnik pokazuje,
  jak zezwolić na duplikaty nazw arkuszy, utworzyć arkusz szczegółowy oraz zapisać
  skoroszyt w C# przy użyciu Aspose.Cells.
og_title: Generuj Excel z JSON w C# – Kompletny poradnik
tags:
- C#
- Excel automation
- JSON
- Aspose.Cells
title: Generowanie Excela z JSON w C# – Przewodnik krok po kroku
url: /pl/net/excel-data-import-export/generate-excel-from-json-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Generowanie pliku Excel z JSON w C# – Przewodnik krok po kroku

Kiedykolwiek potrzebowałeś **generować Excel z JSON**, ale nie byłeś pewien, która biblioteka poradzi sobie z ciężkim zadaniem? Nie jesteś sam. W wielu aplikacjach korporacyjnych otrzymujemy ładunki danych w formacie JSON i musimy przenieść te dane do ładnie sformatowanych arkuszy kalkulacyjnych — pomyśl o raportach sprzedaży, wyciągach z inwentarza czy logach audytu. Dobra wiadomość? Dzięki silnikowi SmartMarker firmy Aspose.Cells możesz zamienić ciąg JSON w w pełni funkcjonalny plik Excel w zaledwie kilku linijkach.

W tym samouczku przeprowadzimy Cię przez cały proces: od przygotowania ładunku JSON, konfiguracji SmartMarker, aby **zezwolić na duplikowanie nazw arkuszy**, stworzenia **arkusza szczegółowego**, aż po **zapisanie skoroszytu w stylu C#**. Po zakończeniu będziesz mieć fragment kodu, który możesz wstawić do dowolnego projektu .NET.

> **Szybkie podsumowanie:**  
> • Główny cel – generowanie Excel z JSON.  
> • Cele dodatkowe – zezwolić na duplikowanie nazw arkuszy, stworzyć arkusz szczegółowy, zapisać skoroszyt w C#.  

## Wymagania wstępne

- .NET 6.0 SDK (lub dowolna nowsza wersja .NET).  
- Visual Studio 2022 lub VS Code z rozszerzeniem C#.  
- Aktywna licencja lub darmowa wersja próbna **Aspose.Cells for .NET** (pakiet NuGet to `Aspose.Cells`).  
- Plik szablonu Excel (`template.xlsx`), który już zawiera znaczniki SmartMarker, takie jak `&=Name` oraz placeholder tabeli szczegółowej.

Jeśli któryś z nich jest Ci nieznany, nie panikuj — instalacja pakietu NuGet to pojedyncze polecenie, a szablon może być zwykłym skoroszytem z kilkoma komórkami placeholder.

## Przegląd rozwiązania

Na wysokim poziomie wykonamy:

1. Zdefiniować ciąg JSON odzwierciedlający dane, które chcemy umieścić w arkuszu.  
2. Skonfigurować `SmartMarkerOptions`, aby zezwalał na duplikowanie nazw arkuszy oraz aby **arkusz szczegółowy** otrzymał przewidywalną nazwę.  
3. Wczytać szablon Excel zawierający znaczniki SmartMarker.  
4. Uruchomić procesor SmartMarker, aby połączyć dane JSON ze skoroszytem.  
5. Zapisać ostateczny plik przy użyciu `workbook.Save(...)`.

Każdy krok jest wyjaśniony poniżej, z pełnymi fragmentami kodu i wyjaśnieniem, dlaczego jest istotny.

---

## Krok 1 – Przygotuj ładunek JSON, który zostanie scalony

Pierwszą rzeczą, której potrzebujesz, jest dokument JSON pasujący do znaczników SmartMarker w Twoim szablonie. Traktuj JSON jako źródło prawdy; każdy klucz staje się placeholderem w pliku Excel.

```csharp
// Step 1: Define the JSON data that will be merged into the worksheet
string jsonData = @"{
    ""Name"": ""John"",
    ""Date"": ""2023-01-01"",
    ""Orders"": [
        { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
        { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
    ]
}";
```

**Dlaczego to jest ważne:**  
SmartMarker odczytuje hierarchię JSON i automatycznie rozszerza tabele dla kolekcji, takich jak `Orders`. Jeśli struktura JSON nie odpowiada znacznikom, scalanie cicho wygeneruje puste wiersze — częsty problem.

---

## Krok 2 – Skonfiguruj SmartMarker, aby zezwalał na duplikowanie nazw arkuszy i nazwij arkusz szczegółowy

Domyślnie Aspose.Cells zabrania duplikowania nazw arkuszy, co może być przeszkodą przy generowaniu arkusza szczegółowego dla każdego rekordu głównego. Klasa `SmartMarkerOptions` pozwala złagodzić tę regułę oraz określić wzorzec nazewnictwa dla nowo tworzonych arkuszy szczegółowych.

```csharp
// Step 2: Create SmartMarker options and allow duplicate base names for detail sheets
var smartMarkerOptions = new Aspose.Cells.SmartMarker.SmartMarkerOptions
{
    // When a detail sheet is generated, it will be named "Detail", "Detail (2)", etc.
    DetailSheetNewName = "Detail",

    // This flag tells the engine that duplicate sheet names are acceptable.
    // Useful when you generate multiple detail sheets from a loop.
    AllowDuplicateSheetNames = true
};
```

**Dlaczego to jest ważne:**  
Jeśli iterujesz po wielu klientach i każda iteracja tworzy nowy arkusz, silnik normalnie wyrzuci wyjątek. Ustawienie `AllowDuplicateSheetNames` na `true` powoduje, że Aspose.Cells automatycznie dodaje numeryczny sufiks, co utrzymuje proces płynnym.

---

## Krok 3 – Wczytaj szablon Excel zawierający znaczniki SmartMarker

Twój szablon to płótno, na którym SmartMarker namaluje dane. Może zawierać dowolne formatowanie — kolory, formuły, wykresy — więc nie musisz odtwarzać tej logiki programowo.

```csharp
// Step 3: Load the workbook that contains SmartMarker tags
using var workbook = new Aspose.Cells.Workbook(@"C:\MyProjects\ExcelDemo\template.xlsx");
```

**Wskazówka:**  
Przechowuj szablon w folderze będącym częścią wyjścia Twojego projektu (np. `Content\Templates`). Dzięki temu możesz odwoływać się do niego przy użyciu ścieżki względnej i uniknąć twardego kodowania ścieżek bezwzględnych.

---

## Krok 4 – Uruchom procesor SmartMarker z JSON i opcjami

Teraz dzieje się magia. `SmartMarkerProcessor` odczytuje JSON, respektuje ustawione opcje i wypełnia skoroszyt odpowiednio.

```csharp
// Step 4: Process the SmartMarker tags using the JSON data and the configured options
workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);
```

**Co dzieje się pod maską?**  
- Procesor skanuje każdą komórkę w poszukiwaniu znaczników takich jak `&=Name` lub `&=Orders.Item`.  
- Zastępuje proste znaczniki wartościami skalarnymi (`Name`, `Date`).  
- Dla kolekcji (`Orders`) tworzy nowy arkusz szczegółowy (nazwany „Detail”) i wypełnia wiersz tabeli dla każdego elementu.  
- Ponieważ zezwoliliśmy na duplikowanie nazw arkuszy, jeśli szablon już posiadał arkusz o nazwie „Detail”, silnik utworzy „Detail (2)”.

---

## Krok 5 – Zapisz scalony skoroszyt na dysku

Na koniec zapisz wypełniony skoroszyt do pliku. Możesz wybrać dowolny format obsługiwany przez Aspose.Cells — XLSX, CSV, PDF itp. Tutaj pozostaniemy przy nowoczesnym XLSX.

```csharp
// Step 5: Save the workbook with the merged data
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

**Dlaczego to jest ważne:**  
Zapisywanie to miejsce, w którym faktycznie **zapisujesz skoroszyt w stylu C#**. Jeśli potrzebujesz przesłać plik z powrotem do klienta webowego, możesz użyć `workbook.Save(Stream, SaveFormat.Xlsx)`.

---

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny, gotowy do uruchomienia program konsolowy. Upewnij się, że przed kompilacją zainstalowałeś pakiet NuGet `Aspose.Cells` (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace ExcelFromJsonDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Define the JSON payload
            string jsonData = @"{
                ""Name"": ""John"",
                ""Date"": ""2023-01-01"",
                ""Orders"": [
                    { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
                    { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
                ]
            }";

            // 2️⃣ Configure SmartMarker options – allow duplicate sheet names & set detail sheet name
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail",
                AllowDuplicateSheetNames = true
            };

            // 3️⃣ Load the template workbook (ensure the path is correct)
            var workbookPath = @"C:\MyProjects\ExcelDemo\template.xlsx";
            using var workbook = new Workbook(workbookPath);

            // 4️⃣ Merge JSON data into the workbook
            workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);

            // 5️⃣ Save the result
            var outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Excel file generated successfully at: {outputPath}");
        }
    }
}
```

### Oczekiwany wynik

- **Arkusz 1** (arkusz główny) wyświetli „John” w komórce `Name` oraz „2023‑01‑01” w komórce `Date`.  
- Nowy arkusz **Detail** pojawi się, zawierający tabelę z dwoma wierszami: jeden dla zamówienia Laptop, drugi dla zamówienia Mouse.  
- Jeśli szablon już miał arkusz o nazwie „Detail”, nowy arkusz zostanie nazwany „Detail (2)”, dzięki flagi `AllowDuplicateSheetNames`.

![Wyjście Excel pokazujące arkusz główny z nazwą i datą oraz arkusz Detail z wierszami zamówień](excel-output.png "wynik generowania excel z json")

*Image alt text:* **generowanie excel z json – przykładowy skoroszyt z arkuszami głównym i szczegółowym**

---

## Częste pytania i przypadki brzegowe

### Co jeśli mój JSON zawiera zagnieżdżone kolekcje?

SmartMarker może obsługiwać zagnieżdżone tablice, ale będziesz musiał dodać dodatkowe arkusze szczegółowe lub użyć znaczników hierarchicznych. Na przykład, `&=Orders.SubItems.Product` automatycznie wygeneruje arkusz trzeciego poziomu.

### Jak dostosować wzorzec nazewnictwa dla duplikowanych arkuszy?

Zamiast statycznego `DetailSheetNewName` możesz przypisać wywołanie zwrotne za pomocą `smartMarkerOptions.DetailSheetNameGenerator`. Pozwala to osadzić znaczniki czasu lub unikalne ID w nazwie arkusza.

```csharp
smartMarkerOptions.DetailSheetNameGenerator = (baseName, index) =>
    $"{baseName}_{DateTime.Now:yyyyMMdd}_{index}";
```

### Czy mogę generować CSV zamiast XLSX?

Oczywiście. Zastąp ostatnie wywołanie `Save` następującym:

```csharp
workbook.Save(outputPath, SaveFormat.Csv);
```

Reszta potoku pozostaje identyczna.

### Czy to działa w ASP.NET Core?

Tak. Ten sam kod może działać wewnątrz akcji kontrolera. Po prostu strumieniuj skoroszyt w odpowiedzi:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0;
return File(ms, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "report.xlsx");
```

---

## Porady profesjonalne i pułapki

- **Porada:** Trzymaj znaczniki SmartMarker w osobnym arkuszu „Template”. Dzięki temu możesz chronić arkusz przed przypadkowymi edycjami, jednocześnie pozwalając procesorowi go odczytać.  
- **Uwaga:** klucze JSON zawierające spacje lub znaki specjalne. Aspose.Cells oczekuje prawidłowych identyfikatorów JavaScript; zmień ich nazwy lub użyj atrybutu `JsonProperty`, jeśli deserializujesz z POCO.  
- **Wskazówka wydajnościowa:** Jeśli przetwarzasz tysiące wierszy, ustaw `smartMarkerOptions.EnableCache = true`, aby ponownie używać skompilowanych znaczników.  
- **Sprawdzenie wersji:** Powyższy kod jest przeznaczony dla Aspose.Cells 23.9+. Wcześniejsze wersje mogą nie obsługiwać `AllowDuplicateSheetNames`.

---

## Zakończenie

Masz teraz kompletny, kompleksowy przepis na **generowanie Excel z JSON** w C#. Konfigurując `SmartMarkerOptions`, pokazaliśmy, jak **zezwolić na duplikowanie nazw arkuszy**, kontrolować nazewnictwo **arkusza szczegółowego** oraz w końcu **zapisać skoroszyt w stylu C#**. Podejście jest w pełni samodzielne — bez zewnętrznych usług, tylko jeden pakiet NuGet.

Kolejne kroki? Spróbuj zamienić źródło JSON na prawdziwe API

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}