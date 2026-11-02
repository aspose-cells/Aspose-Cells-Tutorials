---
category: general
date: 2026-09-08
description: Jak kopiować zakres w Javie przy użyciu Aspose.Cells – dowiedz się, jak
  kopiować tabelę przestawną, duplikować tabelę przestawną i eksportować tabelę przestawną,
  zachowując formatowanie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: pl
lastmod: 2026-09-08
og_description: Jak skopiować zakres w Javie przy użyciu Aspose.Cells. Ten samouczek
  pokazuje, jak skopiować tabelę przestawną, zduplikować tabelę przestawną oraz wyeksportować
  tabelę przestawną, zachowując formatowanie.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Jak skopiować zakres w Javie – kompletny przewodnik Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak skopiować zakres w Javie przy użyciu Aspose.Cells
url: /pl/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skopiować zakres w Javie przy użyciu Aspose.Cells

Jeśli potrzebujesz **jak skopiować zakres** w Javie, Aspose.Cells ułatwia to zadanie. Niezależnie od tego, czy przenosisz zwykły blok komórek, czy w pełni funkcjonalną tabelę przestawną, biblioteka obsługuje operację kopiowania, zachowując formuły, style i pamięć podręczną tabeli przestawnej. W tym przewodniku nauczysz się **copy pivot table**, **duplicate pivot table**, a nawet **export pivot table** do nowego skoroszytu z pełnym formatowaniem.

Samouczek obejmuje wszystko, od konfiguracji projektu po końcowy krok weryfikacji, dzięki czemu możesz uruchomić kod od razu po przeczytaniu. Nie są wymagane żadne zewnętrzne narzędzia poza plikiem JAR Aspose.Cells for Java.

## Wymagania wstępne

- Java 17 (lub dowolny obsługiwany JDK) zainstalowany i skonfigurowany w Twoim IDE.
- Maven lub Gradle do zarządzania zależnościami (przykłady używają Maven).
- Plik źródłowy Excel (`source.xlsx`) zawierający tabelę przestawną w zakresie `A1:H20`.
- Podstawowa znajomość programowania w Javie.

## Krok 1: Dodaj Aspose.Cells do swojego projektu

Aspose.Cells jest komercyjną biblioteką, ale dostępna jest darmowa wersja ewaluacyjna. Dodaj zależność do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Wskazówka:** Jeśli wolisz Gradle, równoważny wpis to:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Dodanie pliku JAR zapewnia dostęp do klas `Workbook`, `Worksheet`, `Range` i `CopyOptions` używanych w całym przewodniku.

## Krok 2: Załaduj źródłowy skoroszyt i wybierz pierwszą arkusz

Pierwsza część **jak skopiować zakres** polega na otwarciu skoroszytu, który zawiera dane, które chcesz przenieść.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Dlaczego to ważne:** Otwarcie skoroszytu tworzy reprezentację w pamięci, którą API może manipulować bez modyfikacji oryginalnego pliku na dysku.

## Krok 3: Zdefiniuj zakres zawierający tabelę przestawną

Tabela przestawna znajduje się wewnątrz prostokątnego bloku. Musisz określić ten blok, aby Aspose.Cells wiedział, co kopiować.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Uwaga:** Metoda `createRange` **nie** kopiuje jeszcze nic; tworzy jedynie obiekt `Range`, który wskazuje na komórki, które zamierzasz zduplikować.

## Krok 4: Utwórz nowy skoroszyt i pobierz jego pierwszy arkusz

Teraz utwórz docelowy skoroszyt, w którym będzie znajdował się skopiowany zakres.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Dlaczego nowy skoroszyt?** Użycie nowego pliku zapewnia, że żadne ukryte style ani nazwy zakresów nie zakłócą operacji kopiowania, co jest szczególnie ważne, gdy **export pivot table** do osobnego pliku.

## Krok 5: Skopiuj zakres (włącznie z tabelą przestawną) do docelowego arkusza

To jest sedno **jak skopiować zakres z formatowaniem**. Obiekt `CopyOptions` instruuje Aspose.Cells, aby zachował wszystko: wartości, formuły, style i pamięć podręczną tabeli przestawnej.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Copy pivot table:** Ponieważ zakres źródłowy zawiera tabelę przestawną, API automatycznie duplikuje pamięć podręczną tabeli przestawnej, więc nowy arkusz zawiera w pełni funkcjonalną tabelę przestawną, zachowującą się dokładnie tak jak oryginał.

## Krok 6: Zapisz docelowy skoroszyt

Na koniec zapisz wynik na dysku.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

Po otwarciu `dest.xlsx` zobaczysz dokładną kopię oryginalnej tabeli przestawnej, wraz z jej formatowaniem, segmentatorami i polami obliczeniowymi.

## Oczekiwany wynik

- `dest.xlsx` zawiera arkusz o nazwie **Sheet1**.
- Komórki `A1:H20` zawierają te same dane i tabelę przestawną co źródło.
- Wszystkie style komórek (czcionki, kolory, obramowania) są zachowane.
- Tabela przestawna jest w pełni interaktywna; odświeżenie jej odzwierciedla podstawowe dane w skopiowanym zakresie.

## Jak skopiować zakres z formatowaniem – głębsze zanurzenie

Poprzedni przykład pokazuje najprostszy scenariusz, ale możesz napotkać warianty wymagające nieco innego podejścia.

### Skopiuj tabelę przestawną do istniejącego skoroszytu

Jeśli potrzebujesz **duplicate pivot table** w skoroszycie, który już zawiera dane, użyj tego samego wywołania `copyRange`, ale wskaż inny adres docelowy:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Eksportuj tylko tabelę przestawną (bez otaczających danych)

Czasami potrzebujesz tylko tabeli przestawnej, a nie danych źródłowych. Zidentyfikuj zakres wyświetlania tabeli przestawnej za pomocą metody `getPivotTable`:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Zachowaj formatowanie warunkowe

Reguły formatowania warunkowego są częścią kolekcji stylów. Flaga `PasteType.ALL` już je kopiuje, ale możesz być bardziej explicite:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Przypadki brzegowe i rozwiązywanie problemów

| Sytuacja | Na co zwrócić uwagę | Zalecane rozwiązanie |
|-----------|-------------------|-----------------|
| Źródłowy i docelowy skoroszyt używają różnych wersji Excela | Niektóre nowsze funkcje tabeli przestawnej (np. model danych) mogą nie renderować się poprawnie | Użyj najnowszej wersji Aspose.Cells i ustaw `Workbook.setFileFormatType(FileFormatType.XLSX)` dla obu skoroszytów |
| Bardzo duże tabele przestawne ( > 10 000 wierszy) powodują obciążenie pamięci | Błędy out‑of‑memory podczas kopiowania | Włącz `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` przed ładowaniem |
| Docelowy arkusz już zawiera nazwany zakres o tej samej nazwie co źródło | Kolizja nazw prowadzi do niepowodzenia `CopyOptions` | Wywołaj `copyOptions.setIgnoreNameConflicts(true)` |

## Pełny, uruchamialny przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do klasy Java. Zawiera wszystkie importy, obsługę błędów i komentarze.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Uruchom program, a następnie otwórz `dest.xlsx`, aby zweryfikować, że tabela przestawna działa dokładnie tak jak oryginał.

## Zakończenie

Teraz wiesz **jak skopiować zakres** w Javie przy użyciu Aspose.Cells, w tym jak **copy pivot table**, **duplicate pivot table** oraz **export pivot table**, zachowując wszystkie formatowania. Biblioteka ukrywa szczegóły niskopoziomowej struktury XML Excela, pozwalając skupić się na logice biznesowej.

### Kolejne kroki

- Zbadaj **copy range with formatting** dla wykresów i obrazów (użyj `PasteType.PICTURES`).
- Zautomatyzuj przetwarzanie wsadowe: iteruj po wielu plikach źródłowych i konsoliduj ich tabele przestawne w skoroszycie podsumowującym.
- Połącz tę technikę z Aspose.Slides, aby generować raporty PowerPoint, które osadzają skopiowaną tabelę przestawną

## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z instrukcjami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zaktualizować źródło tabeli przestawnej Excel przy użyciu Aspose.Cells dla Java: Kompletny przewodnik](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Optymalizacja ładowania tabeli przestawnej w Javie przy użyciu Aspose.Cells – Kompletny przewodnik](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Jak skopiować tabelę przestawną w C# – Konwertuj Excel do PPTX, kopiuj zakres i twórz pole tekstowe](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}