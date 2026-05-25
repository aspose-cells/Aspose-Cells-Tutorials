---
category: general
date: 2026-03-01
description: Lär dig hur du bäddar in teckensnitt i HTML och andra format. Steg‑för‑steg‑handledning
  som täcker inbäddning av teckensnitt i HTML, konvertera Excel till HTML, hur man
  exporterar OLE och konvertera Excel till XPS.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- how to export ole
- convert excel to xps
language: sv
og_description: Hur man bäddar in typsnitt i HTML-, XPS- och OLE-export. Lär dig hela
  arbetsflödet, se körbar Java‑kod och behärska inbäddning av typsnitt i HTML för
  Excel‑konverteringar.
og_title: Hur man bäddar in teckensnitt – Fullständig Java‑handledning
tags:
- Aspose.Cells
- Java
- Document Export
title: Hur man bäddar in typsnitt – Komplett guide för HTML-, XPS- och OLE-export
url: /sv/java/ole-objects-embedded-content/how-to-embed-fonts-complete-guide-for-html-xps-and-ole-expor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man bäddar in typsnitt – Komplett guide för HTML, XPS och OLE‑export

Har du någonsin undrat **how to embed fonts** när du omvandlar en Excel‑arbetsbok till en webbsida eller ett utskriftsbart dokument? Du är inte ensam. Många utvecklare stöter på problem när resultatet ser bra ut på deras maskin men går sönder på en annan eftersom de nödvändiga typsnitten saknas.  

I den här handledningen går vi igenom ett verkligt scenario med Aspose.Cells for Java: vi bäddar in typsnitt i HTML, bevarar emoji‑variationsväljare vid konvertering till XPS, och behåller till och med ett OLE‑objekt redigerbart när vi exporterar till PPTX. I slutet har du en solid, kopiera‑och‑klistra‑lösning som svarar på “how to embed fonts” och även berör **embed fonts in html**, **convert excel to html**, **how to export ole**, och **convert excel to xps**.

## Förutsättningar

- Java 17 (eller någon nyare JDK)  
- Aspose.Cells for Java 25.x eller senare  
- En utvecklings‑IDE (IntelliJ IDEA, Eclipse eller VS Code)  
- Grundläggande kunskap om Excel‑datastrukturer  

Inga externa tjänster krävs—allt körs lokalt.

## Översikt av lösningen

1. **Create a workbook** och använd `WRAPCOLS`‑funktionen för att omvandla ett vertikalt område till en tre‑kolumns layout.  
2. **Save the workbook as XPS** medan du aktiverar font variation selectors så att emoji förblir intakta.  
3. **Export to HTML** med inbäddade typsnitt, vilket garanterar att sidan ser likadan ut överallt.  
4. **Export a workbook containing an OLE object to PPTX**, bevarar redigerbarhet.  
5. **Apply a Smart Marker template** som demonstrerar master‑detail‑databindning.  

Varje steg är isolerat i sin egen H2‑sektion, vilket gör guiden lätt att skumma igenom för både sökmotorer och AI‑assistenter.

![Illustration av hur man bäddar in typsnitt](image.png "hur man bäddar in typsnitt")

*Bildtext: diagram som visar arbetsflödet från Excel till HTML, XPS och PPTX för hur man bäddar in typsnitt.*

---

## Steg 1 – Skapa en arbetsbok och använd WRAPCOLS (Varför detta är viktigt för embed fonts in html)

Innan vi kan prata om att bädda in typsnitt behöver vi en arbetsbok som faktiskt innehåller data. `WRAPCOLS`‑funktionen är ett praktiskt sätt att dela en enda kolumn i flera kolumner, vilket ofta gör den slutliga HTML‑koden mer läsbar.

```java
import com.aspose.cells.*;

public class EmbedFontsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Populate A2:A10 with sample data
        for (int i = 2; i <= 10; i++) {
            sheet.getCells().get("A" + i).putValue("Item " + (i - 1));
        }

        // Use WRAPCOLS to create a 3‑column block starting at A1
        Cell resultCell = sheet.getCells().get("A1");
        resultCell.setFormula("=WRAPCOLS(A2:A10,3)");
        workbook.calculateFormula();

        System.out.println("WRAPCOLS result: " + resultCell.getStringValue());
        // -----------------------------------------------------------------
        // The rest of the steps are demonstrated after this point.
        // -----------------------------------------------------------------
```

**Varför detta steg?**  
`WRAPCOLS`‑anropet genererar ett multi‑column‑område som senare visas i HTML som en tabell. När vi senare **embed fonts in html**, kommer tabellens stil att bero på de typsnitt vi bäddar in, vilket säkerställer konsekvent rendering i alla webbläsare.

## Steg 2 – Spara arbetsboken som XPS medan du bevarar emoji (convert excel to xps)

Om du behöver ett utskriftsklart format är XPS ett bra val. Moderna dokument innehåller ofta emoji eller symboler som använder variationsväljare. Att aktivera `EnableFontVariationSelectors` säkerställer att dessa tecken överlever konverteringen.

```java
        // --------------------------------------------------------------
        // Step 2: Save as XPS with font variation selectors enabled
        // --------------------------------------------------------------
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true); // crucial for emoji

        String xpsPath = "output/withVariations.xps";
        workbook.save(xpsPath, SaveFormat.XPS);
        System.out.println("Workbook saved as XPS at: " + xpsPath);
```

**Vad du får:**  
En XPS‑fil som visar alla inbäddade emoji exakt som i källarbetsboken. Detta uppfyller kravet **convert excel to xps** och visar att typsnittshantering inte är begränsad till HTML.

## Steg 3 – Exportera till HTML med inbäddade typsnitt (how to embed fonts & embed fonts in html)

Nu kommer vi till kärnan i handledningen: **how to embed fonts** när vi konverterar Excel till HTML. Aspose.Cells låter oss bädda in typsnitten direkt i den genererade HTML‑filen, vilket eliminerar behovet av externa typsnittsfiler.

```java
        // --------------------------------------------------------------
        // Step 3: Export to HTML with embedded fonts
        // --------------------------------------------------------------
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setEmbedFonts(true); // this is the key line for embed fonts in html
        htmlOptions.setExportImagesAsBase64(true); // optional, keeps all assets in one file

        String htmlPath = "output/embeddedFonts.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML with embedded fonts saved at: " + htmlPath);
```

**Hur det fungerar:**  
`setEmbedFonts(true)` instruerar renderaren att läsa de typsnittsfiler som används i arbetsboken och bädda in dem som Base64‑kodade `@font-face`‑regler i `<style>`‑taggen. Den resulterande HTML‑filen är självständig, så du kan lägga upp den på vilken server som helst och typsnitten kommer att renderas korrekt—precis vad utvecklare efterfrågar när de söker **how to embed fonts**.

**Förväntat utdrag av output (i `embeddedFonts.html`):**

```html
<style>
@font-face{font-family:"Arial";src:url(data:font/ttf;base64,AAEAAA... ) format('truetype');}
</style>
<table>
  <tr><td>Item 1</td><td>Item 4</td><td>Item 7</td></tr>
  <tr><td>Item 2</td><td>Item 5</td><td>Item 8</td></tr>
  <tr><td>Item 3</td><td>Item 6</td><td>Item 9</td></tr>
</table>
```

Observera `@font-face`‑regeln—detta är det konkreta svaret på **embed fonts in html**.

## Steg 4 – Exportera en arbetsbok som innehåller ett OLE‑objekt till PPTX (how to export ole)

Många affärsrapporter bäddar in Word‑dokument, PDF‑filer eller andra Excel‑blad som OLE‑objekt. När du exporterar en sådan arbetsbok till PowerPoint förlorar du ofta möjligheten att redigera objektet. Aspose.Cells bevarar redigerbarheten direkt ur lådan.

```java
        // --------------------------------------------------------------
        // Step 4: Export a workbook with an OLE object to PPTX
        // --------------------------------------------------------------
        // Load a workbook that already contains an OLE object.
        Workbook oleWorkbook = new Workbook("input/oleObject.xlsx");

        String pptxPath = "output/oleEditable.pptx";
        oleWorkbook.save(pptxPath, SaveFormat.PPTX);
        System.out.println("PPTX with editable OLE object saved at: " + pptxPath);
```

**Varför detta är viktigt:**  
Om du letar efter **how to export ole**, visar detta utdrag det exakta API‑anropet. Den resulterande PowerPoint‑bilden innehåller OLE‑objektet som en levande, dubbelklick‑till‑redigera‑komponent—ingen extra efterbehandling behövs.

## Steg 5 – Använd en Smart Marker‑mall (master‑detail) och avsluta demonstrationen

Smart Markers låter dig binda en datakälla (Map, JSON, DataTable) direkt till en Excel‑mall. Här är ett minimalt exempel som skriver ut master‑detail‑rader.

```java
        // --------------------------------------------------------------
        // Step 5: Apply Smart Marker template (master‑detail)
        // --------------------------------------------------------------
        String smartMarkerTemplate = "${Orders.Master:OrderID,Customer}\n${Orders.Detail:Product,Qty,Price}";
        // Simulated data source
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        java.util.List<java.util.Map<String, Object>> master = new java.util.ArrayList<>();
        java.util.Map<String, Object> masterRow = new java.util.HashMap<>();
        masterRow.put("OrderID", 1001);
        masterRow.put("Customer", "Acme Corp");
        master.add(masterRow);
        dataSource.put("Orders.Master", master);

        java.util.List<java.util.Map<String, Object>> detail = new java.util.ArrayList<>();
        java.util.Map<String, Object> detailRow = new java.util.HashMap<>();
        detailRow.put("Product", "Widget");
        detailRow.put("Qty", 5);
        detailRow.put("Price", 9.99);
        detail.add(detailRow);
        dataSource.put("Orders.Detail", detail);

        SmartMarkerProcessor processor = new SmartMarkerProcessor(new Workbook());
        processor.apply(smartMarkerTemplate, dataSource);
        processor.getWorkbook().save("output/smartMarkerResult.xlsx");
        System.out.println("Smart Marker workbook saved.");
    }
}
```

**Vad du ser:**  
En ny arbetsbok (`smartMarkerResult.xlsx`) där mallens platshållare har ersatts med data. Detta steg handlar inte direkt om typsnitt, men det avrundar handledningen genom att visa ett typiskt rapporteringsflöde som ofta föregår en **embed fonts in html**‑export.

## Vanliga fallgropar & Pro‑tips (för att säkerställa lyckad typsnitts‑inbäddning)

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Typsnitt saknas i HTML‑filen | Arbetsboken använder ett systemtypsnitt som inte är installerat på servern. | Use `Workbook.getSettings().setDefaultFont("Arial")` before loading data, or embed the required font files manually. |
| HTML‑filen blir enorm | Inbäddning av många stora typsnitt ökar filstorleken. | Limit embedding to only the fonts you actually use: `htmlOptions.setFontEmbeddingMode(HtmlFontEmbeddingMode.EmbedSubset)`. |
| Emoji försvinner efter XPS‑konvertering | Variationsväljare tas bort som standard. | Enable `settings.setEnableFontVariationSelectors(true)` as shown in Step 2. |
| OLE‑objekt blir en statisk bild i PPTX | Källarbetsboken sparades med `setSuppressOLEObjects(true)`. | Ensure you **do not** suppress OLE objects when saving to PPTX. |

## Verifiera resultaten

1. Öppna `embeddedFonts.html` i Chrome/Firefox. Tabellen bör visas med det inbäddade typsnittet (t.ex. Arial) även om det typsnittet inte är installerat på maskinen.  
2. Öppna `withVariations.xps` i Windows XPS Viewer. Emoji såsom 👍 bör renderas korrekt.  
3. Öppna `oleEditable.pptx` i PowerPoint. Dubbelklicka på OLE‑formen;

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}