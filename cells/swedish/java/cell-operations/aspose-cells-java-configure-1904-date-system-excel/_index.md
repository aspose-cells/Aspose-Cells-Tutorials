---
date: '2026-02-22'
description: Lär dig hur du ändrar Excels datumssystem till 1904 med Aspose.Cells
  för Java, sätter Exceldatumformat och konverterar Excels 1904‑system effektivt.
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: Ändra Exceldatumssystemet till 1904 med Aspose.Cells Java
url: /sv/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ändra Exceldatumssystem till 1904 med Aspose.Cells Java

Att hantera historiska data i Excel kan vara utmanande eftersom Excel stöder två olika datumssystem. **I den här handledningen kommer du att lära dig hur du ändrar Exceldatumssystemet till 1904-formatet med hjälp av Aspose.Cells för Java**, vilket gör hantering av äldre datum smärtfritt. Vi går igenom hur man initierar en arbetsbok, aktiverar 1904-datumssystemet och sparar ändringen.

## Snabba svar
- **Vad gör 1904-datumssystemet?** Det börjar räkna dagar från 1 januari 1904, vilket förskjuter alla datum med 1462 dagar jämfört med standard‑1900‑systemet.  
- **Varför använda Aspose.Cells för att ändra datumssystemet?** Det erbjuder ett enkelt API som fungerar utan att Excel är installerat och stödjer stora filer.  
- **Vilka Java‑versioner stöds?** JDK 8 eller senare.  
- **Behöver jag en licens?** En gratis provversion fungerar för utvärdering; en licens tar bort användningsgränser.  
- **Kan jag konvertera tillbaka till 1900‑systemet senare?** Ja, bara anropa `setDate1904(false)`.

## Vad är 1904-datumssystemet i Excel?
1904‑datumssystemet användes ursprungligen av de tidiga Macintosh‑versionerna av Excel. Det räknar dagar från 1 januari 1904, vilket är användbart för kompatibilitet med äldre kalkylblad och vissa finansiella modeller.

## Varför ändra Exceldatumssystem med Aspose.Cells?
- **Plattformsoberoende kompatibilitet** – fungerar på Windows, Linux och macOS.  
- **Ingen Excel‑installation krävs** – idealiskt för server‑sidig bearbetning.  
- **Hög prestanda** – hanterar stora arbetsböcker med minimal minnesanvändning.  

## Förutsättningar
- Java Development Kit (JDK) 8 eller högre.  
- Maven eller Gradle för beroendehantering.  
- Grundläggande kunskaper i Java‑programmering.  

## Installera Aspose.Cells för Java

### Maven
Lägg till följande beroende i din `pom.xml`-fil:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Inkludera denna rad i din `build.gradle`-fil:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Licensanskaffning
Aspose erbjuder en gratis provversion, temporär licens och fullständiga kommersiella licenser. Du kan börja med [gratis provversion](https://releases.aspose.com/cells/java/) eller skaffa en temporär licens från [temporär licenssida](https://purchase.aspose.com/temporary-license/).

## Ändra Exceldatumssystem med Aspose.Cells Java

Nedan följer en steg‑för‑steg‑guide som faktiskt **ändrar Exceldatumssystemet**. Varje steg innehåller en kort förklaring följt av exakt kod du behöver.

### Steg 1: Initiera och ladda arbetsboken
Först, skapa en `Workbook`‑instans som pekar på din befintliga Excel‑fil.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Steg 2: Aktivera 1904‑datumssystemet
Använd arbetsbokens inställningar för att byta datumssystem.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Proffstips:** Du kan också anropa `setDate1904(false)` senare om du behöver återgå.

### Steg 3: Spara den modifierade arbetsboken
Slutligen, skriv ändringarna till en ny fil (eller skriv över originalet).

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

> **Obs:** Koden ovan använder klassnamnet `tWorkbook` som ursprungligen angavs. Se till att detta skrivfel stämmer överens med ditt projekts namngivningskonventioner eller korrigera det till `Workbook` om så behövs.

## Ställ in Exceldatum programatiskt (sekundärt nyckelord)
Om du behöver justera enskilda cellvärden efter att ha ändrat systemet kan du använda `Cells.get(i, j).putValue(Date)` där datumet tolkas enligt det aktiva datumssystemet.

## Konvertera Excel 1904‑systemet tillbaka till 1900 (sekundärt nyckelord)
För att återgå, anropa helt enkelt:

```java
workbook.getSettings().setDate1904(false);
```

Spara sedan arbetsboken igen.

## Praktiska tillämpningar
1. **Dataarkivering** – Bevara äldre tidsstämplar vid migrering av gamla Mac‑baserade kalkylblad.  
2. **Plattformsoberoende rapportering** – Generera rapporter som kan öppnas både på Windows och macOS utan datumavvikelser.  
3. **Finansiell modellering** – Anpassa datumberäkningar till äldre finansiella modeller som förväntar sig 1904‑systemet.

## Prestandaöverväganden
- Begränsa arbetsboksoperationer i en enda session för att hålla minnesanvändningen låg.  
- Använd Java:s finjustering av skräpsamling för mycket stora filer.  

## Vanliga frågor

**Q: Vad är skillnaden mellan 1900‑ och 1904‑datumssystemen?**  
A: 1900‑systemet startar den 1 januari 1900, medan 1904‑systemet startar den 1 januari 1904, vilket förskjuter alla datum med 1462 dagar.

**Q: Kan jag ändra datumssystemet för en arbetsbok som för närvarande är öppen i Excel?**  
A: Ja, men du måste först stänga filen i Excel; annars kommer sparoperationen att misslyckas.

**Q: Behöver jag en licens för att använda `setDate1904`?**  
A: Metoden fungerar i den gratis provversionen, men en full licens tar bort utvärderingsbegränsningar.

**Q: Är det möjligt att ändra datumssystemet för endast ett kalkylblad?**  
A: Nej, datumssystemet är en inställning på arbetsboksnivå; den gäller för alla kalkylblad.

**Q: Hur kan jag verifiera att datumssystemet har ändrats?**  
A: Öppna den sparade filen i Excel, gå till **File → Options → Advanced**, och markera rutan **"Use 1904 date system"**.

## Slutsats
Du vet nu hur du **ändrar Exceldatumssystemet** till 1904 med Aspose.Cells för Java, hur du ställer in Exceldatumformat och hur du konverterar tillbaka om det behövs. Inkludera dessa kodsnuttar i dina databehandlingspipelines för att säkerställa datumkompatibilitet över plattformar.

---

**Senast uppdaterad:** 2026-02-22  
**Testad med:** Aspose.Cells 25.3 for Java  
**Författare:** Aspose  

## Resurser
- **Dokumentation:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Nedladdning:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Köp licens:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Gratis provversion:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Temporär licens:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Supportforum:** [Aspose Support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}