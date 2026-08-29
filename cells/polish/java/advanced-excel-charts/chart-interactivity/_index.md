---
date: 2026-08-21
description: Dowiedz się, jak dodać tooltips, data labels i zmienić chart type w wykresach
  Excel przy użyciu Aspose.Cells for Java – przewodnik krok po kroku z interaktywnymi
  przykładami.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Zmień Excel Chart Type
og_description: Dowiedz się, jak dodać tooltips, data labels i zmienić chart type
  w wykresach Excel przy użyciu Aspose.Cells for Java – przewodnik krok po kroku z
  interaktywnymi przykładami.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Jak dodać tooltips i data labels do wykresów Excel w Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Jak dodać tooltips i data labels do wykresów Excel w Java
url: /pl/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj etykiety danych do wykresu Excel i zmień typ wykresu – Aspose.Cells Java

Interaktywne wykresy zapewniają Twoim raportom Excel nowy poziom wglądu, a **jak dodać podpowiedzi** sprawia, że informacje są od razu czytelne. W tym samouczku nauczysz się, jak **dodać etykiety danych do wykresu Excel**, **zmienić typ wykresu** oraz tworzyć interaktywne rozwiązania w Javie przy użyciu Aspose.Cells. Pokażemy również, jak dodać podpowiedzi oraz prosty hiperłącze drill‑down, aby Twoi odbiorcy mogli dogłębnie eksplorować dane.

## Szybkie odpowiedzi
- **Jaka biblioteka jest używana?** Aspose.Cells for Java  
- **Czy mogę zmienić typ wykresu?** Tak – wystarczy zmodyfikować wyliczenie `ChartType` podczas tworzenia wykresu.  
- **Jak dodać podpowiedzi do wykresu?** Użyj API etykiet danych (`setHasDataLabels(true)`) i włącz wyświetlanie wartości.  
- **Czy obsługiwany jest drill‑down?** Możesz dołączyć hiperłącza do punktów danych, aby uzyskać podstawowe zachowanie drill‑down.  
- **Wymagania wstępne?** IDE Java, plik JAR Aspose.Cells oraz plik Excel z przykładowymi danymi.

## Co to jest dodawanie podpowiedzi?
**Dodawanie podpowiedzi** odnosi się do procesu włączania tekstu pojawiającego się po najechaniu, który wyświetla wartość punktu danych lub niestandardowe informacje na wykresie Excel. W Aspose.Cells jest to realizowane poprzez ustawienia etykiet danych wykresu. Podpowiedzi pomagają użytkownikom szybko zrozumieć dane bez zagracania wykresu i mogą być dostosowywane pod kątem czcionki, koloru i formatu.

## Dlaczego używać interaktywnych wykresów z Aspose.Cells?
Aspose.Cells obsługuje **ponad 50 formatów wejścia i wyjścia** — w tym XLSX, CSV, PDF i HTML — i może przetwarzać skoroszyty z **ponad 1 000 arkuszami** bez ładowania całego pliku do pamięci, zapewniając szybkie generowanie wykresów po stronie serwera dla raportowania korporacyjnego. Interaktywne wykresy umożliwiają również osadzanie hiperłączy, dynamiczne aktualizacje danych oraz eksport do formatów przyjaznych sieci, co czyni je idealnymi dla pulpitów nawigacyjnych i portali raportowych.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz następujące elementy:

- Środowisko programistyczne Java (zalecany JDK 8+)  
- biblioteka Aspose.Cells for Java (pobierz ze [strony pobierania Aspose.Cells for Java](https://releases.aspose.com/cells/java/))  
- Przykładowy skoroszyt (`data.xlsx`) zawierający dane, które chcesz zwizualizować  

## Krok 1: konfigurowanie projektu Java

1. Utwórz nowy projekt Java w swoim ulubionym IDE (IntelliJ IDEA, Eclipse itp.).  
2. Dodaj plik JAR Aspose.Cells do ścieżki kompilacji projektu lub zależności Maven/Gradle.

## Krok 2: ładowanie danych

Aby pracować z wykresami, najpierw potrzebujesz skoroszytu załadowanego do pamięci.

Klasa `Workbook` reprezentuje plik Excel, a `Worksheet` reprezentuje pojedynczy arkusz w tym pliku.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Jak zmienić typ wykresu w Aspose.Cells?

Utwórz nowy wykres z żądanym wyliczeniem `ChartType`; Aspose.Cells nie modyfikuje typu istniejącego wykresu w miejscu, więc musisz dodać nowy wykres odpowiedniego typu i opcjonalnie usunąć stary. Takie podejście zapewnia, że wszystkie serie i osie zostaną poprawnie odtworzone dla nowej reprezentacji wizualnej.

## Krok 3: tworzenie wykresu (i zmiana jego typu)

Możesz wybrać dowolny typ wykresu pasujący do Twojej analizy. Poniżej tworzymy **wykres kolumnowy**, ale możesz łatwo przełączyć się na wykres liniowy, kołowy lub słupkowy, zmieniając wyliczenie `ChartType`.

Obiekt `Chart` udostępnia metody konfigurowania wizualnej reprezentacji danych w arkuszu.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Porada:** Aby **zmienić typ wykresu Excel**, zamień `ChartType.COLUMN` na `ChartType.LINE`, `ChartType.PIE` itp.

## Jak dodać podpowiedzi do wykresu Excel?

Załaduj swój wykres, włącz etykiety danych i ustaw flagę `showValue`. Podpowiedź będzie wtedy wyświetlać wartość komórki źródłowej, gdy użytkownik najedzie na punkt danych w wygenerowanym pliku Excel lub widoku HTML. Możesz także dostosować czcionkę, kolor i tło podpowiedzi, aby pasowały do stylu raportu.

Klasa `DataLabel` kontroluje wygląd i zawartość etykiet danych, które również pełnią funkcję podpowiedzi.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## Krok 4: dodawanie interaktywności

### 4.1. Dodawanie podpowiedzi (dodaj podpowiedzi do wykresu)

Podpowiedzi pojawiają się, gdy użytkownik najedzie na punkt danych. Poniższy kod włącza etykiety danych i wyświetla wartość jako podpowiedź.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Dodawanie etykiet danych – **dodaj etykiety danych do wykresu Excel**

Etykiety danych zapewniają trwałą wskazówkę wizualną bezpośrednio na wykresie. Możesz wyświetlać je jako dymki, aby zwiększyć czytelność.

Klasa `DataLabel` kontroluje wygląd etykiet w każdej serii. Wywołując `setHasDataLabels(true)` i konfigurując właściwości takie jak `setShowValue(true)`, osadzasz wartość liczbową bezpośrednio na wykresie, co sprawia, że jest ona natychmiast widoczna bez żadnej interakcji. Dodatkowe opcje pozwalają wyświetlać nazwy serii, procenty lub własny tekst, aby uzyskać bogatszy kontekst.

> **Dlaczego dodawać etykiety danych?** Umieszczenie etykiet danych bezpośrednio na wykresie eliminuje potrzebę najeżdżania lub zgadywania wartości przez użytkowników, poprawiając przejrzystość raportu.

### 4.3. Implementacja drill‑down (hiperłącze na punkcie danych)

Prosty sposób na dodanie możliwości drill‑down to dołączenie hiperłącza do konkretnego punktu. Kliknięcie punktu otwiera stronę internetową z szczegółowymi informacjami.

Klasa `Hyperlink` dołącza klikalne łącze do elementu wykresu, umożliwiając nawigację drill‑down.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Jak dodać etykiety danych do wykresu Excel?

Klasa `DataLabel` kontroluje wygląd etykiet w każdej serii. Wywołując `setHasDataLabels(true)` i konfigurując właściwości takie jak `setShowValue(true)`, osadzasz wartość liczbową bezpośrednio na wykresie, co sprawia, że jest ona natychmiast widoczna bez żadnej interakcji. Dodatkowe opcje pozwalają wyświetlać nazwy serii, procenty lub własny tekst, aby uzyskać bogatszy kontekst.

## Krok 5: zapisywanie skoroszytu

Po skonfigurowaniu wykresu zapisz skoroszyt, aby interaktywne funkcje zostały zapisane w pliku wyjściowym.

Wywołanie `workbook.save` zapisuje zmodyfikowany skoroszyt do pliku w wybranym formacie.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Częste problemy i rozwiązania

| Problem | Rozwiązanie |
|-------|----------|
| **Podpowiedzi się nie wyświetlają** | Upewnij się, że `setHasDataLabels(true)` jest wywoływane przed konfigurowaniem `setShowValue(true)`. |
| **Hiperłącze nie jest klikalne** | Sprawdź, czy format wyjściowy obsługuje hiperłącza (np. XLSX, nie CSV). |
| **Typ wykresu się nie zmienia** | Sprawdź ponownie, czy zmodyfikowałeś właściwe wyliczenie `ChartType` przy dodawaniu wykresu. |

## Najczęściej zadawane pytania

**P: Jak mogę zmienić typ wykresu po jego utworzeniu?**  
O: Musisz utworzyć nowy wykres z żądanym `ChartType`. Aspose.Cells nie oferuje konwersji typu w miejscu, więc usuń stary wykres i dodaj nowy.

**P: Czy mogę dostosować wygląd podpowiedzi?**  
O: Tak. Użyj właściwości `DataLabel`, takich jak `setFontSize`, `setFontColor` i `setBackgroundColor`, aby stylizować tekst podpowiedzi.

**P: Jak obsłużyć interakcje użytkownika w aplikacji webowej?**  
O: Wyeksportuj skoroszyt do pliku HTML lub XLSX i użyj JavaScript po stronie klienta do przechwytywania zdarzeń kliknięcia na elementach wykresu.

**P: Gdzie mogę znaleźć więcej przykładów i dokumentacji?**  
O: Odwiedź [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/), aby uzyskać pełną listę klas i metod związanych z wykresami.

## Zakończenie

Teraz wiesz, jak **dodać etykiety danych do wykresu Excel**, **zmienić typ wykresu Excel**, **tworzyć interaktywne rozwiązania wykresów w Javie**, oraz wzbogacić je o podpowiedzi, etykiety danych i hiperłącza drill‑down przy użyciu Aspose.Cells for Java. Te ulepszenia sprawiają, że Twoje raporty Excel są znacznie bardziej angażujące i pouczające dla użytkowników końcowych.

---

**Ostatnia aktualizacja:** 2026-08-21  
**Testowano z:** Aspose.Cells for Java 24.12  
**Autor:** Aspose

## Powiązane samouczki

- [Jak modyfikować wykresy Excel i etykiety danych przy użyciu Aspose.Cells for Java](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Wyodrębnianie etykiet osi wykresu Excel przy użyciu Aspose.Cells Java: Kompletny przewodnik](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Tworzenie wykresów bąbelkowych w Excel przy użyciu Aspose.Cells for Java: Przewodnik krok po kroku](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}