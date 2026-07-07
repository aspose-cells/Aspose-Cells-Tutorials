---
date: '2026-07-07'
description: Poznaj przykład wykresu Aspose Cells, aby tworzyć dynamiczne wykresy
  przestawne w Excelu przy użyciu Java. Postępuj zgodnie z instrukcjami krok po kroku,
  aby uzyskać płynną analizę danych.
keywords:
- aspose cells chart example
- how to create pivot chart
- dynamic pivot chart excel
- export pivot chart excel
- add pivot chart workbook
og_description: Poznaj przykład wykresu Aspose Cells, aby tworzyć dynamiczne wykresy
  przestawne w Excelu przy użyciu Java. Postępuj zgodnie z instrukcjami krok po kroku,
  aby uzyskać płynną analizę danych.
og_title: 'Aspose Cells Chart Example: Opanowanie wykresów przestawnych w Java'
schemas:
- author: Aspose
  dateModified: '2026-07-07'
  description: Learn the Aspose Cells chart example to create dynamic pivot charts
    in Excel using Java. Follow step‑by‑step instructions for seamless data analysis.
  headline: 'Aspose Cells Chart Example: Mastering Pivot Charts in Java'
  type: TechArticle
- description: Learn the Aspose Cells chart example to create dynamic pivot charts
    in Excel using Java. Follow step‑by‑step instructions for seamless data analysis.
  name: 'Aspose Cells Chart Example: Mastering Pivot Charts in Java'
  steps:
  - name: Load the Source Workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory.
  - name: Add a Worksheet for the Pivot Chart
    text: Create a dedicated chart sheet to keep the visual separate from raw data.
  - name: Insert a Pivot Table
    text: First, define the data range for the pivot table, then add it to the chart
      sheet. The `PivotTable` class represents a pivot table in a worksheet and provides
      methods to define its data source, layout, and calculations.
  - name: Create and Configure the Pivot Chart
    text: The `Chart` class represents any Excel chart. Here we create a column chart
      linked to the pivot table.
  - name: Export the Workbook
    text: Save the workbook with the new pivot chart to an `.xlsx` file, or directly
      to PDF if you need a static report.
  type: HowTo
- questions:
  - answer: Yes, call `chart.toImage("chart.png", ImageFormat.PNG)` after configuring
      the chart.
    question: Can I export a pivot chart directly to an image file?
  - answer: The library can preserve existing VBA macros, but it does not create or
      modify them programmatically.
    question: Does Aspose.Cells support Excel macros in pivot charts?
  - answer: Absolutely—invoke `pivotTable.refreshData()` and then `chart.refresh()`
      to reflect the latest values.
    question: Is it possible to update the pivot chart after changing the source data?
  - answer: Over 40 types, including column, line, area, pie, radar, and stacked bar,
      all fully supported for pivot data.
    question: Which chart types are available for pivot charts?
  - answer: Yes, a purchased license removes evaluation limits and enables full feature
      set.
    question: Do I need a license to use the Maven/Gradle setup in production?
  type: FAQPage
title: 'Aspose Cells Chart Example: Opanowanie wykresów przestawnych w Java'
url: /pl/java/charts-graphs/aspose-cells-java-pivot-charts-excel-tutorial/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Przykład wykresu Aspose Cells: Opanowanie wykresów przestawnych w Javie

W dzisiejszym świecie opartym na danych, przekształcanie surowych liczb w przejrzyste wizualne wnioski jest niezbędne. Ten samouczek pokazuje **aspose cells chart example**, którego potrzebujesz, aby zbudować dynamiczne wykresy przestawne w Excelu przy użyciu Javy. Po zakończeniu tego przewodnika będziesz w stanie załadować skoroszyt, dodać dedykowany arkusz wykresu, powiązać tabelę przestawną i wyeksportować wynik — wszystko w kilku linijkach kodu.

## Szybkie odpowiedzi
- **Jaka jest podstawowa klasa do pracy z plikami Excel?** `Workbook` reprezentuje cały plik Excel w pamięci.  
- **Który artefakt Maven dodaje Aspose.Cells do projektu?** `com.aspose:aspose-cells` (wersja 25.3 lub nowsza).  
- **Czy mogę utworzyć wykres przestawny bez licencji?** Tak, wersja próbna działa w środowisku deweloperskim, ale licencja usuwa ograniczenia oceny.  
- **Ile typów wykresów obsługuje Aspose.Cells?** Ponad 40 typów wykresów, w tym liniowy, słupkowy, kołowy i radarowy.  
- **Jaki jest najszybszy sposób eksportu wykresu przestawnego do PDF?** Wywołaj `chart.toPdf("output.pdf")` po skonfigurowaniu źródła danych wykresu.

## Czym jest wykres przestawny w Excelu?
**Wykres przestawny** to interaktywna wizualna reprezentacja tabeli przestawnej, umożliwiająca użytkownikom dynamiczne eksplorowanie zagregowanych danych. Korzystając z Aspose.Cells, możesz generować te wykresy programowo bez otwierania Excela. Automatycznie aktualizuje się, gdy zmienia się podległa tabela przestawna, obsługuje filtrowanie i może być dostosowywany przy użyciu różnych typów wykresów, tytułów i legend, co czyni go potężnym narzędziem analizy danych.

## Dlaczego używać Aspose.Cells dla Javy do tworzenia wykresów przestawnych?
Aspose.Cells obsługuje **ponad 50 formatów wejścia i wyjścia** oraz może radzić sobie ze skoroszytami zawierającymi **setki arkuszy**, przy zużyciu pamięci poniżej 200 MB. Jego API tworzy, modyfikuje i renderuje wykresy w **poniżej 2 sekund** dla typowych zestawów danych 10 KB, co czyni go idealnym rozwiązaniem do raportowania po stronie serwera.

## Wymagania wstępne

- **Aspose.Cells for Java** w wersji 25.3 lub nowszej.  
- System budowania Maven lub Gradle.  
- JDK 8 lub nowszy oraz IDE, takie jak IntelliJ IDEA, Eclipse lub NetBeans.  
- Podstawowa znajomość Javy; znajomość Excela jest pomocna, ale nie wymagana.

### Wymagane biblioteki i zależności
- **Maven:** dodaj zależność Aspose.Cells (zobacz sekcję *aspose cells maven setup* poniżej).  
- **Gradle:** uwzględnij tę samą artefakt w pliku `build.gradle`.

### Kroki uzyskania licencji
- **Bezpłatna wersja próbna:** rozpocznij od wersji próbnej, aby zapoznać się z przykładem wykresu Aspose Cells.  
- **Licencja tymczasowa:** uzyskaj tymczasowy klucz do rozszerzonego testowania.  
- **Zakup:** kup pełną licencję na [oficjalnej stronie Aspose](https://purchase.aspose.com/buy).

## Jak skonfigurować Aspose.Cells dla Javy

### Zależność Maven (aspose cells maven setup)

Dodaj następujący fragment do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```

### Zależność Gradle

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Podstawowa inicjalizacja
Po dodaniu zależności, zainicjalizuj bibliotekę jak pokazano poniżej:

```java
// Initialize license (optional for trial)
License license = new License();
license.setLicense("Aspose.Cells.lic");

// Create a Workbook object – this loads or creates an Excel file.
Workbook workbook = new Workbook();
```

## Jak utworzyć wykres przestawny przy użyciu Aspose.Cells dla Javy?

Załaduj dane źródłowe, wygeneruj tabelę przestawną i powiąż ją z wykresem — wszystko w kilku prostych krokach. Proces obejmuje załadowanie skoroszytu zawierającego dane źródłowe, utworzenie tabeli przestawnej podsumowującej te dane, dodanie dedykowanego arkusza wykresu, powiązanie tabeli przestawnej z wykresem, dostosowanie wyglądu wykresu oraz zapisanie skoroszytu w żądanym formacie.

### Krok 1: Załaduj źródłowy skoroszyt
Klasa `Workbook` jest obiektem najwyższego poziomu Aspose.Cells, który reprezentuje pojedynczy plik Excel w pamięci.

```java
Workbook workbook = new Workbook("data.xlsx");
```

### Krok 2: Dodaj arkusz dla wykresu przestawnego
Utwórz dedykowany arkusz wykresu, aby oddzielić wizualizację od surowych danych.

```java
int chartSheetIndex = workbook.getWorksheets().addChart("PivotChartSheet");
Worksheet chartSheet = workbook.getWorksheets().get(chartSheetIndex);
```

### Krok 3: Wstaw tabelę przestawną
Najpierw określ zakres danych dla tabeli przestawnej, a następnie dodaj ją do arkusza wykresu.

Klasa `PivotTable` reprezentuje tabelę przestawną w arkuszu i udostępnia metody do definiowania jej źródła danych, układu i obliczeń.

```java
int pivotTableIndex = chartSheet.getPivotTables().add("A1:D100", "PivotTable1", 0, 0);
PivotTable pivotTable = chartSheet.getPivotTables().get(pivotTableIndex);
pivotTable.addFieldToArea(PivotFieldType.ROW, 0);   // Category
pivotTable.addFieldToArea(PivotFieldType.DATA, 1);  // Values
```

### Krok 4: Utwórz i skonfiguruj wykres przestawny
Klasa `Chart` reprezentuje dowolny wykres Excel. Tutaj tworzymy wykres słupkowy powiązany z tabelą przestawną.

```java
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 5, 0, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
chart.getNSeries().add("=PivotTable1!$B$2:$B$5", true);
chart.setTitle("Sales by Region");
```

### Krok 5: Eksportuj skoroszyt
Zapisz skoroszyt z nowym wykresem przestawnym do pliku `.xlsx` lub bezpośrednio do PDF, jeśli potrzebny jest statyczny raport.

```java
workbook.save("PivotChartResult.xlsx", SaveFormat.XLSX);
// Optional PDF export
workbook.save("PivotChartResult.pdf", SaveFormat.PDF);
```

## Praktyczne zastosowania dynamicznych wykresów przestawnych

- **Raportowanie finansowe:** Automatyczne generowanie kwartalnych pulpitów, które aktualizują się przy imporcie nowych danych.  
- **Analiza sprzedaży:** Wizualizacja trendów sprzedaży regionalnej za pomocą jednego wywołania API.  
- **Zarządzanie zapasami:** Śledzenie poziomów zapasów i punktów zamawiania w czasie rzeczywistym.  
- **Wgląd w klientów:** Łączenie danych demograficznych z historią zakupów w celu uzyskania interaktywnych wykresów.  
- **Zarządzanie projektami:** Pokazywanie przydziału zasobów i odchyleń w harmonogramie przy użyciu wykresów przestawnych.

## Wskazówki dotyczące wydajności przy dużych zestawach danych

- **Zarządzanie pamięcią:** Wywołaj `workbook.dispose()` po zapisaniu, aby zwolnić zasoby natywne.  
- **Operacje wsadowe:** Użyj `CellsHelper.copyRange` do przenoszenia dużych bloków danych zamiast pętli komórka po komórce.  
- **Ładowanie leniwe:** Podczas przetwarzania plików większych niż 100 MB, włącz `LoadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, aby utrzymać niskie zużycie pamięci.

## Typowe problemy i rozwiązania

| Problem | Rozwiązanie |
|---------|-------------|
| **Tabela przestawna nie odzwierciedla nowych danych** | Odśwież tabelę przestawną przy użyciu `pivotTable.refreshData()` przed utworzeniem wykresu. |
| **Wykres jest pusty** | Upewnij się, że zakres źródła danych wykresu odpowiada zakresowi wynikowemu tabeli przestawnej. |
| **Błędy braku pamięci przy dużych plikach** | Użyj `LoadOptions` z `MemorySetting.MEMORY_PREFERENCE` i zamknij arkusze, których już nie potrzebujesz. |

## Najczęściej zadawane pytania

**Q: Czy mogę wyeksportować wykres przestawny bezpośrednio do pliku obrazu?**  
A: Tak, wywołaj `chart.toImage("chart.png", ImageFormat.PNG)` po skonfigurowaniu wykresu.

**Q: Czy Aspose.Cells obsługuje makra Excel w wykresach przestawnych?**  
A: Biblioteka może zachować istniejące makra VBA, ale nie tworzy ani nie modyfikuje ich programowo.

**Q: Czy można zaktualizować wykres przestawny po zmianie danych źródłowych?**  
A: Oczywiście — wywołaj `pivotTable.refreshData()`, a następnie `chart.refresh()`, aby odzwierciedlić najnowsze wartości.

**Q: Jakie typy wykresów są dostępne dla wykresów przestawnych?**  
A: Ponad 40 typów, w tym słupkowy, liniowy, powierzchniowy, kołowy, radarowy i skumulowany słupkowy, wszystkie w pełni obsługiwane dla danych przestawnych.

**Q: Czy potrzebuję licencji, aby używać konfiguracji Maven/Gradle w produkcji?**  
A: Tak, zakupiona licencja usuwa ograniczenia oceny i umożliwia pełny zestaw funkcji.

---

**Ostatnia aktualizacja:** 2026-07-07  
**Testowano z:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  

## Zasoby

- [Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Pobierz Aspose.Cells dla Javy](https://releases.aspose.com/cells/java/)
- [Kup licencję](https://purchase.aspose.com/buy)
- [Bezpłatna wersja próbna i licencje tymczasowe](https://releases.aspose.com/cells/java/)
- [Forum wsparcia Aspose](https://forum.aspose.com/c/cells/9)

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

```java
import com.aspose.cells.Workbook;

// Load an existing workbook
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/pivotTable_test.xls");
```

```java
   import com.aspose.cells.Workbook;
   ```

```java
   String dataDir = "YOUR_DATA_DIRECTORY";
   Workbook workbook = new Workbook(dataDir + "/pivotTable_test.xls");
   ```

```java
   import com.aspose.cells.SheetType;
   import com.aspose.cells.Worksheet;
   ```

```java
   int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
   Worksheet sheet3 = workbook.getWorksheets().get(sheetIndex);
   sheet3.setName("PivotChart");
   ```

```java
   import com.aspose.cells.Chart;
   import com.aspose.cells.ChartType;
   ```

```java
   int chartIndex = sheet3.getCharts().add(ChartType.COLUMN, 0, 5, 28, 16);
   Chart chart = sheet3.getCharts().get(chartIndex);
   ```

```java
   chart.setPivotSource("PivotTable!PivotTable1");
   chart.setHidePivotFieldButtons(false);
   ```

```java
   String outDir = "YOUR_OUTPUT_DIRECTORY";
   workbook.save(outDir + "/CPCBasedOnPTable_out.xls");
   ```

## Powiązane samouczki

- [Opanowanie tabel przestawnych w Excelu przy użyciu Aspose.Cells dla Javy: Kompletny przewodnik po analizie danych](/cells/java/data-analysis/excel-pivot-tables-aspose-cells-java-tutorial/)
- [Utwórz skoroszyt i dodaj wykresy przy użyciu Aspose.Cells dla Javy: Kompletny przewodnik](/cells/java/charts-graphs/create-workbook-add-charts-aspose-cells-java/)
- [Dostosowywanie wykresów Excel w Javie: Opanowanie Aspose.Cells dla płynnej wizualizacji danych](/cells/java/charts-graphs/excel-chart-customization-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}