---
category: general
date: 2026-07-03
description: Dołącz eksport formuł w Javie, aby konwertować komórki Excela na tekst
  przy użyciu Aspose.Cells. Dowiedz się, jak wydrukować zakres Excela i efektywnie
  uzyskać ciąg wartości komórek.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: pl
og_description: Uwzględnij eksport formuł w Javie, aby konwertować komórki Excela
  na tekst. Przewodnik krok po kroku pokazujący, jak wydrukować zakres Excela i pobrać
  wartości komórek jako ciąg znaków.
og_title: Uwzględnij eksport formuł w Javie – konwertuj komórki Excela na tekst
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Uwzględnij eksport formuł w Javie – konwertuj komórki Excela na tekst
url: /pl/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksportowanie Formuł w Javie – Konwersja Komórek Excel na Tekst

Czy kiedykolwiek potrzebowałeś **include formulas export** przy pobieraniu danych z skoroszytu Excel? Być może tworzysz usługę raportowania, która musi zachować oryginalne formuły, jednocześnie dostarczając schludny tekstowy blok danych. W takim wypadku jesteś we właściwym miejscu. Ten przewodnik krok po kroku pokazuje, jak konwertować komórki Excel na zwykły tekst — *włączając* wszelkie osadzone formuły — przy użyciu Aspose.Cells for Java.

Poruszymy także, jak **print Excel range**, dostosować **export table options**, a na końcu **get cell values string**, które możesz logować, wysyłać przez API lub przechowywać w bazie danych. Po zakończeniu będziesz mieć w pełni działający fragment kodu i solidne zrozumienie przyczyn każdego wywołania.

## Co Zdobędziesz

- Pełny, gotowy do skopiowania program w Javie, który odczytuje plik `.xlsx`, wybiera zakres i eksportuje go jako sformatowany ciąg znaków.
- Zrozumienie klasy `ExportTableOptions` oraz dlaczego przełączanie `setExportAsString` i `setIncludeFormula` ma znaczenie.
- Wskazówki dotyczące obsługi dużych arkuszy, radzenia sobie z różnymi typami danych i dostosowywania formatu wyjściowego.
- Szybka lista kontrolna typowych pułapek (np. scalone komórki, ukryte wiersze i formaty liczb zależne od lokalizacji).

### Wymagania wstępne

- Java 17 lub nowsza (kod kompiluje się również w starszych wersjach, ale użyjemy najnowszego LTS).
- Aspose.Cells for Java 23.10 (lub dowolna nowsza wersja) — możesz pobrać go z Maven Central.
- Przykładowy plik `input.xlsx` umieszczony w folderze, którym zarządzasz (ścieżka jest na stałe wpisana w przykładzie dla przejrzystości).

Jeśli już je masz, zanurzmy się.

## Krok 1: Konfiguracja Projektu i Dodanie Zależności

Najpierw utwórz projekt Maven (lub Gradle, jeśli wolisz). Dodaj zależność Aspose.Cells do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro tip:** Jeśli używasz firmowego proxy, upewnij się, że repozytorium jest dostępne; w przeciwnym razie kompilacja zakończy się błędem „Could not resolve dependencies”.

Gdy Maven zakończy pobieranie, możesz przystąpić do pisania kodu w Javie.

## Krok 2: Załaduj Skoroszyt i Pobierz Żądany Arkusz

Pierwsza linia przykładu kodu pokazuje, jak otworzyć istniejący skoroszyt:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Zastąp `YOUR_DIRECTORY` absolutną lub względną ścieżką do swojego pliku. Konstruktor `Workbook` automatycznie wykrywa format pliku (XLS, XLSX, CSV itp.), więc nie musisz go podawać.

Następnie pobieramy pierwszy arkusz:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Dlaczego pierwszy arkusz? W wielu szablonach dane znajdują się na pierwszej karcie, ale możesz podać dowolny indeks lub nawet użyć `get("SheetName")`, jeśli wolisz podejście nazwane.

## Krok 3: Zdefiniuj Zakres, Który Chcesz Eksportować

Teraz następuje sedno operacji **convert excel cells text**. Informujesz Aspose.Cells, które komórki pobrać, tworząc obiekt `Range`:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

Ciąg znaków `"A1:C3"` to klasyczny adres w stylu A1. Można go również zbudować programowo:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Ta elastyczność pomaga, gdy rozmiar zakresu jest dynamiczny — na przykład, odczytujesz ostatni używany wiersz za pomocą `ws.getCells().getMaxDataRow()`.

## Krok 4: Skonfiguruj Export Table Options, aby Uwzględnić Formuły

Tutaj znajduje się magia **include formulas export**. Domyślnie Aspose.Cells zwraca *wyświetlane* wartości. Jeśli komórka zawiera `=SUM(A1:A3)`, otrzymasz obliczoną liczbę, a nie tekst formuły. Aby to zmienić, skonfiguruj `ExportTableOptions`:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

Dlaczego oba flagi? `setExportAsString(true)` instruuje API, aby łączyło komórki przy użyciu domyślnego separatora (tabulator dla kolumn, nowa linia dla wierszy). `setIncludeFormula(true)` zmienia źródło wartości z „wyświetlanej wartości” na „surową formułę”. Jeśli potrzebujesz tylko wartości, pozostaw `false`.

### Opcjonalne Dostosowania

- `eto.setExportHiddenRows(true);` – uwzględnia wiersze ukryte w Excelu.
- `eto.setExportHiddenColumns(true);` – to samo dla kolumn.
- `eto.setExportAsHTML(true);` – zwraca HTML zamiast zwykłego tekstu.

Śmiało eksperymentuj; klasa opcji to plac zabaw **export table options**.

## Krok 5: Pobierz Zakres jako Sformatowany Ciąg

Teraz pobieramy dane:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

Zwrócony `txt` wygląda mniej więcej tak (zakładając, że A1:C3 zawiera mieszankę wartości i formuł):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Zauważ tabulator (`\t`) oddzielający kolumny oraz nową linię (`\n`) oddzielającą wiersze. Możesz później podzielić ciąg, jeśli potrzebujesz tablicy 2‑D:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Krok 6: Wydrukuj Wynik – „Print Excel Range” w Prostej Formie

Na koniec wypisujemy ciąg na konsolę:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

Uruchomienie programu wyświetla dokładnie taki wynik, jak powyżej. Stąd możesz zapisać ciąg do pliku logu, wysłać go przez HTTP lub przechować w dokumencie NoSQL.

## Pełny, Gotowy do Uruchomienia Przykład

Łącząc wszystko razem, oto kompletny program. Skopiuj, wklej i naciśnij **Run** — bez brakujących importów.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Oczekiwany Wynik (przykład)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Jeśli Twój skoroszyt zawiera liczby sformatowane jako daty, pojawią się w formacie specyficznym dla lokalizacji (np. `2026‑07‑03`). Aby wymusić format ISO, możesz dostosować `ExportTableOptions` przy użyciu własnego `NumberFormat`.

## Obsługa Przypadków Brzegowych i Częste Pytania

### Co jeśli zakres zawiera scalone komórki?

Scalone komórki są traktowane jako wartość lewego‑górnego elementu. Reszta scalanego obszaru pojawi się jako puste ciągi. Jeśli potrzebujesz adresu scalanego regionu, wywołaj `Cell.getMergedRange()` przed eksportem.

### Czy mogę wyeksportować ogromny arkusz (setki tysięcy wierszy)?

Tak, ale uważaj na zużycie pamięci. Użyj `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, aby Aspose.Cells przesyłało dane na dysk. Rozważ także eksport w partiach (np. po 10 000 wierszy), aby ciąg był łatwiejszy do obsługi.

### Jak zmienić separator kolumn?

`ExportTableOptions` udostępnia metodę `setSeparator(char separator)`. Aby uzyskać wyjście w stylu CSV, ustaw ją na `','`:

```java
eto.setSeparator(',');
```

### Czy formuły respektują odwołania zewnętrzne?

Jeśli formuła odwołuje się do innego skoroszytu, Aspose.Cells zachowa tekst odwołania (`='[Other.xlsx]Sheet1'!A1`). Nie wyliczy wartości zewnętrznej, chyba że załadujesz również ten skoroszyt.

## Pro Tipy dla Kodu Gotowego do Produkcji

- **Cache the workbook** jeśli odczytujesz the

## Co Powinieneś Nauczyć Się Następnie?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}