---
date: '2026-09-02'
description: Dowiedz się, jak dodać slicer do skoroszytów Excel przy użyciu Aspose.Cells
  for Java, umożliwiając potężne filtrowanie danych, interaktywne pulpity oraz szybszą
  analizę.
keywords:
- how to add slicer
- load excel workbook java
- filter data excel slicer
- insert slicer worksheet
- aspose cells filtering
lastmod: '2026-09-02'
og_description: Jak dodać slicer do Excela przy użyciu Aspose.Cells for Java – przewodnik
  krok po kroku, który pokazuje, jak załadować skoroszyt, dołączyć interaktywny slicer
  i zapisać plik do dynamicznego raportowania.
og_image_alt: Developer guide showing Java code that adds an Excel slicer using Aspose.Cells
og_title: Jak dodać slicer do Excela przy użyciu Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to add slicer to Excel workbooks using Aspose.Cells for Java,
    enabling powerful data filtering, interactive dashboards, and faster analysis.
  headline: How to add slicer to Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to add slicer to Excel workbooks using Aspose.Cells for Java,
    enabling powerful data filtering, interactive dashboards, and faster analysis.
  name: How to add slicer to Excel with Aspose.Cells for Java
  steps:
  - name: '**Free trial:** Download the library and experiment with its capabilities.'
    text: '**Free trial:** Download the library and experiment with its capabilities.'
  - name: '**Temporary license:** Request a temporary license for extended testing
      at [Aspose''s Temporary License Page](https://purchase.aspose.com/temporary-license/).'
    text: '**Temporary license:** Request a temporary license for extended testing
      at [Aspose''s Temporary License Page](https://purchase.aspose.com/temporary-license/).'
  - name: '**Purchase license:** For production use, buy a full license from [Aspose
      Purchase](https://purchase.aspose.com/buy).'
    text: '**Purchase license:** For production use, buy a full license from [Aspose
      Purchase](https://purchase.aspose.com/buy).'
  - name: '**Financial reporting:** Filter quarterly sales figures with a single click
      to spot trends.'
    text: '**Financial reporting:** Filter quarterly sales figures with a single click
      to spot trends.'
  - name: '**Inventory management:** View stock levels by product category without
      rebuilding queries.'
    text: '**Inventory management:** View stock levels by product category without
      rebuilding queries.'
  - name: '**HR analytics:** Quickly compare employee performance across departments.'
    text: '**HR analytics:** Quickly compare employee performance across departments.'
  type: HowTo
- questions:
  - answer: Yes – call `worksheet.getSlicers().add` repeatedly with different column
      indexes or positions.
    question: Can I add multiple slicers to the same table?
  - answer: Absolutely – the same `add` method works with pivot tables as long as
      they exist on the worksheet.
    question: Does Aspose.Cells support slicers for PivotTables?
  - answer: You can modify properties such as `setStyle`, `setCaption`, `setWidth`,
      and `setHeight` after creation.
    question: Is it possible to customize slicer style programmatically?
  - answer: Aspose.Cells for Java 25.3 supports Java 8 and newer, including Java 11,
      17, and later LTS releases.
    question: What Java versions are compatible?
  - answer: Use `worksheet.getSlicers().removeAt(index)`, where `index` corresponds
      to the slicer’s position in the collection.
    question: How do I remove a slicer that is no longer needed?
  type: FAQPage
tags:
- add slicer
- Aspose.Cells
- Java Excel automation
- data filtering
- Excel slicer
title: Jak dodać slicer do Excela przy użyciu Aspose.Cells for Java
url: /pl/java/advanced-features/add-slicers-excel-aspose-cells-java-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak dodać segmentator do Excela przy użyciu Aspose.Cells dla Javy

## Wprowadzenie

W nowoczesnych aplikacjach opartych na danych **how to add slicer** do skoroszytów Excel jest częstym wymaganiem dla programistów potrzebujących interaktywnych, gotowych do filtrowania raportów. Aspose.Cells for Java pozwala programowo wstawiać segmentatory do tabel, dając użytkownikom końcowym taką samą możliwość kliknięcia‑i‑filtrowania, jaką oferuje interfejs desktopowy. W tym przewodniku zobaczysz, dlaczego segmentatory są ważne, jak skonfigurować bibliotekę oraz dokładny kod potrzebny do załadowania skoroszytu, dołączenia segmentatora i zapisania wyniku.

**Co się nauczysz**
- Jak wyświetlić aktualną wersję Aspose.Cells dla Javy  
- Jak **załadować skoroszyt Excel w Javie** i dotrzeć do docelowego arkusza  
- Jak znaleźć określoną tabelę i dodać segmentator  
- Jak używać segmentatora do **filtrowania danych w stylu Excel slicer**  
- Jak zapisać zmodyfikowany skoroszyt  

Zanim rozpoczniesz, upewnij się, że spełniasz poniższe wymagania wstępne.

## Szybkie odpowiedzi
- **Co to jest segmentator?** Interaktywny filtr wizualny, który pozwala użytkownikom natychmiast zawęzić dane w tabeli lub tabeli przestawnej.  
- **Która wersja Aspose.Cells jest wymagana?** Aspose.Cells for Java 25.3 lub nowsza.  
- **Czy potrzebna jest licencja?** Bezpłatna wersja próbna działa do oceny; licencja jest obowiązkowa w środowiskach produkcyjnych.  
- **Czy mogę załadować istniejący skoroszyt?** Tak – utwórz `new Workbook("path/to/file.xlsx")`.  
- **Czy segmentator zachowuje się jak natywny segmentator Excela?** Absolutnie – oferuje ten sam interfejs i możliwości filtrowania.

## Jak dodać segmentator do Excela przy użyciu Aspose.Cells dla Javy?

Aby dodać segmentator, najpierw załaduj docelowy skoroszyt, następnie utwórz obiekt segmentatora powiązany z wybraną kolumną tabeli, umieść segmentator na arkuszu i w końcu zapisz skoroszyt. Poniższe kroki szczegółowo opisują każde z tych działań, dostarczając fragmenty kodu do konfiguracji projektu, tworzenia segmentatora, jego umieszczania oraz zapisu pliku.

### Wymagania wstępne

Przed implementacją Aspose.Cells for Java upewnij się, że masz:

#### Wymagane biblioteki i wersje

Dołącz Aspose.Cells jako zależność przy użyciu Maven lub Gradle:

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

#### Wymagania dotyczące środowiska
- Zainstalowany Java Development Kit (JDK) 8 lub nowszy.  
- IDE, takie jak IntelliJ IDEA lub Eclipse, do edycji i uruchamiania kodu.

#### Wymagania dotyczące wiedzy
Podstawowa znajomość programowania w Javie jest wymagana; znajomość struktury plików Excel jest pomocna, ale nieobowiązkowa.

### Konfiguracja Aspose.Cells dla Javy

Najpierw uzyskaj wersję próbną lub stałą licencję z oficjalnej strony:

#### Kroki uzyskania licencji
1. **Bezpłatna wersja próbna:** Pobierz bibliotekę i przetestuj jej możliwości.  
2. **Licencja tymczasowa:** Poproś o tymczasową licencję do rozszerzonego testowania na [Stronie tymczasowej licencji Aspose](https://purchase.aspose.com/temporary-license/).  
3. **Zakup licencji:** Do użytku produkcyjnego kup pełną licencję na [Aspose Purchase](https://purchase.aspose.com/buy).

#### Podstawowa inicjalizacja
Zainicjuj Aspose.Cells w swojej aplikacji Java:
```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Set license if available
        License license = new License();
        license.setLicense("path/to/your/license/file.lic");

        System.out.println("Aspose.Cells is ready to use!");
    }
}
```
Po zainicjowaniu biblioteki jesteś gotowy do pracy z plikami Excel.

## Dlaczego używać segmentatorów w Excelu?

Segmentatory zapewniają natychmiastowe filtrowanie kliknięciem, bez konieczności pisania formuł czy kodu VBA. Poprawiają czytelność pulpitów, umożliwiają szybkie eksplorowanie danych i redukują potrzebę wielu statycznych raportów. W dużych wdrożeniach segmentatory mogą skrócić czas analizy nawet o 70 %, ponieważ użytkownicy nie muszą ręcznie odtwarzać zapytań.

## Filtrowanie danych przy użyciu segmentatora

Segmentatory to wizualny sposób **filter data with slicer**. Po podłączeniu do tabeli użytkownicy klikają przyciski segmentatora, aby natychmiast ukryć lub wyświetlić wiersze spełniające wybrane kryteria — bez potrzeby formuł. Ten rozdział wyjaśnia, dlaczego segmentatory są przełomem w interaktywnych raportach Excel.

## Przewodnik wdrożeniowy

Poniżej znajdziesz krok‑po‑kroku instrukcję, która pokazuje dokładnie, jak dodać segmentator do tabeli Excel.

### Wyświetlanie wersji Aspose.Cells dla Javy

Klasa `VersionInfo` udostępnia aktualną wersję biblioteki, co jest przydatne przy debugowaniu i wsparciu technicznym.

`VersionInfo` jest klasą pomocniczą zwracającą ciąg wersji Aspose.Cells.  
```java
System.out.println("Aspose.Cells version: " + com.aspose.cells.VersionInfo.getVersion());
```
Znajomość wersji pomaga zweryfikować, że używasz wydania obsługującego segmentatory (dostępne od wersji 20.9).

### Ładowanie istniejącego skoroszytu Excel

Aby manipulować skoroszytem, najpierw tworzysz obiekt `Workbook`.

`Workbook` reprezentuje cały plik Excel w pamięci, udostępniając arkusze, tabele i inne komponenty.  
```java
Workbook workbook = new Workbook("input.xlsx");
```
Ładuje plik bez blokowania źródła, umożliwiając operacje odczytu i zapisu.

### Dostęp do określonego arkusza i tabeli

Po załadowaniu, zlokalizuj arkusz zawierający docelową tabelę.

`Worksheet` jest obiektem przechowującym wiersze, kolumny i tabele dla jednego arkusza.  
```java
Worksheet sheet = workbook.getWorksheets().get("SalesData");
Table table = sheet.getTables().get(0); // assumes the first table is the target
```
Jeśli skoroszyt zawiera wiele tabel, dostosuj indeks lub użyj nazwy tabeli.

### Dodawanie segmentatora do tabeli Excel

Teraz **add a slicer** do filtrowania tabeli według kolumny „Region” i umieścimy go w komórce `H5`.

`Slicer` jest klasą tworzącą interaktywny interfejs filtrowania.  
```java
int slicerIndex = sheet.getSlicers().add(table.getIndex(), 2, "H5"); // column index 2 = Region
Slicer slicer = sheet.getSlicers().get(slicerIndex);
slicer.setCaption("Region");
slicer.setStyle(SlicerStyle.Light1);
```
Segmentator pojawia się dokładnie w określonym miejscu, a jego podpis, styl i rozmiar można dostosować programowo.

### Zapisywanie zmodyfikowanego skoroszytu

Na koniec zapisz zmiany na dysku.

`Workbook.save` zapisuje reprezentację w pamięci do fizycznego pliku.  
```java
workbook.save("output_with_slicer.xlsx");
```
Pamiętaj, aby wywołać `workbook.dispose()` w długotrwale działających usługach, aby zwolnić zasoby natywne.

## Praktyczne zastosowania

Dodawanie segmentatorów z Aspose.Cells dla Javy zwiększa analizę danych w wielu scenariuszach:

1. **Raportowanie finansowe:** Filtruj kwartalne wyniki sprzedaży jednym kliknięciem, aby dostrzec trendy.  
2. **Zarządzanie zapasami:** Przeglądaj poziomy zapasów według kategorii produktów bez konieczności przebudowy zapytań.  
3. **Analiza HR:** Szybko porównuj wyniki pracowników w różnych działach.  

Możesz połączyć generowanie segmentatorów z automatycznym importem danych z baz danych lub usług sieciowych, tworząc kompleksowe potoki raportowania od końca do końca.

## Wskazówki dotyczące wydajności

Podczas przetwarzania dużych skoroszytów pamiętaj o następujących wskazówkach:

- **Zarządzanie pamięcią:** Wywołaj `workbook.dispose()` po zakończeniu, aby zwolnić pamięć natywną.  
- **Przetwarzanie wsadowe:** Podziel bardzo duże pliki na mniejsze części, aby utrzymać zużycie pamięci pod kontrolą.  
- **API strumieniowe:** Dla plików powyżej 200 MB użyj trybu strumieniowego `LoadOptions`, aby uniknąć ładowania całego skoroszytu do pamięci.

Aspose.Cells może obsługiwać **ponad 100 formatów wejścia i wyjścia** oraz przetwarzać wielostronicowe skoroszyty przy zużyciu mniej niż 200 MB RAM, gdy włączone jest strumieniowanie.

## Typowe problemy i rozwiązania

| Problem | Rozwiązanie |
|-------|----------|
| **Slicer not visible** | Upewnij się, że docelowa tabela zawiera co najmniej jedną kolumnę z unikalnymi wartościami; segmentatory potrzebują unikalnych elementów do wyświetlenia. |
| **Exception on `add` method** | Zweryfikuj, czy odwołanie do komórki (np. `"H5"`) mieści się w używanym zakresie arkusza oraz czy indeks kolumny odpowiada istniejącej kolumnie tabeli. |
| **License not applied** | Potwierdź, że ścieżka do pliku licencji jest prawidłowa i że `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` jest wywoływane przed jakimikolwiek wywołaniami Aspose.Cells. |

## Najczęściej zadawane pytania

**Q: Czy mogę dodać wiele segmentatorów do tej samej tabeli?**  
A: Tak – wywołaj `worksheet.getSlicers().add` wielokrotnie, podając różne indeksy kolumn lub pozycje.

**Q: Czy Aspose.Cells obsługuje segmentatory dla tabel przestawnych?**  
A: Absolutnie – ta sama metoda `add` działa z tabelami przestawnymi, o ile istnieją na arkuszu.

**Q: Czy można programowo dostosować styl segmentatora?**  
A: Możesz modyfikować właściwości takie jak `setStyle`, `setCaption`, `setWidth` i `setHeight` po jego utworzeniu.

**Q: Jakie wersje Javy są kompatybilne?**  
A: Aspose.Cells for Java 25.3 wspiera JDK 8 i nowsze, w tym Java 11, 17 oraz późniejsze wersje LTS.

**Q: Jak usunąć segmentator, którego już nie potrzebuję?**  
A: Użyj `worksheet.getSlicers().removeAt(index)`, gdzie `index` odpowiada pozycji segmentatora w kolekcji.

**Ostatnia aktualizacja:** 2026-09-02  
**Testowano z:** Aspose.Cells 25.3 dla Javy  
**Autor:** Aspose  









```java
import com.aspose.cells.*;

public class DisplayAsposeCellsVersion {
    public static void main(String[] args) throws Exception {
        String version = CellsHelper.getVersion();
        System.out.println("Aspose.Cells for Java Version: " + version);
    }
}
```

```java
import com.aspose.cells.*;

public class LoadExcelWorkbook {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/sampleCreateSlicerToExcelTable.xlsx");
    }
}
```

```java
import com.aspose.cells.*;

public class AccessWorksheetAndTable {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/sampleCreateSlicerToExcelTable.xlsx");
        
        Worksheet worksheet = workbook.getWorksheets().get(0);
        ListObject table = worksheet.getListObjects().get(0);
    }
}
```

```java
import com.aspose.cells.*;

public class AddSlicerToExcelTable {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/sampleCreateSlicerToExcelTable.xlsx");
        
        Worksheet worksheet = workbook.getWorksheets().get(0);
        ListObject table = worksheet.getListObjects().get(0);
        
        int idx = worksheet.getSlicers().add(table, 0, "H5");
    }
}
```

```java
import com.aspose.cells.*;

public class SaveExcelWorkbookWithSlicer {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";
        
        Workbook workbook = new Workbook(dataDir + "/sampleCreateSlicerToExcelTable.xlsx");
        
        Worksheet worksheet = workbook.getWorksheets().get(0);
        ListObject table = worksheet.getListObjects().get(0);
        
        int idx = worksheet.getSlicers().add(table, 0, "H5");
        
        workbook.save(outDir + "/outputCreateSlicerToExcelTable.xlsx", SaveFormat.XLSX);
    }
}
```

## Powiązane samouczki

- [Zarządzanie skoroszytami Excel i segmentatorami przy użyciu Aspose.Cells dla Javy: Kompletny przewodnik](/cells/java/workbook-operations/manage-excel-workbooks-aspose-cells-java/)
- [Mistrzostwo w tabelach przestawnych w Excelu przy użyciu Aspose.Cells dla Javy: Kompletny przewodnik analizy danych](/cells/java/data-analysis/excel-pivot-tables-aspose-cells-java-tutorial/)
- [Jak efektywnie filtrować dane podczas ładowania skoroszytów Excel przy użyciu Aspose.Cells w Javie](/cells/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}