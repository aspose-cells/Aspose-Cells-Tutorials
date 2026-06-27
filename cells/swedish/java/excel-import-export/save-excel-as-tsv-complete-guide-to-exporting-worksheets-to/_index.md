---
category: general
date: 2026-06-27
description: Spara Excel som TSV snabbt med Java. Lär dig hur du exporterar ett kalkylblad
  till text, exporterar bladet som ren text och exporterar Excel‑datasträng med Aspose.Cells.
draft: false
keywords:
- save excel as tsv
- export worksheet to text
- export sheet plain text
- export excel data string
language: sv
og_description: Spara Excel som TSV med Java. Den här handledningen visar hur du exporterar
  kalkylblad till text, exporterar blad som ren text och exporterar Excel-data som
  sträng på ett effektivt sätt.
og_title: Spara Excel som TSV – Steg‑för‑steg exportguide
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
title: Spara Excel som TSV – Komplett guide för att exportera kalkylblad till text
url: /sv/java/excel-import-export/save-excel-as-tsv-complete-guide-to-exporting-worksheets-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spara Excel som TSV – Komplett guide för att exportera kalkylblad till text

Har du någonsin behövt **spara Excel som TSV** men varit osäker på vilken API‑anrop du ska använda? Du är inte ensam. Många utvecklare fastnar när de försöker omvandla ett kalkylblad till en tab‑separerad fil för vidare bearbetning. Den goda nyheten? Med några rader Java och Aspose.Cells kan du exportera ett kalkylblad till text, exportera bladets rena text och till och med exportera Excel‑datat som en sträng utan att svettas.

I den här handledningen går vi igenom hela arbetsflödet – från att ladda en arbetsbok till att konfigurera exportalternativ och slutligen skriva en TSV‑fil till disk. När du är klar kommer du kunna **spara Excel som TSV** i vilket Java‑projekt som helst, oavsett om du hanterar ett enda blad eller batchar dussintals filer.

## Vad den här guiden täcker

* Laddar en Excel‑arbetsbok från disk  
* Väljer rätt kalkylblad (eller loopar över många)  
* Konfigurerar `ExportTableOptions` för att producera ren‑text‑utdata  
* Skriver data som en tab‑separerad värdefil (TSV)  
* Tips för att hantera stora områden, olika avgränsare och Unicode‑tecken  

Inga externa verktyg behövs – bara Aspose.Cells för Java och en Java 8+‑runtime.

---

## Steg 1: Ställ in ditt projekt och ladda arbetsboken

Innan vi dyker in i koden, se till att du har lagt till Aspose.Cells‑JAR‑filen i ditt projekts classpath. Om du använder Maven ser beroendet ut så här:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Nu kan vi ladda arbetsboken:

```java
// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – print the number of worksheets
System.out.println("Worksheets count: " + workbook.getWorksheets().getCount());
```

> **Varför detta är viktigt:** Att ladda filen är första steget i alla **export Excel data string**‑arbetsflöden. Om filen inte kan öppnas fungerar inget annat.

### Pro‑tips
Om du arbetar med lösenordsskyddade filer, anropa `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.

---

## Steg 2: Välj kalkylbladet du vill exportera

Du kan hämta det första bladet, ett blad efter namn, eller iterera över alla. Här är det enklaste fallet – att exportera det första kalkylbladet:

```java
// Step 2: Access the first worksheet (or any specific sheet)
Worksheet ws = workbook.getWorksheets().get(0);
System.out.println("Exporting sheet: " + ws.getName());
```

Om du behöver **export worksheet to text** för varje blad, omslut koden ovan med en `for`‑loop:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    // Export each sheet separately...
}
```

---

## Steg 3: Skapa och konfigurera exportalternativ

Kärnan i **export sheet plain text** ligger i `ExportTableOptions`. Genom att växla några egenskaper gör vi området till en ren‑text‑sträng med tab‑avgränsare:

```java
// Step 3: Create export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();

// Step 4: Configure the options – export as plain text and use a tab delimiter
exportOptions.setExportAsString(true);   // Returns a string instead of binary Excel format
exportOptions.setDelimiter('\t');        // Tab character makes it TSV
```

> **Varför använda `setExportAsString(true)`?**  
> Det får Aspose.Cells att behandla utdata som rå text, vilket är exakt vad du behöver när du vill **spara Excel som TSV**. Alternativet skulle vara CSV eller HTML‑export, vilket inte ger dig ren tab‑separering.

### Edge case: Anpassade avgränsare
Om ditt downstream‑system förväntar sig ett pipe‑tecken (`|`) istället för en tab, ändra bara avgränsaren:

```java
exportOptions.setDelimiter('|');
```

---

## Steg 4: Exportera det önskade området till en textfil

Nu skriver vi faktiskt TSV‑filen. Metoden `exportTable` tar tre argument: cellområdet, sökvägen för utdata och de `ExportTableOptions` vi just konfigurerat.

```java
// Step 5: Export the range A1:D20 to a text file using the configured options
ws.getCells().exportTable("A1:D20", "YOUR_DIRECTORY/out.tsv", exportOptions);
System.out.println("TSV file created successfully!");
```

Om du vill exportera hela det använda området, ersätt `"A1:D20"` med `ws.getCells().getMaxDisplayRange()`:

```java
String fullRange = ws.getCells().getMaxDisplayRange();
ws.getCells().exportTable(fullRange, "out.tsv", exportOptions);
```

### Pro‑tips
Efter export kan du även fånga strängen direkt:

```java
String tsvContent = ws.getCells().exportTable("A1:D20", exportOptions);
System.out.println(tsvContent); // Handy for debugging or sending over a network
```

Det ger dig den råa **export Excel data string** utan att röra filsystemet.

---

## Steg 5: Hantera stora filer och prestandatips

När du arbetar med massiva kalkylblad (hundratusentals rader), överväg dessa optimeringar:

| Problem | Lösning |
|---------|----------|
| Minnesbelastning | Använd `WorkbookFactory.create(InputStream)` för att strömma filen istället för att ladda den helt. |
| Långsam I/O | Skriv till en `BufferedWriter` eller använd NIO `Files.newBufferedWriter`. |
| Unicode‑tecken | Säkerställ att utdatafilen skrivs med UTF‑8: `exportTable(..., "out.tsv", exportOptions, Encoding.getUTF8())`. |

Nedan är ett kodsnutt som kombinerar streaming och UTF‑8‑kodning:

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

## Vanliga fallgropar och hur du undviker dem

1. **Glömt att sätta `setExportAsString(true)`.**  
   Utan denna flagga genererar Aspose en binär Excel‑fil, vilket förstör ditt mål att **export worksheet to text**.

2. **Använder fel avgränsare.**  
   Ett kommatecken istället för en tab ger dig CSV, inte TSV. Dubbelkolla `setDelimiter('\t')`.

3. **Felaktig områdessyntax.**  
   `"A1:D20"` fungerar, men `"A1:D20:"` (extra kolon) kastar ett `IllegalArgumentException`.  

4. **Filbehörigheter.**  
   Se till att mål‑katalogen är skrivbar. På Linux löser ofta `chmod 755` problemet.

---

## Sammanfattning – komplett fungerande exempel

Här är det fullständiga, färdiga programmet som demonstrerar **spara Excel som TSV** från början till slut:

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

När du kör detta program får du en tab‑separerad fil (`out.tsv`) som vilket downstream‑system som helst – vare sig det är en databasinläsare, ett Unix‑`awk`‑script eller en enkel kalkylbladsvisare – kan konsumera.

---

## Slutsats

Vi har gått igenom allt du behöver för att **spara Excel som TSV** med Java och Aspose.Cells. Från att ladda arbetsboken, välja rätt blad, konfigurera `ExportTableOptions` och slutligen skriva filen, har du nu ett robust, produktionsklart mönster för **export worksheet to text**, **export sheet plain text** och **export Excel data string**‑scenarier.

Vad blir nästa steg? Prova att exportera flera områden, byta avgränsare i farten, eller strömma utdata direkt till ett HTTP‑svar för webbaserade nedladdningar. Samma principer gäller, och du kommer upptäcka att hantera Excel‑data i ren text är en barnlek när grunderna är på plats.

Har du frågor eller stöter på en knasig edge case? lämna en kommentar nedan, och lycka till med kodandet!


## Vad bör du lära dig härnäst?


Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Export Excel Data to HTML5 Using Aspose.Cells Java](/cells/english/java/import-export/aspose-cells-java-export-excel-html5/)
- [Effortless Data Export from Excel using Aspose.Cells for Java](/cells/english/java/import-export/aspose-cells-java-excel-data-export/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}