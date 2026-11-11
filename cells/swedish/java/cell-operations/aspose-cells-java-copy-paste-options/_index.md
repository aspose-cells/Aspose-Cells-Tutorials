---
date: '2026-10-28'
description: Lär dig hur du klistrar in värden med Aspose.Cells copy and paste options
  i Java, med step‑by‑step code, Maven dependency setup och licensing tips.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Lär dig hur du klistrar in värden med Aspose.Cells copy and paste
  options i Java, med step‑by‑step code, Maven dependency setup och licensing tips.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Hur man klistrar in värden med Aspose.Cells copy and paste options
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Hur man klistrar in värden med Aspose.Cells copy and paste options
url: /sv/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man klistrar in värden med Aspose.Cells kopierings‑ och inklistringsalternativ

Att automatisera Excel‑rapportering i Java innebär att du kan skapa, konsolidera och formatera arbetsböcker utan att någonsin öppna Excel manuellt. Med **Aspose.Cells** får du full kontroll över formler, dolda rader och cellvärden, så att dina rapporter förblir korrekta och lätta. I den här handledningen lär du dig hur du använder **CopyOptions.ReferToDestinationSheet** för att hålla formler korrekta och **PasteOptions** för att klistra in endast de synliga värden du behöver.

## Snabba svar
- **Vad gör `CopyOptions.ReferToDestinationSheet`?** Det skriver om formler så att de pekar på destinationsbladet efter en kopieringsoperation.  
- **Hur kan jag klistra in endast synliga celler?** Anropa `PasteOptions.setOnlyVisibleCells(true)` tillsammans med `PasteType.VALUES`.  
- **Vilken biblioteksversion krävs?** Aspose.Cells 25.3 eller senare.  
- **Behöver jag en licens för produktion?** Ja – en permanent eller tillfällig licens tar bort utvärderingsgränser.  
- **Kan jag använda Maven eller Gradle?** Båda stöds; se beroende‑snuttarna nedan.

## Vad betyder “automatisera Excel‑rapportering”?
Att automatisera Excel‑rapportering innebär att generera och uppdatera Excel‑arbetsböcker programmässigt, vilket gör att du kan skapa, slå ihop och formatera rapporter utan manuell kopiering‑och‑inklistra, vilket minskar fel och sparar timmar av repetitivt arbete. Detta tillvägagångssätt är idealiskt för schemalagda batch‑jobb, datadrivna instrumentpaneler och finansiella konsoliderings‑pipelines.

## Varför använda CopyOptions och PasteOptions för rapportering?
Dessa två klasser låter dig behålla formelreferenser intakta när du kopierar data **och** extrahera endast de celler som är synliga efter filtrering eller dolda rader. Att använda dem tillsammans minskar mängden data som överförs med upp till 80 % i vanliga filtrerade‑tabellsituationer och garanterar att formler fortsätter att beräkna korrekt i destinationsbladet.

## Förutsättningar
- Java 8 eller högre.  
- Maven eller Gradle för beroendehantering.  
- Aspose.Cells 25.3+ (prövning, tillfällig eller permanent licens).  

## Installera Aspose.Cells för Java

Lägg till biblioteket i ditt projekt med någon av följande:

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

### Licensanskaffning
- **Gratis provversion** – full uppsättning funktioner för utvärdering.  
- **Tillfällig licens** – tar bort provversionsgränser medan du testar.  
- **Permanent licens** – rekommenderas för produktionsarbetsbelastningar.

Initiera Aspose.Cells i din Java‑kod:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Steg‑för‑steg‑guide

### 1. copyOptions med referToDestinationSheet

#### Översikt
`CopyOptions` är Aspose.Cells konfigurationsobjekt som styr hur formler och cellreferenser hanteras under en kopieringsoperation. Att sätta `CopyOptions.ReferToDestinationSheet` till `true` skriver om formelreferenser så att de pekar på det nya bladet efter kopieringen.

#### Steg 1: initiera arbetsbok och kalkylblad  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Steg 2: konfigurera copyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Steg 3: utför kopieringsoperation  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Varför detta är viktigt*: Formler som ursprungligen refererade till `Sheet1` kommer nu korrekt att referera till `DestSheet`, vilket håller dina automatiserade rapporter pålitliga.

**Felsökningstips**: Om formler fortfarande refererar till det gamla bladet, säkerställ att `setReferToDestinationSheet(true)` anropas **före** kopieringen.

### 2. pasteOptions för endast värden från synliga celler

#### Översikt
`PasteOptions` är Aspose.Cells inställningsobjekt som definierar vad som klistras in. Att använda `PasteType.VALUES` tillsammans med `onlyVisibleCells=true` kopierar endast de visade värdena, och ignorerar dolda rader/kolumner och formatering.

#### Steg 1: initiera arbetsbok och kalkylblad  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Steg 2: konfigurera pasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Steg 3: utför inklistringsoperation  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Varför detta är viktigt*: Idealiskt för att extrahera filtrerade data eller skapa rena rapporter utan dolda rader eller formateringsbrus.

**Felsökningstips**: Verifiera att rader/kolumner verkligen är dolda i Excel innan du kopierar; annars kommer de att inkluderas.

## Praktiska tillämpningar
1. **Finansiell konsolidering** – slå ihop månatliga blad till en huvudarbetsbok samtidigt som alla formler förblir korrekta.  
2. **Export av filtrerade data** – hämta endast synliga rader från en filtrerad tabell till ett sammanfattningsblad.  
3. **Schemalagd rapportgenerering** – automatisera nattlig Excel‑rapportskapning med exakta cellvärden och korrekta referenser.

## Prestandaöverväganden
- **Disposera arbetsböcker** när du är klar (`wb.dispose();`) för att frigöra inhemska resurser.  
- **Batch‑operationer** – gruppera flera kopierings‑/inklistringsanrop för att minska overhead.  
- **Övervaka minne** – stora arbetsböcker kan kräva ökad heap (`-Xmx2g`).  
- Aspose.Cells stöder **50+ in‑ och utdataformat** och kan bearbeta arbetsböcker med **upp till 2 miljoner rader** utan att ladda hela filen i minnet, vilket levererar hög genomströmning för företagsarbetsbelastningar.

## Vanliga frågor

**Q: Vad används `CopyOptions.ReferToDestinationSheet` för?**  
A: Den skriver om formelreferenser så att de pekar på destinationsbladet efter en kopiering, vilket säkerställer att rapporteringsformler förblir korrekta.

**Q: Hur klistrar jag in endast synliga celler?**  
A: Sätt `PasteOptions.setOnlyVisibleCells(true)` och välj `PasteType.VALUES`.

**Q: Kan jag använda Aspose.Cells utan att köpa en licens?**  
A: Ja, en gratis provversion eller tillfällig licens finns tillgänglig för utvärdering, men en permanent licens krävs för produktion.

**Q: Varför är vissa referenser fortfarande felaktiga efter kopiering?**  
A: Dubbelkolla att `ReferToDestinationSheet` är aktiverat **före** kopieringsoperationen och att källformlerna inte innehåller länkar till externa arbetsböcker.

**Q: Vilka bästa praxis för minneshantering bör jag följa?**  
A: Disposera `Workbook`‑objekt när du är klar, bearbeta stora filer i delar och övervaka JVM‑heap‑användning.

**Q: Är det möjligt att kombinera CopyOptions och PasteOptions i en operation?**  
A: Ja, du kan kedja dem genom att först kopiera med `CopyOptions` och sedan tillämpa `PasteOptions` på målområdet.

## Resurser
- **Documentation**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **Purchase**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Free trial**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **Temporary license**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **Support forum**: [Aspose support](https://forum.aspose.com/c/cells)

---

**Senast uppdaterad:** 2026-10-28  
**Testad med:** Aspose.Cells 25.3 for Java  
**Författare:** Aspose

## Relaterade handledningar

- [Läs Excel‑fil Java – Master Workbook Cell Manipulation med Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Lägg till data i cell i Excel med Aspose.Cells för Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Konvertera Excel‑cellrad‑kolumn‑index med Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}