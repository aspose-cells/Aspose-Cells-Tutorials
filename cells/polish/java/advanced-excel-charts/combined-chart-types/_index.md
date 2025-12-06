---
date: 2025-12-06
description: Dowiedz się, jak dodać serie danych, utworzyć połączone typy wykresów,
  zapisać skoroszyt Excel i wyeksportować wykres do formatu PNG przy użyciu Aspose.Cells
  for Java.
language: pl
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Dodaj serie danych, aby utworzyć wykres kombinowany przy użyciu Aspose.Cells
url: /java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj serię danych, aby utworzyć wykres kombinowany przy użyciu Aspose.Cells

W tym samouczku **dodasz serię danych** do skoroszytu Excel i nauczysz się, jak **tworzyć wykresy kombinowane** przy użyciu Aspose.Cells for Java. Przejdziemy przez każdy krok — od przygotowania skoroszytu, dodawania serii, dostosowywania legendy, po **zapisanie skoroszytu Excel** oraz eksport **wykresu do PNG**. Po zakończeniu będziesz mieć gotowy wykres kombinowany, który możesz osadzić w raportach lub pulpitach nawigacyjnych.

## Szybkie odpowiedzi
- **Która biblioteka tworzy wykresy kombinowane?** Aspose.Cells for Java  
- **Jak dodać serię danych?** Use `chart.getNSeries().add(...)`  
- **Czy mogę wyeksportować wykres jako obraz?** Yes, with `chart.toImage(...)` (PNG)  
- **W jakim formacie mogę zapisać skoroszyt?** Standard `.xlsx` (Excel)  
- **Czy potrzebna jest licencja do produkcji?** A valid Aspose.Cells license is required  

## Co oznacza **add data series** w Aspose.Cells?
Dodanie serii danych informuje wykres, które komórki zawierają wartości, które chcesz przedstawić. Każda seria może reprezentować linię, kolumnę lub inny typ wykresu, a możesz je mieszać, aby stworzyć **wykres kombinowany**.

## Dlaczego tworzyć **combined chart**?
Wykres kombinowany pozwala wyświetlać różne zestawy danych z odrębnymi reprezentacjami wizualnymi (np. seria liniowa na wykresie kolumnowym) w jednym widoku. Jest to idealne rozwiązanie do porównywania trendów z sumami, podkreślania korelacji lub dostarczania bogatszych wniosków w kompaktowym formacie.

## Wymagania wstępne
- Java Development Kit (JDK) 8 lub wyższy  
- Biblioteka Aspose.Cells for Java (pobierz z poniższego linku)  
- Podstawowa znajomość składni Java oraz koncepcji Excela  

## Rozpoczęcie

Najpierw pobierz bibliotekę Aspose.Cells for Java z oficjalnej strony:

[Pobierz Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Po dodaniu pliku JAR do classpathu projektu, możesz rozpocząć budowanie wykresu.

### Krok 1: Importuj klasy Aspose.Cells
```java
import com.aspose.cells.*;
```

### Krok 2: Utwórz nowy skoroszyt
```java
Workbook workbook = new Workbook();
```

### Krok 3: Uzyskaj dostęp do pierwszego arkusza
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Krok 4: Dodaj obiekt wykresu kombinowanego  
Zaczniemy od wykresu liniowego, a później dodamy inne serie, aby uzyskać efekt **combined chart**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Dodawanie danych do wykresu

Teraz, gdy kontener wykresu istnieje, musimy go zasilić danymi.

### Krok 5: Zdefiniuj zakresy danych i **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** Pierwszy parametr (`"A1:A5"`) jest zakresem dla pierwszej serii, a drugi (`"B1:B5"`) tworzy drugą serię, która zostanie połączona z pierwszą.

### Krok 6: Ustaw dane kategorii (oś X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Dostosowywanie wykresu

Dobry wykres opowiada historię. Dodajmy mu tytuły, etykiety osi i czytelną legendę.

### Krok 7: Ustaw tytuł wykresu i etykiety osi
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Krok 8: **Add legend chart** i dostosuj jej pozycję
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Zapisywanie i eksportowanie wykresu

Po dostosowaniu będziesz chciał **zapisać skoroszyt Excel** i także wygenerować obraz.

### Krok 9: Zapisz skoroszyt jako plik Excel
```java
workbook.save("CombinedChart.xlsx");
```

### Krok 10: Eksportuj **chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Metoda `chart.toImage` **generuje obrazy wykresu excel**, które mogą być używane na stronach internetowych, w raportach lub e‑mailach.

## Typowe problemy i rozwiązywanie

| Problem | Rozwiązanie |
|-------|----------|
| **Brak danych** | Sprawdź, czy zakresy komórek (`A1:A5`, `B1:B5`, `C1:C5`) rzeczywiście zawierają dane przed utworzeniem wykresu. |
| **Legenda zachodzi na wykres** | Ustaw `chart.getLegend().setOverlay(false)` lub przenieś legendę na inną pozycję (np. `RIGHT`). |
| **Plik obrazu jest pusty** | Upewnij się, że wykres ma co najmniej jedną serię i że `chart.toImage` jest wywoływane po wszystkich dostosowaniach. |
| **Zapisywanie powoduje wyjątek** | Sprawdź, czy masz uprawnienia do zapisu w docelowym katalogu i czy plik nie jest otwarty w Excelu. |

## Najczęściej zadawane pytania

**Q: Jak zainstalować Aspose.Cells for Java?**  
A: Pobierz plik JAR z oficjalnej strony i dodaj go do classpathu projektu. Link do pobrania: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Czy mogę tworzyć inne typy wykresów oprócz linii i kolumn?**  
A: Tak, Aspose.Cells obsługuje wykresy słupkowe, kołowe, punktowe, obszarowe i wiele innych. Zapoznaj się z dokumentacją API, aby zobaczyć pełną listę.

**Q: Czy wymagana jest licencja do użytku produkcyjnego?**  
A: Ważna licencja Aspose.Cells jest wymagana przy wdrożeniach produkcyjnych. Dostępna jest darmowa wersja próbna do oceny.

**Q: Jak mogę zmienić kolory poszczególnych serii?**  
A: Użyj `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (lub podobnej) po dodaniu serii.

**Q: Gdzie mogę znaleźć więcej przykładów kodu?**  
A: Obszerna dokumentacja i dodatkowe przykłady są dostępne na stronie referencyjnej Aspose: [here](https://reference.aspose.com/cells/java/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.Cells for Java 24.12  
**Author:** Aspose