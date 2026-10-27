---
date: '2026-04-08'
description: Dowiedz się, jak tworzyć wykres liniowy z markerami przy użyciu Aspose.Cells
  for Java, dodać wykres do arkusza i dostosować wykresy Excela do automatycznego
  raportowania.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Utwórz wykres liniowy z markerami przy użyciu Aspose.Cells dla Javy
url: /pl/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie i stylowanie wykresów Excel przy użyciu Aspose.Cells Java

## Wprowadzenie

W dzisiejszym świecie napędzanym danymi, **wykres liniowy z markerami** jest jednym z najskuteczniejszych sposobów wizualizacji trendów i wartości odstających. Niezależnie od tego, czy tworzysz automatyczne raporty, czy pulpit nawigacyjny aktualizowany codziennie, możliwość programowego dodania wykresu liniowego z markerami do arkusza oszczędza niezliczone ręczne kroki. Ten samouczek przeprowadzi Cię przez użycie Aspose.Cells dla Javy do tworzenia, stylizacji i eksportu takich wykresów, abyś mógł skupić się na wnioskach zamiast na żmudnym manipulowaniu Excelem.

**Czego się nauczysz**
- Inicjalizacja skoroszytu i wypełnianie go danymi przy użyciu Aspose.Cells.  
- **Jak dodać wykres liniowy z markerami do arkusza** i skonfigurować jego wygląd.  
- Dostosowywanie kolorów serii, markerów i innych opcji stylizacji.  
- Zapisanie skoroszytu jako pliku Excel zawierającego stylizowany wykres.

## Szybkie odpowiedzi
- **Jaka jest podstawowa klasa do rozpoczęcia?** `Workbook` inicjalizuje nowy plik Excel.  
- **Który typ wykresu tworzy wykres liniowy z markerami?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **Jak ustawić niestandardowe kolory punktów serii?** Użyj `chart.getNSeries().setColorVaried(true)` i ustaw kolory obszaru markerów.  
- **Czy potrzebna jest licencja do pełnej funkcjonalności?** Tak, płatna lub tymczasowa licencja Aspose.Cells usuwa ograniczenia wersji próbnej.  
- **Czy mogę wyeksportować wynik jako XLSX?** Oczywiście—`workbook.save("StyledChart.xlsx")` tworzy plik XLSX.

## Wymagania wstępne

Zanim zaczniesz tworzyć i stylizować wykresy przy użyciu Aspose.Cells dla Javy, upewnij się, że masz następującą konfigurację:

### Wymagane biblioteki
Dołącz Aspose.Cells jako zależność w swoim projekcie. Oto instrukcje zarówno dla użytkowników Maven, jak i Gradle:

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Wymagania dotyczące konfiguracji środowiska
- Zainstalowany Java Development Kit (JDK) w systemie.  
- Zintegrowane środowisko programistyczne (IDE), takie jak IntelliJ IDEA lub Eclipse, do kodowania i testowania.

### Wymagania wiedzy
Wymagana jest podstawowa znajomość programowania w Javie, a także zaznajomienie się ze skoroszytami Excel i koncepcjami wykresów.

### Uzyskanie licencji
Aspose.Cells jest produktem komercyjnym, który wymaga licencji do pełnej funkcjonalności. Możesz uzyskać bezpłatną wersję próbną, aby ocenić jego funkcje, poprosić o tymczasową licencję do dłuższego testowania lub zakupić produkt do długoterminowego użytku.

- **Bezpłatna wersja próbna:** [Download Free Trial](https://releases.aspose.com/cells/java/)  
- **Licencja tymczasowa:** [Request Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Zakup:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)

## Konfiguracja Aspose.Cells dla Java

Po zainstalowaniu niezbędnych zależności skonfiguruj środowisko programistyczne do używania Aspose.Cells. Rozpocznij od zaimportowania biblioteki i zainicjalizowania obiektu `Workbook` w aplikacji Java:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Przewodnik implementacji

W tej sekcji podzielimy implementację na poszczególne funkcje: Inicjalizacja skoroszytu i wypełnianie danymi, Tworzenie i konfiguracja wykresu, Dostosowywanie serii oraz Zapis skoroszytu.

### Funkcja 1: Inicjalizacja skoroszytu i wypełnianie danymi

**Przegląd:** Ta funkcja koncentruje się na tworzeniu nowego skoroszytu, dostępnie do jego pierwszego arkusza oraz wypełnianiu go danymi do tworzenia wykresu.

#### Krok 1: Inicjalizacja skoroszytu
Rozpocznij od utworzenia obiektu `Workbook`:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Krok 2: Ustaw tytuły kolumn i wypełnij dane
Zdefiniuj nagłówki kolumn i wypełnij wiersze przykładowymi danymi:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Funkcja 2: Tworzenie i konfiguracja wykresu

**Przegląd:** Ta funkcja pokazuje, jak dodać wykres do arkusza skoroszytu, ustawić jego styl i skonfigurować podstawowe właściwości.

#### Krok 3: Dodaj wykres do arkusza
Dodaj wykres liniowy z markerami danych:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Funkcja 3: Konfiguracja i dostosowanie serii

**Przegląd:** Zwiększ atrakcyjność wizualną wykresów, dostosowując ustawienia serii, takie jak różnorodne kolory i style markerów.

#### Krok 4: Dostosuj ustawienia serii
Skonfiguruj dane serii, zastosuj niestandardowe formatowanie i dostosuj markery:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Funkcja 4: Zapis skoroszytu

**Przegląd:** Na koniec zapisz skoroszyt, aby zachować zmiany i zapewnić, że wykres zostanie uwzględniony w pliku Excel.

#### Krok 5: Zapisz skoroszyt
Zapisz swój skoroszyt wraz z nowo utworzonymi wykresami:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### Typowe problemy i rozwiązywanie

- **Wykres jest pusty:** Sprawdź, czy zakresy komórek użyte w `setXValues` i `setValues` prawidłowo odwołują się do wypełnionych komórek.  
- **Kolory nie są stosowane:** Upewnij się, że `chart.getNSeries().setColorVaried(true)` jest wywoływane przed dostosowywaniem poszczególnych serii.  
- **Błędy licencji:** Licencja próbna może ograniczać liczbę wykresów; zainstaluj pełną licencję, aby usunąć ograniczenia.

## Najczęściej zadawane pytania

**P: Czy mogę tworzyć inne typy wykresów (np. słupkowy, kołowy) przy użyciu Aspose.Cells?**  
O: Tak, Aspose.Cells obsługuje szeroką gamę typów wykresów; po prostu zamień `ChartType.LINE_WITH_DATA_MARKERS` na żądaną wartość wyliczeniową.

**P: Czy muszę zamykać skoroszyt lub zwalniać zasoby?**  
O: Klasa `Workbook` zarządza zasobami automatycznie, ale w długotrwale działających aplikacjach możesz wywołać `workbook.dispose()`, aby zwolnić pamięć.

**P: Czy można dodać wiele wykresów do tego samego arkusza?**  
O: Oczywiście—wywołaj `worksheet.getCharts().add(...)` dla każdego wykresu, który chcesz wstawić.

**P: Jak wyeksportować plik do starszego formatu Excel (XLS)?**  
O: Użyj `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`.

**P: Czy wykres zachowa styl po otwarciu w Microsoft Excel?**  
O: Tak, Aspose.Cells zapisuje natywne obiekty wykresów Excel, więc wszystkie style, kolory i markery pojawiają się dokładnie tak, jak zostały zdefiniowane.

---

**Ostatnia aktualizacja:** 2026-04-08  
**Testowano z:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}