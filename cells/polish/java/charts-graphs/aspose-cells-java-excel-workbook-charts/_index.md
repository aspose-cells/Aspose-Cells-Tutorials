---
date: '2026-04-11'
description: Naucz się automatyzacji Excela w Javie z Aspose.Cells. Ten tutorial pokazuje,
  jak utworzyć skoroszyt Excela w Javie, wypełnić dane w Excelu w Javie oraz zapisać
  plik Excela w Javie z wykresami.
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: 'Automatyzacja Excela w Javie: Tworzenie skoroszytów i wykresów przy użyciu
  Aspose'
url: /pl/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatyzacja Excel w Javie: Tworzenie skoroszytów i wykresów przy użyciu Aspose

## Wprowadzenie

Automatyzacja zadań w Excelu przy użyciu Javy może zaoszczędzić godziny ręcznej pracy, szczególnie gdy trzeba generować raporty, pulpity nawigacyjne lub wykresy oparte na danych w locie. **Excel automation java** z Aspose.Cells zapewnia czyste, wysokowydajne API, które obsługuje wszystko, od tworzenia skoroszytu po zaawansowane formatowanie wykresów. W tym samouczku nauczysz się, jak skonfigurować Aspose.Cells, **create an Excel workbook java**, wypełnić go danymi, dodać wykres, zastosować formatowanie 3‑D i w końcu **save the Excel file java**.

### Szybkie odpowiedzi
- **Which library simplifies Excel automation in Java?** Aspose.Cells for Java.  
- **Can I add 3‑D charts programmatically?** Yes – the API supports 3‑D formatting and lighting effects.  
- **Do I need a license for development?** A free trial license is available; a commercial license is required for production.  
- **What Java build tools are supported?** Maven and Gradle are both fully supported.  
- **What file formats can I export?** XLS, XLSX, CSV, PDF and many more.

## Co to jest automatyzacja Excel w Javie?

Automatyzacja Excel java odnosi się do procesu generowania, modyfikowania i zapisywania skoroszytów Excel programowo przy użyciu kodu Java. Eliminuje ręczną edycję arkuszy, zapewnia spójność i umożliwia integrację z innymi systemami, takimi jak bazy danych czy usługi internetowe.

## Dlaczego warto używać Aspose.Cells dla Javy?

- **Rich feature set** – od prostych wartości komórek po złożone wykresy, tabele przestawne i formatowanie warunkowe.  
- **No Microsoft Office dependency** – działa w dowolnym środowisku po stronie serwera.  
- **High performance** – zoptymalizowane pod kątem dużych zestawów danych i scenariuszy wielowątkowych.  
- **Broad format support** – odczyt/zapis XLS, XLSX, ODS, CSV, PDF, HTML i inne.

## Wymagania wstępne

- **Java Development Kit (JDK) 8+**  
- **Maven or Gradle** do zarządzania zależnościami  
- **Aspose.Cells for Java 25.3 or later** (trial or licensed)  

## Konfiguracja Aspose.Cells dla Javy

Dodaj bibliotekę do swojego projektu, używając jednej z poniższych konfiguracji.

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Uzyskanie licencji

Poproś o darmową licencję próbną na stronie Aspose lub zakup pełną licencję do użytku produkcyjnego. Umieść plik licencji w projekcie i załaduj go w czasie wykonywania.

## Podstawowa inicjalizacja i konfiguracja

Po rozwiązaniu zależności możesz rozpocząć kodowanie.

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## Przewodnik krok po kroku

### Krok 1: Jak utworzyć skoroszyt Excel w Javie

Utwórz nową instancję skoroszytu, która będzie zawierała wszystkie Twoje arkusze.

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### Krok 2: Dodaj arkusze (w tym arkusz wykresu)

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### Krok 3: Jak wypełnić dane w Excelu w Javie

Wstaw przykładowe dane, które będą referencją dla wykresu.

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### Krok 4: Dodaj wykres kolumnowy do skoroszytu

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### Krok 5: Zastosuj formatowanie kolorów w obszarze wykresu

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### Krok 6: Skonfiguruj legendę i serię danych

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### Krok 7: Zastosuj formatowanie 3D do serii

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### Krok 8: Ustaw kolory serii dla lepszej wizualnej odróżnialności

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### Krok 9: Jak zapisać plik Excel w Javie

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## Praktyczne zastosowania

- **Financial Reporting** – Generuj kwartalne sprawozdania z dynamicznymi wykresami.  
- **Data‑Analysis Dashboards** – Twórz interaktywne pulpity nawigacyjne, które odświeżają się automatycznie.  
- **Inventory Management** – Eksportuj poziomy zapasów i trendy do Excela do przeglądu przez interesariuszy.  
- **Project Planning** – Twórz wykresy w stylu Gantta bezpośrednio z systemów planowania opartych na Javie.

## Wskazówki dotyczące wydajności automatyzacji Excel w Javie

- **Reuse Workbook Objects** podczas przetwarzania wielu arkuszy, aby zmniejszyć zużycie pamięci.  
- **Batch Cell Updates** przy użyciu `Cells.importArray` dla dużych zestawów danych zamiast pojedynczych wywołań `putValue`.  
- **Dispose Resources** wywołując `book.dispose()` po zapisaniu dużych plików.

## Najczęściej zadawane pytania

**Q: Czy mogę wygenerować XLSX zamiast XLS?**  
A: Tak – po prostu zmień rozszerzenie pliku w `book.save("output.xlsx")`; Aspose automatycznie wybiera odpowiedni format.

**Q: Czy wymagana jest licencja do rozwoju?**  
A: Darmowa licencja próbna działa w fazie rozwoju i testowania. Wdrożenia produkcyjne wymagają zakupionej licencji.

**Q: Jak dodać więcej typów wykresów?**  
A: Użyj wyliczenia `ChartType` (np. `ChartType.PIE`, `ChartType.LINE`) przy wywoływaniu `charts.add(...)`.

**Q: Co zrobić, jeśli trzeba zabezpieczyć skoroszyt?**  
A: Wywołaj `book.getSettings().setPassword("yourPassword")` przed zapisem.

**Q: Czy Aspose.Cells obsługuje pliki z włączonymi makrami?**  
A: Tak – możesz tworzyć lub zachować makra VBA w skoroszytach XLSM.

---

**Last Updated:** 2026-04-11  
**Tested With:** Aspose.Cells 25.3 (Java)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}