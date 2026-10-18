---
category: general
date: 2026-06-27
description: Integreer lettertypen in HTML wanneer je Excel naar HTML converteert.
  Leer hoe je een werkmap als HTML kunt opslaan met ingebedde lettertypen met eenvoudige
  Java‑code.
draft: false
keywords:
- embed fonts in html
- convert excel to html
- save workbook as html
- Java Excel to HTML conversion
- Aspose.Cells HTML export
language: nl
og_description: Lettertypen insluiten in HTML tijdens het converteren van Excel naar
  HTML. Deze gids laat zien hoe je een werkmap als HTML opslaat met ingesloten lettertypen
  met behulp van Java.
og_title: Lettertypen insluiten in HTML – Excel naar HTML converteren en werkmap opslaan
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  headline: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  type: TechArticle
- description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  name: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  steps:
  - name: Right‑click the page → “View Page Source”.
    text: Right‑click the page → “View Page Source”.
  - name: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
    text: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
  - name: Load or create the workbook.
    text: Load or create the workbook.
  - name: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
    text: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
  - name: Call `Workbook.save` with those options.
    text: Call `Workbook.save` with those options.
  type: HowTo
tags:
- Java
- Aspose.Cells
- HTML
- Excel
title: Lettertypen insluiten in HTML – Excel naar HTML converteren & werkmap opslaan
url: /nl/java/excel-import-export/embed-fonts-in-html-convert-excel-to-html-save-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lettertypen insluiten in HTML – Excel naar HTML converteren & Werkmap opslaan

Heb je ooit **lettertypen in HTML moeten insluiten** wanneer je *Excel naar HTML converteert*? Misschien bouw je een rapportageportaal en voldoen de standaard weblettertypen niet. Het goede nieuws is dat je niet hoeft te voldoen aan de saaie, generieke uitstraling—Aspose.Cells laat je de exacte lettertypen die je in de spreadsheet hebt gebruikt, direct in het gegenereerde HTML‑bestand opnemen.

In deze tutorial lopen we een volledig, kant‑klaar Java‑voorbeeld door dat **werkmap opslaat als HTML** met ingesloten lettertypen, uitlegt waarom je dit zou willen doen, en wijst op een paar valkuilen die je kunt tegenkomen. Aan het einde heb je een zelfstandige HTML‑pagina die er precies uitziet als het oorspronkelijke Excel‑blad, zonder ontbrekende tekens, zonder externe CSS‑problemen.

## Wat je zult leren

- Hoe je een bestaande Excel-werkmap (of een nieuwe vanaf nul) in Java laadt.  
- Hoe je `HtmlSaveOptions` configureert om de lettertypen van de werkmap direct in de HTML-uitvoer in te sluiten.  
- Hoe je `Workbook.save` aanroept zodat het bestand wordt weggeschreven als **HTML met ingesloten lettertypen**.  
- Tips voor het omgaan met grote lettertypebestanden, aangepaste lettertype‑mappen en het oplossen van veelvoorkomende valkuilen.

> **Voorvereiste:** Je hebt Aspose.Cells voor Java (nieuwste versie) op je classpath en een Java 8+ runtime nodig. Andere externe bibliotheken zijn niet vereist.

---

## Stap 1: Het project instellen en vereiste klassen importeren

Voordat we in de code duiken, zorgen we dat de ontwikkelomgeving klaar is. Als je Maven gebruikt, voeg dan de Aspose.Cells‑dependency toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the newest version available -->
</dependency>
```

Als je Gradle verkiest, is het equivalent:

```gradle
implementation 'com.aspose:aspose-cells:23.12'
```

> **Pro tip:** Houd de bibliotheek up‑to‑date. Nieuwe releases verbeteren vaak de lettertype‑afhandeling en verkleinen de grootte van de ingesloten data.

Importeer nu de klassen die we nodig hebben:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.HtmlSaveOptions;
import com.aspose.cells.SaveFormat;
import java.io.File;
```

Deze imports geven ons toegang tot het werkmap‑model, de HTML‑exportopties en een paar hulpprogramma‑klassen.

---

## Stap 2: De Excel‑werkmap laden (of maken)

Je kunt een bestaand `.xlsx`‑bestand laden of een werkmap ter plekke aanmaken. Voor illustratie gaan we ervan uit dat er een bestand `Sample.xlsx` in de `resources`‑map van het project staat.

```java
// Load an existing workbook
String inputPath = "resources/Sample.xlsx";
Workbook wb = new Workbook(inputPath);
```

Als je geen bronbestand hebt, kun je snel een werkmap genereren:

```java
// Create a workbook from scratch (optional)
Workbook wb = new Workbook();               // creates a new empty workbook
wb.getWorksheets().get(0).getCells().putValue("A1", "Hello, world!");
```

> **Waarom dit belangrijk is:** Wanneer je lettertypen insluit, haalt Aspose.Cells de exacte lettertype‑definities uit de werkmap. Als de werkmap aangepaste lettertypen bevat, worden deze meegeleverd met de HTML, waardoor visuele getrouwheid gegarandeerd is.

---

## Stap 3: HtmlSaveOptions configureren om lettertypen in te sluiten

Dit is het hart van de tutorial. Standaard schrijft `HtmlSaveOptions` CSS die naar systeemlettertypen verwijst. Om dat gedrag te wijzigen, schakelen we de vlag `setEmbedFonts(true)` in.

```java
// Step 1: Create HTML save options
HtmlSaveOptions htmlOpts = new HtmlSaveOptions(SaveFormat.HTML);

// Step 2: Enable embedding of fonts in the HTML output
htmlOpts.setEmbedFonts(true);

// (Optional) Reduce the size of embedded fonts by subsetting only used glyphs
htmlOpts.setSubsetFonts(true);
```

### Wat de opties doen

| Optie | Standaard | Effect bij wijziging |
|--------|-----------|----------------------|
| `setEmbedFonts(true)` | `false` | Voegt de volledige lettertypebestanden toe (meestal als Base64‑gecodeerde data‑URI’s) in de gegenereerde HTML. |
| `setSubsetFonts(true)` | `false` | Beperkt het ingesloten lettertype tot alleen de daadwerkelijk gebruikte tekens, waardoor de bestandsgrootte drastisch wordt verkleind. |
| `setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_ALL)` | `EMBED_ALL` | Je kunt ervoor kiezen alleen specifieke lettertypen in te sluiten als je licentie‑beperkingen hebt. |

> **Randgeval:** Als de werkmap een lettertype gebruikt dat niet op de server is geïnstalleerd, valt Aspose.Cells terug op een standaard systeemlettertype. Zorg ervoor dat alle aangepaste lettertypen beschikbaar zijn in de font‑directory van de Java‑runtime of registreer ze handmatig via `FontConfig`.

---

## Stap 4: De werkmap opslaan als HTML met ingesloten lettertypen

Nu de opties zijn ingesteld, roepen we simpelweg `save` aan. De output wordt een enkel `.html`‑bestand dat zowel de werkmap‑data **als** de lettertypebestanden direct in de markup bevat.

```java
// Step 3: Save the workbook as an HTML file with embedded fonts
String outputDir = "output";
new File(outputDir).mkdirs(); // Ensure the folder exists

String outputPath = outputDir + File.separator + "page.html";
wb.save(outputPath, htmlOpts);

System.out.println("HTML file with embedded fonts created at: " + outputPath);
```

Wanneer je `page.html` opent in een moderne browser, wordt de pagina weergegeven met exact dezelfde typografie als in Excel—geen externe lettertypebestanden, geen ontbrekende tekens.

---

## Stap 5: Het resultaat verifiëren en de output begrijpen

Open het gegenereerde HTML‑bestand in een browser (Chrome, Firefox, Edge—elk werkt). Je zou het werkblad getrouw moeten zien. Om dubbel te controleren dat de lettertypen echt zijn ingesloten:

1. Klik met de rechtermuisknop op de pagina → “View Page Source”.  
2. Zoek naar `@font-face`. Je vindt een CSS‑regel met een `src: url(data:font/ttf;base64,…)`‑regel—dit is de Base64‑gecodeerde lettertype‑data.  

Als je dat ziet, is de stap **lettertypen insluiten in HTML** geslaagd.

### Veelgestelde vragen

- **“Waarom is het HTML‑bestand groter dan verwacht?”**  
  Het insluiten van volledige lettertypebestanden kan enkele honderden kilobytes toevoegen. Gebruik `setSubsetFonts(true)` om het te verkleinen, of overweeg alleen de benodigde bladen te converteren.

- **“Kan ik alleen een specifiek lettertype insluiten?”**  
  Ja. Stel `htmlOpts.setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_SPECIFIED)` in en voeg de gewenste lettertypen toe via `htmlOpts.getSpecifiedFontNames().add("MyCustomFont")`.

- **“Wat als het lettertype gelicentieerd is en ik het niet mag insluiten?”**  
  Schakel de vlag uit (`setEmbedFonts(false)`) en bied een web‑safe fallback via CSS, of host het lettertype op een CDN waar je toestemming voor hebt.

---

## Stap 6: Grote werkmappen en prestatie‑tips

Lettertypen insluiten werkt goed voor bescheiden spreadsheets, maar een werkmap met tientallen aangepaste lettertypen kan de HTML‑grootte doen exploderen. Hier zijn enkele prestatie‑gerichte aanbevelingen:

- **Subset lettertypen** (zoals al getoond) om alleen gebruikte glyphs te behouden.  
- **Exporteer alleen de benodigde werkbladen** met `htmlOpts.setExportActiveWorksheetOnly(true)`.  
- **Comprimeer de HTML** na generatie (bijv. gzip op de server) om netwerk‑latentie te verminderen.  
- **Cache de gegenereerde HTML** als hetzelfde Excel‑bestand vaak wordt opgevraagd.

---

## Stap 7: Volgende stappen – verder gaan dan basis‑export

Nu je **lettertypen in HTML hebt ingesloten**, kun je gerelateerde mogelijkheden verkennen:

- **Excel naar HTML converteren met afbeeldingen** (`htmlOpts.setExportImagesAsBase64(true)`).  
- **PDF genereren in plaats van HTML** (`wb.save("output.pdf", SaveFormat.PDF)`).  
- **Responsieve HTML maken** door `htmlOpts.setExportActiveWorksheetOnly` en `htmlOpts.setExportGridLines` aan te passen.  

Al deze functies volgen hetzelfde patroon: configureer een `*SaveOptions`‑object, zet de juiste vlaggen, en roep `Workbook.save` aan.

---

## Conclusie

Je hebt zojuist geleerd hoe je **lettertypen in HTML kunt insluiten** terwijl je **Excel naar HTML converteert** en **de werkmap opslaat als HTML** met Aspose.Cells voor Java. De belangrijkste stappen zijn:

1. Laad of maak de werkmap.  
2. Maak `HtmlSaveOptions` aan en schakel `setEmbedFonts(true)` in.  
3. Roep `Workbook.save` aan met die opties.

Het resultaat is een enkel, draagbaar HTML‑bestand dat er precies uitziet als je oorspronkelijke spreadsheet—geen ontbrekende lettertypen, geen extra CSS‑bestanden, en geen afhankelijkheid van de lettertypen die op de client zijn geïnstalleerd.

Voel je vrij om te experimenteren met lettertype‑subsetting, selectieve insluiting, of zelfs dit te combineren met server‑side caching voor scenario's met veel verkeer. Als je tegen vreemde zaken aanloopt (bijvoorbeeld onverwacht grote bestanden of ontbrekende glyphs), bekijk dan de optionele instellingen die we hebben behandeld en pas ze aan.

Happy coding, en geniet van de pixel‑perfecte HTML die je nu rechtstreeks vanuit je Java‑applicaties kunt leveren!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel naar HTML converteren in Java met Aspose.Cells: Een stapsgewijze handleiding](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Excel exporteren naar HTML met Aspose.Cells voor Java: Een complete gids](/cells/english/java/workbook-operations/export-excel-to-html-aspose-cells-java/)
- [Excel exporteren naar HTML met IStreamProvider & Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/workbook-operations/export-excel-html-streamprovider-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}