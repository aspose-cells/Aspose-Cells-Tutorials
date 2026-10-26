---
category: general
date: 2026-10-26
description: Lär dig hur du kopierar en pivottabell till en ny arbetsbok med Java,
  bevarar formatering och pivottabellens definition samtidigt som du kopierar ett
  Excel‑område med formatering via Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: sv
lastmod: 2026-10-26
og_description: Kopiera pivottabell till en ny arbetsbok i Java med Aspose.Cells.
  Den här guiden visar hur du kopierar ett Excel‑område, bevarar formatering och skapar
  en tom arbetsbok på ett effektivt sätt.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Kopiera pivottabell till en ny arbetsbok i Java – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hur man kopierar en pivottabell till en ny arbetsbok i Java
url: /sv/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så kopierar du en pivottabell till en ny arbetsbok i Java

Om du behöver **kopiera pivottabell** från en Excel‑fil till en annan, visar den här guiden en komplett, körbar lösning. Du får se hur du bevarar pivottabellens definition, behåller all formatering och undviker vanliga fallgropar när du kopierar ett Excel‑intervall.

Att kopiera en pivottabell väcker ofta frågor som *how to copy pivot* utan att bryta datakällan eller förlora stilar. I slutet av den här handledningen har du ett självständigt Java‑program som skapar en tom arbetsbok, kopierar det önskade intervallet och sparar resultatet med pivottabellen intakt.

## Vad du kommer att uppnå

* Ladda en källarbetsbok som innehåller en pivottabell.  
* **Create empty workbook** som kommer att ta emot den kopierade datan.  
* **Copy excel range** som inkluderar pivottabellen, med alternativ som behåller pivottabellen och formateringen.  
* Spara destinationsfilen och verifiera att pivottabellen fungerar exakt som originalet.

### Förutsättningar

* Java 17 eller senare.  
* Aspose.Cells för Java (version 23.10 eller nyare).  
* Grundläggande kunskap om Java‑IDE:er (IntelliJ IDEA, Eclipse osv.).

> **Pro tip:** Använd den kostnadsfria Aspose.Cells‑utvärderingslicensen för snabb testning; ersätt den med en full licens innan produktionsanvändning.

## Kopiera pivottabell till en ny arbetsbok

Det första steget är att konfigurera käll‑ och destinationsarbetsböckerna. Destinationen startar som ett **create empty workbook**‑anrop, vilket ger dig en ren fil med ett enda kalkylblad.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Varför detta fungerar

* `new Workbook()` **creates empty workbook** med ett standardsblad, vilket undviker behovet av att ta bort befintliga data.  
* `CopyOptions` instruerar Aspose.Cells att kopiera **pivot table**‑metadata, inte bara råvärden. `PASTE_ALL`‑läget för med sig cellstilar, talformat och villkorsstyrd formatering—vilket uppfyller kravet **copy range with formatting**.  
* `copyRange` utför en **copy excel range**‑operation som respekterar källans interna strukturer, så pivottabellen förblir funktionell efter kopieringen.

## Hur du kopierar pivottabell utan att förlora formatering

Om du bara använder standard‑`CopyOptions` kan viss stilinformation utelämnas i äldre Aspose.Cells‑versioner. Genom att explicit ange klistra‑in‑typen garanteras att **copy range with formatting** respekteras.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

Genom att lägga till `setPasteSpecialType` säkerställs att kolumnbredder, radhöjder och även datavalideringsregler följer med intervallet. Detta är särskilt användbart när pivottabellen sträcker sig över flera kolumner med anpassade bredder.

## Skapa tom arbetsbok innan kopiering

Ibland försöker utvecklare kopiera in i en befintlig arbetsbok som redan innehåller data. Det kan leda till överlappande intervall eller oväntade överskrivningar. Att börja med ett **create empty workbook**‑anrop isolerar operationen:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

Om du behöver mer än ett blad i destinationen kan du lägga till dem efter kopieringen:

```java
destWb.getWorksheets().add("Summary");
```

## Kopiera excel‑intervall med formatering med CopyOptions

Utöver pivottabeller fungerar samma mönster för alla **copy excel range** som kräver bevarande av formatering—diagram, tabeller eller villkorsstyrda format.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

`CopyOptions`‑instansen förblir densamma, så du får ett konsekvent beteende över olika intervall.

### Särskilda fall att beakta

| Situation                              | Recommended handling |
|----------------------------------------|----------------------|
| Källarbetsboken har flera pivottabeller   | Kopiera varje pivottabells intervall separat eller kopiera hela bladet. |
| Destinationen innehåller redan data      | Välj en icke‑konfliktande startcell (t.ex. "H1") när du anropar `copyRange`. |
| Pivottabellens datakälla är extern (t.ex. DB) | Se till att destinationsarbetsboken pekar på samma externa datakälla, eller uppdatera pivottabellen efter kopieringen. |
| Stor arbetsbok ( > 10 MB )             | Öka Java‑heap‑storleken (`-Xmx2g`) för att undvika `OutOfMemoryError`. |

## Verifiera resultatet

Efter att programmet har körts, öppna `destination.xlsx`. Du bör se:

* Samma pivottabellslayout som i `source.xlsx`.  
* Alla cellfärger, talformat och kolumnbredder bevarade.  
* Pivottabellens datakälla pekar fortfarande på det ursprungliga dataintervallet i den nya filen, så en uppdatering av pivottabellen uppdaterar värdena korrekt.

Om pivottabellen visas som en statisk tabell, dubbelkolla att `CopyOptions.setPasteType(PasteType.PASTE_ALL)` är angivet. Utan detta alternativ behandlar Aspose.Cells pivottabellen som vanlig data.

## Slutsats

Du vet nu hur du **copy pivot table** till en ny arbetsbok i Java samtidigt som du bevarar formatering, datakopplingar och bladlayout. Den kompletta lösningen demonstrerar hur man laddar en källfil, **create empty workbook**, konfigurerar **copy excel range**‑alternativ och sparar resultatet.  

Härifrån kan du utforska relaterade ämnen som **how to copy pivot** över olika kalkylblad, bädda in diagram tillsammans med pivottabeller, eller automatisera batch‑bearbetning av flera arbetsböcker. Experimentera med `CopyOptions`‑inställningarna för att passa dina specifika automatiseringsbehov, så får du ett robust verktyg för Excel‑manipulation inom räckhåll.

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa ny arbetsbok i Java – Fullständig guide för att kopiera pivottabell](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Kopiera pivottabell mellan arbetsböcker – Steg‑för‑steg Java‑guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [Hur man kopierar intervall och bevarar en pivottabell i Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}