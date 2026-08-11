---
category: general
date: 2026-08-11
description: Skapa en ny arbetsbok med Aspose i Java, lägg till en anpassad egenskap
  i Excel och spara sedan arbetsboken som XLSB med ett fullständigt steg‑för‑steg‑exempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: sv
lastmod: 2026-08-11
og_description: Skapa en ny arbetsbok med Aspose i Java, lägg till en anpassad egenskap
  i Excel och spara arbetsboken som XLSB med ett komplett, färdig‑att‑köra exempel.
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: Skapa ny arbetsbok Aspose – lägg till anpassad egenskap i Excel
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: Skapa ny arbetsbok Aspose – lägg till anpassad egenskap i Excel och spara som
  XLSB
url: /sv/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ny arbetsbok Aspose – lägg till anpassad egenskap Excel och spara som XLSB

Om du behöver **create new workbook Aspose** i en Java‑applikation, visar den här guiden exakt hur du gör det. Du kommer att lära dig att **add custom property Excel**, hämta värdet och **save workbook as XLSB** utan att förlora någon metadata.

Handledningen täcker allt från projektuppsättning till verifiering av den sparade filen. Ingen extern dokumentation krävs; följ bara stegen och kör koden.

## Förutsättningar

- Java Development Kit (JDK) 8 eller högre installerat.
- Maven eller Gradle för att hantera beroenden (exemplet använder Maven).
- En aktiv Aspose.Cells for Java‑licens (eller använd gratis utvärderingsläge för testning).

## Steg 1: Lägg till Aspose.Cells i ditt projekt

Lägg till Aspose.Cells Maven‑artefaktet i din `pom.xml`. Detta beroende tillhandahåller de klasser som behövs för **create new workbook Aspose**‑objekt.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Om du föredrar Gradle, ersätt Maven‑snutten med motsvarande rad `implementation "com.aspose:aspose-cells:23.12"`.

## Steg 2: Skapa en ny arbetsbok Aspose

Det första funktionella steget är att instansiera ett `Workbook`‑objekt. Detta objekt representerar en Excel‑fil i minnet och är ingångspunkten för alla vidare operationer.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

Att skapa en ny arbetsbok Aspose ger dig en tom arbetsbok med ett standardblad, redo för anpassningar.

## Steg 3: Lägg till anpassad egenskap Excel

Anpassade egenskaper låter dig lagra godtycklig metadata i en Excel‑fil. Här **add custom property Excel** med namnet `ProjectId` och ett numeriskt värde.

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

`add`‑metoden accepterar ett egenskapsnamn och ett värde av någon stödjande typ (string, number, date, osv.). Denna metadata följer med filen var du än kopierar den.

## Steg 4: Hämta och visa den anpassade egenskapen

Att läsa tillbaka egenskapen verifierar att den sparades korrekt. Du kan också använda det hämtade värdet i din affärslogik.

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

Casting till `int` fungerar eftersom vi lagrade ett numeriskt värde. Om du lagrar en string, använd `(String)` istället.

## Steg 5: Spara arbetsbok som XLSB

Nu **save workbook as XLSB**. XLSB‑formatet lagrar arbetsboken i en binär representation, vilket är snabbare att öppna och mindre på disk. Alla anpassade egenskaper bevaras automatiskt.

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Ersätt `"WithCustomProps.xlsb"` med en absolut sökväg om du behöver filen i en specifik katalog. `SaveFormat.XLSB`‑enumet talar om för Aspose.Cells att skriva i det binära formatet.

## Steg 6: Verifiera resultatet

Kör programmet från din IDE eller kommandorad:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

Du bör se:

```
ProjectId = 12345
```

Öppna `WithCustomProps.xlsb` i Excel. Navigera till **File → Info → Properties → Advanced Properties → Custom**. `ProjectId`‑posten med värdet `12345` kommer att listas, vilket bekräftar att steget **add custom property excel** lyckades och att **save workbook as xlsb**‑operationen behöll metadata.

## Vanliga frågor och kantfall

### Vad händer om jag behöver lagra en string‑egenskap?

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

Hämta den med:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### Kan jag lägga till flera anpassade egenskaper på en gång?

Ja. Anropa `add` upprepade gånger för varje namn/värde‑par. Aspose.Cells begränsar inte antalet anpassade egenskaper, men håll den totala storleken rimlig för att undvika att filen blir onödigt stor.

### Hur påverkar det binära formatet prestandan?

XLSB‑filer laddas snabbare eftersom de undviker XML‑parsing. Detta märks särskilt för arbetsböcker med många rader, formler eller inbäddade bilder.

### Vad händer om jag behöver arbeta med en befintlig XLSX‑fil?

Ersätt `new Workbook()`‑konstruktorn med `new Workbook("ExistingFile.xlsx")`. Resten av stegen (lägga till egenskaper, spara som XLSB) förblir identiska.

## Fullständig källkod

Nedan är det kompletta, färdiga att köra‑exemplet. Kopiera det till en fil med namnet `CustomPropertiesXlsb.java` i din `src/main/java`‑mapp.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Att köra den här klassen skapar en XLSB‑fil som innehåller den anpassade egenskapen och kan öppnas i vilken modern version av Microsoft Excel som helst.

## Slutsats

Du vet nu hur du **create new workbook Aspose**, **add custom property Excel** och **save workbook as XLSB** med Java. Exemplet demonstrerar hela livscykeln: initiering, metadata‑injektion, verifiering och binär serialisering.

Nästa steg är att utforska relaterade ämnen som **setting document properties**, **working with Excel formulas** eller **converting between XLSX and XLSB**. Var och en av dessa bygger på samma Aspose.Cells‑API som du just använde, så du kan utöka lösningen utan att lära dig nya bibliotek.

Känn dig fri att experimentera med olika datatyper, flera arbetsblad eller lösenordsskydd—Aspose.Cells stödjer alla dessa scenarier direkt. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Create Save Excel Workbook Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}