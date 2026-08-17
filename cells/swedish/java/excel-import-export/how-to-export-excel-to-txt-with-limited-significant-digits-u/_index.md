---
category: general
date: 2026-08-17
description: Exportera Excel till TXT samtidigt som du begränsar signifikanta siffror
  – lär dig hur du ställer in siffror och konverterar Excel till text i Java med ett
  komplett Aspose.Cells‑exempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: sv
lastmod: 2026-08-17
og_description: Exportera Excel till TXT samtidigt som du begränsar signifikanta siffror.
  Denna handledning visar hur du ställer in siffror och konverterar Excel till text
  med Aspose.Cells för Java.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: Exportera Excel till TXT med begränsat antal signifikanta siffror – Java‑guide
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: Hur man exporterar Excel till TXT med begränsat antal signifikanta siffror
  med Java
url: /sv/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera Excel till TXT med begränsat antal signifikanta siffror med Java

Om du behöver **exportera Excel till TXT** samtidigt som du styr antalet signifikanta siffror, ger den här guiden en färdig lösning. Du får se hur du anger siffror, konverterar Excel till text och håller utdata prydlig med en enda konfigurationsändring.

Exemplet använder Aspose.Cells for Java 25.10, som introducerar alternativet `setSignificantDigits`. När du är klar med tutorialen kan du generera en TXT‑fil som bara innehåller de siffror du vill ha, utan extra avrundningskod.

## Vad du kommer att uppnå

- Skapa en arbetsbok programatiskt.
- Infoga ett numeriskt värde i en cell.
- Konfigurera TXT‑spara‑alternativ för att begränsa signifikanta siffror.
- Spara arbetsboken som en ren‑text‑fil.
- Förstå hur inställningen `significantDigits` fungerar och hur du anpassar den för andra scenarier.

### Förutsättningar

- Java 17 eller senare (koden kompileras även med Java 8).
- Aspose.Cells for Java 25.10 eller nyare. Ladda ner JAR‑filen från [Aspose‑webbplatsen](https://products.aspose.com/cells/java) och lägg till den i ditt projekts classpath.
- En IDE eller en enkel textredigerare och ett byggverktyg för kommandoraden (Maven/Gradle).

## Steg 1: Ställ in projektet och importera Aspose.Cells

Skapa ett nytt Java‑projekt och lägg till Aspose.Cells‑JAR‑filen i byggsökvägen. Om du använder Maven, lägg till följande beroende i `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Proffstips:** Använd `jdk17`‑klassificeraren för den senaste Java‑runtime‑miljön; den minskar risken för kompatibilitetsvarningar.

## Steg 2: Skapa en arbetsbok och skriv ett värde

Arbetsboken representerar en Excel‑fil i minnet. Du kan lägga till data i vilken cell som helst med metoden `putValue`.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

Numret `123.456789` blir källan för vår TXT‑export. Som standard skulle Aspose.Cells skriva alla decimaler, vilket ofta ger bullriga textfiler.

## Steg 3: Konfigurera TXT‑spara‑alternativ för att begränsa signifikanta siffror

Aspose.Cells tillhandahåller `TxtSaveOptions` för fin‑inställning av ren‑text‑utdata. Metoden `setSignificantDigits` talar om för exportören hur många siffror som ska behållas **totalt**, inte bara efter decimalpunkten.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

När `significantDigits` är satt till `4` avrundar exportören värdet `123.456789` till `123.5`. Detta beteende motsvarar den matematiska definitionen av signifikanta siffror: de fyra första icke‑noll siffrorna behålls.

### Hur inställningen skiljer sig från “begränsa decimaler”

- **begränsa decimaler** (`setDecimalPlaces`) tar bort siffror *efter* decimalpunkten, oavsett heltalsdelen.
- **signifikanta siffror** (`setSignificantDigits`) räknar siffror från den första icke‑noll siffran, vilket är användbart när tal varierar i storlek.

Om du istället behöver ett fast antal decimaler, ersätt raden ovan med:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Steg 4: Spara arbetsboken som en TXT‑fil

Skriv nu arbetsboken till disk med de konfigurerade alternativen.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

När programmet körs skapas `significant_digits.txt` i arbetskatalogen. Filen innehåller en enda rad:

```
123.5
```

### Förväntad utdata

| Cell | Ursprungligt värde | Exporterat (4 signifikanta siffror) |
|------|--------------------|------------------------------------|
| A1   | 123.456789         | 123.5                              |

Om du ändrar `setSignificantDigits(4)` till `6` blir utdata `123.457`. Prova olika värden för att se hur avrundningen anpassas.

## Steg 5: Vanliga variationer och kantfall

### Exportera ett helt område

Om du vill exportera mer än en cell, fyll helt enkelt området innan du sparar:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

Samma `significantDigits`‑inställning gäller för varje numerisk cell, vilket säkerställer enhetlig precision i hela filen.

### Hantera localespecifika decimalavgränsare

Aspose.Cells respekterar system‑locale när text skrivs. För att tvinga en punkt (`.`) som decimalavgränsare, ange kultur för `TxtSaveOptions`:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

Detta är praktiskt när målprogrammet förväntar ett specifikt format, exempelvis CSV‑tolkare som bara accepterar `.`.

### Skriva över befintliga filer

Metoden `save` skriver över målfilen som standard. Om du vill undvika oavsiktlig dataförlust, kontrollera först om filen finns:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Stora arbetsböcker och minnesanvändning

När du exporterar mycket stora kalkylblad, överväg att strömma utdata:

```java
saveOptions.setEnableMemorySaving(true);
```

Detta alternativ minskar heap‑förbrukningen genom att skriva rader inkrementellt.

## Fullständigt fungerande exempel

Nedan är hela programmet som du kan kopiera, klistra in och köra direkt:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

När du kör koden får du `significant_digits.txt` med följande innehåll (tab‑separerade kolumner):

```
123.5	0.001235	98770
```

Varje tal följer regeln **4 signifikanta siffror**, vilket visar att inställningen fungerar över olika storlekar.

## Slutsats

Du vet nu hur du **exporterar Excel till TXT** samtidigt som du styr antalet signifikanta siffror. Genom att använda `TxtSaveOptions.setSignificantDigits` kan du **ange siffror**, **begränsa decimaler** och **begränsa signifikanta siffror** i en enda, underhållbar rad kod. Metoden fungerar för enskilda celler, hela områden och stora arbetsböcker.

### Nästa steg

- Utforska andra egenskaper i `TxtSaveOptions` såsom `setDelimiter('\t')` för att anpassa kolumnseparatorer.
- Kombinera exportören med `CsvSaveOptions` om du behöver kommaseparerade värden istället för ren text.
- Integrera rutinen i en webbtjänst som tar emot uppladdade Excel‑filer och returnerar trimmad TXT‑utdata i realtid.

Känn dig fri att experimentera med olika siffersättningar och locales. Om du stöter på ett scenario där de inbyggda alternativen inte uppfyller ett speciellt krav, kan du alltid efterbehandla den genererade TXT‑filen med vanliga Java‑I/O‑verktyg.

Lycka till med kodandet!


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra fler API‑funktioner och utforska alternativa implementeringssätt i dina egna projekt.

- [Hur man konverterar text till tal i Excel med Aspose.Cells for Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [Hur man skapar och exporterar Excel till HTML med Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Hur man exporterar anpassade Excel‑egenskaper till PDF med Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}