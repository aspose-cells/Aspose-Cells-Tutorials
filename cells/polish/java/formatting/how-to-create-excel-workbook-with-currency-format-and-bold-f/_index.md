---
category: general
date: 2026-08-20
description: Utwórz skoroszyt Excel w Javie przy użyciu Aspose.Cells, ustaw format
  waluty, dodaj pogrubioną czcionkę i zaimportuj tablicę stylów dla stylizowanych
  komórek.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: pl
lastmod: 2026-08-20
og_description: Utwórz skoroszyt Excel w Javie, ustaw format waluty, dodaj pogrubioną
  czcionkę i dowiedz się, jak zaimportować styl przy użyciu Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Utwórz skoroszyt Excel ze stylizowanymi komórkami walutowymi w Javie
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Jak utworzyć skoroszyt Excel z formatem walutowym i pogrubioną czcionką w Javie
url: /pl/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć skoroszyt Excel z formatem waluty i pogrubioną czcionką w Javie

Jeśli potrzebujesz **create excel workbook** programowo, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Przejdziemy przez tworzenie skoroszytu, zastosowanie formatu waluty, dodanie pogrubionej czcionki oraz użycie funkcji **how to import style** w Aspose.Cells, aby każda zaimportowana komórka wyglądała spójnie.

Na końcu otrzymasz gotowy do użycia plik `DataTableWithStyleArray.xlsx`, który wyświetla liczby jako dolary i podkreśla je pogrubioną czcionką. Nie jest wymagana ręczna formatowanie w Excelu.

## Wymagania wstępne

- Zainstalowany Java 17 lub nowszy.
- Licencja Aspose.Cells for Java (lub darmowy klucz ewaluacyjny).
- Maven lub Gradle do zarządzania zależnością `aspose-cells`.
- Podstawowa znajomość kolekcji Java i `DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Wskazówka:** Jeśli napotkasz `LicenseException`, umieść plik licencji w classpath i wywołaj `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` przed utworzeniem skoroszytu.

## Jak utworzyć skoroszyt Excel ze stylizowanymi komórkami walutowymi

Ta sekcja zawiera kluczowe kroki. Każdy krok wyjaśnia **dlaczego** jest istotny, a nie tylko **co** wpisać.

### Krok 1: Inicjalizacja skoroszytu i arkusza

Utworzenie nowego skoroszytu zapewnia czysty kontener dla wszystkich kolejnych formatowań.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Dlaczego:** Obiekt `Workbook` reprezentuje cały plik Excel. Dostęp do pierwszego `Worksheet` pozwala od razu rozpocząć wypełnianie danymi.

### Krok 2: Zbuduj DataTable z danymi liczbowymi

`DataTable` naśladuje tabelę bazy danych, co ułatwia masowy import wierszy.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Dlaczego:** Użycie `DOUBLE` zapewnia zachowanie precyzji dziesiętnej wartości, co jest niezbędne, gdy później **format cells currency**.

### Krok 3: Zdefiniuj styl – format waluty i pogrubioną czcionkę

Tutaj **ustawiamy format waluty** i **dodajemy pogrubioną czcionkę** do obiektu `Style`.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Dlaczego:** Ciąg formatu `Number` `$#,##0.00` informuje Excel, aby traktował komórkę jako wartość pieniężną, natomiast `setBold(true)` przyciąga uwagę do liczb. Umieszczenie stylu w tablicy przygotowuje nas do kroku **how to import style**.

### Krok 4: Skonfiguruj opcje importu, aby używać tablicy stylów

Aspose.Cells umożliwia przekazanie `Style[]` poprzez `ImportTableOptions`. To jest oficjalna metoda **how to import style**.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Dlaczego:** Bez `ImportTableOptions` zaimportowane komórki odziedziczyłyby domyślny styl, tracąc zdefiniowane formatowanie waluty i pogrubienie.

### Krok 5: Importuj DataTable do arkusza

Teraz przenosimy dane do arkusza w komórce `A1`, automatycznie stosując tablicę stylów.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` wskazuje, że pierwszy wiersz `DataTable` zawiera nagłówki kolumn.
- `"A1"` jest lewym górnym rogiem, od którego rozpoczyna się import.

> **Dlaczego:** Importowanie z tablicą stylów zapewnia, że każda zaimportowana komórka otrzyma styl **format cells currency**, który przygotowaliśmy wcześniej.

### Krok 6: Zapisz skoroszyt na dysku

Na koniec zapisz skoroszyt znajdujący się w pamięci do fizycznego pliku.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Dlaczego:** Zapis utrwala formatowanie, umożliwiając Tobie lub procesom downstream otwarcie pliku w Excelu z pożądanym wyglądem.

## Pełny kod źródłowy

Poniżej znajduje się kompletny, gotowy do uruchomienia kod klasy Java. Skopiuj go do swojego IDE, zamień `YOUR_DIRECTORY` na istniejący folder i uruchom.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Oczekiwany wynik

Po otwarciu `DataTableWithStyleArray.xlsx` w Microsoft Excel powinieneś zobaczyć:

| Kwota |
|-------|
| **$1,234.56** |
| **$7,890.12** |

- Liczby są wyświetlane w **formatcie waluty** (znak `$`, dwie miejsca po przecinku).
- Czcionka obu komórek jest **pogrubiona**, co wyróżnia je.

## Typowe warianty i przypadki brzegowe

| Scenariusz | Co zmienić | Powód |
|------------|------------|-------|
| **Inna waluta** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Użyj symbolu euro lub dowolnego formatu specyficznego dla lokalizacji. |
| **Wiele kolumn z różnymi stylami** | Create multiple `Style` objects, populate `styleArray` in the same order as columns. | Każda kolumna może mieć własny format liczbowy, czcionkę, tło itp. |
| **Duże zestawy danych** | Use `cells.importDataTable(dataTable, false, "A1", importOptions);` and set `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | Poprawia wydajność poprzez pomijanie wierszy nagłówków lub niepotrzebnych metadanych. |
| **Stosowanie stylu po imporcie** | Call `cells.get("A2").setStyle(currencyStyle);` for individual cells. | Przydatne, gdy tylko podzbiór wierszy wymaga specjalnego formatowania. |

## Wskazówki do użycia w produkcji

- **Zarejestruj licencję wcześnie**: Zarejestruj licencję Aspose.Cells przed utworzeniem skoroszytu, aby uniknąć znaku wodnego wersji ewaluacyjnej.
- **Bezpieczeństwo wątków**: Instancje `Workbook` **nie** są bezpieczne wątkowo. Utwórz osobną instancję na każdy wątek, jeśli generujesz wiele plików jednocześnie.
- **Zarządzanie pamięcią**: Dla bardzo dużych arkuszy rozważ użycie strumieniowego API `Workbook` (`Workbook` → `WorkbookDesigner`), aby utrzymać niskie zużycie pamięci.
- **Testowanie**: Dołącz test jednostkowy, który otwiera zapisany plik przy użyciu Apache POI i sprawdza, czy format liczbowy stylu komórki odpowiada `"$#,##0.00"`.

## Zakończenie

Teraz wiesz, jak **create excel workbook** w Javie, **ustawić format waluty**, **dodać pogrubioną czcionkę** oraz poprawnie **how to import style** przy użyciu `ImportTableOptions` w Aspose.Cells. To kompleksowe rozwiązanie eliminuje ręczne kroki w Excelu i zapewnia, że każda zaimportowana komórka stosuje ten sam styl **format cells currency**.

Gotowy na kolejne wyzwanie? Spróbuj dodać formatowanie warunkowe, osadzenie wykresów lub eksportowanie skoroszytu do PDF — wszystko przy użyciu tej samej techniki tablicy stylów. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}