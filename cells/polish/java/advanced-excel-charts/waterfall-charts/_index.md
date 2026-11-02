---
date: 2026-09-02
description: Dowiedz się, jak utworzyć wykres wodospadowy w Excelu w Javie przy użyciu
  Aspose.Cells, ustawić zakres danych wykresu, dostosować etykiety i wyeksportować
  do formatu XLSX.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: Wykresy wodospadowe
og_description: Utwórz wykres wodospadowy w Excelu przy użyciu Aspose.Cells dla Javy
  – ustaw zakres danych wykresu, dodaj etykiety danych i wyeksportuj do formatu XLSX
  w kilku krokach.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Utwórz wykres wodospadowy w Excelu przy użyciu Aspose.Cells dla Javy
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Utwórz wykres wodospadowy w Excelu przy użyciu Aspose.Cells dla Javy
url: /pl/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wykresy wodospadowe

## Wprowadzenie do wykresów wodospadowych przy użyciu Aspose.Cells for Java

W tym samouczku nauczysz się, jak **utworzyć wykres wodospadowy w Excelu** i **ustawić zakres danych wykresu** przy użyciu Aspose.Cells for Java. Wykresy wodospadowe zamieniają serię liczb dodatnich i ujemnych w przejrzystą historię wizualną, co czyni je idealnymi do sprawozdań finansowych, przeglądów wyników sprzedaży i wszelkich scenariuszy, w których trzeba zobaczyć, jak poszczególne pozycje przyczyniają się do sumy.

## Szybkie odpowiedzi
- **Czym jest wykres wodospadowy?** Wizualizacja, która pokazuje, jak początkowa wartość jest zwiększana i zmniejszana przez serię wartości pośrednich, kończąc się ostatecznym sumą.  
- **Która biblioteka jest używana?** Aspose.Cells for Java.  
- **Czy potrzebuję licencji?** Darmowa wersja próbna działa w środowisku deweloperskim; licencja komercyjna jest wymagana w produkcji.  
- **Czy mogę zapisać plik jako XLSX?** Tak – użyj `workbook.save("FileName.xlsx")`.  
- **Czy jest odpowiedni do wizualizacji danych w Javie?** Zdecydowanie; Aspose.Cells oferuje bogate funkcje wykresów bez konieczności instalacji Office.

## Czym jest wykres wodospadowy?
Wykres wodospadowy wyświetla kolejno dodatnie i ujemne wkłady do wartości początkowej, pomagając zrozumieć, jak każdy element wpływa na ostateczny wynik. Poprzez wizualizację zysków i strat obok siebie, sprawia, że złożone przepływy finansowe są natychmiast czytelne.

## Dlaczego używać Aspose.Cells for Java do dodania wykresu wodospadowego?
Aspose.Cells pozwala generować wykresy Excel na dowolnym serwerze, w potoku CI lub na komputerze bez konieczności posiadania Microsoft Excel. Obsługuje **ponad 15 formatów wyjściowych** (XLSX, PDF, HTML, CSV i inne), przetwarza skoroszyty z **ponad 500 wierszami** w mniej niż sekundę i zapewnia programistyczną kontrolę nad każdym elementem wykresu — od kolorów po etykiety danych.

## Wymagania wstępne

Zanim przejdziemy do kodu, upewnij się, że spełniasz następujące wymagania:

- Aspose.Cells for Java: Musisz mieć zainstalowane Aspose.Cells for Java. Możesz je pobrać ze strony wydania Aspose.Cells for Java: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Środowisko programistyczne Java: Upewnij się, że masz zainstalowaną Javę w systemie oraz gotowe narzędzie budowania (Maven/Gradle).

Teraz rozpocznijmy tworzenie wykresu wodospadowego krok po kroku.

## Jak ustawić zakres danych wykresu wodospadowego w Javie
Załaduj nowy skoroszyt, wypełnij go danymi, dodaj obiekt `Chart`, określ zakres serii i na końcu zapisz plik. Ten proces jest prosty: tworzysz skoroszyt, wypełniasz komórki kategoriami i wartościami, tworzysz wykres, wiążesz zakresy danych, a następnie eksportujesz skoroszyt. Wynikiem jest w pełni funkcjonalny wykres wodospadowy gotowy do użycia w raportach lub pulpitach nawigacyjnych.

### Krok 1: import Aspose.Cells
Pakiet `com.aspose.cells` zawiera wszystkie klasy potrzebne do manipulacji plikami Excel, w tym tworzenie skoroszytów, obsługę arkuszy i generowanie wykresów.

### Krok 2: inicjalizacja skoroszytu i arkusza
**Workbook** reprezentuje plik Excel, a **Worksheet** jest pojedynczym arkuszem w tym pliku. Tworzenie tych obiektów zapewnia płótno zarówno dla surowych danych, jak i wykresu.

### Krok 3: wprowadzenie danych
Kolumna A zawiera etykiety kategorii, natomiast kolumna B zawiera wartości liczbowe dla wykresu wodospadowego. Ten układ odpowiada typowemu przepływowi zysk‑i‑strata używanemu w analizie finansowej.

### Krok 4: utworzenie wykresu wodospadowego
Obiekt **Chart** tworzy reprezentację wizualną; ustawienie jego typu na `ChartType.WATERFALL` konfiguruje go jako wykres wodospadowy. Użyj metody `add`, aby ustawić zakres danych wykresu dla serii (`"B2:B6"`), i połącz oś kategorii z `"A2:A6"`.

### Krok 5: zapisanie skoroszytu
Zapisanie skoroszytu zapisuje wykres i dane w określonym formacie pliku. Wywołaj `workbook.save("WaterfallChart.xlsx")`, aby wygenerować plik XLSX, lub zmień parametr formatu, aby wyeksportować do PDF, CSV lub HTML.

## Typowe problemy i rozwiązania
- **Wykres jest pusty** – Sprawdź, czy odwołania do zakresu danych (`B2:B6` i `A2:A6`) odpowiadają rzeczywistym komórkom zawierającym Twoje wartości i kategorie.  
- **Wartości ujemne nie wyświetlają się prawidłowo** – Upewnij się, że typ serii jest ustawiony na `ChartType.WATERFALL`; inne typy wykresów traktują wartości ujemne inaczej.  
- **Plik nie otwiera się w Excelu** – Użyj najnowszej wersji Aspose.Cells i potwierdź, że rozszerzenie pliku odpowiada formatowi (`.xlsx` dla Excela).

## Najczęściej zadawane pytania

### Jak mogę dostosować wygląd mojego wykresu wodospadowego?
Możesz modyfikować właściwości, takie jak `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())`, aby zmienić kolory słupków, włączyć etykiety danych za pomocą `setShowDataLabels(true)` oraz dostosować tytuły osi poprzez `getCategoryAxis().setTitle("Stage")`. Dokumentacja API Aspose.Cells zawiera pełną listę opcji konfigurowalnych.

### Czy mogę utworzyć wiele wykresów wodospadowych w tym samym arkuszu?
Tak. Po dodaniu pierwszego wykresu, powtórz kroki tworzenia wykresu z innym zakresem danych i nowym obiektem `Chart`. Każdy wykres jest niezależny i może być umieszczony w dowolnym miejscu arkusza.

### Czy Aspose.Cells jest kompatybilny z różnymi środowiskami programistycznymi Java?
Zdecydowanie. Biblioteka działa z Eclipse, IntelliJ IDEA, NetBeans oraz każdym systemem budowania obsługującym Maven lub Gradle. Nie są wymagane dodatkowe wtyczki.

### Czy mogę dodać dodatkowe serie danych do mojego wykresu wodospadowego?
Możesz dodać więcej serii, wywołując `chart.getNSeries().add("C2:C6", true)` i konfigurować każdą serię osobno. Pozwala to porównać wiele scenariuszy obok siebie.

### Gdzie mogę znaleźć więcej zasobów i przykładów dla Aspose.Cells for Java?
Przeglądaj pełną dokumentację w odniesieniu do API Aspose.Cells Java: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## FAQ

**Q: Jak ustawić zakres danych wykresu wodospadowego finansowego?**  
A: Użyj metody `add` na serii wykresu, przekazując zakres komórek zawierający Twoje wartości, np. `"B2:B6"`.

**Q: Czy mogę wyeksportować skoroszyt do PDF zamiast XLSX?**  
A: Tak, wywołaj `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);`, aby wygenerować wersję PDF.

**Q: Co zrobić, jeśli potrzebuję utworzyć wykres wodospadowy z większą liczbą kategorii?**  
A: Rozszerz zakres danych zarówno w kolumnie wartości, jak i w kolumnie kategorii, a następnie odpowiednio zaktualizuj wywołania `add` i `setCategoryData`.

**Q: Czy istnieje sposób na automatyczne formatowanie słupków dodatnich i ujemnych?**  
A: Przejdź przez kolekcję `Series` i ustaw kolor `FillFormat` w zależności od znaku każdej wartości; Aspose.Cells umożliwia programowe stosowanie formatowania warunkowego.

**Q: Czy Aspose.Cells obsługuje dynamiczne aktualizacje danych dla wykresów?**  
A: Tak. Po modyfikacji wartości komórek, po prostu ponownie zapisz skoroszyt — wykres automatycznie odzwierciedli nowe dane.

---

**Ostatnia aktualizacja:** 2026-09-02  
**Testowano z:** Aspose.Cells for Java (latest)  
**Autor:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## Powiązane samouczki

- [Dostosuj etykiety danych wykresu Excel przy użyciu Aspose.Cells for Java: Przewodnik krok po kroku](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Dodaj etykiety danych do wykresu Excel za pomocą Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Jak tworzyć i eksportować wykresy w Javie przy użyciu Aspose.Cells: Kompletny przewodnik](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}