---
date: '2026-10-17'
description: Dowiedz się, jak ustawić kształt etykiet danych wykresu Excel w języku
  Java przy użyciu Aspose.Cells. Ten przewodnik pokazuje, jak szybko i efektywnie
  modyfikować etykiety wykresów Excel.
keywords:
- how to set shape
- modify excel chart labels
- customize chart data labels
- add data label shape
lastmod: '2026-10-17'
og_description: Dowiedz się, jak ustawić kształt etykiet danych wykresu Excel w języku
  Java przy użyciu Aspose.Cells. Ten przewodnik krok po kroku pomaga szybko modyfikować
  etykiety wykresów Excel.
og_image_alt: Guide showing how to set shape of Excel chart data labels using Aspose.Cells
  for Java
og_title: Jak ustawić kształt etykiet danych wykresu Excel w języku Java
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  headline: How to set shape of Excel chart data labels in Java
  type: TechArticle
- description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  name: How to set shape of Excel chart data labels in Java
  steps:
  - name: load your workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory. Use `new Workbook("input.xlsx")` to load the file
      you want to modify.
  - name: access the chart
    text: '`Worksheet` represents a single sheet within a workbook. `Worksheet ws
      = workbook.getWorksheets().get(0);` retrieves the first worksheet. `Chart` is
      an object that represents a chart embedded in a worksheet. `Chart chart = ws.getCharts().get(0);`
      obtains the first chart on that sheet.'
  - name: retrieve series and modify data labels
    text: '`Series` represents a data series plotted on a chart. Each `Series` object
      contains a `DataLabel` collection. `DataLabel` controls the appearance of a
      data label for a series. `DataLabelShapeType` is an enumeration of possible
      shapes for data labels. Call `series.getDataLabels().setShapeType(DataLab'
  - name: save your workbook
    text: After applying the shape, invoke `workbook.save("output.xlsx");` to write
      the changes back to disk.
  type: HowTo
- questions:
  - answer: Loop through each series in the chart and call `setShapeType` on the series’
      `DataLabel` object.
    question: How do I change the shape of multiple data labels at once?
  - answer: Yes. With proper memory management, it processes workbooks containing
      hundreds of thousands of rows without loading the entire file into memory.
    question: Can Aspose.Cells for Java handle large Excel files efficiently?
  - answer: Missing Maven dependencies, using an outdated library version, or providing
      an invalid license file are typical pitfalls.
    question: What are common issues when setting up Aspose.Cells?
  - answer: Set the shape type to `DataLabelShapeType.DEFAULT` to restore the original
      appearance.
    question: Is there a way to revert data label shapes to default?
  - answer: Iterate over `ws.getCharts()` and apply the same `setShapeType` logic
      to each chart’s series collection.
    question: How can I apply this customization to multiple charts in a workbook?
  type: FAQPage
tags:
- excel chart
- aspose.cells
- java chart customization
- data label shape
title: Jak ustawić kształt etykiet danych wykresu Excel w języku Java
url: /pl/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Opanowanie dostosowywania wykresów w Javie z Aspose.Cells: zmiana kształtów etykiet danych

## Wprowadzenie

Poprawa atrakcyjności wizualnej wykresów Excel jest kluczowa przy przygotowywaniu raportów lub pulpitów nawigacyjnych, szczególnie jeśli używasz Javy. Dzięki Aspose.Cells — potężnej bibliotece do zarządzania i manipulacji arkuszami kalkulacyjnymi — możesz **how to set shape** etykiet danych wykresu w kilku linijkach kodu. Ten samouczek poprowadzi Cię przez zmianę kształtu etykiet danych w wykresie Excel przy użyciu Aspose.Cells dla Javy. Po zakończeniu będziesz wiedział, jak:

- Uzyskać dostęp i modyfikować etykiety danych wykresu
- Ustawić niestandardowe kształty etykiet danych
- Zapisz zmiany w skoroszycie

## Szybkie odpowiedzi
- **Jaka jest podstawowa klasa do pracy z plikami Excel?** `Workbook` reprezentuje cały plik Excel w pamięci.  
- **Która metoda ustawia kształt etykiety?** `setShapeType(DataLabelShapeType shape)` na obiekcie `DataLabel`.  
- **Czy potrzebuję licencji do rozwoju?** Darmowa tymczasowa licencja działa w trybie oceny; pełna licencja jest wymagana w produkcji.  
- **Czy mogę zastosować kształt do wielu serii?** Tak — iteruj po każdej serii i wywołaj `setShapeType`.  
- **Czy to podejście jest kompatybilne z dużymi skoroszytami?** Aspose.Cells przetwarza wielostronicowe skoroszyty bez ładowania całego pliku do pamięci.

## Co oznacza how to set shape?
Fraza **how to set shape** odnosi się do konfigurowania wizualnego obrysu etykiety danych wykresu, takiego jak zamiana zwykłego prostokąta na dymek lub elipsę. Zmiana kształtu poprawia czytelność i podkreśla kluczowe punkty danych. Wybierając odpowiedni kształt, możesz wyróżnić etykietę, grupować powiązane punkty lub dopasować się do wytycznych marki korporacyjnej, co zwiększa ogólną czytelność wykresu.

## Dlaczego warto używać Aspose.Cells do dostosowywania etykiet wykresów?
Aspose.Cells obsługuje **ponad 50 formatów wejściowych i wyjściowych** — w tym XLSX, CSV, ODS i PDF — i może manipulować skoroszytami zawierającymi **do 1 miliona wierszy** bez wyczerpywania pamięci. Jego API pozwala programowo modyfikować wykresy, eliminując potrzebę ręcznych edycji w Excelu i zapewniając spójny styl w raportach automatycznych.

## Wymagania wstępne

- **Aspose.Cells for Java Library**: Wymagana wersja 25.3 lub nowsza.
- **Java Development Environment**: Zainstalowany JDK na komputerze.
- **IDE Setup**: Użyj IDE, takiego jak IntelliJ IDEA lub Eclipse, do pisania i uruchamiania kodu.

### Wymagane biblioteki i zależności

Dla użytkowników Maven, dodaj następującą zależność do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Użytkownicy Gradle powinni dodać to do swojego pliku `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Uzyskanie licencji

Aspose.Cells oferuje darmową licencję próbną, którą możesz uzyskać ze [strony tymczasowej licencji Aspose](https://purchase.aspose.com/temporary-license/). Pozwala to na pełny dostęp do wszystkich funkcji bez ograniczeń przez określony czas.

## Konfiguracja Aspose.Cells dla Javy

Gdy środowisko jest gotowe, skonfigurujmy Aspose.Cells. Oto jak rozpocząć:

### Kroki instalacji

1. **Pobierz bibliotekę**: Użyj Maven lub Gradle, jak pokazano powyżej.

2. **Konfiguracja licencji**:  
   - `License` jest klasą, która stosuje plik licencji Aspose.Cells, aby włączyć pełną funkcjonalność.  
   - Pobierz i zastosuj tymczasową licencję używając tego fragmentu kodu po zainicjowaniu obiektu `Workbook`:

    ```java
    License license = new License();
    license.setLicense("path/to/your/license/file");
    ```

3. **Podstawowa inicjalizacja**: Utwórz instancję `Workbook`, aby rozpocząć pracę z plikami Excel.

## Jak ustawić kształt etykiet danych w wykresie?

Załaduj swój skoroszyt, znajdź docelowy wykres i zastosuj pożądany kształt do jego etykiet danych. Poniższe bezpośrednie kroki pozwolą to zrobić w mniej niż minutę.

### Przewodnik krok po kroku

#### Krok 1: załaduj swój skoroszyt

Klasa `Workbook` jest obiektem najwyższego poziomu w Aspose.Cells, który reprezentuje pojedynczy plik Excel w pamięci. Użyj `new Workbook("input.xlsx")`, aby załadować plik, który chcesz zmodyfikować.

#### Krok 2: uzyskaj dostęp do wykresu

`Worksheet` reprezentuje pojedynczy arkusz w skoroszycie.  
`Worksheet ws = workbook.getWorksheets().get(0);` pobiera pierwszy arkusz.  
`Chart` jest obiektem reprezentującym wykres osadzony w arkuszu.  
`Chart chart = ws.getCharts().get(0);` uzyskuje pierwszy wykres na tym arkuszu.

#### Krok 3: pobierz serie i zmodyfikuj etykiety danych

`Series` reprezentuje serię danych wykreślaną na wykresie.  
Każdy obiekt `Series` zawiera kolekcję `DataLabel`.  
`DataLabel` kontroluje wygląd etykiety danych dla serii.  
`DataLabelShapeType` jest wyliczeniem możliwych kształtów etykiet danych.  
Wywołaj `series.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);`, aby ustawić kształt. Wyliczenie oferuje dziesiątki opcji, takich jak `RECTANGLE`, `CLOUD` i `WEDGE_ELLIPSE_CALLOUT`.

#### Krok 4: zapisz swój skoroszyt

Po zastosowaniu kształtu wywołaj `workbook.save("output.xlsx");`, aby zapisać zmiany na dysku.

## Porady dotyczące rozwiązywania problemów

- **Problemy ze ścieżką pliku**: Upewnij się, że ścieżka pliku jest absolutna lub poprawnie względna względem katalogu roboczego projektu.  
- **Niezgodność wersji biblioteki**: Upewnij się, że używasz Aspose.Cells w wersji 25.3 lub nowszej; starsze wersje nie posiadają metody `setShapeType`.  
- **Nieobsługiwane typy wykresów**: Niektóre starsze typy wykresów (np. radar) mogą nie udostępniać właściwości kształtu etykiet danych; przełącz się na obsługiwany typ wykresu, taki jak kolumnowy lub liniowy.

## Praktyczne zastosowania

1. **Raportowanie finansowe** – Podkreśl kluczowe marże zysku za pomocą etykiet w stylu dymka.  
2. **Treści edukacyjne** – Użyj etykiet w kształcie chmury, aby przyciągnąć uwagę do ważnych punktów danych w materiałach dydaktycznych.  
3. **Analiza marketingowa** – Zastosuj niestandardowe kształty, aby odróżnić wskaźniki wydajności kampanii na pulpitach nawigacyjnych.

Integracja Aspose.Cells z pipeline'ami danych lub systemami CRM pozwala automatycznie generować w pełni stylizowane raporty, redukując ręczną pracę i zapewniając wizualizacje zgodne z marką.

## Wskazówki dotyczące wydajności

Podczas pracy z dużymi plikami Excel:

- **Optymalizacja użycia pamięci**: Wywołaj `workbook.dispose();` po zapisaniu, aby szybko zwolnić zasoby natywne.  
- **Przetwarzanie wsadowe**: Przetwarzaj wykresy w grupach, a nie pojedynczo, aby zminimalizować narzut tworzenia obiektów.  
- **Efektywna obsługa danych**: Unikaj ciężkich obliczeń wewnątrz pętli iterujących tysiące wierszy; oblicz wartości wcześniej.

## Zakończenie

Teraz wiesz, **how to set shape** etykiet danych wykresu Excel w Javie przy użyciu Aspose.Cells. Ta możliwość nie tylko podnosi estetykę wykresów, ale także poprawia zrozumienie danych przez użytkowników końcowych. Poznaj dodatkowe opcje dostosowywania — takie jak kolory etykiet, czcionki i linie prowadzące — aby jeszcze bardziej udoskonalić wizualizacje.

W razie pytań lub potrzeb pomocy, odwołaj się do [forum wsparcia Aspose](https://forum.aspose.com/c/cells/9).

## Najczęściej zadawane pytania

**Q: Jak zmienić kształt wielu etykiet danych jednocześnie?**  
A: Przejdź pętlą po każdej serii w wykresie i wywołaj `setShapeType` na obiekcie `DataLabel` serii.

**Q: Czy Aspose.Cells dla Javy radzi sobie efektywnie z dużymi plikami Excel?**  
A: Tak. Przy odpowiednim zarządzaniu pamięcią przetwarza skoroszyty zawierające setki tysięcy wierszy bez ładowania całego pliku do pamięci.

**Q: Jakie są typowe problemy przy konfiguracji Aspose.Cells?**  
A: Brak zależności Maven, używanie przestarzałej wersji biblioteki lub podanie nieprawidłowego pliku licencji to typowe pułapki.

**Q: Czy istnieje sposób, aby przywrócić kształty etykiet danych do domyślnych?**  
A: Ustaw typ kształtu na `DataLabelShapeType.DEFAULT`, aby przywrócić pierwotny wygląd.

**Q: Jak zastosować tę personalizację do wielu wykresów w skoroszycie?**  
A: Iteruj po `ws.getCharts()` i zastosuj tę samą logikę `setShapeType` do kolekcji serii każdego wykresu.

## Zasoby

- [Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Pobierz Aspose.Cells dla Javy](https://releases.aspose.com/cells/java/)
- [Kup licencję](https://purchase.aspose.com/buy)
- [Darmowa licencja próbna](https://releases.aspose.com/cells/java/)
- [Licencja tymczasowa](https://purchase.aspose.com/temporary-license/)

---  

**Ostatnia aktualizacja:** 2026-10-17  
**Testowano z:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  



```java
Workbook wb = new Workbook("YOUR_DATA_DIRECTORY/sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```
```java
Worksheet ws = wb.getWorksheets().get(0);
Chart ch = ws.getCharts().get(0);
```
```java
Series srs = ch.getNSeries().get(0);
srs.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);
```
```java
wb.save("YOUR_OUTPUT_DIRECTORY/outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

## Powiązane samouczki

- [Modyfikacja etykiet danych wykresu Excel przy użyciu Aspose.Cells Java](/cells/java/charts-graphs/modify-excel-chart-data-labels-aspose-cells-java/)
- [Jak zmienić rozmiar etykiet w wykresach Excel przy użyciu Aspose.Cells dla Javy](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [Dodawanie etykiet do wykresów Excel przy użyciu Aspose Cells dla Javy](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}