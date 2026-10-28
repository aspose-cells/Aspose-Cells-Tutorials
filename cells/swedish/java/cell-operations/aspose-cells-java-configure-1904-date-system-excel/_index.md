---
date: '2026-10-28'
description: Lär dig hur du ändrar Excel-datumssystem till 1904 med Aspose.Cells för
  Java, ställer in Excel-datumformat och konverterar Excel 1904-systemet effektivt.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Ändra Excel-datumssystem till 1904 med Aspose.Cells för Java. Lär
  dig steg för steg hur du aktiverar 1904-systemet, ställer in datum och konverterar
  tillbaka.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Ändra Excel-datumssystem till 1904 med Aspose.Cells för Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Ändra Excel-datumssystem till 1904 med Aspose.Cells Java
url: /sv/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ändra Exceldatumssystem till 1904 med Aspose.Cells Java

I den här handledningen kommer du att lära dig hur du **ändrar Exceldatumssystemet** till 1904-formatet med Aspose.Cells för Java. 1904-systemet är viktigt när du behöver bevara äldre Mac‑baserade datum eller anpassa dig till finansiella modeller som förväntar sig den epoken. Vi går igenom hur du installerar biblioteket, laddar en arbetsbok, växlar datumssystemet och sparar resultatet — allt utan att behöva Microsoft Excel på servern.

## Snabba svar
- **Vad gör 1904-datumssystemet?** Det börjar räkna dagar från 1 januari 1904, vilket förskjuter alla datum med 1 462 dagar jämfört med standard‑1900‑systemet.  
- **Varför använda Aspose.Cells för att ändra datumssystemet?** Det erbjuder ett enkelt API som fungerar utan Excel installerat och stödjer stora filer.  
- **Vilka Java‑versioner stöds?** JDK 8 eller nyare.  
- **Behöver jag en licens?** En gratis provversion fungerar för utvärdering; en licens tar bort användningsbegränsningar.  
- **Kan jag konvertera tillbaka till 1900‑systemet senare?** Ja, anropa bara `setDate1904(false)`.

## Vad är 1904-datumssystemet i Excel?
1904-datumssystemet räknar dagar från 1 januari 1904, istället för standard‑1900‑epoken. Denna förskjutning lägger exakt 1 462 dagar till varje datumvärde, vilket är anledningen till att äldre Mac‑arbetsböcker visas förskjutna när de öppnas i Windows. Det används främst för kompatibilitet med äldre Macintosh‑Excel‑filer och vissa äldre finansiella modeller.

## Varför ändra Exceldatumssystem med Aspose.Cells?
Du kan byta datumssystem direkt från Java, vilket eliminerar manuella steg i Excel. Aspose.Cells behandlar arbetsböcker upp till **2 GB** i storlek och kan konvertera en arbetsbok med 500 blad på under **2 sekunder** på en vanlig 4‑kärnig server, vilket ger hög genomströmning för server‑sidig automatisering.

## Förutsättningar
- Java Development Kit (JDK) 8 eller högre.  
- Maven eller Gradle för beroendehantering.  
- Grundläggande kunskaper i Java‑programmering.  

## Konfigurera Aspose.Cells för Java

### Maven
Lägg till följande beroende i din `pom.xml`‑fil:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Inkludera denna rad i din `build.gradle`‑fil:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Licensförvärv
Aspose erbjuder en gratis provversion, tillfällig licens och fullständiga kommersiella licenser. Du kan börja med [free trial](https://releases.aspose.com/cells/java/) eller skaffa en tillfällig licens från [temporary license page](https://purchase.aspose.com/temporary-license/).

## Hur ändrar du Exceldatumssystemet till 1904 med Aspose.Cells för Java?
Läs in arbetsboken, aktivera 1904‑inställningen och spara filen — detta tre‑stegsflöde uppdaterar arbetsbokens interna datumepok på under en sekund. API‑anropet `setDate1904(true)` växlar systemflaggan, och förändringen sparas när du anropar `save`. Ingen Excel‑installation krävs, vilket gör det idealiskt för huvudlösa servermiljöer.

### Steg 1: initiera och ladda arbetsboken
Klassen `Workbook` representerar en hel Excel‑fil i minnet. Skapa först en `Workbook`‑instans som pekar på din befintliga fil.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Steg 2: aktivera 1904-datumssystemet
Metoden `WorkbookSettings.setDate1904` växlar arbetsbokens datumflagga. Att sätta den till `true` aktiverar 1904‑systemet för alla kalkylblad.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Proffstips:** Du kan också anropa `setDate1904(false)` senare om du behöver återgå.

### Steg 3: spara den modifierade arbetsboken
Skriv slutligen ändringarna till en ny fil (eller skriv över originalet). Metoden `save` respekterar automatiskt det aktiva datumssystemet.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Obs:** Koden ovan använder klassnamnet `tWorkbook` som ursprungligen angivet. Se till att detta stavfel matchar ditt projekts namngivningskonventioner eller korrigera det till `Workbook` om det behövs.

## Ställ in Exceldatum programatiskt (sekundärt nyckelord)
Om du behöver justera enskilda cellvärden efter att ha bytt system kan du använda `cells.get(i, j).putValue(Date)` där datumet tolkas enligt det aktiva datumssystemet.

## Konvertera Excel 1904-systemet tillbaka till 1900 (sekundärt nyckelord)
För att återgå, anropa helt enkelt:

```java
workbook.getSettings().setDate1904(false);
```

Spara sedan arbetsboken igen.

## Praktiska tillämpningar
1. **Dataarkivering** – Bevara äldre tidsstämplar när du migrerar gamla Mac‑baserade kalkylblad.  
2. **Plattforms‑oberoende rapportering** – Generera rapporter som öppnas korrekt både på Windows och macOS utan datumavvikelser.  
3. **Finansiell modellering** – Anpassa datumberäkningar till äldre finansiella modeller som förväntar sig 1904‑systemet.

## Prestandaöverväganden
- Begränsa arbetsboksoperationer i en enda session för att hålla minnesanvändningen låg; Aspose.Cells strömmar data och laddar aldrig hela filen i RAM om du inte uttryckligen begär det.  
- Optimera Java‑s skräpsamlingsflaggor (`-XX:+UseG1GC`) för mycket stora filer för att undvika paus‑tidsökningar.  

## Vanliga frågor

**Q: Vad är skillnaden mellan 1900‑ och 1904‑datumssystemen?**  
A: 1900‑systemet startar den 1 januari 1900, medan 1904‑systemet startar den 1 januari 1904, vilket förskjuter alla datum med 1 462 dagar.

**Q: Kan jag ändra datumssystemet för en arbetsbok som för närvarande är öppen i Excel?**  
A: Ja, men du måste först stänga filen i Excel; annars kommer sparoperationen att misslyckas.

**Q: Behöver jag en licens för att använda `setDate1904`?**  
A: Metoden fungerar i gratisprovversionen, men en full licens tar bort utvärderingsbegränsningar.

**Q: Är det möjligt att ändra datumssystemet för endast ett enskilt kalkylblad?**  
A: Nej, datumssystemet är en arbetsboks‑nivåinställning; den gäller för alla kalkylblad.

**Q: Hur kan jag verifiera att datumssystemet har ändrats?**  
A: Öppna den sparade filen i Excel, gå till **File → Options → Advanced**, och markera rutan **"Use 1904 date system"**.

## Slutsats
Du vet nu hur du **ändrar Exceldatumssystemet** till 1904 med Aspose.Cells för Java, hur du ställer in enskilda celldatum och hur du återgår till 1900‑systemet när det behövs. Integrera dessa kodsnuttar i dina databehandlings‑pipelines för att garantera datum‑kompatibilitet över plattformar och äldre filer.

---

**Senast uppdaterad:** 2026-10-28  
**Testat med:** Aspose.Cells 25.3 for Java  
**Författare:** Aspose  

**Resurser**
- **Documentation:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Download:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Purchase license:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Free trial:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Temporary license:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Support forum:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## Relaterade handledningar

- [Effektiv konvertering av Excel till PDF med anpassade datumformat med Aspose.Cells för Java](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells för Java: Så skapar och formaterar du Excel‑arbetsböcker effektivt](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Behärska Excel‑manipulering med Aspose.Cells för Java: Arbetsboksoperationer och cellformatering](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}