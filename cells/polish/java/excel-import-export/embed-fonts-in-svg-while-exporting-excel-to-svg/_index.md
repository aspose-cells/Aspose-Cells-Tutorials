---
category: general
date: 2026-08-14
description: Osadź czcionki w formacie SVG podczas eksportowania pliku Excel do SVG
  przy użyciu Aspose.Cells. Dowiedz się, jak ustawić obszar wydruku, ustawić opcje
  wydruku i używać funkcji WRAPCOLS.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: pl
lastmod: 2026-08-14
og_description: Osadź czcionki w SVG podczas eksportowania pliku Excel do SVG przy
  użyciu Aspose.Cells. Ten przewodnik pokazuje, jak ustawić obszar wydruku, skonfigurować
  opcje drukowania i zastosować funkcję WRAPCOLS.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Osadzanie czcionek w SVG podczas eksportowania Excela do SVG – krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Osadź czcionki w SVG podczas eksportowania Excela do SVG
url: /pl/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Osadzanie czcionek w SVG podczas eksportowania Excela do SVG

Jeśli potrzebujesz **osadzić czcionki w SVG podczas eksportowania Excela do SVG**, ten samouczek pokaże Ci dokładnie, jak to zrobić przy użyciu Aspose.Cells for Java. Omówimy także, jak **ustawić obszar wydruku**, **ustawić opcje wydruku** oraz **użyć funkcji WRAPCOLS**, aby sformatować dane bez utraty układu.

Przejdziesz przez kompletny, gotowy do uruchomienia przykład, który ładuje istniejący skoroszyt, stosuje formułę `WRAPCOLS`, konfiguruje specyficzne dla SVG opcje obrazu, definiuje region wydruku i w końcu zapisuje plik jako SVG z osadzonymi czcionkami. Nie jest wymagana żadna zewnętrzna dokumentacja — po prostu skopiuj kod, uruchom go i sprawdź wygenerowany SVG.

## Osadzanie czcionek w SVG – konfigurowanie ImageOrPrintOptions

Osadzanie czcionek zapewnia, że SVG renderuje się dokładnie tak, jak w Excelu, nawet na maszynach, które nie mają zainstalowanych oryginalnych krojów pisma.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Dlaczego to ważne*: Gdy `setEmbedFonts(true)` jest włączone, Aspose.Cells zapisuje dane czcionki bezpośrednio w sekcji `<defs>` SVG. Wynikiem jest samodzielny plik, który wygląda identycznie we wszystkich przeglądarkach i na różnych platformach.

## Eksport Excela do SVG – pełny przepływ pracy

Poniższe kroki ilustrują proces od początku do końca, od wczytania skoroszytu po zapisanie pliku SVG.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Oczekiwany wynik**: `output.svg` pojawia się w `YOUR_DIRECTORY`. Otworzenie go w przeglądarce pokazuje arkusz z wszystkimi osadzonymi czcionkami, dane zawinięte w trzy kolumny (dzięki `WRAPCOLS`) i renderowane tylko komórki w zakresie `A1:H30`.

## Ustawienie obszaru wydruku dla arkusza

Zdefiniowanie obszaru wydruku ogranicza eksportowane SVG do określonego zakresu, co zmniejsza rozmiar pliku i skupia uwagę odbiorcy na istotnych danych.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Wskazówka*: Zakres używa notacji A1 Excela. Jeśli potrzebujesz dynamicznego zakresu, możesz obliczyć go programowo przy użyciu `ws.getCells().getMaxDisplayRange()`.

## Ustawienie opcji wydruku dla wyjścia SVG

Opcje wydruku kontrolują, w jaki sposób Aspose.Cells przetwarza arkusz na obraz. Oprócz osadzania czcionek, możesz dostosować rozdzielczość, skalowanie i układ strony.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Dlaczego warto ustawić opcje wydruku*: Bez wyraźnych ustawień Aspose.Cells używa domyślnych wartości, które mogą pominąć osadzanie czcionek lub zastosować niepożądany współczynnik skalowania, co prowadzi do rozmytych lub nieprawidłowo stylizowanych SVG.

## Użycie funkcji WRAPCOLS do zawijania danych w kolumnach

`WRAPCOLS` to formuła Excela, która rozdziela pionowy zakres na określoną liczbę kolumn. Jest przydatna, gdy chcesz wyświetlić długą listę w zwartym układzie.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

Gdy skoroszyt zostanie zapisany, Aspose.Cells ocenia formułę, tworząc układ trzech kolumn w zdefiniowanym obszarze wydruku. Ta technika działa dla dowolnego rozmiaru zakresu — wystarczy dostosować drugi argument do żądanej liczby kolumn.

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się pełny program w Javie, który możesz wkleić do dowolnego IDE. Upewnij się, że biblioteka Aspose.Cells for Java znajduje się w classpath.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Kroki weryfikacji**

1. Uruchom program.  
2. Otwórz `output.svg` w przeglądarce internetowej.  
3. Potwierdź, że tekst używa tego samego kroju pisma co oryginalny plik Excel (czcionki są osadzone).  
4. Zweryfikuj, że pojawiają się tylko komórki w zakresie `A1:H30` oraz że dane z `A2:A10` są wyświetlane w trzech kolumnach.

## Typowe pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| Czcionki brakują w SVG | `setEmbedFonts(false)` lub plik czcionki jest niedostępny | Upewnij się, że `setEmbedFonts(true)` i że czcionka jest zainstalowana na maszynie uruchamiającej kod |
| WRAPCOLS nie jest oceniane | Silnik obliczeniowy wyłączony | Wywołaj `workbook.calculateFormula()` przed eksportem lub pozwól Aspose.Cells ocenić podczas zapisu |
| Wyeksportowany SVG jest pusty | Obszar wydruku nie zawiera żadnych danych | Sprawdź ponownie zakres przekazywany do `setPrintArea` |
| Plik SVG jest ogromny | Nie zastosowano skalowania, wysoka rozdzielczość obrazu | Dostosuj `imgOptions.setResolution(96)` lub podobnie, aby kontrolować DPI |

## Pro tip: ponowne użycie ImageOrPrintOptions dla wielu arkuszy

Jeśli Twój skoroszyt zawiera kilka arkuszy, które wymagają identycznych ustawień SVG, utwórz jedną instancję `ImageOrPrintOptions` i przypisz ją do `PageSetup` każdego arkusza. To zmniejsza zużycie pamięci i zapewnia spójne osadzanie czcionek we wszystkich wyeksportowanych plikach.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Kolejne kroki

* **Eksport do innych formatów wektorowych** – Zmien `ImageFormat.SVG` na `ImageFormat.PDF`, aby uzyskać wysokiej jakości PDFy.  
* **Przetwarzanie wsadowe** – Przejdź pętlą przez folder z plikami `.xlsx` i generuj SVG automatycznie.  
* **Obsługa własnych czcionek** – Użyj `FontSettings`, aby wczytać czcionki z określonego katalogu, gdy systemowe czcionki są niewystarczające.  

Opanowując **embed fonts in SVG**, **export excel to svg**, **set print area**, **set print options** i **use WRAPCOLS function**, możesz zautomatyzować generowanie wysokiej jakości SVG dla raportów, pulpitów nawigacyjnych i wizualizacji webowych bezpośrednio z danych Excela. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak ustawić obszar wydruku w Excelu przy użyciu Aspose.Cells dla .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Ustaw obszar wydruku Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Ustaw obszar wydruku Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}