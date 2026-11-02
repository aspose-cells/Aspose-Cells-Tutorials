---
category: general
date: 2026-09-11
description: Utwórz nowy arkusz i skopiuj zakres Excela przy użyciu Aspose.Cells.
  Dowiedz się, jak kopiować zakres między arkuszami, zachowując tabele przestawne.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: pl
lastmod: 2026-09-11
og_description: Utwórz nowy arkusz i skopiuj zakres w Excelu przy użyciu Aspose.Cells.
  Ten samouczek pokazuje dokładne kroki kopiowania zakresu między arkuszami oraz zachowania
  tabel przestawnych w niezmienionym stanie.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Utwórz nowy arkusz i skopiuj zakres w Excelu – przewodnik Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Utwórz nowy arkusz i skopiuj zakres Excela przy użyciu Aspose.Cells
url: /pl/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz nowy arkusz i skopiuj zakres Excel przy użyciu Aspose.Cells

Jeśli potrzebujesz **create new worksheet** i przenieść dane w pliku Excel, Aspose.Cells ułatwia to. Ten przewodnik pokazuje dokładnie, jak skopiować zakres Excel z jednego arkusza do drugiego, zachowując wszystkie tabele przestawne znajdujące się w zakresie.

Dowiesz się, jak **copy excel range**, jak **copy range between sheets**, oraz dlaczego metoda `copy` w Aspose.Cells zachowuje definicje tabel przestawnych. Nie są wymagane żadne zewnętrzne narzędzia — wystarczy projekt Java z biblioteką Aspose.Cells.

## Wymagania wstępne

- Java 17 lub nowszy zainstalowany
- Aspose.Cells for Java (wersja 23.12 lub nowsza) dodany do classpathu projektu
- Źródłowy skoroszyt (`input.xlsx`) zawierający tabelę przestawną w zakresie, który chcesz skopiować
- Podstawowa znajomość składni Java oraz zarządzania zależnościami Maven/Gradle

## Krok 1: Skonfiguruj projekt i zaimportuj Aspose.Cells

Create a simple Maven project (or Gradle, if you prefer) and add the Aspose.Cells dependency:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Then import the required classes in your Java source file:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Dlaczego ten krok ma znaczenie*: Importowanie właściwych klas daje dostęp do `Workbook`, `Worksheet`, `Range` oraz metody `copy`, która obsłuży przeniesienie zakresu.

## Krok 2: Załaduj źródłowy skoroszyt

Open the workbook that contains the data you want to copy. The following code loads `input.xlsx` from a directory you specify:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Wyjaśnienie*: `Workbook` reprezentuje cały plik Excel. Jednorazowe załadowanie daje dostęp do odczytu i zapisu wszystkich arkuszy oraz kolekcji komórek.

## Krok 3: Zidentyfikuj źródłowy zakres zawierający tabelę przestawną

Select the worksheet that holds the pivot table and define the exact cell block you want to copy. In this example we copy cells A1 through D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Dlaczego to ważne*: Tworząc obiekt `Range`, informujesz Aspose.Cells, które dokładnie komórki (w tym wszelkie osadzone obiekty, takie jak tabele przestawne) mają zostać zduplikowane.

## Krok 4: **Create new worksheet**, który otrzyma skopiowane dane

Now we add a fresh sheet to the same workbook. This is the point where the primary keyword appears:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Wyjaśnienie*: Dodanie nowego arkusza izoluje skopiowane dane, ułatwiając weryfikację, że operacja **copy excel range** zakończyła się sukcesem, nie wpływając na oryginalny arkusz.

## Krok 5: Skopiuj zakres – tabela przestawna jest zachowywana automatycznie

Use the `copy` method to move the range from the source sheet to the destination sheet. Aspose.Cells copies formulas, formatting, and pivot‑table definitions:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Dlaczego to działa*: Metoda `copy` wykonuje głęboką kopię źródłowych komórek. Nie kopiuje jedynie wartości; odtwarza całą strukturę komórek, w tym pamięć podręczną tabeli przestawnej. Dlatego możesz **copy range aspose.cells** i nadal widzieć działającą tabelę przestawną na nowym arkuszu.

## Krok 6: Zapisz skoroszyt z nowym arkuszem

Finally, write the modified workbook to disk:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Wynik*: `output.xlsx` zawiera teraz oryginalny arkusz oraz nowy arkusz nazwany **Copy**, który posiada dokładnie ten sam zakres, włącznie z tabelą przestawną.

## Pełny działający przykład

Putting all the pieces together, here is the complete, runnable program:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Oczekiwany wynik**: Otwórz `output.xlsx` w Excelu. Zobaczysz arkusz o nazwie **Copy**, którego komórki A1:D20 zawierają te same dane, formatowanie oraz aktywną tabelę przestawną identyczną z oryginałem.

## Częste pytania i przypadki brzegowe

- **Co jeśli źródłowy zakres zawiera scalone komórki?**  
  Metoda `copy` kopiuje również informacje o scalaniu, więc scalone komórki pozostają niezmienione w arkuszu docelowym.

- **Czy mogę kopiować do innego skoroszytu?**  
  Tak. Załaduj drugą instancję `Workbook`, utwórz zakres docelowy w tym skoroszycie i wywołaj `sourceRange.copy(destinationRange)`. Metoda automatycznie obsługuje kopiowanie między skoroszytami.

- **Co jeśli docelowy arkusz już zawiera dane?**  
  Operacja kopiowania nadpisuje wszystkie istniejące komórki, które pokrywają się z zakresem docelowym. Aby uniknąć utraty danych, upewnij się, że obszar docelowy jest pusty lub użyj innej komórki początkowej (np. `"B2"`).

- **Czy pamięć podręczna tabeli przestawnej jest duplikowana?**  
  Aspose.Cells ponownie używa oryginalnej pamięci podręcznej, co oznacza, że nowa tabela przestawna pozostaje powiązana z tym samym źródłem danych. Jeśli potrzebujesz niezależnej pamięci, musisz odtworzyć tabelę przestawną po skopiowaniu.

## Wskazówki i najlepsze praktyki

- **Pro tip**: Użyj `Workbook.setForceFormulaRecalculation(true)` przed zapisem, jeśli zakres zawiera formuły zależne od danych poza skopiowanym blokiem.  
- **Uwaga** na duże zakresy: kopiowanie ogromnych arkuszy może zużywać dużo pamięci. Rozważ kopiowanie w mniejszych fragmentach, jeśli napotkasz `OutOfMemoryError`.  
- **Wskazówka wydajnościowa**: Wyłącz aktualizację ekranu (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) podczas pracy z bardzo dużymi plikami, aby przyspieszyć proces kopiowania.

## Zakończenie

Teraz wiesz, jak **create new worksheet** i **copy excel range** między arkuszami przy użyciu Aspose.Cells, zachowując tabele przestawne i wszystkie atrybuty komórek. Ta technika pozwala programowo duplikować bloki danych, tworzyć szablony raportów lub przekształcać skoroszyty bez ręcznego kopiowania‑wklejania.

Następnie, zapoznaj się z powiązanymi tematami, takimi jak **copy range aspose.cells** dla operacji między skoroszytami, automatyzacja odświeżania tabel przestawnych lub eksportowanie skopiowanego arkusza do PDF. Eksperymentuj z różnymi zakresami źródłowymi i nazwami arkuszy, aby dopasować je do swojego scenariusza automatyzacji. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Copy Shapes Between Excel Sheets Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}