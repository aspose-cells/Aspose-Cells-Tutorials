---
category: general
date: 2026-03-01
description: Dowiedz się, jak wyeksportować plik CSV z zeszytu Java, jednocześnie
  ustawiając znaczące cyfry i zakres eksportu do CSV w jednym, przejrzystym przewodniku.
draft: false
keywords:
- how to export csv
- set significant digits
- export range to csv
- Java workbook export
- CSV formatting Java
language: pl
og_description: Opanuj eksport CSV w Javie, ustawianie znaczących cyfr oraz eksport
  zakresu do CSV, korzystając z praktycznego kodu i wskazówek.
og_title: Jak wyeksportować CSV w Javie – pełny przewodnik krok po kroku
tags:
- Java
- Aspose.Cells
- CSV
- Data Export
title: Jak eksportować CSV w Javie – Ustaw znaczące cyfry i zakres eksportu do CSV
url: /pl/java/excel-import-export/how-to-export-csv-with-java-set-significant-digits-export-ra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyeksportować CSV w Javie – Ustaw znaczące cyfry i zakres eksportu do CSV

Zastanawiałeś się kiedyś **jak wyeksportować csv** z skoroszytu Java bez utraty precyzji numerycznej? Być może próbowałeś szybkiego `toString()` i skończyło się na bałaganie z błędami zaokrągleń. To częsty problem, szczególnie gdy musisz **ustawić znaczące cyfry** dla danych finansowych lub wyników naukowych.  

W tym tutorialu zobaczysz kompletny, gotowy do uruchomienia przykład, który pokazuje **jak wyeksportować csv**, jak **ustawić znaczące cyfry**, a nawet jak **wyeksportować zakres do csv**, zachowując porządek w danych. Przejdziemy przez każdy wiersz, wyjaśnimy *dlaczego* wywołania API są takie, a nie inne, i podpowiemy, jak uniknąć typowych pułapek. Bez dodatkowej dokumentacji do przeszukiwania — po prostu samodzielne rozwiązanie, które możesz skopiować i wkleić już dziś.

## Czego się nauczysz

- Utwórz skoroszyt i skonfiguruj precyzję numeryczną przy użyciu `setNumberSignificantDigits`.
- Wyeksportuj określony zakres komórek jako ładnie sformatowany ciąg CSV.
- Parsuj daty w japońskim erze przy użyciu `DateTimeFormatInfo`.
- Przelicz formuły, aby wyniki dynamicznych tablic były aktualne.
- Wygeneruj tabelę przestawną jako obraz PNG.
- Użyj Smart Marker, aby wstawić komentarze i ostatecznie zapisać skoroszyt.

Wszystko to realizowane jest przy pomocy biblioteki Aspose.Cells for Java, wersja 23.12 (najnowsza w momencie pisania). Jeśli masz plik JAR na classpath, jesteś gotowy do działania.

---

## Krok 1: Utwórz skoroszyt i **Ustaw znaczące cyfry**

Zanim będziemy mogli cokolwiek wyeksportować, potrzebujemy obiektu skoroszytu. Pierwszą rzeczą, którą wielu programistów pomija, jest precyzja numeryczna. Domyślnie Aspose.Cells używa pełnej precyzji podwójnej, co może prowadzić do długich, nieporęcznych ciągów w CSV. Ustawienie liczby znaczących cyfr przycina wynik, zachowując najważniejsze cyfry.

```java
import com.aspose.cells.*;

public class CsvExportDemo {

    public static void main(String[] args) throws Exception {

        // Step 1 – initialise workbook and limit numeric values to 5 significant digits
        Workbook workbook = new Workbook();
        WorkbookSettings settings = workbook.getSettings();
        // This is the key call that **set significant digits** for all numeric cells
        settings.setNumberSignificantDigits(5);
```

**Dlaczego to ważne?**  
Jeśli wyeksportujesz komórkę zawierającą `12345.6789` bez ograniczania cyfr, CSV pokaże pełną wartość, zagracając raporty. Z `setNumberSignificantDigits(5)` ta sama komórka stanie się `12346`, co często jest tym, czego oczekują użytkownicy biznesowi.

> **Pro tip:** Jeśli potrzebujesz innej precyzji w poszczególnych kolumnach, możesz zastosować niestandardowy `Style` zamiast ustawienia globalnego.

---

## Krok 2: **Export Range to CSV** – Formatowanie ma znaczenie

Teraz, gdy skoroszyt jest gotowy, pobierzmy prostokątny blok danych i przekształćmy go w ciąg CSV. Zastosujemy także format dwukropkowy (`0.00`), aby każda liczba była ładnie wyrównana.

```java
        // Step 2 – define export options and pull the range B2:D10 as CSV
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);          // we want a string, not a file yet
        exportOptions.setNumberFormat("0.00");          // enforce two decimal places

        // Create a dummy range with some sample data for illustration
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
        cells.get("B2").putValue(123.456);
        cells.get("C2").putValue(78.9);
        cells.get("D2").putValue(0.12345);
        // ... populate more rows as needed ...

        Range dataRange = cells.createRange("B2:D10");
        String csvData = dataRange.exportDataTable(exportOptions).toString();

        System.out.println("=== CSV Output ===");
        System.out.println(csvData);
```

Wywołanie `exportDataTable` wykonuje najcięższą pracę. Ponieważ ustawiliśmy `exportAsString`, metoda zwraca `String`, który możemy wydrukować, zapisać do pliku lub wysłać przez HTTP. Krok **export range to csv** respektuje także globalne `setNumberSignificantDigits`, które zdefiniowaliśmy wcześniej, więc liczby są zarówno zaokrąglone do pięciu znaczących cyfr, *jak i* wyświetlane z dwoma miejscami po przecinku.

**Oczekiwany wynik (skrócony):**

```
=== CSV Output ===
123.46,78.90,0.12
...
```

> **Common question:** *Co zrobić, jeśli potrzebny jest inny separator, np. średnik?*  
> Po prostu wywołaj `exportOptions.setSeparator(";")` przed eksportem.

---

## Krok 3: Parsowanie daty w japońskim erze (dodatkowe narzędzie)

Choć nie jest to bezpośrednio związane z CSV, wiele arkuszy Excel zawiera daty specyficzne dla lokalizacji. Oto jak zamienić japoński ciąg erowy, taki jak `"R3/04/01"`, na standardowy obiekt `DateTime`.

```java
        // Step 3 – parse Japanese era date (Reiwa 3)
        DateTime japaneseDate = DateTime.parse("R3/04/01", new DateTimeFormatInfo(Locale.JAPAN));
        System.out.println("Parsed Japanese date: " + japaneseDate);
```

Wyjście:

```
Parsed Japanese date: 2021-04-01T00:00:00
```

**Dlaczego to dodajemy?**  
Jeśli Twój eksport CSV zasila systemy downstream oczekujące dat w formacie ISO‑8601, najpierw musisz znormalizować wszelkie formaty lokalne. Ten fragment kodu pokazuje *jak* i *dlaczego* w jednym miejscu.

---

## Krok 4: Przelicz formuły – Utrzymaj wyniki dynamicznych tablic aktualne

Jeśli Twój skoroszyt zawiera formuły (np. `=SUM(A1:A10)`), nie zostaną one automatycznie zaktualizowane po zmianie ustawień. Wywołanie `calculateFormula` wymusza pełne przeliczenie, zapewniając, że wyeksportowany CSV odzwierciedla najnowsze wartości.

```java
        // Step 4 – recalculate all formulas
        workbook.calculateFormula();
```

> **Watch out:** Duże skoroszyty mogą wymagać zauważalnego czasu na przeliczenie. W scenariuszach krytycznych pod względem wydajności rozważ użycie `calculateFormula(FormulaCalculationOptions)`, aby ograniczyć zakres.

---

## Krok 5: Wygeneruj pierwszą tabelę przestawną jako obraz PNG

Czasami potrzebny jest wizualny zrzut tabeli przestawnej obok CSV. Poniższy kod renderuje pierwszą tabelę przestawną na pierwszym arkuszu do pliku PNG.

```java
        // Step 5 – render pivot table as PNG
        PivotTable pivot = sheet.getPivotTables().get(0); // assumes a pivot exists
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.Png);
        // The range that the pivot occupies is turned into an image
        pivot.getRange().toImage("output/pivot.png", imgOptions);
```

**Tip:** Jeśli skoroszyt nie zawiera jeszcze tabeli przestawnej, możesz ją utworzyć programowo — zobacz dokumentację Aspose.Cells po szybki przykład.

---

## Krok 6: Użyj Smart Marker, aby dodać komentarz i zapisać skoroszyt

Smart Marker pozwala wstawiać dynamiczną treść do komórek przy użyciu prostych placeholderów. Tutaj zapisujemy komentarz typu „Reviewed by QA” w wyznaczonej komórce, a następnie zapisujemy skoroszyt.

```java
        // Step 6 – apply Smart Marker comment
        SmartMarkerProcessor smartMarker = new SmartMarkerProcessor(workbook);
        smartMarker.apply("${Comment}", java.util.Collections.singletonMap("Comment", "Reviewed by QA"));

        // Finally, save the workbook with the comment embedded
        workbook.save("output/commented.xlsx");
    }
}
```

Placeholder `${Comment}` może znajdować się w dowolnym miejscu arkusza (np. komórka `A1`). Gdy uruchomisz `apply`, placeholder zostanie zastąpiony podaną wartością.

**Result:** Znajdziesz plik `output/commented.xlsx` zawierający komentarz, a także wcześniej wygenerowany `pivot.png` oraz ciąg CSV wydrukowany w konsoli.

---

## Pełny działający przykład

Łącząc wszystkie elementy, oto kompletny program, który możesz skompilować i uruchomić:

```java
import com.aspose.cells.*;
import java.util.Collections;
import java.util.Locale;

public class CsvExportDemo {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Workbook & Significant Digits -----------
        Workbook workbook = new Workbook();
        WorkbookSettings settings = workbook.getSettings();
        settings.setNumberSignificantDigits(5); // **set significant digits**

        // ----------- Step 2: Populate Sample Data & Export CSV ----------
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
        cells.get("B2").putValue(123.456);
        cells.get("C2").putValue(78.9);
        cells.get("D2").putValue(0.12345);
        // (Add more rows if you like)

        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setNumberFormat("0.00");
        Range dataRange = cells.createRange("B2:D10");
        String csvData = dataRange.exportDataTable(exportOptions).toString();

        System.out.println("=== CSV Output ===");
        System.out.println(csvData);

        // ----------- Step 3: Japanese Era Date ----------
        DateTime japaneseDate = DateTime.parse("R3/04/01", new DateTimeFormatInfo(Locale.JAPAN));
        System.out.println("Parsed Japanese date: " + japaneseDate);

        // ----------- Step 4: Recalculate Formulas ----------
        workbook.calculateFormula();

        // ----------- Step 5: Render Pivot Table ----------
        if (!sheet.getPivotTables().isEmpty()) {
            PivotTable pivot = sheet.getPivotTables().get(0);
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.Png);
            pivot.getRange().toImage("output/pivot.png", imgOptions);
        }

        // ----------- Step 6: Smart Marker Comment ----------
        SmartMarkerProcessor smartMarker = new SmartMarkerProcessor(workbook);
        smartMarker.apply("${Comment}", Collections.singletonMap("Comment", "Reviewed by QA"));
        workbook.save("output/commented.xlsx");
    }
}
```

### Oczekiwany wynik w konsoli

```
=== CSV Output ===
123.46,78.90,0.12
...
Parsed Japanese date: 2021-04-01T00:00:00
```

Znajdziesz również `output/pivot.png` (jeśli tabela przestawna istniała) oraz `output/commented.xlsx` na dysku.

---

## Najczęściej zadawane pytania i przypadki brzegowe

- **Czy mogę eksportować bezpośrednio do fizycznego pliku CSV?**  
  Tak. Zastąp blok `exportAsString` wywołaniem `dataRange.exportDataTable("output/data.csv", exportOptions);`.

- **Co zrobić, jeśli mój arkusz używa innej lokalizacji dla liczb?**  
  Ustaw `exportOptions.setCultureInfo(new CultureInfo("fr-FR"))` przed eksportem; spowoduje to zamianę

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}