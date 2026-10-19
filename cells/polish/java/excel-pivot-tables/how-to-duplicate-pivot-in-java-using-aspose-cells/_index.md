---
category: general
date: 2026-09-18
description: jak duplikować tabelę przestawną w Javie przy użyciu Aspose.Cells – szybko
  i niezawodnie kopiować tabelę przestawną między skoroszytami
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: pl
lastmod: 2026-09-18
og_description: jak duplikować tabelę przestawną w Javie przy użyciu Aspose.Cells.
  Przejrzyj ten kompletny samouczek, aby skopiować tabelę przestawną między skoroszytami
  przy użyciu czystego kodu Java.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Duplikowanie tabeli przestawnej w Javie – przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak zduplikować tabelę przestawną w Javie przy użyciu Aspose.Cells
url: /pl/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak duplikować tabelę przestawną w Javie przy użyciu Aspose.Cells

Jeśli potrzebujesz **jak duplikować tabelę przestawną** w aplikacji Java, ten przewodnik pokaże Ci dokładne kroki. Ładując skoroszyt Excel, definiując obszar komórek tabeli przestawnej i kopiując ten zakres do nowego skoroszytu, możesz przenieść tabelę przestawną bez utraty jej definicji ani danych.

Kopiowanie tabeli przestawnej jest częstym wymogiem, gdy generujesz raporty, archiwizujesz analizy lub dzielisz duży skoroszyt na modułowe części. W tym samouczku dowiesz się, jak **skopiować zakres między skoroszytami**, jak **załadować skoroszyt Excel w Javie**, oraz jak bezpiecznie **skopiować tabelę przestawną**.

Zakończysz z gotowym do uruchomienia programem Java, który duplikuje tabelę przestawną z `Source.xlsx` do `PivotCopied.xlsx` przy użyciu Aspose.Cells dla Javy.

## Wymagania wstępne

* Zainstalowany JDK 8 lub nowszy.
* Maven (lub inne narzędzie budujące) do zarządzania zależnościami.
* Aspose.Cells for Java w wersji 23.10 lub późniejszej. Dodaj następującą zależność Maven do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* Źródłowy skoroszyt (`Source.xlsx`) zawierający tabelę przestawną w zakresie **A1:H30**.

## Jak duplikować tabelę przestawną w Javie

Podstawowa idea jest prosta:

1. **Załaduj źródłowy skoroszyt** – daje Ci dostęp do arkusza, który zawiera tabelę przestawną.
2. **Zdefiniuj obszar komórek** obejmujący tabelę przestawną.
3. **Utwórz docelowy skoroszyt** – pusty plik, który otrzyma skopiowany zakres.
4. **Skopiuj zakres** – Aspose.Cells automatycznie duplikuje definicję tabeli przestawnej.
5. **Zapisz docelowy skoroszyt** – masz teraz osobny plik z taką samą tabelą przestawną.

Poniżej znajduje się kompletny, gotowy do uruchomienia program Java, który realizuje te kroki.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Dlaczego to działa

* **Aspose.Cells** traktuje tabelę przestawną jako część kolekcji komórek arkusza. Gdy wywołujesz `copyRange`, biblioteka kopiuje nie tylko wartości komórek, ale także podlegający cache i definicję tabeli przestawnej, dzięki czemu nowy skoroszyt zawiera w pełni funkcjonalny duplikat.
* Obiekt `CopyOptions` domyślnie zachowuje formuły, formaty i osadzone obiekty. Możesz go dostosować (np. `setCopyColumnWidths(true)`), jeśli potrzebujesz dodatkowej kontroli.

## Kopiowanie zakresu między skoroszytami – szczegółowy przegląd

Choć powyższy przykład kopiuje pojedynczy spójny blok, `copyRange` może obsłużyć dowolny prostokątny obszar. Jeśli Twoja tabela przestawna obejmuje nieprzyległe zakresy, możesz wywołać `copyRange` wielokrotnie lub użyć `Worksheet.copy`, aby zduplikować cały arkusz.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Wskazówka:** Przy kopiowaniu dużych skoroszytów włącz `CopyOptions.setPreserveCellStyle(true)`, aby uniknąć niepotrzebnego duplikowania stylów, co może poprawić wydajność.

## Jak skopiować tabelę przestawną do skoroszytu – obsługa wielu tabel przestawnych

Jeśli arkusz źródłowy zawiera więcej niż jedną tabelę przestawną, możesz iterować po tabelach przestawnych arkusza i kopiować każdą z osobna:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

To podejście zapewnia, że każda tabela przestawna zachowuje swoją pierwotną nazwę i źródło danych.

## Ładowanie skoroszytu Excel w Javie – typowe pułapki

* **Separatory ścieżek plików:** Używaj ukośników (`/`) lub `File.separator`, aby kod był niezależny od platformy.
* **Brak licencji:** Aspose.Cells działa w trybie ewaluacyjnym, ale wynik będzie zawierał znak wodny. Zarejestruj licencję przy pomocy `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` przed załadowaniem skoroszytu, aby usunąć znak wodny.
* **Duże pliki:** Dla skoroszytów większych niż 100 MB rozważ użycie `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` z opcjami strumieniowania, aby zmniejszyć zużycie pamięci.

## Pełny przykład od początku do końca – podsumowanie

Łącząc wszystkie elementy, oto ostateczny program, który możesz skopiować i wkleić do swojego IDE:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Oczekiwany wynik:** Po wykonaniu, `PivotCopied.xlsx` pojawia się w określonym katalogu. Otwierając go w Excelu, zobaczysz taki sam układ tabeli przestawnej, filtry i dane jak w `Source.xlsx`. Wszystkie pola obliczeniowe i formatowanie są zachowane.

## Najczęściej zadawane pytania

* **Czy to działa ze starszymi formatami Excela (.xls)?**  
  Tak. Aspose.Cells automatycznie wykrywa format. Użyj `new Workbook("file.xls")` i ta sama logika kopiowania ma zastosowanie.

* **Co jeśli tabela przestawna odwołuje się do zewnętrznych źródeł danych?**  
  Kopia zachowuje pierwotne odwołanie do źródła danych. Jeśli środowisko docelowe nie może uzyskać dostępu do tego źródła, tabela przestawna wyświetli błędy `#REF!`. Aby tego uniknąć, odśwież tabelę po skopiowaniu lub zmień jej źródło danych za pomocą `PivotTable.setDataSource(...)`.

* **Czy mogę skopiować tabelę przestawną do konkretnej nazwy arkusza?**  
  Oczywiście. Po utworzeniu docelowego arkusza, zmień jego nazwę:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Podsumowanie

Teraz wiesz, **jak duplikować tabele przestawne** w Javie przy użyciu Aspose.Cells, **jak kopiować zakres między skoroszytami** oraz najlepsze praktyki **ładowania skoroszytu Excel w Javie**. Stosując pięcioetapowy proces — ładowanie, definiowanie, tworzenie docelowego skoroszytu, kopiowanie i zapisywanie — możesz automatyzować generowanie raportów, archiwizować analizy lub dzielić złożone skoroszyty bez utraty funkcjonalności tabel przestawnych.

Następnie, zapoznaj się z powiązanymi tematami, takimi jak **kopiowanie tabeli przestawnej do skoroszytu** z wieloma arkuszami, lub zintegrowanie zduplikowanej tabeli przestawnej w większym potoku przetwarzania danych przy użyciu Apache POI w scenariuszach nie‑Aspose. Eksperymentuj z różnymi ustawieniami `CopyOptions`, aby precyzyjnie dostroić wydajność przy bardzo dużych skoroszytach.

Miłego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak tworzyć tabele przestawne w Excelu przy użyciu Aspose.Cells dla Javy: Kompletny przewodnik](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Jak zaktualizować źródło tabeli przestawnej w Excelu przy użyciu Aspose.Cells dla Javy: Kompletny przewodnik](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Grupowanie pól tabeli przestawnej w skoroszytach Excel przy użyciu Aspose.Cells dla Javy – Kompletny przewodnik](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}