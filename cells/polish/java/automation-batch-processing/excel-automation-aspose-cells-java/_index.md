---
date: '2026-07-21'
description: Dowiedz się, jak używać aspose cells maven do tworzenia skoroszytów Excel,
  dodawania wykresów i zapisywania plików w Javie, wraz z poradami dotyczącymi licencjonowania.
keywords:
- aspose cells maven
- aspose cells license
- create excel workbook java
- save excel java
lastmod: '2026-07-21'
og_description: Dowiedz się, jak używać aspose cells maven do tworzenia skoroszytów
  Excel, dodawania wykresów i zapisywania plików w Javie. Zawiera porady dotyczące
  licencjonowania oraz przewodnik krok po kroku.
og_image_alt: 'Developer guide: Create Excel workbook with charts using aspose cells
  maven in Java'
og_title: 'aspose cells maven: Automatyzuj skoroszyty Excel i wykresy w Javie'
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Learn how to use aspose cells maven to create Excel workbooks, add
    charts, and save files in Java with licensing tips.
  headline: 'aspose cells maven: Automate Excel Workbook & Charts in Java'
  type: TechArticle
- description: Learn how to use aspose cells maven to create Excel workbooks, add
    charts, and save files in Java with licensing tips.
  name: 'aspose cells maven: Automate Excel Workbook & Charts in Java'
  steps:
  - name: Instantiate a New Workbook Object
    text: The `Workbook` class is the top‑level object that holds all worksheets,
      styles, and charts.
  - name: Access the First Worksheet
    text: '`Worksheet` represents a single sheet inside the workbook; you can retrieve
      it via the `getWorksheets().get(0)` method.'
  - name: Populate Cells with Sample Data
    text: The `Cells` collection lets you write values directly to specific cell addresses.
      **Explanation** – This code creates a workbook, selects the first sheet, and
      writes a small data table that will later be visualized with a chart.
  - name: Ensure a Workbook Exists
    text: If you haven’t already, instantiate a `Workbook` as shown earlier.
  - name: Retrieve the First Worksheet
    text: Reuse the worksheet reference from the previous section.
  - name: Add Sample Data (if not already present)
    text: Populate the same cells to guarantee the chart has data to display.
  - name: Access the Chart Collection
    text: '`Charts` is a collection that holds all chart objects for a worksheet.'
  - name: Add and Configure a New Chart
    text: The `add` method creates a chart of the specified type (e.g., Pyramid) at
      the given cell range; `getNSeries()` then links the chart to the data source.
      **Explanation** – This snippet adds a Pyramid chart positioned at cells D5 to
      K20 and binds it to the data range A1:B5.
  - name: Assume the Workbook Is Populated
    text: All previous steps have prepared the workbook with data and a chart.
  - name: Save the Workbook
    text: Specify the output folder and filename; the library writes the file in native
      Excel format (`.xlsx`). **Explanation** – The `save` call persists the in‑memory
      workbook to a physical file, making it available for users, downstream processes,
      or further automation.
  type: HowTo
- questions:
  - answer: Yes. Use `workbook.getWorksheets().add()` to append additional sheets,
      each with its own data and charts.
    question: Can I create multiple worksheets in one workbook?
  - answer: Load the file with `new Workbook("existing.xlsx")`, modify cells or charts,
      then call `save` to overwrite or write a new file.
    question: How do I update an existing Excel file?
  - answer: Absolutely. The streaming mode processes files with **100,000+ rows**
      while keeping memory usage under **200 MB**.
    question: Is Aspose.Cells efficient with large data sets?
  - answer: Over **30** chart types, including Column, Line, Pie, Radar, Pyramid,
      and Funnel. See the official docs for the full list.
    question: Which chart types are supported?
  - answer: Purchase a perpetual license, a subscription, or request an extended temporary
      license via the Aspose portal.
    question: What licensing options are available for production?
  type: FAQPage
tags:
- aspose cells
- excel automation
- java
- maven
- licensing
title: 'aspose cells maven: Automatyzuj skoroszyty Excel i wykresy w Javie'
url: /pl/java/automation-batch-processing/excel-automation-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Opanowanie automatyzacji Excel: Tworzenie skoroszytu Excel i dodawanie wykresów przy użyciu Aspose.Cells Java

## Wprowadzenie

W dzisiejszym świecie napędzanym danymi, **aspose cells maven** pozwala automatyzować zadania Excel z poziomu Javy, redukując ręczną pracę i eliminując błędy ludzkie. Niezależnie od tego, czy tworzysz raporty finansowe, generujesz pulpity nawigacyjne, czy integrujesz arkusze kalkulacyjne z większą aplikacją Java, ten samouczek pokaże, jak stworzyć skoroszyt, wypełnić go, dodać wykresy i zapisać wynik — wszystko przy użyciu kilku linii kodu.

### Czego się nauczysz
- Jak skonfigurować Aspose.Cells dla Java przy użyciu Maven  
- Tworzenie skoroszytu Excel od podstaw  
- Wypełnianie arkuszy przykładowymi danymi  
- Dodawanie i konfigurowanie wykresów za pomocą kolekcji wykresów  
- Efektywne zapisywanie skoroszytu  

Gotowy zwiększyć wydajność? Zweryfikujmy, czy masz wszystko, czego potrzebujesz.

## Szybkie odpowiedzi
- **Który artefakt Maven dodaje Aspose.Cells?** `com.aspose:aspose-cells`  
- **Czy mogę dodawać wykresy bez zainstalowanego Excela?** Tak, Aspose.Cells działa całkowicie samodzielnie.  
- **Czy potrzebuję licencji do produkcji?** Ważna licencja Aspose.Cells jest wymagana do nieograniczonego użycia.  
- **Jakie formaty plików mogę eksportować?** Ponad 50 formatów, w tym XLSX, CSV, PDF i HTML.  
- **Czy obsługa strumieniowa jest dostępna dla dużych plików?** Tak, użyj API strumieniowego `WorkbookDesigner` dla skoroszytów wielostronicowych.

## Co to jest aspose cells maven?
`aspose cells maven` odnosi się do zależności Maven, która wprowadza bibliotekę Aspose.Cells dla Java do Twojego projektu, umożliwiając programową manipulację plikami Excel bez Microsoft Office. Dodając ten artefakt do swojego `pom.xml`, Maven automatycznie pobiera wymagane pliki JAR oraz zależności tranzytywne, co pozwala kompilować i uruchamiać kod tworzący, odczytujący i modyfikujący pliki Excel w pełni z poziomu Javy.

## Dlaczego warto używać Aspose.Cells dla Java?
Aspose.Cells for Java oferuje kompleksowy zestaw funkcji do tworzenia, edycji, konwersji i renderowania plików Excel bez wymogu posiadania Microsoft Office. Obsługuje ponad 50 formatów wejściowych i wyjściowych, zapewnia wysoką wydajność przy przetwarzaniu dużych skoroszytów oraz zaawansowane możliwości, takie jak generowanie wykresów, obliczanie formuł i formatowanie warunkowe, co czyni go idealnym rozwiązaniem dla raportowania klasy korporacyjnej i aplikacji opartych na danych.

## Wymagania wstępne

- **Aspose.Cells for Java** (użyjemy wersji 25.3)  
- **Java Development Kit (JDK)** – 8 lub nowszy  
- **IDE** – IntelliJ IDEA, Eclipse lub dowolny edytor, który preferujesz  

### Wymagane biblioteki

Dodaj zależność Maven lub Gradle do konfiguracji swojego projektu.

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
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```  

### Uzyskanie licencji

- **Free Trial** – przetestuj wszystkie funkcje bez kosztów.  
- **Temporary License** – wydłuż okres próbny dla większych ocen.  
- **Full License** – odblokuj nieograniczone użycie w produkcji.  

Uzyskaj tymczasową lub pełną licencję z [Aspose](https://purchase.aspose.com/temporary-license/).

## Konfigurowanie Aspose.Cells dla Java

Najpierw upewnij się, że biblioteka znajduje się na ścieżce klas, a następnie zastosuj licencję przy uruchamianiu aplikacji:

`License` to klasa, która ładuje i stosuje plik licencji Aspose.Cells, aby włączyć pełną funkcjonalność biblioteki.  
```java
License license = new License();
license.setLicense("path_to_your_license_file.lic");
```  

Po zastosowaniu licencji jesteś gotowy, aby rozpocząć tworzenie skoroszytów.

## Przewodnik implementacji

Przejdziemy przez trzy podstawowe funkcje: tworzenie skoroszytu, dodawanie wykresu i zapisywanie pliku. Każda sekcja zaczyna się od krótkiej, bezpośredniej odpowiedzi, po której następują szczegółowe kroki.

## Jak utworzyć nowy skoroszyt Excel przy użyciu Aspose.Cells?

`Worksheet` reprezentuje pojedynczy arkusz w skoroszycie, zawierający komórki, wiersze, kolumny i inne obiekty.  
Aby rozpocząć, zainicjuj klasę `Workbook`, która reprezentuje cały plik Excel w pamięci, wraz z jego arkuszami, stylami i wykresami. Ten pojedynczy obiekt zapewnia pełne API do dodawania danych, formatowania komórek i wstawiania elementów wizualnych. Po utworzeniu możesz od razu uzyskać dostęp do domyślnego arkusza, aby rozpocząć wypełnianie wierszy i kolumn.

### Krok 1: Utwórz nowy obiekt Workbook  
Klasa `Workbook` jest obiektem najwyższego poziomu, który przechowuje wszystkie arkusze, style i wykresy.  

```java
Workbook workbook = new Workbook();
```  

### Krok 2: Uzyskaj dostęp do pierwszego arkusza  
`Worksheet` reprezentuje pojedynczy arkusz w skoroszycie; możesz go pobrać za pomocą metody `getWorksheets().get(0)`.  

```java
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
```  

### Krok 3: Wypełnij komórki przykładowymi danymi  
Kolekcja `Cells` pozwala zapisywać wartości bezpośrednio pod konkretne adresy komórek.  

```java
Cells cells = sheet.getCells();

// Populate cell A1 with value 50
cells.get("A1").setValue(50);

// Continue for other cells...
cells.get("A2").setValue(100);
cells.get("A3").setValue(150);
cells.get("B1").setValue(4);
cells.get("B2").setValue(20);
cells.get("B3").setValue(50);
```  

**Wyjaśnienie** – Ten kod tworzy skoroszyt, wybiera pierwszy arkusz i zapisuje małą tabelę danych, która później zostanie zwizualizowana na wykresie.

## Jak dodać wykres do arkusza?

`Charts` jest kolekcją, która przechowuje wszystkie obiekty wykresów dla arkusza.  
Po wypełnieniu arkusza użyj jego kolekcji `Charts`, aby utworzyć nowy obiekt wykresu. Wybierz żądany typ wykresu, ustaw jego pozycję na arkuszu i powiąż go z zakresem komórek zawierających serię danych. Wykres jest renderowany natychmiast i może być dalej dostosowywany przy użyciu tytułów, legend i opcji stylizacji.

### Krok 1: Upewnij się, że istnieje skoroszyt  
Jeśli jeszcze tego nie zrobiłeś, zainicjuj `Workbook` jak pokazano wcześniej.  

```java
Workbook workbook = new Workbook();
```  

### Krok 2: Pobierz pierwszy arkusz  
Ponownie użyj referencji do arkusza z poprzedniej sekcji.  

```java
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
```  

### Krok 3: Dodaj przykładowe dane (jeśli nie są już obecne)  
Wypełnij te same komórki, aby zapewnić, że wykres ma dane do wyświetlenia.  

```java
Cells cells = sheet.getCells();

cells.get("A1").setValue(50);
cells.get("A2").setValue(100);
cells.get("A3").setValue(150);
cells.get("B1").setValue(4);
cells.get("B2").setValue(20);
cells.get("B3").setValue(50);
```  

### Krok 4: Uzyskaj dostęp do kolekcji wykresów  
`Charts` jest kolekcją, która przechowuje wszystkie obiekty wykresów dla arkusza.  

```java
ChartCollection charts = sheet.getCharts();
```  

### Krok 5: Dodaj i skonfiguruj nowy wykres  
Metoda `add` tworzy wykres określonego typu (np. Pyramid) w podanym zakresie komórek; `getNSeries()` następnie łączy wykres ze źródłem danych.  

```java
int chartIndex = charts.add(ChartType.PYRAMID, 5, 0, 15, 5);
Chart chart = charts.get(chartIndex);

// Set the data source for the chart series
SeriesCollection serieses = chart.getNSeries();
serieses.add("A1:B3", true); // 'true' means first row has headers
```  

**Wyjaśnienie** – Ten fragment dodaje wykres piramidalny umieszczony w komórkach od D5 do K20 i wiąże go z zakresem danych A1:B5.

## Jak zapisać plik Excel na dysku?

Gdy Twój skoroszyt jest w pełni przygotowany z danymi i wykresami, zapisz go na fizyczny plik przy użyciu metody `save`. Podaj docelową ścieżkę pliku i opcjonalnie określ format; Aspose.Cells wybiera odpowiedni zapis na podstawie rozszerzenia pliku. Operacja zapisuje skoroszyt w wybranym formacie, czyniąc go gotowym do dystrybucji lub dalszego przetwarzania.

### Krok 1: Załóż, że skoroszyt jest wypełniony  
Wszystkie poprzednie kroki przygotowały skoroszyt z danymi i wykresem.  

```java
Workbook workbook = new Workbook();
```  

### Krok 2: Zapisz skoroszyt  
Określ folder wyjściowy i nazwę pliku; biblioteka zapisuje plik w natywnym formacie Excel (`.xlsx`).  

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "CreateChart_out.xls");
```  

**Wyjaśnienie** – Wywołanie `save` utrwala skoroszyt w pamięci do fizycznego pliku, udostępniając go użytkownikom, procesom downstream lub dalszej automatyzacji.

## Praktyczne zastosowania

Aspose.Cells for Java błyszczy w wielu rzeczywistych scenariuszach:

1. **Financial Reporting** – Generuj miesięczne bilanse z dynamicznymi wykresami, które aktualizują się automatycznie z danych bazodanowych.  
2. **Inventory Management** – Twórz pulpity kontrolne poziomu zapasów i wizualizuj trendy w wielu magazynach.  
3. **Project Tracking** – Twórz wykresy Gantta i wykresy postępu bezpośrednio w plikach Excel do dystrybucji wśród interesariuszy.  

Możesz połączyć te rozwiązania z klientami JDBC lub REST w Javie, aby pobierać dane na żywo, a następnie pozwolić Aspose.Cells zająć się formatowaniem i tworzeniem wykresów.

## Rozważania dotyczące wydajności

- **Memory Management** – Niezwłocznie zwalniaj duże obiekty `Workbook`; użyj `dispose()` po zakończeniu.  
- **Streaming API** – `WorkbookDesigner` zapewnia API strumieniowe, które przetwarza duże skoroszyty przy niskim zużyciu pamięci. Dla skoroszytów przekraczających 1 000 wierszy włącz strumieniowanie, aby uniknąć ładowania całego pliku do RAM.  
- **Profiling** – Benchmarkuj przy użyciu `System.nanoTime()` Javy wokół krytycznych sekcji, aby wykryć wąskie gardła.  

Stosowanie się do tych praktyk zapewnia, że Twoja automatyzacja skaluje się płynnie.

## Najczęściej zadawane pytania

**Q: Czy mogę utworzyć wiele arkuszy w jednym skoroszycie?**  
A: Tak. Użyj `workbook.getWorksheets().add()`, aby dodać dodatkowe arkusze, każdy z własnymi danymi i wykresami.

**Q: Jak zaktualizować istniejący plik Excel?**  
A: Załaduj plik przy pomocy `new Workbook("existing.xlsx")`, zmodyfikuj komórki lub wykresy, a następnie wywołaj `save`, aby nadpisać lub zapisać nowy plik.

**Q: Czy Aspose.Cells jest wydajne przy dużych zestawach danych?**  
A: Absolutnie. Tryb strumieniowy przetwarza pliki z **100 000+ wierszami**, utrzymując zużycie pamięci poniżej **200 MB**.

**Q: Jakie typy wykresów są obsługiwane?**  
A: Ponad **30** typów wykresów, w tym Column, Line, Pie, Radar, Pyramid i Funnel. Zobacz oficjalną dokumentację, aby poznać pełną listę.

**Q: Jakie opcje licencjonowania są dostępne dla produkcji?**  
A: Kup licencję wieczystą, subskrypcję lub poproś o rozszerzoną licencję tymczasową poprzez portal Aspose.

## Zasoby

- **Dokumentacja**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Pobierz**: [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)  
- **Zakup**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Bezpłatna wersja próbna**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Licencja tymczasowa**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Forum wsparcia**: [Aspose Cells Forum](https://forum.aspose.com/c/cells/9)

---

**Ostatnia aktualizacja:** 2026-07-21  
**Testowano z:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose

## Powiązane samouczki

- [Utwórz skoroszyt i dodaj wykresy przy użyciu Aspose.Cells dla Java: Kompletny przewodnik](/cells/java/charts-graphs/create-workbook-add-charts-aspose-cells-java/)
- [Aspose.Cells Java: Tworzenie i zapisywanie skoroszytów Excel – Przewodnik krok po kroku](/cells/java/workbook-operations/aspose-cells-java-create-save-excel-workbooks/)
- [Automatyzacja Excel i przetwarzanie wsadowe – Samouczki dla Aspose.Cells Java](/cells/java/automation-batch-processing/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}