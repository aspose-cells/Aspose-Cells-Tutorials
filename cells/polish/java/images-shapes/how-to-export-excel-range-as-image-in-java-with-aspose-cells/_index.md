---
category: general
date: 2026-10-10
description: Dowiedz się, jak wyeksportować zakres Excela jako obraz w Javie przy
  użyciu Aspose.Cells. Poradnik obejmuje również eksport wybranych komórek jako obrazu
  oraz zapisanie arkusza Excela jako obrazka.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- export selected cells as image
- save excel worksheet as picture
language: pl
lastmod: 2026-10-10
og_description: Eksportuj zakres Excela jako obraz w Javie, krok po kroku. Zawiera
  eksport wybranych komórek jako obrazu oraz zapisanie arkusza Excela jako obrazka.
og_image_alt: Diagram showing export Excel range as image using Java and Aspose.Cells
og_title: Eksportuj zakres Excela jako obraz w Javie – kompletny przewodnik Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  headline: How to export Excel range as image in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  name: How to export Excel range as image in Java with Aspose.Cells
  steps:
  - name: Why this method matters
    text: '* **Separation of concerns:** Loading, option configuration, and exporting
      are clearly divided. * **Flexibility:** You can change the image format or DPI
      without touching the core logic. * **Error handling:** Throwing `Exception`
      lets the caller decide whether to log, retry, or abort.'
  - name: 1. Merged cells
    text: Aspose.Cells automatically preserves merged cell appearance, but if you
      need to control the rendering, set `options.setOnePagePerSheet(true)` to force
      the whole sheet onto a single page before exporting.
  - name: 2. Hidden rows or columns
    text: 'By default, hidden rows/columns are not rendered. To include them, enable:'
  - name: 3. Large ranges and memory consumption
    text: 'Exporting very large ranges can consume significant memory. If you encounter
      `OutOfMemoryError`, consider:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- Image export
title: Jak wyeksportować zakres Excela jako obraz w Javie przy użyciu Aspose.Cells
url: /pl/java/images-shapes/how-to-export-excel-range-as-image-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyeksportować zakres Excela jako obraz w Javie z Aspose.Cells

Jeśli potrzebujesz **wyeksportować zakres Excela jako obraz**, ten tutorial przeprowadzi Cię przez kompletną rozwiązanie w Javie przy użyciu biblioteki Aspose.Cells. Dowiesz się również, jak **wyeksportować wybrane komórki jako obraz** oraz jak **zapisać arkusz Excela jako obraz** w celach raportowania lub dokumentacji.

Eksportowanie części skoroszytu do obrazu eliminuje potrzebę korzystania z zewnętrznych narzędzi do zrzutów ekranu i gwarantuje wyniki piksel‑perfekcyjne. Po zakończeniu tego przewodnika będziesz posiadać wielokrotnego użytku metodę, która zapisuje PNG (lub dowolny obsługiwany format) bezpośrednio na dysk, gotową do włączenia do PDF‑ów, e‑maili lub stron internetowych.

## Prerequisites

Przed rozpoczęciem upewnij się, że masz:

* Zainstalowany Java 17 lub nowszy.
* Maven 3.8+ (lub inne narzędzie budujące, które obsługuje zależności Maven).
* Licencję Aspose.Cells for Java (bezpłatna wersja próbna działa, ale dodaje znak wodny).
* Przykładowy plik Excel (`input.xlsx`) umieszczony w znanym katalogu.

Poniższe sekcje zakładają, że jesteś zaznajomiony z podstawowym programowaniem w Javie oraz konfiguracją projektu Maven.

## Step 1: Add Aspose.Cells to your project

Dodaj zależność Aspose.Cells Maven do swojego `pom.xml`. Ta biblioteka dostarcza klasy `Workbook`, `Worksheet` i `ImageOrPrintOptions` używane w przykładzie kodu.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

> **Wskazówka:** Utrzymuj numer wersji aktualny; nowsze wydania dodają wsparcie dla formatów i ulepszenia wydajności.

## Step 2: Create a utility method to export a range

Ujęcie logiki eksportu w metodzie ułatwia jej ponowne użycie w różnych projektach oraz obsługę przypadków brzegowych, takich jak scalone komórki czy ukryte wiersze.

```java
import com.aspose.cells.*;

import java.io.File;

/**
 * Exports a specific cell range from an Excel worksheet to an image file.
 *
 * @param workbookPath   Full path to the source .xlsx file.
 * @param sheetIndex     Zero‑based index of the worksheet (0 = first sheet).
 * @param range          A‑style range string, e.g. "A1:G20".
 * @param outputPath     Full path where the image will be saved.
 * @param imageFormat    Desired image format (PNG, JPEG, BMP, etc.).
 * @throws Exception if the file cannot be read or written.
 */
public static void exportRangeAsImage(
        String workbookPath,
        int sheetIndex,
        String range,
        String outputPath,
        ImageFormat imageFormat) throws Exception {

    // Load the workbook
    Workbook wb = new Workbook(workbookPath);

    // Obtain the requested worksheet
    Worksheet ws = wb.getWorksheets().get(sheetIndex);

    // Configure image export options
    ImageOrPrintOptions options = new ImageOrPrintOptions();
    options.setImageFormat(imageFormat);
    // Optional: increase DPI for higher‑resolution output
    options.setHorizontalResolution(300);
    options.setVerticalResolution(300);

    // Export the defined range as an image file
    ws.getCells().exportRangeAsImage(range, outputPath, options);
}
```

### Dlaczego ta metoda ma znaczenie

* **Rozdzielenie odpowiedzialności:** Ładowanie, konfiguracja opcji i eksport są wyraźnie podzielone.
* **Elastyczność:** Możesz zmienić format obrazu lub DPI bez modyfikacji głównej logiki.
* **Obsługa błędów:** Rzucanie `Exception` pozwala wywołującemu zdecydować, czy logować, ponowić próbę, czy przerwać.

## Step 3: Call the method with real parameters

Poniżej znajduje się minimalna metoda `main`, która demonstruje, jak **wyeksportować wybrane komórki jako obraz** oraz jak **zapisać arkusz Excela jako obraz** używając pełnego zakresu arkusza.

```java
public class ExcelImageExporter {
    public static void main(String[] args) {
        try {
            String inputFile   = "C:/Data/input.xlsx";
            String outputFile1 = "C:/Data/range.png";
            String outputFile2 = "C:/Data/full_sheet.png";

            // Export a specific range (A1:G20)
            exportRangeAsImage(
                    inputFile,
                    0,                  // first worksheet
                    "A1:G20",
                    outputFile1,
                    ImageFormat.PNG);   // primary format for lossless quality

            // Export the entire first worksheet – effectively saving the worksheet as picture
            exportRangeAsImage(
                    inputFile,
                    0,
                    "A1:" + getLastCellAddress(inputFile, 0), // compute last used cell
                    outputFile2,
                    ImageFormat.PNG);

            System.out.println("Images generated successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Helper that returns the address of the last used cell in a worksheet.
     */
    private static String getLastCellAddress(String workbookPath, int sheetIdx) throws Exception {
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.getWorksheets().get(sheetIdx);
        // Find the maximum row and column that contain data
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();
        // Convert column index to A‑style letter (0 -> A)
        String colLetter = CellReference.convertNumToColString(maxCol);
        return colLetter + (maxRow + 1);
    }
}
```

#### Expected output

Uruchomienie programu tworzy dwa pliki PNG:

* `range.png` – obraz zawierający tylko komórki **A1:G20**.
* `full_sheet.png` – obraz całego używanego obszaru pierwszego arkusza, skutecznie **zapisujący arkusz Excela jako obraz**.

Możesz otworzyć pliki w dowolnym przeglądarce obrazów, aby zweryfikować, że układ wizualny odpowiada widokowi w Excelu, włączając obramowania komórek, kolory i scalone komórki.

## Step 4: Handle common edge cases

### 1. Merged cells

Aspose.Cells automatycznie zachowuje wygląd scalonych komórek, ale jeśli potrzebujesz kontrolować renderowanie, ustaw `options.setOnePagePerSheet(true)`, aby wymusić umieszczenie całego arkusza na jednej stronie przed eksportem.

### 2. Hidden rows or columns

Domyślnie ukryte wiersze/kolumny nie są renderowane. Aby je uwzględnić, włącz:

```java
options.setSkipEmptyRows(false);
options.setSkipEmptyColumns(false);
```

### 3. Large ranges and memory consumption

Eksport bardzo dużych zakresów może zużywać znaczną ilość pamięci. Jeśli napotkasz `OutOfMemoryError`, rozważ:

* Zmniejszenie DPI (`options.setHorizontalResolution(150)`).
* Eksportowanie zakresu w mniejszych fragmentach i łączenie obrazów przy użyciu biblioteki graficznej.

## Step 5: Verify the result programmatically (optional)

Jeśli Twój proces downstream wymaga potwierdzenia, że obraz został wygenerowany poprawnie, możesz wczytać PNG przy użyciu `javax.imageio.ImageIO` i sprawdzić jego wymiary:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File(outputFile1));
System.out.println("Image width: " + img.getWidth() + " px");
System.out.println("Image height: " + img.getHeight() + " px");
```

Nie‑zerowa szerokość i wysokość wskazują na pomyślny eksport.

## Conclusion

Teraz wiesz, jak **wyeksportować zakres Excela jako obraz** w Javie, jak **wyeksportować wybrane komórki jako obraz**, oraz jak **zapisać arkusz Excela jako obraz** przy użyciu Aspose.Cells. Wielokrotnego użytku metoda `exportRangeAsImage` abstrahuje złożoność, pozwala kontrolować jakość obrazu i działa z dowolnym indeksem arkusza lub zakresem komórek.

Kolejne kroki, które możesz rozważyć:

* Konwertuj PNG do PDF przy użyciu Aspose.PDF w celu raportowania.
* Przetwarzaj wsadowo wiele skoroszytów w katalogu.
* Zintegruj eksport obrazu z endpointem REST Spring Boot, aby klienci mogli żądać obrazów na żądanie.

Śmiało eksperymentuj z różnymi formatami obrazu (`ImageFormat.JPEG`, `ImageFormat.BMP`) oraz ustawieniami DPI, aby spełnić wizualne wymagania Twojego projektu. Szczęśliwego kodowania!

## What Should You Learn Next?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}