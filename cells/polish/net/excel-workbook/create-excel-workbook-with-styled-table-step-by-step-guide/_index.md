---
category: general
date: 2026-03-21
description: Utwórz skoroszyt programu Excel i zaimportuj tabelę danych do Excela,
  ustawiając styl kolumn, wyeksportuj dane do Excela oraz sformatuj datę w komórkach
  Excela w minutach.
draft: false
keywords:
- create excel workbook
- import datatable to excel
- set column style
- export data to excel
- format excel cells date
language: pl
og_description: Szybko twórz skoroszyt Excel. Dowiedz się, jak zaimportować tabelę
  danych do Excela, ustawić styl kolumn, wyeksportować dane do Excela oraz sformatować
  daty w komórkach Excela w jednym przewodniku.
og_title: Utwórz skoroszyt Excel – Pełny poradnik stylizacji i eksportu
tags:
- C#
- Aspose.Cells
- Excel automation
title: Utwórz skoroszyt Excel ze stylizowaną tabelą – przewodnik krok po kroku
url: /pl/net/excel-workbook/create-excel-workbook-with-styled-table-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt Excel – Kompletny samouczek programistyczny

Czy kiedykolwiek potrzebowałeś **create excel workbook**, które wygląda profesjonalnie od razu po wygenerowaniu w kodzie? Być może pobierasz dane z bazy danych i chcesz, aby daty wyświetlały się w odpowiednim formacie bez późniejszego majsterkowania w Excelu. To powszechny problem — zwłaszcza gdy wynik trafia do skrzynki odbiorczej klienta i oczekuje, że wszystko będzie gotowe do użycia.

W tym przewodniku przejdziemy przez jedną, samodzielną rozwiązanie, które **imports datatable to excel**, stosuje **set column style**, a na koniec **export data to excel** jako ładnie sformatowany plik. Zobaczysz dokładnie, jak **format excel cells date**, aby arkusz wyglądał jak profesjonalny raport, i otrzymasz kompletny, gotowy do uruchomienia przykład na końcu. Bez brakujących elementów, bez skrótów typu „zobacz dokumentację” — po prostu czysty kod, który możesz od razu wstawić do swojego projektu.

---

## Co się nauczysz

- Jak **create excel workbook** przy użyciu biblioteki Aspose.Cells (lub dowolnego kompatybilnego API).
- Najszybszy sposób na **import datatable to excel** bez ręcznych pętli komórka‑po‑komórce.
- Techniki **set column style**, w tym zastosowanie formatu daty w określonej kolumnie.
- Jak **export data to excel** jednym wywołaniem `Save`.
- Typowe pułapki przy **format excel cells date** i jak ich unikać.

### Wymagania wstępne

- .NET 6+ (lub .NET Framework 4.6+).  
- Aspose.Cells dla .NET zainstalowany (`Install-Package Aspose.Cells`).  
- `DataTable` gotowy do eksportu — Twoje źródło danych może być SQL, CSV lub cokolwiek, co da się przekształcić w `DataTable`.

Jeśli już czujesz się pewnie w C# i masz te elementy, możesz od razu przystąpić. W przeciwnym razie sekcja „Wymagania wstępne” powyżej zapewni szybki checklist.

---

## Krok 1 – Utwórz instancję skoroszytu Excel

Pierwszą rzeczą, którą robisz, gdy chcesz **create excel workbook** programowo, jest zainicjowanie obiektu workbook. To jak otwarcie pustego notesu, w którym później zapiszesz swoje dane.

```csharp
using Aspose.Cells;
using System.Data;

// Step 1: Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();
```

> **Dlaczego to ważne:**  
> Klasa `Workbook` jest punktem wejścia dla każdej operacji w Aspose.Cells. Utworzenie jej na początku daje czyste płótno, a później możesz załadować istniejący plik, jeśli potrzebujesz dopisać dane zamiast zaczynać od zera.

---

## Krok 2 – Przygotuj DataTable do importu

Zanim będziemy mogli **import datatable to excel**, potrzebujemy `DataTable`. W prawdziwych projektach pochodzi on często z `SqlDataAdapter.Fill` lub `DataTable.Load`. Dla przejrzystości stworzymy metodę, która zwraca gotową tabelę.

```csharp
// Step 2: Obtain the data to be written – a DataTable with three columns
DataTable dataTable = GetData();   // assume GetData() returns the required table

// Example implementation (you can replace this with your own data source)
DataTable GetData()
{
    DataTable dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Quantity", typeof(int));

    dt.Rows.Add(DateTime.Today.AddDays(-2), "Apples", 120);
    dt.Rows.Add(DateTime.Today.AddDays(-1), "Bananas", 85);
    dt.Rows.Add(DateTime.Today, "Cherries", 60);
    return dt;
}
```

> **Wskazówka:** Jeśli Twoje daty są przechowywane jako ciągi znaków, najpierw przekonwertuj je na `DateTime` — w przeciwnym razie krok **format excel cells date** nie zadziała zgodnie z oczekiwaniami.

---

## Krok 3 – Zdefiniuj style dla każdej kolumny (Set Column Style)

Teraz nadchodzi część, w której **set column style**. Utworzymy tablicę obiektów `Style` — po jednym dla każdej kolumny. Pierwsza kolumna otrzyma wbudowany format daty (kod 14), a pozostałe pozostaną w formacie ogólnym (kod 0).

```csharp
// Step 3: Define a style for each column; apply a date format to the first column
Style[] columnStyles = new Style[3];
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = workbook.CreateStyle();
    columnStyles[i].Number = (i == 0) ? 14 : 0;   // 14 = date format, 0 = general
}
```

> **Dlaczego używać obiektów stylu?**  
> Zastosowanie stylu raz i ponowne jego użycie jest znacznie wydajniejsze niż ustawianie formatu w każdej komórce osobno. Gwarantuje to także, że cała kolumna respektuje tę samą regułę **format excel cells date**, co jest kluczowe dla spójności przy otwieraniu pliku w różnych ustawieniach regionalnych.

---

## Krok 4 – Importuj DataTable ze stylami do arkusza

Mając gotowy workbook i zdefiniowane style, teraz **import datatable to excel**. Metoda `ImportDataTable` wykonuje ciężką pracę: zapisuje nagłówki kolumn, wiersze i stosuje przekazane style.

```csharp
// Step 4: Access the first worksheet and import the DataTable using the styles
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

> **Co się dzieje „pod maską”?**  
> - `true` mówi Aspose.Cells, aby uwzględnił nazwy kolumn jako pierwszy wiersz.  
> - `0, 0` to indeksy początkowego wiersza i kolumny (górny‑lewy róg).  
> - `columnStyles` dopasowuje każdą kolumnę do przygotowanego stylu, zapewniając zastosowanie reguły **format excel cells date** w kolumnie z datą.

---

## Krok 5 – Zapisz (wyeksportuj) skoroszyt do pliku fizycznego

Na koniec **export data to excel** zapisując workbook na dysku. Możesz zmienić ścieżkę na dowolny folder lub nawet strumieniowo przesłać plik bezpośrednio w odpowiedzi HTTP w API webowym.

```csharp
// Step 5: Save the workbook with the styled table
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

> **Pro tip:** Użyj `workbook.Save(Stream, SaveFormat.Xlsx)`, gdy musisz przesłać plik przez sieć bez zapisywania go na dysku.

---

## Pełny działający przykład (wszystkie kroki razem)

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Skopiuj‑wklej go do aplikacji konsolowej, dostosuj ścieżkę wyjściową i w kilka sekund będziesz mieć ładnie sformatowany plik Excel.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Get the data (replace GetData with your own source if needed)
        DataTable dataTable = GetData();

        // 3️⃣ Prepare column styles – date format for the first column
        Style[] columnStyles = new Style[3];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            columnStyles[i] = workbook.CreateStyle();
            columnStyles[i].Number = (i == 0) ? 14 : 0;   // 14 = date, 0 = general
        }

        // 4️⃣ Import the DataTable with the styles
        Worksheet worksheet = workbook.Worksheets[0];
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 5️⃣ Save the file
        workbook.Save("StyledTable.xlsx");

        Console.WriteLine("Excel workbook created successfully!");
    }

    // Sample data generator – replace with real data source
    static DataTable GetData()
    {
        DataTable dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(DateTime.Today.AddDays(-2), "Apples", 120);
        dt.Rows.Add(DateTime.Today.AddDays(-1), "Bananas", 85);
        dt.Rows.Add(DateTime.Today, "Cherries", 60);
        return dt;
    }
}
```

**Oczekiwany wynik:**  
Po otwarciu `StyledTable.xlsx` kolumna A wyświetla daty w formacie np. `03/19/2026` (w zależności od Twoich ustawień regionalnych), a kolumny B i C pokazują nazwy produktów oraz ilości jako zwykły tekst/liczby. Nie są potrzebne dodatkowe kroki formatowania — proces **create excel workbook** jest zakończony.

---

## Najczęściej zadawane pytania i przypadki brzegowe

### 1️⃣ Co zrobić, gdy mój DataTable ma więcej niż trzy kolumny?
Dodaj kolejne obiekty `Style` do tablicy `columnStyles` i dostosuj właściwość `Number` dla każdej kolumny, która wymaga specjalnego formatu (np. waluta, procenty). Metoda `ImportDataTable` dopasuje każdy styl według pozycji.

### 2️⃣ Czy mogę zastosować własny format daty zamiast wbudowanego 14?
Oczywiście. Zamień `columnStyles[i].Number = 14;` na:

```csharp
columnStyles[i].Number = 22;               // built‑in custom format ID
columnStyles[i].Custom = "dd‑MMM‑yyyy";    // or any .NET date pattern you like
```

### 3️⃣ Jak **export data to excel** w API webowym bez zapisywania na dysku?
Użyj `MemoryStream`:

```csharp
using (var ms = new MemoryStream())
{
    workbook.Save(ms, SaveFormat.Xlsx);
    ms.Position = 0;
    // return File(ms.ToArray(), "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "Report.xlsx");
}
```

### 4️⃣ Co jeśli lokalizacja użytkownika wymaga innego separatora daty?
Wbudowany format daty (ID 14) respektuje ustawienia regionalne skoroszytu. Jeśli potrzebujesz stałego formatu niezależnie od locale, użyj właściwości `Custom`, jak pokazano wyżej.

### 5️⃣ Czy to działa z .NET Core?
Tak — Aspose.Cells obsługuje .NET Standard 2.0 i nowsze, więc ten sam kod działa na .NET 6, .NET 7 oraz innych kompatybilnych środowiskach.

---

## Wskazówki najlepszych praktyk (Pro Tips)

- **Ponowne używanie stylów**: Tworzenie stylu na kolumnę jest tanie, ale używanie tego samego obiektu stylu dla identycznych kolumn oszczędza pamięć.
- **Unikaj pętli komórka‑po‑komórce**: `ImportDataTable` jest wysoce zoptymalizowane; ręczne pętle są wolniejsze i podatne na błędy.
- **Ustaw kulturę skoroszytu wcześnie**, jeśli potrzebujesz spójnych separatorów liczb/daty w różnych środowiskach:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

- **Waliduj DataTable** przed importem — null‑owe daty spowodują wyjątek przy zastosowaniu stylu daty.
- **Włącz obliczenia**, jeśli po imporcie dodajesz formuły:

```csharp
workbook.CalculateFormula();
```

---

## Zakończenie

Masz teraz kompletny, end‑to‑end przepis na **create excel workbook**, **import datatable to excel**, **set column style**, **export data to excel** oraz **format excel cells date** — wszystko w kilkunastu linijkach C#. Podejście jest szybkie, niezawodne i trzyma kwestie formatowania w kodzie, dzięki czemu gotowy arkusz jest gotowy dla użytkowników biznesowych w momencie otwarcia.

Gotowy na kolejny wyzwanie? Spróbuj dodać formatowanie warunkowe, wstawić wykresy lub przekonwertować

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}