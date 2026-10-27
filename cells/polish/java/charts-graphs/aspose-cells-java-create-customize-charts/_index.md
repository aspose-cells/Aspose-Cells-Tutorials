---
date: '2026-04-08'
description: Dowiedz się, jak generować wykres słupkowy w Javie przy użyciu Aspose.Cells,
  obejmując tworzenie wykresu w Javie, dodawanie arkusza wykresu oraz eksportowanie
  skoroszytu Excel.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Generowanie wykresu kolumnowego z samouczkiem Aspose.Cells Java
url: /pl/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Generowanie wykresu słupkowego przy użyciu Aspose.Cells Java

W dzisiejszych aplikacjach opartych na danych, **generowanie wykresu słupkowego** szybko i programowo może przekształcić surowe liczby w przejrzyste wizualne wnioski. Niezależnie od tego, czy tworzysz pulpit nawigacyjny raportowy, narzędzie analityczne, czy prostą funkcję eksportu, Aspose.Cells for Java zapewnia płynne API do **tworzenia wykresu w Java** projektów bez konieczności korzystania z interfejsu Excel. W tym samouczku nauczysz się, jak skonfigurować bibliotekę, **wypełnić komórki Excel**, dodać **arkusz wykresu**, dostosować **tytuł wykresu** oraz w końcu **wyeksportować skoroszyt Excel** do pliku.

## Szybkie odpowiedzi
- **Co oznacza „generowanie wykresu słupkowego”?** Tworzy pionową wizualizację w postaci słupków na podstawie danych tabelarycznych.  
- **Jakiej biblioteki wymaga?** Aspose.Cells for Java (dostępna darmowa wersja próbna).  
- **Czy potrzebna jest instalacja Excel?** Nie, biblioteka działa niezależnie od Microsoft Excel.  
- **Czy mogę eksportować do formatów innych niż XLS?** Tak – PDF, PNG, SVG itd., za pomocą `workbook.save()`.  
- **Czy licencja jest wymagana w środowisku produkcyjnym?** Tak, wymagana jest zakupiona lub tymczasowa licencja.

## Czym jest wykres słupkowy?
Wykres słupkowy wyświetla serie danych jako pionowe słupki, co ułatwia porównywanie wartości w różnych kategoriach, takich jak regiony, miesiące czy linie produktów. Aspose.Cells pozwala zbudować ten wykres w pełni w kodzie, dając pełną kontrolę nad danymi, stylizacją i formatem wyjściowym.

## Dlaczego warto używać Aspose.Cells do tworzenia wykresów w Java?
- **Brak interfejsu COM** – działa na każdym systemie operacyjnym z JVM.  
- **Bogate opcje stylizacji** – obrazy, gradienty, legendy i własne czcionki.  
- **Wysoka wydajność** – odpowiednia dla dużych zestawów danych.  
- **Wiele formatów eksportu** – XLS, XLSX, PDF, PNG i inne.

## Wymagania wstępne
- **Java Development Kit (JDK) 8+** zainstalowany.  
- Podstawowa znajomość Javy oraz pojęć związanych z Excelem.  

### Wymagane biblioteki
Dodaj Aspose.Cells do swojego projektu, używając jednego z poniższych fragmentów kodu.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Uzyskanie licencji
Aspose oferuje darmową wersję próbną oraz tymczasową licencję do intensywnych testów.

- **Darmowa wersja próbna**: [Pobierz darmowo](https://releases.aspose.com/cells/java/)  
- **Tymczasowa licencja**: [Zamów tutaj](https://purchase.aspose.com/temporary-license/)

## Konfiguracja Aspose.Cells dla Java

Najpierw utwórz instancję `Workbook` – będzie to płótno dla naszych danych i wykresu.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## Przewodnik krok po kroku

### 1. Utwórz i nazwij arkusz
Przechowamy surowe dane w arkuszu o nazwie **Data**.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Wypełnij komórki Excel
Wstaw nazwy regionów i wartości sprzedaży, które wykres słupkowy zwizualizuje.

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Dodaj arkusz wykresu
Oddzielenie wykresu od surowych danych utrzymuje porządek w skoroszycie.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. Utwórz wykres słupkowy
Teraz faktycznie **generujemy obiekty wykresu słupkowego**.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Ustaw obraz jako wypełnienie tła w obszarze wykresu
Obraz tła może sprawić, że wykres będzie się wyróżniał.

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. Ustaw tytuł wykresu
Dostosowanie **tytułu wykresu** poprawia czytelność.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. Skonfiguruj dane serii i legendę
Połącz zakres danych z wykresem i ustaw pozycję legendy.

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. Wyeksportuj skoroszyt Excel
Na koniec **wyeksportuj skoroszyt Excel** do pliku XLS (lub dowolnego obsługiwanego formatu).

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Praktyczne zastosowania
- **Raporty biznesowe** – Automatyczne generowanie wykresów sprzedaży do miesięcznych PDF‑ów.  
- **Narzędzia analizy danych** – Osadzanie dynamicznych wykresów w niestandardowych pulpitach analitycznych.  
- **Pulpity przedsiębiorstw** – Odświeżanie obrazów wykresów w locie w celu monitorowania w czasie rzeczywistym.

## Rozważania dotyczące wydajności
- Aktualizuj komórki partiami przy pracy z dużymi zestawami danych, aby zmniejszyć narzut.  
- Zwolnij zasoby (`workbook.dispose()`), jeśli przetwarzasz wiele skoroszytów w pętli.

## Typowe problemy i rozwiązania
- **Obraz się nie wyświetla** – Sprawdź ścieżkę pliku oraz czy format obrazu (PNG, JPEG) jest obsługiwany.  
- **Wykres jest pusty** – Upewnij się, że odwołania do zakresu danych (`Data!B2:B8`) odpowiadają wypełnionym komórkom.  
- **Błędy braku pamięci** – Przetwarzaj dane w partiach i wywołaj `System.gc()` po dużych zapisach.

## Najczęściej zadawane pytania

**Q: Jak dodać wiele serii do wykresu słupkowego?**  
A: Wywołaj `chart.getNSeries().add()` wielokrotnie z różnymi zakresami danych, np. `"Data!C2:C8"` dla drugiej serii.

**Q: Czy mogę zmienić etykiety osi?**  
A: Tak. Użyj `chart.getCategoryAxis().setTitle("Regions")` i `chart.getValueAxis().setTitle("Sales")`.

**Q: Do jakich formatów mogę eksportować oprócz XLS?**  
A: Użyj `workbook.save("chart.pdf")`, `workbook.save("chart.png")` lub `workbook.save("chart.xlsx")` dla PDF, PNG i XLSX odpowiednio.

**Q: Czy licencja jest wymagana dla wersji deweloperskich?**  
A: Darmowa wersja próbna wystarcza do oceny, ale do wdrożeń produkcyjnych potrzebna jest stała lub tymczasowa licencja.

**Q: Jak mogę zwiększyć szybkość renderowania przy tysiącach wierszy?**  
A: Wypełniaj komórki przy użyciu `cells.importArray()` i minimalizuj ponowne rysowanie wykresu, tworząc go po załadowaniu wszystkich danych.

---

**Ostatnia aktualizacja:** 2026-04-08  
**Testowano z:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  

## Zasoby

- [Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Pobierz Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Kup licencję](https://purchase.aspose.com/buy)
- [Darmowa wersja próbna](https://releases.aspose.com/cells/java/)
- [Żądanie licencji tymczasowej](https://purchase.aspose.com/temporary-license/)
- [Forum wsparcia](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}