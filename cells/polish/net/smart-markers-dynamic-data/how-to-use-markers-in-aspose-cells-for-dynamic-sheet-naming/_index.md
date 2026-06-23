---
category: general
date: 2026-05-23
description: Jak używać znaczników w Aspose.Cells, aby uzyskać dynamiczne nazewnictwo
  arkuszy w automatyzacji Excel. Dowiedz się, jak korzystać ze smart markers, wiązania
  danych JSON i tworzenia arkuszy w kilka minut.
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: pl
og_description: Jak używać znaczników w Aspose.Cells do generowania plików Excel z
  dynamiczną nazwą arkuszy. Kompletny przewodnik krok po kroku z pełnym przykładem
  w C#.
og_title: Jak używać znaczników – dynamiczne nazewnictwo arkuszy w Excelu z Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak używać znaczników w Aspose.Cells do dynamicznego nazewnictwa arkuszy w
  Excelu
url: /pl/net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać markerów w Aspose.Cells do dynamicznego nazewnictwa arkuszy w Excelu

Zastanawiałeś się kiedyś **jak używać markerów**, aby zamienić statyczny szablon Excela w w pełni rozbudowany skoroszyt master‑detail? Nie jesteś sam. Wielu programistów napotyka trudności, gdy potrzebują możliwości *dynamicznego nazewnictwa arkuszy w Excelu*, szczególnie gdy nazwy arkuszy muszą odzwierciedlać wartości danych pochodzących z JSON lub bazy danych.  

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład w C#, który pokazuje **jak używać markerów** z **Aspose.Cells** smart markers, wiązanie danych JSON i pozwala procesorowi tworzyć arkusze, których nazwy zmieniają się w locie. Bez zbędnych wstępów, tylko dokładny kod, który możesz wkleić do Visual Studio i od razu zobaczyć wyniki.

## Czego się nauczysz

- Koncepcję **smart markers** i dlaczego są idealne dla scenariuszy master‑detail.  
- Jak osadzić znaczniki markerów w skoroszycie, które później zostaną zastąpione rzeczywistymi nazwami arkuszy.  
- Konfigurowanie **dynamicznego nazewnictwa arkuszy w Excelu** przy użyciu opcji `DetailSheetNewName`.  
- Uruchamianie `SmartMarkerProcessor` na danych JSON w celu automatycznego generowania wielu arkuszy.  
- Weryfikację wyniku oraz kilka praktycznych wskazówek, jak unikać typowych pułapek.

> **Wymagania wstępne** – Potrzebujesz aktualnego środowiska .NET (≥ .NET 6), biblioteki Aspose.Cells for .NET (możesz pobrać darmową wersję próbną z Aspose) oraz podstawowej znajomości C#.  

---

![przykład użycia markerów w Aspose.Cells](example.png "przykład użycia markerów w Aspose.Cells")

## Jak używać markerów do tworzenia dynamicznego nazewnictwa arkuszy (Krok 1)

Pierwszą rzeczą, której potrzebujemy, jest pusty skoroszyt, który będzie pełnił rolę naszego szablonu. W prawdziwym projekcie prawdopodobnie rozpoczniesz od istniejącego pliku `.xlsx`, który już zawiera układ, formatowanie i komórki zastępcze. Dla przejrzystości stworzymy wszystko programowo.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*Dlaczego to ważne*: Obiekt `Worksheet` to miejsce, w którym umieścimy nasze **smart marker** tagi. Traktuj tagi jako małe zastępniki, które procesor później zamieni na rzeczywiste wartości z JSON.

## Wstawianie tagów Smart Marker (Krok 2)

Teraz umieszczamy znaczniki markerów bezpośrednio w komórkach. Składnia `${...}` informuje Aspose.Cells, że „to jest znacznik”. W naszym przykładzie potrzebujemy dwóch znaczników: jednego dla nazwy arkusza master i drugiego dla nazwy arkusza detail.

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **Pro tip** – Trzymaj nazwy markerów krótkie i znaczące; stają się one kluczami, których użyjesz w ładunku JSON.

## Przygotowanie danych JSON (Krok 3)

Procesor działa z dowolnym źródłem danych, które może być przedstawione jako JSON, `DataSet` lub nawet zwykły obiekt. Oto minimalny ciąg JSON zawierający kolekcję master‑detail. Zauważ, że każde zamówienie zawiera zarówno `MasterSheetName`, jak i `DetailSheetName`.

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*Dlaczego JSON?* To lekki, czytelny dla człowieka format, który świetnie współpracuje z API webowymi. Możesz równie łatwo pobrać te dane z zapytania SQL i zserializować je przy pomocy `Newtonsoft.Json`.

## Inicjalizacja SmartMarkerProcessor (Krok 4)

`SmartMarkerProcessor` to silnik, który skanuje skoroszyt, znajduje znaczniki i wykonuje wiązanie danych. Utworzenie go to jednowierszowy kod.

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## Definiowanie dynamicznego nazewnictwa arkuszy (Krok 5)

Tutaj **dynamiczne nazewnictwo arkuszy w Excelu** naprawdę błyszczy. Ustawiając `DetailSheetNewName`, informujemy procesor, aby dla każdego zamówienia utworzył nowy arkusz detail i nazwał go na podstawie `OrderId`. Zastępnik `${OrderId}` jest rozwiązywany z bieżącego rekordu podczas przetwarzania.

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **Uwaga** – Jeśli zapomnisz dodać składni `${}`, arkusz zostanie dosłownie nazwany „Detail_${OrderId}” zamiast „Detail_1”, „Detail_2” itd.

## Zastosowanie JSON i generowanie arkuszy (Krok 6)

Teraz pozwalamy procesorowi wykonać ciężką pracę. Przeczyta JSON, zastąpi znaczniki i utworzy nowe arkusze w razie potrzeby.

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### Co się dzieje w tle?

1. Procesor odczytuje tablicę `Orders`.  
2. Dla każdego zamówienia tworzy **arkusz master** (używając `${Orders.MasterSheetName}`) oraz **arkusz detail** (korzystając ze wzorca `DetailSheetNewName`).  
3. Wartości komórek są zastępowane odpowiednimi polami JSON, więc pierwsza komórka arkusza master kończy jako „Master_1”, „Master_2” itd.  

## Zapis i weryfikacja wyniku (Opcjonalnie)

Na koniec zapisujemy skoroszyt na dysku. Otwórz plik w Excelu i powinieneś zobaczyć dwa arkusze master (`Master_1`, `Master_2`) oraz dwa dynamicznie nazwane arkusze detail (`Detail_1`, `Detail_2`).  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**Oczekiwany wynik** – Po otwarciu `output.xlsx` zobaczysz:

- Arkusz **Master_1** z komórką A1 = „Master_1”.  
- Arkusz **Detail_1** z komórką A1 = „Detail_1”.  
- Arkusz **Master_2** z komórką A1 = „Master_2”.  
- Arkusz **Detail_2** z komórką A1 = „Detail_2”.  

To pełny cykl **jak używać markerów**, aby osiągnąć **dynamiczne nazewnictwo arkuszy w Excelu** przy użyciu **Aspose.Cells smart markers**.

---

## Często zadawane pytania i przypadki brzegowe

### Co zrobić, jeśli potrzebuję więcej niż dwóch poziomów hierarchii?

Możesz zagnieżdżać znaczniki wewnątrz nowo utworzonych arkuszy detail. Po prostu umieść dodatkowe tagi `${...}` w szablonie przed przetworzeniem. Procesor automatycznie przejdzie przez każdy poziom.

### Czy mogę użyć DataTable zamiast JSON?

Oczywiście. `SmartMarkerProcessor` ma przeciążenia dla `DataSet`, `DataTable` i nawet własnych obiektów. Jedyną zmianą jest wywołanie zamiast `ApplyJson` – użyjesz `ApplyDataSet(myDataSet)`.

### Jak kontrolować kolejność tworzenia arkuszy?

Kolejność podąża za kolejnością w źródłowej kolekcji. Jeśli potrzebujesz niestandardowego sortowania, po prostu posortuj tablicę JSON (lub DataTable) przed przekazaniem jej do procesora.

### Czy istnieje sposób, aby ukryć arkusz szablonu po przetworzeniu?

Tak. Ustaw `sm.Options.RemoveTemplateSheets = true;` przed wywołaniem `ApplyJson`. Oryginalny arkusz (indeks 0) zostanie usunięty z końcowego skoroszytu.

---

## Pełny działający przykład (wszystkie kroki razem)

Poniżej znajduje się kompletny program, który możesz skopiować‑wkleić do nowego projektu konsolowego C#. Upewnij się, że dodałeś odwołanie do pakietu NuGet `Aspose.Cells`.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

Uruchom program, otwórz `output.xlsx` i zobaczysz dynamiczne arkusze dokładnie tak, jak opisano wcześniej.

---

## Podsumowanie

Właśnie omówiliśmy **jak używać markerów** w Aspose.Cells, aby przekształcić zwykły skoroszyt w rozwiązanie master‑detail z **dynamicznym nazewnictwem arkuszy w Excelu**. Najważniejsze wnioski:

1. Umieść `${...}` smart markers tam, gdzie mają pojawić się dane.  
2. Dostarcz JSON (lub inne obsługiwane źródło danych) do `SmartMarkerProcessor`.  
3. Użyj `DetailSheetNewName`, aby procesor nadawał nowe arkusze nazwom w locie.  

Stąd możesz eksplorować bardziej zaawansowane scenariusze — dodawanie tabel, stylowanie komórek czy nawet osadzanie wykresów — wszystko sterowane

## Powiązane samouczki

- [Jak zaimplementować inteligentne markery Aspose.Cells w C# dla dynamicznego raportowania w Excelu](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Generowanie dynamicznych raportów Excel przy użyciu inteligentnych markerów Aspose.Cells .NET](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Mistrzostwo w Aspose.Cells .NET: Implementacja inteligentnych markerów i niestandardowych etykiet dla dynamicznych raportów Excel](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}