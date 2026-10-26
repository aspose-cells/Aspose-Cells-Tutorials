---
category: general
date: 2026-10-26
description: Dowiedz się, jak skopiować tabelę przestawną do nowego skoroszytu przy
  użyciu Javy, zachowując formatowanie i definicję tabeli przestawnej, jednocześnie
  kopiując zakres Excela z formatowaniem za pomocą Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: pl
lastmod: 2026-10-26
og_description: Skopiuj tabelę przestawną do nowego skoroszytu w Javie przy użyciu
  Aspose.Cells. Ten przewodnik pokazuje, jak skopiować zakres Excela, zachować formatowanie
  i efektywnie utworzyć pusty skoroszyt.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Skopiuj tabelę przestawną do nowego skoroszytu w Javie – przewodnik krok
  po kroku
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak skopiować tabelę przestawną do nowego skoroszytu w Javie
url: /pl/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skopiować tabelę przestawną do nowego skoroszytu w Javie

Jeśli potrzebujesz **skopiować tabelę przestawną** z jednego pliku Excel do drugiego, ten przewodnik pokaże Ci kompletną, gotową do uruchomienia rozwiązanie. Zobaczysz, jak zachować definicję tabeli przestawnej, utrzymać wszystkie formatowania i uniknąć typowych pułapek przy kopiowaniu zakresu Excel.

Kopiowanie tabeli przestawnej często rodzi pytania, takie jak *jak skopiować tabelę przestawną* bez uszkadzania źródła danych lub utraty stylów. Po zakończeniu tego samouczka będziesz mieć samodzielny program w Javie, który tworzy pusty skoroszyt, kopiuje wybrany zakres i zapisuje wynik z zachowaną tabelą przestawną.

## Co osiągniesz

* Załaduj skoroszyt źródłowy, który zawiera tabelę przestawną.  
* **Create empty workbook**, który otrzyma skopiowane dane.  
* **Copy excel range**, który obejmuje tabelę przestawną, używając opcji zachowujących tabelę i formatowanie.  
* Zapisz plik docelowy i zweryfikuj, że tabela przestawna działa dokładnie tak jak oryginał.

### Wymagania wstępne

* Java 17 lub nowsza.  
* Aspose.Cells for Java (wersja 23.10 lub nowsza).  
* Podstawowa znajomość środowisk IDE Java (IntelliJ IDEA, Eclipse itp.).  

> **Pro tip:** Użyj darmowej licencji ewaluacyjnej Aspose.Cells do szybkiego testowania; przed użyciem w produkcji zamień ją na pełną licencję.

## Skopiowanie tabeli przestawnej do nowego skoroszytu

Pierwszym krokiem jest przygotowanie skoroszytów źródłowego i docelowego. Dokument docelowy rozpoczyna się od wywołania **create empty workbook**, co daje czysty plik z jedną arkuszem.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Dlaczego to działa

* `new Workbook()` **creates empty workbook** z domyślnym arkuszem, unikając konieczności usuwania istniejących danych.  
* `CopyOptions` instruuje Aspose.Cells, aby kopiował metadane **pivot table**, a nie tylko surowe wartości. Tryb `PASTE_ALL` przenosi także style komórek, formaty liczb i formatowanie warunkowe — spełniając wymóg **copy range with formatting**.  
* `copyRange` wykonuje operację **copy excel range**, która respektuje wewnętrzne struktury źródła, dzięki czemu tabela przestawna pozostaje funkcjonalna po kopiowaniu.

## Jak skopiować tabelę przestawną bez utraty formatowania

Jeśli używasz tylko domyślnych `CopyOptions`, niektóre informacje o stylach mogą być pominięte w starszych wersjach Aspose.Cells. Jawne ustawienie typu wklejania zapewnia, że **copy range with formatting** zostanie zachowane.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

Dodanie `setPasteSpecialType` zapewnia, że szerokości kolumn, wysokości wierszy oraz nawet reguły walidacji danych zostaną przeniesione wraz z zakresem. Jest to szczególnie przydatne, gdy tabela przestawna rozciąga się na wiele kolumn o niestandardowych szerokościach.

## Utworzenie pustego skoroszytu przed kopiowaniem

Czasami programiści próbują kopiować do istniejącego skoroszytu, który już zawiera dane. Może to powodować nakładanie się zakresów lub nieoczekiwane nadpisania. Rozpoczęcie od wywołania **create empty workbook** izoluje operację:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

Jeśli potrzebujesz więcej niż jednego arkusza w docelowym skoroszycie, możesz dodać je po kopiowaniu:

```java
destWb.getWorksheets().add("Summary");
```

## Kopiowanie zakresu Excel z formatowaniem przy użyciu CopyOptions

Poza tabelami przestawnymi, ten sam wzorzec działa dla dowolnego **copy excel range**, które wymaga zachowania formatowania — wykresów, tabel lub formatów warunkowych.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

Instancja `CopyOptions` pozostaje taka sama, więc uzyskasz spójne zachowanie w różnych zakresach.

### Przypadki brzegowe do rozważenia

| Situation                              | Recommended handling |
|----------------------------------------|----------------------|
| Skoroszyt źródłowy zawiera wiele tabel przestawnych   | Skopiuj zakres każdej tabeli przestawnej osobno lub skopiuj cały arkusz. |
| Docelowy skoroszyt już zawiera dane      | Wybierz niekolidująca komórkę początkową (np. „H1”) przy wywoływaniu `copyRange`. |
| Źródło danych tabeli przestawnej jest zewnętrzne (np. DB) | Upewnij się, że docelowy skoroszyt wskazuje to samo zewnętrzne źródło danych lub odśwież tabelę przestawną po kopiowaniu. |
| Duży skoroszyt ( > 10 MB )             | Zwiększ rozmiar sterty JVM (`-Xmx2g`), aby uniknąć `OutOfMemoryError`. |

## Zweryfikuj wynik

Po uruchomieniu programu otwórz `destination.xlsx`. Powinieneś zobaczyć:

* Ten sam układ tabeli przestawnej co w `source.xlsx`.  
* Wszystkie kolory komórek, formaty liczb i szerokości kolumn zachowane.  
* Źródło danych tabeli przestawnej nadal wskazuje na oryginalny zakres danych w nowym pliku, więc odświeżenie tabeli przestawnej aktualizuje wartości poprawnie.

Jeśli tabela przestawna pojawia się jako statyczna tabela, sprawdź ponownie, czy ustawiono `CopyOptions.setPasteType(PasteType.PASTE_ALL)`. Bez tej opcji Aspose.Cells traktuje tabelę przestawną jako zwykłe dane.

## Podsumowanie

Teraz wiesz, jak **copy pivot table** do nowego skoroszytu w Javie, zachowując formatowanie, połączenia danych i układ arkusza. Pełne rozwiązanie pokazuje ładowanie pliku źródłowego, **create empty workbook**, konfigurowanie opcji **copy excel range** oraz zapisywanie wyniku.

Od tego momentu możesz zgłębiać powiązane tematy, takie jak **how to copy pivot** pomiędzy różnymi arkuszami, osadzanie wykresów obok tabel przestawnych lub automatyzacja przetwarzania wsadowego wielu skoroszytów. Eksperymentuj z ustawieniami `CopyOptions`, aby dopasować je do swoich konkretnych potrzeb automatyzacji, a będziesz mieć solidny zestaw narzędzi do manipulacji Excel pod ręką.

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}