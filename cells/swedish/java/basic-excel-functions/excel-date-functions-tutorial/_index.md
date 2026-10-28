---
date: 2026-07-26
description: Lär dig hur du beräknar datumskillnad i Java med Aspose.Cells Excel-datumfunktioner.
  Inkluderar exempel på slutet av månaden, TODAY och DATEDIF.
keywords:
- calculate date difference java
- end of month java
- add excel date formula
- implement excel date functions
- retrieve current date excel
lastmod: 2026-07-26
linktitle: Beräkna datumskillnad i Java – Excel-datumfunktioner
og_description: Beräkna datumskillnad i Java med Aspose.Cells Excel-datumfunktioner.
  Denna guide visar hur du lägger till Excel-datumformler, hämtar aktuella datum och
  får slut‑på‑månaden‑värden effektivt.
og_image_alt: 'Guide: calculate date difference in Java with Aspose.Cells Excel functions'
og_title: Beräkna datumskillnad i Java – Excel-datumfunktioner
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: Learn how to calculate date difference in Java using Aspose.Cells Excel
    date functions. Includes end of month, TODAY, and DATEDIF examples.
  headline: Calculate Date Difference in Java – Excel Date Functions
  type: TechArticle
- description: Learn how to calculate date difference in Java using Aspose.Cells Excel
    date functions. Includes end of month, TODAY, and DATEDIF examples.
  name: Calculate Date Difference in Java – Excel Date Functions
  steps:
  - name: '**Download and Install Aspose.Cells:** Visit [Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
      and download the latest release.'
    text: '**Download and Install Aspose.Cells:** Visit [Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
      and download the latest release.'
  - name: '**Add the Library to Your Project:** Include the JAR file in your build
      path or add the Maven dependency.'
    text: '**Add the Library to Your Project:** Include the JAR file in your build
      path or add the Maven dependency.'
  - name: '**License Configuration:** Place your license file (`Aspose.Cells.lic`)
      in the project resources and load it at runtime to unlock full features.'
    text: '**License Configuration:** Place your license file (`Aspose.Cells.lic`)
      in the project resources and load it at runtime to unlock full features.'
  - name: '**Download the library [here](https://releases.aspose.com/cells/java/).**'
    text: '**Download the library [here](https://releases.aspose.com/cells/java/).**'
  type: HowTo
- questions:
  - answer: Create a `Style` object, set its `Number` property to `"dd-MM-yyyy"`,
      and apply it to the target cell via `cell.setStyle(style)`. **`Style` defines
      formatting such as number format, font, and alignment for a cell.**
    question: How do I format a cell to display dates in `dd‑MM‑yyyy` format?
  - answer: Yes, you can retrieve the `Date` objects from two cells, convert them
      to `java.time.LocalDate`, and use `ChronoUnit.DAYS.between(start, end)` for
      precise control.
    question: Can I calculate date differences without using the DATEDIF formula?
  - answer: Absolutely. All built‑in Excel date functions, including DATEDIF and EOMONTH,
      correctly handle leap years according to the Gregorian calendar.
    question: Does Aspose.Cells support leap‑year calculations?
  - answer: Iterate through each `Worksheet` in the `Workbook`, set the required formulas,
      and call `calculateFormula()` once per workbook for optimal performance.
    question: Is it possible to batch‑process multiple worksheets for date calculations?
  - answer: All functions are available from **Aspose.Cells 23.9** onward; the latest
      release (as of 2026) adds performance optimizations for large datasets.
    question: What version of Aspose.Cells is required for these features?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- excel date functions
- aspose cells
- java excel processing
- date calculations
- java tutorial
title: Beräkna datumskillnad i Java – Excel-datumfunktioner
url: /sv/java/basic-excel-functions/excel-date-functions-tutorial/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel-datumfunktioner handledning

I den här omfattande handledningen är **calculate date difference java** vårt huvudfokus. Vi går igenom hur du använder Aspose.Cells för Java för att arbeta med Excel-datumfunktioner, från att konstruera datum till att hämta dagens datum, beräkna skillnader och hitta månadsslut. Oavsett om du finjusterar en rapporteringsmotor eller automatiserar kalkylblad, kommer dessa tekniker att spara dig tid och minska fel. Låt oss dyka ner!

## Snabba svar
- **How do I calculate date difference in Java?** Använd DATEDIF-funktionen via Aspose.Cells och ange enheten (dagar, månader, år).  
- **How can I get today’s date in Excel from Java?** Anropa TODAY-funktionen via Aspose.Cells eller sätt ett cells värde till `new Date()`.  
- **What method returns the last day of a month?** Använd EOMONTH-funktionen; Aspose.Cells utvärderar den automatiskt.  
- **Do I need a license for Aspose.Cells?** Ja, en giltig licens tar bort utvärderingsvattenmärken och låser upp full funktionalitet.  
- **Which Java version is supported?** Aspose.Cells fungerar med Java 8 och senare.

## Vad är Excel-datumfunktioner?
Excel-datumfunktioner är inbyggda formler som skapar, manipulerar eller utvärderar datum i ett kalkylblad. De låter dig utföra aritmetik, hämta det aktuella datumet eller beräkna månadens gränser utan manuella beräkningar. Genom att använda dessa funktioner kan du lägga till eller subtrahera dagar, månader eller år, bestämma antalet dagar mellan två datum och automatiskt justera för skottår och varierande månadslängder, allt medan datan hålls i ett format som Excel förstår och kan visa enligt regionala inställningar.

## Varför använda Aspose.Cells för Java för att implementera Excel-datumfunktioner?
Aspose.Cells stöder **50+** in‑ och utdataformat, bearbetar kalkylblad med **upp till 1 000 sidor** utan att ladda hela filen i minnet, och utför formelberäkningar med **upp till 3×** snabbare hastighet än inbyggd Excel på samma hårdvara. Denna prestandaförbättring är avgörande för storskaliga datapipelines.

## Förstå datumfunktioner i Excel

Excel erbjuder ett rikt utbud av datumfunktioner som förenklar komplexa beräkningar. Nedan markerar vi de vanligaste och visar hur Aspose.Cells utvärderar dem automatiskt.

### DATE-funktionen
`DATE`‑funktionen skapar ett datumvärde från år-, månad- och dagkomponenter.  
**Direkt svar:** `=DATE(2023, 12, 31)` returnerar serienumret för 31 december 2023, vilket Excel formaterar som ett datum. I Java kan du sätta en cells formel till denna sträng och Aspose.Cells beräknar rätt datum när arbetsboken sparas eller räknas om.

### TODAY-funktionen
`TODAY`‑funktionen returnerar det aktuella systemdatumet utan tidskomponenten.  
**Direkt svar:** `=TODAY()` speglar alltid dagen arbetsboken öppnas eller räknas om, vilket gör den idealisk för dynamiska rapporter.

### DATEDIF-funktionen
`DATEDIF`‑funktionen beräknar skillnaden mellan två datum i dagar, månader eller år.  
**Direkt svar:** `=DATEDIF(A1, B1, "d")` ger antalet dagar mellan datumen i cellerna A1 och B1. Detta är kärnan i vårt **calculate date difference java**‑scenario.

### EOMONTH-funktionen
`EOMONTH`‑funktionen returnerar den sista dagen i månaden för ett givet startdatum, förskjuten med ett angivet antal månader.  
**Direkt svar:** `=EOMONTH(A1, 0)` ger den sista kalenderdagen i den månad som innehåller datumet i A1.

## Arbeta med Aspose.Cells för Java

Nu när vi har gått igenom grunderna, låt oss se hur man konfigurerar Aspose.Cells och använder dessa funktioner programatiskt.

### Konfigurera Aspose.Cells

Innan du kodar, se till att din miljö är klar:

1. **Download and Install Aspose.Cells:** Besök [Aspose.Cells for Java](https://releases.aspose.com/cells/java/) och ladda ner den senaste versionen.  
2. **Add the Library to Your Project:** Inkludera JAR‑filen i din byggsökväg eller lägg till Maven‑beroendet.  
3. **License Configuration:** Placera din licensfil (`Aspose.Cells.lic`) i projektresurserna och ladda den vid körning för att låsa upp alla funktioner.  
4. **Download the library [here](https://releases.aspose.com/cells/java/).**  

### Hur beräknar man datumskillnad i Java med Aspose.Cells?

`Workbook` representerar en hel Excel‑fil i minnet, innehållande arbetsblad, celler och stilar.  
Läs in din arbetsbok, sätt DATEDIF‑formeln och utvärdera den.  
**Direkt svar:** Skapa en `Workbook`, tilldela `=DATEDIF(A2,B2,"d")` till en cell, anropa `calculateFormula()`, och läs sedan det resulterande numeriska värdet. Detta ger det exakta antalet dagar mellan två datum i ett enda API‑anrop.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set the date using the DATE function
worksheet.getCells().get("A1").putValue("=DATE(2023, 9, 7)");

// Get the calculated date value
String calculatedDate = worksheet.getCells().get("A1").getStringValue();

// Print the result
System.out.println("Calculated Date: " + calculatedDate);
```

### Använda DATE-funktionen med Aspose.Cells

Du kan bädda in `DATE`‑formeln direkt i en cell för att konstruera datum från separata år-, månad- och dagvärden.

**Direkt svar:** Sätt en cells formel till `=DATE(2024, 5, 15)`; efter att ha anropat `calculateFormula()` visar cellen `15‑May‑2024` enligt arbetsbokens lokala inställning.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Use the TODAY function to get the current date
worksheet.getCells().get("A1").setFormula("=TODAY()");

// Get the current date value
String currentDate = worksheet.getCells().get("A1").getStringValue();

// Print the result
System.out.println("Current Date: " + currentDate);
```

### Arbeta med TODAY-funktionen

Att hämta det aktuella datumet programatiskt är enkelt.

**Direkt svar:** Tilldela `=TODAY()` till en cell, anropa `calculateFormula()`, och cellen kommer att innehålla dagens datum varje gång arbetsboken öppnas eller räknas om.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set two date values
worksheet.getCells().get("A1").putValue("2023-09-07");
worksheet.getCells().get("A2").putValue("2023-08-01");

// Calculate the difference using DATEDIF
worksheet.getCells().get("A3").setFormula("=DATEDIF(A1, A2, \"d\")");

// Get the difference in days
int daysDifference = worksheet.getCells().get("A3").getIntValue();

// Print the result
System.out.println("Days Difference: " + daysDifference);
```

### Beräkna datumskillnader med DATEDIF

För den centrala **calculate date difference java**‑uppgiften, använd DATEDIF.

**Direkt svar:** Placera `=DATEDIF(C2,D2,"m")` i en cell för att få månadsdifferensen, eller ersätt `"m"` med `"y"` eller `"d"` för år respektive dagar. Efter beräkning, läs det numeriska resultatet via `cell.getIntValue()`.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set a date value
worksheet.getCells().get("A1").putValue("2023-09-07");

// Calculate the end of the month using EOMONTH
worksheet.getCells().get("A2").setFormula("=EOMONTH(A1, 0)");

// Get the end-of-month date
String endOfMonth = worksheet.getCells().get("A2").getStringValue();

// Print the result
System.out.println("End of Month: " + endOfMonth);
```

### Hitta månadens slut

EOMONTH‑funktionen hjälper dig att hitta månadsslutsdatum för faktureringscykler eller rapporteringsperioder.

**Direkt svar:** Sätt en cells formel till `=EOMONTH(E2,0)`; efter formelutvärdering innehåller cellen den sista dagen i månaden för datumet i E2.

## Vanliga fallgropar och tips
- **Formula Re‑calculation:** Anropa alltid `workbook.calculateFormula()` efter att ha satt eller ändrat formler; annars behåller cellerna gamla värden.  
- **Date Serial Numbers:** Excel lagrar datum som serienummer; när du läser värden, använd `cell.getDateValue()` för att få ett `java.util.Date`‑objekt.  
- **Locale Issues:** Datumformatering följer arbetsbokens lokala inställning. Ställ explicit in stilen om du behöver ett specifikt visningsformat.  
- **Large Workbooks:** För filer med **hundratusentals rader**, aktivera `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` för att hålla minnesanvändningen låg.  
- **`WorkbookSettings` configures memory and calculation options for a `Workbook`.**  

## Vanliga frågor

**Q: Hur formaterar jag en cell för att visa datum i formatet `dd‑MM‑yyyy`?**  
A: Skapa ett `Style`‑objekt, sätt dess `Number`‑egenskap till `"dd-MM-yyyy"`, och applicera det på målcell via `cell.setStyle(style)`.  
**`Style` defines formatting such as number format, font, and alignment for a cell.**

**Q: Kan jag beräkna datumskillnader utan att använda DATEDIF‑formeln?**  
A: Ja, du kan hämta `Date`‑objekten från två celler, konvertera dem till `java.time.LocalDate`, och använda `ChronoUnit.DAYS.between(start, end)` för exakt kontroll.

**Q: Stöder Aspose.Cells skottårsberäkningar?**  
A: Absolut. Alla inbyggda Excel-datumfunktioner, inklusive DATEDIF och EOMONTH, hanterar korrekt skottår enligt den gregorianska kalendern.

**Q: Är det möjligt att batch‑processa flera arbetsblad för datumberäkningar?**  
A: Iterera genom varje `Worksheet` i `Workbook`, sätt de nödvändiga formlerna, och anropa `calculateFormula()` en gång per arbetsbok för optimal prestanda.

**Q: Vilken version av Aspose.Cells krävs för dessa funktioner?**  
A: Alla funktioner finns tillgängliga från **Aspose.Cells 23.9** och framåt; den senaste releasen (2026) lägger till prestandaoptimeringar för stora datamängder.

## Slutsats

Denna handledning har gett dig en djupgående genomgång av Excel-datumfunktioner och visat hur du **calculate date difference java** med Aspose.Cells för Java. Du vet nu hur du konfigurerar biblioteket, använder DATE-, TODAY-, DATEDIF- och EOMONTH‑formler, samt hanterar vanliga utmaningar som lokalanpassning och storskalig bearbetning. Inkludera dessa mönster i dina Java‑applikationer för att automatisera datumdriven rapportering och analys med förtroende.

---

**Senast uppdaterad:** 2026-07-26  
**Testad med:** Aspose.Cells 24.11 for Java  
**Författare:** Aspose  
**Relaterade resurser:** API Reference [här](https://reference.aspose.com/cells/java/) | Download Free Trial [här](https://releases.aspose.com/cells/java/)

{{< blocks/products/products-backtop-button >}}

## Relaterade handledningar

- [Behärska 1904-datersystemet i Excel med Aspose.Cells Java för effektiva celloperationer](/cells/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Behärska datavisualisering i Excel: Nummer- och anpassad datumformatering med Aspose.Cells för Java](/cells/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Excel-formler och funktioner handledningar för Aspose.Cells Java](/cells/java/formulas-functions/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

```java
// Create a date style
Style dateStyle = workbook.createStyle();
dateStyle.setCustom("dd-MM-yyyy");

// Apply the style to a cell
worksheet.getCells().get("A1").setStyle(dateStyle);
```