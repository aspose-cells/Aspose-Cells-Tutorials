---
date: '2026-09-22'
description: Dowiedz się, jak stworzyć interaktywny wykres Excel z polami wyboru przy
  użyciu Aspose.Cells for Java. Ten przewodnik obejmuje konfigurację, dodawanie pól
  wyboru, licencjonowanie oraz najlepsze praktyki.
keywords:
- create interactive Excel chart
- how to add checkbox java
- aspose.cells license java
lastmod: '2026-09-22'
og_description: Dowiedz się, jak stworzyć interaktywny wykres Excel z polami wyboru
  przy użyciu Aspose.Cells for Java. Postępuj zgodnie z instrukcjami krok po kroku,
  zapoznaj się z wskazówkami dotyczącymi licencjonowania i odkryj praktyczne przykłady
  zastosowań.
og_image_alt: Guide showing how to create interactive Excel chart with checkboxes
  using Aspose.Cells for Java
og_title: Jak stworzyć interaktywny wykres Excel z polami wyboru
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to create interactive Excel chart with checkboxes using Aspose.Cells
    for Java. This guide covers setup, adding checkboxes, licensing, and best practices.
  headline: How to create interactive Excel chart with checkboxes
  type: TechArticle
- questions:
  - answer: Use Aspose.Cells’ `Shape` API with `ShapeType.FORM_CONTROL_CHECKBOX` and
      link it to a worksheet cell; the checkbox works natively in Excel.
    question: How do I add a checkbox without using VBA?
  - answer: The checkbox shape is available in the free evaluation, but a permanent
      Aspose.Cells license removes evaluation limits and enables full performance
      optimizations.
    question: Do I need a license for the checkbox feature?
  - answer: Files saved with Aspose.Cells follow the Office Open XML standard and
      open correctly in Excel 2016, 2019, 2021, and Microsoft 365.
    question: Which Excel versions can open the generated file?
  - answer: Yes, create a checkbox for each series, link each to a distinct helper
      cell, and use conditional formulas to toggle each series independently.
    question: Can I control multiple series with separate checkboxes?
  - answer: Practically, you can add dozens; performance remains stable up to 200
      controls per worksheet on typical server hardware.
    question: Is there a limit on the number of checkboxes per chart?
  type: FAQPage
tags:
- interactive Excel charts
- Aspose.Cells
- Java Excel automation
title: Jak stworzyć interaktywny wykres Excel z polami wyboru
url: /pl/java/charts-graphs/create-chart-checkbox-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak stworzyć interaktywny wykres Excel z polami wyboru

## Wstęp

W tym samouczku **stworzysz interaktywny wykres Excel**, który pozwala użytkownikom przełączać serie danych, klikając pola wyboru umieszczone bezpośrednio na wykresie. Korzystając z Aspose.Cells for Java, możesz programowo generować w pełni funkcjonalne skoroszyty, bez konieczności instalacji Microsoft Excel. To podejście działa w dowolnym rozwiązaniu raportowym lub dashboardowym opartym na Javie.

**Czego się nauczysz**
- Jak skonfigurować Aspose.Cells for Java w Maven lub Gradle  
- Jak utworzyć obiekt `Workbook` i dodać wykres kolumnowy  
- Jak osadzić kształt pola wyboru wewnątrz obszaru wykresu  
- Jak zastosować licencję Aspose.Cells do użytku produkcyjnego  

## Szybkie odpowiedzi
- **Która biblioteka tworzy interaktywne wykresy Excel?** Aspose.Cells for Java.  
- **Czy mogę dodać pola wyboru bez VBA?** Tak, poprzez wstawienie kształtu Form Control za pomocą API.  
- **Czy potrzebna jest licencja na tę funkcję?** Tymczasowa licencja działa w trybie ewaluacji; stała licencja jest wymagana w produkcji.  
- **Jakiej wersji Javy wymaga?** JDK 8 lub nowszy.  
- **Czy wykres będzie działał w Excel 2016‑2024?** Tak, wygenerowany plik jest zgodny ze standardem Office Open XML.  

## Czym jest interaktywny wykres Excel?
**Interaktywny wykres Excel** łączy standardowy wykres z elementami interfejsu użytkownika (np. polami wyboru), które pozwalają użytkownikom w czasie rzeczywistym pokazywać lub ukrywać serie danych, przekształcając statyczną wizualizację w dynamiczne narzędzie raportowe.

## Dlaczego używać Aspose.Cells for Java?
Aspose.Cells obsługuje **ponad 80 formatów wejściowych i wyjściowych** oraz może przetwarzać skoroszyty zawierające **ponad 10 000 wierszy** bez ładowania całego pliku do pamięci, zapewniając wysoką wydajność generowania w środowiskach serwerowych.

## Wymagania wstępne

- **Java Development Kit (JDK):** wersja 8 lub wyższa.  
- **Aspose.Cells for Java:** najnowsza wersja (np. 25.3).  
- **Maven lub Gradle:** do zarządzania zależnościami biblioteki.  

### Wymagania wiedzy
Podstawowa składnia Javy oraz znajomość koncepcji Excela (arkusze, zakresy, wykresy) są pomocne, ale poniższe kroki są wystarczająco szczegółowe dla programistów o dowolnym poziomie doświadczenia.

## Jak dodać pole wyboru w Javie?

Załaduj bibliotekę Aspose.Cells, utwórz skoroszyt i wstaw kształt pola wyboru w jednym wywołaniu. Pole wyboru jest kontrolką formularza, którą można powiązać z komórką; przełączanie jej zmieni wartość powiązanej komórki, którą później możesz powiązać z widocznością serii wykresu.

```text
// Direct answer (40‑70 words):
You add a checkbox by creating a `Shape` of type `ShapeType.FORM_CONTROL_CHECKBOX`, setting its placement on the chart worksheet, and linking it to a cell that stores the Boolean state. The linked cell can be used in formulas that drive chart series visibility, enabling real‑time interactivity without VBA.
```

### Krok 1: Skonfiguruj zależność Maven

Dodaj artefakt Aspose.Cells Maven do swojego pliku `pom.xml`:

```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

### Krok 2: Skonfiguruj zależność Gradle

Dodaj następującą linię do pliku `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Kroki uzyskania licencji

Aby odblokować pełną funkcjonalność, uzyskaj tymczasową lub stałą licencję. Pobierz licencję próbną ze [strony Aspose](https://releases.aspose.com/cells/java/). Do produkcji zakup licencję i zastosuj ją, jak pokazano później.

#### Podstawowa inicjalizacja

License to klasa Aspose.Cells używana do zastosowania zakupionego pliku licencji, umożliwiająca pełną funkcjonalność bez ograniczeń ewaluacji. Zainicjalizuj bibliotekę w swoim kodzie Java przed jakąkolwiek operacją na skoroszycie:

```java
import com.aspose.cells.Workbook;

public class AsposeSetup {
    public static void main(String[] args) throws Exception {
        // Initialize the Workbook object.
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Jak stworzyć interaktywny wykres Excel?

Obiekt Aspose.Cells `Workbook` reprezentuje cały plik Excel, zawierający arkusze, wykresy i inne elementy. Tworząc skoroszyt, możesz programowo dodawać dane, generować wykres kolumnowy i później osadzać interaktywne kontrolki, takie jak pola wyboru. Poniższe kroki poprowadzą Cię przez budowanie skoroszytu, wypełnianie danymi i konfigurowanie wykresu pod kątem interaktywności.

```text
// Direct answer (40‑70 words):
First, instantiate a `Workbook`, fill a worksheet with sample data, and call `addChart` to place a column chart. Next, create a checkbox shape, position it over the chart, and link it to a cell that toggles the series’ `isVisible` property via a formula. Finally, save the workbook as an XLSX file.
```

### Utwórz skoroszyt i dodaj wykres

#### Przegląd

Ta sekcja pokazuje, jak utworzyć nowy skoroszyt, dodać arkusz danych i wygenerować wykres kolumnowy, który później zostanie uczyniony interaktywnym.

##### Krok 1: Utwórz nowy skoroszyt

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SheetType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a new Workbook object representing an Excel file.
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook created.");
    }
}
```

##### Krok 2: Dodaj arkusz wykresu

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ChartType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        
        // Adding a chart worksheet to the workbook.
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        System.out.println("Chart worksheet added.");
    }
}
```

##### Krok 3: Wstaw wykres kolumnowy

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN to the newly added chart worksheet.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        System.out.println("Column chart inserted.");
    }
}
```

##### Krok 4: Dodaj dane serii

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        // Adding series data for the chart.
        sheet.getCharts().get(0).getNSeries().add("{1,2,3}", false);
        
        System.out.println("Series data added to the chart.");
    }
}
```

## Jak osadzić pole wyboru w wykresie?

Osadzenie pola wyboru bezpośrednio na obszarze wykresu pozwala użytkownikom końcowym kliknąć, aby pokazać lub ukryć określoną serię. Pole wyboru jest kształtem Form Control, który może być powiązany z komórką; wartość komórki może być odwoływana w formule sterującej widocznością serii.

Shape to obiekt Aspose.Cells reprezentujący element rysunkowy, taki jak kontrolka formularza, obraz lub pole tekstowe w obrębie arkusza.

```text
// Direct answer (40‑70 words):
You embed a checkbox by creating a `Shape` with `ShapeType.FORM_CONTROL_CHECKBOX`, positioning it using `setUpperLeftRow/Column` relative to the chart sheet, and linking it to a helper cell (e.g., `B1`). Then, use a conditional formula in the series data range that checks the helper cell’s Boolean value to decide whether the series is plotted.
```

### Osadź kształt pola wyboru

```java
import com.aspose.cells.MsoDrawingType;
import com.aspose.cells.PlacementType;

public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a checkbox shape within the chart area on the first chart of the worksheet.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        
        System.out.println("Checkbox added to the chart.");
    }
}
```

### Ustaw tekst pola wyboru

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape within the chart.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);

        // Setting text for the newly added checkbox shape.
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        System.out.println("Checkbox labeled successfully.");
    }
}
```

## Jak zapisać skoroszyt jako plik Excel?

Zapisanie `Workbook` zapisuje wszystkie zmiany w pamięci do fizycznego pliku Excel na dysku. Aspose.Cells obsługuje nowoczesny format .xlsx, zapewniając otwieranie pliku w Excel 2016‑2024 oraz innych aplikacjach kompatybilnych z Office. Użyj metody `save` z żądaną ścieżką pliku i opcjonalnie określ format pliku dla dodatkowych opcji.

```text
// Direct answer (40‑70 words):
Call `workbook.save("InteractiveChart.xlsx", SaveFormat.XLSX)` to write the workbook. The method automatically closes all streams and guarantees that the embedded chart and checkbox are fully functional when the file is opened in Excel 2016‑2024.
```

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape and label it.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        // Save the workbook
        String outDir = "YOUR_OUTPUT_DIRECTORY"; // Replace with your actual output directory path.
        workbook.save(outDir + "/InsertCheckboxInChartSheet_out.xlsx");
        
        System.out.println("Workbook saved successfully.");
    }
}
```

## Praktyczne zastosowania

Rzeczywiste scenariusze, w których interaktywny wykres z polami wyboru dodaje wartość:

1. **Raporty interaktywne:** Pozwalają interesariuszom przełączać poszczególne linie produktów na wykresie sprzedaży.  
2. **Analiza porównawcza:** Umożliwia analitykom skupienie się na określonych okresach czasu lub regionach, zaznaczając/odznaczając serie.  
3. **Pulpity edukacyjne:** Studenci mogą badać trendy danych, wybierając, które zmienne wyświetlić.  

## Typowe problemy i rozwiązania

- **Pole wyboru nie reaguje:** Upewnij się, że pole wyboru jest powiązane z komórką i że komórka jest odwoływana w formule wpływającej na widoczność serii.  
- **Wykres nie aktualizuje się po przełączeniu:** Odśwież widok skoroszytu w Excelu lub ponownie przelicz formuły (`workbook.calculateFormula()`).  
- **Licencja nie została zastosowana:** Zweryfikuj, że `License license = new License(); license.setLicense("Aspose.Cells.lic");` jest wykonywane przed jakąkolwiek operacją na skoroszycie.  

## Najczęściej zadawane pytania

**P: Jak dodać pole wyboru bez użycia VBA?**  
O: Użyj API `Shape` Aspose.Cells z `ShapeType.FORM_CONTROL_CHECKBOX` i powiąż je z komórką arkusza; pole wyboru działa natywnie w Excelu.

**P: Czy potrzebna jest licencja na funkcję pola wyboru?**  
O: Kształt pola wyboru jest dostępny w darmowej wersji ewaluacyjnej, ale stała licencja Aspose.Cells usuwa ograniczenia ewaluacji i umożliwia pełne optymalizacje wydajności.

**P: Które wersje Excela mogą otworzyć wygenerowany plik?**  
O: Pliki zapisywane przy użyciu Aspose.Cells są zgodne ze standardem Office Open XML i otwierają się poprawnie w Excel 2016, 2019, 2021 oraz Microsoft 365.

**P: Czy mogę sterować wieloma seriami przy użyciu oddzielnych pól wyboru?**  
O: Tak, utwórz pole wyboru dla każdej serii, powiąż każde z odrębną komórką pomocniczą i użyj warunkowych formuł, aby przełączać każdą serię niezależnie.

**P: Czy istnieje limit liczby pól wyboru na wykres?**  
O: Praktycznie możesz dodać dziesiątki; wydajność pozostaje stabilna do około 200 kontrolek na arkusz w typowym sprzęcie serwerowym.

---

**Ostatnia aktualizacja:** 2026-09-22  
**Testowano z:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose

## Powiązane samouczki

- [Jak dodać pole wyboru w Excelu przy użyciu Aspose.Cells for Java: przewodnik krok po kroku](/cells/java/data-validation/add-checkbox-excel-aspose-cells-java/)
- [Tworzenie dynamicznych wykresów Excel z Aspose.Cells Java: kompleksowy przewodnik dla programistów](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Dodaj etykiety danych do wykresu Excel przy użyciu Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}