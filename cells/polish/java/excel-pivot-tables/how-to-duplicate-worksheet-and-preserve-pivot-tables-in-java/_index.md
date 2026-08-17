---
category: general
date: 2026-08-17
description: Jak duplikować arkusz w Javie przy użyciu Aspose.Cells, zachowując tabelę
  przestawną, kopiując tabelę przestawną do nowego skoroszytu oraz tworząc skoroszyt
  z arkusza.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: pl
lastmod: 2026-08-17
og_description: Jak zduplikować arkusz w Javie przy użyciu Aspose.Cells, zachowując
  tabelę przestawną, kopiując tabelę przestawną do nowego skoroszytu oraz tworząc
  skoroszyt z arkusza — wszystkie kroki wyjaśnione.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Jak duplikować arkusz i zachować tabele przestawne – przewodnik Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Jak skopiować arkusz i zachować tabele przestawne w Javie
url: /pl/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zduplikować arkusz i zachować tabele przestawne w Javie

Duplikowanie arkusza przy zachowaniu jego tabeli przestawnej jest częstą potrzebą przy automatyzacji raportowania w Excelu. Ten przewodnik pokazuje, jak skopiować tabelę przestawną do nowego skoroszytu przy użyciu Aspose.Cells for Java, a także jak zachować tabelę przestawną przy tworzeniu skoroszytu z arkusza.

Nauczysz się, jak wczytać istniejący skoroszyt, zduplikować arkusz zawierający tabelę przestawną i zapisać wynik jako nowy plik. Samouczek zakłada, że masz podstawowe środowisko programistyczne Javy oraz ważną licencję Aspose.Cells (bezpłatna wersja ewaluacyjna działa do testów). Nie są wymagane żadne zewnętrzne narzędzia poza plikiem JAR Aspose.Cells.

## Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz:

* Java Development Kit (JDK) 8 lub nowszy.
* Maven lub Gradle do zarządzania zależnością Aspose.Cells.
* Plik Excel (`source.xlsx`) zawierający co najmniej jedną tabelę przestawną w pierwszym arkuszu.
* Katalog, w którym możesz odczytać plik źródłowy i zapisać zduplikowany skoroszyt.

Dodaj zależność Aspose.Cells do swojego `pom.xml` (Maven) lub `build.gradle` (Gradle). Dla Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Jak zduplikować arkusz z tabelą przestawną

Podstawowa operacja to proces trzyetapowy: wczytanie, kopiowanie i zapis. Każdy krok jest wyjaśniony poniżej.

### Krok 1 – Wczytaj skoroszyt zawierający tabelę przestawną

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Dlaczego ten krok jest ważny*: Obiekt `Workbook` reprezentuje cały plik Excel. Pobierając pierwszy arkusz (`get(0)`), celujesz w arkusz, który zawiera tabelę przestawną, którą chcesz zduplikować.

### Krok 2 – Utwórz nowy skoroszyt i zduplikuj cały arkusz

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` klonuje arkusz **włącznie** ze wszystkimi osadzonymi obiektami, formułami i pamięciami podręcznymi tabel przestawnych. Jest to zalecany sposób **jak skopiować tabelę przestawną**, ponieważ definicja tabeli przestawnej i jej źródło danych są przenoszone razem.

### Krok 3 – Zapisz nowy skoroszyt

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

Po wykonaniu, `copy_with_pivot.xlsx` zawiera dokładną kopię oryginalnego arkusza, a tabela przestawna działa bez dodatkowej konfiguracji.

**Oczekiwany wynik**: Otwarcie `copy_with_pivot.xlsx` w Excelu pokazuje zduplikowany arkusz z takim samym układem tabeli przestawnej, filtrami i polami obliczonymi jak w pliku źródłowym.

## Jak skopiować tabelę przestawną do innego skoroszytu

Jeśli potrzebujesz przenieść tabelę przestawną bez kopiowania całego arkusza, możesz wyodrębnić pamięć podręczną tabeli przestawnej i dołączyć ją do nowego arkusza. Poniższy fragment kodu demonstruje to podejście:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Ten kod odpowiada na pytanie **jak skopiować tabelę przestawną**, kopiując tylko obiekt tabeli przestawnej, a nie cały arkusz. Metoda `addCopy` w kolekcji `PivotTables` zapewnia duplikację pamięci podręcznej tabeli przestawnej, spełniając wymagania **jak zachować tabelę przestawną**.

## Jak zachować tabelę przestawną przy tworzeniu skoroszytu z arkusza

Czasami zaczynasz z arkuszem, który nie należy do żadnego skoroszytu (na przykład generujesz arkusz w pamięci). Aby **utworzyć skoroszyt z arkusza** zachowując tabelę przestawną, postępuj zgodnie z poniższymi krokami:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

Dodając arkusz do nowego `Workbook` po pełnym zdefiniowaniu tabeli przestawnej, zapewniasz, że **jak zachować tabelę przestawną** działa nawet wtedy, gdy arkusz pochodzi spoza istniejącego pliku.

## Praktyczne wskazówki i typowe pułapki

| Wskazówka | Dlaczego jest ważne |
|-----|----------------|
| Użyj `addCopy` zamiast `copy` | `addCopy` klonuje podstawową pamięć podręczną tabeli przestawnej; zwykłe `copy` może utracić połączenie ze źródłem danych. |
| Trzymaj pliki źródłowe i docelowe w tym samym systemie plików | Ścieżki względne w źródle danych tabeli przestawnej są prawidłowo rozwiązywane, co zmniejsza liczbę błędów „źródło nie znalezione”. |
| Sprawdź pamięć podręczną tabeli przestawnej po skopiowaniu | Wywołaj `pivot.refresh()`, jeśli dane źródłowe zmieniły się pomiędzy kopiowaniem a zapisem. |
| Zwolnij zasoby skoroszytów po zakończeniu | `sourceWorkbook.dispose();` zwalnia zasoby natywne, co jest ważne przy dużych plikach. |

## Przypadki brzegowe, które możesz napotkać

* **Wiele arkuszy z zależnymi od siebie tabelami przestawnymi** – kopiuj każdy arkusz osobno; współdzielone pamięci podręczne są duplikowane automatycznie, ale może być konieczne ponowne przypisanie zewnętrznych połączeń danych.
* **Tabele przestawne oparte na zewnętrznych zapytaniach SQL** – upewnij się, że środowisko docelowe ma dostęp do tej samej bazy danych; w przeciwnym razie tabela przestawna wyświetli błędy „#REF!”.
* **Duże skoroszyty (>100 MB)** – użyj `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, aby zmniejszyć obciążenie pamięci podczas operacji kopiowania.

## Pełny, działający przykład

Poniżej znajduje się pełny program, który zawiera wszystkie omówione kroki. Zapisz go jako `CopyPivotTable.java`, dostosuj ścieżki do plików i uruchom w wybranym IDE lub za pomocą `javac`/`java`.



## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak tworzyć tabele przestawne w Excelu przy użyciu Aspose.Cells for Java: Kompletny przewodnik](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Jak zaktualizować źródło tabeli przestawnej w Excelu przy użyciu Aspose.Cells for Java: Kompletny przewodnik](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Jak wdrożyć segmentatory w tabelach przestawnych przy użyciu Aspose.Cells for Java: Kompletny przewodnik](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}