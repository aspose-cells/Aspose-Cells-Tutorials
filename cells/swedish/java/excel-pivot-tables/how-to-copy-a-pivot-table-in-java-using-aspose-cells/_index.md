---
category: general
date: 2026-09-27
description: Kopiera pivottabell i Java med Aspose.Cells – en steg‑för‑steg‑guide
  som visar hur man kopierar ett område och bevarar pivottabellens definitioner.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: sv
lastmod: 2026-09-27
og_description: Kopiera pivottabell i Java med Aspose.Cells. Följ den här kompletta
  handledningen för att kopiera ett område i Aspose.Cells och behålla pivottabellens
  definitioner intakta.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: Kopiera en pivottabell i Java – Aspose.Cells snabbguide
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hur man kopierar en pivottabell i Java med Aspose.Cells
url: /sv/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kopierar en pivottabell i Java med Aspose.Cells

Om du behöver **kopiera pivottabell** från en arbetsbok till en annan, visar den här guiden exakt hur du gör det med Aspose.Cells för Java. Lösningen fungerar för alla pivoter du har byggt, och den bevarar pivottabellens definition utan manuell återuppbyggnad.

Du kommer att lära dig hur du laddar källfilen, definierar området som innehåller pivottabellen, kopierar det området till en ny arbetsbok och slutligen sparar resultatet. Handledningen täcker också vanliga fallgropar, såsom att bevara datakällor och hantera stora arbetsböcker.

## Vad du behöver

Innan du börjar, se till att du har:

* Java 17 eller senare (koden kompilerar även med JDK 8+)
* Aspose.Cells för Java 23.9 eller nyare – den senaste versionen erbjuder det mest pålitliga **copy range aspose cells**‑stödet
* En källa‑Excel‑fil som innehåller en pivottabell (t.ex. `SourceWithPivot.xlsx`)
* En IDE eller byggverktyg (Maven/Gradle) som kan referera till Aspose.Cells‑JAR‑filen

## Steg 1: Ladda källarboken som innehåller pivottabellen

Den första åtgärden är att öppna arbetsboken som innehåller den pivottabell du vill duplicera. När filen laddas skapas en minnesrepresentation av alla kalkylblad, celler och pivottabellscachar.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Varför detta är viktigt:**  
Aspose.Cells läser hela arbetsboken, inklusive dolda pivottabellscachar. Om du hoppar över detta steg skulle den efterföljande **copy pivot table**‑operationen förlora den underliggande datakällan.

## Steg 2: Skapa en tom destinationsarbok

Nästa steg är att instansiera en ny arbetsbok som ska ta emot den kopierade pivottabellen. Att börja med en ren arbetsbok undviker oavsiktliga överskrivningar.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Tips:** Standardarboken innehåller ett tomt blad, vilket är perfekt för en enkel kopiering. Om du behöver kopiera till ett specifikt bladnamn, byt namn på `destWs` med `destWs.setName("TargetSheet")`.

## Steg 3: Definiera källområdet som inkluderar pivottabellen

En pivottabell upptar ett rektangulärt block av celler. Du måste ange exakt vilket område som ska kopieras; annars kopieras bara rådata. I detta exempel antar vi att pivottabellen upptar **A1:G20**, men du kan justera adressen så att den matchar din fil.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Varför detta fungerar:**  
När du anropar `createRange` på kalkylbladets `Cells`‑samling inkluderar Aspose.Cells pivottabellens definition, dess cache och eventuell formatering. Detta är kärnan i **how to copy pivot table** korrekt.

## Steg 4: Kopiera det definierade området till destinationsbladet

Använd nu `copy`‑metoden för att duplicera området. Metoden kopierar allt inom området, inklusive pivottabellens definition, formler och stilar.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**Viktigt att notera:**  
Om du bara behöver data utan pivottabellen kan du använda `srcRange.copyData`. För en sann **copy pivot table** måste du dock kopiera hela området som visas ovan.

## Steg 5: Spara destinationsarboken

Till sist skriver du den nya arbetsboken till disk. Den resulterande filen kommer att innehålla en fullt funktionell pivottabell som är identisk med källan.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

När programmet körs skapas `CopyPivotResult.xlsx` med samma pivottabellslayout, filter och beräkningar som originalfilen.

## Förväntat resultat

När du öppnar `CopyPivotResult.xlsx` i Excel:

* Pivottabellen visas på **A1:G20** i det första bladet.
* Alla rad‑/kolumnfält, filter och värdefält är intakta.
* Att uppdatera pivottabellen uppdaterar samma datakälla som källarboken (om källdata är inbäddad).

## Edge cases och praktiska tips

| Situation | Hur du hanterar det |
|-----------|---------------------|
| **Pivottabellen sträcker sig över fler kolumner än förväntat** | Använd `srcWs.getPivotTables().get(0).getPivotTableArea()` för att programatiskt hämta den exakta adressen. |
| **Källarboken innehåller flera pivoter** | Loopa igenom `srcWs.getPivotTables()` och kopiera varje område individuellt, justera destinationsadresserna. |
| **Stora arbetsböcker ger minnespress** | Aktivera `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` innan du laddar källan. |
| **Du behöver bara kopiera pivottabellens definition, inte datan** | Efter kopieringen, ta bort källdataraderna i destinationen med `destWs.getCells().deleteRows(startRow, count)`. |
| **Destinationsfilen måste behålla originalformateringen** | Ställ in `CopyOptions` med `options.setPasteType(PasteType.ALL)` för en fullständig kopia med hög trohet. |

**Pro tip:** Verifiera alltid den kopierade pivottabellen genom att anropa `destWs.getPivotTables().get(0).refresh()` programatiskt. Detta säkerställer att cachen är uppdaterad, särskilt när källdata finns i en extern anslutning.

## Fullständigt körbart exempel

Nedan är hela programmet som du kan kopiera‑klistra in i din IDE. Ersätt `YOUR_DIRECTORY` med den faktiska sökvägen på din maskin.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

När du kör den här koden kommer den att **copy pivot table** exakt som beskrivet, och den demonstrerar det mest raka sättet att **copy range aspose cells** samtidigt som pivottabellens funktionalitet bevaras.

## Slutsats

Du vet nu hur du **copy pivot table** i Java med Aspose.Cells, från att ladda källarboken till att spara destinationsfilen. Guiden täckte de viktigaste stegen, förklarade varför varje steg är viktigt och tog upp vanliga edge cases.  

Nästa steg kan vara att utforska:

* **how to copy pivot table** mellan olika kalkylblad i samma arbetsbok
* Att använda **copy range aspose cells** för att duplicera diagram eller villkorsstyrd formatering
* Att automatisera pivottabellens uppdatering efter kopiering för att hålla data aktuella

Känn dig fri att experimentera med större områden, flera pivoter eller integrera denna logik i en större Excel‑bearbetningspipeline. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}