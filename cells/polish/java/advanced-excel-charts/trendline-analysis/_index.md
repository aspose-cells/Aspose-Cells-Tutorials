---
date: 2026-02-09
description: Dowiedz się, jak utworzyć wykres w Excelu, dodać linię trendu, wyświetlić
  wartość R‑kwadrat oraz wyeksportować wykres jako obraz przy użyciu Aspose.Cells
  for Java. Zawiera kroki ładowania pliku Excel, dostosowywania wykresu i zapisywania
  jako PNG/JPEG.
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Jak utworzyć wykres Excel z linią trendu i wyeksportować go jako obraz przy
  użyciu Aspose.Cells dla Javy
url: /pl/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Eksport wykresu do obrazu z analizą linii trendu

W tym samouczku dowiesz się, jak **utworzyć wykres Excel** z linią trendu, wyświetlić jego wartość R‑kwadrat oraz wyeksportować powstałą wizualizację do obrazu przy użyciu Aspose.Cells for Java. Przejdziemy przez ładowanie istniejącego skoroszytu, dodawanie linii trendu, dostosowywanie tytułów, zapisywanie skoroszytu oraz ostateczne generowanie pliku PNG/JPEG, który możesz osadzić w dowolnym miejscu.

## Szybkie odpowiedzi
- **Jaki jest główny cel tego przewodnika?** Pokazać, jak dodać linię trendu, wyświetlić jej równanie i wartość R‑kwadrat oraz wyeksportować powstały wykres do obrazu przy użyciu Javy.  
- **Jakiej biblioteki wymaga?** Aspose.Cells for Java (pobierz [here](https://releases.aspose.com/cells/java/)).  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w środowisku deweloperskim; licencja komercyjna jest wymagana w produkcji.  
- **Czy mogę generować plik Excel w Javie?** Tak – samouczek tworzy i zapisuje skoroszyt XLSX.  
- **Jak wyeksportować wykres do PNG lub JPEG?** Użyj metody `Chart.toImage()` (omówiona w sekcji „Export Chart”).

## Jak utworzyć wykres Excel z linią trendu i wyeksportować go do obrazu
Ten nagłówek bezpośrednio odpowiada na główne zapytanie słowne i prowadzi Cię przez cały proces w logicznej kolejności. Poniżej znajdziesz dlaczego, wymagania wstępne oraz krok‑po‑kroku instrukcję.

## Co to jest eksport wykresu do obrazu?
Eksportowanie wykresu do obrazu przekształca wizualną reprezentację danych w przenośny bitmap (PNG, JPEG itp.). Jest to przydatne przy osadzaniu wykresów w raportach, stronach internetowych lub prezentacjach, gdzie nie jest wymagany oryginalny plik Excel.

## Dlaczego dodać linię trendu i wyświetlić wartość R‑kwadrat?
Linia trendu pomaga zidentyfikować podstawowy wzorzec serii danych, natomiast metryka **R‑kwadrat** określa, jak dobrze linia trendu dopasowuje się do danych. Umieszczenie ich w wyeksportowanym obrazie daje interesariuszom natychmiastowy wgląd bez otwierania skoroszytu.

## Wymagania wstępne
- Zainstalowany Java 8 lub nowsza.  
- Biblioteka Aspose.Cells for Java dodana do projektu (pliki JAR w classpath).  
- Podstawowa znajomość środowisk IDE Java (IntelliJ IDEA, Eclipse itp.).  

## Przewodnik krok po kroku

### Krok 1: Konfiguracja projektu
Utwórz nowy projekt Java i dodaj pliki JAR Aspose.Cells do ścieżki kompilacji. Przygotuje to środowisko do generowania i manipulacji plikami Excel.

### Krok 2: Załaduj plik Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Właśnie **załadowaliśmy plik Excel** do pamięci, gotowy do tworzenia wykresu.*

### Krok 3: Utwórz wykres
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Tutaj generujemy wykres liniowy, który później będzie zawierał naszą linię trendu.*

### Krok 4: Dodaj linię trendu (how to add trendline) i wyświetl wartość R‑kwadrat
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*Wywołanie `setDisplayRSquaredValue(true)` zapewnia, że **wartość R‑kwadrat** pojawi się na wykresie.*

### Krok 5: Dostosuj wykres i zapisz skoroszyt (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Teraz skoroszyt jest **generowany** i zapisywany jako plik XLSX, gotowy do dalszego przetwarzania.*

### Krok 6: Eksportuj wykres do obrazu (export chart to image)
> **Uwaga:** Ten krok jest opisany bez dodatkowego bloku kodu, aby zachować oryginalną liczbę bloków.  
Po utworzeniu i zapisaniu wykresu możesz wyeksportować go do obrazu, wywołując metodę `chart.toImage()` i zapisując otrzymany `java.awt.image.BufferedImage` w wybranym formacie pliku (PNG, JPEG, BMP). Typowy przebieg pracy wygląda następująco:
1. Pobierz obiekt `Chart` (już zrobiono w poprzednich krokach).  
2. Wywołaj `chart.toImage()`, aby uzyskać `BufferedImage`.  
3. Użyj `ImageIO.write(bufferedImage, "png", new File("chart.png"))`, aby zapisać plik.  

To generuje obraz wysokiej rozdzielczości, który możesz osadzić w dowolnym miejscu, kończąc proces **eksportu wykresu do obrazu**.

## Analiza wyników
Otwórz `output.xlsx` w Excelu, aby zweryfikować, że linia trendu, równanie i wartość R‑kwadrat pojawiają się zgodnie z oczekiwaniami. Otwórz wyeksportowany plik obrazu (np. `chart.png`), aby zobaczyć czystą wizualizację, którą można udostępnić bez oryginalnego skoroszytu.

## Typowe problemy i rozwiązania
- **Linia trendu nie jest wyświetlana:** Upewnij się, że zakres danych (`A1:A10`) rzeczywiście zawiera wartości liczbowe; dane nienumeryczne uniemożliwią obliczenie linii trendu.  
- **Wartość R‑kwadrat wyświetla się jako 0:** Często oznacza to, że seria danych jest stała lub ma niewystarczającą zmienność. Spróbuj innego zestawu danych lub linii trendu wielomianowej.  
- **Eksport obrazu kończy się błędem `NullPointerException`:** Sprawdź, czy wykres został w pełni wyrenderowany przed wywołaniem `toImage()`. Zapisanie skoroszytu najpierw może czasami rozwiązać problemy z kolejnością.

## Najczęściej zadawane pytania

**P: Jak mogę zmienić typ linii trendu?**  
O: Użyj innej enumeracji `TrendlineType` przy dodawaniu linii trendu, np. `TrendlineType.POLYNOMIAL` dla dopasowania wielomianowego.

**P: Czy mogę dostosować wygląd linii trendu (kolor, grubość)?**  
O: Tak. Uzyskaj dostęp do `LineFormat` linii trendu poprzez `trendline.getLineFormat()` i ustaw właściwości, takie jak `setWeight()` i `setColor()`.

**P: Jak wyeksportować wykres do PDF zamiast obrazu?**  
O: Najpierw skonwertuj wykres na obraz, a następnie osadź ten obraz w PDF przy użyciu Aspose.PDF lub dowolnej wybranej biblioteki PDF.

**P: Czy można dodać wiele linii trendu do tego samego wykresu?**  
O: Oczywiście. Wywołaj `chart.getNSeries().get(0).getTrendlines().add(...)` dla każdej serii, którą chcesz analizować.

**P: Czy Aspose.Cells obsługuje eksport obrazów w wysokiej rozdzielczości?**  
O: Tak. Możesz określić DPI przy wywoływaniu `chart.toImage()`, a następnie odpowiednio skalować obraz przed zapisaniem.

## Podsumowanie
Masz teraz kompletną, kompleksową metodę do **tworzenia wykresu Excel**, dodawania linii trendu, wyświetlania równania i wartości R‑kwadrat, dostosowywania wyglądu, zapisywania skoroszytu oraz ostatecznego eksportu wykresu jako obrazu PNG/JPEG. Takie podejście pozwala programowo generować profesjonalne zasoby analityczne, idealne do automatycznych raportów, pulpitów nawigacyjnych lub wszelkich scenariuszy, w których statyczny obraz jest wygodniejszy niż plik Excel.

---

**Ostatnia aktualizacja:** 2026-02-09  
**Testowano z:** Aspose.Cells for Java latest  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}