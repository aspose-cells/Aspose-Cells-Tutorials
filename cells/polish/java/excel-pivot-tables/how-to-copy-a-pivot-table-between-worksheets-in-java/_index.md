---
category: general
date: 2026-10-16
description: Jak skopiować tabelę przestawną w Javie przy użyciu Aspose.Cells – dowiedz
  się, jak efektywnie kopiować zakres do innego arkusza i kopiować zakres między arkuszami.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: pl
lastmod: 2026-10-16
og_description: Jak skopiować tabelę przestawną w Javie przy użyciu Aspose.Cells.
  Ten tutorial pokazuje, jak skopiować zakres do innego arkusza oraz jak skopiować
  zakres między arkuszami, wraz z pełnym kodem.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Jak skopiować tabelę przestawną między arkuszami w Javie – przewodnik krok
  po kroku
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Jak skopiować tabelę przestawną między arkuszami w Javie
url: /pl/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skopiować tabelę przestawną między arkuszami w Javie

Jeśli potrzebujesz **jak skopiować tabelę przestawną** z jednego arkusza do drugiego w tym samym skoroszycie, ten przewodnik zapewnia kompletną, gotową do uruchomienia rozwiązanie. Zobaczysz, jak skopiować zakres źródłowy zawierający tabelę przestawną, zachować jej funkcjonalność i zweryfikować wynik — wszystko przy użyciu Aspose.Cells for Java.

Kopiowanie tabeli przestawnej jest powszechnym zadaniem przy programowym generowaniu raportów, a wykonanie go prawidłowo zapobiega utracie pamięci podręcznej tabeli przestawnej lub uszkodzeniu formuł. Po zakończeniu tego samouczka będziesz w stanie **skopiować zakres do innego arkusza** i **skopiować zakres między arkuszami** bez żadnych ręcznych kroków.

## Czego się nauczysz

* Wczytaj istniejący plik Excel z tabelą przestawną.
* Zdefiniuj zakres źródłowy, który zawiera tabelę przestawną.
* Zdefiniuj zakres docelowy na innym arkuszu.
* Użyj `CopyOptions`, aby zachować tabelę przestawną w nienaruszonym stanie.
* Zweryfikuj, że skopiowana tabela przestawna działa zgodnie z oczekiwaniami.

**Wymagania wstępne**

* Java 17 lub nowsza.
* Aspose.Cells for Java (wersja 23.12 lub nowsza).  
* Plik Excel (`input.xlsx`) zawierający tabelę przestawną na pierwszym arkuszu.

---

## Jak skopiować tabelę przestawną przy użyciu Aspose.Cells

Podstawą operacji jest czterostopniowy proces: wczytanie skoroszytu, zlokalizowanie zakresu źródłowego, ustawienie zakresu docelowego i wykonanie kopiowania. Poniżej każdy krok jest wyjaśniony szczegółowo.

### Krok 1: Wczytaj skoroszyt

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*Dlaczego ten krok?*  
Wczytanie skoroszytu wczytuje cały plik do pamięci, dając dostęp do arkuszy, komórek i pamięci podręcznej tabeli przestawnej. Aspose.Cells odczytuje format pliku automatycznie, więc nie musisz martwić się o `.xls` vs `.xlsx`.

### Krok 2: Zlokalizuj zakres źródłowy zawierający tabelę przestawną

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Dlaczego ten krok?*  
Tabela przestawna jest przechowywana w bloku komórek, który odwołuje się również do ukrytej pamięci podręcznej. Wybierając dokładny zakres (`A1:G20` w tym przykładzie), zapewniasz, że pamięć podręczna pozostaje powiązana po skopiowaniu zakresu.

### Krok 3: Zdefiniuj zakres docelowy na innym arkuszu

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*Dlaczego ten krok?*  
Wybranie docelowego miejsca na innym arkuszu umożliwia **skopiowanie zakresu do innego arkusza**. Komórka w lewym górnym rogu (`A1`) jest typowym punktem startowym, ale możesz umieścić ją w dowolnym miejscu, zmieniając adres.

### Krok 4: Skopiuj zakres źródłowy zachowując tabelę przestawną

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*Dlaczego ten krok?*  
`CopyOptions` kontroluje, co jest przenoszone. Użycie `PasteType.PASTE_ALL` gwarantuje, że tabela przestawna, jej formatowanie i leżące u podstaw formuły zostaną zduplikowane. Bez tych opcji może zostać skopiowana jedynie surowa wartość, co uszkodzi funkcjonalność tabeli przestawnej.

### Krok 5: Zapisz skoroszyt i zweryfikuj wynik

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Otwórz `output.xlsx` w Excelu i potwierdź, że:

* Drugi arkusz zawiera w pełni funkcjonalną tabelę przestawną identyczną z oryginałem.
* Odświeżenie tabeli przestawnej aktualizuje dane, co dowodzi, że pamięć podręczna jest nienaruszona.

---

## Skopiuj zakres do innego arkusza przy użyciu Javy

Jeśli Twoim celem jest po prostu **skopiowanie zakresu do innego arkusza** bez tabeli przestawnej, ten sam kod działa z zwykłym zakresem komórek. Jedyną zmianą jest adres źródłowy. Konfiguracja `CopyOptions` pozostaje taka sama, zapewniając zachowanie formuł i formatowania.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

Ten fragment kodu demonstruje elastyczność API zarówno dla scenariuszy z tabelą przestawną, jak i bez niej.

---

## Skopiuj zakres między arkuszami bez utraty formuł

Kiedy **kopiujesz zakres między arkuszami**, formuły odwołujące się do innych arkuszy mogą się zepsuć, jeśli zmienią się odwołania względne. Aby tego uniknąć:

1. Użyj `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)`, jeśli potrzebujesz tylko formuł.
2. Pozostaw arkusz docelowy w tym samym skoroszycie, aby wewnętrzne odwołania pozostały ważne.
3. Po skopiowaniu wywołaj `workbook.calculateFormula();`, aby wymusić przeliczenie.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

## Profesjonalne wskazówki i typowe pułapki

| Sytuacja | Wskazówka |
|-----------|-----|
| **Pamięć podręczna tabeli przestawnej nie aktualizuje się** | Po skopiowaniu wywołaj `destSheet.getPivotTables().get(0).refresh();`, aby odświeżyć pamięć podręczną. |
| **Kopiowanie do innego skoroszytu** | Użyj `Workbook destWorkbook = new Workbook();`, a następnie `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. Pamiętaj, aby w razie potrzeby skopiować pamięć podręczną tabeli przestawnej osobno. |
| **Duże tabele przestawne** | Zwiększ rozmiar sterty Javy (`-Xmx2g`), aby uniknąć `OutOfMemoryError` podczas kopiowania. |
| **Zachowanie stylów** | Ustaw `copyOptions.setPasteType(PasteType.PASTE_ALL)`; w przeciwnym razie kopiowane będą tylko wartości. |

## Oczekiwany wynik

Uruchomienie pełnego programu generuje `output.xlsx`. Po otwarciu w Excelu:

* **Sheet2!A1:G20** wyświetla tę samą tabelę przestawną co **Sheet1!A1:G20**.
* Lista pól tabeli przestawnej, etykiety wierszy/kolumn oraz wartości danych odpowiadają źródłu.
* Odświeżenie tabeli przestawnej aktualizuje liczby, potwierdzając, że pamięć podręczna jest funkcjonalna.

Konsola wyświetli:

```
Pivot table copied successfully.
```

## Podsumowanie

W tym samouczku nauczyłeś się **jak skopiować tabelę przestawną** z jednego arkusza do drugiego przy użyciu Aspose.Cells for Java. Ładując skoroszyt, wybierając właściwy zakres źródłowy, definiując miejsce docelowe i konfigurując `CopyOptions`, możesz niezawodnie **skopiować zakres do innego arkusza** i **skopiować zakres między arkuszami**, zachowując pełną funkcjonalność tabeli przestawnej.

Następnie możesz zbadać:

* Eksportowanie skopiowanej tabeli przestawnej do PDF lub HTML.
* Automatyzację odświeżania tabel przestawnych w wielu skoroszytach.
* Użycie `CopyOptions` do kopiowania tylko wybranych elementów (np. wartości, formatów).

Śmiało eksperymentuj z różnymi adresami zakresów, strukturami skoroszytów lub nawet kopiami między skoroszytami. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak skopiować zakres w Javie – Kopiowanie tabeli przestawnej przy użyciu Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Jak skopiować tabelę przestawną w Javie – Kompletny przewodnik Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Kopiowanie tabeli przestawnej w Excel – Przewodnik krok po kroku przy użyciu Javy](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}