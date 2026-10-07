---
category: general
date: 2026-10-07
description: Dowiedz się, jak utworzyć plik PNG z zakresu i wyeksportować dane jako
  PNG w Javie. Ten przewodnik pokazuje, jak zapisać obraz zakresu Excel przy użyciu
  Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: pl
lastmod: 2026-10-07
og_description: Utwórz PNG z zakresu w Javie i wyeksportuj dane jako PNG za pomocą
  Aspose.Cells. Skorzystaj z tego kompletnego samouczka, aby natychmiast zapisać obraz
  zakresu Excel.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Utwórz PNG z zakresu w Javie – krok po kroku przewodnik Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak utworzyć PNG z zakresu w Javie przy użyciu Aspose.Cells
url: /pl/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć PNG z zakresu w Javie przy użyciu Aspose.Cells

Jeśli potrzebujesz **utworzyć PNG z zakresu** w skoroszycie Excel, ten samouczek pokaże Ci dokładnie, jak to zrobić. Po zakończeniu przewodnika będziesz w stanie **wyeksportować dane jako PNG**, zapisać obraz zakresu Excel i ponownie wykorzystać plik w raportach lub stronach internetowych.

Zobaczysz kompletny, uruchamialny program w Javie, który ładuje skoroszyt, wybiera żądane komórki, renderuje je jako PNG i zapisuje wynik na dysku. Nie są wymagane żadne zewnętrzne narzędzia — Aspose.Cells obsługuje wszystko wewnętrznie.

## Co obejmuje ten samouczek

* Wymagania wstępne i konfiguracja Maven dla Aspose.Cells
* Ładowanie skoroszytu zawierającego tabelę przestawną lub dowolny zakres danych
* Definiowanie dokładnego zakresu komórek, który chcesz przekonwertować
* Konfigurowanie opcji obrazu dla wyjścia PNG
* Renderowanie zakresu i zapisywanie pliku PNG
* Typowe pułapki i wskazówki dotyczące obrazów wysokiej jakości

Po ukończeniu tych kroków będziesz w stanie **przekonwertować arkusz na PNG** dla dowolnego zakresu, niezależnie od tego, czy jest to prosta tabela, czy złożony wykres przestawny.

## Wymagania wstępne

* Java 17 lub nowszy (kod kompiluje się z JDK 11+)
* Maven 3.6+ (lub Gradle, jeśli wolisz)
* Aspose.Cells for Java 23.12 lub nowszy – dodaj zależność pokazana poniżej
* Istniejący plik Excel (`PivotWithStyle.xlsx`) zawierający zakres, który chcesz przechwycić

> **Pro tip:** Jeśli nie masz licencji, możesz poprosić o tymczasowy klucz ewaluacyjny od Aspose. Biblioteka działa w trybie ewaluacyjnym bez dodatkowej konfiguracji.

### Zależność Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Krok 1: Załaduj skoroszyt zawierający docelowy zakres

Pierwszą operacją jest otwarcie pliku Excel. Aspose.Cells odczytuje plik do pamięci bez wymogu posiadania Microsoft Office.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Dlaczego to jest ważne*: Ładowanie skoroszytu daje dostęp do arkuszy, komórek i właściwości ustawień strony potrzebnych do renderowania.

## Krok 2: Uzyskaj dostęp do arkusza zawierającego zakres

Większość skoroszytów ma domyślny arkusz o indeksie 0, ale możesz również użyć nazwy arkusza.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Jeśli Twoje dane znajdują się na innym arkuszu, zamień `0` na odpowiedni indeks lub użyj `workbook.getWorksheets().get("SheetName")`.

## Krok 3: Zdefiniuj zakres komórek, który chcesz przekonwertować

Możesz określić dowolny prostokątny obszar używając notacji A1. W tym przykładzie przechwytujemy `A1:D15`, co może być tabelą przestawną lub zwykłym blokiem danych.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Przypadek brzegowy*: Gdy zakres zawiera scalone komórki, Aspose.Cells automatycznie rozszerza obraz, aby uwzględnić scalony obszar.

## Krok 4: Przygotuj opcje obrazu PNG

`ImageOrPrintOptions` pozwala kontrolować format, rozdzielczość i inne szczegóły renderowania. Ustawienie formatu zapisu na PNG zapewnia jakość bezstratną.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Zwiększenie DPI jest przydatne, gdy źródłowe komórki zawierają małe czcionki lub szczegółowe wykresy.

## Krok 5: Ogranicz obszar renderowania do wybranego zakresu

Przypisując zakres jako obszar wydruku, Aspose.Cells renderuje tylko te komórki i ignoruje resztę arkusza.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Jeśli pominiesz ten krok, cały arkusz zostanie zrastrowany, co może marnować pamięć i generować większy obraz.

## Krok 6: Renderuj zakres i dodaj obraz do arkusza (opcjonalnie)

Jeśli chcesz osadzić wygenerowany PNG z powrotem w skoroszycie (w celach podglądu), możesz dodać go jako obraz. Ten krok jest opcjonalny w scenariuszach czystego eksportu.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Dlaczego możesz to zrobić*: Niektóre przepływy pracy wymagają, aby obraz był częścią skoroszytu przed dystrybucją, np. tworzenie raportu do druku, który łączy natywne komórki i obrazy.

## Krok 7: Zapisz plik PNG na dysku

Na koniec zapisz obraz do pliku. Metoda `save` respektuje format określony w `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Po zakończeniu programu, `PivotImage.png` będzie zawierał pikselowo idealny zrzut komórek `A1:D15`.

### Oczekiwany wynik

* Plik o nazwie `PivotImage.png` znajdujący się w `YOUR_DIRECTORY`.
* Obraz pokazuje dokładny układ, czcionki, kolory i obramowania z wybranego zakresu.
* Jeśli źródłowy zakres zawiera tabelę przestawną, renderowany obraz zawiera te same style i obliczone wartości, jak wyświetlane w Excelu.

## Obsługa typowych scenariuszy

### Eksportowanie nieciągłego zakresu

Aspose.Cells nie renderuje rozłącznych zakresów w jednym obrazie. Aby wyeksportować wiele obszarów, utwórz osobne obrazy dla każdego zakresu i połącz je później przy użyciu biblioteki przetwarzania obrazów (np. ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Zapisywanie dużego arkusza jako PNG

Renderowanie całego arkusza obejmującego tysiące wierszy może zużywać znaczną ilość pamięci. Zminimalizuj to poprzez:

* Zmniejszenie DPI (`imageOptions.setResolution(72)`) dla mniejszego pliku.
* Użycie `setPageCount` aby ograniczyć liczbę renderowanych stron.
* Eksportowanie jednej drukowalnej strony na raz za pomocą `worksheet.getPageSetup().setPrintArea(...)`.

### Zachowanie formuł komórek

Obraz PNG jest formatem rastrowym; formuły nie są zachowywane. Jeśli odbiorcy potrzebują surowych danych, wyeksportuj także zakres jako CSV lub JSON używając `Range.exportDataTable()`.

## Pełny, uruchamialny przykład

Poniżej znajduje się pełna klasa Java, którą możesz skopiować i wkleić do swojego IDE. Zamień `YOUR_DIRECTORY` na absolutną lub względną ścieżkę na swoim komputerze.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Uruchom program poleceniem `mvn compile exec:java` (lub używając preferowanego narzędzia budującego). Po wykonaniu otwórz `PivotImage.png`, aby zweryfikować wynik.

## Zakończenie

Teraz wiesz, jak **utworzyć PNG z zakresu** w Javie przy użyciu Aspose.Cells, skutecznie **wyeksportować dane jako PNG** i **zapisać obraz zakresu Excel** dla dowolnego scenariusza raportowania lub udostępniania. Kroki — ładowanie skoroszytu, definiowanie zakresu, konfigurowanie opcji obrazu, ustawianie obszaru wydruku i zapisywanie pliku — obejmują cały przepływ pracy dla **konwersji arkusza na PNG** i **zapisu komórek jako PNG**.

### Kolejne kroki

* Eksperymentuj z różnymi wartościami `Resolution`, aby zbalansować jakość i rozmiar pliku.
* Użyj `ImageOrPrintOptions.setTransparent(true)`, jeśli potrzebujesz PNG z przezroczystym tłem.
* Połącz wiele obrazów zakresów w jeden PDF używając `PdfSaveOptions` dla raportów wielostronicowych.
* Zbadaj eksport do innych formatów rastrowych (JPEG, BMP) zmieniając `setSaveFormat`.

Śmiało dostosuj ten wzorzec do wykresów, tabel lub nawet całych arkuszy. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak wyeksportować arkusz Excel do PNG przy użyciu Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Konwertowanie Excela do PNG przy użyciu Aspose.Cells dla Java: Przewodnik krok po kroku](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Tworzenie zakresu złączenia w Excelu przy użyciu Aspose.Cells Java: Kompletny przewodnik](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}