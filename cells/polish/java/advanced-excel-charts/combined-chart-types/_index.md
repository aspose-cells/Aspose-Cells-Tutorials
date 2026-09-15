---
date: 2026-02-14
description: Dowiedz się, jak wyeksportować wykres do formatu PNG, dodać serię danych,
  połączyć wykres liniowo‑słupkowy, zapisać skoroszyt jako XLSX oraz dodać legendę
  wykresu przy użyciu Aspose.Cells for Java.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: Eksportuj wykres do PNG i dodaj serię danych do wykresu kombinowanego
url: /pl/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Eksport wykresu do PNG i dodanie serii danych dla wykresu połączonego

W tym samouczku **add data series** do skoroszytu Excel, **combine line and column chart** elementy oraz dowiesz się, jak **export chart to PNG** przy użyciu Aspose.Cells for Java. Przejdziemy krok po kroku — od konfiguracji skoroszytu, dodania wykresu do arkusza, dostosowania legendy, po **save workbook as xlsx** i wygenerowanie obrazu PNG wykresu. Na końcu będziesz mieć gotowy wykres połączony, który możesz osadzić w raportach lub pulpitach nawigacyjnych.

## Szybkie odpowiedzi
- **Która biblioteka tworzy wykresy połączone?** Aspose.Cells for Java  
- **Jak dodać serię danych?** Use `chart.getNSeries().add(...)`  
- **Jak mogę wyeksportować wykres do png?** Call `chart.toImage("file.png", ImageFormat.getPng())`  
- **W jakim formacie pliku mogę zapisać skoroszyt?** Standard `.xlsx` (save workbook as xlsx)  
- **Czy potrzebuję licencji do produkcji?** A valid Aspose.Cells license is required  

## Co to jest **export chart to PNG** w Aspose.Cells?
Eksportowanie wykresu do PNG tworzy obraz rastrowy wykresu Excel, który może być wyświetlany na stronach internetowych, w raportach lub e‑mailach bez konieczności używania aplikacji Excel.

## Dlaczego tworzyć **combined line column chart**?
Wykres połączony pozwala wyświetlać różne zestawy danych przy użyciu odrębnych reprezentacji wizualnych (np. seria liniowa na serii słupkowej) w jednym widoku. Jest to idealne rozwiązanie do porównywania trendów z sumami, podkreślania korelacji lub dostarczania bogatszych informacji w kompaktowym formacie.

## Wymagania wstępne
- Java Development Kit (JDK) 8 lub nowszy  
- Biblioteka Aspose.Cells for Java (pobierz z poniższego linku)  
- Podstawowa znajomość składni Java i pojęć Excel  

## Rozpoczęcie

Najpierw pobierz bibliotekę Aspose.Cells for Java z oficjalnej strony:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Gdy plik JAR zostanie dodany do classpathu Twojego projektu, możesz rozpocząć tworzenie wykresu.

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

### Krok 4: Dodaj obiekt wykresu połączonego do arkusza  
Zaczniemy od wykresu liniowego, a później dodamy serię słupkową, aby uzyskać efekt **combined line column chart**.
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

### Krok 7: **Set chart axis labels** i tytuł
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

Po dostosowaniu będziesz chciał **save workbook as xlsx** i także wygenerować obraz.

### Krok 9: Zapisz skoroszyt jako plik Excel (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### Krok 10: **Export chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Metoda `chart.toImage` **generates excel chart** obrazy, które mogą być używane na stronach internetowych, w raportach lub e‑mailach.

## Typowe problemy i rozwiązywanie

| Problem | Rozwiązanie |
|---------|-------------|
| **Brak danych** | Sprawdź, czy zakresy komórek (`A1:A5`, `B1:B5`, `C1:C5`) rzeczywiście zawierają dane przed utworzeniem wykresu. |
| **Legenda nakłada się na wykres** | Ustaw `chart.getLegend().setOverlay(false)` lub przenieś legendę na inną pozycję (np. `RIGHT`). |
| **Plik obrazu jest pusty** | Upewnij się, że wykres ma co najmniej jedną serię i że `chart.toImage` jest wywoływane po wszystkich dostosowaniach. |
| **Zapisywanie powoduje wyjątek** | Sprawdź, czy masz uprawnienia do zapisu w docelowym katalogu oraz czy plik nie jest otwarty w Excelu. |

## Najczęściej zadawane pytania

**P: Jak zainstalować Aspose.Cells for Java?**  
A: Pobierz plik JAR z oficjalnej strony i dodaj go do classpathu swojego projektu. Link do pobrania: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**P: Czy mogę tworzyć inne typy wykresów oprócz liniowego i słupkowego?**  
A: Tak, Aspose.Cells obsługuje wykresy słupkowe, kołowe, punktowe, powierzchniowe i wiele innych typów wykresów. Zapoznaj się z dokumentacją API, aby zobaczyć pełną listę.

**P: Czy licencja jest wymagana do użytku produkcyjnego?**  
A: Wymagana jest ważna licencja Aspose.Cells do wdrożeń produkcyjnych. Dostępna jest bezpłatna wersja próbna do oceny.

**P: Jak mogę zmienić kolory poszczególnych serii?**  
A: Użyj `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (lub podobnego) po dodaniu serii.

**P: Gdzie mogę znaleźć więcej przykładów kodu?**  
A: Kompleksowa dokumentacja i dodatkowe przykłady są dostępne na stronie referencyjnej Aspose: [here](https://reference.aspose.com/cells/java/).

---

**Ostatnia aktualizacja:** 2026-02-14  
**Testowano z:** Aspose.Cells for Java najnowsza wersja  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}