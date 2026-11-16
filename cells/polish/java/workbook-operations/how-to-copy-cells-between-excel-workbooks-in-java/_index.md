---
category: general
date: 2026-11-16
description: Jak kopiować komórki między skoroszytami Excela w Javie – załadować skoroszyt,
  skopiować zakres między skoroszytami (w tym tabelę przestawną) i zapisać plik skoroszytu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: pl
lastmod: 2026-11-16
og_description: Jak kopiować komórki między skoroszytami Excela w Javie. Dowiedz się,
  jak wczytać skoroszyt Excela, skopiować zakres (w tym tabelę przestawną) między
  skoroszytami oraz zapisać plik skoroszytu.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: Jak kopiować komórki między skoroszytami Excel w Javie – kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: Jak kopiować komórki między skoroszytami Excela w Javie
url: /pl/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak kopiować komórki między skoroszytami Excel w Javie

Jeśli potrzebujesz **skopiować komórki** z jednego skoroszytu Excel do drugiego przy użyciu Javy, ten przewodnik pokaże Ci niezawodny sposób, aby to zrobić. Nauczysz się, jak **załadować skoroszyt Excel w Javie**, skopiować zakres, który może zawierać tabelę przestawną, oraz w końcu **zapisać plik skoroszytu** z skopiowanymi danymi.

Ten tutorial obejmuje:

* Ładowanie źródłowego skoroszytu i wybór arkusza.  
* Zdefiniowanie dokładnego zakresu, który chcesz przenieść (w tym tabeli przestawnej).  
* Utworzenie docelowego skoroszytu i skopiowanie zakresu.  
* Zapisanie pliku docelowego.  

Przykład używa biblioteki Aspose.Cells for Java, która działa z plikami Excel bez wymogu posiadania Microsoft Office. Kod działa na Java 8+ oraz w dowolnym nowoczesnym IDE (IntelliJ IDEA, Eclipse, VS Code itp.).

---

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

| Wymaganie | Powód |
|-------------|--------|
| Java Development Kit (JDK) 8 lub nowszy | Wymagany do kompilacji i uruchomienia kodu. |
| Narzędzie budowania Maven lub Gradle | Ułatwia dodanie zależności Aspose.Cells. |
| Biblioteka Aspose.Cells for Java (najnowsza wersja) | Udostępnia klasy `Workbook`, `Worksheet` i `Range` używane w przykładzie. |
| Dwa pliki Excel (`source.xlsx` oraz pusty folder dla `dest.xlsx`) | Plik źródłowy musi zawierać dane i, opcjonalnie, tabelę przestawną, którą chcesz skopiować. |

Dodaj zależność Aspose.Cells do swojego `pom.xml` (Maven) lub `build.gradle` (Gradle). Przykład dla Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## Jak kopiować komórki z Aspose.Cells

Poniższe kroki przeprowadzą Cię przez cały proces. Każdy krok zawiera kod Java, wyjaśnienie **dlaczego** krok jest istotny oraz wskazówkę, jak uniknąć typowych pułapek.

### Krok 1: Załaduj źródłowy skoroszyt

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Dlaczego?**  
`Workbook` reprezentuje cały plik Excel. Załadowanie go daje dostęp do wszystkich arkuszy, komórek i obiektów, takich jak tabele przestawne. Użycie pierwszego arkusza jest powszechne, ale możesz wybrać dowolny arkusz po nazwie (`srcWb.getWorksheets().get("Sheet2")`).

**Porada:**  
Jeśli plik źródłowy jest duży, rozważ ładowanie w trybie *memory‑efficient*: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }});`

### Krok 2: Zdefiniuj zakres, który zawiera tabelę przestawną

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Dlaczego?**  
Obiekt `Range` abstrahuje prostokątny blok komórek. Określając `"A1:G20"` informujesz Aspose.Cells, które komórki — w tym wszelkie osadzone tabele przestawne — mają zostać skopiowane. Biblioteka automatycznie kopiuje dane, style i definicje tabel przestawnych.

**Przypadek brzegowy:**  
Jeśli tabela przestawna rozciąga się poza określony zakres, rozszerz adres (np. `"A1:Z100"`). Możesz także użyć `srcWs.getCells().getMaxDataColumn()` i `getMaxDataRow()`, aby dynamicznie obliczyć używany obszar.

### Krok 3: Utwórz docelowy skoroszyt

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Dlaczego?**  
Świeży skoroszyt zapewnia, że żadne niechciane formatowanie ani ukryte arkusze nie zakłócą skopiowanej zawartości. Domyślny skoroszyt już zawiera jeden arkusz, którego użyjemy jako docelowego.

### Krok 4: Skopiuj zakres do docelowego skoroszytu

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Dlaczego?**  
`copyRange` obsługuje wszystkie atrybuty komórek: wartości, formuły, formatowanie oraz nawet pamięci podręczne tabel przestawnych. Kopiując do `"A1"` umieszczasz zakres w lewym górnym rogu arkusza docelowego, zachowując pierwotny układ.

**Częste pytanie:** *Czy tabela przestawna pozostanie funkcjonalna?*  
Tak. Aspose.Cells kopiuje definicję tabeli przestawnej i jej pamięć podręczną, więc tabela działa dokładnie tak, jak w skoroszycie źródłowym.

### Krok 5: Zapisz docelowy skoroszyt

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Dlaczego?**  
Wywołanie `save` zapisuje skoroszyt w pamięci do fizycznego pliku `.xlsx`. Możesz także zapisać w innych formatach (`.xls`, `.csv`, `.pdf`) zmieniając rozszerzenie pliku lub używając `SaveOptions`.

**Wskazówka:**  
Jeśli potrzebujesz przesłać plik w odpowiedzi sieciowej, użyj `destWb.save(OutputStream, SaveFormat.XLSX);` zamiast ścieżki do pliku.

---

## Kopiowanie zakresu między skoroszytami – pełny kod źródłowy

Poniżej znajduje się kompletny, gotowy do uruchomienia kod klasy Java. Zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę na swoim komputerze.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Oczekiwany wynik:**  
`dest.xlsx` zawiera dokładną kopię zakresu `A1:G20` z `source.xlsx`. Jeśli zakres źródłowy zawierał tabelę przestawną, plik docelowy pokazuje tę samą tabelę z prawidłowo połączonym źródłem danych.

Możesz otworzyć `dest.xlsx` w Excelu, LibreOffice lub dowolnym przeglądarce obsługującej `.xlsx`, aby zweryfikować, że wartości, formatowanie i funkcjonalność tabeli przestawnej zostały zachowane.

---

## Kopiowanie skoroszytu z tabelą przestawną – co powinieneś wiedzieć

* **Pivot cache is copied automatically.** Biblioteka przenosi podlegającą pamięć podręczną, więc tabela przestawna nie wymaga ręcznego odświeżania.  
* **External data sources are not transferred.** Jeśli tabela przestawna pobiera dane z zewnętrznej bazy, musisz zapewnić, że skoroszyt docelowy ma dostęp do tego samego źródła lub odtworzyć pamięć podręczną lokalnie.  
* **Large pivot tables may increase memory usage.** Dla bardzo dużych skoroszytów rozważ zwiększenie przydziału pamięci JVM (`-Xmx2g`), aby uniknąć `OutOfMemoryError`.

---

## Zapisz plik skoroszytu w różnych formatach

Aspose.Cells pozwala zapisać wynik w wielu formatach bez dodatkowych zmian w kodzie:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

Wybierz format, który pasuje do Twojego procesu downstream. Ta sama logika `copyRange` działa niezależnie od wybranego formatu końcowego.

---

## Ładowanie skoroszytu Excel w Javie – dodatkowe wskazówki

* **Loading encrypted files:** Użyj `LoadOptions` z hasłem:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Reading only specific sheets:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

Te opcje mogą przyspieszyć krok **load excel workbook java**, szczególnie przy dużych plikach.

---

## Podsumowanie

Teraz wiesz, **jak kopiować komórki** między skoroszytami Excel w Javie, **jak kopiować zakres między skoroszytami**, który zawiera **tabelę przestawną**, oraz **jak zapisać plik skoroszytu** w potrzebnym formacie. Postępując zgodnie z powyższymi krokami, możesz zintegrować manipulację danymi Excel z dowolną aplikacją Java — niezależnie od tego, czy tworzysz silnik raportowy, potok ETL, czy prostą usługę konwersji plików.

**Kolejne kroki**, które możesz rozważyć:

* Użyj **copy range between workbooks**, aby scalić wiele raportów w

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Zapisz nowy skoroszyt w Javie – Tutorial kopiowania zakresu między skoroszytami](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [Jak kopiować tabele przestawne między skoroszytami Excel w Javie](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [Jak kopiować zakres w Javie – kopiowanie tabeli przestawnej z Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}