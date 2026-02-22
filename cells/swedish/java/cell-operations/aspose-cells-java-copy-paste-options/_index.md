---
date: '2026-02-22'
description: Lär dig hur du automatiserar Excel‑rapportering med Aspose.Cells i Java
  genom att använda CopyOptions och PasteOptions för att hålla formlerna korrekta
  och bara klistra in synliga värden.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Automatisera Excel‑rapportering – Bemästra CopyOptions och PasteOptions i Java
  med Aspose.Cells
url: /sv/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

 all translations. Ensure no extra spaces.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatisera Excel-rapportering med Aspose.Cells: CopyOptions & PasteOptions i Java

Letar du efter att **automatisera Excel-rapportering** med Java? Med Aspose.Cells kan du programatiskt kopiera, klistra in och justera formler så att dina rapporter förblir korrekta och endast den data du behöver överförs. I den här handledningen går vi igenom två viktiga funktioner—**CopyOptions.ReferToDestinationSheet** och **PasteOptions**—som låter dig bevara formelreferenser och klistra in värden endast från synliga celler.

## Snabba svar
- **Vad gör `CopyOptions.ReferToDestinationSheet`?** Justerar formler så att de pekar på destinationsbladet när data kopieras.  
- **Hur kan jag klistra in endast synliga celler?** Sätt `PasteOptions.setOnlyVisibleCells(true)` med `PasteType.VALUES`.  
- **Vilken biblioteksversion krävs?** Aspose.Cells 25.3 eller senare.  
- **Behöver jag en licens för produktion?** Ja, en permanent eller tillfällig licens tar bort utvärderingsbegränsningar.  
- **Kan jag använda Maven eller Gradle?** Båda stöds; se beroendesnuttarna nedan.

## Vad betyder “automatisera Excel-rapportering”?
Att automatisera Excel-rapportering innebär att programatiskt generera, konsolidera och formatera Excel-arbetsböcker, vilket eliminerar manuella kopiera‑klistra‑steg och minskar fel. Aspose.Cells erbjuder ett kraftfullt API som låter Java‑utvecklare manipulera kalkylblad i stor skala.

## Varför använda CopyOptions och PasteOptions för rapportering?
- **Behålla formelintegritet** när data flyttas mellan blad.  
- **Exkludera dolda rader/kolumner** för att hålla rapporterna rena och fokuserade.  
- **Öka prestanda** genom att kopiera endast nödvändig data istället för hela områden.

## Förutsättningar
- Java 8 eller högre.  
- Maven eller Gradle för beroendehantering.  
- Aspose.Cells 25.3+ (prövning, tillfällig eller permanent licens).  

## Installera Aspose.Cells för Java

Add the library to your project with one of the following:

**Maven**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Licensinnehav
- **Gratis provversion** – Fullt funktionspaket för utvärdering.  
- **Tillfällig licens** – Tar bort provversionsbegränsningar medan du testar.  
- **Permanent licens** – Rekommenderas för produktionsarbetsbelastningar.

Initialize Aspose.Cells in your Java code:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Steg‑för‑steg‑guide

### 1. CopyOptions med ReferToDestinationSheet

#### Översikt
Att sätta `CopyOptions.ReferToDestinationSheet` till `true` skriver om formelreferenser så att de pekar på det nya bladet efter kopieringsoperationen.

#### Steg 1: Initiera Workbook och Worksheets
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Steg 2: Konfigurera CopyOptions
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Steg 3: Utför kopieringsoperation
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Varför detta är viktigt*: Formler som ursprungligen refererade till `Sheet1` kommer nu korrekt att referera till `DestSheet`, vilket gör dina automatiserade rapporter pålitliga.

**Felsökningstips**: Om formler fortfarande refererar till det gamla bladet, säkerställ att `setReferToDestinationSheet(true)` anropas **innan** kopieringen.

### 2. PasteOptions för enbart värden från synliga celler

#### Översikt
`PasteOptions` låter dig definiera vad som klistras in. Genom att använda `PasteType.VALUES` tillsammans med `onlyVisibleCells=true` kopieras endast de visade värdena, dolda rader/kolumner och formatering ignoreras.

#### Steg 1: Initiera Workbook och Worksheets
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Steg 2: Konfigurera PasteOptions
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Steg 3: Utför klistra‑in‑operation
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Varför detta är viktigt*: Perfekt för att extrahera filtrerad data eller skapa rena rapporter utan dolda rader eller formateringsbrus.

**Felsökningstips**: Verifiera att rader/kolumner verkligen är dolda i Excel innan du kopierar; annars kommer de att inkluderas.

## Praktiska tillämpningar
1. **Finansiell konsolidering** – Slå samman månatliga blad till en huvudarbetsbok samtidigt som alla formler förblir korrekta.  
2. **Export av filtrerad data** – Hämta endast synliga rader från ett filtrerat tabell till ett sammanfattningsblad.  
3. **Schemalagd rapportgenerering** – Automatisera nattlig Excel‑rapportskapning med exakta cellvärden och korrekta referenser.

## Prestandaöverväganden
- **Avsluta Workbooks** när du är klar (`wb.dispose();`) för att frigöra inhemska resurser.  
- **Batch‑operationer** – Gruppera flera kopierings-/klistra‑in‑anrop för att minska overhead.  
- **Övervaka minne** – Stora arbetsböcker kan kräva ökad heap (`-Xmx2g`).

## Vanliga frågor

**Q1: Vad används `CopyOptions.ReferToDestinationSheet` för?**  
A: Det skriver om formelreferenser så att de pekar på destinationsbladet efter en kopiering, vilket säkerställer att rapporteringsformler förblir korrekta.

**Q2: Hur klistrar jag in endast synliga celler?**  
A: Sätt `PasteOptions.setOnlyVisibleCells(true)` och välj `PasteType.VALUES`.

**Q3: Kan jag använda Aspose.Cells utan att köpa en licens?**  
A: Ja, en gratis provversion eller tillfällig licens finns tillgänglig för utvärdering, men en permanent licens krävs för produktion.

**Q4: Varför är vissa referenser fortfarande felaktiga efter kopiering?**  
A: Dubbelkolla att `ReferToDestinationSheet` är aktiverat **innan** kopieringsoperationen och att källformlerna inte innehåller externa arbetsboks‑länkar.

**Q5: Vilka bästa praxis för minneshantering bör jag följa?**  
A: Avsluta `Workbook`‑objekt när du är klar, bearbeta stora filer i delar och övervaka JVM‑heap‑användning.

**Q6: Är det möjligt att kombinera CopyOptions och PasteOptions i en operation?**  
A: Ja, du kan kedja dem genom att först kopiera med `CopyOptions` och sedan tillämpa `PasteOptions` på målområdet.

## Resurser
- **Dokumentation**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Nedladdning**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Köp**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Gratis provversion**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Tillfällig licens**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Supportforum**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Senast uppdaterad:** 2026-02-22  
**Testad med:** Aspose.Cells 25.3 för Java  
**Författare:** Aspose