---
category: general
date: 2026-03-22
description: Jak generować raport Excel w C# przy użyciu szablonu master‑detail. Dowiedz
  się, jak szybko wypełniać szablon Excel w C#, używając SmartMarker do powtarzalnych
  arkuszy.
draft: false
keywords:
- how to generate excel report
- populate excel template c#
- excel smartmarker c#
- master detail excel c#
- c# excel automation
language: pl
og_description: Jak wygenerować raport Excel w C# przy użyciu szablonu wielokrotnego
  użytku. Ten przewodnik krok po kroku pokazuje, jak wypełnić szablon Excel w C# danymi
  master‑detail.
og_title: Jak wygenerować raport Excel w C# – kompletny samouczek SmartMarker
tags:
- Excel
- C#
- SmartMarker
- Reporting
title: Jak wygenerować raport Excel w C# – pełny przewodnik z użyciem SmartMarker
url: /pl/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wygenerować raport Excel w C# – Kompletny przewodnik z użyciem SmartMarker

Zastanawiałeś się kiedyś **jak wygenerować raport Excel** w C# bez pisania niekończącego się kodu komórka‑po‑komórce? Nie jesteś sam. Większość deweloperów napotyka problem, gdy potrzebny jest elegancki raport wielo‑arkuszowy odzwierciedlający relacje master‑detail — pomyśl o zamówieniach i pozycjach zamówień — a nie chcą przy tym wymyślać koła od nowa przy każdym projekcie.

Dobre wieści? Dzięki gotowemu szablonowi Excel oraz silnikowi **SmartMarker** z Aspose.Cells, możesz **populate Excel template C#** w zaledwie kilku linijkach. W tym tutorialu przejdziemy przez scenariusz z życia wzięty, wyjaśnimy, dlaczego każdy krok ma znaczenie, i dostarczymy kompletny, gotowy do uruchomienia przykład, który możesz skopiować‑wkleić już dziś.

> **Co otrzymasz:** raport Excel master‑detail, w którym każde zamówienie generuje własny arkusz, wszystko napędzane zwykłymi obiektami C#. Bez ręcznego iterowania po komórkach, bez kruchych formuł — po prostu czysty, łatwy w utrzymaniu kod.

---

## Prerequisites

Zanim zaczniemy, upewnij się, że masz:

- **.NET 6.0** (lub nowszy) zainstalowany – kod jest skierowany do .NET 6, ale działa także na .NET Framework 4.7+.
- **Aspose.Cells for .NET** pakiet NuGet (`Install-Package Aspose.Cells`) – dostarcza klasy `Workbook`, `SmartMarkerProcessor` i powiązane.
- Plik Excel o nazwie **MasterDetailTemplate.xlsx** umieszczony w `YOUR_DIRECTORY`. Powinien zawierać blok SmartMarker taki jak `{{Orders.OrderId}}` w pierwszym arkuszu oraz zagnieżdżony blok `{{Orders.Items.Prod}}` dla pozycji.
- Podstawową znajomość anonimowych typów w C# – użyjemy ich do modelowania zamówień i pozycji.

Jeśli któryś z tych elementów jest Ci nieznany, nie martw się. Później wspomnimy o alternatywach (np. użycie EPPlus), ale podstawowa koncepcja pozostaje ta sama.

---

## Krok 1: Załaduj szablon Excel zawierający bloki SmartMarker

Pierwszą rzeczą, którą robimy, jest otwarcie pliku szablonu. Traktuj szablon jako szkielet; SmartMarker później wypełni go rzeczywistymi danymi.

```csharp
using Aspose.Cells;

// Load the template containing SmartMarker tags
var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Dlaczego to ważne:** Oddzielenie układu (szablonu) od danych (obiektów C#) sprawia, że projektanci i programiści są zadowoleni. Projektanci mogą modyfikować czcionki, kolory czy formuły bez ingerencji w kod.

---

## Krok 2: Zbuduj źródło danych master‑detail

Następnie tworzymy dane, które wypełnią szablon. Dla typowego raportu zamówień masz kolekcję zamówień, z których każde ma własną kolekcję pozycji.

```csharp
// Master‑detail data: a list of orders, each with a list of items
var masterDetailData = new
{
    Orders = new[]
    {
        new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Prod = "A", Qty = 2 },
                new { Prod = "B", Qty = 1 }
            }
        },
        new
        {
            OrderId = 2,
            Items = new[]
            {
                new { Prod = "C", Qty = 5 }
            }
        }
    }
};
```

> **Pro tip:** Używaj typów silnie typowanych zamiast anonimowych, jeśli potrzebujesz ich ponownego użycia w wielu raportach. Podejście anonimowe utrzymuje przykład zwięzłym.

**Dlaczego to ważne:** SmartMarker działa poprzez dopasowywanie nazw właściwości (`Orders`, `OrderId`, `Items`, `Prod`, `Qty`) do znaczników w szablonie. Hierarchia musi się zgadzać dokładnie, w przeciwnym razie silnik pominie te sekcje.

---

## Krok 3: Powiedz SmartMarkerowi, aby utworzył nowy arkusz dla każdego rekordu master

Domyślnie SmartMarker zapisuje wszystkie wiersze w jednym arkuszu. Chcemy, aby każde zamówienie znajdowało się w osobnym arkuszu, co jest idealne do późniejszego drukowania lub wysyłania PDF‑ów per zamówienie.

```csharp
// Enable a separate sheet for each master (order) record
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableRepeatingSheet = true // each Order gets its own sheet
};
```

**Dlaczego to ważne:** `EnableRepeatingSheet` eliminuje potrzebę ręcznego klonowania arkuszy. Silnik kopiuje oryginalny arkusz, wstrzykuje dane zamówienia i automatycznie zmienia nazwę arkusza (zazwyczaj używając wartości z pierwszej kolumny).

---

## Krok 4: Przetwórz szablon przy użyciu danych

Teraz łączymy wszystko razem. `SmartMarkerProcessor` przechodzi przez skoroszyt, zamienia znaczniki i tworzy nowe arkusze zgodnie z instrukcjami.

```csharp
// Apply the data to the workbook
workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);
```

**Dlaczego to ważne:** Ta pojedyncza linijka wykonuje najcięższą pracę — parsowanie szablonu, iterowanie po kolekcjach i obsługę zagnieżdżonych tabel. To serce **populate Excel template C#** bez żadnych ręcznych pętli.

---

## Krok 5: Zapisz gotowy raport

Na koniec zapisujemy wypełniony skoroszyt na dysku. Możesz także przesłać go bezpośrednio jako strumień w odpowiedzi HTTP dla aplikacji webowych.

```csharp
// Save the generated report
workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");
```

**Dlaczego to ważne:** Zapis do pliku daje nam namacalny artefakt, który można otworzyć w Excelu, udostępnić interesariuszom lub przekazać do dalszych procesów, np. konwersji do PDF.

---

## Pełny działający przykład (Gotowy do kopiowania)

Poniżej znajduje się kompletny program, łącznie z dyrektywami `using` i metodą `Main`. Wstaw go do aplikacji konsolowej, dostosuj ścieżki plików i uruchom.

```csharp
using System;
using Aspose.Cells;

namespace ExcelReportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template
            var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

            // 2️⃣ Build master‑detail data
            var masterDetailData = new
            {
                Orders = new[]
                {
                    new
                    {
                        OrderId = 1,
                        Items = new[]
                        {
                            new { Prod = "A", Qty = 2 },
                            new { Prod = "B", Qty = 1 }
                        }
                    },
                    new
                    {
                        OrderId = 2,
                        Items = new[]
                        {
                            new { Prod = "C", Qty = 5 }
                        }
                    }
                }
            };

            // 3️⃣ Enable a new sheet per order
            var smartMarkerOptions = new SmartMarkerOptions
            {
                EnableRepeatingSheet = true
            };

            // 4️⃣ Process the template with data
            workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);

            // 5️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");

            Console.WriteLine("Excel report generated successfully!");
        }
    }
}
```

### Oczekiwany wynik

Po otwarciu `MasterDetailResult.xlsx` zobaczysz:

- **Arkusz „Order_1”** – zawiera nagłówek zamówienia 1 oraz dwa wiersze dla produktów A i B.
- **Arkusz „Order_2”** – zawiera nagłówek zamówienia 2 oraz pojedynczy wiersz dla produktu C.
- Wszystkie formuły, formatowanie i wykresy z oryginalnego szablonu pozostają nienaruszone.

![Excel report with separate sheets for each order – example of populated workbook](/images/excel-report-example.png "Generated Excel report with master‑detail data")

*Image alt text: generated Excel report with separate sheets for each order, showing how to generate Excel report using C# and SmartMarker.*

---

## Często zadawane pytania i przypadki brzegowe

### Co zrobić, jeśli potrzebuję statycznego arkusza (np. podsumowania) obok powtarzających się arkuszy?

Ustaw `EnableRepeatingSheet = true` **tylko** na arkuszu zawierającym blok master. Inne arkusze pozostaną nietknięte, więc możesz zachować stronę podsumowania w oryginalnym szablonie.

### Czy mogę użyć DataTable zamiast anonimowych obiektów?

Oczywiście. SmartMarker współpracuje z każdym obiektem implementującym `IEnumerable`. Po prostu zamień anonimowy typ na `DataTable` i upewnij się, że nazwy kolumn pasują do znaczników.

```csharp
DataTable ordersTable = GetOrdersFromDatabase();
var data = new { Orders = ordersTable };
```

### Jak zmienić konwencję nazewnictwa generowanych arkuszy?

Zaimplementuj własny interfejs `ISmartMarkerSheetNaming` (lub manipuluj `workbook.Worksheets` po przetworzeniu). Większość deweloperów po prostu zmienia nazwę arkusza na podstawie wartości komórki:

```csharp
foreach (var sheet in workbook.Worksheets)
{
    sheet.Name = $"Order_{sheet.Cells["A1"].StringValue}";
}
```

### Co jeśli mój szablon używa innej składni placeholderów?

SmartMarker pozwala na niestandardowe delimitery poprzez `SmartMarkerOptions`. Na przykład, aby używać `<< >>` zamiast `{{ }}`:

```csharp
smartMarkerOptions.StartTag = "<<";
smartMarkerOptions.EndTag = ">>";
```

---

## Wskazówki przy skalowaniu tego podejścia

- **Cache'uj szablon** w pamięci, jeśli generujesz wiele raportów na żądanie; wczytywanie z dysku przy każdym wywołaniu zwiększa opóźnienie.
- **Połącz z konwersją do PDF** (`workbook.Save("report.pdf", SaveFormat.Pdf)`) dla wyjść przyjaznych e‑mailom.
- **Parametryzuj ścieżki plików** przy pomocy plików konfiguracyjnych lub zmiennych środowiskowych, aby rozwiązanie było przenośne między dev, test i prod.
- **Testuj warstwę danych** oddzielnie; SmartMarker jest deterministyczny, więc wystarczy zweryfikować, że dostarczane dane odpowiadają oczekiwanej schemacie.

---

## Zakończenie

Omówiliśmy **jak wygenerować raport Excel** w C# od początku do końca, od załadowania szablonu z włączonym SmartMarker po zapis wielo‑arkuszowego skoroszytu odzwierciedlającego relacje master‑detail. Dzięki **populate Excel template C#** w kilku linijkach kodu unikasz kruchej logiki komórka‑po‑komórce i dajesz projektantom swobodę kształtowania ostatecznego wyglądu.

Następnie możesz zbadać:

- Użycie **populate Excel template C#** z wykresami, które automatycznie aktualizują się w każdym arkuszu.
- Integrację **excel smartmarker c#** z ASP.NET Core, aby strumieniować raporty bezpośrednio do przeglądarek.
- Automatyzację **c# excel automation** pipeline’ów, które pobierają dane z API lub baz danych.

Spróbuj, zmodyfikuj szablon i zobacz, jak szybko możesz przekształcić surowe dane w elegancki raport Excel. Masz pytania lub ciekawy przypadek użycia? zostaw komentarz poniżej — happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}