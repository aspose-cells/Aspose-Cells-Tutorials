---
category: general
date: 2026-11-22
description: Lär dig hur du exporterar Excel som text och skapar en flikavgränsad
  fil. Den här guiden visar hur du ställer in att citera alla fält och sparar kalkylblads­text
  effektivt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as text
- quote all fields
- create tab-delimited file
- save spreadsheet text
- export spreadsheet tab-delimited
language: sv
lastmod: 2026-11-22
og_description: Exportera Excel som text och skapa en tabbavgränsad fil. Följ den
  här steg‑för‑steg‑handledningen för att citera alla fält och spara kalkylblads­text
  med Java.
og_image_alt: Screenshot showing Java code that exports an Excel workbook as a tab‑delimited
  text file
og_title: Exportera Excel som text – guide för tabbavgränsad fil
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  headline: How to export Excel as text with tab‑delimited output
  type: TechArticle
- description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  name: How to export Excel as text with tab‑delimited output
  steps:
  - name: Prepare the workbook and sample data
    text: Creating a workbook gives you something to export. In a real project you
      would load an existing file with `new Workbook("input.xlsx")`; here we generate
      a tiny sheet so the example runs out‑of‑the‑box.
  - name: Configure export options – delimiter, quoting, and output mode
    text: The core of **export spreadsheet tab‑delimited** lies in `ExportTableOptions`.
      You set the delimiter to a tab (`'\t'`) and enable `setQuoteAllFields(true)`
      so every cell is wrapped in double quotes. This eliminates ambiguity when a
      cell itself contains a tab or newline.
  - name: Save the workbook as a tab‑delimited text file
    text: Now you actually **export excel as text**. The `save` method takes the target
      path and the `ExportOptions` you configured.
  type: HowTo
tags:
- export excel as text
- quote all fields
- tab-delimited file
- spreadsheet export
- Java
title: Hur man exporterar Excel som text med tabbavgränsad utskrift
url: /sv/java/excel-import-export/how-to-export-excel-as-text-with-tab-delimited-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man exporterar Excel som text med tab‑avgränsad output

Om du behöver **exportera Excel som text**, går den här handledningen igenom hela processen för att skapa en tab‑avgränsad fil från en arbetsbok. Oavsett om du bygger en data‑migrationspipeline eller bara behöver en snabb CSV‑liknande dump för efterföljande bearbetning, låter stegen nedan dig **spara kalkylblads‑text** med full kontroll över avgränsare och citattecken.

Att exportera kalkylbladsdata som ren text är ofta mer portabelt än att behålla det inhemska `.xlsx`‑formatet. I den här guiden lär du dig också hur du **citerar alla fält**, vilket garanterar att värden som innehåller tabbar, kommatecken eller radbrytningar blir säkert inkapslade.

## Vad du behöver

Innan du börjar, se till att du har:

* Java 17 eller senare installerat.  
* Aspose.Cells for Java‑biblioteket (koden använder `ExportOptions` och `ExportTableOptions` från detta bibliotek). Du kan lägga till det via Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* En IDE eller en enkel textredigerare för att kompilera och köra Java‑programmet.

## Exportera Excel som text – steg‑för‑steg

Följande avsnitt delar upp uppgiften i tre logiska steg. Varje steg förklarar **varför** det är viktigt, inte bara **vad** du ska skriva.

### Steg 1: Förbered arbetsboken och exempeldata

Att skapa en arbetsbok ger dig något att exportera. I ett riktigt projekt skulle du ladda en befintlig fil med `new Workbook("input.xlsx")`; här genererar vi ett litet blad så att exemplet kan köras direkt.

```java
import com.aspose.cells.*;

public class ExportExcelAsText {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook or create a new one
        Workbook wb = new Workbook();
        Worksheet sheet = wb.getWorksheets().get(0);

        // Populate sample data – this will be part of the exported text
        sheet.getCells().get("A1").setValue("Name");
        sheet.getCells().get("B1").setValue("Age");
        sheet.getCells().get("A2").setValue("Alice");
        sheet.getCells().get("B2").setValue(30);
        sheet.getCells().get("A3").setValue("Bob, Jr."); // contains a comma
        sheet.getCells().get("B3").setValue(25);
```

*Varför detta steg?*  
En arbetsbok är källobjektet för alla exportoperationer. Genom att lägga till några rader kan du verifiera att **citering av alla fält** verkligen skyddar kommatecken och andra specialtecken.

### Steg 2: Konfigurera exportalternativ – avgränsare, citattecken och utskriftsläge

Kärnan i **exportera kalkylblad tab‑avgränsat** ligger i `ExportTableOptions`. Du sätter avgränsaren till en tabb (`'\t'`) och aktiverar `setQuoteAllFields(true)` så att varje cell omsluts av dubbla citattecken. Detta eliminerar tvetydighet när en cell själv innehåller en tabb eller radbrytning.

```java
        // Step 2: Create table export options and configure delimiter and quoting
        ExportTableOptions tableExportOptions = new ExportTableOptions();
        tableExportOptions.setDelimiter('\t');            // Use a tab as the field separator
        tableExportOptions.setQuoteAllFields(true);      // Quote every field for safety

        // Create overall export options and attach the table options
        ExportOptions exportOptions = new ExportOptions();
        exportOptions.setExportTableOptions(tableExportOptions);
        exportOptions.setExportAsString(true);            // Produce plain‑text output
```

*Varför detta steg?*  
- **Avgränsare** bestämmer hur kolumner separeras. En tabb (`\t`) skapar en **tab‑avgränsad fil** som många data‑bearbetningsverktyg accepterar.  
- **Citering av alla fält** garanterar att även om en cell innehåller en avgränsare, förblir den resulterande texten parsbar.  
- Att sätta `ExportAsString` får Aspose.Cells att generera en sträng snarare än en binär arbetsbok, vilket är exakt vad du behöver för **spara kalkylblads‑text**.

### Steg 3: Spara arbetsboken som en tab‑avgränsad textfil

Nu exporterar du faktiskt **excel som text**. `save`‑metoden tar målsökvägen och de `ExportOptions` du konfigurerat.

```java
        // Step 3: Save the workbook as a tab‑delimited text file
        wb.save("output/table.txt", exportOptions);
    }
}
```

När programmet är klart hittar du `output/table.txt` som innehåller:

```
"Name"	"Age"
"Alice"	"30"
"Bob, Jr."	"25"
```

*Varför detta steg?*  
`save`‑anropet skriver **tab‑avgränsad fil** till disk, vilket i praktiken **sparar kalkylblads‑text** i ett format som kan öppnas av Excel, Notepad eller vilket data‑importverktyg som helst som förstår tabbar.

## Hur man citerar alla fält vid export av Excel som text

Om du utelämnar `setQuoteAllFields(true)` kommer celler som innehåller tabbar, kommatecken eller radbrytningar att förstöra strukturen i utdatafilen. Till exempel skulle raden `Bob, Jr.` delas upp i två kolumner och korrupta datasetet. Aktivera alltid citering när:

* Din källdata kan innehålla kommatecken, tabbar eller radbrytningar.  
* Nedströms‑parsern förväntar sig citerade CSV/TSV‑filer.  
* Du behöver en deterministisk export oavsett cellinnehåll.

## Skapa en tab‑avgränsad fil utan Aspose.Cells (valfritt)

Om du föredrar en ren‑Java‑lösning utan tredjepartsbibliotek kan du iterera över rader och skriva dem manuellt:

```java
try (PrintWriter pw = new PrintWriter(new FileWriter("output/manual.txt"))) {
    for (int r = 0; r < sheet.getCells().getMaxDataRow() + 1; r++) {
        List<String> rowValues = new ArrayList<>();
        for (int c = 0; c < sheet.getCells().getMaxDataColumn() + 1; c++) {
            String value = sheet.getCells().get(r, c).getStringValue();
            // Quote all fields manually
            rowValues.add('"' + value.replace("\"", "\"\"") + '"');
        }
        pw.println(String.join("\t", rowValues));
    }
}
```

Detta kodsnutt demonstrerar samma **exportera kalkylblad tab‑avgränsat**‑logik: en tabb‑avgränsare, citat för varje fält och skrivning av resultatet som ren text. Att använda Aspose.Cells förenklar dock hanteringen av stora arbetsböcker, bevarar formatering och minskar boilerplate‑kod.

## Vanliga fallgropar och pro‑tips

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **Saknade tabbar i utdata** | Avgränsaren är kvar på standardkomma. | Anropa explicit `setDelimiter('\t')`. |
| **Ociterade kommatecken bryter kolumner** | `quoteAllFields` är inte aktiverat. | Använd `setQuoteAllFields(true)` eller citera manuellt. |
| **Filen skapas inte** | Utdatamappen finns inte. | Se till att `output/`‑mappen finns eller använd `Files.createDirectories`. |
| **Kodningsproblem** | Standardplattformens kodning kan förstöra icke‑ASCII‑tecken. | Skicka `ExportOptions.setEncoding(Encoding.getUTF8())` om det behövs. |

## Testa resultatet

Efter att programmet har körts:

1. Öppna `output/table.txt` i en vanlig textredigerare. Du bör se varje värde omslutet av dubbla citattecken och kolumner separerade av ett enda tabbtecken.  
2. Importera filen i Excel (`Data → From Text/CSV`). Välj **Tab** som avgränsare; Excel placerar korrekt varje citerat värde i sin egen cell.  
3. Verifiera att specialtecken (kommatecken, radbrytningar osv.) har bevarats.

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [hur man exporterar excel – guide för tab‑avgränsad text](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/)
- [Spara Excel som textfil med anpassad separator med Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Hur man sparar Excel som text med Aspose.Cells – steg‑för‑steg guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}