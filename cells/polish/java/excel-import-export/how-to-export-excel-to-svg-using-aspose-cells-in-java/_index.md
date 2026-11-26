---
category: general
date: 2026-11-25
description: Eksportuj Excel do SVG przy użyciu Aspose.Cells w Javie – krok po kroku
  przewodnik, jak zapisać Excel jako SVG i utworzyć obraz wektorowy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to svg
- save excel as svg
- excel to vector image
- convert excel to svg
- export excel as svg
language: pl
lastmod: 2026-11-25
og_description: Eksportuj pliki Excel do SVG za pomocą Aspose.Cells w Javie. Dowiedz
  się, jak zapisać Excel jako SVG i generować wysokiej jakości obrazy wektorowe w
  kilku linijkach kodu.
og_image_alt: Screenshot of an Excel worksheet exported to SVG format
og_title: Eksportuj Excel do SVG w Javie – kompletny samouczek Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  headline: How to export Excel to SVG using Aspose.Cells in Java
  type: TechArticle
- description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  name: How to export Excel to SVG using Aspose.Cells in Java
  steps:
  - name: Load the workbook containing the data
    text: '```java import com.aspose.cells.Workbook;'
  - name: Set up image export options for SVG
    text: '```java import com.aspose.cells.ImageOrPrintOptions; import com.aspose.cells.ImageFormat;'
  - name: Save the workbook as an SVG file
    text: '```java import com.aspose.cells.SaveFormat;'
  - name: What to explore next
    text: '* **Export Excel as PNG or JPEG** – change `exportOptions.setImageFormat(ImageFormat.PNG)`
      for raster output. * **Convert Excel to PDF** – use `PdfSaveOptions` for printable
      documents. * **Batch processing** – combine the above code with a file‑system
      watcher to automatically **convert Excel to SVG*'
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
- Excel
title: Jak wyeksportować Excel do SVG przy użyciu Aspose.Cells w Javie
url: /pl/java/excel-import-export/how-to-export-excel-to-svg-using-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyeksportować Excel do SVG przy użyciu Aspose.Cells w Javie

Jeśli potrzebujesz **wyeksportować Excel do SVG**, ten przewodnik pokaże Ci, jak to zrobić przy pomocy Aspose.Cells dla Javy. Dowiesz się, jak **zapisać Excel jako SVG** i wygenerować wysokiej jakości **obraz wektorowy** w kilku linijkach kodu.

Eksportowanie skoroszytu Excel do pliku SVG pozwala osadzić arkusz w stronach internetowych, raportach lub w dowolnym środowisku, które preferuje skalowalne grafiki. Format SVG zachowuje czcionki, kolory i obramowania komórek bez pikselizacji, jaką daje obraz rastrowy.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* Java 17 lub nowszą zainstalowaną.
* Aktywną licencję Aspose.Cells dla Javy (lub tymczasowy klucz ewaluacyjny).
* Projekt Maven lub Gradle, w którym możesz dodać zależność Aspose.Cells.

Dodaj bibliotekę Aspose.Cells do swojego projektu:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.10'
```

## Eksport Excel do SVG – krok po kroku

Proces składa się z trzech prostych kroków: wczytaj skoroszyt, skonfiguruj opcje eksportu SVG i zapisz wynik. Każdy krok wyjaśniony jest poniżej.

### Krok 1: Wczytaj skoroszyt zawierający dane

```java
import com.aspose.cells.Workbook;

public class ExcelToSvgDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel file you want to convert.
        Workbook workbook = new Workbook("C:/Data/Report.xlsx");
        // Continue with export options...
    }
}
```

**Dlaczego to ważne:**  
`Workbook` jest centralnym obiektem w Aspose.Cells. Wczytanie pliku raz daje dostęp do wszystkich arkuszy, stylów i osadzonych obiektów, które później zostaną wyrenderowane przez eksportera SVG.

### Krok 2: Skonfiguruj opcje eksportu obrazu dla SVG

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;

ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setImageFormat(ImageFormat.SVG); // Guarantees a vector output
exportOptions.setOnePagePerSheet(true);       // Export each sheet as a single SVG page
exportOptions.setTransparent(true);           // Preserve transparent backgrounds
```

**Dlaczego to ważne:**  
`ImageOrPrintOptions` pozwala kontrolować format wyjściowy. Wybranie `ImageFormat.SVG` zapewnia, że wynik będzie **obrazem wektorowym**, a nie bitmapą. Włączenie `OnePagePerSheet` eliminuje podziały na strony wewnątrz arkusza, co zazwyczaj jest pożądane, gdy SVG będzie wyświetlane w przeglądarce.

### Krok 3: Zapisz skoroszyt jako plik SVG

```java
import com.aspose.cells.SaveFormat;

workbook.save("C:/Output/Report.svg", exportOptions);
System.out.println("Excel workbook successfully exported to SVG.");
```

**Dlaczego to ważne:**  
Metoda `save` łączy wczytany skoroszyt z skonfigurowanymi `exportOptions`. Wywołanie zapisuje w pełni zgodny plik SVG, który można otworzyć w przeglądarkach, Inkscape lub dowolnym edytorze obsługującym grafikę wektorową.

## Pełny przykład do uruchomienia

Połączenie trzech kroków w jedną, samodzielną aplikację, którą możesz od razu skompilować i uruchomić:

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("C:/Data/FontVariation.xlsx");

        // 2. Configure SVG export options
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setImageFormat(ImageFormat.SVG);
        exportOptions.setOnePagePerSheet(true);
        exportOptions.setTransparent(true);

        // 3. Export to SVG
        workbook.save("C:/Output/WithVariationSelectors.svg", exportOptions);
        System.out.println("Export complete: Excel saved as SVG.");
    }
}
```

**Oczekiwany wynik**

Uruchomienie programu wypisuje:

```
Export complete: Excel saved as SVG.
```

Plik `WithVariationSelectors.svg` znajdziesz w `C:/Output`. Otworzenie go w przeglądarce pokazuje arkusz jako skalowalną grafikę, z zachowanym tekstem, obramowaniami i kolorami komórek.

## Typowe warianty i przypadki brzegowe

| Sytuacja | Zalecana zmiana |
|-----------|------------------------|
| **Wiele arkuszy** | Przejdź przez `workbook.getWorksheets()` i wywołaj `save` dla każdego arkusza, opcjonalnie dopisując nazwę arkusza do nazwy pliku. |
| **Duże skoroszyty** | Zwiększ `exportOptions.setRenderThreadCount(int)`, aby używać równoległego renderowania, co skróci czas konwersji. |
| **Niestandardowe DPI** | Wywołaj `exportOptions.setHorizontalResolution(int)` i `exportOptions.setVerticalResolution(int)`, aby kontrolować skalowanie viewBox w SVG. |
| **Osadzanie czcionek** | Ustaw `exportOptions.setExportFontAsSVG(true)`, aby osadzić definicje czcionek bezpośrednio w SVG, zapewniając identyczny wygląd na maszynach bez oryginalnych czcionek. |
| **Pliki zabezpieczone hasłem** | Podaj hasło przy wczytywaniu: `Workbook workbook = new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("pwd"); }});` |

## Porady profesjonalne

* **Unikaj fallbacku rastrowego** – Jeśli arkusz zawiera złożone wykresy, sprawdź, czy pojawiają się jako elementy wektorowe w SVG. Jeśli nie, włącz `exportOptions.setExportChartAsSVG(true)`.
* **Wydajność** – Przy konwersjach wsadowych, ponownie używaj jednej instancji `ImageOrPrintOptions` zamiast tworzyć nową dla każdego pliku.
* **Testowanie** – Zweryfikuj wygenerowany SVG przy pomocy internetowego walidatora (np. W3C SVG Validator), aby wcześnie wykryć ewentualne nieprawidłowości w znacznikach.

## Zweryfikuj konwersję

Możesz programowo potwierdzić, że plik wyjściowy jest rzeczywiście SVG:

```java
import java.nio.file.Files;
import java.nio.file.Paths;

byte[] data = Files.readAllBytes(Paths.get("C:/Output/Report.svg"));
String content = new String(data, "UTF-8");
if (content.contains("<svg")) {
    System.out.println("File is a valid SVG.");
}
```

Obecność elementu `<svg>` w korzeniu wskazuje na udaną operację **convert Excel to SVG**.

## Podsumowanie

Ten tutorial pokazał, jak **wyeksportować Excel do SVG** przy użyciu Aspose.Cells dla Javy. Ładując skoroszyt, konfigurując `ImageOrPrintOptions` dla SVG i wywołując `save`, możesz **zapisać Excel jako SVG** i uzyskać czystą konwersję **Excel do obrazu wektorowego**. Od tego momentu możesz osadzać SVG w stronach internetowych, dołączać go do dokumentacji lub dalej przetwarzać dowolnym narzędziem do grafiki wektorowej.

### Co dalej eksplorować

* **Eksport Excel jako PNG lub JPEG** – zmień `exportOptions.setImageFormat(ImageFormat.PNG)`, aby uzyskać wyjście rastrowe.
* **Konwersja Excel do PDF** – użyj `PdfSaveOptions` dla dokumentów gotowych do druku.
* **Przetwarzanie wsadowe** – połącz powyższy kod z obserwatorem systemu plików, aby automatycznie **convert Excel to SVG** dla każdego nowego skoroszytu w folderze.

Śmiało eksperymentuj z opcjami i pozwól, aby elastyczność Aspose.Cells przekształciła Twoje dane Excel w dowolny format wizualny, którego potrzebujesz. Powodzenia w kodowaniu!

## Co powinieneś się nauczyć dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Export Excel to SVG – Step‑by‑Step Java Guide](/cells/english/java/excel-import-export/how-to-export-excel-to-svg-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}