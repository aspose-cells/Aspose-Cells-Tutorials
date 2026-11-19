---
category: general
date: 2026-11-19
description: Leer hoe je een draaitabel in Java kunt kopiëren terwijl je de gegevens
  en lay‑out behoudt. Deze stapsgewijze handleiding laat ook zien hoe je Excel‑draaitabellen
  efficiënt kunt kopiëren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- how to preserve pivot
- preserve pivot table
- copy excel pivot
language: nl
lastmod: 2026-11-19
og_description: Kopieer draaitabel in Java met Aspose.Cells. Volg deze gids om te
  leren hoe je draaitabellen behoudt en Excel‑draaitabelgegevens nauwkeurig kopieert.
og_image_alt: Illustration of the copy pivot table workflow in Java
og_title: Kopieer draaitabel in Java – volledige Aspose.Cells-gids
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy pivot table in Java while preserving its data and
    layout. This step‑by‑step guide also shows how to copy excel pivot tables efficiently.
  headline: How to copy pivot table in Java with Aspose.Cells
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Pivot tables
title: Hoe een draaitabel te kopiëren in Java met Aspose.Cells
url: /nl/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een draaitabel te kopiëren in Java met Aspose.Cells

Als je een **copy pivot table** van het ene werkboek naar het andere moet kopiëren, laat deze gids je precies zien hoe je dat in Java doet. Of je nu een rapportage‑engine bouwt of gegevens migreert, je ziet een betrouwbare manier om de cache, velden en opmaak van de draaitabel te behouden.

Het kopiëren van een draaitabel kan lastig zijn omdat een eenvoudige bereik‑kopie vaak de onderliggende gegevensbron verliest. In deze tutorial gebruiken we Aspose.Cells om **how to copy pivot** te gebruiken terwijl elke berekening intact blijft, en we behandelen ook **how to preserve pivot** tabellen wanneer het doelwerkboek leeg is.

## Vereisten

* Java 17 of nieuwer geïnstalleerd.
* Aspose.Cells for Java (versie 23.9 of later) toegevoegd aan de classpath van je project.
* Twee Excel‑bestanden: een bronwerkboek dat de draaitabel bevat en een leeg doelwerkboek (of een werkboek waarin je wilt samenvoegen).

Je hebt geen speciale licentie nodig voor het code‑voorbeeld, maar een geldige Aspose.Cells‑licentie verwijdert evaluatiewatermerken.

## Stap 1: Laad het bronwerkboek dat de draaitabel bevat

De eerste stap is het openen van het werkboek dat de oorspronkelijke draaitabel bevat. Het laden van het bestand geeft je toegang tot het werkblad, de cellen en de draaitabel‑cache.

```java
// Step 1: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Waarom dit belangrijk is*: Aspose.Cells leest het volledige werkboek, inclusief verborgen cache‑gegevens die de draaitabel aandrijven. Zonder het volledige bestand te laden, zou de kopieerbewerking de definitie van de draaitabel verliezen.

## Stap 2: Bereid het doelwerkboek voor

Maak een nieuw werkboek aan (of open een bestaand) en haal het eerste werkblad op. Hier wordt de draaitabel geplaatst.

```java
// Step 2: Create a new destination workbook and get its first worksheet
Workbook destWb = new Workbook();                     // empty workbook
Worksheet destWs = destWb.getWorksheets().get(0);    // first sheet
```

*Tip*: Als je al een doelwerkboek hebt, vervang dan de `new Workbook()`‑aanroep door `new Workbook("target.xlsx")`. Hiermee kun je **copy excel pivot** in een vooraf ingevuld werkboek plaatsen.

## Stap 3: Definieer het celgebied dat de draaitabel omsluit

Je moet het exacte bereik opgeven dat de draaitabel omvat. Het bereik bevat de tabel van de draaitabel, de veldlijst en alle omringende gegevens die je wilt behouden.

```java
// Step 3: Define the cell area that covers the pivot table in the source sheet
CellArea area = CellArea.createCellArea("A1", "H30"); // adjust as needed
```

*Waarom dit belangrijk is*: De `CellArea` vertelt Aspose.Cells wat gekopieerd moet worden. Als het gebied te klein is, wordt de draaitabel afgekapt; als het te groot is, kopieer je onnodige gegevens. Pas de coördinaten aan op basis van de werkelijke grootte van de draaitabel.

## Stap 4: Voer de kopie‑bewerking uit met CopyOptions

Gebruik de `copy`‑methode op de cellen‑collectie van het bronwerkblad. Het doorgeven van een nieuw `CopyOptions()`‑object zorgt ervoor dat alle opmaak, formules en de draaitabel‑cache worden overgedragen.

```java
// Step 4: Copy the defined range (including the pivot table) to the destination worksheet
srcWb.getWorksheets().get(0).getCells().copy(area, destWs.getCells(), new CopyOptions());
```

### Waarom `CopyOptions` de draaitabel behoudt

`CopyOptions` vertelt Aspose.Cells om het bereik te behandelen als een *geheel* object in plaats van een platte set waarden. Dit is de sleutel tot **how to preserve pivot** tabellen: de onderliggende draaitabel‑cache wordt gedupliceerd, zodat het doelwerkboek de draaitabel kan herberekenen zonder handmatige tussenkomst.

## Stap 5: Sla het doelwerkboek op

Schrijf tenslotte het doelbestand naar schijf. Het opgeslagen bestand zal een volledig functionele kopie van de oorspronkelijke draaitabel bevatten.

```java
// Step 5: Save the destination workbook – the pivot table is preserved
destWb.save("YOUR_DIRECTORY/copied_with_pivot.xlsx");
```

*Verwacht resultaat*: Het openen van `copied_with_pivot.xlsx` in Excel toont dezelfde draaitabel, compleet met slicers, filters en berekende velden. Je kunt deze vernieuwen, en de gegevensbron zal wijzen naar het gekopieerde bereik binnen hetzelfde werkboek.

---

![Diagram dat het proces van het kopiëren van een draaitabel toont](/images/copy-pivot-table-workflow.png){.align-center width=600 alt="Diagram dat de workflow van het kopiëren van een draaitabel van bron- naar doelwerkboek illustreert"}

## Hoe draaitabellen over meerdere werkbladen te kopiëren

Als je **copy excel pivot** tabellen van meerdere bladen moet kopiëren, herhaal dan Stappen 3‑4 voor elk bronwerkblad. Je kunt ook door `srcWb.getWorksheets()` itereren en elke draaitabel kopiëren naar een overeenkomend blad in `destWb`. Hier is een beknopt loop‑voorbeeld:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet srcWs = srcWb.getWorksheets().get(i);
    Worksheet newDestWs = destWb.getWorksheets().add();
    // Assume each pivot occupies A1:H30 – adjust per sheet if needed
    CellArea area = CellArea.createCellArea("A1", "H30");
    srcWs.getCells().copy(area, newDestWs.getCells(), new CopyOptions());
}
destWb.save("YOUR_DIRECTORY/multi_sheet_copy.xlsx");
```

*Pro tip*: Gebruik `srcWs.getPivotTables().getCount()` om te detecteren of een blad daadwerkelijk een draaitabel bevat voordat je kopieert. Dit voorkomt het kopiëren van irrelevante gegevens.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Draaitabel verliest zijn cache** | Het gebruik van `Worksheet.copy()` zonder `CopyOptions` kopieert alleen celwaarden. | Gebruik altijd `srcWs.getCells().copy(..., new CopyOptions())`. |
| **Doel toont #REF! fouten** | De gekopieerde draaitabel verwijst nog steeds naar de externe gegevensbron van het oorspronkelijke werkboek. | Roep na het kopiëren `destWs.getPivotTables().get(0).refresh();` aan om de cache aan het nieuwe bereik te binden. |
| **Slicers verdwijnen** | Slicers worden opgeslagen buiten het hoofdcelgebied. | Breid `CellArea` uit om slicer‑bereiken op te nemen, of kopieer het volledige werkblad (`srcWs.copy(destWs, new CopyOptions())`). |
| **Prestatie‑vertraging bij grote draaitabellen** | Het kopiëren van enorme bereiken met opmaak kan traag zijn. | Gebruik `CopyOptions.setOnlyData(true)` als je geen opmaak nodig hebt, en pas vervolgens de stijlen handmatig opnieuw toe. |

## Hoe de opmaak van de draaitabel te behouden bij het bijwerken van gegevens

Soms moet je **how to preserve pivot** lay-out behouden nadat de brongegevens zijn gewijzigd. Na het kopiëren kun je de stijl van de draaitabel vergrendelen:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.setPreserveFormatting(true);   // keeps colors, fonts, and layout
pt.refresh();                     // recalculates with new data
```

Het instellen van `PreserveFormatting` zorgt ervoor dat eventuele aangepaste stijlen die je in de bron hebt toegepast, de kopie overleven.

## De kopie verifiëren

Een snelle manier om te bevestigen dat de kopie geslaagd is, is de draaitabeldefinities te vergelijken:

```java
PivotTable srcPt = srcWb.getWorksheets().get(0).getPivotTables().get(0);
PivotTable destPt = destWs.getPivotTables().get(0);

System.out.println("Source fields: " + srcPt.getFields().size());
System.out.println("Destination fields: " + destPt.getFields().size());
// Both numbers should match
```

Als de aantallen overeenkomen en het doelwerkboek zonder fouten opent, heb je succesvol **copy pivot table**.

## Conclusie

Je weet nu hoe je **copy pivot table** van het ene Excel‑werkboek naar het andere kunt kopiëren met Aspose.Cells voor Java, en je hebt de exacte stappen gezien om **how to copy pivot** uit te voeren terwijl je de cache, opmaak en slicers van de draaitabel intact houdt. Hetzelfde patroon werkt voor **copy excel pivot** scenario's over meerdere bladen, en je kunt de code aanpassen voor randgevallen zoals het behouden van draaitabel‑opmaak of het verwerken van grote datasets.

### Volgende stappen

* Verken **preserve pivot table** opties zoals `setPreserveFormatting` en `refresh` voor dynamische gegevensbronnen.  
* Probeer draaitabellen te kopiëren tussen werkboeken met verschillende kolomvolgordes—pas de `CellArea` dienovereenkomstig aan.  
* Combineer deze techniek met Aspose.Slides om snapshots van draaitabellen in PowerPoint‑presentaties in te sluiten.

Veel plezier met coderen, en voel je vrij om te experimenteren met variaties die passen bij jouw specifieke automatiseringspipeline!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe bereik te kopiëren en een draaitabel te behouden in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Hoe een draaitabel tussen werkbladen te kopiëren in Java](/cells/english/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/)
- [Hoe een draaitabel naar een nieuw werkboek te kopiëren in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}