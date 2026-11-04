---
category: general
date: 2026-10-20
description: Leer hoe je een draaitabel kunt kopiëren met Aspose.Cells in Java. Deze
  tutorial laat zien hoe je een bereik naar een nieuw blad kopieert en een draaitabelblad
  veilig dupliceert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new sheet
- duplicate pivot table sheet
language: nl
lastmod: 2026-10-20
og_description: Hoe een draaitabel te kopiëren met Aspose.Cells in Java. Volg deze
  gids om een bereik naar een nieuw blad te kopiëren en een draaitabelblad te dupliceren
  zonder gegevens te verliezen.
og_image_alt: Screenshot showing how to copy pivot table from one worksheet to another
  in a Java program
og_title: Hoe een draaitabel te kopiëren in Java – volledige Aspose.Cells‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  headline: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  name: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that holds the original pivot table.
    text: Load the workbook that holds the original pivot table.
  - name: Identify the exact range that includes the pivot table.
    text: Identify the exact range that includes the pivot table.
  - name: Create a new worksheet that will receive the copied data.
    text: Create a new worksheet that will receive the copied data.
  - name: Use the `Range.copy` method to transfer the range to the new sheet.
    text: Use the `Range.copy` method to transfer the range to the new sheet.
  - name: Save the workbook to a new file.
    text: Save the workbook to a new file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hoe een draaitabel te kopiëren in Java met Aspose.Cells – stapsgewijze gids
url: /nl/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een draaitabel te kopiëren in Java met Aspose.Cells – stapsgewijze handleiding

Als je **hoe je een draaitabel moet kopiëren** in een Java‑applicatie nodig hebt, leidt deze gids je door de exacte stappen. Of je nu een rapportage‑engine bouwt of gegevensmigratie automatiseert, je zult zien hoe je een bereik naar een nieuw blad kopieert terwijl je de definitie en gegevens van de draaitabel behoudt.

Het kopiëren van een draaitabel kan riskant aanvoelen omdat de onderliggende cache en veldinstellingen vaak verloren gaan. Deze tutorial toont een betrouwbare aanpak met Aspose.Cells, laat de volledige uitvoerbare code zien en legt uit waarom elke regel belangrijk is. Aan het einde kun je een draaitabelblad in enkele seconden dupliceren.

## Vereisten

* Java 8 of nieuwer geïnstalleerd.
* Aspose.Cells for Java (versie 23.10 of later) toegevoegd aan de classpath van je project.
* Een bronwerkmap (`source.xlsx`) die een draaitabel bevat in het bereik `A1:G20`.
* Basiskennis van Java en Excel-concepten.

Er zijn geen extra bibliotheken nodig; Aspose.Cells verwerkt alle Excel‑bewerkingen intern.

## Hoe een draaitabel te kopiëren – algemene strategie

Het kernidee is simpel:

1. Laad de werkmap die de originele draaitabel bevat.
2. Identificeer het exacte bereik dat de draaitabel omvat.
3. Maak een nieuw werkblad aan dat de gekopieerde gegevens zal ontvangen.
4. Gebruik de `Range.copy`‑methode om het bereik naar het nieuwe blad over te brengen.  
   Deze methode kopieert automatisch de draaitabel‑cache, zodat de draaitabel functioneel blijft.
5. Sla de werkmap op in een nieuw bestand.

Omdat de kopie‑operatie op bereikniveau werkt, behoudt het **dubbele draaitabelblad** alle veldconfiguraties, filters en berekende items.

## Stap 1: Laad de bronwerkmap

```java
// Import Aspose.Cells classes
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Waarom dit belangrijk is*: Het laden van de werkmap geeft je toegang tot de werkbladen, cellen en de draaitabel‑cache. Aspose.Cells leest het volledige bestand in het geheugen, zodat volgende bewerkingen snel en thread‑safe zijn.

## Stap 2: Definieer het bronbereik dat de draaitabel bevat

```java
        // Locate the first worksheet (index 0) and create a range covering the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)               // first sheet
                                    .getCells()
                                    .createRange("A1:G20"); // adjust if your pivot table is larger
```

*Waarom dit belangrijk is*: De `createRange`‑aanroep vertelt Aspose.Cells precies welke cellen gekopieerd moeten worden. Het opnemen van het volledige draaitabelgebied zorgt ervoor dat de verborgen cache‑rijen ook worden overgebracht. Als je een deel van de cache weglaat, zal de gekopieerde draaitabel leeg lijken.

## Stap 3: Voeg een bestemmingswerkblad toe voor de gekopieerde gegevens

```java
        // Add a new worksheet that will hold the duplicated pivot table
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");
```

*Waarom dit belangrijk is*: Het toevoegen van een apart blad isoleert de gekopieerde draaitabel van de originele, waardoor het eenvoudig is om resultaten te vergelijken of het blad als sjabloon voor verdere verwerking te gebruiken.

## Stap 4: Kopieer het bereik naar het bestemmingswerkblad (draaientabel wordt behouden)

```java
        // Copy the defined range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

*Waarom dit belangrijk is*: De `copy`‑methode kopieert niet alleen celwaarden en opmaak, maar ook de draaitabel‑cache. Dit is de cruciale stap die je in staat stelt om **dubbele draaitabelblad** te maken zonder functionaliteit te verliezen.

## Stap 5: Sla de werkmap op met het gekopieerde bereik

```java
        // Persist the workbook to a new file
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

*Waarom dit belangrijk is*: Opslaan maakt een nieuw Excel‑bestand (`result.xlsx`) aan dat zowel de originele als het gedupliceerde draaitabelblad bevat. Je kunt het bestand nu in Excel openen om te verifiëren dat de draaitabel exact werkt zoals voorheen.

## Volledig, uitvoerbaar voorbeeld

Alles bij elkaar genomen, hier is het volledige programma dat je kunt kopiëren‑plakken in je IDE:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1. Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2. Define the source range that contains the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)
                                    .getCells()
                                    .createRange("A1:G20");

        // 3. Add a destination worksheet for the copied data
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");

        // 4. Copy the range to the destination worksheet (pivot table is preserved)
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5. Save the workbook with the copied range
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

### Verwachte output

* Het openen van `result.xlsx` toont twee werkbladen:
  * **Sheet1** – de originele gegevens en draaitabel.
  * **CopyResult** – een exacte duplicaat van de draaitabel, volledig functioneel.
* Alle draaitabelvelden, filters en berekende items gedragen zich identiek aan de bron.

Als je de bron‑draaientabel wijzigt na het kopiëren, zal het gedupliceerde blad **niet** die wijzigingen weergeven omdat de cache op het moment van kopiëren werd gedupliceerd. Deze isolatie is vaak wenselijk wanneer je een momentopname van het rapport nodig hebt.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Draaitabel verschijnt leeg** | Het gekopieerde bereik sloot de verborgen cache‑rijen uit. | Zorg ervoor dat het bereik de volledige cache omvat (meestal enkele rijen onder de zichtbare tabel). |
| **Bestemmingsbladnaam bestaat al** | `add("CopyResult")` geeft een uitzondering als de naam al in gebruik is. | Gebruik `workbook.getWorksheets().addUniqueName("CopyResult")` of controleer `contains` voordat je toevoegt. |
| **Bestandspad‑fouten** | Onjuiste `YOUR_DIRECTORY` leidt tot `FileNotFoundException`. | Gebruik absolute paden of Java’s `Paths.get(...).toAbsolutePath()` om locaties op te lossen. |
| **Prestatie‑vertraging bij grote werkmappen** | Het kopiëren van enorme bereiken kopieert onnodige cellen. | Beperk het bereik tot het exacte draaitabelgebied, of gebruik `Range.copy` met `CopyOptions` om opmaak over te slaan indien niet nodig. |

## Pro‑tip: `CopyOptions` gebruiken voor fijnere controle

Als je alleen de draaitabelgegevens nodig hebt en celopmaak wilt overslaan, kun je een `CopyOptions`‑object doorgeven:

```java
CopyOptions options = new CopyOptions();
options.setCopyStyle(false);        // skip styles
options.setCopyMerged(true);        // keep merged cells
sourceRange.copy(destinationSheet.getCells().createRange("A1"), options);
```

Dit verkleint de bestandsgrootte van het gedupliceerde blad en versnelt de kopie‑operatie, vooral bij grote werkmappen.

## Hoe een bereik naar een nieuw blad te kopiëren zonder formules te verliezen

Het bovenstaande voorbeeld kopieert al formules omdat `Range.copy` ze standaard behoudt. Als je alleen waarden wilt (bijv. om de huidige staat te bevriezen), stel je `options.setPasteType(PasteType.VALUES)` in.

```java
CopyOptions opt = new CopyOptions();
opt.setPasteType(PasteType.VALUES);
sourceRange.copy(destinationSheet.getCells().createRange("A1"), opt);
```

Nu bevat het bestemmingsblad statische waarden, maar de draaitabel blijft functioneren omdat de cache deel uitmaakt van het bereik.

## Samenvatting van de oplossing

* **Hoe een draaitabel te kopiëren** – laad de werkmap, definieer het exacte bereik, voeg een nieuw werkblad toe, kopieer het bereik en sla op.
* Het proces toont ook **bereik kopiëren naar nieuw blad** en hoe je **dubbele draaitabelblad** veilig kunt maken.
* Je kunt de kopie fijn afstellen met `CopyOptions` voor prestatie‑ of alleen‑waarde scenario's.

## Volgende stappen en gerelateerde onderwerpen

* **Draaitabel‑cache programmatisch vernieuwen** – gebruik `PivotTable.refreshData()` na het bijwerken van brongegevens.
* **Draaitabel exporteren naar PDF** – combineer deze kopieertechniek met `PdfSaveOptions` om momentopname‑rapporten te maken.
* **Automatiseer duplicatie van meerdere bladen** – loop door alle werkbladen en pas dezelfde kopielogica toe.

Experimenteer met deze variaties om het patroon aan te passen aan jouw specifieke rapportage‑pipeline. Als je edge‑cases tegenkomt, zoals externe gegevensbronnen of VBA‑gestuurde draaitabellen, werkt dezelfde bereik‑kopie‑aanpak, maar moet je mogelijk ook de onderliggende verbindingsobjecten kopiëren.

---

*Veel plezier met coderen!* Als deze tutorial je heeft geholpen **hoe je een draaitabel moet kopiëren** te leren, deel hem dan gerust met teamgenoten of lever verbeteringen aan.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe bereik te kopiëren en een draaitabel te behouden in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Nieuwe werkmap maken in Java – volledige gids voor het kopiëren van een draaitabel](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Draaitabel kopiëren tussen werkmappen – stapsgewijze Java‑gids](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}