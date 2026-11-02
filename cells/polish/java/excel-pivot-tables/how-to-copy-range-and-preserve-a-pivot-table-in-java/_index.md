---
category: general
date: 2026-09-21
description: Dowiedz się, jak skopiować zakres w Javie, zachowując tabelę przestawną.
  Ten przewodnik krok po kroku pokaże Ci, jak bezpiecznie wyeksportować tabelę przestawną.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- preserve pivot table
- export pivot table
- how to preserve pivot
language: pl
lastmod: 2026-09-21
og_description: Jak skopiować zakres w Javie, zachowując tabelę przestawną. Zapoznaj
  się z tym kompletnym przewodnikiem, aby bezpiecznie eksportować tabele przestawne.
og_image_alt: Screenshot of Java code copying a range and preserving a pivot table
og_title: Jak skopiować zakres i zachować tabelę przestawną w Javie
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  headline: How to copy range and preserve a pivot table in Java
  type: TechArticle
- description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  name: How to copy range and preserve a pivot table in Java
  steps:
  - name: Load the source workbook
    text: '```java // Load the source workbook that contains the pivot table Workbook
      srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx"); Worksheet srcWs = srcWb.getWorksheets().get(0);
      ```'
  - name: Define the range that covers the pivot table
    text: '```java // Define the range covering the pivot table (including its data
      source) Range srcRange = srcWs.getCells().createRange("A1:G20"); ```'
  - name: Create an empty destination workbook
    text: '```java // Create a new, empty destination workbook Workbook destWb = new
      Workbook(); Worksheet destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range – the pivot table is preserved
    text: '```java // Copy the defined range to the destination sheet – the pivot
      table is preserved destWs.getCells().copyRange(srcRange, new CellArea("A1",
      "G20")); ```'
  - name: Save the destination workbook
    text: '```java // Save the destination workbook with the copied pivot table destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
      ```'
  - name: Copy pivot table across different workbook versions
    text: Aspose.Cells supports older `.xls` files as well as the newer `.xlsx` format.
      The same code works regardless of the file extension, making it a universal
      solution for **how to preserve pivot** across versions.
  - name: Preserving pivot table when using a filtered source
    text: 'If the source pivot is filtered, the filter state is also copied. Should
      you need to reset filters in the destination, call `PivotTable.refreshData()`
      after copying:'
  - name: Export pivot table as a static snapshot
    text: Sometimes you may want a static copy (values only) rather than a live pivot.
      Replace `copyRange` with `copyRange` followed by `pt.setEnableRefresh(false)`
      to disable further calculations.
  - name: Handling large workbooks
    text: For workbooks with many worksheets, limit the copy operation to the specific
      sheet to reduce memory usage. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to fine‑tune performance.
  type: HowTo
tags:
- Java
- Aspose.Cells
- pivot table
- Excel automation
- range copy
title: Jak skopiować zakres i zachować tabelę przestawną w Javie
url: /pl/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skopiować zakres i zachować tabelę przestawną w Javie

Jeśli potrzebujesz **how to copy range** zawierającego tabelę przestawną, ten przewodnik pokaże Ci niezawodny sposób na zachowanie tabeli przestawnej w nienaruszonym stanie. Wielu programistów boryka się z utratą tabeli przestawnej podczas eksportu danych, ale poniższe podejście pozwala **copy pivot table** danych bez uszkadzania jej funkcjonalności. Po zakończeniu tego samouczka będziesz w stanie **preserve pivot table** strukturę, **export pivot table** pliki i zrozumiesz **how to preserve pivot** w różnych scenariuszach.

Przykład używa Aspose.Cells for Java, popularnej biblioteki do automatyzacji Excela. Nie wymaga dodatkowych narzędzi poza standardowym środowiskiem programistycznym Javy.

## Wymagania wstępne

* Zainstalowany Java 17 (lub nowszy).
* Maven lub Gradle do zarządzania zależnościami.
* Aspose.Cells for Java (wersja 23.9 lub nowsza). Dodaj następującą zależność Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

* Źródłowy skoroszyt (`Source.xlsx`) zawierający tabelę przestawną, którą chcesz skopiować.

## Jak skopiować zakres i zachować tabelę przestawną w nienaruszonym stanie

Główną ideą jest skopiowanie **range**, które obejmuje całą tabelę przestawną — łącznie z jej źródłem danych — przy użyciu `copyRange`. Ta metoda kopiuje zarówno surowe dane, jak i definicję tabeli przestawnej, zapewniając, że docelowy skoroszyt otrzyma w pełni funkcjonalną tabelę przestawną.

### Krok 1: Załaduj źródłowy skoroszyt

```java
// Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Dlaczego ten krok?*  
Załadowanie skoroszytu daje dostęp do arkusza, w którym znajduje się tabela przestawna. Klasa `Workbook` abstrahuje cały plik Excel, natomiast `Worksheet` zapewnia operacje na poziomie komórek.

### Krok 2: Zdefiniuj zakres obejmujący tabelę przestawną

```java
// Define the range covering the pivot table (including its data source)
Range srcRange = srcWs.getCells().createRange("A1:G20");
```

*Dlaczego ten krok?*  
Tabela przestawna nie jest pojedynczą komórką; rozciąga się na blok obejmujący nagłówki, wiersze danych i pamięć podręczną tabeli przestawnej. Określając zakres, który w pełni zawiera tabelę przestawną, zapewniasz, że `copyRange` skopiuje również ukrytą pamięć podręczną, co jest niezbędne dla zachowania **preserve pivot table**.

### Krok 3: Utwórz pusty docelowy skoroszyt

```java
// Create a new, empty destination workbook
Workbook destWb = new Workbook();
Worksheet destWs = destWb.getWorksheets().get(0);
```

*Dlaczego ten krok?*  
Rozpoczęcie od czystego skoroszytu zapobiega przypadkowym konfliktom z istniejącymi arkuszami lub nazwanymi zakresami. Docelowy skoroszyt otrzyma skopiowany zakres, skutecznie **export pivot table** zawartość.

### Krok 4: Skopiuj zakres – tabela przestawna zostaje zachowana

```java
// Copy the defined range to the destination sheet – the pivot table is preserved
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
```

*Dlaczego ten krok?*  
`copyRange` wykonuje głęboką kopię: wartości komórek, formatowanie i metadane tabeli przestawnej są przenoszone. To krytyczna operacja, która umożliwia **copy pivot table** bez utraty jej funkcjonalności. Obiekt `CellArea` określa, gdzie zakres zostanie umieszczony w docelowym arkuszu.

### Krok 5: Zapisz docelowy skoroszyt

```java
// Save the destination workbook with the copied pivot table
destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
```

*Dlaczego ten krok?*  
Zapisanie finalizuje proces **export pivot table**. Powstały plik (`DestWithPivot.xlsx`) zawiera w pełni działającą tabelę przestawną, którą możesz otworzyć w Excelu, Google Sheets lub innym przeglądarce arkuszy kalkulacyjnych.

## Weryfikacja, że tabela przestawna została zachowana

Otwórz `DestWithPivot.xlsx` w Excelu i sprawdź następujące elementy:

1. Tabela przestawna pojawia się w tej samej lokalizacji (A1:G20) co w źródle.
2. Odświeżenie tabeli przestawnej aktualizuje dane poprawnie, co dowodzi, że pamięć podręczna została skopiowana.
3. Całe formatowanie (szerokości kolumn, formaty liczb) jest zgodne z oryginałem.

Jeśli którykolwiek z tych testów nie powiedzie się, sprawdź, czy zakres źródłowy w pełni obejmuje tabelę przestawną i jej źródło danych. Częstym błędem jest wybranie zakresu, który nie obejmuje pamięci podręcznej danych, co prowadzi do uszkodzonej tabeli przestawnej.

## Dodatkowe uwagi

### Kopiowanie tabeli przestawnej między różnymi wersjami skoroszytów

Aspose.Cells obsługuje starsze pliki `.xls` oraz nowszy format `.xlsx`. Ten sam kod działa niezależnie od rozszerzenia pliku, co czyni go uniwersalnym rozwiązaniem dla **how to preserve pivot** między wersjami.

### Zachowanie tabeli przestawnej przy użyciu filtrowanego źródła

Jeśli źródłowa tabela przestawna jest filtrowana, stan filtru również zostaje skopiowany. Jeśli potrzebujesz zresetować filtry w docelowym skoroszycie, wywołaj `PivotTable.refreshData()` po skopiowaniu:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.refreshData();   // Clears filters but keeps the pivot definition
```

### Eksport tabeli przestawnej jako statycznego migawki

Czasami możesz potrzebować statycznej kopii (tylko wartości) zamiast aktywnej tabeli przestawnej. Zastąp `copyRange` wywołaniem `copyRange`, a następnie `pt.setEnableRefresh(false)`, aby wyłączyć dalsze obliczenia.

```java
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
PivotTable pt = destWs.getPivotTables().get(0);
pt.setEnableRefresh(false); // Makes the pivot static
```

### Obsługa dużych skoroszytów

W przypadku skoroszytów z wieloma arkuszami ogranicz operację kopiowania do konkretnego arkusza, aby zmniejszyć zużycie pamięci. Użyj `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, aby precyzyjnie dostroić wydajność.

## Pełny przykład do uruchomienia

Poniżej znajduje się pełny program, który możesz skopiować, wkleić i uruchomić. Dostosuj ścieżki plików do swojego środowiska.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the range covering the pivot table (including its data source)
        // Adjust the range as needed to fully contain your pivot
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a new, empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 4: Copy the defined range – the pivot table is preserved
        destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));

        // Optional: If you need a static snapshot, disable refresh
        // PivotTable pt = destWs.getPivotTables().get(0);
        // pt.setEnableRefresh(false);

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");

        System.out.println("Pivot table copied successfully. File saved as DestWithPivot.xlsx");
    }
}
```

**Oczekiwany wynik**

```
Pivot table copied successfully. File saved as DestWithPivot.xlsx
```

Po otwarciu `DestWithPivot.xlsx` powinieneś zobaczyć oryginalną tabelę przestawną w pełni funkcjonalną, co potwierdza, że pomyślnie wykonałeś **how to copy range** przy jednoczesnym **preserve pivot table**.

## Typowe pułapki i wskazówki profesjonalne

| Problem | Dlaczego się dzieje | Rozwiązanie |
|-------|----------------|-----|
| Tabela przestawna pojawia się, ale pokazuje błędy `#REF!` | Skopiowany zakres pominął ukryty arkusz pamięci podręcznej | Rozszerz zakres źródłowy, aby obejmował całą pamięć podręczną (zwykle wiersze pod tabelą przestawną) |
| Docelowy skoroszyt jest większy niż oczekiwano | `copyRange` kopiuje także formatowanie | Użyj `CopyOptions`, aby wykluczyć formatowanie, jeśli rozmiar jest problemem |
| Odświeżanie nie powodzi się z komunikatem „Data source not found” | Źródłowy skoroszyt używał zewnętrznych połączeń danych | Zreplikuj połączenie w docelowym skoroszycie lub najpierw skopiuj arkusz źródła danych |

**Wskazówka:** Zawsze wykonuj szybkie sprawdzenie `destWs.getPivotTables().size()` po skopiowaniu. Jeśli liczba wynosi zero, zakres nie zawierał definicji tabeli przestawnej i należy go rozszerzyć.

## Zakończenie

W tym samouczku pokazaliśmy **how to copy range** zawierający tabelę przestawną i zapewniliśmy, że zachowanie **preserve pivot table** pozostaje nienaruszone. Ładując źródłowy skoroszyt, definiując kompleksowy zakres, używając `copyRange` i zapisując plik docelowy, możesz niezawodnie **export pivot table** dane i odpowiedzieć na pytanie **how to preserve pivot** w projektach Java.

Kolejne kroki, które możesz rozważyć, to:
* Automatyzacja kopiowania dla wielu arkuszy (użyj drugorzędnego słowa kluczowego **copy pivot table** w pętli).
* Konwersja wyeksportowanego skoroszytu do CSV przy zachowaniu surowych danych (nadal logika **preserve pivot table** dla źródła).

## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Kopiowanie tabeli przestawnej w Javie – zachowanie, eksport do PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [Jak zaktualizować źródło tabeli przestawnej w Excelu przy użyciu Aspose.Cells for Java: Kompletny przewodnik](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Jak wyeksportować tabelę przestawną jako obraz w C# – przewodnik krok po kroku](/cells/english/net/pivot-tables/how-to-export-pivot-table-as-an-image-in-c-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}