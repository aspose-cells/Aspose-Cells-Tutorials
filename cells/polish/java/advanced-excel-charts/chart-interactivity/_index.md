---
date: 2025-12-04
description: Dowiedz się, jak tworzyć interaktywne wykresy w Javie przy użyciu Aspose.Cells,
  dodawać podpowiedzi do wykresu oraz tworzyć wykresy drill‑down dla bogatszej wizualizacji
  danych.
language: pl
linktitle: Create Interactive Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Utwórz interaktywny wykres w Javie z Aspose.Cells
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie interaktywnego wykresu Java

## Wprowadzenie

Interaktywne wykresy dają użytkownikom możliwość przeglądania punktów danych, wyświetlania szczegółów po najechaniu oraz zagłębiania się w bardziej szczegółowe zestawy danych — wszystko bez opuszczania arkusza kalkulacyjnego. W tym samouczku nauczysz się **jak tworzyć interaktywne wykresy Java** przy użyciu Aspose.Cells. Przeprowadzimy Cię przez dodawanie podpowiedzi (tooltipów), etykiet danych oraz implementację funkcji drill‑down, aby Twoje wykresy stały się bardziej angażujące i informacyjne.

## Szybkie odpowied
- **Jakiej biblioteki używać?** Aspose.Cells for Java  
- **Czy mogę dodać podpowiedzi do wykresu?** Tak, przy użyciu API etykiet danych NSeries  
- **Czy obsługiwany jest drill‑down?** Tak, poprzez dołączanie hiperłączy do punktów danych  
- **Jakiiku jest tworzony?** Standardowy skoroszyt XLSX z osadzonymi wykresami  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna wystarcza do oceny; licencja komercyjna jest wymagana w produkcji  

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz- Środowisko programistyczne Java (zalecany JDK 8+)  
- Bibliotekę Aspose.Cells for Java (pobierz z oficjalnej [strony wydania Aspose](https://releases.aspose.com/cells/java/))  
- Przykładowy plik Excel o nazwie **data.xlsx** zawierający dane, które chcesz zwizualizować  

## Krok 1: Konfiguracja projektu Java

1. Utwórz nowy projekt Java w ulubionym IDE (IntelliJ IDEA, Eclipse, VS Code itp.).  
2. Dodaj plik JAR Aspose.Cells do classpath projektu — albo umieszczając JAR w folderze `libs`, albo dodając zależność Maven/Gradle.  

## Krok 2: Ładowanie danych

Aby zbudować interaktywny wykres, najpierw potrzebujesz arkusza z danymi. Poniższy fragment kodu otwiera istniejący skoroszyt i pobiera pierwszy arkusz.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Wskazówka:** Upewnij się, że zakres danych, który chcesz wykreślić, jest ciągły; Aspose.Cells automatycznie wykryje zakres po powiązaniu serii.  

## Krok 3: Tworzenie wykresu

Teraz tworzymy wykres kolumnowy i umieszczamy go w arkuszu. Możesz zmienić `ChartType.COLUMN` na inny typ (np. `ChartType.LINE`), jeśli wolisz inny styl wizualny.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Dlaczego to ważne:** Dodanie wykresu programowo daje pełną kontrolę nad jego rozmiarem, pozycją i źródłem danych, co jest niezbędne przy tworzeniu interaktywnych doświadczeń.  

## Krok 4: Dodawanie interaktywności

### Jak dodać podpowiedzi do wykresu

Podpowiedzi (lub etykiety danych wyświetlające wartości) pomagają użytkownikom natychmiast zobaczyć dokładną liczbę za każdym słupkiem. Poniższy kod włącza etykiety danych i konfiguruje ich wyświetlanie wartości.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### Jak dodać etykiety danych (callouty)

Jeśli chcesz, aby etykiety pojawiały się jako callouty zamiast zwykłego tekstu, zmień właściwość `ShowLabelAsDataCallout`.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### Jak dodać wykres drill‑down

Funkcja drill‑down pozwala użytkownikowi kliknąć punkt danych i przejść do powiązanego widoku szczegółowego — najczęściej realizowana za pomocą hiperłącza. Poniżej dołączamy URL do pierwszego punktu w serii.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Częsty błąd:** Pamiętaj, aby ustawić docelowy adres hiperłącza na stronę, która może wyświetlić szczegółowe dane (np. raport internetowy lub inny arkusz Excel). W przeciwnym razie kliknięcie spowoduje prowadzenie do nieistniejącego linku.  

## Krok 5: Zapisywanie skoroszytu

Po skonfigurowaniu wykresu zapisz skoroszyt. Powstały plik zawiera interaktywny wykres gotowy do otwarcia w Excelu lub dowolnym kompatybilnym przeglądarce.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Zakończenie

W tym przewodniku nauczyłeś się **jak tworzyć interaktywne wykresy Java** przy użyciu Aspose.Cells, obejmując:

- Ładowanie danych z istniejącego skoroszytu  
- Programowe tworzenie wykresu kolumnowego  
- Dodawanie podpowiedzi i etykiet danych typu callout  
- Implementację funkcji drill‑down za pomocą hiperłączy  
- Zapisywanie finalnego skoroszytu  

Te techniki przekształcają statyczne arkusze kalkulacyjne w dynamiczne, przyjazne użytkownikowi pulpity, które zwiększają zrozumienie danych i podejmowanie decyzji.

## Najczęściej zadawane pytania

**P: Jak mogę zmienić typ wykresu?**  
Odp: Zmodyfikuj enum `ChartType` w metodzie `add` (np. `ChartType.LINE` dla wykresu liniowego).

**P: Czy mogę dostosować wygląd podpowiedzi?**  
Odp: Tak, możesz dostosować rozmiar czcionki, kolor, tło i inne właściwości stylu za pomocą obiektu `DataLabels`.

**P: Jak obsłużyć interaktywność wykresu w aplikacji webowej?**  
Odp: Wyeksportuj skoroszyt do XLSX, a następnie użyj biblioteki wykresów JavaScript (np. Highcharts) do renderowania danych po stronie klienta lub osadź plik Excel w Office Web Viewer, który obsługuje hiperłącza.

**P: Gdzie mogę znaleźć więcej przykładów?**  
Odp: Odwiedź oficjalną [referencję API Aspose.Cells Java](https://reference.aspose.com/cells/java/), aby uzyskać pełną listę klas i metod związanych z wykresami.

**P: Czy potrzebna jest licencja do użytku produkcyjnego?**  
Odp: Tak, wymagana jest licencja komercyjna do wdrożenia; dostępna jest darmowa licencja ewaluacyjna do testów.

---

**Ostatnia aktualizacja:** 2025-12-04  
**Testowano z:** Aspose.Cells for Java 24.12 (najnowsza w momencie pisania)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}