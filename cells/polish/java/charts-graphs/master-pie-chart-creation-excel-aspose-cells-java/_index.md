---
"date": "2025-04-07"
"description": "Dowiedz się, jak tworzyć i dostosowywać wykresy kołowe w programie Excel za pomocą Aspose.Cells for Java. Postępuj zgodnie z tym przewodnikiem krok po kroku, aby udoskonalić swoje umiejętności wizualizacji danych."
"title": "Tworzenie wykresów kołowych w programie Excel przy użyciu Aspose.Cells dla języka Java — kompleksowy przewodnik"
"url": "/pl/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Tworzenie wykresów kołowych w programie Excel przy użyciu Aspose.Cells dla języka Java
## Wstęp
Tworzenie angażujących i informacyjnych wykresów kołowych w programie Excel może przekształcić surowe dane w potężne spostrzeżenia, umożliwiając szybkie podejmowanie świadomych decyzji biznesowych. Masz problemy z wbudowanymi funkcjami programu Microsoft Excel lub szukasz skalowalnego rozwiązania, które bezproblemowo integruje się z aplikacjami Java? Aspose.Cells for Java jest tutaj, aby pomóc.

Ten samouczek przeprowadzi Cię przez proces tworzenia i dostosowywania wykresów kołowych w plikach Excela przy użyciu Aspose.Cells for Java. Dowiedz się, jak wydajnie dodawać dane, konfigurować elementy wykresu i finalizować skoroszyt — wszystko z łatwością i precyzją.

**Czego się nauczysz:**
- Konfigurowanie i używanie Aspose.Cells dla Java
- Tworzenie nowego skoroszytu i wypełnianie go przykładowymi danymi
- Dodawanie i dostosowywanie wykresów kołowych w arkuszu kalkulacyjnym programu Excel
- Najlepsze praktyki dotyczące konfiguracji i optymalizacji wykresów

Zacznijmy od omówienia warunków wstępnych.
## Wymagania wstępne
Zanim zaczniesz, upewnij się, że masz następujące rzeczy:
### Wymagane biblioteki, wersje i zależności
Sprawdź, czy w projekcie uwzględniono pakiet Aspose.Cells dla Java w wersji 25.3 lub nowszej, korzystając z Maven lub Gradle.
**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```
**Stopień:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```
### Wymagania dotyczące konfiguracji środowiska
- Pakiet Java Development Kit (JDK) zainstalowany w systemie.
- Zintegrowane środowisko programistyczne (IDE), takie jak IntelliJ IDEA, Eclipse lub NetBeans.
### Wymagania wstępne dotyczące wiedzy
Przydatna będzie podstawowa znajomość programowania w Javie i struktur plików programu Excel.
## Konfigurowanie Aspose.Cells dla Java
Aspose.Cells to potężna biblioteka, która umożliwia programistom tworzenie, modyfikowanie i renderowanie arkuszy kalkulacyjnych Excel w aplikacjach Java. Oto, jak możesz ją skonfigurować:
1. **Instalacja**: Dodaj zależność Maven lub Gradle, jak pokazano powyżej.
2. **Nabycie licencji**:
   - Uzyskaj bezpłatną licencję próbną do wstępnego testowania [Bezpłatna wersja próbna Aspose](https://releases.aspose.com/cells/java/).
   - Złóż wniosek o tymczasową licencję, aby przetestować pełne funkcje bez ograniczeń za pośrednictwem [Licencja tymczasowa](https://purchase.aspose.com/temporary-license/).
3. **Podstawowa inicjalizacja**: Zacznij od utworzenia instancji `Workbook` Klasa, która reprezentuje Twój plik Excel.
```java
import com.aspose.cells.Workbook;
// Utwórz i zainicjuj nowy skoroszyt
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook();
```
## Przewodnik wdrażania
Teraz wdrożymy każdą funkcję krok po kroku, aby utworzyć skoroszyt programu Excel z wykresem kołowym.
### 1. Tworzenie i inicjowanie skoroszytu
**Przegląd**:Zaczynamy od zainicjowania naszego `Workbook` obiekt i uzyskujemy dostęp do jego pierwszego arkusza kalkulacyjnego, w którym dodamy dane i wykresy.
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorksheetCollection;

String dataDir = "YOUR_DATA_DIRECTORY";
// Utwórz nową instancję skoroszytu
Workbook workbook = new Workbook();
// Uzyskaj dostęp do pierwszego arkusza w skoroszycie
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
```
### 2. Dodawanie przykładowych danych do komórek
**Przegląd**:Wypełnij arkusz przykładowymi danymi, które zostaną przedstawione na wykresie kołowym.
```java
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

Cells cells = sheet.getCells();
// Dodaj nazwy krajów w kolumnie A
Cell cell = cells.get("A1");
cell.setValue("Italy");
cell = cells.get("A2");
cell.setValue("Germany");
// Kontynuuj dla innych krajów...
// Dodaj odpowiednie dane sprzedaży w kolumnie B
cell = cells.get("B1");
cell.setValue(10000);
cell = cells.get("B2");
cell.setValue(20000);
// Kontynuuj, aby zobaczyć resztę danych...
```
### 3. Dodawanie wykresu kołowego do arkusza kalkulacyjnego
**Przegląd**:Wstaw wykres kołowy do arkusza kalkulacyjnego, używając wstępnie zdefiniowanych zakresów danych.
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;

ChartCollection charts = sheet.getCharts();
// Dodaj wykres kołowy w określonym miejscu i rozmiarze
int chartIndex = charts.add(ChartType.PIE, 15, 4, 40, 15);
Chart chart = charts.get(chartIndex);
```
### 4. Konfigurowanie serii wykresów
**Przegląd**:Zdefiniuj zakres danych dotyczących sprzedaży i kategorii (nazwy krajów), aby mieć pewność, że wykres kołowy dokładnie odzwierciedla zestaw danych.
```java
import com.aspose.cells.SeriesCollection;

SeriesCollection serieses = chart.getNSeries();
// Ustaw dane sprzedaży jako źródło danych wykresu
serieses.add("B1:B8", true);
// Określ dane kategorii (nazwy krajów)
serieses.setCategoryData("A1:A8");
// Włącz różne kolory dla każdego wycinka koła
serieses.setColorVaried(true);

// Aby wykres był bardziej przejrzysty, wyświetl na nim tabelę danych
chart.setShowDataTable(true);
```
### 5. Ustawianie tytułu i stylu wykresu
**Przegląd**:Dostosuj tytuł wykresu, aby zwiększyć jego czytelność i prezentację.
```java
import com.aspose.cells.Color;

// Ustaw tytuł wykresu za pomocą opcji stylizacji
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```
### 6. Konfigurowanie etykiet danych dla serii wykresów
**Przegląd**:Dodaj etykiety danych do każdego wycinka koła, zapewniając przejrzysty podział wartości.
```java
import com.aspose.cells.DataLabels;
import com.aspose.cells.LabelPositionType;

for (int i = 0; i < serieses.getCount(); i++) {
    DataLabels datalabels = serieses.get(i).getDataLabels();
    // Umieść etykiety wewnątrz podstawy każdego kawałka ciasta
    datalabels.setPosition(LabelPositionType.INSIDE_BASE);
    // Konfigurowanie opcji wyświetlania etykiet
    datalabels.setShowCategoryName(true);
    datalabels.setShowValue(true);
    datalabels.setShowPercentage(false);
    datalabels.setShowLegendKey(true);
}
```
### 7. Zapisywanie skoroszytu
**Przegląd**:Zakończ plik Excela, zapisując wszystkie dane i wykresy na dysku.
```java
import com.aspose.cells.SaveFormat;

String outDir = "YOUR_OUTPUT_DIRECTORY";
// Zapisz skoroszyt w pliku Excel
workbook.save(outDir + "/HTCPChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
## Zastosowania praktyczne
- **Analityka biznesowa**:Używaj wykresów kołowych w raportach sprzedaży w celu wizualizacji udziałów w rynku lub dystrybucji przychodów w poszczególnych regionach.
- **Narzędzia edukacyjne**:Tworzenie interaktywnych modułów edukacyjnych prezentujących rozkłady danych statystycznych.
- **Zarządzanie projektami**:Wizualne przedstawienie alokacji zasobów i wykorzystania budżetu interesariuszom.
## Rozważania dotyczące wydajności
Aby zoptymalizować wydajność:
- Zminimalizuj wykorzystanie pamięci poprzez efektywne zarządzanie rozmiarem skoroszytu.
- W przypadku pracy z rozległymi zbiorami danych należy wykorzystywać funkcje Aspose.Cells, takie jak strumieniowe przesyłanie dużych plików.
- Stosuj najlepsze praktyki języka Java dotyczące zarządzania pamięcią, aby zapewnić odpowiednie zwalnianie zasobów po ich wykorzystaniu.
## Wniosek
Dzięki temu przewodnikowi nauczyłeś się tworzyć, konfigurować i dostosowywać wykresy kołowe w programie Excel przy użyciu Aspose.Cells for Java. Ta potężna biblioteka umożliwia programistom bezproblemową integrację zaawansowanych funkcji arkusza kalkulacyjnego w aplikacjach Java.
Jeśli chcesz dowiedzieć się więcej, rozważ zapoznanie się z innymi typami wykresów lub rozszerz możliwości manipulowania danymi o dodatkowe funkcje oferowane przez Aspose.Cells.
## Sekcja FAQ
1. **Czy mogę używać Aspose.Cells za darmo?**
   - Tak, dostępna jest bezpłatna wersja próbna. Aby uzyskać pełny dostęp do funkcji bez ograniczeń, możesz ubiegać się o tymczasową licencję.
2. **Czy można tworzyć inne typy wykresów używając Aspose.Cells?**
   - Oczywiście! Możesz tworzyć wykresy słupkowe, wykresy liniowe i inne, dostosowując `ChartType`.
3. **Jak obsługiwać duże zbiory danych w programie Excel za pomocą języka Java?**
   - Stosuj wydajne techniki ładowania danych i rozważ przesyłanie strumieniowe bardzo dużych plików.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}