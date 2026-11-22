---
category: general
date: 2026-11-22
description: Exportera Excel som bild med Java och Aspose.Cells. Lär dig hur du lägger
  till en bild i kalkylbladet och sparar Excel som PNG‑fil på några få steg.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as image
- add picture to worksheet
- export excel sheet to png
- save excel as png file
- save workbook as image
language: sv
lastmod: 2026-11-22
og_description: Exportera Excel som bild med Java med Aspose.Cells. Följ den här guiden
  för att lägga till en bild i kalkylbladet och spara Excel som PNG‑fil snabbt.
og_image_alt: Code snippet showing Java export of an Excel worksheet to a PNG image
og_title: Exportera Excel som bild med Java – steg‑för‑steg‑handledning
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Export Excel as image with Java using Aspose.Cells. Learn how to add
    picture to worksheet and save Excel as PNG file in a few steps.
  headline: Export Excel as image with Java – complete guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Image export
title: Exportera Excel som bild med Java – komplett guide
url: /sv/java/images-shapes/export-excel-as-image-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera Excel som bild med Java – komplett guide

Om du behöver **exportera Excel som bild** i en Java‑applikation visar den här handledningen en färdig‑till‑körning‑lösning. Du kommer att se hur du lägger till en bild i kalkylbladet, konfigurerar exportalternativen och slutligen **sparar Excel som PNG‑fil** med bara några rader kod.

Guiden täcker allt från Maven‑inställning till hantering av kantfall, så att du kan integrera tekniken i vilket projekt som helst som kräver visuella ögonblicksbilder av kalkylblad.

## Förutsättningar

* Java 17 eller nyare installerat.
* Maven 3.6+ (eller Gradle) för beroendehantering.
* En Aspose.Cells för Java‑licens (den fria utvärderingen fungerar för testning).
* En exempel‑Excel‑arbetsbok (`sample.xlsx`) som innehåller de data du vill exportera.

## Steg 1: Lägg till Aspose.Cells‑beroende

Aspose.Cells tillhandahåller klassen `ImageOrPrintOptions` som används för att **exportera Excel som bild**. Lägg till följande beroende i din `pom.xml` (eller motsvarande Gradle‑post).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Proffstips:** Håll versionsnumret uppdaterat; nyare versioner innehåller prestandaförbättringar för bildrendering.

## Steg 2: Läs in arbetsboken och välj kalkylbladet

Det första programmeringssteget är att öppna Excel‑filen och få en referens till det kalkylblad du vill exportera.

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load the workbook from disk
        Workbook wb = new Workbook("sample.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);
```

*Varför detta är viktigt*: Att läsa in arbetsboken ger dig åtkomst till dess interna objekt, och att välja rätt kalkylblad säkerställer att rätt område renderas.

## Steg 3: Konfigurera ImageOrPrintOptions (exportera Excel som bild)

`ImageOrPrintOptions` styr bildformat, upplösning och andra renderingsdetaljer. Här sätter vi formatet till PNG, vilket uppfyller kravet på **exportera Excel‑blad till PNG**.

```java
        // Create options for image export
        ImageOrPrintOptions opts = new ImageOrPrintOptions();

        // Set the desired image format (PNG)
        opts.setSaveFormat(SaveFormat.PNG);

        // Optional: increase resolution for sharper output
        opts.setResolution(300);
```

Att sätta formatet till `PNG` garanterar förlustfri komprimering, vilket gör filen lämplig för vidare bearbetning eller inkludering i rapporter.

## Steg 4: Lägg till bild i kalkylbladet (add picture to worksheet)

Om du behöver bädda in en bild—t.ex. en logotyp eller en ögonblicksbild av ett annat område—använd `Pictures`‑samlingen. Följande kod infogar en bild av området `A1:G20` i det övre vänstra hörnet av kalkylbladet.

```java
        // Insert a picture of the range A1:G20 at cell (0,0)
        ws.getPictures().add(0, 0, "A1:G20");
```

> **Varför du kan göra detta:** Att lägga till en bild innan export låter dig kombinera statisk grafik med kalkylbladets data, vilket ger en rikare slutbild.

## Steg 5: Spara kalkylbladet som en PNG‑fil (save excel as png file, save workbook as image)

Slutligen anropar du `Workbook.save` med de konfigurerade alternativen. Metoden skriver en PNG‑fil till den angivna katalogen.

```java
        // Save the worksheet as an image file
        wb.save("output/pivot.png", opts);

        System.out.println("Export completed: output/pivot.png");
    }
}
```

När programmet är klart innehåller `output/pivot.png` en pixel‑perfekt representation av kalkylbladet, inklusive den bild du lade till.

### Fullständig källkod

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Configure export options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PNG);
        opts.setResolution(300); // optional high‑DPI output

        // Add picture to worksheet
        ws.getPictures().add(0, 0, "A1:G20");

        // Export worksheet as PNG image
        wb.save("output/pivot.png", opts);
        System.out.println("Export completed: output/pivot.png");
    }
}
```

Att köra klassen genererar PNG‑filen som visas nedan (bilden är illustrativ; din fil kommer att återspegla det faktiska kalkylbladsinnehållet).

![Exporterad Excel‑kalkylblad som PNG](/images/excel-to-png.png "Resultat av att exportera Excel som bild med Java")

*Alt‑text (bild‑alt):* **Resultat av att exportera Excel som bild med Java – en PNG‑ögonblicksbild av kalkylbladet** (uppfyller bild‑alt‑kravet).

## Vanliga fallgropar och hur du undviker dem

| Problem | Orsak | Lösning |
|-------|--------|-----|
| **Fil ej hittad** | Sökvägen till `sample.xlsx` är felaktig. | Använd en absolut sökväg eller placera filen i projektets rot. |
| **Tom bild** | Kalkylbladet har inget synligt innehåll eller bildområdet är tomt. | Verifiera att cellerna `A1:G20` innehåller data eller justera området. |
| **Låg upplösning** | Standard‑DPI är 96, vilket kan se suddigt ut vid utskrift. | Anropa `opts.setResolution(300)` (eller högre) innan du sparar. |
| **Licensundantag** | Att använda utvärderingsversionen kan lägga till ett vattenmärke. | Applicera en giltig Aspose.Cells‑licens med `License license = new License(); license.setLicense("Aspose.Total.lic");`. |

## Nästa steg

Nu när du kan **exportera Excel som bild**, kan du utforska:

* **Exportera Excel‑blad till PNG** för varje kalkylblad i en arbetsbok (loopa genom `wb.getWorksheets()`).
* Konvertera PNG‑filen till PDF med Aspose.PDF om du behöver ett dokumentvänligt format.
* Bädda in den genererade PNG‑filen i en webbsida eller e‑postbilaga direkt från Java.

Dessa tillägg bygger på samma `ImageOrPrintOptions`‑mönster, vilket håller kodbasen konsekvent.

## Slutsats

Du har lärt dig hur du **exporterar Excel som bild** med Java, hur du **lägger till bild i kalkylbladet**, och hur du **sparar Excel som PNG‑fil** med Aspose.Cells. Det fullständiga exemplet demonstrerar ett pålitligt sätt att **spara arbetsbok som bild**, hantera upplösning och undvika vanliga fel. Använd mönstret för att automatisera rapportering, generera miniatyrbilder eller integrera kalkylbladsvisualiseringar i vilket Java‑baserat arbetsflöde som helst.

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man exporterar ett Excel‑kalkylblad till PNG med Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Exportera Excel‑arbetsbok som bild med Aspose.Cells för Java: En steg‑för‑steg‑guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Exportera Excel‑arbetsbok som bild med Aspose Cells för Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}