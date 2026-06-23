---
category: general
date: 2026-05-30
description: Dowiedz się, jak dodać naprzemienne kolory wierszy w arkuszach C#, ustawić
  tło komórki za pomocą jednolitego wzoru wypełnienia oraz łatwo dostosować styl komórek
  arkusza.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: pl
og_description: Łatwe zmienianie kolorów wierszy w arkuszach C#. Dowiedz się, jak
  ustawić tło komórki, używać jednolitego wypełnienia i opanować styl komórek arkusza.
og_title: Naprzemienne kolory wierszy w arkuszach C# – Kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Naprzemienne kolory wierszy w arkuszach C# – Kompletny przewodnik
url: /pl/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Alternujące kolory wierszy w arkuszach C# – Kompletny przewodnik

Zastanawiałeś się kiedyś, jak sprawić, by eksport do Excela wyglądał profesjonalnie, używając **alternujących kolorów wierszy**? Nie jesteś sam — programiści ciągle pytają, jak *dodać kolor tła* do wierszy bez pisania miliona linii kodu.  

W tym tutorialu przejdziemy krok po kroku przez prosty sposób na **ustawienie tła komórek** w każdym wierszu, zastosowanie **solid fill pattern** oraz kontrolowanie **worksheet cell style**, aby rezultat był zarówno czytelny, jak i atrakcyjny wizualnie.

## Czego się nauczysz

- Pobieranie danych do `DataTable` (lub dowolnego źródła tabelarycznego).  
- Tworzenie tablicy obiektów `Style`, które naprzemiennie używają dwóch kolorów.  
- Importowanie `DataTable` do arkusza przy jednoczesnym zastosowaniu tych stylów.  
- Weryfikacja wyniku i ewentualna korekta kolorów lub wzorów.  

Nie potrzebujesz żadnych zewnętrznych narzędzi poza środowiskiem .NET i biblioteką do obsługi arkuszy (w przykładach użyjemy **Aspose.Cells**). Po zakończeniu będziesz mieć metodę, którą możesz wstawić do dowolnego potoku raportowania.

---

## Krok 1: Pobranie danych źródłowych jako `DataTable`

Na początek — bez danych nie ma czego stylizować. Poniżej znajduje się mały pomocnik, który tworzy `DataTable` z przykładowymi wierszami. W prawdziwym projekcie zamienisz to na wywołanie bazy danych lub parser CSV.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Dlaczego to ważne:** Umieszczenie danych w `DataTable` pozwala silnikowi arkusza *zaimportować* je jednym wywołaniem, automatycznie zachowując nazwy kolumn i typy danych.

## Krok 2: Utwórz style **Alternujących kolorów wierszy**

Teraz wygenerujemy tablicę obiektów `Style` — po jednym na każdy wiersz — tak, aby parzyste wiersze otrzymały jasny żółty odcień, a nieparzyste delikatny cyan. To jest sedno techniki **alternujących kolorów wierszy**.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### Dlaczego używać **Solid Fill Pattern**?

Właściwość `Pattern` informuje silnik, jak renderować kolor. Wypełnienie `Solid` gwarantuje, że całe tło komórki zostanie pomalowane, eliminując słabe linie siatki, które mogłyby się pojawić. To najczęstszy sposób na **ustawienie tła komórek**, gdy chcesz uzyskać czysty wygląd.

## Krok 3: Importuj `DataTable` z przygotowanymi stylami

Gdy tablica stylów jest gotowa, wywołanie importu staje się jedną linią kodu. Aspose.Cells automatycznie zastosuje odpowiedni styl do każdego wiersza.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **Co dzieje się pod maską?**  
> Biblioteka iteruje po każdym wierszu, kopiuje wartości do komórek, a następnie stosuje pasujący `Style` z `rowStyles`. Ponieważ już zdefiniowaliśmy **solid fill pattern**, każda komórka w wierszu dziedziczy ten sam kolor tła, dając idealne **alternujące kolory wierszy**.

## Krok 4: Zapisz skoroszyt i zweryfikuj wynik

Szybki zapis pozwala otworzyć plik w Excelu (lub dowolnym kompatybilnym podglądzie) i zobaczyć efekt.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

Po otwarciu pliku wiersze 1, 3, 5… będą jasnym żółtym, natomiast wiersze 2, 4, 6… jasnym cyanem. Nagłówki kolumn pozostają białe, co podkreśla dane.

![Worksheet showing alternating row colors](/images/alternating-row-colors.png "Screenshot of worksheet with alternating row colors")

*Tekst alternatywny obrazu:* **alternujące kolory wierszy** – zrzut ekranu arkusza, w którym tło każdego wiersza naprzemiennie przechodzi od jasnego żółtego do jasnego cyanowego.

## Krok 5: Dalsze dostosowywanie (opcjonalnie)

### Zmiana kolorów

Jeśli Twoja marka używa innych odcieni, po prostu zamień `Color.LightYellow` i `Color.LightCyan` na dowolny `System.Drawing.Color`, który preferujesz. Na przykład:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Użyj innego **Background Type**

Choć `BackgroundType.Solid` jest najczęstszy, możesz eksperymentować z `BackgroundType.Gray125`, `BackgroundType.Horizontal` lub dowolnym wzorem obsługiwanym przez bibliotekę. Zmienia to teksturę wizualną, jednocześnie **dodając kolor tła**.

### Zastosuj **Worksheet Cell Style** do konkretnych kolumn

Czasami chcesz, aby efekt naprzemienny dotyczył tylko kolumn danych, pozostawiając pierwszą kolumnę (np. identyfikatory) niezmienioną. Utwórz osobny styl dla tej kolumny i przypisz go po imporcie:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## Zakończenie

Masz teraz kompletną, wielokrotnego użytku rozwiązanie dla **alternujących kolorów wierszy** w arkuszach C#. Tworząc tablicę obiektów `Style`, **ustawiając tło komórek** przy użyciu **solid fill pattern** i importując `DataTable` jednym wywołaniem, możesz generować profesjonalnie wyglądające raporty przy minimalnej ilości kodu.  

Od tego momentu możesz:

- **Dodać kolor tła** do wierszy nagłówków dla dodatkowego wyróżnienia.  
- Połączyć technikę z formatowaniem warunkowym, aby uzyskać dynamiczne wskazówki wizualne.  
- Zbadać inne właściwości **worksheet cell style**, takie jak czcionki, obramowania czy formaty liczb.

Wypróbuj to w następnym procesie eksportu — Twoi użytkownicy podziękują Ci za czytelniejsze i bardziej przejrzyste arkusze. Szczęśliwego kodowania!

## Co warto się nauczyć dalej?

- [Set Row Height in Worksheet with Aspose.Cells for .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Convert Excel Cell Names to Row and Column Indices Using Aspose.Cells for .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Set Worksheet Tab Colors in Excel Using Aspose.Cells .NET - A Comprehensive Guide](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}