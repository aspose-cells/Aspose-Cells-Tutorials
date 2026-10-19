---
date: '2026-09-02'
description: Leer hoe u klikbare afbeelding-Excel-werkboeken maakt met Aspose.Cells
  for Java, door hyperlinks toe te voegen aan afbeeldingen voor interactieve spreadsheets.
keywords:
- create clickable image
- add image hyperlink
- add hyperlink to picture
- interactive excel spreadsheet
- how to add hyperlink
lastmod: '2026-09-02'
og_description: Leer hoe u klikbare afbeelding-Excel-werkboeken maakt met Aspose.Cells
  for Java, door hyperlinks, screen tips toe te voegen en de prestaties te optimaliseren
  in slechts een paar regels code.
og_image_alt: 'Developer guide: create clickable image Excel using Aspose.Cells for
  Java'
og_title: Maak klikbare afbeelding in Excel met Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  headline: Create clickable image Excel using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  name: Create clickable image Excel using Aspose.Cells for Java
  steps:
  - name: prepare your workbook
    text: We start by creating a new workbook and selecting the first sheet.
  - name: insert a label and adjust cell size
    text: Add a descriptive label and give the cell enough space for the picture.
  - name: add the image
    text: '`Picture` represents an image object placed on a worksheet. *Tip*: Replace
      `"path/to/aspose-logo.jpg"` with the actual path to your image file.'
  - name: configure placement and add the hyperlink
    text: '`Hyperlink` defines a link associated with a cell, shape, or picture, enabling
      navigation when clicked.'
  - name: set a screen tip and save the workbook
    text: Provide a helpful tooltip and write the workbook to disk.
  type: HowTo
- questions:
  - answer: Aspose.Cells for Java.
    question: What library is required?
  - answer: Yes – the API works with both .xls and .xlsx.
    question: Can I use .xlsx files?
  - answer: A trial works for evaluation; a permanent license is required for production.
    question: Do I need a license?
  - answer: About 20 lines to add a clickable image.
    question: How many lines of code?
  - answer: Workbook objects are not thread‑safe; create separate instances per thread.
    question: Is it thread‑safe?
  type: FAQPage
tags:
- create clickable image
- Aspose.Cells
- Java Excel automation
title: Maak klikbare afbeelding in Excel met Aspose.Cells for Java
url: /nl/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak klikbare afbeelding Excel met Aspose.Cells voor Java

## Introductie

Als je **create clickable image Excel** werkboeken wilt maken die gebruikers met één klik naar websites, documenten of andere bronnen laten springen, ben je hier aan het juiste adres. In deze tutorial laten we zien hoe Aspose.Cells for Java je in staat stelt **add hyperlink Excel picture** objecten toe te voegen, schermtips te configureren en je spreadsheets zowel mooi als functioneel te houden.

### Wat je zult leren
- Een Aspose.Cells-werkmap initialiseren in Java.  
- Een afbeelding invoegen en omzetten in een klikbare hyperlink.  
- Belangrijke methoden zoals `addHyperlink`, `setPlacement` en `setScreenTip`.  
- Best practices voor prestaties en licenties.

## Snelle antwoorden
- **Welke bibliotheek is vereist?** Aspose.Cells for Java.  
- **Kan ik .xlsx‑bestanden gebruiken?** Ja – de API werkt met zowel .xls als .xlsx.  
- **Heb ik een licentie nodig?** Een proefversie werkt voor evaluatie; een permanente licentie is vereist voor productie.  
- **Hoeveel regels code?** Ongeveer 20 regels om een klikbare afbeelding toe te voegen.  
- **Is het thread‑safe?** Workbook‑objecten zijn niet thread‑safe; maak aparte instanties per thread.  
- **Kan ik een screen tip toevoegen in Excel?** Ja – gebruik `Hyperlink.setScreenTip()` om nuttige zweeftiptekst te tonen.

## Hoe maak je klikbare afbeelding Excel met Aspose.Cells voor Java

Je maakt een klikbare afbeelding Excel-werkboek door een `Workbook` te laden of te maken, een `Picture`‑object in te voegen, een `Hyperlink` aan die afbeelding te koppelen, eventueel een screen tip in te stellen, en tenslotte het bestand op te slaan. De API behandelt alle low‑level Excel‑XML, zodat je slechts een paar eenvoudige regels Java‑code hoeft te schrijven.

### Vereisten
Voordat je begint, zorg ervoor dat je het volgende hebt:

- **Aspose.Cells for Java** (v25.3 of later).  
- **JDK 8+** geïnstalleerd.  
- Een IDE (IntelliJ IDEA, Eclipse of NetBeans) en Maven of Gradle voor afhankelijkheidsbeheer.  

### Vereiste bibliotheken
Voeg Aspose.Cells toe aan je project:

**Maven**  
```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```  

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```  

### Licentie‑acquisitie
Aspose.Cells is commercieel, maar je kunt starten met een gratis proefversie of een tijdelijke licentie aanvragen:

- Gratis proefversie: Download van [Aspose Downloads](https://releases.aspose.com/cells/java/).  
- Tijdelijke licentie: Vraag aan via de [Temporary License page](https://purchase.aspose.com/temporary-license/).  
- Aankoop: Voor langdurig gebruik, bezoek [Aspose Purchase](https://purchase.aspose.com/buy).

### Basisinitialisatie
De `Workbook`‑klasse vertegenwoordigt een volledig Excel‑bestand in het geheugen. Je maakt een instantie ervan en haalt vervolgens een referentie op naar het eerste werkblad. `Worksheet` vertegenwoordigt een enkel blad binnen de werkmap.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

## Stap‑voor‑stap implementatie

### Stap 1: bereid je werkmap voor
We beginnen met het maken van een nieuwe werkmap en het selecteren van het eerste blad.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

### Stap 2: voeg een label toe en pas de celgrootte aan
Voeg een beschrijvend label toe en geef de cel voldoende ruimte voor de afbeelding.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```  

### Stap 3: voeg de afbeelding toe
`Picture` vertegenwoordigt een afbeeldingobject geplaatst op een werkblad.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```  
*Tip*: Vervang `"path/to/aspose-logo.jpg"` door het daadwerkelijke pad naar je afbeeldingsbestand.

### Stap 4: configureer plaatsing en voeg de hyperlink toe
`Hyperlink` definieert een link die gekoppeld is aan een cel, vorm of afbeelding, waardoor navigatie mogelijk is bij klikken.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```  

### Stap 5: stel een screen tip in en sla de werkmap op
Geef een nuttige tooltip en schrijf de werkmap naar schijf.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```  

## Waarom een hyperlink Excel‑afbeelding toevoegen?

Het insluiten van een klikbare afbeelding stelt je in staat branding‑elementen, iconen of diagrammen om te zetten in directe navigatiepunten, waardoor het aantal klikken dat nodig is om gerelateerde inhoud te bereiken wordt verminderd. Deze aanpak verhoogt de gebruikers efficiëntie in marketing‑dashboards, technische handleidingen en educatieve werkbladen.

## Hoe een screen tip toevoegen in Excel

Je voegt een screen tip toe door `hyperlink.setScreenTip("Your tip here")` aan te roepen op het `Hyperlink`‑object dat aan de afbeelding is gekoppeld. De tip verschijnt wanneer de cursor over de afbeelding zweeft, waardoor gebruikers contextuele begeleiding krijgen zonder het blad te overladen.

## Probleemoplossingstips
- **Fout in afbeeldingspad** – controleer het bestandspad en zorg ervoor dat de applicatie leesrechten heeft.  
- **Licentie niet toegepast** – als de proefversie verloopt, kunnen hyperlinks stoppen met werken; pas een geldige licentie toe met `License.setLicense`.  
- **Hyperlink niet klikbaar** – controleer of de `PlacementType` van de afbeelding is ingesteld op `FREE_FLOATING`.

## Praktische toepassingen
Het insluiten van klikbare afbeeldingen is nuttig in veel scenario's:

1. **Marketingrapporten** – link merklogo's naar productpagina's.  
2. **Technische documentatie** – voeg diagrammen toe die gedetailleerde schema's openen.  
3. **Educatieve werkbladen** – zet iconen om in snelkoppelingen voor aanvullende video's.  
4. **Projectdashboards** – laat statusiconen gerelateerde taakvolgers openen.

## Prestatieoverwegingen
- Houd de bestandsgrootte van afbeeldingen redelijk; grote afbeeldingen verhogen het geheugenverbruik van de werkmap.  
- Verwijder ongebruikte objecten (`workbook.dispose()`) bij het verwerken van veel bestanden in een lus.  
- Upgrade naar de nieuwste versie van Aspose.Cells voor prestatieverbeteringen en bugfixes.

## Conclusie
Je weet nu hoe je een hyperlink aan afbeeldingen in Excel kunt toevoegen met Aspose.Cells for Java, waardoor je **create clickable image Excel** werkboeken kunt maken die rijker en interactiever zijn. Experimenteer met verschillende URL's, screen tips en afbeeldingsplaatsingen om aan je rapportagebehoeften te voldoen. Vervolgens kun je onderzoeken hoe je hyperlinks aan vormen toevoegt of bulkafbeeldingsinvoeging automatiseert over meerdere werkbladen.

## Veelgestelde vragen

**Q:** Wat is de maximale afbeeldingsgrootte die wordt ondersteund door Aspose.Cells for Java?  
**A:** Er is geen strikt limiet, maar zeer grote afbeeldingen kunnen de prestaties beïnvloeden en de bestandsgrootte vergroten.

**Q:** Kan ik deze functie gebruiken met .xlsx‑bestanden?  
**A:** Ja, de API werkt met zowel `.xls` als `.xlsx`‑formaten.

**Q:** Hoe moet ik uitzonderingen afhandelen bij het toevoegen van hyperlinks?  
**A:** Plaats de code in een try‑catch‑blok en log `Exception`‑details om pad‑ of licentieproblemen te diagnosticeren.

**Q:** Is het mogelijk om een hyperlink van een afbeelding te verwijderen nadat deze is toegevoegd?  
**A:** Ja – haal het `Picture`‑object op en roep `pic.getHyperlink().remove()` aan of verwijder de afbeelding uit de collectie.

**Q:** Waarom werkt mijn hyperlink mogelijk niet zoals verwacht?  
**A:** Veelvoorkomende oorzaken zijn een onjuiste URL‑string, ontbrekende `http://`/`https://`‑prefix, of een niet-gelicentieerde proefversie die bepaalde functies uitschakelt.

## Aanvullende bronnen
- **Documentatie:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Aankoop en proefversie:** Bezoek [Aspose Purchase](https://purchase.aspose.com/buy) of [Temporary License Page](https://purchase.aspose.com/temporary-license/) voor licentieopties.  
- **Supportforum:** Voor hulp, bekijk het [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**Laatst bijgewerkt:** 2026-09-02  
**Getest met:** Aspose.Cells for Java 25.3  
**Auteur:** Aspose

## Gerelateerde tutorials

- [Hoe hyperkoppelingen te maken in Excel met Aspose.Cells voor Java - Een stap‑voor‑stap gids](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [Hoe Excel‑cellen te stijlen en hyperkoppelingen toe te voegen met Aspose.Cells voor Java](/cells/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Afbeelding toevoegen aan Excel‑opmerking met Aspose.Cells voor Java: Een volledige gids](/cells/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}