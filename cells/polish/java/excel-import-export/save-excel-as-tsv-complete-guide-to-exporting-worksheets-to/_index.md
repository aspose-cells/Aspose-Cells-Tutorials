---
category: general
date: 2026-06-27
description: Szybko zapisz plik Excel jako TSV przy użyciu Javy. Dowiedz się, jak
  wyeksportować arkusz do tekstu, wyeksportować arkusz jako zwykły tekst oraz wyeksportować
  ciąg danych Excel przy użyciu Aspose.Cells.
draft: false
keywords:
- save excel as tsv
- export worksheet to text
- export sheet plain text
- export excel data string
language: pl
og_description: Zapisz Excel jako TSV przy użyciu Javy. Ten poradnik pokazuje, jak
  wyeksportować arkusz do tekstu, wyeksportować arkusz jako zwykły tekst oraz efektywnie
  wyeksportować dane z Excela jako ciąg znaków.
og_title: Zapisz Excel jako TSV – Przewodnik krok po kroku eksportu
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  headline: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  type: TechArticle
- description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  name: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  steps:
  - name: Pro tip
    text: If you’re dealing with password‑protected files, call `new Workbook("file.xlsx",
      new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.
  - name: 'Edge case: Custom delimiters'
    text: 'If your downstream system expects a pipe (`|`) instead of a tab, just change
      the delimiter:'
  - name: Pro tip
    text: 'After exporting, you can also capture the string directly:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Zapisz Excel jako TSV – Kompletny przewodnik po eksportowaniu arkuszy do tekstu
url: /pl/java/excel-import-export/save-excel-as-tsv-complete-guide-to-exporting-worksheets-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zapisz Excel jako TSV – Kompletny przewodnik po eksportowaniu arkuszy do tekstu

Kiedykolwiek potrzebowałeś **zapisz Excel jako TSV**, ale nie wiedziałeś, którego wywołania API użyć? Nie jesteś sam. Wielu programistów napotyka trudności, gdy próbują przekształcić arkusz kalkulacyjny w plik z wartościami oddzielonymi tabulacjami do dalszego przetwarzania. Dobra wiadomość? Kilka linii Java i Aspose.Cells pozwala wyeksportować arkusz do tekstu, wyeksportować czysty tekst arkusza oraz nawet wyeksportować ciąg danych Excel bez wysiłku.

W tym samouczku przeprowadzimy Cię przez cały proces — od załadowania skoroszytu, przez konfigurację opcji eksportu, aż po zapisanie pliku TSV na dysku. Po zakończeniu będziesz w stanie **zapisz Excel jako TSV** w dowolnym projekcie Java, niezależnie od tego, czy obsługujesz pojedynczy arkusz, czy przetwarzasz dziesiątki plików.

## Co obejmuje ten przewodnik

* Ładowanie skoroszytu Excel z dysku  
* Wybór odpowiedniego arkusza (lub iteracja po wielu)  
* Konfigurowanie `ExportTableOptions`, aby uzyskać wyjście w formie czystego tekstu  
* Zapisywanie danych jako plik z wartościami oddzielonymi tabulacjami (TSV)  
* Wskazówki dotyczące obsługi dużych zakresów, różnych separatorów i znaków Unicode  

Nie są wymagane żadne zewnętrzne narzędzia — wystarczy Aspose.Cells dla Java oraz środowisko uruchomieniowe Java 8+.

---

## Krok 1: Skonfiguruj projekt i załaduj skoroszyt

Zanim przejdziemy do kodu, upewnij się, że dodałeś plik JAR Aspose.Cells do classpath swojego projektu. Jeśli używasz Maven, zależność wygląda tak:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Teraz możemy załadować skoroszyt:

```java
// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – print the number of worksheets
System.out.println("Worksheets count: " + workbook.getWorksheets().getCount());
```

> **Dlaczego to ważne:** Ładowanie pliku jest pierwszym krokiem w każdym **export Excel data string** workflow. Jeśli pliku nie da się otworzyć, nic innego nie zadziała.

### Porada
Jeśli masz do czynienia z plikami zabezpieczonymi hasłem, wywołaj `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.

---

## Krok 2: Wybierz arkusz, który chcesz wyeksportować

Możesz pobrać pierwszy arkusz, arkusz po nazwie lub iterować po wszystkich. Oto najprostszy przypadek — eksport pierwszego arkusza:

```java
// Step 2: Access the first worksheet (or any specific sheet)
Worksheet ws = workbook.getWorksheets().get(0);
System.out.println("Exporting sheet: " + ws.getName());
```

Jeśli potrzebujesz **export worksheet to text** dla każdego arkusza, otocz powyższy kod pętlą `for`:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    // Export each sheet separately...
}
```

---

## Krok 3: Utwórz i skonfiguruj opcje eksportu

Serce **export sheet plain text** leży w `ExportTableOptions`. Przełączając kilka właściwości, zamieniamy zakres w ciąg czystego tekstu z separatorem tabulacji:

```java
// Step 3: Create export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();

// Step 4: Configure the options – export as plain text and use a tab delimiter
exportOptions.setExportAsString(true);   // Returns a string instead of binary Excel format
exportOptions.setDelimiter('\t');        // Tab character makes it TSV
```

> **Dlaczego używać `setExportAsString(true)`?**  
> Powoduje to, że Aspose.Cells traktuje wynik jako surowy tekst, co jest dokładnie tym, czego potrzebujesz, gdy chcesz **zapisz Excel jako TSV**. Alternatywą byłby eksport CSV lub HTML, które nie zapewniają czystego rozdzielenia tabulacjami.

### Przypadek brzegowy: Niestandardowe separatory
Jeśli Twój system docelowy oczekuje pionowej kreski (`|`) zamiast tabulacji, po prostu zmień separator:

```java
exportOptions.setDelimiter('|');
```

---

## Krok 4: Wyeksportuj wybrany zakres do pliku tekstowego

Teraz faktycznie zapisujemy plik TSV. Metoda `exportTable` przyjmuje trzy argumenty: zakres komórek, ścieżkę wyjściową oraz skonfigurowane `ExportTableOptions`.

```java
// Step 5: Export the range A1:D20 to a text file using the configured options
ws.getCells().exportTable("A1:D20", "YOUR_DIRECTORY/out.tsv", exportOptions);
System.out.println("TSV file created successfully!");
```

Jeśli chcesz wyeksportować *cały* używany zakres, zamień `"A1:D20"` na `ws.getCells().getMaxDisplayRange()`:

```java
String fullRange = ws.getCells().getMaxDisplayRange();
ws.getCells().exportTable(fullRange, "out.tsv", exportOptions);
```

### Porada
Po eksporcie możesz także bezpośrednio pobrać ciąg znaków:

```java
String tsvContent = ws.getCells().exportTable("A1:D20", exportOptions);
System.out.println(tsvContent); // Handy for debugging or sending over a network
```

Daje to surowy **export Excel data string** bez ingerencji w system plików.

---

## Krok 5: Obsługa dużych plików i wskazówki dotyczące wydajności

Podczas pracy z ogromnymi arkuszami (setki tysięcy wierszy) rozważ następujące optymalizacje:

| Problem | Rozwiązanie |
|---------|-------------|
| Presja pamięci | Użyj `WorkbookFactory.create(InputStream)`, aby strumieniowo odczytywać plik zamiast ładować go w całości. |
| Wolny I/O | Zapisuj przy użyciu `BufferedWriter` lub NIO `Files.newBufferedWriter`. |
| Znaki Unicode | Upewnij się, że plik wyjściowy jest zapisywany w UTF‑8: `exportTable(..., "out.tsv", exportOptions, Encoding.getUTF8())`. |

Poniżej fragment kodu łączący strumieniowanie i kodowanie UTF‑8:

```java
try (InputStream is = Files.newInputStream(Paths.get("input.xlsx"));
     BufferedWriter writer = Files.newBufferedWriter(Paths.get("out.tsv"), StandardCharsets.UTF_8)) {

    Workbook wb = new Workbook(is);
    Worksheet sheet = wb.getWorksheets().get(0);
    ExportTableOptions opts = new ExportTableOptions();
    opts.setExportAsString(true);
    opts.setDelimiter('\t');

    String tsv = sheet.getCells().exportTable("A1:D20", opts);
    writer.write(tsv);
}
```

---

## Typowe pułapki i jak ich unikać

1. **Zapomniano ustawić `setExportAsString(true)`.**  
   Bez tego flagi Aspose wygeneruje binarny plik Excel, co uniemożliwi osiągnięcie celu **export worksheet to text**.

2. **Użycie niewłaściwego separatora.**  
   Przecinek zamiast tabulacji da Ci CSV, nie TSV. Sprawdź dwukrotnie `setDelimiter('\t')`.

3. **Niepoprawna składnia zakresu.**  
   `"A1:D20"` jest w porządku, ale `"A1:D20:"` (dodatkowy dwukropek) spowoduje `IllegalArgumentException`.

4. **Uprawnienia do pliku.**  
   Upewnij się, że docelowy katalog jest zapisywalny. W Linuksie często pomaga `chmod 755`.

---

## Podsumowanie – kompletny działający przykład

Oto pełny, gotowy do uruchomienia program demonstrujący **zapisz Excel jako TSV** od początku do końca:

```java
import com.aspose.cells.*;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;

public class ExcelToTsv {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Choose worksheet (first sheet in this case)
        Worksheet ws = workbook.getWorksheets().get(0);

        // Set up export options for plain‑text TSV output
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);   // Export as string
        exportOptions.setDelimiter('\t');        // Tab delimiter for TSV

        // Define the range you want to export
        String range = "A1:D20"; // Change as needed or use ws.getCells().getMaxDisplayRange()

        // Export to a file
        ws.getCells().exportTable(range, "YOUR_DIRECTORY/out.tsv", exportOptions);
        System.out.println("Successfully saved Excel as TSV at YOUR_DIRECTORY/out.tsv");
    }
}
```

Uruchomienie tego programu tworzy plik z wartościami oddzielonymi tabulacjami (`out.tsv`), który może być odczytany przez dowolny system downstream — czy to loader bazy danych, skrypt Unix `awk`, czy prosty podgląd arkusza.

---

## Zakończenie

Omówiliśmy wszystko, co potrzebne, aby **zapisz Excel jako TSV** przy użyciu Java i Aspose.Cells. Od załadowania skoroszytu, przez wybór właściwego arkusza, konfigurację `ExportTableOptions`, aż po zapis pliku — masz teraz solidny, gotowy do produkcji wzorzec dla scenariuszy **export worksheet to text**, **export sheet plain text** i **export Excel data string**.

Co dalej? Spróbuj wyeksportować wiele zakresów, dynamicznie zmieniać separatory lub strumieniowo przesyłać wynik bezpośrednio w odpowiedzi HTTP dla pobrań webowych. Te same zasady obowiązują, a obsługa danych Excel w formie czystego tekstu stanie się bułką z masłem, gdy opanujesz podstawy.

Masz pytania lub napotkałeś nietypowy przypadek? zostaw komentarz poniżej i powodzenia w kodowaniu!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz krok po kroku wyjaśnienia, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Jak wyeksportować dane Excel do HTML5 przy użyciu Aspose.Cells Java](/cells/english/java/import-export/aspose-cells-java-export-excel-html5/)
- [Bezproblemowy eksport danych z Excel przy użyciu Aspose.Cells dla Java](/cells/english/java/import-export/aspose-cells-java-excel-data-export/)
- [Jak wyeksportować arkusz Excel do PNG przy użyciu Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}