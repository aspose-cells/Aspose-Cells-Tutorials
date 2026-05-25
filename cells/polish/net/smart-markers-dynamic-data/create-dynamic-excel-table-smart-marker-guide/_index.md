---
category: general
date: 2026-05-23
description: Utwórz dynamiczną tabelę Excel przy użyciu szablonu i danych JSON. Dowiedz
  się, jak załadować szablon Excel, zautomatyzować raport Excel oraz szybko wypełnić
  Excel danymi z JSON.
draft: false
keywords:
- create dynamic excel table
- load excel template
- automate excel report
- populate excel from json
- generate excel report json
language: pl
og_description: Stwórz dynamiczną tabelę Excel w kilka minut przy użyciu szablonu
  i JSON. Ten tutorial pokazuje, jak załadować szablon Excel, zautomatyzować raport
  Excel oraz wypełnić Excel danymi z JSON.
og_title: Utwórz dynamiczną tabelę Excel – przewodnik po Smart Marker
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create dynamic excel table using a template and JSON data. Learn how
    to load excel template, automate excel report, and populate excel from json quickly.
  headline: Create Dynamic Excel Table – Smart Marker Guide
  type: TechArticle
tags:
- Excel
- Smart Markers
- JSON
- .NET
title: Utwórz dynamiczną tabelę Excel – przewodnik po Smart Marker
url: /pl/net/smart-markers-dynamic-data/create-dynamic-excel-table-smart-marker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz dynamiczną tabelę Excel – przewodnik po Smart Marker

Czy kiedykolwiek potrzebowałeś **create dynamic excel table**, które automatycznie rozszerza się dla każdego rekordu w Twoim zestawie danych? Nie jesteś jedyny. Niezależnie od tego, czy tworzysz miesięczny pulpit sprzedaży, czy pakiet faktur dla poszczególnych klientów, możliwość **populate excel from json** bez pisania niekończących się pętli może zaoszczędzić godziny.

W tym samouczku przeprowadzimy Cię przez kompletną, praktyczną rozwiązanie, które pokaże, jak **load excel template**, osadzić Smart Marker, podać mu JSON i w końcu **automate excel report**. Po zakończeniu będziesz mieć gotowy do uruchomienia projekt .NET, który generuje dopracowany skoroszyt Excel z jednego ładunku JSON.

---

## Czego będziesz potrzebować

- **Aspose.Cells for .NET** (lub dowolna biblioteka obsługująca Smart Markers). Przykład używa wersji 24.5, ale każda nowsza wersja działa.
- Visual Studio 2022 (lub Twój ulubiony IDE C#).
- Prosty plik szablonu Excel (`template.xlsx`) umieszczony w folderze, którym zarządzasz.
- Łańcuch JSON zawierający kolekcję o nazwie `Customers`.

To wszystko — bez dodatkowych usług, bez połączeń z bazą danych, tylko czysty kod.

## Krok 1: Utwórz skoroszyt szablonu – Load Excel Template

Pierwszą rzeczą, którą robimy, jest **load excel template** w pamięci. Traktuj szablon jako płótno, na którym specjalny placeholder informuje procesor, gdzie powtarzać wiersze.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook (make sure the path is correct)
Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

// Grab the first worksheet – this is where our Smart Marker lives
Worksheet worksheet = workbook.Worksheets[0];
```

> **Dlaczego to ważne:** Ładowanie szablonu raz minimalizuje operacje I/O na plikach i pozwala ponownie używać tego samego układu w wielu raportach. Izoluje także logikę Smart Marker od reszty kodu, co stanowi czyste rozdzielenie odpowiedzialności.

## Krok 2: Wstaw Smart Marker — Create Dynamic Excel Table

Teraz osadzamy **Smart Marker**, który powtórzy tabelę dla każdego wpisu w kolekcji `Customers`. Składnia `${Customers.RepeatWorksheet}` instruuje Aspose.Cells, aby sklonował cały arkusz dla każdego klienta.

```csharp
// Place the Smart Marker in cell A1 (top‑left corner)
worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");
```

> **Wskazówka:** Jeśli potrzebujesz powtarzać tylko wiersze zamiast całych arkuszy, użyj `${Customers.Repeat}` w pierwszym wierszu tabeli. Powtarzanie na poziomie arkusza jest przydatne, gdy każdy klient otrzymuje własną zakładkę.

## Krok 3: Przygotuj SmartMarkerProcessor — Automate Excel Report

Po umieszczeniu markera tworzymy `SmartMarkerProcessor`. Ten obiekt koordynuje powiązanie danych między JSON a szablonem Excel.

```csharp
// Initialize the processor with the workbook that contains the marker
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

Procesor jest lekki; możesz go ponownie używać dla wielu ładunków JSON, jeśli chcesz.

## Krok 4: Dostarcz dane JSON — Populate Excel from JSON

Tutaj dzieje się magia. Dostarczamy łańcuch JSON zawierający tablicę klientów. Każdy klient może mieć pola takie jak `Name`, `Email` i `Total`.

```csharp
// Sample JSON data – in a real scenario you might read this from a file or API
string customersJson = @"
{
  ""Customers"": [
    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
  ]
}";

// Apply the JSON to the processor – this populates the workbook
processor.ApplyJson(customersJson);
```

> **Dlaczego JSON?** JSON jest niezależny od języka i łatwy do generowania z API, baz danych lub nawet ręcznego wprowadzania. Użycie `ApplyJson` oznacza, że nie musisz ręcznie mapować obiektów; procesor wykonuje ciężką pracę.

## Krok 5: Zapisz wynik — Generate Excel Report JSON

Na koniec zapisujemy wypełniony skoroszyt na dysku. Plik wyjściowy zawiera teraz osobny arkusz dla każdego klienta, wypełniony danymi z naszego JSON.

```csharp
// Save the filled workbook – choose a path that makes sense for your app
workbook.Save(@"C:\Reports\output.xlsx");
```

### Oczekiwany wynik

- **output.xlsx** będzie zawierał trzy arkusze nazwane `Sheet1`, `Sheet2`, `Sheet3` (lub według konwencji nazewnictwa używanej w Twoim szablonie).
- Każdy arkusz wyświetli wartości `Name`, `Email` i `Total` dla jednego klienta.
- Układ zaprojektowany w `template.xlsx` (nagłówki, stylowanie, formuły) zostanie zachowany we wszystkich wygenerowanych arkuszach.

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Skopiuj i wklej go do aplikacji konsolowej, dostosuj ścieżki plików i naciśnij **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace DynamicExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            string templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert the Smart Marker that repeats the worksheet per customer
            worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");

            // 3️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // 4️⃣ JSON data containing a collection of customers
            string customersJson = @"
            {
                ""Customers"": [
                    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
                    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
                    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
                ]
            }";

            // Apply the JSON – this populates the workbook dynamically
            processor.ApplyJson(customersJson);

            // 5️⃣ Save the generated report
            string outputPath = @"C:\Reports\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Dynamic Excel report generated at: {outputPath}");
        }
    }
}
```

Uruchom program, otwórz `output.xlsx`, a zobaczysz **create dynamic excel table** w działaniu — każdy klient otrzymuje własny arkusz, w pełni sformatowany zgodnie z Twoim projektem.

## Częste pytania i przypadki brzegowe

| Question | Answer |
|----------|--------|
| *Co jeśli mój JSON ma zagnieżdżone obiekty?* | Smart Markers obsługują notację kropkową (`${Customers.Address.City}`), pod warunkiem że hierarchia JSON jest zgodna. |
| *Czy mogę nazwać wygenerowane arkusze po nazwie klienta?* | Tak — dodaj marker taki jak `${Customers.Name}` w komórce nazwy arkusza lub użyj `processor.ApplyJson(customersJson, \"Customers\")` z wzorcem nazewnictwa. |
| *Co z dużymi zestawami danych (10 k+ wierszy)?* | Procesor strumieniuje dane efektywnie, ale monitoruj zużycie pamięci. Rozważ podzielenie raportu na wiele plików, jeśli napotkasz limity wydajności. |
| *Czy potrzebuję licencji na Aspose.Cells?* | Darmowa wersja ewaluacyjna działa do testów, ale wersja licencjonowana usuwa znaki wodne ewaluacji i zapewnia pełne funkcje. |
| *Czy mogę używać tego podejścia z .NET Core?* | Oczywiście — Aspose.Cells obsługuje .NET 6/7/8. Wystarczy odwołać się do pakietu NuGet, a kod pozostaje taki sam. |

## Wskazówki dla implementacji gotowych do produkcji

- **Validate JSON** przed przekazaniem go do `ApplyJson`. Nieprawidłowy ładunek spowoduje wyrzucenie `JsonParseException`.
- **Cache the template** jeśli generujesz wiele raportów w krótkim czasie; wielokrotne ładowanie z dysku jest niepotrzebnym I/O.
- **Lock the workbook** podczas przetwarzania, jeśli uruchamiasz to w wielowątkowej usłudze webowej, aby uniknąć warunków wyścigu.
- **Add error handling** wokół `workbook.Save`, aby elegancko obsłużyć problemy z uprawnieniami lub zablokowanymi plikami.
- **Customize styling** w szablonie (formatowanie warunkowe, formuły), aby wygenerowane arkusze zachowały logikę biznesową bez dodatkowego kodu.

## Zakończenie

Masz teraz solidny, kompleksowy wzorzec, jak **create dynamic excel table** przy użyciu szablonu, Smart Markers i danych JSON. Dzięki **load excel template**, wstawieniu markera powtarzania i **populate excel from json**, możesz **automate excel report** generowanie przy użyciu zaledwie kilku linii C#.

Kolejne kroki? Spróbuj dodać wykresy odwołujące się do dynamicznych tabel lub wyeksportować ten sam JSON do PDF przy użyciu Aspose.Words. Możesz także poeksperymentować z **generate excel report json** z zapytania do bazy danych, aby zamknąć pętlę.

## Powiązane samouczki

- [Utwórz tabelę przestawną w Excelu przy użyciu Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Utwórz dynamiczne wykresy liniowe w Excelu przy użyciu Aspose.Cells for .NET: przewodnik krok po kroku](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Jak tworzyć pola wyboru w Excelu przy użyciu Aspose.Cells for .NET | Samouczek walidacji danych](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}