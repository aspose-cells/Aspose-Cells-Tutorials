---
category: general
date: 2026-06-17
description: Ustaw format daty w Excelu przy użyciu C#, a także ustaw tło komórki,
  zastosuj kolor tekstu i pokoloruj kolumnę w Excelu podczas importu. Dowiedz się
  krok po kroku.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: pl
og_description: Ustaw format daty w Excelu przy użyciu C#, jednocześnie ustawiając
  tło komórki, stosując kolor czcionki i kolorując kolumnę w Excelu podczas importu.
  Pełny poradnik.
og_title: Ustaw format daty w Excelu przy użyciu C# – Kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: Ustaw format daty w Excelu za pomocą C# – Kompletny przewodnik formatowania
  importu
url: /pl/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ustaw format daty w Excelu przy użyciu C# – Kompletny przewodnik po formatowaniu importu

Kiedykolwiek potrzebowałeś **ustawić format daty** w arkuszu Excel generowanym z kodu C#, a jednocześnie chciałeś, aby kolumna miała własne tło lub kolor tekstu? Nie jesteś sam. W wielu scenariuszach raportowania pobierasz `DataTable` z bazy danych, wkładasz go do arkusza i potem walczysz, aby daty wyglądały prawidłowo, a kolumny przyciągały uwagę odpowiednimi kolorami.  

W tym samouczku przejdziemy przez czyste, kompleksowe rozwiązanie, które **ustawia format daty**, **ustawia tło komórki**, **stosuje kolor tekstu**, a nawet **koloruje kolumnę w Excelu** podczas importu danych. Po zakończeniu będziesz mieć wielokrotnego użytku wzorzec, który obsługuje **excel import formatting** bez typowych prób i błędów.

> **Co będzie potrzebne**  
> * .NET 6+ (lub .NET Framework 4.7+)  
> * Aspose.Cells for .NET (darmowa wersja próbna wystarczy do testów)  
> * Źródło `DataTable` – dowolne zapytanie ADO.NET będzie odpowiednie  
> * Visual Studio lub ulubione IDE  

Zaczynajmy.

---

## Przegląd rozwiązania

Podzielimy problem na trzy logiczne części:

1. **Pobranie danych źródłowych** – `DataTable` z wierszami, które chcesz wyeksportować.  
2. **Utworzenie stylów specyficznych dla kolumn** – jeden styl dla kolumny z datą, inny dla kolumny tekstowej oraz dowolne dodatkowe formatowanie, które chcesz dodać.  
3. **Import tabeli ze stylami** – użyj `Worksheet.Cells.ImportDataTable`, aby każda kolumna odziedziczyła przygotowany styl.

Dlaczego tak? Ponieważ Aspose.Cells pozwala dołączyć tablicę `Style` bezpośrednio do wywołania `ImportDataTable`, co eliminuje potrzebę drugiego przebiegu w celu ponownego zastosowania formatowania. To szybsze, mniej podatne na błędy i utrzymuje kod schludnym.

---

## Krok 1: Pobranie danych do eksportu

Najpierw potrzebujesz `DataTable`. W prawdziwym projekcie prawdopodobnie wywołasz procedurę składowaną lub użyjesz Entity Framework, aby ją wypełnić, ale dla ilustracji zamockujemy prostą tabelę z kolumną daty i tekstową.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Porada:** Jeśli Twoje źródło używa dat nullable, upewnij się, że typ kolumny to `typeof(DateTime?)` – Aspose i tak zastosuje później przypisany format.

---

## Krok 2: Przygotowanie tablicy stylów – po jednym dla każdej kolumny

Teraz tworzymy `Style[]`, którego długość odpowiada liczbie kolumn w `DataTable`. Każdy element będzie przechowywał formatowanie dla odpowiedniej kolumny.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 Ustaw format daty dla pierwszej kolumny

Pierwsza kolumna (`OrderDate`) powinna wyświetlać się jako „MM/dd/yyyy”. Aspose używa wbudowanego indeksu formatu liczbowego 14 dla krótkiej daty, ale możesz także podać własny ciąg formatowy, jeśli wolisz.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Dlaczego to ważne:** Excel przechowuje daty jako liczby seryjne. Przypisując format liczbowy, informujesz Excel, aby renderował te liczby jako czytelne daty zamiast surowych numerów.

### 2.2 Ustaw tło komórki dla drugiej kolumny

Nadajmy kolumnie `CustomerName` jasnoniebieskie tło. To właśnie tutaj wchodzi w grę **set cell background**.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Uwaga:** Bez ustawienia `Pattern` na `Solid`, kolor pierwszoplanowy nie pojawi się, ponieważ domyślny wzór to „None”.

### 2.3 Zastosuj kolor pierwszoplanowy (tekst) – opcjonalny dodatek

Jeśli chcesz, aby sam tekst miał kontrastowy kolor, możesz dostosować ten sam styl:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

Spełnia to wymóg **apply foreground color**, zachowując jednocześnie tło kolumny.

---

## Krok 3: Import DataTable ze zdefiniowanymi stylami

Mając gotowe style, ostatni krok to jednorazowe wywołanie, które importuje dane i stosuje style kolumna po kolumnie.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Jak to działa:** Aspose odczytuje tablicę `columnStyles` i mapuje każdy `Style` na odpowiadający indeks kolumny. Wiersz nagłówka dziedziczy domyślny styl, chyba że dostarczysz osobny styl dla wiersza 0.

### 3.1 Zapisz skoroszyt

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Uruchom program, otwórz *FormattedReport.xlsx* i powinieneś zobaczyć:

- kolumnę **OrderDate** wyświetlaną jako daty (np. `06/15/2026`).  
- kolumnę **CustomerName** z jasnoniebieskim wypełnieniem i ciemnoniebieskim tekstem.  

To całość **excel import formatting** w mniej niż 30 linijkach C#.

---

## Podsumowanie krok po kroku (z wyjaśnieniem dlaczego)

| Krok | Co robisz | Dlaczego to ważne |
|------|-----------|-------------------|
| **Pobranie danych** | Wywołaj `GetData()`, aby wypełnić `DataTable`. | Dostarcza ustrukturyzowane źródło, które Aspose może bezpośrednio przetworzyć. |
| **Utworzenie tablicy stylów** | Alokuj `Style[]` o długości równej liczbie kolumn. | Umożliwia stylowanie poszczególnych kolumn w jednym wywołaniu importu. |
| **Ustaw format daty** | `columnStyles[0].Number = 14;` | Zapewnia prawidłowe wyświetlanie dat w Excelu. |
| **Ustaw kolor tła** | `ForegroundColor = LightBlue; Pattern = Solid;` | Podkreśla kolumnę, spełniając **set cell background**. |
| **Zastosuj kolor tekstu** | `Font.Color = DarkBlue;` | Poprawia czytelność i spełnia **apply foreground color**. |
| **Import ze stylami** | `ImportDataTable(..., columnStyles);` | Jednoprzebiegowy import, który respektuje wszystkie formatowania. |
| **Zapis skoroszytu** | `wb.Save(...);` | Trwale zapisuje wynik dla dalszych użytkowników. |

---

## Obsługa przypadków brzegowych i najczęstsze pytania

### Co zrobić, jeśli mam więcej niż dwie kolumny?

Po prostu rozszerz tablicę `columnStyles` i przypisz `Style` do każdego indeksu, który Cię interesuje. Nieprzypisane indeksy odziedziczą domyślny styl, co jest w pełni akceptowalne.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### Jak sformatować kolumnę jako walutę?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### Czy mogę osobno stylować wiersz nagłówka?

Tak. Po imporcie możesz pobrać pierwszy wiersz i zastosować odrębny styl:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### Co zrobić, gdy `DataTable` zawiera nullowe daty?

Aspose pozostawi te komórki puste. Jeśli wolisz placeholder, np. „N/A”, możesz wstępnie przetworzyć tabelę:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Następnie dostosuj styl, aby wyświetlał własny format pokazujący „N/A” dla wartości sentinel.

---

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do skopiowania program. Uruchom go jako aplikację konsolową, a otrzymasz ładnie sformatowany plik Excel.



## Co powinieneś nauczyć się dalej?

Poniższe samouczki dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletny kod oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkryć alternatywne podejścia w własnych projektach.

- [Ustaw kolor czcionki w komórkach Excel przy użyciu Aspose.Cells dla .NET](/cells/english/net/formatting/setting-font-color/)
- [Ustaw kolor czcionki w .NET Excel z Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Ustaw szerokość kolumn Excel w pikselach przy użyciu Aspose.Cells dla .NET | Przewodnik krok po kroku](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}