---
category: general
date: 2026-03-27
description: Jak powiązać dane w C# przy użyciu Aspose.Cells – dowiedz się, jak zapisać
  skoroszyt jako XLSX, dodać wykres i wyeksportować Excel z wykresem w kilka minut.
draft: false
keywords:
- how to bind data
- save workbook as xlsx
- create excel workbook c#
- how to add chart
- export excel with chart
language: pl
og_description: Jak powiązać dane w C# z Aspose.Cells. Ten przewodnik pokazuje, jak
  zapisać skoroszyt jako XLSX, dodać wykres i wyeksportować Excel z wykresem.
og_title: Jak powiązać dane w C# – Utwórz skoroszyt Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Jak powiązać dane w C# – Utwórz skoroszyt Excel
url: /pl/net/excel-data-import-export/how-to-bind-data-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak powiązać dane w C# – Utwórz skoroszyt Excel

Zastanawiałeś się kiedyś **jak powiązać dane** z wykresem w C#, nie tracąc włosów? Nie jesteś jedyny. Wielu programistów napotyka trudności, gdy muszą programowo generować pliki Excel, które naprawdę *wyglądają* tak, jakby je tworzyli ręcznie.  

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który tworzy skoroszyt Excel, wypełnia go danymi, powiązuje te dane z wykresem Waterfall i ostatecznie zapisuje plik jako `.xlsx`. Po zakończeniu dokładnie będziesz wiedział, jak **zapisz skoroszyt jako XLSX**, **jak dodać wykres** do arkusza oraz jak **wyeksportuj Excel z wykresem** do dalszego raportowania.

> **Wymagania wstępne** – Potrzebujesz Aspose.Cells dla .NET (bezpłatna wersja próbna działa dobrze) oraz środowiska programistycznego .NET, takiego jak Visual Studio 2022. Nie są wymagane żadne inne pakiety NuGet.

---

## Co obejmuje ten przewodnik

- **Utwórz skoroszyt Excel C#** – skonfiguruj nowy `Workbook` i arkusz.  
- **Jak powiązać dane** – mapuj swoje numeryczne serie i etykiety kategorii na źródło danych wykresu.  
- **Jak dodać wykres** – wstaw wykres Waterfall i skonfiguruj jego tytuł.  
- **Zapisz skoroszyt jako XLSX** – zapisz plik na dysku, aby każdy mógł otworzyć go w Excelu.  
- **Wyeksportuj Excel z wykresem** – gotowy produkt to w pełni funkcjonalny skoroszyt, który możesz udostępnić.

Jeśli czujesz się komfortowo z podstawową składnią C#, uznasz to za bułkę z masłem. Zanurzmy się.

---

## Krok 1: Utwórz skoroszyt Excel w C#  

Na początek – potrzebujemy obiektu skoroszytu, z którym będziemy pracować. Pomyśl o klasie `Workbook` jako o pustym notesie, który później wypełnisz stronami (arkuszami) i zawartością.

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class WaterfallDemo
{
    static void Main()
    {
        // Initialize a new workbook – this is your blank Excel file.
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0). It’s already created for us.
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Wskazówka:** Jeśli kiedykolwiek potrzebujesz wielu arkuszy, po prostu wywołaj `workbook.Worksheets.Add()` i zachowaj referencję do każdego nowego `Worksheet`.

---

## Krok 2: Wypełnij arkusz kategoriami i wartościami  

Teraz **create excel workbook c#**‑style data. Przykład używa klasycznego scenariusza Waterfall: start, revenue, cost, profit i end.

```csharp
        // Add header labels.
        worksheet.Cells["A1"].PutValue("Category");
        worksheet.Cells["B1"].PutValue("Amount");

        // Sample data – you can replace these with your own source (database, API, etc.).
        string[] categoryLabels = { "Start", "Revenue", "Cost", "Profit", "End" };
        double[] values = { 0, 150, -70, 0, 80 };

        // Fill rows 2‑6 with the data.
        for (int i = 0; i < categoryLabels.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(categoryLabels[i]); // Column A
            worksheet.Cells[i + 1, 1].PutValue(values[i]);       // Column B
        }
```

Dlaczego wstawiamy `0` dla „Start” i „Profit”? W wykresie Waterfall te zera działają jako *łączniki*, które zapewniają prawidłowy przepływ wizualny. Jeśli je pominiesz, wykres będzie wyglądał na zepsuty.

---

## Krok 3: Jak dodać wykres – Wstaw wykres Waterfall  

Mając dane na miejscu, czas **jak dodać wykres**. Aspose.Cells robi to tak łatwo, jak wywołanie `Charts.Add`.

```csharp
        // Insert a Waterfall chart starting at row 7, column 0 and spanning to row 25, column 10.
        int chartIndex = worksheet.Charts.Add(ChartType.Waterfall, 7, 0, 25, 10);
        Chart waterfallChart = worksheet.Charts[chartIndex];

        // Give the chart a meaningful title.
        waterfallChart.Title.Text = "Quarterly Waterfall";
```

Współrzędne `(7,0,25,10)` definiują lewy‑górny oraz prawy‑dolny komórkę ramki wykresu. Dostosuj je do swojego układu.

---

## Krok 4: Jak powiązać dane – Połącz serie i kategorie  

Oto serce tego samouczka: **jak powiązać dane** do wykresu. Metoda `NSeries.Add` przyjmuje zakres wartości Y, natomiast `CategoryData` wskazuje etykiety osi X.

```csharp
        // Bind the numeric series (values) – the second parameter “true” tells Aspose to treat it as a series.
        waterfallChart.NSeries.Add("B2:B6", true);

        // Bind the category (X‑axis) labels.
        waterfallChart.NSeries.CategoryData = "A2:A6";
```

Zauważ, że odwołujemy się do tych samych komórek, które wypełniliśmy wcześniej (`A2:A6` dla kategorii, `B2:B6` dla kwot). Jeśli kiedykolwiek zmienisz układ danych, po prostu zaktualizuj te zakresy odpowiednio.

---

## Krok 5: Zapisz skoroszyt jako XLSX – Zapisz plik  

Na koniec **zapisz skoroszyt jako XLSX**. Metoda `Save` automatycznie wybiera właściwy format na podstawie rozszerzenia pliku.

```csharp
        // Save the workbook to disk. Replace YOUR_DIRECTORY with an actual path.
        workbook.Save("YOUR_DIRECTORY/WaterfallChart.xlsx");
    }
}
```

Kiedy otworzysz `WaterfallChart.xlsx` w Excelu, zobaczysz ładnie wyrenderowany wykres Waterfall, który odzwierciedla wprowadzone dane. To część **wyeksportuj Excel z wykresem** zakończona.

---

## Oczekiwany wynik  

- **Plik Excel:** `WaterfallChart.xlsx` znajdujący się w folderze, który określiłeś.  
- **Układ arkusza:** Kolumna A zawiera kategorie, Kolumna B zawiera kwoty, a wykres znajduje się pod tabelą.  
- **Wygląd wykresu:** Wykres Waterfall zatytułowany „Quarterly Waterfall” z pięcioma kolumnami reprezentującymi Start, Revenue, Cost, Profit i End.  

![przykład wykresu waterfall powiązanie danych](waterfall_chart.png "Wykres Waterfall wygenerowany przez Aspose.Cells")

*Tekst alternatywny obrazu zawiera główne słowo kluczowe, pomagając zarówno SEO, jak i cytowaniu przez AI.*

---

## Częste pytania i przypadki brzegowe  

### Co jeśli moje źródło danych jest dynamiczne?  
Zastąp statyczne tablice pętlą, która odczytuje dane z bazy danych lub API. Dopóki zapisujesz wartości w tym samym zakresie komórek, kod powiązania pozostaje niezmieniony.

### Czy mogę zmienić typ wykresu?  
Oczywiście. Zamień `ChartType.Waterfall` na `ChartType.Column`, `ChartType.Line` itd. Pamiętaj tylko, aby dostosować dane serii, jeśli nowy wykres wymaga innego układu.

### Jak ustawić kolory wykresu?  
Użyj `waterfallChart.NSeries[0].Format.Fill.ForeColor = Color.Yellow;` (lub dowolnego `System.Drawing.Color`). Jest to przydatne, gdy chcesz, aby kolumna „Profit” wyróżniała się.

### Co jeśli muszę wyeksportować do PDF zamiast XLSX?  
Wywołaj `workbook.Save("Report.pdf", SaveFormat.Pdf);`. Wykres zostanie automatycznie wyrenderowany w pliku PDF.

---

## Wskazówki dla kodu gotowego do produkcji  

- **Dispose objects** – Owiń `Workbook` w blok `using`, jeśli używasz .NET Core, aby szybko zwolnić zasoby.  
- **Path handling** – Użyj `Path.Combine(Environment.CurrentDirectory, "WaterfallChart.xlsx")`, aby uniknąć ręcznego wpisywania separatorów.  
- **Error handling** – Przechwyć `Exception` wokół `Save`, aby wcześnie wykryć problemy z uprawnieniami lub brakiem miejsca na dysku.  
- **Version check** – Aspose.Cells 23.10+ wprowadził ulepszone wsparcie dla Waterfall; upewnij się, że używasz najnowszej wersji, aby uzyskać najlepsze rezultaty.

---

## Zakończenie  

Masz teraz kompletny przykład od początku do końca, który demonstruje **jak powiązać dane** w C#, **create excel workbook c#**, **jak dodać wykres**, **zapisz skoroszyt jako XLSX**, oraz **wyeksportuj Excel z wykresem**. Kod jest gotowy do wstawienia w dowolny projekt .NET, a koncepcje skalują się do większych zestawów danych i różnych typów wykresów.

Gotowy na kolejny krok? Spróbuj dodać wiele serii, eksperymentuj z wykresami skumulowanymi lub zautomatyzuj generowanie miesięcznych raportów, które będą wysyłane e‑mailem do interesariuszy. Nie ma granic, gdy opanujesz podstawy automatyzacji Excel przy użyciu Aspose.Cells.

Szczęśliwego kodowania i niech Twoje arkusze kalkulacyjne zawsze renderują się perfekcyjnie!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}