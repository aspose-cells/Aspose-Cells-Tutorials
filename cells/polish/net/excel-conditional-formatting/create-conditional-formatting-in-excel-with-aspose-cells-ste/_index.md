---
category: general
date: 2026-06-30
description: Utwórz formatowanie warunkowe w skoroszycie Excel przy użyciu Aspose.Cells.
  Dowiedz się, jak ustawić tło komórki, ocenić komórki i programowo zbudować plik.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: pl
og_description: Utwórz formatowanie warunkowe w skoroszycie Excel przy użyciu Aspose.Cells.
  Skorzystaj z tego pełnego samouczka, aby ustawić tło komórek, nadać im rangę i zautomatyzować
  Excel.
og_title: Utwórz formatowanie warunkowe w Excelu przy użyciu Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Tworzenie formatowania warunkowego w Excelu z Aspose.Cells – przewodnik krok
  po kroku
url: /pl/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie formatowania warunkowego w Excelu przy użyciu Aspose.Cells – przewodnik krok po kroku

Zastanawiałeś się kiedyś, jak **utworzyć formatowanie warunkowe** w pliku Excel bez otwierania interfejsu użytkownika? Nie jesteś sam. Wielu programistów musi **tworzyć skoroszyty Excel** w locie, a robienie tego programowo oszczędza godziny ręcznej pracy. W tym tutorialu pokażemy dokładnie, jak **utworzyć formatowanie warunkowe**, stylizować komórki i nawet rankingować najwyższe wartości — wszystko przy użyciu potężnej biblioteki Aspose.Cells dla .NET.

Przejdziemy przez praktyczny przykład: generowanie arkusza wyników, podświetlanie wysokich wyników jasnym zielonym oraz nadanie złego tła trzem najlepszym uczestnikom. Po zakończeniu będziesz wiedział **jak ustawić tło komórki**, **jak rankingować komórki** oraz **jak używać Aspose** do zaawansowanej automatyzacji Excela. Bez zbędnych wstępów, tylko kompletny, gotowy do uruchomienia kod, który możesz wkleić do dowolnego projektu C#.

## Czego się nauczysz

- Jak **utworzyć skoroszyt Excel** przy użyciu Aspose.Cells  
- Jak wypełnić zakres losowymi danymi (wynikami)  
- Jak **ustawić tło komórki** przy użyciu jednolitych kolorów  
- Jak zastosować regułę opartą na formule do **rankingowania komórek** i podświetlenia trzech najlepszych  
- Jak zapisać wynik jako plik .xlsx  

Wymagania wstępne: .NET 6+ (lub .NET Framework 4.6+), Visual Studio (lub dowolne IDE C#) oraz odwołanie do pakietu NuGet Aspose.Cells. Jeśli nigdy wcześniej nie używałeś Aspose, nie martw się — pokażemy **jak używać Aspose** od podstaw.

---

![Create conditional formatting example](https://example.com/images/create-conditional-formatting.png "Zrzut ekranu pokazujący formatowanie warunkowe w wygenerowanym pliku Excel")

*Tekst alternatywny obrazu: przykład formatowania warunkowego w skoroszycie Excel wygenerowanym przy użyciu Aspose.Cells.*

## Jak utworzyć skoroszyt Excel przy użyciu Aspose.Cells

Na początek potrzebujesz obiektu workbook, z którym będziesz pracować. Aspose.Cells robi to w jednej linii.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

Dlaczego zmieniamy nazwę arkusza? Jasna nazwa (np. **Scores**) ułatwia późniejsze odwołania, szczególnie gdy udostępniasz plik użytkownikom nietechnicznym.  

Teraz, gdy skoroszyt istnieje, wypełnijmy kolumnę A losowymi wynikami.

## Jak wypełnić dane – tworzenie losowych wyników

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

Krótka uwaga: `PutValue` automatycznie wykrywa typ danych, więc nie musisz rzutować na `int`. Pętla zaczyna się od `i = 0`, ale zapisuje do wiersza `i + 1`, ponieważ wiersze w Excelu są numerowane od 1, a kolekcja `Cells` od 0.

## Jak ustawić tło komórki dla wysokich wyników

Teraz **utworzymy formatowanie warunkowe**, które pomaluje każdy wynik ≥ 80 jasnym zielonym odcieniem.

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

Właściwość `ForegroundColor` kontroluje kolor wypełnienia, natomiast `Pattern = BackgroundType.Solid` mówi Excelowi, aby użył jednolitego wypełnienia zamiast gradientu lub wzoru. To jest sedno **jak ustawić tło komórki** w oparciu o progowy próg liczbowy.

## Jak rankingować komórki i podświetlić top‑3

Rankingowanie jest nieco trudniejsze, ponieważ potrzebujemy formuły, która ocenia każdą komórkę względem całego zakresu. Aspose.Cells pozwala używać tej samej składni formuł Excel, którą wpisujesz w UI.

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

Dlaczego w formule jest `A2`? Aspose ocenia formułę względnie do każdej komórki w zakresie, więc `A2` automatycznie przeskakuje do `A3`, `A4` itd., gdy reguła jest stosowana wiersz po wierszu. Funkcja `RANK` zwraca pozycję wartości w określonym zakresie, a część `<=3` zapewnia, że tylko trzy najwyższe wyniki otrzymają złote wypełnienie.

## Jak zapisać skoroszyt

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

Zastąp `YOUR_DIRECTORY` ścieżką bezwzględną lub względną, do której aplikacja ma prawo zapisu. Po uruchomieniu metody otwórz plik w Excelu i zobaczysz:

- Jasnozielone komórki dla każdego wyniku ≥ 80  
- Złote komórki dla trzech najwyższych wyników, niezależnie od tego, czy również są ≥ 80  

To pełny **pipeline tworzenia formatowania warunkowego**.

---

## Pełny, gotowy do uruchomienia przykład

Oto cała metoda jeszcze raz, gotowa do skopiowania i wklejenia do aplikacji konsolowej lub dowolnej klasy C#:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### Oczekiwany rezultat

Po otwarciu `Scores_ConditionalFormatting.xlsx`:

- Komórki z wartościami **80** lub wyższymi świecą jasnozielonym kolorem.  
- Trzy najwyższe liczby (nawet jeśli są poniżej 80) mają **złote** tło.  
- Wszystkie pozostałe komórki zachowują domyślne białe tło.

Ten wizualny sygnał natychmiast informuje menedżera, kto jest najlepszym wykonawcą, bez ręcznego sortowania.

---

## Często zadawane pytania i przypadki brzegowe

**Co zrobić, jeśli potrzebuję więcej niż trzy najlepsze wyniki?**  
Po prostu zmień część formuły `<=3` na `<=5` (lub dowolną liczbę). Reguła automatycznie się dostosuje.

**Czy mogę zastosować wiele zakresów formatowania?**  
Oczywiście. Wywołaj ponownie `sheet.ConditionalFormattings.Add` z innym zakresem, a następnie dodaj warunki do nowego obiektu `ConditionalFormatting`.

**A co ze starszymi wersjami Excela?**  
Aspose.Cells domyślnie zapisuje w nowoczesnym formacie `.xlsx`, który jest kompatybilny z Excel 2007 i nowszymi. Jeśli potrzebujesz `.xls`, przekaż `SaveFormat.Excel97To2003` do metody `Save`.

**Czy istnieje wpływ na wydajność przy dużych arkuszach?**  
Formatowanie warunkowe jest przechowywane jako metadane, więc nie wpływa znacząco na rozmiar pliku. Jednak generowanie setek tysięcy wierszy może zwiększyć zużycie pamięci — rozważ przetwarzanie w partiach.

---

## Kolejne kroki

Teraz, gdy opanowałeś **tworzenie formatowania warunkowego**, możesz zgłębić:

- **Jak tworzyć wykresy Excel** programowo (kolejny klejnot Aspose.Cells)  
- **Jak ustawić tło komórki** w oparciu o wartości tekstowe (np. „Pass/Fail”)  
- **Jak używać Aspose.Cells do walidacji danych** i list rozwijanych  

Każdy z tych tematów opiera się na tych samych podstawach, które właśnie poznałeś, więc poczujesz się jak w domu.

---

## Podsumowanie

Przeszliśmy razem kompletny, end‑to‑end przykład, jak **tworzyć formatowanie warunkowe** w skoroszycie Excel przy użyciu Aspose.Cells. Od inicjalizacji skoroszytu, wypełniania danych, **ustawiania tła komórki**, rankingowania najlepszych wykonawców, po ostateczne zapisanie pliku — każdy krok został omówiony z myślą o **rankingowaniu komórek** i **korzystaniu z Aspose**.  

Wypróbuj kod, zmodyfikuj progi i zobacz, jak szybko możesz generować eleganckie raporty dla dowolnego scenariusza biznesowego. Masz własny pomysł, którym chcesz się podzielić? zostaw komentarz poniżej — miłego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Automate Excel Conditional Formatting Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java&#58; A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}