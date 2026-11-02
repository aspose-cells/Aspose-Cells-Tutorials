---
category: general
date: 2026-08-20
description: Leer hoe je Excel naar TXT exporteert, terwijl je het aantal decimalen
  beperkt, significante cijfers behoudt en de werkmap als TXT opslaat met Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: nl
lastmod: 2026-08-20
og_description: Exporteer Excel naar TXT met Aspose.Cells. Deze gids laat zien hoe
  je decimalen kunt beperken, significante cijfers kunt behouden en een werkmap als
  TXT kunt opslaan in Java.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: Excel naar TXT exporteren in Java – decimale plaatsen en significante cijfers
  regelen
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
title: Hoe Excel exporteren naar TXT met Aspose.Cells en de decimale precisie regelen
url: /nl/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Excel naar TXT exporteren met Aspose.Cells en decimale precisie beheersen

Als je **Excel naar TXT moet exporteren** en wilt dat de output een specifiek aantal decimalen respecteert, biedt deze gids een volledige oplossing. Je ziet hoe je decimalen kunt beperken, significante cijfers kunt behouden, en **werkmap opslaan als TXT** met behulp van de Aspose.Cells‑bibliotheek voor Java.

De tutorial loopt door het maken van een werkmap, het invoegen van een hoge‑precisie waarde, het configureren van de TXT‑opslaan‑opties, en het schrijven van het bestand naar schijf. Aan het einde kun je een tekstbestand genereren dat precies de precisie bevat die je nodig hebt, zonder handmatige nabewerking.

## Wat je nodig hebt

- Java 17 (of een ondersteunde JDK)
- Aspose.Cells for Java 23.10 of nieuwer
- Een IDE of build‑tool (Maven/Gradle) om afhankelijkheden te beheren
- Schrijfrechten voor de doelmap

## Stap 1: Maak een werkmap en krijg toegang tot het eerste werkblad

Een werkmap maken is de eerste stap wanneer je **Excel naar TXT wilt exporteren**. De `Workbook`‑klasse vertegenwoordigt het volledige Excel‑bestand, en `Worksheet` geeft je toegang tot cellen.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Waarom dit belangrijk is*: Het werkmap‑object bevat alle gegevens, stijlen en metadata. Beginnen met een nieuwe werkmap garandeert dat er geen verborgen opmaak de tekst‑export beïnvloedt.

## Stap 2: Voeg een numerieke waarde toe en beperk decimalen

Voeg een getal in dat veel decimalen heeft zodat je kunt demonstreren hoe je **decimalen kunt beperken** tijdens het exporteren.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*Waarom dit belangrijk is*: Excel slaat de volledige precisie op, maar bij het later exporteren wil je de waarde mogelijk afkappen of afronden. De instelling `limit decimal places` handelt dit automatisch af.

## Stap 3: Configureer TXT‑opslaan‑opties om significante cijfers te behouden

Aspose.Cells biedt `TxtSaveOptions`. Het instellen van `significantDigits` vertelt de exporter om alleen het vereiste aantal betekenisvolle cijfers te behouden, waarbij voorloopnullen worden genegeerd.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*Waarom dit belangrijk is*: De optie **keep significant digits** zorgt ervoor dat het uitvoerbestand een voorspelbare hoeveelheid precisie bevat, wat essentieel is voor downstream‑systemen die een vaste‑breedte numeriek formaat verwachten.

## Stap 4: Sla de werkmap op als TXT

Schrijf tenslotte de werkmap naar een tekstbestand. De `save`‑methode respecteert de opties die je hebt geconfigureerd, zodat het resulterende bestand de beperkte decimale weergave bevat.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*Waarom dit belangrijk is*: Het gebruik van **save workbook as txt** met de voorbereide `TxtSaveOptions` garandeert dat het geëxporteerde bestand overeenkomt met de precisiebeperkingen die je in de vorige stap hebt ingesteld.

### Verwachte inhoud van `SignificantDigits.txt`

```
0.00012346
```

De waarde toont vijf significante cijfers (`12346`) na afronding, en de voorloopnullen worden behouden volgens het TXT‑formaat.

## Variaties en randgevallen

| Scenario | Aanpassing |
|----------|------------|
| **Verschillend aantal significante cijfers** | Call `txtOptions.setSignificantDigits(n)` where `n` is 1‑15. |
| **Een bereik exporteren in plaats van het hele blad** | Use `txtOptions.setExportRange("A1:B10")` before saving. |
| **Kolomscheidingstekens behouden** | Set `txtOptions.setSeparator('\t')` for tab‑delimited output. |
| **Grote werkbladen** | Increase `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` to avoid `OutOfMemoryError`. |

## Veelvoorkomende valkuilen en pro‑tips

- **Verwar significante cijfers niet met decimalen**. Voorloopnullen worden niet meegeteld als significant; gebruik `setSignificantDigits` voor betekenisvolle precisie en `setDecimalPlaces` als je een vast aantal cijfers na de decimale punt nodig hebt.
- **Geef altijd een absoluut uitvoerpad op** bij het uitvoeren vanuit een IDE om permissiefouten te voorkomen.
- **Valideer het gegenereerde bestand** met een eenvoudige `java.nio.file.Files.readAllLines(Paths.get(outputPath))`‑aanroep om te verzekeren dat de inhoud voldoet aan de verwachtingen voordat je het aan downstream‑processen doorgeeft.

## Volledige broncode ter referentie

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

Het uitvoeren van het programma produceert `SignificantDigits.txt` met de enkele regel `0.00012346`, wat aantoont dat het **export excel to txt**‑proces zowel de **limit decimal places**‑ als de **keep significant digits**‑vereisten respecteert.

## Conclusie

Je weet nu hoe je **Excel naar TXT kunt exporteren** met Aspose.Cells voor Java terwijl je de numerieke precisie beheerst. Door `TxtSaveOptions` te configureren kun je **decimalen beperken**, **significante cijfers behouden**, en betrouwbaar **werkmap opslaan als txt** zonder extra nabewerking.

Vervolgens kun je verkennen:

- Meerdere bladen exporteren naar afzonderlijke TXT‑bestanden (`save workbook as txt` per blad)
- Gebruik `setSeparator` om CSV‑compatibele output te maken
- Automatiseren van batch‑conversies voor grote datasets

Voel je vrij om te experimenteren met verschillende aantallen cijfers en scheidingstekens om aan de exacte behoeften van je project te voldoen. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe Excel maken en exporteren naar HTML met Aspose.Cells Java \| Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Excel opslaan als tekst – Complete C#‑gids voor exporteren van Excel naar TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Excel‑werkmap exporteren als afbeelding met Aspose.Cells voor Java: Een stap‑voor‑stap gids](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}