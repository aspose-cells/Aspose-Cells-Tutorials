---
category: general
date: 2026-06-08
description: Jak połączyć arkusze w Excelu przy użyciu SmartMarkerProcessor do raportów
  master‑detail. Wypełnij arkusz główny i łatwo wygeneruj raport Excel master‑detail.
draft: false
keywords:
- how to link sheets
- populate master sheet
- create master detail excel
- generate master detail report
language: pl
og_description: Jak połączyć arkusze w Excelu za pomocą SmartMarkerProcessor. Dowiedz
  się, jak wypełnić arkusz główny i wygenerować raport master‑detail w kilka minut.
og_title: Jak połączyć arkusze w Excelu za pomocą SmartMarker – krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  headline: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  type: TechArticle
- description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  name: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  steps:
  - name: Multiple Detail Rows per Master
    text: If a master row has several related details, SmartMarker repeats the master
      row once and then writes *all* matching detail rows beneath it. No extra code
      is needed—just ensure your `Details` collection contains every row.
  - name: Missing Details
    text: When a master entry has no matching detail rows, the detail sheet simply
      skips that section. If you need a placeholder (e.g., “No items”), you can add
      a calculated column in the template that uses an Excel formula like `=IF(COUNTA(A2:B2)=0,"No
      items","")`.
  - name: Large Datasets
    text: 'Processing tens of thousands of rows can be memory‑intensive. To keep performance
      snappy:'
  - name: Custom Column Mapping
    text: If your property names don’t line up (`MasterKey` vs `Id`), you can use
      the `SmartMarkerProcessor.Map` method to create an alias before processing.
  type: HowTo
tags:
- Excel
- SmartMarker
- C#
- master‑detail
title: Jak połączyć arkusze w Excelu za pomocą SmartMarker – Przewodnik krok po kroku
url: /pl/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak połączyć arkusze w Excelu za pomocą SmartMarker – przewodnik krok po kroku

Zastanawiałeś się kiedyś **jak połączyć arkusze** w Excelu bez ręcznego kopiowania wierszy czy pisania niekończących się pętli VBA? Nie jesteś sam. Większość programistów napotyka problem, gdy potrzebują czystego raportu master‑detail, który pozostaje zsynchronizowany w miarę zmian danych. Dobra wiadomość? SmartMarkerProcessor wykona ciężką pracę za Ciebie, zamieniając kilka linii C# w w pełni funkcjonalny skoroszyt master‑detail.

W tym samouczku przeprowadzimy Cię przez dokładne kroki **wypełniania arkusza master**, skonfigurowania arkusza szczegółowego oraz ostatecznie **generowania raportu master‑detail**, który aktualizuje się automatycznie. Po zakończeniu będziesz mieć wzorzec, który możesz wstawić do dowolnego projektu .NET.

> **Uwaga wstępna:** Potrzebujesz GrapeCity Documents for Excel (GcExcel) w wersji 2024 lub nowszej, środowiska programistycznego .NET (Visual Studio 2022 świetnie się sprawdza) oraz podstawowej znajomości C#. Nie są wymagane dodatkowe pakiety NuGet poza GcExcel.

---

## Przegląd rozwiązania

Zanim zanurzymy się w kod, rozłóżmy, co tak naprawdę oznacza „łączenie arkuszy” w kontekście SmartMarker:

1. **Arkusz master** – Zawiera jeden wiersz na encję (np. listę klientów).
2. **Arkusz szczegółowy** – Zawiera wiersze należące do wiersza master (np. zamówienia dla każdego klienta).
3. **Składnia SmartMarker** – Mały język znaczników (`{MasterSheet}#master;{DetailSheet}#detail`), który informuje procesor, jak powiązać dwie tabele danych.
4. **Opcje procesora** – Włączenie `MasterDetail` sprawia, że silnik automatycznie powtarza wiersze master i wstawia powiązane wiersze szczegółowe pod nimi.

Zrozumienie tych elementów pomoże Ci później dostosować podejście — być może potrzebujesz trójpoziomowego zagnieżdżenia lub formatowania warunkowego. Trzymaj ten model mentalny pod ręką, gdy będziemy przechodzić przez implementację.

---

## Krok 1: Przygotowanie danych hierarchicznych do przetwarzania master‑detail

Pierwszą rzeczą, której potrzebujesz, jest źródło danych odzwierciedlające relację master‑detail. W większości rzeczywistych scenariuszy pochodzi to z bazy danych, ale dla przejrzystości użyjemy anonimowego obiektu literałowego.

```csharp
// Step 1: Prepare hierarchical data for master‑detail processing
var sampleData = new
{
    // Master collection – one row per category
    Master = new[]
    {
        new { Id = 1, Name = "A" },
        new { Id = 2, Name = "B" }
    },

    // Detail collection – rows reference MasterId
    Details = new[]
    {
        new { MasterId = 1, Item = "Item1" },
        new { MasterId = 2, Item = "Item2" }
    }
};
```

**Dlaczego to ważne:** SmartMarker nie zgaduje magicznie relacji; szuka pasujących nazw właściwości (`MasterId` → `Id`). Strukturyzując dane w ten sposób, dajemy procesorowi klarowną mapę, co jest fundamentem **jak połączyć arkusze** skutecznie.

> **Pro tip:** Jeśli Twoje dane znajdują się w obiektach `DataTable`, wystarczy udostępnić je jako właściwości o tych samych nazwach — SmartMarker działa z dowolną kolekcją enumerowalną.

---

## Krok 2: Utworzenie skoroszytu i załadowanie szablonu

SmartMarker działa na istniejącym skoroszycie Excel, zazwyczaj szablonie, który już zawiera nazwy arkuszy i znaczniki zastępcze. Utwórzmy skoroszyt w pamięci i dodajmy dwa puste arkusze nazwane *MasterSheet* i *DetailSheet*.

```csharp
using GrapeCity.Documents.Excel;

// Step 2: Create a workbook and add template sheets
IWorkbook wb = new Workbook();

// Create the master sheet and add a header row
IWorksheet masterSheet = wb.Worksheets.Add("MasterSheet");
masterSheet.Range["A1"].Value = "ID";
masterSheet.Range["B1"].Value = "Name";

// Create the detail sheet and add its header
IWorksheet detailSheet = wb.Worksheets.Add("DetailSheet");
detailSheet.Range["A1"].Value = "Master ID";
detailSheet.Range["B1"].Value = "Item";
```

Możesz także załadować plik `.xlsx` z dysku (`wb.Open("Template.xlsx")`), jeśli wolisz najpierw zaprojektować układ w Excelu. Ważne jest, aby nazwy arkuszy zgadzały się z tymi, które odwołujesz w ciągu SmartMarker.

---

## Krok 3: Inicjalizacja SmartMarkerProcessor i włączenie trybu Master‑Detail

Teraz wprowadzamy silnik, który odczyta znaczniki i wstawi dane. `SmartMarkerProcessor` przyjmuje skoroszyt jako argument konstruktora, a flaga `Options.MasterDetail` mówi mu, aby traktował znaczniki `#master` i `#detail` jako powiązaną parę.

```csharp
// Step 3: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

// Enable master‑detail mode on the processor options
processor.Options.MasterDetail = true;
```

**Dlaczego włączamy `MasterDetail`?** Bez tej flagi procesor potraktowałby `{MasterSheet}#master` i `{DetailSheet}#detail` jako niezależne operacje, tracąc kluczowy związek między wierszami. Ustawienie flagi to jedyna linijka, która sprawia, że **jak połączyć arkusze** naprawdę działa.

---

## Krok 4: Definicja ciągu SmartMarker i uruchomienie procesora

Ciąg znaczników mówi SmartMarker, który arkusz jest master, a który szczegółowy. Składnia jest prosta: `{SheetName}#master;{SheetName}#detail`. Możesz także dodać dodatkowe znaczniki (np. `#header`), ale nie są one potrzebne w podstawowym raporcie.

```csharp
// Step 4: Execute the smart‑marker processing, linking master and detail sheets
string marker = "{MasterSheet}#master;{DetailSheet}#detail";
processor.Process(marker, sampleData);
```

Podczas wykonywania `Process` silnik:

1. Zapisuje każdy wiersz master do *MasterSheet* zaczynając od pierwszego pustego wiersza po nagłówku.
2. Dla każdego wiersza master przeszukuje kolekcję `Details`, wybiera wiersze, w których `MasterId` pasuje do `Id` mastera, i zapisuje je do *DetailSheet* bezpośrednio pod odpowiednim wpisem mastera.

---

## Krok 5: Zapis lub eksport gotowego skoroszytu

W tym momencie masz w pełni wypełniony skoroszyt. Możesz zapisać go na dysk, przesłać strumieniowo do klienta webowego lub nawet przekonwertować na PDF.

```csharp
// Save the workbook to a file (you could also stream it to a response)
wb.Save("MasterDetailReport.xlsx");
```

Otwórz plik, a zobaczysz dwa arkusze: *MasterSheet* wymienia `A` i `B`, natomiast *DetailSheet* pokazuje `Item1` pod masterem `1` oraz `Item2` pod masterem `2`. To istota **wypełniania arkusza master** i **generowania raportu master‑detail** w jednym kroku.

---

## Przegląd wizualny

![Diagram illustrating how to link sheets in Excel using SmartMarkerProcessor](https://example.com/diagram.png "How to link sheets diagram")

Diagram (tekst alternatywny zawiera główne słowo kluczowe) pokazuje przepływ danych od obiektów C# → SmartMarkerProcessor → połączonych arkuszy Excela.

---

## Obsługa typowych przypadków brzegowych

### Wiele wierszy szczegółowych na jeden master

Jeśli wiersz master ma kilka powiązanych szczegółów, SmartMarker powtarza wiersz master raz, a następnie zapisuje *wszystkie* pasujące wiersze szczegółowe pod nim. Nie wymaga dodatkowego kodu — wystarczy, że Twoja kolekcja `Details` zawiera wszystkie wiersze.

### Brak szczegółów

Gdy wpis master nie ma pasujących wierszy szczegółowych, arkusz szczegółowy po prostu pomija tę sekcję. Jeśli potrzebujesz zastępczego komunikatu (np. „Brak pozycji”), możesz dodać obliczaną kolumnę w szablonie, używając formuły Excel, takiej jak `=IF(COUNTA(A2:B2)=0,"No items","")`.

### Duże zestawy danych

Przetwarzanie dziesiątek tysięcy wierszy może być intensywne pod względem pamięci. Aby utrzymać wydajność:

- Użyj `processor.Options.EnableStreaming = true` (dostępne w GcExcel 2025+).
- Podziel dane na partie i przetwarzaj każdą osobno, a następnie scal skoroszyty.

### Niestandardowe mapowanie kolumn

Jeśli nazwy Twoich właściwości nie pasują (`MasterKey` vs `Id`), możesz użyć metody `SmartMarkerProcessor.Map`, aby przed przetwarzaniem utworzyć alias.

```csharp
processor.Map("MasterId", "Id"); // tells the engine that MasterId maps to Id
```

---

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny program gotowy do skopiowania i uruchomienia od razu.



## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Mistrzowskie formuły zewnętrznych odnośników w Excelu przy użyciu Aspose.Cells dla Javy](/cells/english/java/formulas-functions/aspose-cells-java-external-link-formulas-excel/)
- [Mistrzowskie dynamiczne arkusze Excel w Javie z Aspose.Cells&#58; Kompletny przewodnik](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Mistrzowskie dynamiczne raporty Excel przy użyciu Aspose.Cells Java&#58; Nazwane zakresy i złożone formuły](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}