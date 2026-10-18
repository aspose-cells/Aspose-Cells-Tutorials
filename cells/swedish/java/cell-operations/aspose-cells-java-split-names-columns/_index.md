---
date: '2026-03-15'
description: Lär dig hur du delar upp namn i separata kolumner och sparar arbetsboken
  xlsx med Aspose Cells Java i en steg‑för‑steg‑handledning.
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: aspose cells java – Dela namn i kolumner
url: /sv/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Behärska **aspose cells java**: Dela namn i kolumner

Välkommen till vår omfattande **aspose cells java**‑handledning. I den här guiden kommer du att lära dig **hur man delar namn** som lagras i en enda Excel‑kolumn till två separata kolumner—förnamn och efternamn—med den kraftfulla text‑till‑kolumner‑funktionen. Oavsett om du rensar upp en kontaktlista, förbereder data för en CRM‑import eller helt enkelt behöver ett snabbt sätt att omstrukturera kalkylblad, visar den här handledningen exakt hur du **sparar arbetsbok xlsx** efter transformationen.

## Snabba svar
- **Vad täcker den här handledningen?** Dela fullständiga namnsträngar i för- och efternamnskolumner med Aspose.Cells för Java.  
- **Vilken biblioteksversion används?** Den senaste stabila releasen (från 2026).  
- **Behöver jag en licens?** En gratis provversion fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Kan jag dela på andra avgränsare?** Ja—byt bara separatorn i `TxtLoadOptions`.  
- **Är utdata en .xlsx‑fil?** Absolut, arbetsboken sparas i XLSX‑format.

## Vad är **aspose cells java**?
**Aspose.Cells java** är ett högpresterande Java‑API som låter utvecklare skapa, modifiera, konvertera och rendera Excel‑filer utan att behöva Microsoft Office. Det stödjer alla vanliga Excel‑format och erbjuder avancerade funktioner såsom formler, diagram och datamanipulation.

## Varför använda **aspose cells java** för att dela namn?
- **Ingen installation**: Fungerar i alla server‑sidiga Java‑miljöer.  
- **Hastighet**: Hantera stora kalkylblad snabbare än inbyggd Excel‑interop.  
- **Precision**: Full kontroll över avgränsare, kolumnintervall och utdataformat.  
- **Tillförlitlighet**: Inga COM‑ eller Office‑beroenden, vilket gör det idealiskt för moln‑ eller container‑distributioner.

## Förutsättningar
- Java Development Kit (JDK) 8 eller nyare.  
- En IDE som IntelliJ IDEA eller Eclipse (valfritt men rekommenderat).  
- Maven eller Gradle för beroendehantering.  

### Maven‑inställning
Lägg till Aspose.Cells‑beroendet i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle‑inställning
Lägg till biblioteket i din `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **Proffstips:** Använd en tillfällig licens från Aspose‑portalen för att låsa upp full funktionalitet under utveckling.

## Steg‑för‑steg‑implementering

### Steg 1: Skapa en arbetsbok och öppna det första kalkylbladet
Först importerar du de grundläggande klasserna och instansierar en ny arbetsbok. Detta ger dig en ren Excel‑fil redo för datainmatning.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### Steg 2: Fyll kalkylbladet med exempelnamn
Därefter lägger du till några fullständiga namnsträngar i kolumn **A**. I ett riktigt projekt skulle du läsa dessa från en databas eller CSV‑fil.

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### Steg 3: Konfigurera Text Load Options för kolumnsplittning
`TxtLoadOptions`‑klassen talar om för Aspose.Cells hur texten ska tolkas. Här använder vi ett mellanslag (`' '`) som avgränsare.

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### Steg 4: Dela texten i två kolumner
Anropa nu `textToColumns()` på det cellområde som innehåller namnen. Parametrarna `(0, 0, 5, opts)` betyder *börja på rad 0, kolumn 0, bearbeta 5 rader, med de alternativ vi just definierade*.

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

Efter detta anrop innehåller kolumn A förnamnen och kolumn B efternamnen.

### Steg 5: Spara arbetsboken som en XLSX‑fil
Slutligen skriver du den modifierade arbetsboken till disk. `SaveFormat`‑enumet säkerställer att filen lagras i det moderna XLSX‑formatet.

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **Varför detta är viktigt:** Genom att använda **save workbook xlsx** garanterar du kompatibilitet med de senaste versionerna av Excel, Google Sheets och andra kalkylbladsverktyg.

## Praktiska tillämpningar
- **Datastädning:** Separera snabbt sammanslagna fält innan de laddas in i analys‑pipelines.  
- **CRM‑integration:** Omvandla en platt kontaktlista till en strukturerad tabell för import.  
- **HR‑system:** Dela anställdas fullständiga namn för löne- eller förmånsbehandling.

## Prestandaöverväganden
När du arbetar med tusentals rader:

1. **Batch‑uppdateringar:** Använd `ws.getCells().setRowHeight()` eller liknande batch‑metoder för att minska overhead.  
2. **Minneshantering:** Anropa `wb.calculateFormula()` endast när det behövs, och frigör stora objekt omedelbart.  
3. **Skräpsamling:** Kör JVM med lämpliga heap‑inställningar (`-Xmx2g` för stora filer) för att undvika OutOfMemory‑fel.

## Vanliga problem och lösningar
| Problem | Lösning |
|-------|----------|
| **Namn innehåller mellanstavelse** (t.ex. “John A. Doe”) | Justera separatorn eller efterbehandla den andra kolumnen för att extrahera efternamnet. |
| **Oväntade tomma celler** | Verifiera att källintervallet (`textToColumns`‑parametrar) matchar de faktiska dataraderna. |
| **Licens ej hittad** | Placera den tillfälliga licensfilen (`Aspose.Cells.lic`) i projektets rot eller ange licensen programatiskt. |

## Vanliga frågor

**Q: Vad är Aspose.Cells Java?**  
A: Ett kraftfullt bibliotek som låter dig skapa, modifiera och konvertera Excel‑filer programatiskt med Java.

**Q: Kan jag dela kolumner baserat på andra avgränsare än mellanslag?**  
A: Ja, anpassa `TxtLoadOptions`‑separatorn efter dina data.

**Q: Hur hanterar jag stora dataset med Aspose.Cells?**  
A: Optimera prestanda genom att hantera minnet och minimera arbetsboksoperationer, som beskrivits ovan.

**Q: Finns det support om jag stöter på problem?**  
A: Besök [Aspose Forum](https://forum.aspose.com/c/cells/9) för community‑hjälp eller kontakta Aspose supportteam direkt.

**Q: Vilka format kan Aspose.Cells spara arbetsböcker i?**  
A: Stöder ett brett spektrum av Excel‑filformat, inklusive XLSX, XLS, CSV och fler.

## Resurser

- **Dokumentation:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Nedladdning:** [Aspose.Cells Java Releases](https://releases.aspose.com/cells/java/)
- **Köp:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Gratis provversion:** [Try Aspose.Cells for Free](https://releases.aspose.com/cells/java/)
- **Tillfällig licens:** [Request a Temporary License](https://purchase.aspose.com/temporary-license/)

Lycka till med kodningen, och njut av att utnyttja hela kraften i **aspose cells java** i dina projekt!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Senast uppdaterad:** 2026-03-15  
**Testad med:** Aspose.Cells 25.3 for Java  
**Författare:** Aspose