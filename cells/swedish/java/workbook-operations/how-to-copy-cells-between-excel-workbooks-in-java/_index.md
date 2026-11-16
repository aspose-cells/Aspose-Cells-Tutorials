---
category: general
date: 2026-11-16
description: Hur man kopierar celler mellan Excel-arbetsböcker i Java – ladda en arbetsbok,
  kopiera ett område mellan arbetsböcker (inklusive en pivottabell) och spara arbetsboksfilen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: sv
lastmod: 2026-11-16
og_description: Hur man kopierar celler mellan Excel‑arbetsböcker i Java. Lär dig
  att läsa in en Excel‑arbetsbok, kopiera ett område (inklusive en pivottabell) mellan
  arbetsböcker och spara arbetsboksfilen.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: Hur man kopierar celler mellan Excel‑arbetsböcker i Java – komplett guide
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: Hur du kopierar celler mellan Excel‑arbetsböcker i Java
url: /sv/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kopierar celler mellan Excel‑arbetsböcker i Java

Om du behöver **kopiera celler** från en Excel‑arbetsbok till en annan med Java, visar den här guiden ett pålitligt sätt att göra det. Du kommer att lära dig hur du **läser in Excel‑arbetsbok Java**, kopierar ett område som kan innehålla en pivottabell och slutligen **sparar arbetsboksfil** med de kopierade data.

Denna handledning täcker:

* Laddning av en källarbetsbok och val av ett kalkylblad.  
* Definition av det exakta område du vill flytta (inklusive en pivottabell).  
* Skapande av en destinationsarbetsbok och kopiering av området.  
* Sparande av destinationsfilen.  

Exemplet använder Aspose.Cells för Java‑biblioteket, som arbetar med Excel‑filer utan att kräva Microsoft Office. Koden körs på Java 8+ och i vilken modern IDE som helst (IntelliJ IDEA, Eclipse, VS Code, etc.).

---

## Förutsättningar

Innan du börjar, se till att du har:

| Krav | Orsak |
|------|-------|
| Java Development Kit (JDK) 8 eller nyare | Krävs för att kompilera och köra koden. |
| Maven eller Gradle byggverktyg | Förenklar tillägget av Aspose.Cells‑beroendet. |
| Aspose.Cells för Java‑bibliotek (senaste versionen) | Tillhandahåller klasserna `Workbook`, `Worksheet` och `Range` som används i exemplet. |
| Två Excel‑filer (`source.xlsx` och en tom mapp för `dest.xlsx`) | Källfilen måste innehålla data och, eventuellt, en pivottabell du vill kopiera. |

Lägg till Aspose.Cells‑beroendet i din `pom.xml` (Maven) eller `build.gradle` (Gradle). Exempel för Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## Hur man kopierar celler med Aspose.Cells

Följande steg guidar dig genom hela processen. Varje steg innehåller Java‑koden, en förklaring av **varför** steget är viktigt och ett tips för att undvika vanliga fallgropar.

### Steg 1: Ladda källarbetsboken

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Varför?**  
`Workbook` representerar hela Excel‑filen. När du laddar den får du åtkomst till alla kalkylblad, celler och objekt såsom pivottabeller. Att använda det första kalkylbladet är vanligt, men du kan välja vilket blad som helst genom namn (`srcWb.getWorksheets().get("Sheet2")`).

**Proffstips:**  
Om källfilen är stor, överväg att ladda den i *minnes‑effektivt* läge: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }});`

### Steg 2: Definiera området som inkluderar pivottabellen

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Varför?**  
Ett `Range`‑objekt abstraherar ett rektangulärt block av celler. Genom att ange `"A1:G20"` talar du exakt till Aspose.Cells vilka celler—inklusive eventuell inbäddad pivottabell—som ska kopieras. Biblioteket kopierar automatiskt underliggande data, format och pivottabellsdefinitioner.

**Edge case:**  
Om pivottabellen sträcker sig utanför det definierade området, utöka adressen (t.ex. `"A1:Z100"`). Du kan också använda `srcWs.getCells().getMaxDataColumn()` och `getMaxDataRow()` för att dynamiskt beräkna det använda området.

### Steg 3: Skapa destinationsarbetsboken

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Varför?**  
En ny arbetsbok säkerställer att ingen oönskad formatering eller dolda blad stör det kopierade innehållet. Standardarbetsboken innehåller redan ett kalkylblad, som vi kommer att använda som mål.

### Steg 4: Kopiera området till destinationsarbetsboken

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Varför?**  
`copyRange` hanterar alla cellattribut: värden, formler, formatering och även pivottabellscachar. Genom att kopiera till `"A1"` placerar du området i det övre‑vänstra hörnet av destinationsbladet, vilket bevarar den ursprungliga layouten.

**Vanlig fråga:** *Kommer pivottabellen att förbli funktionell?*  
Ja. Aspose.Cells kopierar pivottabellens definition och dess cache, så pivottabellen fungerar exakt som i källarbetsboken.

### Steg 5: Spara destinationsarbetsboken

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Varför?**  
Genom att anropa `save` skrivs den minnes‑lagrade arbetsboken till en fysisk `.xlsx`‑fil. Du kan även spara till andra format (`.xls`, `.csv`, `.pdf`) genom att ändra filändelsen eller använda `SaveOptions`.

**Tips:**  
Om du behöver strömma filen som ett webbsvar, använd `destWb.save(OutputStream, SaveFormat.XLSX);` istället för en filsökväg.

---

## Kopiera område mellan arbetsböcker – komplett källkod

Nedan är den fullständiga, körklara Java‑klassen. Ersätt `YOUR_DIRECTORY` med den faktiska mappen på din maskin.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Förväntat resultat:**  
`dest.xlsx` innehåller en exakt kopia av området `A1:G20` från `source.xlsx`. Om källområdet innehöll en pivottabell visar destinationsfilen samma pivottabell med dess datakälla korrekt länkad till de kopierade cellerna.

Du kan öppna `dest.xlsx` i Excel, LibreOffice eller någon annan visare som stödjer `.xlsx` för att verifiera att värden, formatering och pivottabellens funktionalitet är bevarade.

---

## Kopiera pivottabell‑arbetsbok – vad du bör veta

* **Pivot‑cache kopieras automatiskt.** Biblioteket överför den underliggande cachen, så pivottabellen behöver inte uppdateras manuellt.  
* **Externa datakällor överförs inte.** Om pivottabellen hämtar data från en extern databas måste du säkerställa att destinationsarbetsboken kan nå samma källa, eller återskapa cachen lokalt.  
* **Stora pivottabeller kan öka minnesanvändningen.** För mycket stora arbetsböcker, överväg att öka JVM‑heapen (`-Xmx2g`) för att undvika `OutOfMemoryError`.

---

## Spara arbetsboksfil i olika format

Aspose.Cells låter dig spara resultatet i många format utan extra kodändringar:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

Välj det format som matchar din efterföljande process. Samma `copyRange`‑logik fungerar oavsett vilket slutformat du väljer.

---

## Ladda Excel‑arbetsbok Java – ytterligare tips

* **Ladda krypterade filer:** Använd `LoadOptions` med ett lösenord:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Läsa endast specifika blad:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

Dessa alternativ kan snabba upp **load excel workbook java**‑steget, särskilt för stora filer.

---

## Slutsats

Du vet nu **hur man kopierar celler** mellan Excel‑arbetsböcker i Java, hur man **kopierar område mellan arbetsböcker** som innehåller en **pivottabell**, och hur man **sparar arbetsboksfil** i det format du behöver. Genom att följa stegen ovan kan du integrera Excel‑datamanipulation i vilken Java‑applikation som helst—oavsett om du bygger en rapporteringsmotor, ett ETL‑flöde eller ett enkelt fil‑konverteringsverktyg.

**Nästa steg** du kan utforska:

* Använd **copy range between workbooks** för att slå ihop flera rapporter till


## Vad bör du lära dig härnäst?


Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Save New Workbook in Java – Copy Range Between Workbooks Tutorial](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [How to copy pivot tables between Excel workbooks in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [How to copy range in Java – Copy Pivot Table with Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}