---
category: general
date: 2026-06-30
description: Sortuj unikalne wartości w Excelu przy użyciu Javy. Dowiedz się, jak
  ustawiać formuły, przeliczać formuły i generować unikalną listę w Excelu za pomocą
  Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: pl
og_description: Sortuj unikalne wartości w Excelu przy użyciu Javy. Ten przewodnik
  pokazuje, jak ustawić formułę, przeliczyć formuły i w ciągu kilku minut wygenerować
  unikalną listę w Excelu.
og_title: Sortowanie unikalnych wartości w Excelu – Samouczek Java dla formuł tablicowych
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Sortowanie unikalnych wartości w Excelu – Kompletny przewodnik Java po ustawianiu
  formuł tablicowych
url: /pl/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sort Unique Values Excel – Complete Java Guide to Set Array Formulas

Zastanawiałeś się kiedyś, jak **sort unique values Excel** bez przeciągania formuł? Nie jesteś jedyny. W wielu scenariuszach raportowania potrzebna jest czysta, alfabetycznie posortowana lista odrębnych wpisów, a robienie tego ręcznie jest uciążliwe.  

Dobre wieści? Kilka linii kodu Java pozwala **set array formula** na arkuszu, a następnie **recalculate formulas**, dzięki czemu rozprzestrzeniony zakres wypełnia się automatycznie. W tym samouczku przeprowadzimy Cię przez wszystko — od tworzenia skoroszytu po generowanie unikalnej listy w stylu Excel — abyś mógł osadzić rozwiązanie bezpośrednio w swojej aplikacji.

## Co obejmuje ten samouczek

- Ustawienie projektu Java z Aspose.Cells (biblioteka napędzająca fragment kodu).  
- Użycie funkcji `SORT` i `UNIQUE` razem, aby **generate unique list Excel** wyniki.  
- Zastosowanie **array formula** do komórki programowo.  
- Wywołanie przebiegu obliczeń, aby krok **how to recalculate formulas** odbył się natychmiast.  
- Weryfikacja wyniku i dostosowanie rozwiązania do przypadków brzegowych, takich jak puste komórki lub nieciągłe zakresy.

Po zakończeniu tego przewodnika będziesz mógł wstawić gotową metodę do dowolnej usługi Java, która potrzebuje eksportować czyste arkusze Excel.

> **Pro tip:** Jeśli już używasz Maven, dodanie Aspose.Cells jako zależności oszczędza Ci ręcznego zarządzania plikami JAR.

---

## Wymagania wstępne

| Requirement | Why it matters |
|-------------|----------------|
| Java 8 or newer | Aspose.Cells targets Java 8+. |
| Maven (or Gradle) | Upraszcza zarządzanie zależnościami. |
| Aspose.Cells for Java | Udostępnia `Workbook`, `Worksheet` oraz API formuł, których użyjemy. |
| Basic familiarity with Excel functions | Zrozumienie `SORT` i `UNIQUE` pomaga dostosować kod. |

> *Jeśli jeszcze nie masz Aspose.Cells, dodaj to do swojego `pom.xml`*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Krok 1: Utwórz nowy skoroszyt (Jak rozpocząć ustawianie formuły)

Najpierw potrzebujemy pustego skoroszytu. Traktuj go jak pustą płótno, na którym później **set array formula** w komórce `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Dlaczego tworzyć nowy skoroszyt?*  
> Gwarantuje czyste środowisko, unikając ukrytych formuł, które mogłyby zakłócić nasze dane testowe.

---

## Krok 2: Wypełnij przykładowe dane (Opcjonalne, ale przydatne)

Aby wyraźnie zobaczyć wynik, wypełnijmy kolumnę **B** kilkoma powtarzającymi się wpisami.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *Dlaczego używać kolumny B?*  
> Formuła, którą napiszemy, odwołuje się do `B1:B10`, więc umieszczenie danych w tej kolumnie odzwierciedla klasyczny przykład w Excel.

---

## Krok 3: Ustaw formułę tablicową, która **Sort Unique Values Excel**

Teraz dzieje się magia. Łączymy `UNIQUE` (aby usunąć duplikaty) z `SORT` (aby posortować je alfabetycznie). Powstałe wyrażenie jest **array formula**, co oznacza, że automatycznie rozleje się na sąsiednie komórki.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Jak to działa

- `UNIQUE(B1:B10)` przeszukuje zakres i zwraca pionową tablicę unikalnych ciągów.  
- `SORT(...)` przyjmuje tę tablicę i sortuje ją rosnąco.  
- Otoczenie całego wyrażenia znakiem `=` i wywołanie `setFormulaArray` informuje Aspose.Cells, aby traktował wynik jako **spilled array**, tak jak w Excel.

> **Note:** Jeśli używasz starszej wersji Excel, która nie posiada `SORT` lub `UNIQUE`, możesz cofnąć się do `SORT(UNIQUE(...))` z funkcją **LET** lub użyć starszych formuł tablicowych (`=INDEX(...)`). Samouczek koncentruje się na nowoczesnym podejściu dynamicznych tablic, ponieważ jest to najczystszy sposób na **generate unique list Excel** dzisiaj.

---

## Krok 4: Przelicz formuły, aby rozprzestrzeniony zakres został wypełniony

Po umieszczeniu formuły, skoroszyt nie ocenia jej automatycznie. To tutaj wkracza krok **how to recalculate formulas**.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Wywołanie `calculateFormula()` zmusza Aspose.Cells do uruchomienia silnika Excel, wypełniając komórki `A1`, `A2`, … posortowanymi unikalnymi wartościami.

> *Dlaczego nie polegać na leniwej ewaluacji?*  
> W kontekście po stronie serwera często potrzebujesz danych gotowych do eksportu (CSV, PDF itp.) zaraz po obliczeniu, więc wywołanie explicite zapewnia spójność.

---

## Krok 5: Zweryfikuj wynik (Opcjonalne debugowanie)

Zawsze warto wydrukować rozprzestrzenione wartości na konsolę — szczególnie gdy uczysz się nowego API.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

Uruchomienie programu wypisuje:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

Otwórz `SortedUniqueValues.xlsx` i zobaczysz te same dane rozlewające się od `A1` w dół.

---

## Obsługa przypadków brzegowych

### Puste komórki w zakresie źródłowym

Jeśli `B1:B10` zawiera puste komórki, `UNIQUE` potraktuje je jako odrębny wpis. Aby pominąć puste, otocz zakres funkcją `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Dane nieciągłe

Gdy Twoje dane znajdują się w wielu kolumnach, możesz je połączyć przy pomocy `CHOOSE` lub `TEXTJOIN` przed zastosowaniem `UNIQUE`. Na przykład:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Te modyfikacje pokazują elastyczność **how to set formula** w bardziej złożonych scenariuszach.

---

## Pełny działający przykład (wszystkie kroki połączone)

Poniżej znajduje się kompletny, uruchamialny program Java. Skopiuj‑wklej go do swojego IDE, dodaj zależność Aspose.Cells i naciśnij *Run*.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Expected output** (wyświetlony w konsoli) odpowiada posortowanej, odduplikowanej liście, o której rozmawialiśmy wcześniej. Otwierając wygenerowany plik Excel, zobaczysz te same wartości rozlewające się od `A1` w dół.

---

## Najczęściej zadawane pytania

**Q: Czy to działa ze starszymi wersjami Excel (przed Office 365)?**  
A: Funkcje `SORT` i `UNIQUE` są częścią silnika Dynamic Array wprowadzonego w Excel 365. Dla starszych plików trzeba używać klasycznych formuł tablicowych, takich jak `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells nadal potrafi je ocenić, ale składnia jest bardziej rozbudowana.

**Q: Czy mogę ustawić formułę tablicową w innym zakresie niż `A1`?**  
A: Oczywiście. Po prostu zmień adres w `cells.get("A1")`. Rozlewana tablica zawsze zacznie się w podanej komórce i rozciągnie się w prawo i w dół w razie potrzeby.

**Q: Co jeśli moje dane źródłowe są większe niż `B1:B10`?**  
A: Zastąp statyczny zakres dynamicznym, np. `B:B` lub nazwanym zakresem. Formuła stanie się `=SORT(UNIQUE(B:B))`. Bądź ostrożny przy odwołaniach do całych kolumn w bardzo dużych arkuszach; mogą one wpływać na wydajność.

---

## Zakończenie

Właśnie omówiliśmy **how to set formula** w Javie, aby **sort unique values Excel**, jak **recalculate formulas**, oraz jak **generate unique list Excel** przy użyciu potężnego API Aspose.Cells. Kroki są proste: utwórz skoroszyt, wypełnij danymi, zastosuj formułę tablicową, wywołaj obliczenia i zweryfikuj wynik.  

Od tego momentu możesz rozbudować rozwiązanie — dodać formatowanie warunkowe, eksport do PDF lub zintegrować metodę z usługą webową, która dostarcza gotowe raporty. Główna idea pozostaje taka sama: pozwól funkcjom Excela wykonać ciężką pracę, a Javie zarządzać procesem.

Gotowy, aby podnieść poziom automatyzacji Excela? Spróbuj zamienić `SORT` na `SORTBY`, aby sortować według drugiej kolumny, lub poeksperymentuj z `FILTER`, aby wykluczyć wiersze nie spełniające reguł biznesowych. Możliwości są praktycznie nieograniczone.

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}