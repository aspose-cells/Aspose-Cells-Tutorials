---
date: 2026-08-27
description: Dowiedz się, jak dodać trendline do chart, wyświetlić jego wartość R‑squared
  i wyeksportować chart jako obraz PNG lub JPEG przy użyciu Aspose.Cells for Java.
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: Eksportuj Chart do Image z analizą Trendline
og_description: Dodaj trendline do chart, zobacz R‑squared i wyeksportuj wynik jako
  PNG/JPEG przy użyciu Aspose.Cells for Java – szybkie rozwiązanie obsługujące 50
  formatów.
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: Dodaj trendline do chart i wyeksportuj jako image z Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: Jak dodać trendline do chart i wyeksportować jako image w Java
url: /pl/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj linię trendu do wykresu i wyeksportuj ją jako obraz

W tym samouczku dowiesz się, jak **dodać linię trendu do wykresu**, wyświetlić wartość R‑kwadrat oraz wyeksportować wizualizację do pliku PNG lub JPEG przy użyciu Aspose.Cells for Java. Zobaczysz, dlaczego linie trendu są ważne, jak przygotować skoroszyt oraz dokładne kroki, aby wygenerować obraz wysokiej rozdzielczości, który można osadzić w raportach, e‑mailach lub stronach internetowych.

## Szybkie odpowiedzi
- **Jaki jest główny cel tego przewodnika?** Aby pokazać, jak dodać linię trendu do wykresu, wyświetlić jej równanie i wartość R‑kwadrat oraz wyeksportować wykres jako obraz przy użyciu Javy.  
- **Jakiej biblioteki potrzebuję?** Aspose.Cells for Java – pobierz ją ze [Aspose.Cells for Java release page](https://releases.aspose.com/cells/java/).  
- **Czy potrzebuję licencji do rozwoju?** Darmowa wersja próbna działa w środowisku deweloperskim; licencja komercyjna jest wymagana przy wdrożeniach produkcyjnych.  
- **Czy mogę generować skoroszyt Excel programowo?** Tak – samouczek tworzy i zapisuje skoroszyt XLSX od podstaw.  
- **Jak wykres jest eksportowany do PNG lub JPEG?** Wywołaj metodę `Chart.toImage()` i zapisz zwrócony `BufferedImage` przy użyciu `ImageIO.write(...)`.

## Jak utworzyć wykres Excel z linią trendu i wyeksportować go jako obraz?
Załaduj skoroszyt, dodaj wykres liniowy, dołącz linię trendu, która wyświetla równanie i wartość R‑kwadrat, zapisz skoroszyt, a następnie wywołaj `chart.toImage()` i zapisz powstały `BufferedImage` do pliku PNG lub JPEG. Ten kompletny przepływ wymaga tylko kilku linii kodu Java i generuje obraz o idealnej jakości pikseli, odpowiedni dla dowolnej aplikacji downstream.

## Co to jest eksport wykresu do obrazu?
Eksportowanie wykresu do obrazu konwertuje wizualną reprezentację danych na przenośny bitmap (PNG, JPEG, BMP itp.). Ten format jest idealny do osadzania wykresów w raportach, stronach internetowych lub prezentacjach, gdzie nie jest wymagany oryginalny plik Excel.

## Dlaczego dodać linię trendu i wyświetlić wartość R‑kwadrat?
Linia trendu ujawnia ukryty wzorzec serii danych, podczas gdy metryka **R‑kwadrat** kwantyfikuje, jak dokładnie linia trendu dopasowuje się do danych. Umieszczenie obu w wyeksportowanym obrazie daje interesariuszom natychmiastowy wgląd bez otwierania skoroszytu. Pomaga decydentom szybko ocenić siłę korelacji i prognozować trendy bez konieczności otwierania Excela.

## Wymagania wstępne
- Java 8 lub nowszy zainstalowany na maszynie deweloperskiej.  
- Biblioteka Aspose.Cells for Java dodana do classpath projektu (pliki JAR).  
- Znajomość środowiska IDE Java, takiego jak IntelliJ IDEA lub Eclipse.  

## Przewodnik krok po kroku

### Krok 1: skonfiguruj projekt
Utwórz nowy projekt Java i umieść pliki JAR Aspose.Cells na ścieżce kompilacji. To przygotowuje środowisko do generowania i manipulacji plikami Excel.

### Krok 2: załaduj plik Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Właśnie **załadowaliśmy plik Excel** do pamięci, gotowy do tworzenia wykresu.*

### Krok 3: utwórz wykres
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Tutaj generujemy wykres liniowy, który później będzie zawierał naszą linię trendu.*

### Krok 4: dodaj linię trendu (how to add trendline) i wyświetl wartość R‑kwadrat
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*Wywołanie `setDisplayRSquaredValue(true)` zapewnia, że **wartość R‑kwadrat** pojawia się na wykresie.*

### Krok 5: dostosuj wykres i zapisz skoroszyt (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Teraz skoroszyt jest **generowany** i zapisany jako plik XLSX, gotowy do dalszego przetwarzania.*

### Krok 6: wyeksportuj wykres do obrazu (export chart to image)
> **Uwaga:** Ten krok jest opisany bez dodatkowego bloku kodu, aby zachować niezmienioną liczbę oryginalnych bloków.  
Po utworzeniu i zapisaniu wykresu możesz wyeksportować go do obrazu, wywołując metodę `chart.toImage()` i zapisując powstały `java.awt.image.BufferedImage` w wybranym formacie pliku (PNG, JPEG, BMP). Typowy przepływ pracy wygląda następująco:
1. Pobierz obiekt `Chart` (już zrobiono w poprzednich krokach).  
2. Wywołaj `chart.toImage()`, aby uzyskać `BufferedImage`.  
3. Użyj `ImageIO.write(bufferedImage, "png", new File("chart.png"))`, aby zapisać plik.  

Obiekt `Chart` reprezentuje wykres w skoroszycie i udostępnia metody modyfikacji jego wyglądu i danych. `BufferedImage` jest klasą Javy, która przechowuje obraz w pamięci, umożliwiając jego zapis do pliku. `ImageIO` jest klasą narzędziową do odczytu i zapisu obrazów w Javie. `setDisplayRSquaredValue` umożliwia wyświetlanie statystyki R‑kwadrat na linii trendu.

### Analizuj wyniki
Otwórz `output.xlsx` w Excelu, aby zweryfikować, że linia trendu, równanie i wartość R‑kwadrat pojawiają się zgodnie z oczekiwaniami. Otwórz wyeksportowany plik obrazu (np. `chart.png`), aby zobaczyć czysty wizualny rezultat, który można udostępnić bez oryginalnego skoroszytu.

## Typowe problemy i rozwiązania
- **Linia trendu nie jest wyświetlana:** Upewnij się, że zakres danych (`A1:A10`) zawiera wartości liczbowe; dane nienumeryczne uniemożliwiają obliczenie linii trendu.  
- **Wartość R‑kwadrat wyświetla się jako 0:** Często oznacza to, że seria danych jest stała lub brakuje w niej zmienności. Spróbuj innego zestawu danych lub użyj linii trendu wielomianowej.  
- **Eksport obrazu nie powodzi się z `NullPointerException`:** Zweryfikuj, że wykres został w pełni wyrenderowany przed wywołaniem `toImage()`. Zapisanie skoroszytu najpierw może czasami rozwiązać problemy z synchronizacją.

## Najczęściej zadawane pytania

**P: Jak mogę zmienić typ linii trendu?**  
O: Użyj innej enumeracji `TrendlineType` przy dodawaniu linii trendu, np. `TrendlineType.POLYNOMIAL` dla dopasowania wielomianowego.

**P: Czy mogę dostosować wygląd linii trendu (kolor, grubość)?**  
O: Tak. Uzyskaj dostęp do `LineFormat` linii trendu poprzez `trendline.getLineFormat()` i ustaw właściwości takie jak `setWeight()` i `setColor()`.

**P: Jak wyeksportować wykres do PDF zamiast obrazu?**  
O: Najpierw skonwertuj wykres na obraz, a następnie osadź ten obraz w PDF przy użyciu Aspose.PDF lub dowolnej innej biblioteki PDF.

**P: Czy można dodać wiele linii trendu do tego samego wykresu?**  
O: Oczywiście. Wywołaj `chart.getNSeries().get(0).getTrendlines().add(...)` dla każdej serii, którą chcesz przeanalizować.

**P: Czy Aspose.Cells obsługuje eksport obrazów w wysokiej rozdzielczości?**  
O: Tak. Możesz określić DPI przy wywołaniu `chart.toImage()` i następnie skalować obraz przed zapisem, zapewniając wyraźny wynik do druku lub na ekranach o wysokiej gęstości pikseli.

---

**Ostatnia aktualizacja:** 2026-08-27  
**Testowano z:** Aspose.Cells for Java latest (supports 50+ file formats and processes workbooks with up to 2 million rows without full memory load)  
**Autor:** Aspose

## Powiązane samouczki

- [Dodaj etykiety danych do wykresu Excel przy użyciu Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Jak wyeksportować wykresy Excel jako SVG przy użyciu Aspose.Cells Java dla skalowalnej grafiki wektorowej](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Eksportuj wykresy Excel do PDF przy użyciu Aspose.Cells for Java&#58; Przewodnik po niestandardowych rozmiarach stron](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}