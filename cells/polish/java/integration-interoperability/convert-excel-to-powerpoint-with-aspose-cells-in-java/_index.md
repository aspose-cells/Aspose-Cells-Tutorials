---
category: general
date: 2026-09-21
description: Konwertuj Excel na PowerPoint przy użyciu Aspose.Cells w Javie – dowiedz
  się, jak wyeksportować wykres do PPTX i zapisać skoroszyt jako PPTX w kilku linijkach
  kodu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- save workbook as pptx
- how to export chart to pptx
- create powerpoint from excel chart
language: pl
lastmod: 2026-09-21
og_description: Konwertuj Excel na PowerPoint przy użyciu Aspose.Cells w Javie. Ten
  tutorial pokazuje, jak wyeksportować wykres do formatu PPTX i zapisać skoroszyt
  jako PPTX z edytowalnymi polami tekstowymi.
og_image_alt: Screenshot of Java code converting an Excel workbook to a PowerPoint
  presentation
og_title: Konwertuj Excel do PowerPoint przy użyciu Aspose.Cells – przewodnik Java
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Convert Excel to PowerPoint with Aspose.Cells in Java – learn how to
    export chart to PPTX and save workbook as PPTX in just a few lines of code.
  headline: Convert Excel to PowerPoint with Aspose.Cells in Java
  type: TechArticle
- questions:
  - answer: Yes. Loop through each worksheet, export its chart to a new slide using
      `PdfSaveOptions`, and then save the workbook once after processing all sheets.
    question: Can I convert multiple worksheets into separate PowerPoint slides?
  - answer: Only chart and textbox objects are transferred to PowerPoint. Cell formatting
      stays in the Excel file; it does not appear in the PPTX.
    question: Does this method preserve cell formatting?
  - answer: 'Use `SaveFormat.PDF` and the same `PdfSaveOptions`. The `setExportEditableTextBoxes`
      flag works for PDF as well. ## Next steps Now that you know how to **save workbook
      as PPTX** and **export chart to PPTX**, you might explore: * Adding multiple
      charts to different slides (`create powerpoint from exc'
    question: What if I need to export to PDF instead of PPTX?
  type: FAQPage
tags:
- Excel
- PowerPoint
- Aspose.Cells
- Java
title: Konwertuj Excel do PowerPoint przy użyciu Aspose.Cells w Javie
url: /pl/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertuj Excel do PowerPoint przy użyciu Aspose.Cells w Javie

Jeśli potrzebujesz **konwertować Excel do PowerPoint**, ten przewodnik pokaże Ci zwięzły, gotowy do produkcji sposób wykonania tego zadania. Zobaczysz, jak wyeksportować wykres do PPTX, zachować edytowalne pola tekstowe oraz **zapisać skoroszyt jako PPTX** w zaledwie trzech linijkach kodu Java.

Wielu programistów eksportuje dane do PDF, ale PowerPoint często lepiej sprawdza się w prezentacjach wymagających dynamicznych wykresów i edytowalnych elementów. Ten tutorial obejmuje wszystko, czego potrzebujesz — od konfiguracji projektu po obsługę typowych problemów — abyś mógł stworzyć prezentację PowerPoint z wykresem Excel bez opuszczania swojego środowiska IDE Java.

## Prerequisites

Zanim rozpoczniesz, upewnij się, że masz:

* Java 17 lub nowszą.
* Maven (lub Gradle) do zarządzania zależnościami.
* Licencję Aspose.Cells for Java (bezpłatna wersja próbna wystarczy do oceny).
* Plik Excel (`ChartAndTextbox.xlsx`) zawierający przynajmniej jeden wykres i pole tekstowe.

## Step 1: Add Aspose.Cells to your project

Pierwszym krokiem jest dołączenie biblioteki Aspose.Cells. Korzystając z Maven, dodaj następującą zależność do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Jeśli używasz Gradle, równoważny zapis to:
> ```groovy
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Dołączenie biblioteki daje dostęp do klas `Workbook`, `PdfSaveOptions` oraz wyliczenia `SaveFormat`, które są niezbędne do konwersji.

## Step 2: Load the workbook that contains the chart and textbox

Teraz wczytaj plik Excel. Klasa `Workbook` odczytuje cały skoroszyt do pamięci, zachowując wykresy, formuły i pola tekstowe.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Adjust the path to point to your Excel file
        String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";

        // Load the workbook
        Workbook workbook = new Workbook(sourcePath);
        
        // Continue with conversion...
    }
}
```

**Dlaczego to ważne:** Wczytanie skoroszytu w pierwszej kolejności zapewnia, że wszystkie osadzone obiekty (wykresy, obrazy, pola tekstowe) są dostępne podczas procesu eksportu. Jeśli plik nie zostanie znaleziony, Aspose.Cells zgłosi wyraźny `FileNotFoundException`, który możesz przechwycić, aby zapewnić lepsze doświadczenie użytkownika.

## Step 3: Configure export options to keep text boxes editable

Aspose.Cells używa `PdfSaveOptions` do kontrolowania sposobu zapisu obiektów, gdy docelowym formatem jest PowerPoint. Włączając `setExportEditableTextBoxes(true)`, każde pole tekstowe w arkuszu Excel pozostaje edytowalne po konwersji.

```java
import com.aspose.cells.PdfSaveOptions;

PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.setExportEditableTextBoxes(true); // Text boxes stay editable in the PPTX
```

> **Dlaczego używać `PdfSaveOptions` dla PPTX?**  
> Wewnątrz Aspose.Cells ponownie wykorzystuje potok renderowania PDF do generowania plików PowerPoint, co umożliwia precyzyjną kontrolę nad edytowalnymi elementami. Ustawienie tego flagi jest zalecanym sposobem zachowania edytowalności pól tekstowych.

## Step 4: Save the workbook as a PowerPoint presentation

Na koniec wywołaj `workbook.save` z parametrem `SaveFormat.PPTX`. Ten krok kończy **workflow tworzenia PowerPoint z wykresem Excel**.

```java
import com.aspose.cells.SaveFormat;

String targetPath = "YOUR_DIRECTORY/Result.pptx";
workbook.save(targetPath, SaveFormat.PPTX, saveOptions);
System.out.println("Conversion successful! PPTX saved to " + targetPath);
```

Łącząc wszystko razem, pełny program wygląda tak:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.PdfSaveOptions;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook containing the chart and textbox
            String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2. Create PDF save options and enable editable text boxes for PPTX output
            PdfSaveOptions saveOptions = new PdfSaveOptions();
            saveOptions.setExportEditableTextBoxes(true); // text boxes will remain editable in the PPTX

            // 3. Save the workbook as a PowerPoint presentation using the configured options
            String targetPath = "YOUR_DIRECTORY/Result.pptx";
            workbook.save(targetPath, SaveFormat.PPTX, saveOptions);

            System.out.println("Conversion successful! PPTX saved to " + targetPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Expected output

Uruchomienie programu wypisuje:

```
Conversion successful! PPTX saved to YOUR_DIRECTORY/Result.pptx
```

Po otwarciu `Result.pptx` w Microsoft PowerPoint zobaczysz:

* Oryginalny wykres Excel wyświetlony jako natywny wykres PowerPoint (edytowalny w edytorze wykresów PowerPoint).
* Pole tekstowe z Excela pojawia się jako edytowalny kształt, umożliwiając bezpośrednią zmianę tekstu na slajdzie.

## Handling common edge cases

| Situation | Recommended approach |
|-----------|----------------------|
| **File not found** | Wrap the `Workbook` constructor in a `try‑catch` block and display a clear message. |
| **Workbook has no chart** | Verify the sheet contains a chart (`worksheet.getCharts().getCount() > 0`) before conversion; otherwise, skip the step or add a placeholder. |
| **Large Excel files** | Increase the JVM heap size (`-Xmx2g`) to avoid `OutOfMemoryError` during rendering. |
| **License not set** | Call `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` before loading the workbook to remove the evaluation watermark. |

## Frequently asked questions

**Q: Can I convert multiple worksheets into separate PowerPoint slides?**  
A: Yes. Loop through each worksheet, export its chart to a new slide using `PdfSaveOptions`, and then save the workbook once after processing all sheets.

**Q: Does this method preserve cell formatting?**  
A: Only chart and textbox objects are transferred to PowerPoint. Cell formatting stays in the Excel file; it does not appear in the PPTX.

**Q: What if I need to export to PDF instead of PPTX?**  
A: Use `SaveFormat.PDF` and the same `PdfSaveOptions`. The `setExportEditableTextBoxes` flag works for PDF as well.

## Next steps

Now that you know how to **save workbook as PPTX** and **export chart to PPTX**, you might explore:

* Adding multiple charts to different slides (`create powerpoint from excel chart` with a loop).
* Customizing slide layouts using Aspose.Slides for Java for richer presentation styling.
* Embedding images from Excel cells into PowerPoint using the `Picture` class.

These extensions let you build fully automated reporting pipelines that generate polished presentations directly from Excel data.

---

**Summary:** This tutorial demonstrated a reliable way to **convert Excel to PowerPoint** using Aspose.Cells for Java. By loading the workbook, configuring `PdfSaveOptions` to keep text boxes editable, and saving with `SaveFormat.PPTX`, you obtain a PowerPoint file that contains live charts and editable shapes—perfect for dynamic business presentations. Feel free to adapt the code for batch processing or integrate it into larger reporting solutions.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells in Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}