---
category: general
date: 2026-05-04
description: Utwórz plik Excel z szablonu i mapuj JSON do Excela z dynamicznym nazewnictwem
  arkuszy. Dowiedz się, jak wypełnić Excel z JSON i wygenerować Excel przy użyciu
  JSON w kilka minut.
draft: false
keywords:
- create excel from template
- map json to excel
- populate excel from json
- dynamic worksheet naming excel
- generate excel using json
language: pl
og_description: Szybko twórz pliki Excel z szablonu. Ten przewodnik pokazuje, jak
  mapować JSON do Excela, wypełniać Excel danymi z JSON, używać dynamicznego nazewnictwa
  arkuszy oraz generować Excel przy użyciu JSON.
og_title: Utwórz Excel z szablonu – Kompletny samouczek .NET
tags:
- C#
- Aspose.Cells
- SmartMarker
- JSON
title: Tworzenie Excela z szablonu – Przewodnik krok po kroku dla programistów .NET
url: /pl/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie Excela z szablonu – Kompletny samouczek .NET

Czy kiedykolwiek potrzebowałeś **create Excel from template**, ale utknąłeś, żonglując danymi JSON i nazwami arkuszy? Nie jesteś jedyny. W wielu projektach raportowych szablon zawiera układ, a ładunek JSON dostarcza rzeczywiste wartości, a połączenie ich ze sobą może być uciążliwe.  

Dobre wieści? Kilka linii C# i silnika SmartMarker w Aspose Cells pozwala **populate Excel from JSON**, zmienić nazwę arkuszy szczegółowych w locie i w końcu **generate Excel using JSON** bez konieczności dotykania interfejsu użytkownika.  

W tym samouczku przeprowadzimy Cię przez cały proces: wczytanie szablonu, mapowanie JSON do Excela, konfigurowanie dynamicznego nadawania nazw arkuszom oraz zapisanie finalnego skoroszytu. Po zakończeniu będziesz mieć wielokrotnego użytku fragment kodu, który możesz wstawić do dowolnej usługi .NET. Bez zewnętrznych narzędzi, tylko czysty kod.

---

## Czego będziesz potrzebował

- **Aspose.Cells for .NET** (v24.10 lub nowszy) – biblioteka napędzająca SmartMarker.  
- Plik **template.xlsx** zawierający znaczniki SmartMarker, takie jak `{Master:Name}` i `{Detail:Item}`.  
- Plik **data.json** odpowiadający strukturze master‑detail.  
- Visual Studio 2022 (lub dowolne preferowane IDE) docelowo .NET 6 lub nowszy.  

To wszystko. Jeśli masz już te elementy, jesteś gotowy do startu.

---

## Tworzenie Excela z szablonu – przegląd

Podstawowa idea jest prosta: traktuj plik Excel jako *szablon* i pozwól SmartMarkerowi zastąpić znaczniki wartościami z Twojego JSON. Biblioteka umożliwia także zmianę nazwy arkusza szczegółowego na podstawie pola master, co jest właśnie mocną stroną **dynamic worksheet naming excel**.  

Poniżej znajduje się pełny, gotowy do uruchomienia kod. Śmiało skopiuj i wklej go do aplikacji konsolowej oraz wskaż ścieżki do własnych plików.

```csharp
// ------------------------------------------------------------
// Full example: create Excel from template using JSON data
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains SmartMarker tags
            //    (e.g., {Master:Name} in the master sheet and {Detail:Item} in the detail sheet)
            string templatePath = @"C:\MyProject\Templates\template.xlsx";
            Workbook wb = new Workbook(templatePath);

            // 2️⃣ Read the JSON data that will populate the markers
            //    The JSON should match the structure expected by the template.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // 3️⃣ Configure the SmartMarker processor to rename the detail sheet
            //    dynamically based on the master record’s Name field.
            //    This demonstrates dynamic worksheet naming excel.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // 4️⃣ Execute the SmartMarker processing using the JSON data.
            //    This step maps JSON to Excel and populates every marker.
            wb.SmartMarkerProcessor.Execute(json);

            // 5️⃣ Save the processed workbook – now it’s a brand‑new file.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Excel file generated successfully at: " + outputPath);
        }
    }
}
```

> **Oczekiwany rezultat:**  
> - Arkusz master wyświetli nazwę z `Master.Name`.  
> - Arkusz detail zostanie przemianowany na coś w stylu `Detail_JohnDoe`.  
> - Wszystkie wiersze `{Detail:Item}` zostaną wypełnione tablicą items z JSON.

---

## Mapowanie JSON do Excela – wczytywanie danych

Zanim silnik SmartMarker wykona swoją magię, JSON musi być **poprawnie sformatowany** i odzwierciedlać hierarchię używaną w szablonie. Typowy JSON master‑detail wygląda tak:

```json
{
  "Master": {
    "Name": "John Doe",
    "Date": "2026-05-04"
  },
  "Detail": [
    { "Item": "Widget A", "Qty": 10, "Price": 2.5 },
    { "Item": "Widget B", "Qty": 5,  "Price": 5.0 }
  ]
}
```

**Dlaczego to jest ważne:**  
- Klucze `Master` i `Detail` bezpośrednio odpowiadają znacznikom `{Master:…}` i `{Detail:…}`.  
- Jeśli struktura JSON odbiega, SmartMarker nie znajdzie dopasowania i komórki pozostaną puste.  

**Wskazówka:** Zweryfikuj swój JSON przy użyciu szybkiego walidatora online lub `System.Text.Json.JsonDocument.Parse(json)`, aby wcześnie wykryć błędy składni.

---

## Wypełnianie Excela z JSON – konfiguracja SmartMarker

SmartMarker działa, skanując skoroszyt w poszukiwaniu znaczników, a następnie wstrzykując dane. Krok **populate excel from json** to w zasadzie wywołanie `Execute`, które widzieliśmy wcześniej, ale istnieje kilka opcjonalnych ustawień, które warto wymienić:

| Ustawienie | Co robi | Kiedy używać |
|------------|---------|--------------|
| `Options.CaseSensitive` | Traktuje nazwy znaczników jako wrażliwe na wielkość liter. | Gdy szablon miesza wielkość liter i potrzebne jest ścisłe dopasowanie. |
| `Options.RemoveEmptyRows` | Usuwa wiersze, które nie otrzymały danych. | Aby utrzymać finalny arkusz w porządku, gdy niektóre elementy detail są opcjonalne. |
| `Options.EnableHyperlink` | Pozwala, aby hiperłącza w JSON stały się klikalne. | Gdy potrzebujesz klikalnych adresów URL w raporcie. |

Możesz je łączyć w następujący sposób:

```csharp
wb.SmartMarkerProcessor.Options.CaseSensitive = true;
wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;
```

---

## Dynamic Worksheet Naming Excel – konfiguracja nazwy arkusza szczegółowego

Jednym z trudniejszych wymagań w wielu projektach jest **dynamic worksheet naming excel**. Zamiast statycznego arkusza „Detail”, możesz chcieć, aby każdy raport zawierał nazwę klienta lub numer zamówienia.  

Linia:

```csharp
wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";
```

robi dokładnie to. Znacznik `{Master.Name}` jest zastępowany *po* przetworzeniu JSON, więc nowa nazwa arkusza staje się `Detail_JohnDoe`.  

**Przypadek brzegowy:** Jeśli nazwa zawiera znaki niedozwolone w nazwach arkuszy (`:`, `\`, `/`, `?`, `*`, `[`, `]`), Aspose automatycznie je oczyszcza, ale możesz wstępnie oczyścić ciąg w JSON, jeśli potrzebny jest konkretny format.

---

## Generowanie Excela przy użyciu JSON – wykonanie i zapis

Ostatnie dwie linie kodu (`Execute` i `Save`) to miejsce, w którym dzieje się magia **generate excel using json**. W tle Aspose parsuje JSON do tabeli danych, iteruje po szablonie i zapisuje plik wyjściowy.  

Jeśli potrzebujesz generować wiele skoroszytów w pętli (np. po jednym na klienta), po prostu przenieś tworzenie `Workbook` do wnętrza pętli i odpowiednio zmień nazwę pliku wyjściowego:

```csharp
foreach (var customerJson in customers)
{
    Workbook wb = new Workbook(templatePath);
    wb.SmartMarkerProcessor.Options.DetailSheetNewName = $"Detail_{customerJson.Master.Name}";
    wb.SmartMarkerProcessor.Execute(customerJson);
    wb.Save($@"C:\Reports\Report_{customerJson.Master.Name}.xlsx");
}
```

Ten wzorzec jest powszechny w usługach raportowania wsadowego.

---

## Częste pułapki i wskazówki profesjonalne

- **Brakujące znaczniki:** Jeśli komórka nadal pokazuje `{Master:Name}`, znacznik nie został rozpoznany. Sprawdź pisownię i upewnij się, że znacznik znajduje się w komórce, a nie w komentarzu.  
- **Duże ładunki JSON:** Przy ogromnych zestawach danych rozważ strumieniowanie JSON lub użycie `DataTable` zamiast surowego ciągu, aby zmniejszyć obciążenie pamięci.  
- **Bezpieczeństwo wątków:** Instancje `Workbook` nie są bezpieczne wątkowo. Utwórz nową instancję na wątek, jeśli uruchamiasz zadania równoległe.  
- **Blokady plików:** Upewnij się, że szablon nie jest otwarty w Excelu podczas działania kodu; w przeciwnym razie napotkasz `IOException`.  

> **Wskazówka pro:** Przechowuj kopię oryginalnego szablonu w folderze tylko do odczytu. Zapobiega to przypadkowym nadpisaniom podczas debugowania.

---

## Pełny działający przykład – podsumowanie

Oto cały program ponownie, tym razem z komentarzami wierszowymi dla każdej nieoczywistej linii:

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Path to the Excel template that contains SmartMarker tags.
            string templatePath = @"C:\MyProject\Templates\template.xlsx";

            // Load the workbook – this is the "create excel from template" step.
            Workbook wb = new Workbook(templatePath);

            // Read JSON data that maps directly to the template's tags.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // OPTIONAL: tweak SmartMarker behavior (case‑sensitivity, empty rows, etc.).
            wb.SmartMarkerProcessor.Options.CaseSensitive = false;
            wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;

            // Set up dynamic worksheet naming based on the master record's Name field.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // Run the SmartMarker engine – this is where we "populate excel from json".
            wb.SmartMarkerProcessor.Execute(json);

            // Save the newly generated workbook – the final "generate excel using json" step.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Workbook created at: " + outputPath);
        }
    }
}
```

Uruchomienie tej aplikacji konsolowej wygeneruje `output.xlsx` z przemianowanym arkuszem detail i wszystkimi wypełnionymi danymi.

---

## Kolejne kroki i powiązane tematy

- **Eksport do PDF:** Po wygenerowaniu skoroszytu możesz wywołać `wb.Save("report.pdf", SaveFormat.Pdf);`, aby dostarczyć wersję PDF.  
- **Wypełnianie wykresów:** SmartMarker obsługuje także źródła danych wykresów; wystarczy powiązać tablicę JSON z zakresem serii wykresu.  
- **Formatowanie warunkowe:** Użyj wbudowanych reguł Excela w szablonie; przetrwają one po zamianie przez SmartMarker.  
- **Optymalizacja wydajności:** W scenariuszach o dużej objętości ponownie używaj jednej instancji `Workbook` z `Clone`, aby uniknąć wielokrotnego odczytu/zapisu plików.  

Śmiało eksperymentuj z różnymi strukturami JSON, wzorcami nazewnictwa lub nawet łącz wiele szablonów w jednym uruchomieniu. Elastyczność **create excel from template** przy użyciu Aspose.Cells pozwala dostosować rozwiązanie do faktur, pulpitów nawigacyjnych czy dowolnych potrzeb raportowych.

---

## Wizualne podsumowanie

![Przepływ pracy Create Excel from Template pokazujący JSON → SmartMarker → Dynamic Sheet Naming](/images/create-excel-from-template-workflow.png "Diagram przepływu Create Excel from Template")

*(Tekst alternatywny zawiera główne słowo kluczowe dla SEO)*

---

### Podsumowanie

Omówiliśmy wszystko, co potrzebne do **create Excel from template**, **map JSON to Excel**, **populate Excel from JSON**, użycia **dynamic worksheet naming excel**, a w końcu **generate Excel using JSON**. Kod jest kompletny, wyjaśnienia mówią *dlaczego* każda linia ma znaczenie i masz teraz solidne podstawy do budowy większych potoków raportowych.  

Masz pomysł, który chcesz wdrożyć? Dodaj komentarz poniżej, a wspólnie rozwiążemy problem. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}