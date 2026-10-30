---
category: general
date: 2026-08-08
description: Jak skopiować tabelę przestawną w Aspose.Cells i skopiować zakres do
  skoroszytu przy użyciu Javy. Dowiedz się, jakie są dokładne kroki, aby zduplikować
  tabelę przestawną przy użyciu CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: pl
lastmod: 2026-08-08
og_description: Jak skopiować tabelę przestawną w Aspose.Cells i skopiować zakres
  do skoroszytu w Javie. Przejrzyj ten kompletny przewodnik, aby zduplikować tabelę
  przestawną przy użyciu CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Jak skopiować tabelę przestawną w Aspose.Cells – skopiuj zakres do skoroszytu
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Jak skopiować tabelę przestawną w Aspose.Cells – skopiuj zakres do skoroszytu
url: /pl/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skopiować tabelę przestawną w Aspose.Cells – kopiowanie zakresu do skoroszytu

Jeśli potrzebujesz **jak skopiować tabelę przestawną** w pliku Excel przy użyciu Aspose.Cells, ten przewodnik pokaże Ci dokładny proces. Po zakończeniu samouczka będziesz w stanie **skopiować zakres do skoroszytu**, zachowując definicję tabeli przestawnej.

Przykład używa Javy, ale te same koncepcje mają zastosowanie do dowolnego języka .NET współpracującego z Aspose.Cells. Nie są wymagane żadne zewnętrzne narzędzia — wystarczy biblioteka Aspose.Cells for Java oraz podstawowe środowisko programistyczne.

## Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz:

* Java Development Kit (JDK) 8 lub nowszy.
* Maven lub Gradle do zarządzania zależnościami (przykład używa Maven).
* Aspose.Cells for Java 23.9 (lub najnowsza wersja) dodana do Twojego projektu.
* Skoroszyt wejściowy (`input.xlsx`) zawierający przynajmniej jedną tabelę przestawną w pierwszym arkuszu.

Posiadanie tych elementów zapobiega błędom w czasie wykonywania, gdy kod odwołuje się do skoroszytu.

## Jak skopiować tabelę przestawną przy użyciu Aspose.Cells

Ta sekcja przeprowadza przez każdy krok niezbędny do **skopiowania tabeli przestawnej** z jednej części arkusza do drugiej, przy użyciu klasy `CopyOptions`.

### Krok 1: Dodaj Aspose.Cells do swojego projektu

Jeśli używasz Maven, dodaj następującą zależność do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Dlaczego ten krok jest ważny*: Biblioteka dostarcza klasy `Workbook`, `CopyOptions` i inne niezbędne do operacji **aspose.cells copy range**. Bez tej zależności kompilator nie może rozpoznać tych typów.

### Krok 2: Załaduj źródłowy skoroszyt

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Załadowanie pliku tworzy w‑pamięci reprezentację arkusza kalkulacyjnego. Obiekt `Workbook` zapewnia dostęp do arkuszy, komórek i tabel przestawnych.

### Krok 3: Skonfiguruj opcje kopiowania, aby uwzględnić tabelę przestawną

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` informuje Aspose.Cells, że operacja powinna zachować metadane tabeli przestawnej. Jeśli pominiesz tę flagę, tabela przestawna zostanie zredukowana do danych statycznych, tracąc interaktywność.

### Krok 4: Skopiuj żądany zakres wraz z tabelą przestawną

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

Metoda `copyRange` kopiuje komórki, formatowanie oraz — dzięki ustawieniom z poprzedniego kroku — wszystkie tabele przestawne, które przecinają zakres. To jest sedno funkcjonalności **copy range to workbook**.

### Krok 5: Zapisz zmodyfikowany skoroszyt

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Zapis zapisuje zmiany do nowego pliku (`output.xlsx`). Teraz możesz otworzyć ten plik w Excelu i zobaczyć, że tabela przestawna została dokładnie zduplikowana w miejscu, gdzie zakres został skopiowany.

## Pełny, działający przykład

Łącząc wszystkie elementy, oto kompletny program, który możesz skompilować i uruchomić:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Oczekiwany wynik

* `output.xlsx` zawiera te same dane co `input.xlsx`.
* Tabela przestawna, która pierwotnie zajmowała zakres źródłowy, pojawia się w komórkach docelowych, w pełni funkcjonalna (filtry, możliwość odświeżania itp.).
* Wszystkie formatowania komórek, formuły i szerokości kolumn są zachowane, ponieważ `copyRange` kopiuje cały blok komórek.

## Częste pytania i przypadki brzegowe

**Co zrobić, jeśli zakres docelowy zachodzi na istniejącą tabelę przestawną?**  
Aspose.Cells nadpisze komórki docelowe. Aby uniknąć utraty danych, upewnij się, że obszar docelowy jest pusty lub najpierw przenieś istniejącą tabelę przestawną.

**Czy mogę skopiować tabelę przestawną między arkuszami?**  
Tak. Użyj `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);`, gdzie `targetSheetIndex` wskazuje na arkusz docelowy.

**Czy `setCopyPivotTable(true)` kopiuje podstawowe źródło danych?**  
Metoda kopiuje tylko odwołanie do pamięci podręcznej tabeli przestawnej. Jeśli dane źródłowe znajdują się w tym samym skoroszycie, tabela przestawna w miejscu docelowym będzie wskazywać tę samą pamięć podręczną. Aby zduplikować pamięć podręczną, musisz ręcznie utworzyć nową pamięć podręczną tabeli przestawnej.

**Jak efektywnie skopiować duży zakres?**  
Podczas kopiowania bardzo dużych zakresów rozważ użycie `CopyOptions.setCopyFormula(true)` i `setCopyDataValidation(true)` tylko w razie potrzeby. Zmniejszenie liczby opcji może poprawić wydajność.

## Wskazówki dotyczące niezawodnego użycia **aspose.cells copy range**

* **Pro tip:** Zawsze wywołuj `workbook.calculateFormula()` po kopiowaniu, jeśli zakres zawiera formuły zależne od pamięci podręcznej tabeli przestawnej.
* **Uwaga:** Ukryte arkusze. `copyRange` działa tylko na widocznych arkuszach, chyba że wyraźnie odwołasz się do ukrytego arkusza po indeksie.
* **Sprawdź wersję:** Flaga `setCopyPivotTable` jest dostępna od Aspose.Cells 20.9. Upewnij się, że Twoja wersja biblioteki ją obsługuje.

## Podsumowanie

Teraz wiesz **jak skopiować tabelę przestawną** w Aspose.Cells oraz jak **skopiować zakres do skoroszytu**, zachowując pełną funkcjonalność tabeli przestawnej. Kroki — dodanie biblioteki, załadowanie skoroszytu, skonfigurowanie `CopyOptions`, wykonanie kopiowania i zapis — tworzą powtarzalny wzorzec, który możesz zastosować w innych scenariuszach kopiuj‑wklej.

Następnie zapoznaj się z powiązanymi tematami, takimi jak **aspose.cells copy range** dla wykresów, formatowania warunkowego i walidacji danych. Eksperymentuj z kopiowaniem między różnymi formatami plików (XLSX → XLS), aby rozszerzyć możliwości automatyzacji. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak tworzyć tabele przestawne w Excelu przy użyciu Aspose.Cells dla Javy&#58; Kompletny przewodnik](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Jak zaktualizować źródło tabeli przestawnej w Excelu przy użyciu Aspose.Cells dla Javy&#58; Kompletny przewodnik](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Jak wdrożyć segmentatory w tabelach przestawnych przy użyciu Aspose.Cells dla Javy&#58; Kompletny przewodnik](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}