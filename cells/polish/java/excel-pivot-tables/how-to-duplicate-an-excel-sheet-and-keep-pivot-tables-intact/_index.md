---
category: general
date: 2026-10-23
description: Dowiedz się, jak zduplikować arkusz Excel w Javie, zachowując tabele
  przestawne. Ten przewodnik pokazuje również, jak kopiować tabele przestawne, kopiować
  zakresy Excel oraz kopiować arkusz z danymi przestawnymi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: pl
lastmod: 2026-10-23
og_description: Zduplikuj arkusz Excel w Javie, zachowując tabele przestawne. Skorzystaj
  z tego pełnego samouczka, aby kopiować tabele przestawne, zakresy w Excelu oraz
  arkusz z danymi tabel przestawnych.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Duplikowanie arkusza Excel z tabelami przestawnymi w Javie – przewodnik
  krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Jak skopiować arkusz Excela i zachować nienaruszone tabele przestawne w Javie
url: /pl/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zduplikować arkusz Excel i zachować tabele przestawne w Java

Jeśli potrzebujesz **zduplikować arkusz Excel** z zachowaniem wszystkich tabel przestawnych, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Zobaczysz zwięzłe rozwiązanie, które kopiuje arkusz, kopiuje określony zakres i nawet kopiuje tabelę przestawną do innego skoroszytu — wszystko w czystej Javie przy użyciu Aspose.Cells.

Duplikowanie arkusza Excel to powszechne zadanie, gdy generujesz miesięczne raporty z szablonu lub potrzebujesz kopii testowej do eksperymentów. Poniższy kod działa z Aspose.Cells 25.11 lub nowszym, które wprowadziło opcję `setCopyPivotTable(true)`.

## Czego będziesz potrzebować

Przed rozpoczęciem upewnij się, że masz:

- Java 17 (lub dowolny nowoczesny JDK) zainstalowany
- Aspose.Cells for Java 25.11 lub nowszy w swoim projekcie (współrzędna Maven `com.aspose:aspose-cells:25.11`)
- Źródłowy skoroszyt (`SourceWithPivot.xlsx`) zawierający już tabelę przestawną
- IDE lub narzędzie budujące według własnego wyboru (IntelliJ IDEA, Eclipse, Maven, Gradle, itp.)

## Krok 1: Załaduj źródłowy skoroszyt, który zawiera tabelę przestawną

Pierwsza operacja to otwarcie skoroszytu, w którym znajduje się tabela przestawna, którą chcesz zachować.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Dlaczego ten krok ma znaczenie:** Załadowanie źródłowego skoroszytu daje dostęp do obiektów arkuszy, komórek i osadzonych tabel przestawnych. Bez tego nie możesz odwołać się do danych tabeli, które planujesz skopiować.

## Krok 2: Utwórz pusty skoroszyt docelowy (lub załaduj istniejący)

Możesz rozpocząć od pustego skoroszytu lub otworzyć istniejący plik, który otrzyma zduplikowany arkusz.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **Wskazówka:** Jeśli już masz skoroszyt raportowy, zamień powyższą linię na `new Workbook("ExistingReport.xlsx")`, aby dodać zduplikowany arkusz do niego.

## Krok 3: Skopiuj cały arkusz – tabela przestawna jest zachowywana automatycznie

Kopiowanie całego arkusza to najprostszy sposób na **copy sheet with pivot**. Aspose.Cells automatycznie kopiuje definicję tabeli przestawnej oraz jej pamięć podręczną.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Dlaczego to działa:** `addCopy` klonuje strukturę arkusza, wartości komórek, style oraz wszelkie osadzone tabele przestawne. Nowy arkusz w `dstWb` będzie wyglądał identycznie jak oryginał, łącznie z pamięcią podręczną tabeli.

## Krok 4: (Opcjonalnie) Skopiuj tylko określony zakres, który zawiera tabelę przestawną

Czasami nie potrzebujesz całego arkusza — może wystarczy fragment zawierający tabelę przestawną. Wtedy **copy Excel range** i wyraźne żądanie skopiowania tabeli przestawnej są przydatne.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **Jak to pomaga:** `setCopyPivotTable(true)` wymusza na silniku duplikację definicji tabeli przestawnej, nawet gdy kopiujesz ograniczony zakres. Bez tego flagi skopiowane zostaną jedynie surowe dane, a tabela przestawna zostanie utracona.

## Krok 5: Zapisz skoroszyt docelowy

Na koniec zapisz zduplikowaną zawartość do nowego pliku.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Oczekiwany wynik

Uruchomienie programu tworzy plik `DuplicatedWithPivot.xlsx` w katalogu docelowym. Otwórz go w Excelu i zobaczysz:

- Nowy arkusz o nazwie `Sheet1 (Copy)` (lub oryginalna nazwa z dopiskiem „Copy”)
- Tabela przestawna wygląda dokładnie tak jak w arkuszu źródłowym i jest w pełni funkcjonalna
- Jeśli użyto opcjonalnego kopiowania zakresu, obecne będą tylko komórki A1:G30, ale tabela przestawna nadal działa, ponieważ jej pamięć podręczna została skopiowana

## Częste pytania i przypadki brzegowe

### Jak skopiować tabelę przestawną do innego skoroszytu bez kopiowania całego arkusza?

Jeśli potrzebujesz jedynie tabeli przestawnej i leżących pod nią danych, skopiuj zakres obejmujący zarówno źródło danych, jak i tabelę, a następnie użyj `setCopyPivotTable(true)`. Ten sam kod z **Kroku 4** ma zastosowanie; wystarczy upewnić się, że zakres obejmuje źródło danych.

### Co jeśli źródłowy skoroszyt ma wiele arkuszy z tabelami przestawnymi?

Powtórz **Krok 3** dla każdego arkusza, który chcesz zduplikować:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### Czy to działa z chronionymi arkuszami?

Aspose.Cells może kopiować chronione arkusze, ale najpierw musisz je odchronić, jeśli zamierzasz modyfikować tabelę po skopiowaniu:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### Czy mogę skopiować tabelę przestawną do istniejącego skoroszytu, który już zawiera arkusz o tej samej nazwie?

Tak. Użyj `addCopy` z unikalną nazwą:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Pro tip: zweryfikuj pamięć podręczną tabeli przestawnej

Po skopiowaniu możesz programowo potwierdzić, że pamięć podręczna istnieje:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

Jeśli identyfikator pamięci podręcznej wypisze liczbę nieujemną, tabela przestawna została pomyślnie zduplikowana.

## Podsumowanie

Teraz wiesz, jak **duplicate Excel sheet** w Javie, zachowując każdą tabelę przestawną, jak **copy pivot** bezpośrednio, jak **copy Excel range** zawierający tabelę przestawną oraz jak **copy sheet with pivot** lub **copy pivot to workbook** przy użyciu Aspose.Cells 25.11+. Zastosuj te wzorce, aby zautomatyzować generowanie raportów, tworzyć klony szablonów lub budować środowiska testowe wymagające identycznych analiz opartych na tabelach przestawnych.

Gotowy na dalsze eksperymenty? Spróbuj wyeksportować zduplikowany skoroszyt do PDF lub programowo odświeżyć pamięć podręczną tabeli po skopiowaniu, aby zapewnić aktualność danych. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne przykłady kodu oraz szczegółowe wyjaśnienia, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Jak zduplikować arkusz i zachować tabele przestawne w Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [Jak skopiować tabelę przestawną w Java – kompletny przewodnik Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Jak skopiować zakres i zachować tabelę przestawną w Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}