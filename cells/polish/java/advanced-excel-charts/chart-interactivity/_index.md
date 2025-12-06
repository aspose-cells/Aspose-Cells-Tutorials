---
date: 2025-12-06
description: Dowiedz się, jak zmienić typ wykresu w Excelu i tworzyć interaktywne
  wykresy w Javie przy użyciu Aspose.Cells. Dodaj podpowiedzi do wykresu, etykiety
  danych oraz drill‑down, aby uzyskać bogatszą wizualizację danych.
language: pl
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Zmień typ wykresu w Excelu przy użyciu Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zmień typ wykresu Excel i dodaj interaktywność

## Wprowadzenie

Interaktywne wykresy dają Twoim raportom Excel nowy poziom wglądu, pozwalając użytkownikom na najeżdżanie, klikanie i eksplorowanie punktów danych bezpośrednio. W tym samouczku **zmienisz typ wykresu Excel** i **stworzysz interaktywne rozwiązania wykresów Java** przy użyciu Aspose.Cells for Java. Przejdziemy przez dodawanie podpowiedzi (tooltipów) do wykresu, etykiet danych oraz prostego hiperłącza drill‑down, aby Twoja publiczność mogła zagłębić się w liczby.

## Szybkie odpowiedzi
- **Jakiej biblioteki użyto?** Aspose.Cells for Java  
- **Czy mogę zmienić typ wykresu?** Tak – wystarczy zmodyfikować enum `ChartType` podczas tworzenia wykresu.  
- **Jak dodać podpowiedzi do wykresu?** Użyj API etykiet danych (`setHasDataLabels(true)`) i włącz wyświetlanie wartości.  
- **Czy obsługiwany jest drill‑down?** Możesz dołączyć hiperłącza do punktów danych, aby uzyskać podstawowe zachowanie drill‑down.  
- **Wymagania wstępne?** IDE Java, plik JAR Aspose.Cells oraz plik Excel z przykładowymi danymi.

## Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz następujące elementy:

- Środowisko programistyczne Java (zalecany JDK 8+)  
- Biblioteka Aspose.Cells for Java (pobierz z [tutaj](https://releases.aspose.com/cells/java/))  
- Przykładowy skoroszyt (`data.xlsx`) zawierający dane, które chcesz zwizualizować  

## Krok 1: Konfiguracja projektu Java

1. Utwórz nowy projekt Java w ulubionym IDE (IntelliJ IDEA, Eclipse itp.).  
2. Dodaj plik JAR Aspose.Cells do ścieżki kompilacji projektu lub zależności Maven/Gradle.

## Krok 2: Ładowanie danych

Aby pracować z wykresami, najpierw musisz wczytać skoroszyt do pamięci.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Krok 3: Tworzenie wykresu (i zmiana jego typu)

Możesz wybrać dowolny typ wykresu pasujący do Twojej analizy. Poniżej tworzymy **wykres kolumnowy**, ale możesz łatwo przełączyć się na wykres liniowy, kołowy lub słupkowy, zmieniając enum `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Wskazówka:** Aby **zmienić typ wykresu Excel**, zamień `ChartType.COLUMN` na `ChartType.LINE`, `ChartType.PIE` itp.

## Krok 4: Dodawanie interaktywności

### 4.1. Dodawanie podpowiedzi (Add Tooltips to Chart)

Podpowiedzi pojawiają się, gdy użytkownik najedzie na punkt danych. Poniższy kod włącza etykiety danych i wyświetla wartość jako podpowiedź.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Dodawanie etykiet danych

Etykiety danych zapewniają stałą wizualną wskazówkę bezpośrednio na wykresie. Możesz wyświetlać je jako dymki, aby zwiększyć czytelność.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Implementacja drill‑down (Hyperlink on a Data Point)

Prosty sposób na dodanie możliwości drill‑down polega na dołączeniu hiperłącza do konkretnego punktu. Kliknięcie punktu otwiera stronę internetową z szczegółowymi informacjami.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Krok 5: Zapisywanie skoroszytu

Po skonfigurowaniu wykresu zapisz skoroszyt, aby interaktywne funkcje zostały zachowane w pliku wyjściowym.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Typowe problemy i rozwiązania

| Problem | Rozwiązanie |
|-------|----------|
| **Podpowiedzi nie wyświetlają się** | Upewnij się, że `setHasDataLabels(true)` jest wywoływane przed konfiguracją `setShowValue(true)`. |
| **Hiperłącze nie klikalne** | Sprawdź, czy format wyjściowy obsługuje hiperłącza (np. XLSX, a nie CSV). |
| **Typ wykresu się nie zmienia** | Sprawdź ponownie, czy zmodyfikowałeś właściwy enum `ChartType` przy dodawaniu wykresu. |

## Najczęściej zadawane pytania

**Q: Jak mogę zmienić typ wykresu po jego utworzeniu?**  
A: Musisz utworzyć nowy wykres z żądanym `ChartType`. Aspose.Cells nie oferuje konwersji typu w miejscu, więc usuń stary wykres i dodaj nowy.

**Q: Czy mogę dostosować wygląd podpowiedzi?**  
A: Tak. Użyj właściwości `DataLabel`, takich jak `setFontSize`, `setFontColor` i `setBackgroundColor`, aby stylizować tekst podpowiedzi.

**Q: Jak obsłużyć interakcje użytkownika w aplikacji webowej?**  
A: Eksportuj skoroszyt do pliku HTML lub XLSX i użyj JavaScript po stronie klienta, aby przechwytywać zdarzenia kliknięcia na elementach wykresu.

**Q: Gdzie mogę znaleźć więcej przykładów i dokumentacji?**  
A: Odwiedź [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) po pełną listę klas i metod związanych z wykresami.

## Podsumowanie

Teraz wiesz, jak **zmienić typ wykresu Excel**, **tworzyć interaktywne rozwiązania wykresów Java** oraz wzbogacić je o podpowiedzi, etykiety danych i hiperłącza drill‑down przy użyciu Aspose.Cells for Java. Te ulepszenia sprawiają, że Twoje raporty Excel są znacznie bardziej angażujące i pouczające dla użytkowników końcowych.

---

**Ostatnia aktualizacja:** 2025-12-06  
**Testowano z:** Aspose.Cells for Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}