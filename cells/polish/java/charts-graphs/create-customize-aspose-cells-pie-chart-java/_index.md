---
"date": "2025-04-08"
"description": "Naucz się tworzyć i dostosowywać wykresy kołowe za pomocą Aspose.Cells dla Java. Przewodnik krok po kroku z przykładami kodu dla programistów."
"title": "Opanowanie Aspose.Cells i tworzenie i dostosowywanie wykresów kołowych w Javie"
"url": "/pl/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Opanowanie Aspose.Cells: Tworzenie i dostosowywanie wykresów kołowych w Javie

## Wstęp
Tworzenie atrakcyjnych wizualnie wykresów jest powszechnym wymogiem przy wizualizacji danych w programie Excel. Niezależnie od tego, czy prezentujesz informacje demograficzne, czy analizujesz trendy rynkowe, wykresy kołowe oferują przejrzysty sposób na przedstawienie danych proporcjonalnych. Jednak programowe konfigurowanie tych wykresów może być skomplikowane. Ten samouczek przeprowadzi Cię przez proces tworzenia i dostosowywania wykresu kołowego Aspose.Cells przy użyciu języka Java, upraszczając proces dla programistów.

**Czego się nauczysz:**
- Skonfiguruj środowisko za pomocą Aspose.Cells dla Java.
- Utwórz nowy skoroszyt i uzyskaj dostęp do komórek arkusza kalkulacyjnego.
- Wprowadź dane do określonych komórek, aby przygotować się do utworzenia wykresu.
- Wygeneruj wykres kołowy na podstawie tych danych.
- Dostosuj wygląd wykresu kołowego, w tym kolory, tytuły i legendy.

Zanim zaczniesz, upewnij się, że masz podstawową wiedzę na temat programowania w Javie i zarządzania zależnościami Maven lub Gradle. Skonfigurujmy nasze środowisko!

## Wymagania wstępne
Aby skorzystać z tego samouczka, będziesz potrzebować:
- **Zestaw narzędzi programistycznych Java (JDK)**: Wersja 8 lub nowsza.
- **Zintegrowane środowisko programistyczne (IDE)**: Takie jak IntelliJ IDEA lub Eclipse.
- **Zarządzanie zależnościami**:Do zarządzania zależnościami używaj Maven lub Gradle.

### Wymagane biblioteki i zależności
Upewnij się, że w swoim projekcie uwzględniłeś Aspose.Cells for Java używając Maven lub Gradle.

**Maven**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Etapy uzyskania licencji
Aspose.Cells for Java to komercyjna biblioteka, ale możesz zacząć od bezpłatnej wersji próbnej lub ubiegać się o tymczasową licencję. Odwiedź [strona zakupu](https://purchase.aspose.com/buy) aby zbadać opcje licencjonowania.

## Konfigurowanie Aspose.Cells dla Java
Najpierw upewnij się, że środowisko Twojego projektu zawiera niezbędne biblioteki, dodając je za pomocą Maven lub Gradle, jak pokazano powyżej. Po dołączeniu możesz zainicjować Aspose.Cells:

```java
import com.aspose.cells.Workbook;

// Zainicjuj nową instancję skoroszytu
Workbook workbook = new Workbook();
```

## Przewodnik wdrażania

### Tworzenie i konfiguracja skoroszytu
Utworzenie skoroszytu to pierwszy krok, w którym skonfigurujesz swoje dane.

#### Importuj biblioteki
Upewnij się, że te importy znajdują się na górze pliku:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Krok 1: Utwórz instancję skoroszytu
```java
// Tworzy pustą instancję skoroszytu do pracy.
Workbook workbook = new Workbook();
```
Ten krok inicjuje plik Excela programowo, co pozwala na manipulowanie nim za pomocą funkcjonalności Aspose.Cells.

### Dostęp do komórek arkusza kalkulacyjnego lub ich modyfikacja
Następnie wprowadź dane do komórek arkusza kalkulacyjnego, które zostaną wykorzystane do utworzenia wykresu kołowego.

#### Krok 2: Dostęp do arkusza kalkulacyjnego i jego komórek
```java
// Otwórz pierwszy arkusz w skoroszycie.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Wprowadź przykładowe wartości użyte w wykresie kołowym do określonych komórek.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Wprowadź wartości procentowe wykresu kołowego do określonych komórek.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
Tutaj wypełniasz arkusz danymi, które będą reprezentować różne segmenty wykresu kołowego.

### Utwórz wykres kołowy

#### Krok 3: Dodaj wykres kołowy do arkusza kalkulacyjnego
```java
// Utwórz wykres kołowy w arkuszu kalkulacyjnym.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
Ten krok dodaje nowy wykres kołowy do arkusza kalkulacyjnego w określonych pozycjach i wymiarach.

### Konfigurowanie serii i danych wykresu kołowego

#### Krok 4: Ustaw serię dla wykresu
```java
// Skonfiguruj zakres danych serii dla wykresu.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Połącz tytuł wykresu kołowego z komórką zawierającą tekst tytułu.
pie.getTitle().setLinkedSource("D2");
```
Ten kod łączy zakres danych i tworzy serie dla wykresu kołowego.

### Konfigurowanie legendy wykresu i wyglądu tytułu

#### Krok 5: Dostosuj legendę i tytuł wykresu
```java
// Ustaw pozycję legendy na dole wykresu.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Ustaw właściwości czcionki dla tytułu wykresu.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
Możliwość dostosowania wyglądu zwiększa czytelność i atrakcyjność wizualną.

### Dostosuj kolory serii wykresów

#### Krok 6: Zmień kolory segmentów kołowych
```java
import com.aspose.cells.Color;

// Uzyskaj dostęp i dostosuj kolory poszczególnych segmentów wykresu kołowego.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
Ustawienia te personalizują wykres tak, aby pasował do określonych schematów kolorów.

### Automatyczne dopasowanie kolumn i zapisywanie skoroszytu

#### Krok 7: Dostosuj szerokości kolumn i zapisz plik
```java
// Automatyczne dopasowanie wszystkich kolumn.
worksheet.autoFitColumns();

// Zdefiniuj ścieżkę zastępczą katalogu wyjściowego, w którym zostanie zapisany skoroszyt.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Zapisz zmodyfikowany skoroszyt w pliku Excel w określonym katalogu.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
Na koniec dopasuj kolumny automatycznie i zapisz skoroszyt.

## Zastosowania praktyczne
1. **Analiza demograficzna**:Użyj wykresów kołowych do przedstawienia rozkładu populacji w różnych krajach lub regionach.
2. **Raporty o udziałach w rynku**:Zilustruj udziały rynkowe różnych firm w danym sektorze.
3. **Alokacja budżetu**:Zobacz, w jaki sposób budżety są rozdzielane w różnych działach organizacji.

Aplikacje te demonstrują wszechstronność i użyteczność pakietu Aspose.Cells w scenariuszach z życia wziętych.

## Rozważania dotyczące wydajności
Aby zoptymalizować wydajność podczas korzystania z Aspose.Cells:
- Zminimalizuj użycie pamięci poprzez usuwanie obiektów, które nie są już potrzebne.
- Wykorzystuj wydajne struktury danych do przetwarzania dużych zbiorów danych.
- Stwórz profil swojej aplikacji, aby zidentyfikować wąskie gardła.

Przestrzeganie najlepszych praktyk gwarantuje płynne działanie i responsywność aplikacji.

## Wniosek
Ten samouczek przeprowadził Cię przez kroki tworzenia i dostosowywania wykresu kołowego za pomocą Aspose.Cells w Javie. Dzięki tej wiedzy możesz teraz zastosować te techniki do różnych zadań wizualizacji danych w swoich projektach. Aby uzyskać dalsze informacje, rozważ zanurzenie się w dodatkowych typach wykresów i zaawansowanych opcjach dostosowywania dostępnych w Aspose.Cells.


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}