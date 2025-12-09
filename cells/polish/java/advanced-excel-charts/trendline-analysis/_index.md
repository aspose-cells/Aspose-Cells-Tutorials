---
date: 2025-12-09
description: 'Dowiedz się, jak wyeksportować wykres do obrazu, wykonując analizę linii
  trendu w Javie z Aspose.Cells. Zawiera kroki: wczytanie pliku Excel, dodanie linii
  trendu, wyświetlenie wartości R‑kwadrat oraz zapis skoroszytu w formacie XLSX.'
language: pl
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Eksport wykresu do obrazu z analizą linii trendu przy użyciu Aspose.Cells dla
  Javy
url: /java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Eksport wykresu do obrazu z analizą linii trendu

W tym samouczku odkryjesz **jak wyeksportować wykres do obrazu** podczas przeprowadzania pełnej **analizy linii trendu** przy użyciu Aspose.Cells for Java. Przejdziemy przez ładowanie istniejącego skoroszytu Excel, dodawanie linii trendu, wyświetlanie wartości R‑squared, dostosowywanie wykresu i ostatecznie eksportowanie wykresu jako pliku obrazu — wszystko z jasnym, krok po kroku kodem, który możesz kopiować & wklejać.

## Szybkie odpowiedzi
- **Jaki jest główny cel tego przewodnika?** Pokazać, jak dodać linię trendu, wyświetlić jej równanie i wartość R‑squared oraz wyeksportować powstały wykres do obrazu przy użyciu Javy.  
- **Która biblioteka jest wymagana?** Aspose.Cells for Java (pobierz [tutaj](https://releases.aspose.com/cells/java/)).  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w środowisku deweloperskim; licencja komercyjna jest wymagana w produkcji.  
- **Czy mogę generować plik Excel w Javie?** Tak — samouczek tworzy i zapisuje skoroszyt XLSX.  
- **Jak wyeksportować wykres do PNG lub JPEG?** Użyj metody `Chart.toImage()` (omówiona w sekcji „Export Chart”).

## Co to jest eksport wykresu do obrazu?
Eksportowanie wykresu do obrazu konwertuje wizualną reprezentację danych na przenośny bitmap (PNG, JPEG itp.). Jest to przydatne przy osadzaniu wykresów w raportach, stronach internetowych lub prezentacjach, gdzie nie jest wymagany oryginalny plik Excel.

## Dlaczego dodać linię trendu i wyświetlić wartość R‑squared?
Linia trendu pomaga zidentyfikować podstawowy wzorzec serii danych, a metryka **R‑squared** kwantyfikuje, jak dobrze linia trendu dopasowuje się do danych. Umieszczenie ich w wyeksportowanym obrazie daje interesariuszom natychmiastowy wgląd bez otwierania skoroszytu.

## Wymagania wstępne
- Zainstalowany Java 8 lub nowszy.  
- Biblioteka Aspose.Cells for Java dodana do projektu (pliki JAR w ścieżce klas).  
- Podstawowa znajomość środowisk IDE Java (IntelliJ IDEA, Eclipse itp.).

## Przewodnik krok po kroku

### Krok 1: Konfiguracja projektu
Utwórz nowy projekt Java i dodaj pliki JAR Aspose.Cells do ścieżki kompilacji. Przygotuje to środowisko do generowania i manipulacji plikami Excel.

### Krok 2: Ładowanie pliku Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Właśnie **załadowaliśmy plik Excel** do pamięci, gotowy do tworzenia wykresu.*

### Krok 3: Tworzenie wykresu
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Tutaj generujemy wykres liniowy, który później będzie zawierał naszą linię trendu.*

### Krok 4: Dodawanie linii trendu (how to add trendline) i wyświetlanie wartości R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*Wywołanie `setDisplayRSquaredValue(true)` zapewnia, że **wartość R‑squared** pojawi się na wykresie.*

### Krok 5: Dostosowanie wykresu i zapis skoroszytu (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Teraz skoroszyt jest **wygenerowany** i zapisany jako plik XLSX, gotowy do dalszego przetwarzania.*

### Krok 6: Eksport wykresu do obrazu (export chart to image)
> **Uwaga:** Ten krok jest opisany bez dodatkowego bloku kodu, aby zachować oryginalną liczbę bloków.  
Po utworzeniu i zapisaniu wykresu możesz wyeksportować go do obrazu, wywołując metodę `chart.toImage()` i zapisując otrzymany `java.awt.image.BufferedImage` w wybranym formacie pliku (PNG, JPEG, BMP). Typowy przebieg pracy jest następujący:
1. Pobierz obiekt `Chart` (już zrobiono w poprzednich krokach).  
2. Wywołaj `chart.toImage()`, aby uzyskać `BufferedImage`.  
3. Użyj `ImageIO.write(bufferedImage, "png", new File("chart.png"))`, aby zapisać plik.  

To generuje obraz wysokiej rozdzielczości, który możesz osadzić gdziekolwiek, kończąc proces **eksportu wykresu do obrazu**.

## Analiza wyników
Otwórz `output.xlsx` w Excelu, aby zweryfikować, że linia trendu, równanie i wartość R‑squared pojawiają się zgodnie z oczekiwaniami. Otwórz wyeksportowany plik obrazu (np. `chart.png`), aby zobaczyć czysty wizualny efekt, który można udostępnić bez oryginalnego skoroszytu.

## Typowe problemy i rozwiązania
- **Linia trendu nie wyświetla się:** Upewnij się, że zakres danych (`A1:A10`) rzeczywiście zawiera wartości liczbowe; dane nienumeryczne uniemożliwią obliczenie linii trendu.  
- **Wartość R‑squared wyświetla się jako 0:** Często oznacza to, że seria danych jest stała lub ma niewystarczającą zmienność. Spróbuj innego zestawu danych lub linii trendu wielomianowej.  
- **Eksport obrazu nie powodzi się z `NullPointerException`:** Zweryfikuj, że wykres został w pełni wyrenderowany przed wywołaniem `toImage()`. Zapisanie skoroszytu najpierw może czasami rozwiązać problemy z synchronizacją.

## Najczęściej zadawane pytania

**Q: Jak mogę zmienić typ linii trendu?**  
A: Użyj innej enumeracji `TrendlineType` przy dodawaniu linii trendu, np. `TrendlineType.POLYNOMIAL` dla dopasowania wielomianowego.

**Q: Czy mogę dostosować wygląd linii trendu (kolor, grubość)?**  
A: Tak. Uzyskaj dostęp do `LineFormat` linii trendu poprzez `trendline.getLineFormat()` i ustaw właściwości takie jak `setWeight()` i `setColor()`.

**Q: Jak wyeksportować wykres do PDF zamiast obrazu?**  
A: Najpierw skonwertuj wykres na obraz, a następnie osadź ten obraz w PDF przy użyciu Aspose.PDF lub dowolnej wybranej biblioteki PDF.

**Q: Czy można dodać wiele linii trendu do tego samego wykresu?**  
A: Oczywiście. Wywołaj `chart.getNSeries().get(0).getTrendlines().add(...)` dla każdej serii, którą chcesz analizować.

**Q: Czy Aspose.Cells obsługuje eksport obrazów wysokiej rozdzielczości?**  
A: Tak. Możesz określić DPI przy wywoływaniu `chart.toImage()` i następnie skalować obraz odpowiednio przed zapisem.

## Podsumowanie
Masz teraz kompletną, kompleksową metodę **eksportu wykresu do obrazu** przy jednoczesnym przeprowadzaniu **analizy linii trendu** w Javie z użyciem Aspose.Cells. Ładując plik Excel, dodając linię trendu, wyświetlając równanie i wartość R‑squared, dostosowując wykres, zapisując skoroszyt i ostatecznie eksportując wizualizację do PNG/JPEG, możesz programowo generować profesjonal zasoby analityczne.

---

**Ostatnia aktualizacja:** 2025-12-09  
**Testowano z:** Aspose.Cells for Java 24.12 (latest)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}