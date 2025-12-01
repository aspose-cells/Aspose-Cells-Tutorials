---
date: 2025-12-01
description: Dowiedz się, jak zmienić typ wykresu w Excelu i dodać interaktywne funkcje,
  takie jak podpowiedzi, etykiety danych i drill‑down, korzystając z Aspose.Cells
  dla Javy.
language: pl
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Zmień typ wykresu w Excelu i dodaj interaktywność – Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zmień typ wykresu Excel i dodaj interaktywność

## Wprowadzenie

Interaktywne wykresy pozwalają odbiorcom na bieżąco eksplorować dane, a możliwość **zmiany typu wykresu Excel** daje elastyczność w prezentacji informacji w najbardziej efektywnym formacie wizualnym. W tym samouczku dowiesz się, jak używać Aspose.Cells for Java do zmiany typu wykresu, dodawania podpowiedzi (tooltipów), osadzania etykiet danych oraz tworzenia linków drill‑down — wszystko bez opuszczania kodu Java. Po zakończeniu będziesz posiadać w pełni funkcjonalny, interaktywny skoroszyt Excel, który możesz osadzić w raportach, dashboardach lub aplikacjach webowych.

## Szybkie odpowiedzi
- **Czy mogę zmienić typ wykresu programowo?** Tak – użyj wyliczenia `ChartType` podczas tworzenia lub aktualizacji wykresu.  
- **Jak dodać podpowiedzi do wykresu?** Włącz etykiety danych i ustaw `ShowValue` na true.  
- **Jaki jest najprostszy sposób na dodanie linków drill‑down?** Dołącz hiperłącze do punktu danych za pomocą `getHyperlinks().add(url)`.  
- **Czy potrzebna jest licencja na Aspose.Cells?** Bezpłatna wersja próbna wystarcza do rozwoju; licencja jest wymagana w środowisku produkcyjnym.  
- **Jaką wersję Javy obsługuje biblioteka?** Java 8 i nowsze są w pełni wspierane.

## Co oznacza „zmiana typu wykresu Excel”?

Zmiana typu wykresu polega na zamianie wizualnej reprezentacji (np. z wykresu kolumnowego na liniowy) przy zachowaniu niezmienionych danych źródłowych. Jest to przydatne, gdy odkryjesz, że inny wykres lepiej komunikuje trendy, porównania lub rozkłady.

## Dlaczego warto dodać interaktywność do wykresów Excel?

- **Lepszy wgląd w dane:** Podpowiedzi i etykiety danych pozwalają użytkownikom zobaczyć dokładne wartości bez przewijania.  
- **Atrakcyjne prezentacje:** Elementy interaktywne utrzymują zainteresowanie odbiorców.  
- **Możliwość drill‑down:** Hiperłącza umożliwiają przejście do szczegółowych arkuszy lub zasobów zewnętrznych.  
- **Ponowne wykorzystanie zasobów:** Jeden skoroszyt może obsługiwać wiele scenariuszy raportowych poprzez prostą zmianę typu wykresu.

## Wymagania wstępne

- Środowisko programistyczne Java (JDK 8+)  
- Biblioteka Aspose.Cells for Java (pobierz z [here](https://releases.aspose.com/cells/java/))  
- Przykładowy plik Excel (`data.xlsx`) zawierający dane, które chcesz zwizualizować

## Przewodnik krok po kroku

### Krok 1: Konfiguracja projektu Java

1. Utwórz nowy projekt Java w ulubionym IDE (IntelliJ IDEA, Eclipse, VS Code itp.).  
2. Dodaj plik JAR Aspose.Cells do ścieżki klas projektu.

### Krok 2: Załaduj źródłowy skoroszyt

Zaczynamy od wczytania istniejącego skoroszytu, który zawiera dane dla naszego wykresu.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Krok 3: Utwórz wykres i **zmień jego typ**

Poniżej tworzymy wykres kolumnowy, a następnie od razu pokazujemy, jak można przełączyć go na wykres liniowy, jeśli zajdzie taka potrzeba.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **Pro tip:** Zmiana typu wykresu po jego utworzeniu jest tak prosta, jak wywołanie `setChartType(...)`. Spełnia to główne słowo kluczowe **change Excel chart type** bez konieczności tworzenia nowego obiektu wykresu.

### Krok 4: Dodaj interaktywność

#### 4.1 Dodaj podpowiedzi do wykresu

Podpowiedzi wyświetlają się, gdy użytkownik najedzie kursorem na punkt danych. W Aspose.Cells są realizowane poprzez etykiety danych.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2 Dodaj etykiety danych (**add data labels chart**)

Etykiety danych mogą pokazywać dokładną wartość, nazwę kategorii lub oba te elementy. Tutaj używamy stylu dymku.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3 Implementuj drill‑down (**add drill down excel**)

Link drill‑down pozwala użytkownikom kliknąć punkt i przejść do szczegółowego widoku, zarówno wewnątrz skoroszytu, jak i na stronę internetową.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### Krok 5: Zapisz skoroszyt

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Typowe problemy i rozwiązania

| Problem | Przyczyna | Rozwiązanie |
|---------|-----------|--------------|
| Podpowiedzi się nie wyświetlają | `HasDataLabels` nie jest włączone | Upewnij się, że wywołano `setHasDataLabels(true)` przed konfiguracją `ShowValue`. |
| Link drill‑down nie działa | Nieprawidłowy format URL | Sprawdź, czy URL zaczyna się od `http://` lub `https://`. |
| Typ wykresu się nie zmienia | Używana starsza wersja Aspose.Cells | Zaktualizuj do najnowszej wersji (testowano z 24.12). |

## Najczęściej zadawane pytania

**Q: Jak mogę zmienić typ wykresu po jego utworzeniu?**  
A: Wywołaj `chart.setChartType(ChartType.YOUR_CHOICE)` na istniejącym obiekcie `Chart`. To bezpośrednio spełnia wymóg **change Excel chart type**.

**Q: Czy mogę dostosować wygląd podpowiedzi?**  
A: Tak. Użyj `chart.getNSeries().get(0).getPoints().getDataLabels()` aby ustawić rozmiar czcionki, kolor i tło.

**Q: Czy można dodać wiele linków drill‑down w jednym wykresie?**  
A: Oczywiście. Przejdź pętlą po punktach i wywołaj `getHyperlinks().add(url)` dla każdego punktu, który ma być połączony.

**Q: Czy Aspose.Cells obsługuje inne typy wykresów, takie jak kołowy czy radarowy?**  
A: Wszystkie typy wykresów zdefiniowane w wyliczeniu `ChartType` są obsługiwane, w tym `PIE`, `RADAR`, `AREA` itp.

**Q: Gdzie mogę znaleźć więcej przykładów?**  
A: Odwiedź oficjalną [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) po pełną listę metod związanych z wykresami.

## Zakończenie

Teraz wiesz, jak **zmienić typ wykresu Excel**, osadzić **podpowiedzi**, dodać **etykiety danych** oraz stworzyć linki **drill‑down** przy użyciu Aspose.Cells for Java. Te interaktywne funkcje przekształcają statyczne arkusze kalkulacyjne w dynamiczne narzędzia eksploracji danych, idealne do dashboardów, raportów i analiz webowych.

---

**Ostatnia aktualizacja:** 2025-12-01  
**Testowano z:** Aspose.Cells 24.12 for Java  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}