---
date: 2026-02-16
description: Dowiedz się, jak ustawić zakres danych wykresu i stworzyć wykres wodospadowy
  w Javie przy użyciu Aspose.Cells. Przewodnik krok po kroku, jak dodać wykres serii
  danych, dostosować go i wyeksportować do XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Ustaw zakres danych wykresu – wykres wodospadowy Aspose.Cells for Java
url: /pl/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Wykresy wodospadowe

## Introduction to Waterfall Charts using Aspose.Cells for Java

W tym samouczku nauczysz się, jak **set chart data range** i utworzyć **waterfall chart** przy użyciu Aspose.Cells for Java. Wykresy wodospadowe są niezbędnym narzędziem w wizualizacji danych, ponieważ pozwalają zobaczyć skumulowany efekt serii dodatnich i ujemnych wartości. Niezależnie od tego, czy przygotowujesz sprawozdanie finansowe, raport z wyników sprzedaży, czy inną analizę opartą na danych, wykres wodospadowy może przekształcić surowe liczby w jasne, praktyczne wnioski.

## Szybkie odpowiedzi
- **What is a waterfall chart?** Wizualizacja pokazująca, jak wartość początkowa jest zwiększana i zmniejszana przez serię wartości pośrednich, kończąc się sumą końcową.  
- **Which library is used?** Aspose.Cells for Java.  
- **Do I need a license?** Darmowa wersja próbna działa w środowisku deweloperskim; licencja komercyjna jest wymagana w produkcji.  
- **Can I save the file as XLSX?** Tak – użyj `workbook.save("FileName.xlsx")`.  
- **Is it suitable for Java data visualization?** Zdecydowanie; Aspose.Cells oferuje bogate funkcje wykresów bez konieczności instalacji Office.

## Co to jest wykres wodospadowy?

Wykres wodospadowy wyświetla kolejno dodatnie i ujemne wkłady do wartości początkowej, pomagając zrozumieć, jak każdy element wpływa na ostateczny wynik.

## Dlaczego warto używać Aspose.Cells for Java do dodania wykresu wodospadowego?
- **No Microsoft Excel required** – generuj wykresy na dowolnym serwerze lub w potoku CI.  
- **Full control over formatting** – kolory, etykiety danych i osie mogą być dostosowywane programowo.  
- **Supports multiple output formats** – XLSX, PDF, HTML i inne.  
- **High performance** – idealny dla dużych skoroszytów i automatycznego raportowania.

## Wymagania wstępne

Zanim przejdziemy do kodu, upewnij się, że masz następujące wymagania:

- Aspose.Cells for Java: Musisz mieć zainstalowane Aspose.Cells for Java. Możesz pobrać je z [here](https://releases.aspose.com/cells/java/).
- Java Development Environment: Upewnij się, że Java jest zainstalowana w twoim systemie.

Teraz rozpocznijmy tworzenie wykresu wodospadowego krok po kroku.

## Jak ustawić zakres danych wykresu dla wykresu wodospadowego w Javie

### Krok 1: Import Aspose.Cells

```java
import com.aspose.cells.*;
```

Najpierw musisz zaimportować bibliotekę Aspose.Cells do swojego projektu Java. Biblioteka ta zapewnia rozbudowaną funkcjonalność pracy z plikami Excel, w tym tworzenie wykresów.

### Krok 2: Inicjalizacja Workbook i Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Utwórz nowy skoroszyt i dodaj do niego arkusz. Użyjemy tego arkusza do wprowadzenia danych i **add chart to worksheet**.

### Krok 3: Wprowadzenie danych

Teraz wypełnijmy arkusz danymi, które chcemy przedstawić na wykresie wodospadowym.

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

W tym przykładzie mamy kategorie w kolumnie A oraz odpowiadające im wartości w kolumnie B. Możesz zastąpić te dane własnym zestawem danych.

### Krok 4: Utworzenie wykresu wodospadowego

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Dodaliśmy wykres wodospadowy do naszego arkusza, określiliśmy serię danych i dane kategorii. To kluczowy krok, który **adds waterfall chart** do twojego arkusza. Zauważ, że metoda `add` używa zakresu `"B2:B6"` – to miejsce, w którym **set chart data range** dla serii. Możesz dalej dostosować wygląd wykresu (kolory, etykiety danych itp.) używając właściwości obiektu `Chart`.

### Krok 5: Zapisanie skoroszytu

```java
workbook.save("WaterfallChart.xlsx");
```

Zapisz skoroszyt do pliku. Przykład używa formatu XLSX, ale Aspose.Cells umożliwia również **export excel pdf java**‑compatible pliki, takie jak PDF, CSV i wiele innych formatów. Spełnia to wymaganie **save workbook xlsx**.

## Typowe problemy i rozwiązania

- **Chart appears blank** – Zweryfikuj, czy odwołania do zakresu danych (`B2:B6` i `A2:A6`) odpowiadają rzeczywistym komórkom zawierającym twoje wartości i kategorie.  
- **Negative values not displayed correctly** – Upewnij się, że typ serii jest ustawiony na `ChartType.WATERFALL`; inne typy wykresów traktują wartości ujemne inaczej.  
- **File not opening in Excel** – Upewnij się, że używasz najnowszej wersji Aspose.Cells (najświeższego wydania) oraz że rozszerzenie pliku odpowiada formatowi (`.xlsx` dla Excela).

## Najczęściej zadawane pytania

### Jak mogę dostosować wygląd mojego wykresu wodospadowego?

Możesz dostosować wygląd wykresu wodospadowego, modyfikując właściwości takie jak kolory, etykiety danych i etykiety osi. Zapoznaj się z dokumentacją Aspose.Cells, aby uzyskać szczegółowe wskazówki.

### Czy mogę utworzyć wiele wykresów wodospadowych w tym samym arkuszu?

Tak, możesz utworzyć wiele wykresów wodospadowych w tym samym arkuszu, stosując te same kroki z różnymi zakresami danych.

### Czy Aspose.Cells jest kompatybilny z różnymi środowiskami programistycznymi Java?

Tak, Aspose.Cells for Java jest kompatybilny z różnymi środowiskami programistycznymi Java, w tym Eclipse, IntelliJ IDEA i NetBeans.

### Czy mogę dodać dodatkowe serie danych do mojego wykresu wodospadowego?

Oczywiście, możesz dodać więcej serii danych do wykresu wodospadowego, aby skutecznie przedstawić złożone scenariusze danych. To przykład, jak możesz **add data series chart** programowo.

### Gdzie mogę znaleźć więcej zasobów i przykładów dla Aspose.Cells for Java?

Możesz przeglądać dokumentację Aspose.Cells for Java pod adresem [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) w celu uzyskania szczegółowych informacji i przykładów kodu.

## FAQ

**Q: Jak ustawić zakres danych wykresu dla finansowego wykresu wodospadowego?**  
A: Użyj metody `add` na serii wykresu, przekazując zakres komórek zawierających twoje wartości, np. `"B2:B6"`.

**Q: Czy mogę wyeksportować skoroszyt do PDF zamiast XLSX?**  
A: Tak, wywołaj `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);`, aby uzyskać **export excel pdf java**‑compatible wyjście.

**Q: Co zrobić, jeśli potrzebuję utworzyć finansowy wykres wodospadowy z większą liczbą kategorii?**  
A: Rozszerz zakres danych zarówno w kolumnie wartości, jak i w kolumnie kategorii, a następnie odpowiednio zaktualizuj wywołania `add` i `setCategoryData`.

**Q: Czy istnieje sposób na automatyczne formatowanie dodatnich i ujemnych słupków?**  
A: Możesz iterować po kolekcji `Series` i ustawiać kolor `FillFormat` w zależności od znaku każdej wartości.

**Q: Czy Aspose.Cells obsługuje dynamiczne aktualizacje danych dla wykresów?**  
A: Tak, możesz modyfikować wartości komórek po utworzeniu wykresu; wykres odzwierciedli zmiany po zapisaniu skoroszytu.

---

**Ostatnia aktualizacja:** 2026-02-16  
**Testowano z:** Aspose.Cells for Java (latest)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}