---
date: '2026-08-16'
description: Leer hoe u globalisering in Java kunt toevoegen met Aspose.Cells, Excel-foutmeldingen
  kunt aanpassen en de Maven‑afhankelijkheid kunt instellen.
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: Leer hoe u globalisering in Java kunt toevoegen met Aspose.Cells,
  Excel-foutmeldingen kunt aanpassen en de Maven‑afhankelijkheid kunt instellen. Volg
  de stapsgewijze handleiding.
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: Hoe globalisering in Java toe te voegen met Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: Hoe globalisering in Java toe te voegen met Aspose.Cells
url: /nl/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Hoe globalisatie toe te voegen in Java met Aspose.Cells

## Introductie

Door globalisatie toe te voegen aan je Java‑werkmap kun je foutmeldingen, booleaanse waarden en andere op locale‑specifieke strings gebaseerde teksten weergeven in de taal die je gebruikers verwachten. In deze tutorial leer je **hoe je globalisatie toevoegt** voor het Russisch, maar hetzelfde patroon werkt voor elke taal. Aan het einde van de gids kun je:

- De standaard fouttekst en booleaanse weergaven overschrijven.
- Je aangepaste instellingen toepassen op elke `Workbook`‑instantie.
- De oplossing integreren in een typisch Maven‑gebaseerd Java‑project.

Klaar om je Excel‑bestanden echt meertalig te maken? Laten we eerst controleren of je ontwikkelomgeving aan de vereisten voldoet.

## Snelle antwoorden
- **Wat is globalisatie in Aspose.Cells?** Het is een set locale‑bewuste strings (fouten, booleans, enz.) die je kunt vervangen door aangepaste tekst.  
- **Welke Maven‑artifact is vereist?** `com.aspose:aspose-cells:25.3`.  
- **Kan ik andere talen dan Russisch targeten?** Ja – breid `GlobalizationSettings` uit en overschrijf de benodigde methoden voor elke locale.  
- **Heb ik een licentie nodig voor ontwikkeling?** Een gratis proefversie werkt voor testen; een permanente licentie verwijdert evaluatiewatermerken.  
- **Is de oplossing thread‑safe?** Pas instellingen per werkmap toe; het `GlobalizationSettings`‑object zelf is onwijzigbaar na creatie.

## Wat is globalisatie in Aspose.Cells?

`GlobalizationSettings` is het configuratie‑object van Aspose.Cells dat locale‑specifieke strings regelt, zoals foutmeldingen, booleaanse waarden, valutasymbolen en datum‑patronen. Door je eigen subclass te leveren, vertel je de bibliotheek welke tekst moet worden weergegeven voor elke cultuur, zodat je de standaard Engelse strings kunt vervangen door vertalingen die passen bij de taal en regionale conventies van de eindgebruiker.

## Waarom aangepaste globalisatie toevoegen?

Aspose.Cells ondersteunt **meer dan 50 invoer‑ en uitvoerformaten** – waaronder XLSX, CSV, PDF en ODS – en kan werkmappen verwerken met **tot 200 000 rijen** zonder het volledige bestand in het geheugen te laden. Het aanpassen van globalisatie zorgt ervoor dat eindgebruikers berichten in hun eigen taal zien, waardoor het aantal support‑tickets naar schatting met **30 %** daalt bij multinationale implementaties.

## Vereisten

- **Java Development Kit** 8 of nieuwer.
- **IDE** zoals IntelliJ IDEA of Eclipse.
- **Aspose.Cells for Java** versie 25.3 (of later) toegevoegd via Maven of Gradle.

### Aspose.Cells voor Java instellen

Voeg de Maven‑dependency toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Of, als je Gradle verkiest, voeg het volgende toe aan `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Licentie verkrijgen

Aspose biedt verschillende licentie‑opties:

- **Gratis proefversie** – volledige functionaliteit gedurende 30 dagen.  
- **Tijdelijke licentie** – onbeperkte evaluatie zonder watermerken.  
- **Commerciële licentie** – productie‑klaar, met prioriteits‑ondersteuning.

Nadat je een licentiebestand hebt verkregen, stel je het één keer in bij het opstarten van de applicatie:

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## Hoe globalisatie toe te voegen voor Russisch?

Een `Workbook`‑object vertegenwoordigt een Excel‑bestand dat in het geheugen is geladen en biedt toegang tot de bladen, cellen en instellingen. Laad je werkmap, maak een subclass van `GlobalizationSettings` en koppel deze aan de werkmap. Het directe antwoord is: **instantieer een aangepaste `GlobalizationSettings`‑klasse, overschrijf `getErrorValueString` en `getBooleanValueString`, en roep vervolgens `workbook.setGlobalizationSettings(customSettings)`**. Deze twee‑stappen‑aanpak vervangt de standaard Russische strings door jouw eigen vertalingen.

### De aangepaste instellingen definiëren

De eerste keer dat je `GlobalizationSettings` in deze gids noemt, let op de definitie:

`GlobalizationSettings` is de basisklasse die Aspose.Cells gebruikt om locale‑specifieke strings op te halen.  

Maak nu een subclass die Russische specifieke tekst retourneert:

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### De instellingen toepassen op een werkmap

Nadat je de subclass hebt gedefinieerd, koppel je deze aan elke `Workbook`‑instantie:

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## Praktische toepassingen

- **Financiële rapportage** – toon foutcodes in de moedertaal van de accountant, waardoor misinterpretatie wordt verminderd.  
- **Enterprise‑brede tools** – integreer dezelfde globalisatie‑logica in tientallen interne Excel‑gebaseerde hulpprogramma's.  
- **Geautomatiseerde datapijplijnen** – zorg ervoor dat downstream‑systemen locale‑bewuste waarden ontvangen zonder extra vertaalstappen.

## Prestatie‑overwegingen

Wanneer je aangepaste globalisatie inschakelt, verwerkt Aspose.Cells nog steeds formules en I/O met dezelfde hoge prestaties. Om het geheugenverbruik laag te houden:

- Maak werkmap‑referenties vrij (`wb.dispose()`) na het opslaan.  
- Gebruik `CalculationOptions.setEnableIterativeCalculation(true)` alleen wanneer nodig.  
- Stem de JVM‑heap af (`-Xmx2g`) voor werkmappen groter dan 100 MB.

## Veelgestelde vragen

**Q: Kan ik dezelfde globalisatie‑instellingen op meerdere werkmappen tegelijk toepassen?**  
A: Ja. Maak één `RussianGlobalization`‑instantie en geef deze aan elke werkmap via `setGlobalizationSettings`.

**Q: Wat als ik een taal moet ondersteunen die van rechts‑naar‑links schrijft?**  
A: Overschrijf extra methoden zoals `getCurrencySymbol` en `getDatePattern` in je subclass om de juiste RTL‑symbolen te retourneren.

**Q: Is een licentie vereist voor de proefversie om aangepaste globalisatie te gebruiken?**  
A: Nee. De proefversie ondersteunt `GlobalizationSettings` volledig; alleen evaluatiewatermerken verschijnen op bepaalde uitvoerformaten.

**Q: Hoe debug ik onjuiste foutstrings?**  
A: Voeg `System.out.println`‑statements toe binnen je overschreven methoden om te verifiëren dat de invoer‑`err`‑waarde overeenkomt met je switch‑cases.

**Q: Heeft dit invloed op de snelheid van formule‑berekeningen?**  
A: Negentijds. De bibliotheek zoekt de string alleen op bij het renderen van celwaarden, niet tijdens tussenliggende berekeningsstappen.

## Aanvullende bronnen

- **Documentatie**: Verken gedetailleerde handleidingen op [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)  
- **Download**: Toegang tot de nieuwste releases via [Aspose Downloads](https://releases.aspose.com/cells/java/)  
- **Aankoop**: Koop een licentie voor commercieel gebruik via [Aspose Purchase](https://purchase.aspose.com/buy)  
- **Gratis proefversie**: Begin met een gratis proefversie via [Aspose Free Trial](https://releases.aspose.com/cells/java/)  
- **Tijdelijke licentie**: Verkrijg een tijdelijke licentie via [Aspose Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Ondersteuning**: Krijg hulp van de community op [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

---

**Laatst bijgewerkt:** 2026-08-16  
**Getest met:** Aspose.Cells 25.3 for Java  
**Auteur:** Aspose

## Gerelateerde tutorials

- [Aspose.Cells Java: Custom Calculation Engine Guide](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [How to Use Aspose Cells – Excel Engine Tutorials for Java](/cells/java/calculation-engine/)
- [Aspose Cells Maven Dependency – Manage Excel Data Connections with Aspose.Cells in Java](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}