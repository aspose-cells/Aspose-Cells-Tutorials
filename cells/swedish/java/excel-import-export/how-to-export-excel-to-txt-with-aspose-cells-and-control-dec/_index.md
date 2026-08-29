---
category: general
date: 2026-08-20
description: Lär dig att exportera Excel till TXT samtidigt som du begränsar antalet
  decimaler, behåller signifikanta siffror och sparar arbetsboken som TXT med Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: sv
lastmod: 2026-08-20
og_description: Exportera Excel till TXT med Aspose.Cells. Denna guide visar hur du
  begränsar decimaler, behåller signifikanta siffror och sparar arbetsboken som TXT
  i Java.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: Exportera Excel till TXT i Java – kontrollera decimalplatser och signifikanta
  siffror
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Hur man exporterar Excel till TXT med Aspose.Cells och styr decimalprecision
url: /sv/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så exporterar du Excel till TXT med Aspose.Cells och kontrollerar decimalprecision

Om du behöver **exportera Excel till TXT** och säkerställa att utdata följer ett specifikt antal decimaler, ger den här guiden en komplett lösning. Du kommer att se hur du begränsar decimaler, behåller signifikanta siffror och **sparar arbetsbok som TXT** med hjälp av Aspose.Cells‑biblioteket för Java.

Handledningen går igenom att skapa en arbetsbok, infoga ett högprecisionsvärde, konfigurera TXT‑sparalternativen och skriva filen till disk. I slutet kan du generera en textfil som innehåller exakt den precision du kräver, utan manuell efterbehandling.

## Vad du behöver

- Java 17 (eller någon annan stödd JDK)
- Aspose.Cells för Java 23.10 eller nyare
- En IDE eller byggverktyg (Maven/Gradle) för att hantera beroenden
- Skrivbehörighet till mål‑katalogen

## Steg 1: Skapa en arbetsbok och få åtkomst till det första kalkylbladet

Att skapa en arbetsbok är det första steget när du vill **exportera Excel till TXT**. Klassen `Workbook` representerar hela Excel‑filen, och `Worksheet` ger dig åtkomst till celler.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Varför detta är viktigt*: Arbetsboksobjektet innehåller all data, stilar och metadata. Att börja med en ny arbetsbok garanterar att ingen dold formatering stör textexporten.

## Steg 2: Lägg till ett numeriskt värde och begränsa decimaler

Infoga ett tal med många decimaler så att du kan demonstrera hur du **begränsar decimaler** vid export.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*Varför detta är viktigt*: Excel lagrar full precision, men när du senare exporterar kan du vilja trunkera eller avrunda värdet. Inställningen `limit decimal places` hanterar detta automatiskt.

## Steg 3: Konfigurera TXT‑sparalternativ för att behålla signifikanta siffror

Aspose.Cells tillhandahåller `TxtSaveOptions`. Genom att sätta `significantDigits` instrueras exportören att behålla endast det erforderliga antalet meningsfulla siffror, och ignorera inledande nollor.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*Varför detta är viktigt*: Alternativet **keep significant digits** säkerställer att utdatafilen innehåller en förutsägbar mängd precision, vilket är avgörande för efterföljande system som förväntar sig ett fast bredd‑numeriskt format.

## Steg 4: Spara arbetsboken som TXT

Slutligen skriver du arbetsboken till en textfil. Metoden `save` respekterar de alternativ du konfigurerat, så den resulterande filen kommer att innehålla den begränsade decimalrepresentationen.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*Varför detta är viktigt*: Att använda **save workbook as txt** med de förberedda `TxtSaveOptions` garanterar att den exporterade filen matchar de precision‑restriktioner du satte i föregående steg.

### Förväntat innehåll i `SignificantDigits.txt`

```
0.00012346
```

Värdet visar fem signifikanta siffror (`12346`) efter avrundning, och de inledande nollorna bevaras enligt TXT‑formatet.

## Variationer och specialfall

| Scenario | Justering |
|----------|------------|
| **Olika antal signifikanta siffror** | Anropa `txtOptions.setSignificantDigits(n)` där `n` är 1‑15. |
| **Exportera ett område istället för hela bladet** | Använd `txtOptions.setExportRange("A1:B10")` innan du sparar. |
| **Bevara kolumnseparatorer** | Ställ in `txtOptions.setSeparator('\t')` för tab‑avgränsad output. |
| **Stora kalkylblad** | Öka `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` för att undvika `OutOfMemoryError`. |

## Vanliga fallgropar och pro‑tips

- **Förväxla inte signifikanta siffror med decimaler**. Inledande nollor räknas inte som signifikanta; använd `setSignificantDigits` för meningsfull precision och `setDecimalPlaces` om du behöver ett fast antal siffror efter decimaltecknet.
- **Ange alltid en absolut utdataväg** när du kör från en IDE för att undvika behörighetsfel.
- **Validera den genererade filen** med ett enkelt anrop `java.nio.file.Files.readAllLines(Paths.get(outputPath))` för att säkerställa att innehållet matchar förväntningarna innan du skickar det till efterföljande processer.

## Fullständig källkod för referens

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

När programmet körs genereras `SignificantDigits.txt` som innehåller den enda raden `0.00012346`, vilket visar att processen **export excel to txt** respekterar både kraven **limit decimal places** och **keep significant digits**.

## Slutsats

Du vet nu hur du **exporterar Excel till TXT** med Aspose.Cells för Java samtidigt som du kontrollerar numerisk precision. Genom att konfigurera `TxtSaveOptions` kan du **begränsa decimaler**, **behålla signifikanta siffror**, och på ett pålitligt sätt **spara arbetsbok som txt** utan extra efterbehandling.

Nästa steg kan du utforska:

- Exportera flera blad till separata TXT‑filer (`save workbook as txt` per blad)
- Använda `setSeparator` för att skapa CSV‑kompatibel output
- Automatisera batch‑konverteringar för stora datamängder

Känn dig fri att experimentera med olika antal siffror och separatorer för att passa ditt projekts exakta behov. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur man skapar och exporterar Excel till HTML med Aspose.Cells Java \| Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Spara Excel som text – Komplett C#‑guide för att exportera Excel till TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Exportera Excel‑arbetsbok som bild med Aspose.Cells för Java: En steg‑för‑steg‑guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}