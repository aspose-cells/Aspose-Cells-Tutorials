---
category: general
date: 2026-07-14
description: Kopiera pivottabell mellan arbetsböcker med Java. Lär dig hur du kopierar
  pivottabell, kopierar Excel‑område och exporterar pivottabell på några minuter.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- copy range between workbooks
- export pivot table
language: sv
lastmod: 2026-07-14
og_description: Kopiera pivottabell i Java snabbt. Den här guiden visar hur du kopierar
  en pivottabell, kopierar ett Excel‑område och exporterar pivottabellen med Aspose.Cells.
og_image_alt: Diagram illustrating copy pivot table process between two Excel workbooks
og_title: Kopiera pivottabell mellan arbetsböcker – Java‑automatiseringstutorial
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Copy pivot table between workbooks using Java. Learn how to copy pivot,
    copy Excel range, and export pivot table in minutes.
  headline: Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Kopiera pivottabell mellan arbetsböcker – Steg‑för‑steg Java‑guide
url: /sv/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiera pivottabell mellan arbetsböcker – Komplett Java‑handledning

Har du någonsin behövt **copy pivot table** från en arbetsbok till en annan och undrat varför de vanliga copy‑paste‑knepen alltid förstör layouten? Du är inte ensam. I många rapporteringspipeline lever pivottabellen i en huvudfil, men nedströmsprocesser kräver en lättviktig kopia.  

I den här guiden går vi igenom ett rent, programatiskt sätt att duplicera en pivottabell—ingen manuell trixning krävs. I slutet kommer du att veta **how to copy pivot**, hur du **copy Excel range** på ett säkert sätt, och till och med hur du **export pivot table** till en ny fil, allt med Aspose.Cells för Java.

## Vad du kommer att bygga

- Läs in en källarbetsbok som redan innehåller en pivottabell.  
- Skapa (eller öppna) en målarbetsbok.  
- Definiera det exakta området som innehåller pivottabellen.  
- Kopiera det området—inklusive pivottabellens definition—till den nya arbetsboken.  
- Spara resultatet så att andra appar kan öppna det utan att förlora några beräkningar.

Inga externa verktyg, ingen VBA, bara ren Java‑kod som du kan lägga in i vilket Maven‑ eller Gradle‑projekt som helst.

## Förutsättningar

- Java 17 eller senare (koden fungerar på Java 8+, men nyare JDK‑versioner ger bättre prestanda).  
- Aspose.Cells for Java 23.9 eller nyare – lägg till beroendet från Maven Central.  
- Två Excel‑filer: `SourceWithPivot.xlsx` (innehåller pivottabellen) och en tom platshållare för kopian.  

Om du är ny på Aspose.Cells abstraherar biblioteket de lågnivå‑OOXML‑detaljerna, så att du kan behandla kalkylblad som vanliga Java‑objekt.

## Steg 1: Ställ in ditt projekt

Först, lägg till Aspose.Cells Maven‑artefaktet i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust if you use a different JDK -->
</dependency>
```

Eller, för Gradle:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

> **Pro tip:** Om du använder en IDE som IntelliJ, låt den automatiskt importera biblioteket; det sparar mycket skrivande.

## Steg 2: Läs in källarboken

Vi behöver en `Workbook`‑instans som pekar på filen som innehåller pivottabellen. Konstruktorn läser in hela filen i minnet, så du kan arbeta med den offline.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {

        // Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

Varför läsa in den först? Eftersom pivottabellens cache, fältlista och layout alla lagras i bladet. Att hämta arbetsboken till minnet garanterar att vi kopierar *definitionen* och inte bara de renderade värdena.

## Steg 3: Skapa eller öppna målarbetsboken

Du har två val: börja med en helt ny arbetsbok, eller öppna en befintlig mall. Här skapar vi en tom, vilket är det vanligaste scenariot när du behöver en ren kopia.

```java
        // Create an empty destination workbook (or open an existing one)
        Workbook destinationWorkbook = new Workbook(); // blank workbook with a default sheet
```

Om du senare bestämmer dig för att kopiera till ett specifikt blad, ersätt bara `getWorksheets().get(0)` med rätt index eller namn.

## Steg 4: Definiera det exakta området som innehåller pivottabellen

En pivottabell upptar vanligtvis ett rektangulärt block. Det säkraste tillvägagångssättet är att ange de övre‑vänstra och nedre‑högra cellerna explicit. I vårt exempel ligger pivottabellen från **A1** till **H30**.

```java
        // Define the range in the source sheet that includes the pivot table
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)                     // first worksheet
                                          .getCells()
                                          .createRange("A1:H30");
```

> **Varför inte använda `copyRows`?**  
> `copyRows` kopierar råa cellvärden men kastar bort den underliggande pivottabellscachen. Genom att kopiera hela området bevarar Aspose.Cells pivottabellens metadata, vilket gör att destinationen behåller full interaktivitet.

## Steg 5: Kopiera området (inklusive pivottabellen) till destinationen

Nu händer magin. `copy`‑metoden klonar allt—värden, formler, format och själva pivottabellobjektet—till målplatsen.

```java
        // Copy the defined range (with the pivot table) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)               // destination sheet
                                            .getCells()
                                            .createRange("A1"));
```

Om du behöver klistra in i en annan cell, ändra bara `"A1"` till `"C5"` eller någon annan adress du önskar. Metoden justerar automatiskt interna referenser så att pivottabellen fortsätter att fungera.

## Steg 6: Spara målarbetsboken

Slutligen, skriv den nya arbetsboken till disk. Den resulterande filen kan öppnas i Excel, LibreOffice eller någon annan kalkylbladsvisare, och pivottabellen kommer att fungera exakt som i källan.

```java
        // Save the destination workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

### Förväntat resultat

- `CopyPivotResult.xlsx` öppnas med en fullt funktionell pivottabell som är identisk med originalet.  
- Alla slicers, filter och beräknade fält förblir intakta.  
- Ingen dataförlust—värden beräknas i farten när du uppdaterar pivottabellen.

## Vanliga variationer och kantfall

| Situation | Vad du ska justera |
|-----------|--------------------|
| **Kopiera till en befintlig arbetsbok** | Läs in målarbetsboken istället för att skapa en ny: `new Workbook("ExistingFile.xlsx")`. |
| **Pivottabellen sträcker sig över en okänd storlek** | Använd `Worksheet.getPivotTables().get(0).getPivotTableRange()` för att programatiskt hämta den exakta adressen. |
| **Bevara datakopplingar** | Efter kopiering, anropa `destinationWorkbook.getWorksheets().get(0).getPivotTables().get(0).setRefreshOnLoad(true);` för att hålla externa datalänkar aktiva. |
| **Exportera pivottabell som CSV** | När den är kopierad kan du anropa `destinationWorkbook.save("PivotExport.csv", SaveFormat.CSV);` – detta plattar bara till pivottabellens värden. |

> **Var uppmärksam på:** När käll- och målarbetsböcker använder olika landsinställningar kan talformat förändras. Ange explicit arbetsbokens `setLocale` om du behöver konsekvens.

## Fullständigt fungerande exempel (alla importeringar inkluderade)

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load source workbook containing the pivot
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

        // 2️⃣ Create (or open) destination workbook
        Workbook destinationWorkbook = new Workbook(); // blank workbook

        // 3️⃣ Identify the range that encloses the pivot table
        //    If you don't know the range, you can retrieve it via:
        //    PivotTable pt = sourceWorkbook.getWorksheets().get(0).getPivotTables().get(0);
        //    String address = pt.getPivotTableRange().getRefersTo();
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:H30");

        // 4️⃣ Copy the range (pivot included) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)
                                            .getCells()
                                            .createRange("A1"));

        // 5️⃣ Persist the result
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully!");
    }
}
```

Kör programmet, öppna `CopyPivotResult.xlsx`, och du kommer att se exakt samma pivottabell som du började med—redo för vidare analys eller distribution.

## Sammanfattning

Vi har just demonstrerat **how to copy pivot** från en arbetsbok till en annan med Aspose.Cells för Java. Stegen omfattade att läsa in källan, definiera det exakta **copy Excel range**, utföra kopieringen och slutligen **export pivot table** till en ny fil. Genom att hantera området snarare än enskilda celler garanterar vi att pivottabellens interna cache följer med, vilket håller rapporten dynamisk.

## Vad du kan utforska härnäst

- **Automatisera uppdatering**: Schemalägg kopieringsoperationen med ett Quartz‑jobb så att dina nedströmsfiler hålls uppdaterade.  
- **Kopiera flera pivottabeller**: Loopa igenom `sourceWorkbook.getWorksheets().get(0).getPivotTables()` och kopiera varje till separata blad.  
- **Applicera styling**: Använd `Style`‑objekt för att harmonisera typsnitt och färger i målarbetsboken.  

Om du har frågor om att hantera stora arbetsböcker eller bevara externa datakällor, lämna en kommentar nedan. Lycka till med kodandet, och njut av friheten med programmatisk Excel‑automation!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Excel-pivottabellmanipulation med Aspose.Cells Java&#58; En omfattande guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Hur man uppdaterar Excel-pivottabellens källa med Aspose.Cells för Java&#58; En omfattande guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automatisera styling och sparande av Excel-pivottabell med Aspose.Cells för Java&#58; En omfattande guide](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}