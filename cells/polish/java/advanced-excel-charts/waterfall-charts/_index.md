---
date: 2025-12-10
description: Dowiedz się, jak stworzyć wykres wodospadowy w Javie przy użyciu Aspose.Cells.
  Przewodnik krok po kroku, jak dodać wykres do arkusza, dostosować go i zapisać skoroszyt
  jako XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Jak utworzyć wykres wodospadowy przy użyciu Aspose.Cells dla Javy
url: /pl/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Wykresy wodospadowe

## Wprowadzenie do wykresów wodospadowych przy użyciu Aspose.Cells for Java

W tym samouczku nauczysz się **tworzyć wykres wodospadowy** przy użyciu Aspose.Cells for Java. Wykresy wodospadowe są niezbędnym narzędziem w wizualizacji danych, ponieważ pozwalają zobaczyć skumulowany efekt serii wartości dodatnich i ujemnych. Niezależnie od tego, czy przygotowujesz sprawozdanie finansowe, raport wydajności sprzedaży, czy inną analizę opartą na danych, wykres wodospadowy może przekształcić surowe liczby w przejrzyste, praktyczne wnioski.

## Szybkie odpowiedzi
- **What is a waterfall chart?** Wizualizacja pokazująca, jak początkowa wartość jest zwiększana i zmniejszana przez serię wartości pośrednich, kończąc się ostatecznym wynikiem.  
- **Which library is used?** Aspose.Cells for Java.  
- **Do I need a license?** Darmowa wersja próbna wystarcza do rozwoju; do produkcji wymagana jest licencja komercyjna.  
- **Can I save the file as XLSX?** Tak – użyj `workbook.save("FileName.xlsx")`.  
- **Is it suitable for Java data visualization?** Absolutnie; Aspose.Cells oferuje bogate funkcje wykresów bez konieczności instalacji Office.

## Co to jest wykres wodospadowy?
Wykres wodospadowy wyświetla kolejno dodatnie i ujemne wkłady do wartości początkowej, pomagając zrozumieć, jak każdy element wpływa na ostateczny wynik.

## Dlaczego używać Aspose.Cells for Java do dodania wykresu wodospadowego?
- **No Microsoft Excel required** – generuj wykresy na dowolnym serwerze lub w potoku CI.  
- **Full control over formatting** – kolory, etykiety danych i osie można dostosować programowo.  
- **Supports multiple output formats** – XLSX, PDF, HTML i inne.  
- **High performance** – idealne dla dużych skoroszytów i automatycznych raportów.

## Wymagania wstępne

Zanim przejdziesz do kodu, upewnij się, że spełniasz następujące wymagania:

- Aspose.Cells for Java: Musisz mieć zainstalowane Aspose.Cells for Java. Możesz pobrać je [here](https://releases.aspose.com/cells/java/).

- Java Development Environment: Upewnij się, że Java jest zainstalowana w Twoim systemie.

Teraz rozpocznijmy tworzenie wykresu wodospadowego krok po kroku.

## Jak stworzyć wykres wodospadowy w Javie

### Krok 1: Importuj Aspose.Cells

```java
import com.aspose.cells.*;
```

Najpierw musisz zaimportować bibliotekę Aspose.Cells do swojego projektu Java. Biblioteka ta zapewnia rozbudowaną funkcjonalność pracy z plikami Excel, w tym tworzenie wykresów.

### Krok 2: Zainicjalizuj skoroszyt i arkusz

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Utwórz nowy skoroszyt i dodaj do niego arkusz. Użyjemy tego arkusza do wprowadzenia danych i **dodania wykresu do arkusza**.

### Krok 3: Wprowadź dane

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

W tym przykładzie mamy kategorie w kolumnie A oraz odpowiadające im wartości w kolumnie B. Możesz zastąpić te dane własnym zestawem.

### Krok 4: Utwórz wykres wodospadowy

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Dodaliśmy wykres wodospadowy do naszego arkusza, określiliśmy serię danych oraz dane kategorii. To kluczowy krok, który **dodaje wykres wodospadowy** do arkusza Dalsze dostosowanie wyglądu wykresu (kolory, etykiety danych itp.) można wykonać za pomocą właściwości obiektu `Chart`.

### Krok 5: Zapisz skoroszyt

```java
workbook.save("WaterfallChart.xlsx");
```

Zapisz skoroszyt do pliku. Przykład używa formatu XLSX, ale Aspose.Cells umożliwia także eksport do PDF, CSV i wielu innych formatów. Spełnia to wymaganie **save workbook xlsx**.

## Typowe problemy i rozwiązania

- **Chart appears blank** – Sprawdź, czy odwołania do zakresów danych (`B2:B6` i `A2:A6`) odpowiadają rzeczywistym komórkom zawierającym Twoje wartości i kategorie.  
- **Negative values not displayed correctly** – Upewnij się, że typ serii jest ustawiony na `ChartType.WATERFALL`; inne typy wykresów traktują wartości ujemne inaczej.  
- **File not opening in Excel** – Upewnij się, że używasz najnowszej wersji Aspose.Cells (ostatnie wydanie) oraz że rozszerzenie pliku pasuje do formatu (`.xlsx` dla Excela).

## Najczęściej zadawane pytania

### Jak mogę dostosować wygląd mojego wykresu wodospadowego?

Możesz dostosować wygląd wykresu wodospadowego, modyfikując takie właściwości jak kolory, etykiety danych i etykiety osi. Zapoznaj się z dokumentacją Aspose.Cells, aby uzyskać szczegółowe wskazówki.

### Czy mogę utworzyć wiele wykresów wodospadowych w tym samym arkuszu?

Tak, możesz utworzyć wiele wykresów wodospadowych w tym samym arkuszu, postępując zgodnie z tymi samymi krokami, używając różnych zakresów danych.

### Czy Aspose.Cells jest kompatybilny z różnymi środowiskami programistycznymi Javy?

Tak, Aspose.Cells for Java jest kompatybilny z różnymi środowiskami programistycznymi Javy, w tym Eclipse, IntelliJ IDEA i NetBeans.

### Czy mogę dodać dodatkowe serie danych do mojego wykresu wodospadowego?

Oczy możesz dodać więcej serii danych do wykresu wodospadowego, aby skutecznie przedstawić złożone scenariusze danych.

### Gdzie mogę znaleźć więcej zasobów i przykładów dla Aspose.Cells for Java?

Możesz przeglądać dokumentację Aspose.Cells for Java pod adresem [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) w celu uzyskania szczegółowych informacji i przykładów kodu.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.Cells for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}