---
category: general
date: 2026-10-07
description: Dowiedz się, jak duplikować tabele przestawne w Excelu przy użyciu Javy
  i Aspose.Cells. Szybko skopiuj tabelę przestawną, kopiując jej zakres między skoroszytami.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: pl
lastmod: 2026-10-07
og_description: Jak duplikować tabele przestawne w Excelu przy użyciu Javy i Aspose.Cells.
  Postępuj zgodnie z tym przewodnikiem, aby skopiować tabelę przestawną, kopiując
  jej zakres między skoroszytami.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Jak duplikować tabele przestawne w Excelu przy użyciu Javy – pełny poradnik
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: Jak duplikować tabele przestawne w Excelu przy użyciu Javy – przewodnik krok
  po kroku
url: /pl/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak duplikować tabele przestawne w Excelu przy użyciu Javy – przewodnik krok po kroku

Jeśli potrzebujesz **jak duplikować tabelę przestawną** w skoroszycie Excel, ten tutorial pokazuje kompletną, gotową do uruchomienia rozwiązanie. Korzystając z Aspose.Cells for Java możesz skopiować tabelę przestawną wraz z jej danymi źródłowymi, kopiując podstawowy zakres, a następnie zapisać wynik jako nowy skoroszyt.

Duplikowanie tabeli przestawnej często wydaje się trudne, ponieważ pamięć podręczna tabeli przestawnej jest ukryta wewnątrz arkusza. Kopiując cały zakres, który zawiera tabelę przestawną, Aspose.Cells automatycznie odtwarza pamięć podręczną w docelowym skoroszycie, więc otrzymujesz w pełni funkcjonalną kopię bez ręcznego manipulowania XML.

W tym przewodniku:

* Załadujesz skoroszyt źródłowy zawierający tabelę przestawną.  
* Zdefiniujesz dokładny zakres obejmujący tabelę przestawną.  
* Skopiujesz ten zakres do nowego skoroszytu, zachowując definicję tabeli przestawnej.  
* Zapiszesz nowy plik i zweryfikujesz, że tabela przestawna działa.  

Kroki działają z każdą wersją Excela obsługiwaną przez Aspose.Cells (2007‑2024) i wymagają zaledwie kilku linii kodu Java.

## Wymagania wstępne

| Wymaganie | Dlaczego jest to ważne |
|-------------|----------------|
| **Java 8 or newer** | Aspose.Cells jest zbudowany dla Java 8+. |
| **Aspose.Cells for Java** (latest version) | Udostępnia API `Workbook`, `Range` i `CopyRange` używane w przykładzie. |
| **Source workbook** with a pivot table (e.g., `Source.xlsx`) | Tabela przestawna, którą chcesz zduplikować. |
| **Write permission** to the target directory | Wymagana do zapisania `CopyWithPivot.xlsx`. |

Dodaj zależność Maven Aspose.Cells do swojego `pom.xml` (lub pobierz JAR ręcznie):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## Jak duplikować tabele przestawne – pełna implementacja

Poniżej znajduje się samodzielny program Java, który demonstruje **jak duplikować tabelę przestawną** poprzez kopiowanie zakresu zawierającego tabelę przestawną. Kod zawiera obsługę błędów, komentarze i krok weryfikacji.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### Wyjaśnienie każdego kroku

| Krok | Co robi kod | Dlaczego jest to ważne przy **kopiowaniu tabeli przestawnej** |
|------|-------------|----------------------------------------|
| **1️⃣ Load source workbook** | `new Workbook(srcPath)` odczytuje `Source.xlsx`. | Plik źródłowy jest jedynym miejscem, w którym istnieje oryginalna tabela przestawna. |
| **2️⃣ Define the range** | `createRange("A1:G20")` tworzy obiekt `Range`, który obejmuje tabelę przestawną i jej dane. | Tabela przestawna jest przechowywana razem z pamięcią podręczną; kopiowanie całego zakresu zapewnia przeniesienie również pamięci podręcznej. |
| **3️⃣ Copy the range** | `copyRange(srcRange, "A1")` zapisuje zakres w docelowym arkuszu. | To jest sedno **kopiowania zakresu między skoroszytami** – API automatycznie obsługuje ukryte obiekty. |
| **4️⃣ Refresh pivot** | `pivotTable.refresh()` wymusza przeliczenie tabeli przestawnej. | Gwarantuje, że zduplikowana tabela przestawna wyświetla te same wartości co oryginał, szczególnie po modyfikacjach. |
| **5️⃣ Save workbook** | `destWb.save(destPath)` zapisuje plik na dysku. | Tworzy ostateczny wynik **kopiowania zakresu Excel**, który możesz otworzyć w Excelu. |

#### Oczekiwany wynik

Po uruchomieniu programu otwórz `CopyWithPivot.xlsx`. Zobaczysz arkusz wyglądający identycznie jak arkusz źródłowy, a tabela przestawna działa dokładnie tak jak oryginał – możesz rozwijać wiersze, filtrować pola i odświeżać dane bez błędów.

## Typowe warianty i przypadki brzegowe

### 1️⃣ Kopiowanie tabeli przestawnej obejmującej wiele arkuszy

Jeśli dane źródłowe tabeli przestawnej znajdują się na innym arkuszu niż sama tabela, uwzględnij oba arkusze w operacji kopiowania. Najprostsze podejście to najpierw skopiować cały arkusz źródłowy, a następnie skopiować arkusz z tabelą przestawną:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Obsługa nazwanych zakresów

Aspose.Cells zachowuje nazwane zakresy podczas kopiowania zakresu. Jednak jeśli docelowy skoroszyt już zawiera nazwę o tym samym identyfikatorze, zostanie rzucony `CellsException`. Rozwiąż to, zmieniając nazwę konfliktującego zakresu przed kopiowaniem:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Duże skoroszyty i wydajność

Kopiowanie bardzo dużych zakresów (setki tysięcy wierszy) może być intensywne pod względem pamięci. Włącz **optymalizację pamięci**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Zachowanie integralności formuł

Jeśli zakres źródłowy zawiera formuły odwołujące się do komórek poza kopiowanym obszarem, te odwołania zostaną zerwane po kopiowaniu. Aby tego uniknąć, rozszerz zakres tak, aby obejmował wszystkie zależne komórki, lub użyj `copyRange` z flagą `CopyOptions` `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Porady profesjonalne dla niezawodnego **kopiowania zakresu między skoroszytami**

* **Always use absolute addresses** (`$A$1:$G$20`) when the source sheet may be renamed.  
* **Refresh after copy** – even though Aspose.Cells rebuilds the cache, calling `refresh()` eliminates occasional stale‑cache warnings in Excel.  
* **Validate the pivot**: after saving, open the file programmatically and call `pivotTable.validate()` to ensure no broken references.  
* **Version compatibility**: the code works with Excel 2007‑2024 files (`.xlsx`, `.xlsm`). For legacy `.xls` files, set `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## Pełny listing źródłowy (gotowy do kompilacji)

```java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // --------------------------------------------------------------------
        // 1️⃣ Load source workbook
        // --------------------------------------------------------------------
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 2️⃣ Define the range that contains the pivot table
        // --------------------------------------------------------------------
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        String pivotRangeAddress = "A1:G20"; // adjust to your pivot's actual area
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // --------------------------------------------------------------------
        // 3️⃣ Copy the range (including the pivot) to a new workbook
        // --------------------------------------------------------------------
        Workbook destWb = new Workbook(); // blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 4️⃣ Refresh the duplicated pivot (ensures correct values)
        // --------------------------------------------------------------------
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet


## Co powinieneś się nauczyć dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak skopiować tabelę przestawną w Javie – kompletny przewodnik Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Jak tworzyć tabele przestawne w Excelu przy użyciu Aspose.Cells for Java: kompleksowy przewodnik](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Jak zaktualizować źródło tabeli przestawnej w Excelu przy użyciu Aspose.Cells for Java: kompleksowy przewodnik](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}