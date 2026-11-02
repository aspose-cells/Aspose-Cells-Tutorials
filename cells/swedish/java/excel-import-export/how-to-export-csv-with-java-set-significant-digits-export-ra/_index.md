---
category: general
date: 2026-03-01
description: Lär dig hur du exporterar CSV från en Java‑arbetsbok samtidigt som du
  ställer in signifikanta siffror och exportintervall till CSV i en enda, tydlig guide.
draft: false
keywords:
- how to export csv
- set significant digits
- export range to csv
- Java workbook export
- CSV formatting Java
language: sv
og_description: Behärska hur du exporterar CSV i Java, ställer in signifikanta siffror
  och exporterar intervall till CSV med praktisk kod och tips.
og_title: Hur man exporterar CSV med Java – Fullständig steg‑för‑steg‑guide
tags:
- Java
- Aspose.Cells
- CSV
- Data Export
title: Hur man exporterar CSV med Java – Ställ in signifikanta siffror och exportera
  intervall till CSV
url: /sv/java/excel-import-export/how-to-export-csv-with-java-set-significant-digits-export-ra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man exporterar CSV med Java – Ställ in signifikanta siffror & exportera område till CSV

Har du någonsin undrat **hur man exporterar csv** från en Java-arbetsbok utan att förlora numerisk precision? Kanske har du provat en snabb `toString()` och hamnat i en röra av avrundningsfel. Det är ett vanligt problem, särskilt när du behöver **ställa in signifikanta siffror** för finansiella data eller vetenskapliga resultat.  

I den här handledningen får du se ett komplett, färdigt‑att‑köra exempel som visar **hur man exporterar csv**, hur man **ställer in signifikanta siffror**, och till och med hur man **exporterar område till csv** samtidigt som du håller dina data prydliga. Vi går igenom varje rad, förklarar *varför* bakom API‑anropen och ger dig tips för att undvika de vanliga fallgroparna. Inga extra dokument att jaga—bara en självständig lösning du kan kopiera‑klistra in idag.

## Vad du kommer att lära dig

- Skapa en arbetsbok och konfigurera numerisk precision med `setNumberSignificantDigits`.
- Exportera ett specifikt cellområde som en snyggt formaterad CSV-sträng.
- Analysera japanska era‑datum med `DateTimeFormatInfo`.
- Räkna om formler så dynamiska‑arrayresultat hålls aktuella.
- Rendera en pivottabell till en PNG‑bild.
- Använd Smart Marker för att injicera kommentarer och slutligen spara arbetsboken.

Allt detta görs med Aspose.Cells för Java‑biblioteket, version 23.12 (den senaste vid skrivtillfället). Om du har JAR‑filen på din classpath är du redo att köra.

---

## Steg 1: Skapa en arbetsbok och **ställ in signifikanta siffror**

Innan vi kan exportera något behöver vi ett arbetsboksobjekt. Det första många utvecklare förbiser är numerisk precision. Som standard använder Aspose.Cells full dubbelprecision, vilket kan leda till långa, otympliga strängar i CSV. Genom att ange antalet signifikanta siffror trimmas utskriften samtidigt som de viktigaste siffrorna bevaras.

```java
import com.aspose.cells.*;

public class CsvExportDemo {

    public static void main(String[] args) throws Exception {

        // Step 1 – initialise workbook and limit numeric values to 5 significant digits
        Workbook workbook = new Workbook();
        WorkbookSettings settings = workbook.getSettings();
        // This is the key call that **set significant digits** for all numeric cells
        settings.setNumberSignificantDigits(5);
```

**Varför är detta viktigt?**  
Om du exporterar en cell som innehåller `12345.6789` utan att begränsa siffror kommer CSV‑filen att visa hela värdet, vilket rör till rapporterna. Med `setNumberSignificantDigits(5)` blir samma cell `12346`, vilket ofta är vad affärsanvändare förväntar sig.

> **Proffstips:** Om du behöver olika precision per kolumn kan du använda en anpassad `Style` istället för den globala inställningen.

---

## Steg 2: **Exportera område till CSV** – Formatering är viktigt

Nu när arbetsboken är klar, låt oss hämta ett rektangulärt block med data och omvandla det till en CSV‑sträng. Vi kommer också att tvinga fram ett två‑decimalformat (`0.00`) så att varje tal hamnar snyggt i linje.

```java
        // Step 2 – define export options and pull the range B2:D10 as CSV
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);          // we want a string, not a file yet
        exportOptions.setNumberFormat("0.00");          // enforce two decimal places

        // Create a dummy range with some sample data for illustration
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
        cells.get("B2").putValue(123.456);
        cells.get("C2").putValue(78.9);
        cells.get("D2").putValue(0.12345);
        // ... populate more rows as needed ...

        Range dataRange = cells.createRange("B2:D10");
        String csvData = dataRange.exportDataTable(exportOptions).toString();

        System.out.println("=== CSV Output ===");
        System.out.println(csvData);
```

Anropet `exportDataTable` gör det tunga arbetet. Eftersom vi satte `exportAsString` returnerar metoden en `String` som vi kan skriva ut, spara till en fil eller skicka via HTTP. Steget **exportera område till csv** respekterar också den globala `setNumberSignificantDigits` som vi definierade tidigare, så siffrorna både avrundas till fem signifikanta siffror *och* visas med två decimaler.

**Förväntad output (avkortad):**

```
=== CSV Output ===
123.46,78.90,0.12
...
```

> **Vanlig fråga:** *Vad händer om jag behöver ett annat avgränsningstecken, som ett semikolon?*  
> Anropa helt enkelt `exportOptions.setSeparator(";")` innan export.

---

## Steg 3: Analysera ett japanskt era‑datum (bonusverktyg)

Även om det inte är direkt relaterat till CSV innehåller många Excel‑ark lokalspecifika datum. Så här kan du omvandla en japansk era‑sträng som `"R3/04/01"` till ett standard‑`DateTime`‑objekt.

```java
        // Step 3 – parse Japanese era date (Reiwa 3)
        DateTime japaneseDate = DateTime.parse("R3/04/01", new DateTimeFormatInfo(Locale.JAPAN));
        System.out.println("Parsed Japanese date: " + japaneseDate);
```

Utdata:

```
Parsed Japanese date: 2021-04-01T00:00:00
```

**Varför inkludera detta?**  
Om din CSV‑export matar nerströmsystem som förväntar sig ISO‑8601‑datum, måste du först normalisera eventuella lokala format. Detta kodsnutt visar *hur* och *varför* på ett och samma ställe.

---

## Steg 4: Räkna om formler – håll dynamiska‑arrayresultat färska

Om din arbetsbok innehåller formler (t.ex. `=SUM(A1:A10)`) uppdateras de inte automatiskt efter att vi ändrat inställningarna. Att anropa `calculateFormula` tvingar en fullständig omräkning, vilket säkerställer att den exporterade CSV‑filen speglar de senaste värdena.

```java
        // Step 4 – recalculate all formulas
        workbook.calculateFormula();
```

> **Observera:** Stora arbetsböcker kan ta märkbar tid att räkna om. För prestandakritiska scenarier, överväg `calculateFormula(FormulaCalculationOptions)` för att begränsa omfattningen.

---

## Steg 5: Rendera den första pivottabellen till en PNG‑bild

Ibland behöver du en visuell ögonblicksbild av en pivottabell tillsammans med CSV‑filen. Följande kod renderar den första pivottabellen på det första kalkylbladet till en PNG‑fil.

```java
        // Step 5 – render pivot table as PNG
        PivotTable pivot = sheet.getPivotTables().get(0); // assumes a pivot exists
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.Png);
        // The range that the pivot occupies is turned into an image
        pivot.getRange().toImage("output/pivot.png", imgOptions);
```

**Tips:** Om arbetsboken ännu inte innehåller en pivottabell kan du skapa en programatiskt—se Aspose.Cells‑dokumentationen för ett snabbt exempel.

---

## Steg 6: Använd Smart Marker för att skriva en kommentar och spara arbetsboken

Smart Marker låter dig injicera dynamiskt innehåll i celler med enkla platshållare. Här skriver vi en kommentar som “Reviewed by QA” i en bestämd cell och sparar sedan arbetsboken.

```java
        // Step 6 – apply Smart Marker comment
        SmartMarkerProcessor smartMarker = new SmartMarkerProcessor(workbook);
        smartMarker.apply("${Comment}", java.util.Collections.singletonMap("Comment", "Reviewed by QA"));

        // Finally, save the workbook with the comment embedded
        workbook.save("output/commented.xlsx");
    }
}
```

`${Comment}`‑platshållaren kan placeras var som helst i bladet (t.ex. cell `A1`). När `apply` körs ersätts platshållaren med det angivna värdet.

**Resultat:**  
Du hittar en `output/commented.xlsx`‑fil som innehåller kommentaren, plus den tidigare genererade `pivot.png` och CSV‑strängen som skrivs ut i konsolen.

---

## Fullständigt fungerande exempel

Sätter vi ihop allt får du det kompletta programmet som du kan kompilera och köra:

```java
import com.aspose.cells.*;
import java.util.Collections;
import java.util.Locale;

public class CsvExportDemo {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Workbook & Significant Digits -----------
        Workbook workbook = new Workbook();
        WorkbookSettings settings = workbook.getSettings();
        settings.setNumberSignificantDigits(5); // **set significant digits**

        // ----------- Step 2: Populate Sample Data & Export CSV ----------
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
        cells.get("B2").putValue(123.456);
        cells.get("C2").putValue(78.9);
        cells.get("D2").putValue(0.12345);
        // (Add more rows if you like)

        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setNumberFormat("0.00");
        Range dataRange = cells.createRange("B2:D10");
        String csvData = dataRange.exportDataTable(exportOptions).toString();

        System.out.println("=== CSV Output ===");
        System.out.println(csvData);

        // ----------- Step 3: Japanese Era Date ----------
        DateTime japaneseDate = DateTime.parse("R3/04/01", new DateTimeFormatInfo(Locale.JAPAN));
        System.out.println("Parsed Japanese date: " + japaneseDate);

        // ----------- Step 4: Recalculate Formulas ----------
        workbook.calculateFormula();

        // ----------- Step 5: Render Pivot Table ----------
        if (!sheet.getPivotTables().isEmpty()) {
            PivotTable pivot = sheet.getPivotTables().get(0);
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.Png);
            pivot.getRange().toImage("output/pivot.png", imgOptions);
        }

        // ----------- Step 6: Smart Marker Comment ----------
        SmartMarkerProcessor smartMarker = new SmartMarkerProcessor(workbook);
        smartMarker.apply("${Comment}", Collections.singletonMap("Comment", "Reviewed by QA"));
        workbook.save("output/commented.xlsx");
    }
}
```

### Förväntad konsolutdata

```
=== CSV Output ===
123.46,78.90,0.12
...
Parsed Japanese date: 2021-04-01T00:00:00
```

Du hittar också `output/pivot.png` (om en pivottabell fanns) och `output/commented.xlsx` på disken.

---

## Vanliga frågor & specialfall

- **Kan jag exportera till en fysisk CSV‑fil direkt?**  
  Ja. Byt ut `exportAsString`‑blocket mot `dataRange.exportDataTable("output/data.csv", exportOptions);`.

- **Vad händer om mitt blad använder en annan lokal för siffror?**  
  Sätt `exportOptions.setCultureInfo(new CultureInfo("fr-FR"))` innan export; detta kommer att byta

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}