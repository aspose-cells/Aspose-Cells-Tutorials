---
category: general
date: 2026-07-03
description: Utwórz skoroszyt master‑detail przy użyciu inteligentnego znacznika Aspose.Cells
  – automatyzuj tworzenie arkuszy Excel bez wysiłku i zwiększaj wydajność.
draft: false
keywords:
- create master detail workbook
- automate excel sheet creation
- aspose.cells smart marker
language: pl
og_description: Utwórz skoroszyt master‑detail przy użyciu inteligentnego znacznika
  Aspose.Cells. Dowiedz się, jak zautomatyzować tworzenie arkuszy Excel w kilka minut.
og_title: Utwórz skoroszyt Master‑Detail – Przewodnik po inteligentnych znacznikach
  Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Create master detail workbook using Aspose.Cells smart marker – automate
    Excel sheet creation effortlessly and boost productivity.
  headline: Create Master Detail Workbook with Aspose.Cells Smart Marker
  type: TechArticle
tags:
- Aspose.Cells
- Excel
- SmartMarker
- C#
title: Utwórz skoroszyt Master‑Detail przy użyciu Aspose.Cells Smart Marker
url: /pl/net/smart-markers-dynamic-data/create-master-detail-workbook-with-aspose-cells-smart-marker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie skoroszytu Master‑Detail przy użyciu Aspose.Cells Smart Marker

Czy kiedykolwiek potrzebowałeś **utworzyć skoroszyt master‑detail**, ale utknąłeś w miejscu, w którym trzeba duplikować arkusze dla każdego wiersza danych? Nie jesteś sam. W wielu scenariuszach raportowych kończysz pisząc powtarzalny VBA lub ręcznie kopiując‑wklejając, co jest podatne na błędy i czasochłonne.  

Dobrą wiadomością jest to, że technologia smart marker w Aspose.Cells pozwala **zautomatyzować tworzenie arkuszy Excel** przy użyciu zaledwie kilku linii kodu C#. W tym samouczku przeprowadzimy Cię przez cały proces — od wczytania szablonu skoroszytu, przez generowanie arkuszy szczegółowych, po zapisanie finalnego pliku — abyś mógł skupić się na logice biznesowej, a nie na ręcznym manipulowaniu interfejsem Excel.

Po przeczytaniu tego przewodnika będziesz dokładnie wiedział, jak:

* Załadować istniejący skoroszyt zawierający układ smart markerów master‑detail.  
* Podłączyć dowolne źródło danych .NET (DataTable, List<T> itp.) do procesora.  
* Zdefiniować konwencję nazewnictwa nowo tworzonych arkuszy szczegółowych.  
* Uruchomić silnik smart‑marker i wygenerować dopracowany skoroszyt master‑detail gotowy do dystrybucji.

Bez dodatkowych narzędzi, bez makr — czysty kod działający na .NET 6 (lub nowszym). Zanurzmy się.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

| Wymaganie | Dlaczego jest ważne |
|-----------|----------------------|
| **Aspose.Cells for .NET** (najnowsza wersja) | Dostarcza klasę `SmartMarkerProcessor` używaną w całym przykładzie. |
| **.NET 6 SDK** (lub nowszy) | Przykład jest napisany w nowoczesnym C#; starsze frameworki będą działać po drobnych modyfikacjach. |
| **Szablon Excel** (`input.xlsx`) zawierający smart marker taki jak `&=MasterData!A1` w arkuszu master oraz placeholder szczegółowy np. `&=DetailData!A2` w ukrytym arkuszu szablonu. | Procesor zamienia te znaczniki na rzeczywiste dane w czasie wykonywania. |
| **Źródło danych** (np. `DataTable`, `List<Customer>`) | To miejsce, z którego pochodzą rzeczywiste wiersze dla master i detail. |

Jeśli którekolwiek z powyższych brakuje, pobierz Aspose.Cells z NuGet (`Install-Package Aspose.Cells`) i utwórz prosty plik Excel ze wskazanymi znacznikami.

## Krok 1: Konfiguracja projektu i import przestrzeni nazw

Najpierw utwórz aplikację konsolową (lub dowolny projekt .NET) i dodaj niezbędne przestrzenie nazw. Ten krok jest trywialny, ale kluczowy — bez właściwych dyrektyw `using` kompilator zgłosi błąd.

```csharp
using System;
using System.Data;               // For DataTable example
using Aspose.Cells;              // Core Aspose.Cells API
using Aspose.Cells.SmartMarkers; // Smart marker processor
```

*Dlaczego to ważne:* `Aspose.Cells` zapewnia możliwości manipulacji skoroszytem, natomiast `Aspose.Cells.SmartMarkers` zawiera silnik parsujący i rozwijający znaczniki.

## Krok 2: Wczytanie szablonu skoroszytu

Szablon skoroszytu (`input.xlsx`) przechowuje układ master‑detail z placeholderami. Wczytanie go to jednowierszowy kod, ale dodatkowo otoczymy to blokiem `try/catch`, aby od razu wykryć problemy z plikiem.

```csharp
Workbook wb;
try
{
    wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load template workbook: {ex.Message}");
    return;
}
```

*Wskazówka:* Trzymaj szablon w folderze tylko do odczytu lub osadź go jako zasób, jeśli planujesz dystrybuować plik wykonywalny.

## Krok 3: Przygotowanie źródła danych

Smart markery Aspose.Cells mogą konsumować praktycznie dowolny obiekt enumerowalny. Dla ilustracji zbudujemy `DataTable`, który symuluje relację master‑detail: tabela `Customers` (master) oraz tabela `Orders` (detail). `SmartMarkerProcessor` automatycznie połączy wiersze na podstawie wspólnego klucza.

```csharp
// Master table
DataTable customers = new DataTable("Customers");
customers.Columns.Add("CustomerID", typeof(int));
customers.Columns.Add("CompanyName", typeof(string));
customers.Rows.Add(1, "Acme Corp");
customers.Rows.Add(2, "Globex Ltd");

// Detail table
DataTable orders = new DataTable("Orders");
orders.Columns.Add("CustomerID", typeof(int));
orders.Columns.Add("OrderID", typeof(int));
orders.Columns.Add("Product", typeof(string));
orders.Columns.Add("Quantity", typeof(int));
orders.Rows.Add(1, 101, "Widget", 5);
orders.Rows.Add(1, 102, "Gadget", 2);
orders.Rows.Add(2, 201, "Doohickey", 7);

// Combine into a DataSet (the processor can accept DataSet directly)
DataSet ds = new DataSet();
ds.Tables.Add(customers);
ds.Tables.Add(orders);

// The object we pass to the processor – could also be a List<T> or custom collection
object dataSource = ds;
```

*Dlaczego to ważne:* Korzystając z `DataSet`, procesor może automatycznie rozwiązywać relacje (np. wiersze `Orders`, których `CustomerID` pasuje do bieżącego wiersza master). Jeśli masz inne źródło (JSON, EF Core itp.), po prostu zamień `DataSet` na własny obiekt.

## Krok 4: Konfiguracja SmartMarkerProcessor

Teraz tworzymy instancję procesora i określamy, jak mają być nazywane nowo generowane arkusze szczegółowe. Placeholder `{0}` zostanie zastąpiony kolejnym indeksem zaczynającym się od 1.

```csharp
SmartMarkerProcessor sm = new SmartMarkerProcessor
{
    // Naming pattern for detail sheets: Detail_1, Detail_2, …
    DetailSheetNewName = "Detail_{0}"
};
```

*Uwaga o przypadkach brzegowych:* Jeśli Twój skoroszyt już zawiera arkusze o nazwach `Detail_1`, `Detail_2` itp., procesor automatycznie pominie te nazwy, aby uniknąć kolizji.

## Krok 5: Przetworzenie skoroszytu

Po podłączeniu wszystkiego, właściwa praca odbywa się w jednym wywołaniu `Process`. Metoda ta skanuje skoroszyt w poszukiwaniu smart markerów, klonuje arkusz szablonu detail dla każdego wiersza master i wypełnia komórki danymi z `dataSource`.

```csharp
try
{
    sm.Process(wb, dataSource);
}
catch (Exception ex)
{
    Console.WriteLine($"Smart marker processing failed: {ex.Message}");
    return;
}
```

*Co się dzieje „pod maską”?*  
- Procesor odczytuje arkusz master, znajduje znacznik `&=Customers!` i tworzy nowy arkusz dla każdego klienta.  
- Dla każdego nowego arkusza szuka znaczników `&=Orders!`, filtruje tabelę `Orders` po `CustomerID` i wypełnia wiersze.  
- Wzorzec nazewnictwa ustawiony wcześniej zapewnia, że każdy arkusz otrzymuje unikalną, przewidywalną nazwę.

## Krok 6: Zapisanie wynikowego skoroszytu

Na koniec zapisujemy zaktualizowany skoroszyt na dysk. Możesz wybrać dowolny format obsługiwany przez Aspose.Cells (`.xlsx`, `.xls`, `.csv` itp.). Tutaj pozostajemy przy nowoczesnym `.xlsx`.

```csharp
string outputPath = "YOUR_DIRECTORY/output.xlsx";
wb.Save(outputPath);
Console.WriteLine($"Workbook saved successfully to {outputPath}");
```

*Wskazówka:* Jeśli potrzebujesz strumieniowo przesłać plik bezpośrednio w odpowiedzi webowej, użyj przeciążenia `wb.Save(Stream, SaveFormat.Xlsx)`.

## Pełny działający przykład

Łącząc wszystkie elementy, oto samodzielny program konsolowy, który możesz skopiować‑wkleić i uruchomić (wystarczy podmienić `YOUR_DIRECTORY` na rzeczywistą ścieżkę).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace MasterDetailDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            Workbook wb;
            try
            {
                wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to load template: {ex.Message}");
                return;
            }

            // 2️⃣ Build the data source (DataSet with master & detail tables)
            DataTable customers = new DataTable("Customers");
            customers.Columns.Add("CustomerID", typeof(int));
            customers.Columns.Add("CompanyName", typeof(string));
            customers.Rows.Add(1, "Acme Corp");
            customers.Rows.Add(2, "Globex Ltd");

            DataTable orders = new DataTable("Orders");
            orders.Columns.Add("CustomerID", typeof(int));
            orders.Columns.Add("OrderID", typeof(int));
            orders.Columns.Add("Product", typeof(string));
            orders.Columns.Add("Quantity", typeof(int));
            orders.Rows.Add(1, 101, "Widget", 5);
            orders.Rows.Add(1, 102, "Gadget", 2);
            orders.Rows.Add(2, 201, "Doohickey", 7);

            DataSet ds = new DataSet();
            ds.Tables.Add(customers);
            ds.Tables.Add(orders);
            object dataSource = ds;

            // 3️⃣ Configure the processor (detail sheet naming)
            SmartMarkerProcessor sm = new SmartMarkerProcessor
            {
                DetailSheetNewName = "Detail_{0}"
            };

            // 4️⃣ Run the smart‑marker engine
            try
            {
                sm.Process(wb, dataSource);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Processing error: {ex.Message}");
                return;
            }

            // 5️⃣ Save the output workbook
            string outPath = "YOUR_DIRECTORY/output.xlsx";
            wb.Save(outPath);
            Console.WriteLine($"Successfully created master‑detail workbook at {outPath}");
        }
    }
}
```

**Oczekiwany wynik:**  
- `output.xlsx` zawiera oryginalny arkusz master oraz dwa nowe arkusze detail o nazwach `Detail_1` i `Detail_2`.  
- Każdy arkusz detail wymienia zamówienia należące do odpowiedniego klienta, w pełni wypełnione bez żadnego ręcznego kopiowania‑wklejania.

## Często zadawane pytania i przypadki brzegowe

| Pytanie | Odpowiedź |
|----------|-----------|
| *Co zrobić, jeśli mój szablon już ma arkusz o nazwie `Detail_1`?* | Procesor automatycznie zwiększa indeks (`Detail_2`, `Detail_3`, …), aż znajdzie nieużywaną nazwę. |
| *Czy mogę kontrolować kolejność generowanych arkuszy?* | Tak — ustaw `sm.DetailSheetNewName`, aby zawierał prefiks sortujący alfabetycznie, np. `"01_Detail_{0}"`. |
| *Czy muszę zwalniać obiekt `Workbook`?* | `Workbook` implementuje `IDisposable`; jeśli martwisz się zasobami niezarządzanymi, otocz go blokiem `using`. |
| *Czy można użyć łańcucha JSON jako źródła danych?* | Najpierw skonwertuj JSON do `DataSet` lub listy POCO; procesor działa z dowolnym obiektem enumerowalnym. |
| *Jak radzić sobie z dużymi zestawami danych (10 000+ wierszy)?* | Aspose.Cells strumieniuje dane efektywnie, ale warto zwiększyć `Workbook.Settings.MemorySetting` do `MemorySetting.MemoryPreference` dla lepszej wydajności. |

## Podsumowanie


## Co warto się nauczyć dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz szczegółowe wyjaśnienia, pomagające opanować dodatkowe funkcje API i eksplorować alternatywne podejścia w własnych projektach.

- [Tworzenie skoroszytu Excel przy użyciu Aspose.Cells w Javie: przewodnik krok po kroku](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Zaawansowana manipulacja plikami Excel przy użyciu Aspose.Cells dla Javy | Przewodnik po operacjach na skoroszytach](/cells/english/java/workbook-operations/master-excel-manipulation-aspose-cells-java/)
- [Automatyzacja Excel z Aspose.Cells Java: tworzenie skoroszytu master oraz kontrola widoczności kolumn/wierszy](/cells/english/java/workbook-operations/excel-automation-aspose-cells-java-workbook-visibility/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}