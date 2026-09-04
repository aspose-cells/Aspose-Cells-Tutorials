---
category: general
date: 2026-02-23
description: Automatycznie nazwij arkusze Excel i dowiedz się, jak generować arkusze
  automatycznie przy użyciu SmartMarkers. Przewodnik krok po kroku w C# dla dynamicznych
  skoroszytów.
draft: false
keywords:
- auto name excel sheets
- how to generate sheets
- Aspose.Cells SmartMarkers
- dynamic worksheet naming
- C# Excel automation
language: pl
og_description: Automatycznie nazwij arkusze Excel od razu. Dowiedz się, jak generować
  arkusze za pomocą SmartMarkers w C# – kompletny, gotowy do uruchomienia przykład.
og_title: Automatyczne nazewnictwo arkuszy Excel – szybki samouczek C#
tags:
- C#
- Excel
- Aspose.Cells
title: Automatyczne nadawanie nazw arkuszom Excel – łatwy sposób na generowanie arkuszy
url: /pl/net/smart-markers-dynamic-data/auto-name-excel-sheets-easy-way-to-generate-sheets/
---

". It seems cut off. Keep as is.

Now produce final content.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatyczne nadawanie nazw arkuszom Excel – Pełny samouczek C#

Zastanawiałeś się kiedyś, jak **automatycznie nadawać nazwy arkuszom Excel** bez pisania pętli, która ręcznie zmienia nazwy każdej zakładki? Nie jesteś jedyny. W wielu projektach raportowych liczba arkuszy rośnie w czasie wykonywania, a utrzymanie nazw w porządku staje się problemem. Dobra wiadomość? Dzięki **SmartMarkers** z Aspose.Cells możesz pozwolić bibliotece zająć się nadawaniem nazw, a także umożliwia **jak generować arkusze** w locie.

W tym przewodniku przejdziemy przez realistyczny scenariusz: tworzenie skoroszytu, konfigurowanie opcji SmartMarker tak, aby arkusze szczegółowe były automatycznie nazwane *Detail*, *Detail1*, *Detail2*, …, a następnie weryfikację, że arkusze pojawiają się zgodnie z oczekiwaniami. Po zakończeniu będziesz mieć samodzielne, gotowe do skopiowania rozwiązanie, które możesz dostosować do każdego projektu wymagającego dynamicznego tworzenia arkuszy.

---

## Czego będziesz potrzebować

Zanim zaczniemy, upewnij się, że masz:

- **.NET 6+** (lub .NET Framework 4.6.2+). Kod działa na każdym nowoczesnym środowisku uruchomieniowym.
- **Aspose.Cells for .NET** – pakiet NuGet `Install-Package Aspose.Cells`.
- Podstawowy projekt C# (aplikacja konsolowa, WinForms lub ASP.NET – ten sam kod działa wszędzie).
- Visual Studio, VS Code lub ulubione IDE.

Bez dodatkowego interopu Excel, bez COM, tylko czysty kod zarządzany.

---

## Krok 1: Automatyczne nadawanie nazw arkuszom Excel przy użyciu SmartMarkers

Pierwszą rzeczą, którą musisz zrobić, jest poinformowanie Aspose.Cells, jaką nazwę bazową chcesz dla automatycznie tworzonych arkuszy szczegółowych. Robi się to za pomocą klasy `SmartMarkerOptions`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;   // for SmartMarkers
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook that will hold the master sheet.
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Master";

        // -----------------------------------------------------------
        // Step 1: Configure SmartMarker options – set the base name
        // -----------------------------------------------------------
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // This tells SmartMarkers to create sheets named Detail, Detail1, Detail2, …
            DetailSheetNewName = "Detail"
        };
```

**Dlaczego to ważne:** Ustawiając `DetailSheetNewName`, przekazujesz logikę nadawania nazw bibliotece. Nie musisz pisać pętli `for`, która sprawdza istniejące nazwy arkuszy i zwiększa licznik – API robi to za Ciebie, gwarantując unikalne nazwy nawet wtedy, gdy źródło danych zawiera dziesiątki wierszy.

---

## Krok 2: Przygotowanie źródła danych

SmartMarkers działają z dowolną kolekcją `IEnumerable`, `DataTable` lub nawet zwykłą listą obiektów. W tym demo użyjemy prostej listy obiektów reprezentujących szczegóły zamówień.

```csharp
        // -----------------------------------------------------------
        // Step 2: Build a sample data source
        // -----------------------------------------------------------
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop", Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",   Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard",Qty = 3, Price =  45.50 }
        };
```

**Dlaczego to ważne:** Źródło danych decyduje, ile arkuszy szczegółowych zostanie wygenerowanych. Każdy element kolekcji tworzy nowy arkusz na podstawie szablonu SmartMarker, który dodamy w następnym kroku.

---

## Krok 3: Wstawienie szablonu SmartMarker do arkusza głównego

Szablon SmartMarker to po prostu komórka (lub zakres) zawierająca znaczniki zastępcze. Gdy wywołana zostanie metoda `Apply`, znaczniki zostają zastąpione rzeczywistymi danymi, a dla każdego wiersza tworzony jest nowy arkusz.

```csharp
        // -----------------------------------------------------------
        // Step 3: Add a SmartMarker template to the master sheet
        // -----------------------------------------------------------
        // Put a header row
        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Product");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["D1"].PutValue("Unit Price");

        // Insert SmartMarker placeholders starting at row 2
        ws.Cells["A2"].PutValue("&=orders.OrderId");
        ws.Cells["B2"].PutValue("&=orders.Product");
        ws.Cells["C2"].PutValue("&=orders.Qty");
        ws.Cells["D2"].PutValue("&=orders.Price");
```

**Dlaczego to ważne:** Składnia `&=` mówi SmartMarkers, aby „pobrały wartość ze źródła danych”. Gdy uruchomisz `Apply`, Aspose.Cells skopiuje ten wiersz do nowego arkusza dla każdego elementu w `orders`, automatycznie nadając arkuszowi nazwę zgodnie z wcześniej ustawioną opcją.

---

## Krok 4: Zastosowanie opcji SmartMarker – tutaj arkusze są automatycznie nazywane

Teraz następuje moment, w którym biblioteka wykonuje ciężką pracę. Wywołanie `Apply` odczytuje szablon, tworzy arkusze szczegółowe i nadaje im nazwy według `DetailSheetNewName`.

```csharp
        // -----------------------------------------------------------
        // Step 4: Apply SmartMarker – auto name excel sheets happens here
        // -----------------------------------------------------------
        ws.SmartMarkers.Apply(smartMarkerOptions, new { orders });

        // Save the workbook to verify the result
        wb.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Workbook saved. Open AutoNamedSheets.xlsx to see the result.");
    }
}
```

**Dlaczego to ważne:** Metoda `Apply` nie tylko wypełnia dane, ale także respektuje podany wzorzec nazewnictwa. Jeśli otworzysz *AutoNamedSheets.xlsx*, zobaczysz:

- **Detail** – zawiera pierwsze zamówienie.  
- **Detail1** – drugie zamówienie.  
- **Detail2** – trzecie zamówienie.

Bez ręcznego zmieniania nazw.

---

## Krok 5: Weryfikacja wyniku – jak generować arkusze poprawnie

Po uruchomieniu programu otwórz wygenerowany plik. Powinieneś zobaczyć trzy nowe arkusze nazwane dokładnie tak, jak opisano powyżej. To dowód, że udało Ci się opanować **jak generować arkusze** automatycznie.

> **Pro tip:** Jeśli potrzebujesz własnego przyrostka (np. „_Report”), po prostu ustaw `DetailSheetNewName = "Detail_Report"` i biblioteka doda numery po ciągu bazowym.

---

## Przypadki brzegowe i najczęstsze pytania

### Co jeśli nazwa bazowa już istnieje?

Aspose.Cells sprawdza istniejące nazwy arkuszy i dopisuje kolejny numer, aż znajdzie unikalną nazwę. Dlatego nawet jeśli w skoroszycie już istnieje arkusz o nazwie *Detail*, kolejny wygenerowany arkusz będzie nosił nazwę *Detail1*.

### Czy mogę kontrolować kolejność generowanych arkuszy?

Tak. Kolejność podąża za kolejnością w źródle danych. Jeśli potrzebujesz określonej kolejności, posortuj kolekcję przed przekazaniem jej do `Apply`.

### Czy można generować arkusze w innym skoroszycie?

Oczywiście. Utwórz drugą instancję `Workbook`, dodaj arkusz zastępczy i wywołaj `Apply` na tym arkuszu. Ta sama logika nazewnictwa zostanie zastosowana.

### Jak to działa przy dużych zestawach danych?

SmartMarkers są zoptymalizowane pod kątem wydajności. Nawet przy tysiącach wierszy biblioteka efektywnie strumieniuje dane. Upewnij się jedynie, że masz wystarczającą ilość pamięci dla ostatecznego rozmiaru skoroszytu.

---

## Kompletny działający przykład (gotowy do kopiowania)

Poniżej znajduje się pełny program, który możesz wkleić do nowego projektu konsolowego. Nie brakuje żadnych części – od dyrektyw `using` po ostateczne wywołanie `Save`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System;

class AutoNameExcelSheetsDemo
{
    static void Main()
    {
        // 1️⃣ Create workbook and master worksheet
        Workbook workbook = new Workbook();
        Worksheet master = workbook.Worksheets[0];
        master.Name = "Master";

        // 2️⃣ Set up SmartMarker options – this is the key to auto‑naming
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"   // base name for generated sheets
        };

        // 3️⃣ Sample data source – each element will become a new sheet
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop",   Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",    Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard", Qty = 3, Price =  45.50 }
        };

        // 4️⃣ Build a simple template on the master sheet
        master.Cells["A1"].PutValue("Order ID");
        master.Cells["B1"].PutValue("Product");
        master.Cells["C1"].PutValue("Quantity");
        master.Cells["D1"].PutValue("Unit Price");

        master.Cells["A2"].PutValue("&=orders.OrderId");
        master.Cells["B2"].PutValue("&=orders.Product");
        master.Cells["C2"].PutValue("&=orders.Qty");
        master.Cells["D2"].PutValue("&=orders.Price");

        // 5️⃣ Apply SmartMarkers – this auto‑creates and auto‑names the sheets
        master.SmartMarkers.Apply(options, new { orders });

        // 6️⃣ Save and inform the user
        workbook.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Done! Open AutoNamedSheets.xlsx – you’ll see Detail, Detail1, Detail2 …");
    }
}
```

Uruchom program, otwórz powstały plik *AutoNamedSheets.xlsx* i zobacz, jak działa funkcja **automatycznego nadawania nazw arkuszom Excel** w praktyce.

---

## Często zadawane pytania po przeczytaniu

- **Czy mogę użyć tego z istniejącym plikiem szablonu?**  
  Tak. Załaduj skoroszyt przy pomocy `new Workbook("Template.xlsx")` i wskaż `master` na arkusz, który zawiera znaczniki SmartMarker.

- **Co jeśli potrzebuję różnych konwencji nazewnictwa dla różnych typów arkuszy?**  
  Utwórz kilka obiektów `SmartMarkerOptions`, każdy z własnym `DetailSheetNewName`, i zastosuj je do różnych arkuszy głównych.

- **Czy istnieje sposób, aby ukryć arkusz bazowy (ten zawierający szablon)?**  
  Po wywołaniu `Apply` możesz po prostu usunąć arkusz główny: `workbook.Worksheets.RemoveAt(0);` – arkusze szczegółowe pozostaną nienaruszone.

---

## Podsumowanie

Teraz wiesz, **jak automatycznie nadawać nazwy arkuszom Excel** przy użyciu Aspose.Cells SmartMarkers, a także zobaczyłeś solidny wzorzec **jak generować arkusze** dynamicznie w C#. Główna idea jest prosta: skonfiguruj `SmartMarkerOptions.DetailSheetNewName`, podaj kolekcję i pozwól bibliotece zrobić resztę. To podejście eliminuje zbędne pętle, zapewnia unikalne nazwy i skaluje się płynnie.

Gotowy na kolejny krok? Spróbuj zamienić źródło danych na `Data

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}