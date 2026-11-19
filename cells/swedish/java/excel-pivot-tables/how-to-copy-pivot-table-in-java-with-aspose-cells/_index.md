---
category: general
date: 2026-11-19
description: Lär dig hur du kopierar pivottabeller i Java samtidigt som du bevarar
  deras data och layout. Denna steg‑för‑steg‑guide visar också hur du kopierar Excel‑pivottabeller
  effektivt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- how to preserve pivot
- preserve pivot table
- copy excel pivot
language: sv
lastmod: 2026-11-19
og_description: Kopiera pivottabell i Java med Aspose.Cells. Följ den här guiden för
  att lära dig hur du bevarar pivottabeller och kopierar Excel-pivotdata korrekt.
og_image_alt: Illustration of the copy pivot table workflow in Java
og_title: Kopiera pivottabell i Java – komplett Aspose.Cells‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy pivot table in Java while preserving its data and
    layout. This step‑by‑step guide also shows how to copy excel pivot tables efficiently.
  headline: How to copy pivot table in Java with Aspose.Cells
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Pivot tables
title: Hur man kopierar en pivottabell i Java med Aspose.Cells
url: /sv/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så kopierar du pivottabell i Java med Aspose.Cells

Om du behöver **kopiera pivottabell** från en arbetsbok till en annan visar den här guiden exakt hur du gör det i Java. Oavsett om du bygger en rapporteringsmotor eller migrerar data, får du se ett pålitligt sätt att bevara pivottabellens cache, fält och formatering.

Att kopiera en pivottabell kan vara knepigt eftersom en enkel områdeskopia ofta förlorar den underliggande datakällan. I den här handledningen använder vi Aspose.Cells för **hur man kopierar pivottabell** samtidigt som varje beräkning förblir intakt, och vi täcker även **hur man bevarar pivottabeller** när destinationsarboken är tom.

## Förutsättningar

Innan du börjar, se till att du har:

* Java 17 eller nyare installerat.  
* Aspose.Cells för Java (version 23.9 eller senare) tillagd i ditt projekts classpath.  
* Två Excel‑filer: en källarbok som innehåller pivottabellen och en tom destinationsarbok (eller en arbetsbok du vill slå ihop med).

Du behöver ingen speciell licens för kodexemplet, men en giltig Aspose.Cells‑licens tar bort utvärderingsvattenstämplar.

## Steg 1: Läs in källarboken som innehåller pivottabellen

Det första steget är att öppna arbetsboken som håller den ursprungliga pivottabellen. Att läsa in filen ger dig åtkomst till kalkylbladet, cellerna och pivottabellens cache.

```java
// Step 1: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Varför detta är viktigt*: Aspose.Cells läser hela arbetsboken, inklusive dold cache‑data som driver pivottabellen. Utan att läsa in hela filen skulle kopieringsoperationen förlora pivottabellens definition.

## Steg 2: Förbered destinationsarboken

Skapa en ny arbetsbok (eller öppna en befintlig) och hämta dess första kalkylblad. Här kommer pivottabellen att placeras.

```java
// Step 2: Create a new destination workbook and get its first worksheet
Workbook destWb = new Workbook();                     // empty workbook
Worksheet destWs = destWb.getWorksheets().get(0);    // first sheet
```

*Tips*: Om du redan har en målarbok, ersätt anropet `new Workbook()` med `new Workbook("target.xlsx")`. Detta låter dig **kopiera excel pivot** till en förifylld arbetsbok.

## Steg 3: Definiera cellområdet som omger pivottabellen

Du måste ange det exakta området som täcker pivottabellen. Området inkluderar pivottabellens tabell, fältlista och eventuell omgivande data du vill behålla.

```java
// Step 3: Define the cell area that covers the pivot table in the source sheet
CellArea area = CellArea.createCellArea("A1", "H30"); // adjust as needed
```

*Varför detta är viktigt*: `CellArea` talar om för Aspose.Cells vad som ska kopieras. Om området är för litet blir pivottabellen trunkerad; om det är för stort kopierar du onödig data. Justera koordinaterna baserat på din faktiska pivottabellsstorlek.

## Steg 4: Utför kopieringen med CopyOptions

Använd `copy`‑metoden på källkalkylbladets cellsamling. Att skicka ett nytt `CopyOptions()`‑objekt säkerställer att all formatering, formler och pivottabellens cache överförs.

```java
// Step 4: Copy the defined range (including the pivot table) to the destination worksheet
srcWb.getWorksheets().get(0).getCells().copy(area, destWs.getCells(), new CopyOptions());
```

### Varför `CopyOptions` bevarar pivottabellen

`CopyOptions` instruerar Aspose.Cells att behandla området som ett *helhetligt* objekt snarare än en platt mängd värden. Detta är nyckeln till **hur man bevarar pivottabeller**: den underliggande pivottabellscachen dupliceras, så destinationsarboken kan återberäkna pivottabellen utan manuell inblandning.

## Steg 5: Spara destinationsarboken

Till sist skriver du destinationsfilen till disk. Den sparade filen kommer att innehålla en fullt funktionell kopia av den ursprungliga pivottabellen.

```java
// Step 5: Save the destination workbook – the pivot table is preserved
destWb.save("YOUR_DIRECTORY/copied_with_pivot.xlsx");
```

*Förväntat resultat*: När du öppnar `copied_with_pivot.xlsx` i Excel visas en identisk pivottabell, komplett med slicers, filter och beräknade fält. Du kan uppdatera den, och datakällan pekar på det kopierade området i samma arbetsbok.

---

![Diagram som visar processen för att kopiera pivottabell](/images/copy-pivot-table-workflow.png){.align-center width=600 alt="Diagram som illustrerar arbetsflödet för att kopiera pivottabell från källarbok till destinationsarbok"}

## Så kopierar du pivottabeller över flera kalkylblad

Om du behöver **kopiera excel pivot**‑tabeller från flera blad, upprepa Steg 3‑4 för varje källkalkylblad. Du kan också loopa igenom `srcWb.getWorksheets()` och kopiera varje pivottabell till ett motsvarande blad i `destWb`. Här är ett kort exempel på en loop:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet srcWs = srcWb.getWorksheets().get(i);
    Worksheet newDestWs = destWb.getWorksheets().add();
    // Assume each pivot occupies A1:H30 – adjust per sheet if needed
    CellArea area = CellArea.createCellArea("A1", "H30");
    srcWs.getCells().copy(area, newDestWs.getCells(), new CopyOptions());
}
destWb.save("YOUR_DIRECTORY/multi_sheet_copy.xlsx");
```

*Proffstips*: Använd `srcWs.getPivotTables().getCount()` för att kontrollera om ett blad faktiskt innehåller en pivottabell innan du kopierar. Detta undviker att onödig data kopieras.

## Vanliga fallgropar och hur du undviker dem

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **Pivottabellen förlorar sin cache** | Använder `Worksheet.copy()` utan `CopyOptions` kopierar bara cellvärden. | Använd alltid `srcWs.getCells().copy(..., new CopyOptions())`. |
| **Destinationen visar #REF!-fel** | Den kopierade pivottabellen refererar fortfarande till den ursprungliga arbetsbokens externa datakälla. | Efter kopiering, anropa `destWs.getPivotTables().get(0).refresh();` för att binda om cachen till det nya området. |
| **Slicers försvinner** | Slicers lagras utanför huvudcellområdet. | Utöka `CellArea` så att den inkluderar slicer‑områden, eller kopiera hela kalkylbladet (`srcWs.copy(destWs, new CopyOptions())`). |
| **Prestanda blir långsam på stora pivottabeller** | Kopiering av stora områden med formatering kan gå trögt. | Använd `CopyOptions.setOnlyData(true)` om du inte behöver formatering, och återapplicera stilar manuellt. |

## Så bevarar du pivottabellens formatering vid uppdatering av data

Ibland behöver du **hur man bevarar pivottabell**‑layouten efter att källdata har ändrats. Efter kopieringen kan du låsa pivottabellens stil:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.setPreserveFormatting(true);   // keeps colors, fonts, and layout
pt.refresh();                     // recalculates with new data
```

Att sätta `PreserveFormatting` säkerställer att eventuella anpassade stilar du applicerat i källan överlever kopieringen.

## Verifiera kopieringen

Ett snabbt sätt att bekräfta att kopieringen lyckades är att jämföra pivottabellens definitioner:

```java
PivotTable srcPt = srcWb.getWorksheets().get(0).getPivotTables().get(0);
PivotTable destPt = destWs.getPivotTables().get(0);

System.out.println("Source fields: " + srcPt.getFields().size());
System.out.println("Destination fields: " + destPt.getFields().size());
// Both numbers should match
```

Om antalen matchar och destinationen öppnas utan fel har du framgångsrikt **kopierat pivottabell**.

## Slutsats

Du vet nu hur du **kopierar pivottabell** från en Excel‑arbok till en annan med Aspose.Cells för Java, och du har sett de exakta stegen för **hur man kopierar pivottabell** samtidigt som du säkerställer att pivottabellens cache, formatering och slicers förblir intakta. Samma mönster fungerar för **kopiera excel pivot**‑scenarier över flera blad, och du kan anpassa koden för att hantera kantfall som att bevara pivottabellens formatering eller hantera stora datamängder.

### Nästa steg

* Utforska **preserve pivot table**‑alternativ såsom `setPreserveFormatting` och `refresh` för dynamiska datakällor.  
* Prova att kopiera pivottabeller mellan arbetsböcker med olika kolumnordningar – justera `CellArea` därefter.  
* Kombinera denna teknik med Aspose.Slides för att bädda in pivottabellsnapshots i PowerPoint‑presentationer.

Lycka till med kodandet, och känn dig fri att experimentera med variationer som passar just din automationspipeline!


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [How to copy a pivot table between worksheets in Java](/cells/english/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/)
- [How to copy pivot table to a new workbook in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}