---
date: 2026-02-09
description: Dowiedz się, jak dodać etykiety danych do wykresu Excel i zmienić typ
  wykresu przy użyciu Aspose.Cells for Java, a także jak dodać podpowiedzi i interaktywność
  typu drill‑down.
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Dodaj etykiety danych do wykresu Excel przy użyciu Aspose.Cells Java
url: /pl/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj etykiety danych do wykresu Excel i zmień typ wykresu – Aspose.Cells Java

Interaktywne wykresy nadają Twoim raportom Excel nowy poziom wglądu, a **dodawanie etykiet danych do wykresu Excel** sprawia, że informacje są od razu czytelne. W tym samouczku nauczysz się, jak **dodać etykiety danych do wykresu Excel**, zmienić typ wykresu oraz tworzyć interaktywne rozwiązania w Javie z Aspose.Cells. Pokażemy także, jak dodać podpowiedzi (tooltips) i prosty hiperlink drill‑down, aby odbiorcy mogli dogłębnie eksplorować dane.

## Szybkie odpowiedzi
- **Jakiej biblioteki użyto?** Aspose.Cells for Java  
- **Czy mogę zmienić typ wykresu?** Tak – wystarczy zmodyfikować wyliczenie `ChartType` podczas tworzenia wykresu.  
- **Jak dodać podpowiedzi do wykresu?** Użyj API etykiet danych (`setHasDataLabels(true)`) i włącz wyświetlanie wartości.  
- **Czy obsługiwany jest drill‑down?** Możesz dołączyć hiperłącza do punktów danych, aby uzyskać podstawowe zachowanie drill‑down.  
- **Wymagania wstępne?** IDE Java, plik JAR Aspose.Cells oraz plik Excel z przykładowymi danymi.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz następujące elementy:

- Środowisko programistyczne Java (zalecany JDK 8+)  
- Biblioteka Aspose.Cells for Java (pobierz z [tutaj](https://releases.aspose.com/cells/java/))  
- Przykładowy skoroszyt (`data.xlsx`) zawierający dane, które chcesz zwizualizować  

## Krok 1: Konfiguracja projektu Java

1. Utwórz nowy projekt Java w ulubionym IDE (IntelliJ IDEA, Eclipse itp.).  
2. Dodaj plik JAR Aspose.Cells do ścieżki kompilacji projektu lub zależności Maven/Gradle.

## Krok 2: Ładowanie danych

Aby pracować z wykresami, najpierw musisz załadować skoroszyt do pamięci.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Krok 3: Tworzenie wykresu (i zmiana jego typu)

Możesz wybrać dowolny typ wykresu pasujący do Twojej analizy. Poniżej tworzymy **wykres kolumnowy**, ale możesz łatwo przełączyć się na wykres liniowy, kołowy lub słupkowy, zmieniając wyliczenie `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Wskazówka:** Aby **zmienić typ wykresu Excel**, zamień `ChartType.COLUMN` na `ChartType.LINE`, `ChartType.PIE` itp.

## Krok 4: Dodawanie interaktywności

### 4.1. Dodawanie podpowiedzi (Add Tooltips to Chart)

Podpowiedzi pojawiają się, gdy użytkownik najedzie kursorem na punkt danych. Poniższy kod włącza etykiety danych i wyświetla wartość jako podpowiedź.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Dodawanie etykiet danych – **add data labels to excel chart**

Etykiety danych zapewniają stałą wskazówkę wizualną bezpośrednio na wykresie. Możesz wyświetlać je jako dymki, aby zwiększyć czytelność.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **Dlaczego dodawać etykiety danych?** Umieszczenie etykiet danych bezpośrednio na wykresie eliminuje potrzebę najazdu kursorem lub zgadywania wartości, poprawiając przejrzystość raportu.

### 4.3. Implementacja drill‑down (hiperłącze na punkcie danych)

Prosty sposób na dodanie możliwości drill‑down polega na dołączeniu hiperłącza do konkretnego punktu. Kliknięcie punktu otwiera stronę internetową ze szczegółowymi informacjami.

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

## Częste problemy i rozwiązania

| Problem | Rozwiązanie |
|-------|----------|
| **Podpowiedzi się nie wyświetlają** | Upewnij się, że `setHasDataLabels(true)` jest wywoływane przed skonfigurowaniem `setShowValue(true)`. |
| **Hiperłącze nie jest klikalne** | Sprawdź, czy format wyjściowy obsługuje hiperłącza (np. XLSX, nie CSV). |
| **Typ wykresu się nie zmienia** | Sprawdź ponownie, czy zmodyfikowałeś właściwe wyliczenie `ChartType` przy dodawaniu wykresu. |

## Najczęściej zadawane pytania

**P: Jak mogę zmienić typ wykresu po jego utworzeniu?**  
O: Musisz utworzyć nowy wykres z żądanym `ChartType`. Aspose.Cells nie oferuje konwersji typu w miejscu, więc usuń stary wykres i dodaj nowy.

**P: Czy mogę dostosować wygląd podpowiedzi?**  
O: Tak. Użyj właściwości `DataLabel`, takich jak `setFontSize`, `setFontColor` i `setBackgroundColor`, aby stylizować tekst podpowiedzi.

**P: Jak obsłużyć interakcje użytkownika w aplikacji webowej?**  
O: Wyeksportuj skoroszyt do pliku HTML lub XLSX i użyj JavaScript po stronie klienta, aby przechwycić zdarzenia kliknięcia na elementach wykresu.

**P: Gdzie mogę znaleźć więcej przykładów i dokumentacji?**  
O: Odwiedź [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/), aby uzyskać pełną listę klas i metod związanych z wykresami.

## Zakończenie

Teraz wiesz, jak **dodać etykiety danych do wykresu Excel**, **zmienić typ wykresu Excel**, **tworzyć interaktywne rozwiązania wykresów w Javie**, oraz wzbogacić je o podpowiedzi, etykiety danych i hiperłącza drill‑down przy użyciu Aspose.Cells for Java. Te ulepszenia sprawiają, że Twoje raporty Excel są znacznie bardziej angażujące i pouczające dla użytkowników końcowych.

---

**Ostatnia aktualizacja:** 2026-02-09  
**Testowano z:** Aspose.Cells for Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}