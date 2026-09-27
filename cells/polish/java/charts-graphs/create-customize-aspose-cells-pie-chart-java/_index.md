---
date: '2026-09-27'
description: Dowiedz się, jak stworzyć pie chart java przy użyciu Aspose.Cells. Przewodnik
  krok po kroku, jak dostosować Excel pie chart, skonfigurować zależność Maven i generować
  profesjonalne charts.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Stwórz pie chart java przy użyciu Aspose.Cells dla Java. Dowiedz się,
  jak dostosować Excel pie chart, dodać zależność Maven i generować profesjonalne
  charts w kilka minut.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Stwórz pie chart java z Aspose.Cells – Pełny przewodnik Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Jak stworzyć pie chart java przy użyciu Aspose.Cells
url: /pl/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć wykres kołowy java z Aspose.Cells

## Wprowadzenie
Tworzenie **wykresu kołowego** programowo często przypomina układankę, szczególnie gdy potrzebna jest precyzyjna kontrola nad kolorami, legendami i tytułami. W tym przewodniku nauczysz się, jak **utworzyć wykres kołowy java** przy użyciu Aspose.Cells, a następnie dostosować wykres kołowy w Excelu do swojej marki lub stylu raportowania. Przejdziemy przez konfigurację środowiska, wypełnianie danych, generowanie wykresu i drobne poprawki wizualne — wszystko bez opuszczania IDE Java.

**Co się nauczysz**
- Dodaj **zależność Maven Aspose.Cells** do swojego projektu.
- Utwórz skoroszyt, wypełnij komórki danymi i wygeneruj wykres kołowy.
- Zastosuj niestandardowe kolory, tytuły i legendy do wykresu.
- Wyeksportuj skoroszyt do pliku XLSX gotowego do udostępnienia.

Zanim rozpoczniesz, powinieneś być zaznajomiony z podstawową składnią Java i mieć zainstalowany Maven lub Gradle.

## Szybkie odpowiedzi
- **Która biblioteka tworzy wykresy kołowe w Javie?** Aspose.Cells for Java.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w fazie rozwoju; płatna licencja jest wymagana w produkcji.  
- **Jakie współrzędne Maven są wymagane?** `com.aspose:aspose-cells:24.10`.  
- **Czy mogę zmienić kolory segmentów?** Tak, za pomocą metody `setAreaColor` dla każdej serii.  
- **Czy wykres można wyeksportować do XLSX?** Oczywiście — wystarczy wywołać `workbook.save("output.xlsx")`.

## Czym jest wykres kołowy w Excelu?
Wykres kołowy wizualizuje pojedynczą serię danych jako proporcjonalne kawałki koła, co ułatwia porównanie części całości. Kąt każdego kawałka odpowiada jego wartości w stosunku do sumy, umożliwiając szybki wgląd w rozkład wśród kategorii, takich jak udział rynkowy, podział budżetu czy procenty demograficzne.

## Dlaczego używać Aspose.Cells do tworzenia wykresu kołowego java?
Aspose.Cells obsługuje ponad 50 typów wykresów i może obsługiwać arkusze z aż do miliona wierszy bez ładowania całego pliku do pamięci. Ta przewaga wydajnościowa pozwala generować duże raporty na skromnym sprzęcie, jednocześnie oferując precyzyjną kontrolę nad wyglądem wykresu, powiązaniem danych i formatami eksportu, co czyni go lepszym wyborem niż wiele bibliotek open‑source.

## Wymagania wstępne
- **Java Development Kit (JDK)** 8 lub nowszy.
- **IDE** takie jak IntelliJ IDEA lub Eclipse.
- **Maven** lub **Gradle** do zarządzania zależnościami.
- Licencja **trial lub zakupiona Aspose.Cells**.

### Wymagane biblioteki i zależności
Dodaj artefakt Maven Aspose.Cells do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Lub równoważny Gradle:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Kroki uzyskania licencji
Aspose.Cells for Java jest komercyjny, ale możesz rozpocząć od wersji próbnej. Odwiedź [purchase page](https://purchase.aspose.com/buy), aby uzyskać tymczasowy klucz licencyjny.

## Konfiguracja Aspose.Cells dla Java
Najpierw upewnij się, że biblioteka znajduje się na classpath. Po dodaniu zależności możesz zainicjować API, jak pokazano poniżej.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Przewodnik implementacji

### Utwórz i skonfiguruj skoroszyt
Klasa `Workbook` reprezentuje cały plik Excel w pamięci.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Krok 1: utwórz instancję skoroszytu
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Tworzy nowy, pusty skoroszyt, który możesz od razu zacząć wypełniać.

### Uzyskaj dostęp lub modyfikuj komórki arkusza
`Worksheet` reprezentuje pojedynczy arkusz w skoroszycie, zawierający komórki, wiersze i kolumny.  
Zapiszesz dane napędzające wykres kołowy w arkuszu.

#### Krok 2: pobierz pierwszy arkusz i jego komórki
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Wypełnij komórki nazwami kategorii i wartościami, które wykres będzie wykorzystywał.

### Utwórz wykres kołowy
Obiekty `Chart` wizualizują dane w arkuszu i obsługują różne typy, takie jak kołowy, kolumnowy i liniowy.

#### Krok 3: dodaj wykres kołowy do arkusza
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Skonfiguruj serie i dane wykresu kołowego
`Series` definiuje zakres danych i formatowanie wykresu, łącząc komórki arkusza z elementami wizualnymi.

#### Krok 4: ustaw serie dla wykresu
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Skonfiguruj wygląd legendy i tytułu wykresu
`Legend` wykresu wyświetla nazwy serii i kolory, pomagając czytelnikom zidentyfikować każdy kawałek.

#### Krok 5: dostosuj legendę i tytuł wykresu
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Dostosuj kolory serii wykresu
`setAreaColor` ustawia kolor wypełnienia kawałka serii wykresu przy użyciu wartości RGB.

#### Krok 6: zmień kolory segmentów koła
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Automatyczne dopasowanie kolumn i zapis skoroszytu
`autoFitColumns` automatycznie dostosowuje szerokość kolumn do zawartości komórek.

#### Krok 7: dostosuj szerokość kolumn i zapisz plik
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Typowe przypadki użycia
- **Analiza demograficzna:** Pokazuje rozkład populacji w regionach.  
- **Raportowanie udziału rynkowego:** Wizualizuje udział każdego konkurenta w jednym spojrzeniu.  
- **Alokacja budżetu:** Podkreśla, jak środki są podzielone między departamenty.

## Rozważania dotyczące wydajności
- Zwolnij obiekty (`workbook.dispose()`), gdy nie są już potrzebne, aby zwolnić pamięć natywną.  
- Dla ogromnych zestawów danych użyj `WorkbookDesigner` do strumieniowego przetwarzania danych zamiast ładowania wszystkiego naraz.  
- Profiluj przy użyciu Java Flight Recorder, aby wykryć wąskie gardła w generowaniu wykresów.

## Najczęściej zadawane pytania

**P:** Czy mogę wygenerować wiele wykresów kołowych w tym samym skoroszycie?  
**O:** Tak, powtórz kroki tworzenia wykresu dla każdego zakresu danych; każdy wykres jest niezależny.

**P:** Czy Aspose.Cells obsługuje wykresy kołowe 3‑D?  
**O:** Tak; ustaw typ wykresu na `ChartType.PIE_3D` podczas dodawania wykresu.

**P:** Jak zastosować niestandardowy motyw do wszystkich wykresów?  
**O:** Użyj metody `Workbook.setDefaultTheme` przed tworzeniem jakichkolwiek wykresów.

**P:** Do jakich formatów plików mogę wyeksportować skoroszyt?  
**O:** Ponad 30 formatów, w tym XLSX, CSV, PDF i HTML.

**P:** Czy licencja jest wymagana przy komercyjnym wdrożeniu?  
**O:** Tak, ważna licencja usuwa znaki wodne wersji ewaluacyjnej i odblokowuje pełną funkcjonalność.

## Zakończenie
Masz teraz kompletny, od‑a‑do‑końca przepis na **create pie chart java** z Aspose.Cells. Postępując zgodnie z powyższymi krokami, możesz generować dopracowane wykresy kołowe w Excelu, dostosowywać kolory i tytuły oraz osadzać je w dowolnym procesie raportowania. Odkryj inne typy wykresów — kolumnowy, liniowy, radarowy — aby poszerzyć swój zestaw narzędzi do wizualizacji danych.

---

**Ostatnia aktualizacja:** 2026-09-27  
**Testowano z:** Aspose.Cells 24.10 for Java  
**Autor:** Aspose

## Powiązane samouczki

- [Dostosuj etykiety danych wykresu Excel przy użyciu Aspose.Cells dla Java&#58; Przewodnik krok po kroku](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Utwórz dynamiczne wykresy Excel przy użyciu Aspose.Cells Java&#58; Kompletny przewodnik dla programistów](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Utwórz i dostosuj skoroszyty Excel przy użyciu Aspose.Cells Java&#58; Przewodnik krok po kroku](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}