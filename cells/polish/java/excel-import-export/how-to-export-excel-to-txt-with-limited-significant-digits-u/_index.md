---
category: general
date: 2026-08-17
description: Eksportuj Excel do TXT, ograniczając liczbę znaczących cyfr – dowiedz
  się, jak ustawić liczbę cyfr i konwertować Excel na tekst w Javie, korzystając z
  pełnego przykładu Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: pl
lastmod: 2026-08-17
og_description: Eksportuj Excel do TXT, ograniczając liczbę cyfr znaczących. Ten samouczek
  pokazuje, jak ustawić liczbę cyfr i przekonwertować Excel na tekst przy użyciu Aspose.Cells
  dla Javy.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: Eksport Excel do TXT z ograniczoną liczbą cyfr znaczących – przewodnik Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: Jak wyeksportować Excel do TXT z ograniczoną liczbą cyfr znaczących przy użyciu
  Javy
url: /pl/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksportuj Excel do TXT z ograniczoną liczbą cyfr znaczących przy użyciu Javy

Jeśli potrzebujesz **eksportować Excel do TXT**, jednocześnie kontrolując liczbę cyfr znaczących, ten przewodnik dostarcza gotowe rozwiązanie. Zobaczysz, jak ustawić liczbę cyfr, przekonwertować Excel na tekst i utrzymać wynik w porządku dzięki jednej zmianie konfiguracji.

Przykład wykorzystuje Aspose.Cells for Java 25.10, które wprowadza opcję `setSignificantDigits`. Po zakończeniu tutorialu będziesz w stanie wygenerować plik TXT zawierający wyłącznie pożądane cyfry, bez dodatkowego kodu zaokrąglającego.

## Co osiągniesz

- Utworzysz skoroszyt programowo.
- Wstawisz wartość liczbową do komórki.
- Skonfigurujesz opcje zapisu TXT, aby ograniczyć liczbę cyfr znaczących.
- Zapiszesz skoroszyt jako plik tekstowy.
- Zrozumiesz, jak działa ustawienie `significantDigits` i jak je dostosować do innych scenariuszy.

### Wymagania wstępne

- Java 17 lub nowsza (kod kompiluje się również w Java 8).
- Aspose.Cells for Java 25.10 lub nowsza. Pobierz plik JAR ze [strony Aspose](https://products.aspose.com/cells/java) i dodaj go do ścieżki klas projektu.
- IDE lub prosty edytor tekstu oraz narzędzie do budowania wierszem poleceń (Maven/Gradle).

## Krok 1: Konfiguracja projektu i import Aspose.Cells

Utwórz nowy projekt Java i dodaj plik JAR Aspose.Cells do ścieżki kompilacji. Jeśli używasz Maven, dodaj następującą zależność do `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Wskazówka:** Użyj klasyfikatora `jdk17` dla najnowszego środowiska uruchomieniowego Java; zmniejsza to ryzyko ostrzeżeń o niekompatybilności.

## Krok 2: Utwórz skoroszyt i zapisz wartość

Skoroszyt reprezentuje plik Excel w pamięci. Możesz dodać dane do dowolnej komórki, używając metody `putValue`.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

Liczba `123.456789` będzie źródłem naszego eksportu TXT. Domyślnie Aspose.Cells zapisałoby wszystkie miejsca po przecinku, co często prowadzi do „szumu” w plikach tekstowych.

## Krok 3: Skonfiguruj opcje zapisu TXT, aby ograniczyć cyfry znaczące

Aspose.Cells udostępnia `TxtSaveOptions` umożliwiające precyzyjną kontrolę nad wyjściem tekstowym. Metoda `setSignificantDigits` informuje eksporter, ile cyfr zachować **ogólnie**, a nie tylko po przecinku.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

Gdy `significantDigits` jest ustawione na `4`, eksporter zaokrągla wartość `123.456789` do `123.5`. Zachowanie to odpowiada matematycznej definicji cyfr znaczących: pierwsze cztery niezerowe cyfry są zachowane.

### Jak to się różni od „ograniczenia miejsc po przecinku”

- **limit decimals** (`setDecimalPlaces`) usuwa cyfry *po* przecinku, niezależnie od części całkowitej.
- **significant digits** (`setSignificantDigits`) liczy cyfry od pierwszej niezerowej, co jest przydatne, gdy liczby mają różną skalę.

Jeśli potrzebujesz stałej liczby miejsc po przecinku, zamień powyższą linię na:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Krok 4: Zapisz skoroszyt jako plik TXT

Teraz zapisz skoroszyt na dysku, używając skonfigurowanych opcji.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Uruchomienie programu tworzy plik `significant_digits.txt` w katalogu roboczym. Plik zawiera jedną linię:

```
123.5
```

### Oczekiwany wynik

| Komórka | Wartość oryginalna | Wyeksportowane (4 cyfry znaczące) |
|---------|--------------------|-----------------------------------|
| A1      | 123.456789         | 123.5                             |

Jeśli zmienisz `setSignificantDigits(4)` na `6`, wynik będzie `123.457`. Eksperymentuj z różnymi wartościami, aby zobaczyć, jak zachodzi zaokrąglanie.

## Krok 5: Typowe warianty i przypadki brzegowe

### Eksport całego zakresu

Jeśli chcesz wyeksportować więcej niż jedną komórkę, po prostu wypełnij zakres przed zapisem:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

To samo ustawienie `significantDigits` ma zastosowanie do każdej komórki liczbowej, zapewniając spójną precyzję w całym pliku.

### Obsługa separatorów dziesiętnych zależnych od lokalizacji

Aspose.Cells respektuje ustawienia regionalne systemu przy zapisie tekstu. Aby wymusić kropkę (`.`) jako separator dziesiętny, ustaw kulturę w `TxtSaveOptions`:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

Jest to przydatne, gdy docelowa aplikacja oczekuje konkretnego formatu, np. parserów CSV akceptujących wyłącznie `.`.

### Nadpisywanie istniejących plików

Metoda `save` domyślnie nadpisuje docelowy plik. Jeśli chcesz uniknąć przypadkowej utraty danych, najpierw sprawdź, czy plik istnieje:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Duże skoroszyty i zużycie pamięci

Podczas eksportu bardzo dużych arkuszy rozważ strumieniowy zapis wyniku:

```java
saveOptions.setEnableMemorySaving(true);
```

Ta opcja zmniejsza zużycie pamięci heap, zapisując wiersze stopniowo.

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować, wkleić i od razu uruchomić:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Uruchomienie tego kodu tworzy plik `significant_digits.txt` z następującą zawartością (kolumny oddzielone tabulatorem):

```
123.5	0.001235	98770
```

Każda liczba respektuje regułę **4 cyfr znaczących**, co dowodzi, że ustawienie działa przy różnych skalach liczb.

## Podsumowanie

Teraz wiesz, jak **eksportować Excel do TXT**, kontrolując liczbę cyfr znaczących. Korzystając z `TxtSaveOptions.setSignificantDigits`, możesz **ustawić liczbę cyfr**, **ograniczyć miejsca po przecinku** oraz **ograniczyć cyfry znaczące** w jednej, łatwej do utrzymania linii kodu. Podejście działa zarówno dla pojedynczych komórek, pełnych zakresów, jak i dużych skoroszytów.

### Kolejne kroki

- Zbadaj inne właściwości `TxtSaveOptions`, takie jak `setDelimiter('\t')`, aby dostosować separator kolumn.
- Połącz eksportera z `CsvSaveOptions`, jeśli potrzebujesz wartości rozdzielonych przecinkami zamiast zwykłego tekstu.
- Zintegruj tę procedurę z usługą sieciową, która przyjmuje przesłane pliki Excel i zwraca przycięty wynik TXT w locie.

Śmiało eksperymentuj z różnymi limitami cyfr i ustawieniami regionalnymi. Jeśli napotkasz scenariusz, w którym wbudowane opcje nie spełniają specjalnych wymagań, zawsze możesz poddać wygenerowany plik TXT dalszej obróbce przy użyciu standardowych narzędzi I/O Javy.

Miłego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz szczegółowe wyjaśnienia, pomagające opanować dodatkowe funkcje API i poznać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak konwertować tekst na liczby w Excelu przy użyciu Aspose.Cells for Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [Jak tworzyć i eksportować Excel do HTML przy użyciu Aspose.Cells Java | Przewodnik po operacjach na skoroszycie](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Jak eksportować niestandardowe właściwości Excela do PDF przy użyciu Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}