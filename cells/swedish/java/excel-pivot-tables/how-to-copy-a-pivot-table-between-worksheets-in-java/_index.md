---
category: general
date: 2026-10-16
description: Hur man kopierar pivottabell i Java med Aspose.Cells – lär dig att kopiera
  ett område till ett annat blad och kopiera område mellan kalkylblad effektivt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: sv
lastmod: 2026-10-16
og_description: Hur man kopierar pivottabell i Java med Aspose.Cells. Denna handledning
  visar hur du kopierar ett område till ett annat blad och kopierar ett område mellan
  kalkylblad med fullständig kod.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Hur man kopierar en pivottabell mellan kalkylblad i Java – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Hur man kopierar en pivottabell mellan kalkylblad i Java
url: /sv/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kopierar en pivottabell mellan kalkylblad i Java

Om du behöver **how to copy pivot table** från ett blad till ett annat i samma arbetsbok, ger den här guiden en komplett, färdig‑att‑köra lösning. Du kommer att se hur du kopierar källintervallet som innehåller pivottabellen, bevarar dess funktionalitet och verifierar resultatet — allt med Aspose.Cells för Java.

Att kopiera en pivottabell är en vanlig uppgift när du genererar rapporter programatiskt, och att göra det korrekt undviker att förlora pivottabellens cache eller bryta formler. I slutet av den här handledningen kommer du att kunna **copy range to another sheet** och **copy range between worksheets** utan några manuella steg.

## Vad du kommer att lära dig

* Läs in en befintlig Excel‑fil med en pivottabell.
* Definiera källintervallet som innehåller pivottabellen.
* Definiera ett destinationsintervall på ett annat kalkylblad.
* Använd `CopyOptions` för att behålla pivottabellen intakt.
* Verifiera att den kopierade pivottabellen fungerar som förväntat.

**Förutsättningar**

* Java 17 eller senare.
* Aspose.Cells for Java (version 23.12 eller nyare).  
* En Excel‑fil (`input.xlsx`) som innehåller en pivottabell på det första bladet.

---

## Så kopierar du en pivottabell med Aspose.Cells

Kärnan i operationen är en fyrastegsprocess: ladda arbetsboken, lokalisera källintervallet, ange destinationsintervallet och utföra kopieringen. Nedan förklaras varje steg i detalj.

### Steg 1: Ladda arbetsboken

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*Varför detta steg?*  
Laddning av arbetsboken för in hela filen i minnet, vilket ger dig tillgång till kalkylblad, celler och pivottabellens cache. Aspose.Cells läser filformatet automatiskt, så du behöver inte oroa dig för `.xls` vs `.xlsx`.

### Steg 2: Lokalisera källintervallet som innehåller pivottabellen

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Varför detta steg?*  
En pivottabell lagras i ett cellblock som också refererar till en dold cache. Genom att välja exakt intervallet (`A1:G20` i detta exempel) säkerställer du att cachen förblir länkad när intervallet kopieras.

### Steg 3: Definiera destinationsintervallet på ett annat blad

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*Varför detta steg?*  
Att välja en destination på ett annat kalkylblad låter dig **copy range to another sheet**. Den övre vänstra cellen (`A1`) är en vanlig startpunkt, men du kan placera den var som helst genom att ändra adressen.

### Steg 4: Kopiera källintervallet samtidigt som pivottabellen bevaras

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*Varför detta steg?*  
`CopyOptions` styr vad som överförs. Genom att använda `PasteType.PASTE_ALL` garanteras att pivottabellen, dess formatering och underliggande formler dupliceras. Utan dessa alternativ kan endast råvärden kopieras, vilket bryter pivottabellens funktionalitet.

### Steg 5: Spara arbetsboken och verifiera resultatet

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Öppna `output.xlsx` i Excel och bekräfta att:

* Det andra bladet innehåller en fullt funktionell pivottabell som är identisk med originalet.
* Att uppdatera pivottabellen uppdaterar datan, vilket visar att cachen är intakt.

---

## Kopiera intervall till ett annat blad med Java

Om ditt mål bara är att **copy range to another sheet** utan en pivottabell, fungerar samma kod med ett vanligt cellintervall. Den enda förändringen är källadressen. `CopyOptions`‑konfigurationen förblir densamma, vilket säkerställer att formler och formatering bevaras.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

Detta kodsnutt demonstrerar API:ets flexibilitet för både pivottabell‑ och icke‑pivotscenarier.

---

## Kopiera intervall mellan kalkylblad utan att förlora formler

När du **copy range between worksheets**, kan formler som refererar till andra blad bli brutna om de relativa referenserna ändras. För att undvika detta:

1. Använd `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` om du bara behöver formler.
2. Behåll destinationsbladet i samma arbetsbok så interna referenser förblir giltiga.
3. Efter kopiering, anropa `workbook.calculateFormula();` för att tvinga en omräkning.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

Dessa extra steg säkerställer att ett kopierat intervall beter sig exakt som originalet, även när det sträcker sig över flera kalkylblad.

---

## Pro‑tips och vanliga fallgropar

| Situation | Tip |
|-----------|-----|
| **Pivot cache uppdateras inte** | Efter kopiering, anropa `destSheet.getPivotTables().get(0).refresh();` för att uppdatera cachen. |
| **Kopiering till en annan arbetsbok** | Använd `Workbook destWorkbook = new Workbook();` och sedan `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. Kom ihåg att kopiera pivottabellens cache separat om det behövs. |
| **Stora pivottabeller** | Öka Java‑heap‑storleken (`-Xmx2g`) för att undvika `OutOfMemoryError` under kopieringen. |
| **Bevara stilar** | Ställ in `copyOptions.setPasteType(PasteType.PASTE_ALL)`; annars kopieras endast värden. |

---

## Förväntat resultat

Att köra hela programmet genererar `output.xlsx`. När den öppnas i Excel:

* **Sheet2!A1:G20** visar samma pivottabell som **Sheet1!A1:G20**.
* Pivottabellens fältlista, rad-/kolumnetiketter och datavärden matchar källan.
* Att uppdatera pivottabellen uppdaterar siffrorna, vilket bekräftar att cachen fungerar.

Konsolen kommer att skriva ut:

```
Pivot table copied successfully.
```

---

## Slutsats

I den här handledningen lärde du dig **how to copy pivot table** från ett kalkylblad till ett annat med Aspose.Cells för Java. Genom att ladda arbetsboken, välja rätt källintervall, definiera en destination och konfigurera `CopyOptions` kan du på ett pålitligt sätt **copy range to another sheet** och **copy range between worksheets** samtidigt som du bevarar all pivottabellfunktionalitet.  

Nästa kan du utforska:

* Exportera den kopierade pivottabellen till PDF eller HTML.
* Automatisera pivottabelluppdateringar över flera arbetsböcker.
* Använda `CopyOptions` för att kopiera endast specifika element (t.ex. värden, format).

Känn dig fri att experimentera med olika intervalladresser, arbetsbokstruktur eller till och med kopior över arbetsböcker. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man kopierar intervall i Java – Kopiera pivottabell med Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Hur man kopierar pivottabell i Java – Komplett Aspose.Cells‑guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Kopiera pivottabell Excel – Steg‑för‑steg‑guide med Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}