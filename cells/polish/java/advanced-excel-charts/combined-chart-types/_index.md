---
date: 2026-09-02
description: Dowiedz się, jak wyeksportować wykres do PNG, dodać serię danych, połączyć
  wykres liniowo-słupkowy, zapisać skoroszyt jako XLSX oraz dodać legendę wykresu
  przy użyciu Aspose.Cells for Java.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Eksport wykresu do PNG i dodanie serii danych do wykresu łączonego
og_description: Eksport wykresu do PNG przy użyciu Aspose.Cells for Java, połączenie
  wykresu liniowego i słupkowego, dodanie serii danych oraz zapis skoroszytu jako
  XLSX w jednym samouczku.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Eksport wykresu do PNG i dodanie serii danych do wykresu łączonego
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: Eksport wykresu do PNG i dodanie serii danych do wykresu łączonego
url: /pl/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksport wykresu do PNG i dodanie serii danych dla wykresu łączonego

W tym samouczku **dodasz serię danych** do skoroszytu Excel, **połączysz elementy wykresu liniowego i słupkowego**, oraz nauczysz się **eksportować wykres do PNG** przy użyciu Aspose.Cells for Java. Przejdziemy przez każdy krok — od przygotowania skoroszytu, dodania wykresu do arkusza, dostosowania legendy, po **zapisanie skoroszytu jako XLSX** i wygenerowanie obrazu PNG wykresu. Po zakończeniu będziesz mieć gotowy wykres łączony, który możesz osadzić w raportach lub dashboardach.

## Szybkie odpowiedzi
- **Która biblioteka tworzy wykresy łączone?** Aspose.Cells for Java.  
- **Jak dodać serię danych?** Wywołaj `chart.getNSeries().add(...)` z odpowiednim zakresem.  
- **Jak mogę wyeksportować wykres do PNG?** Użyj `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **W jakim formacie pliku mogę zapisać skoroszyt?** Standardowy `.xlsx` (zapisz skoroszyt jako XLSX).  
- **Czy potrzebuję licencji do produkcji?** Tak — wymagana jest ważna licencja Aspose.Cells do wdrożeń produkcyjnych.

## Czym jest eksport wykresu do PNG w Aspose.Cells?
Eksport wykresu do PNG tworzy obraz rastrowy wykresu Excel, który może być wyświetlany na stronach internetowych, w raportach lub e‑mailach bez konieczności posiadania aplikacji Excel. Metoda ta zachowuje dokładny układ wizualny, kolory i znaczniki danych, generując przenośny plik obrazu.

## Dlaczego tworzyć łączony wykres liniowo‑słupkowy?
Łączony wykres liniowo‑słupkowy pozwala wyświetlać różne zestawy danych przy użyciu odmiennych reprezentacji wizualnych (np. seria liniowa nad serią słupkową) w jednej perspektywie. To podejście jest idealne do porównywania trendów z sumami, podkreślania korelacji lub dostarczania bogatszych wniosków przy zachowaniu niewielkiego rozmiaru wizualnego.

## Wymagania wstępne
- Java Development Kit (JDK) 8 lub wyższy  
- Biblioteka Aspose.Cells for Java (pobierz z linku poniżej)  
- Podstawowa znajomość składni Java i pojęć Excel  

## Rozpoczęcie

Najpierw pobierz bibliotekę Aspose.Cells for Java z oficjalnej strony:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Po dodaniu pliku JAR do classpath projektu możesz rozpocząć budowanie wykresu.

### Krok 1: importuj klasy aspose.cells
`Workbook` jest podstawowym obiektem Aspose.Cells, który reprezentuje cały plik Excel w pamięci.  
```java
import com.aspose.cells.*;
```

### Krok 2: utwórz nowy skoroszyt
`Worksheet` reprezentuje pojedynczy arkusz w obrębie `Workbook` i zapewnia dostęp do komórek, wierszy i wykresów.  
```java
Workbook workbook = new Workbook();
```

### Krok 3: uzyskaj dostęp do pierwszego arkusza
`Chart` jest obiektem, który przechowuje wszystkie ustawienia wykresu, serie i opcje renderowania.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Krok 4: dodaj obiekt łączonego wykresu do arkusza  
Zaczniemy od wykresu liniowego, a później dodamy serię słupkową, aby uzyskać efekt **łączonego wykresu liniowo‑słupkowego**.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Dodawanie danych do wykresu

Teraz, gdy kontener wykresu istnieje, musimy go zasilić danymi.

### Krok 5: zdefiniuj zakresy danych i dodaj serię danych
`NSeries` jest kolekcją przechowującą każdą serię danych wykresu. Dodanie serii łączy zakres komórek z wykresem.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** Pierwszy parametr (`"A1:A5"`) to zakres pierwszej serii, a drugi (`"B1:B5"`) tworzy drugą serię, która zostanie połączona z pierwszą.

### Krok 6: ustaw dane kategorii (oś X)
`CategoryAxis` reprezentuje oś poziomą wykresu, kontrolując etykiety wyświetlane wzdłuż osi X.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Dostosowywanie wykresu

Dobry wykres opowiada historię. Dodajmy tytuły, etykiety osi i czytelną legendę.

### Krok 7: ustaw etykiety osi wykresu i tytuł
`Title` ustawia główny tytuł wykresu, a obiekty `Axis` reprezentują osie X i Y.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Krok 8: dodaj legendę wykresu i dostosuj jej pozycję
`Legend` kontroluje położenie i wygląd legendy serii w wykresie.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Zapis i eksport wykresu

Po dostosowaniu będziesz chciał **zapisać skoroszyt jako XLSX** i także wygenerować obraz.

### Krok 9: zapisz skoroszyt jako plik Excel (XLSX)
`Workbook.save` zapisuje skoroszyt w pamięci do pliku w określonym formacie.  
```java
workbook.save("CombinedChart.xlsx");
```

### Krok 10: wyeksportuj wykres do PNG
`Chart.toImage` renderuje wykres jako plik obrazu w wybranym formacie.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Metoda `chart.toImage` **generuje obrazy wykresów Excel**, które mogą być używane na stronach internetowych, w raportach lub e‑mailach.

## Typowe problemy i rozwiązywanie

| Problem | Rozwiązanie |
|---------|-------------|
| **Brak danych** | Sprawdź, czy zakresy komórek (`A1:A5`, `B1:B5`, `C1:C5`) rzeczywiście zawierają dane przed utworzeniem wykresu. |
| **Legenda nachodzi na wykres** | Ustaw `chart.getLegend().setOverlay(false)` lub przenieś legendę na inną pozycję (np. `RIGHT`). |
| **Plik obrazu jest pusty** | Upewnij się, że wykres ma przynajmniej jedną serię i że `chart.toImage` jest wywoływane po wszystkich dostosowaniach. |
| **Zapis zgłasza wyjątek** | Sprawdź, czy masz uprawnienia do zapisu w docelowym katalogu oraz czy plik nie jest otwarty w Excelu. |

## Najczęściej zadawane pytania

**Q: Jak zainstalować Aspose.Cells for Java?**  
A: Pobierz plik JAR z oficjalnej strony i dodaj go do classpath projektu. Link do pobrania: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Czy mogę tworzyć inne typy wykresów oprócz liniowego i słupkowego?**  
A: Tak, Aspose.Cells obsługuje wykresy słupkowe, kołowe, punktowe, powierzchniowe i wiele innych. Zapoznaj się z dokumentacją API, aby zobaczyć pełną listę.

**Q: Czy licencja jest wymagana do użytku produkcyjnego?**  
A: Tak, do wdrożeń produkcyjnych wymagana jest ważna licencja Aspose.Cells. Dostępna jest bezpłatna wersja próbna do oceny.

**Q: Jak mogę zmienić kolory każdej serii?**  
A: Użyj `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (lub podobnej metody) po dodaniu serii.

**Q: Gdzie mogę znaleźć więcej przykładów kodu?**  
A: Szczegółowa dokumentacja i dodatkowe przykłady są dostępne na stronie referencyjnej Aspose: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

---

**Ostatnia aktualizacja:** 2026-09-02  
**Testowano z:** Aspose.Cells for Java najnowsza wersja  
**Autor:** Aspose

## Powiązane samouczki

- [Jak dodać etykiety do wykresów Excel przy użyciu Aspose.Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Jak utworzyć wykres Excel z linią trendu i wyeksportować do obrazu przy użyciu Aspose.Cells for Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Eksport wykresów Excel do PDF przy użyciu Aspose.Cells for Java: Przewodnik po niestandardowych rozmiarach stron](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}