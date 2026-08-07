---
category: general
date: 2026-07-20
description: Pas getalnotatie toe in Excel met Java en Aspose.Cells. Leer hoe je een
  valutastijl toepast in Excel, een Excel-werkmap maakt met Java, en een datatabel
  efficiënt naar Excel importeert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- apply currency style excel
- create excel workbook java
- import datatable to excel
language: nl
lastmod: 2026-07-20
og_description: Pas getalnotatie toe in Excel met Java. Deze gids laat zien hoe je
  valutastijl in Excel toepast, een Excel-werkmap maakt met Java, en stap voor stap
  een datatable naar Excel importeert.
og_image_alt: Screenshot of an Excel workbook where apply number format excel has
  been applied to a currency column
og_title: Nummeropmaak toepassen in Excel met Java – Volledige Aspose.Cells tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Apply number format excel using Java and Aspose.Cells. Learn how to
    apply currency style excel, create excel workbook java, and import datatable to
    excel efficiently.
  headline: Apply Number Format Excel in Java – Complete Aspose.Cells Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Open the workbook with `new Workbook("Existing.xlsx")`, fetch
      the target worksheet, and follow steps 3‑5 to apply the style array to new data.
    question: Can I apply the number format to an existing workbook?
  - answer: Use a different built‑in number index (`14` for short date, `22` for long
      date) or a custom format like `yyyy‑mm‑dd`. The workflow stays the same.
    question: What if I need to format dates instead of currency?
  - answer: 'Yes. Just change the file extension in `workbook.save("MyFile.xls")`.
      Aspose will automatically switch to the binary format. ## Wrap‑Up – What We
      Achieved We have **applied number format excel** to a column of monetary values,
      demonstrated how to **apply currency style excel**, shown the simplest wa'
    question: Does this work with older Excel versions (.xls)?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Nummeropmaak toepassen in Excel met Java – Complete Aspose.Cells-gids
url: /nl/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nummeropmaak toepassen in Excel met Java – Complete Aspose.Cells-gids

Heb je je ooit afgevraagd hoe je **apply number format excel** direct vanuit Java-code kunt toepassen? Misschien maak je financiële rapporten of heb je een snelle manier nodig om een kolom met bedragen te stijlen zonder Excel handmatig te openen. Het goede nieuws? Met Aspose.Cells kun je dit in een handvol regels doen, en je leert ook hoe je **apply currency style excel**, **create excel workbook java**, en **import datatable to excel** allemaal in één nette routine.

In deze tutorial lopen we een real‑world voorbeeld door: een lijst met bedragen opgeslagen in een Java `List<Map<String,Object>>` wordt geïmporteerd in een nieuw werkboek, de eerste kolom krijgt een ingebouwde valuta‑opmaak, en het bestand wordt opgeslagen klaar voor distributie. Klaar om te zien hoe eenvoudig het is? Laten we beginnen.

## Vereisten – Wat je nodig hebt

- **Java Development Kit (JDK) 8+** – de code draait op elke recente JDK.
- **Aspose.Cells for Java** library (the Maven artifact `com.aspose:aspose-cells`) – dit is de engine die ons in staat stelt Excel‑bestanden te manipuleren zonder Office geïnstalleerd.
- Een **favorite IDE** (IntelliJ IDEA, Eclipse, VS Code…) – elke editor volstaat, maar een IDE versnelt het debuggen.
- Basiskennis van **Java collections** – we gebruiken een `List` van `Map`s om een DataTable na te bootsen.

Dat is alles. Geen externe services, geen Excel‑installatie, alleen pure Java.

## Stap 1: Excel-werkboek maken in Java – Een Workbook instantieren

Het eerste wat we nodig hebben is een workbook‑object. Beschouw het als het lege canvas waarop alles zal leven.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook(); // creates an in‑memory Excel file
```

Waarom eerst het workbook maken? Aspose.Cells werkt volledig in het geheugen, zodat je bladen, stijlen en gegevens kunt toevoegen voordat je de schijf raakt. Deze aanpak is snel en houdt je code testbaar.

## Stap 2: Gegevens voorbereiden – Datatable importeren naar Excel met een lijst van maps

In veel enterprise‑applicaties komen gegevens uit databases als tabellen. Hier simuleren we dat met een `List<Map<String,Object>>`. Elke map vertegenwoordigt een rij, en de sleutel `"Amount"` correspondeert met een numerieke waarde.

```java
// Step 2: Build a DataTable‑like structure (list of maps)
List<Map<String, Object>> dataRows = new ArrayList<>();

// Row 1
dataRows.add(new HashMap<>() {{
    put("Amount", 1234.56);
}});
// Row 2
dataRows.add(new HashMap<>() {{
    put("Amount", 7890.12);
}});
```

Je zou kunnen vragen: “Waarom geen `ResultSet` of POJO’s gebruiken?” De `importDataTable`‑methode accepteert elke collectie die zich gedraagt als een DataTable, en een lijst van maps is de meest eenvoudige manier om het concept te demonstreren zonder extra afhankelijkheden.

## Stap 3: Het nummerformaat definiëren – Apply Currency Style Excel

Nu volgt het hart van de tutorial: **apply number format excel**. Aspose.Cells wordt geleverd met ingebouwde nummerformaten; het valuta‑formaat heeft index 5. We halen de standaardstijl van het eerste werkblad, passen het nummerformaat aan, en slaan het op voor later gebruik.

```java
// Step 3: Get the default style and set a currency number format
Style currencyStyle = workbook.getWorksheets().get(0).getCells().getDefaultStyle();
currencyStyle.setNumber(5); // 5 = built‑in currency format ($#,##0.00)
```

Waarom de standaardstijl als basis gebruiken? Deze bevat al het standaardlettertype, de uitlijning en andere instellingen van het werkboek, dus je hoeft alleen te wijzigen wat belangrijk is — in dit geval het nummerformaat. Als je een aangepast formaat nodig hebt (bijv. “€#,##0.00”), kun je in plaats daarvan `currencyStyle.setCustom("#,##0.00 €")` aanroepen.

## Stap 4: Importopties instellen – De stijl‑array koppelen

Aspose.Cells staat je toe een array van `Style`‑objecten door te geven die overeenkomen met de te importeren kolommen. Omdat onze gegevens slechts één kolom hebben, leveren we een array met één element die de valuta‑stijl bevat.

```java
// Step 4: Configure import options with the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(new Style[] { currencyStyle });
```

Als je ooit meerdere kolommen verschillend wilt stijlen, breid dan simpelweg de array uit: `new Style[] { styleForCol1, styleForCol2, … }`. De volgorde van stijlen komt overeen met de volgorde van kolommen in de brongegevens.

## Stap 5: Gegevens importeren – De Datatable naar het werkblad brengen

Met het werkboek klaar, de gegevens voorbereid en de stijlen gedefinieerd, importeren we eindelijk **import datatable to excel**. We beginnen bij cel `A1`, nemen kolomkoppen op (`true`), en geven de `ImportTableOptions` door.

```java
// Step 5: Perform the import
Worksheet worksheet = workbook.getWorksheets().get(0);
worksheet.getCells().importDataTable(dataRows, true, "A1", importOptions);
```

Let op de `true`‑vlag — Aspose.Cells genereert automatisch een header‑rij op basis van de map‑sleutels (`"Amount"`). Als je deze op `false` zet, wordt de header weggelaten, waardoor je meer controle krijgt over de uiteindelijke lay-out.

## Stap 6: Het bestand opslaan – Create Excel Workbook Java op schijf

Het laatste puzzelstukje is het in‑memory werkboek naar een fysiek bestand schrijven. Je kunt elk door Aspose ondersteund formaat kiezen (`.xlsx`, `.xls`, `.csv`, …). Hier slaan we op als een XLSX‑bestand.

```java
// Step 6: Save the workbook to disk
String outputPath = "DataTableWithCurrencyStyle.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Na het uitvoeren van het programma, open je het gegenereerde bestand. Je ziet de kolom `"Amount"` opgemaakt met een dollarteken, twee decimalen en juiste duizendtallen‑scheidingstekens — precies wat je verwacht wanneer je **apply number format excel** toepast voor valutawaarden.

## Verwacht resultaat

| Amount |
|--------|
| $1,234.56 |
| $7,890.12 |

De header “Amount” verschijnt in vet (standaardstijl), en elke cel eronder toont het valuta‑formaat dat we hebben ingesteld. Geen handmatige opmaak in Excel nodig.

## Pro‑tips en veelvoorkomende valkuilen

- **Reuse Styles Wisely** – Stijlen zijn lichtgewicht, maar het maken van een nieuwe `Style` voor elke cel kan de prestaties schaden. Hergebruik altijd een stijl‑object wanneer je hetzelfde formaat op veel cellen toepast, zoals we deden met `currencyStyle`.
- **Custom Formats** – Als je locale een ander valutateken gebruikt, vervang dan `currencyStyle.setNumber(5)` door `currencyStyle.setCustom("€#,##0.00")`. Test het formaat in Excel om te bevestigen dat het zich gedraagt zoals verwacht.
- **Large Datasets** – Voor duizenden rijen, overweeg `importDataTable` te gebruiken met de `ImportTableOptions.setImportDataOnly(true)`‑vlag om header‑generatie over te slaan en de import te versnellen.
- **Thread Safety** – Aspose.Cells‑objecten zijn **niet** thread‑safe. Maak een aparte `Workbook` per thread aan als je rapporten parallel genereert.

## Veelgestelde vragen

**Q: Kan ik het nummerformaat toepassen op een bestaand werkboek?**  
A: Absoluut. Open het werkboek met `new Workbook("Existing.xlsx")`, haal het doel‑werk‑blad op, en volg stap 3‑5 om de stijl‑array op nieuwe gegevens toe te passen.

**Q: Wat als ik datums in plaats van valuta moet opmaken?**  
A: Gebruik een andere ingebouwde nummer‑index (`14` voor korte datum, `22` voor lange datum) of een aangepast formaat zoals `yyyy‑mm‑dd`. De werkwijze blijft hetzelfde.

**Q: Werkt dit met oudere Excel‑versies (.xls)?**  
A: Ja. Verander simpelweg de bestandsextensie in `workbook.save("MyFile.xls")`. Aspose schakelt automatisch over naar het binaire formaat.

## Samenvatting – Wat we hebben bereikt

We hebben **applied number format excel** toegepast op een kolom met monetaire waarden, laten zien hoe je **apply currency style excel** kunt gebruiken, de eenvoudigste manier getoond om **create excel workbook java** te doen, en Aspose.Cells gebruikt om **import datatable to excel** uit te voeren zonder de UI aan te raken. Dit alles gebeurde in een beknopt, zelfstandig programma dat je kunt kopiëren, plakken en uitvoeren.

Wat is het volgende? Probeer het voorbeeld uit te breiden:

- Voeg meer kolommen toe (bijv. “Date”, “Description”) en wijs verschillende stijlen per kolom toe.
- Exporteer dezelfde gegevens naar CSV en vergelijk hoe nummerformaten verloren gaan.
- Integreer de code in een Spring Boot‑service die het werkboek retourneert als een downloadbare HTTP‑respons.

Voel je vrij om te experimenteren, en als je tegen problemen aanloopt, laat dan een reactie achter. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Apply Styles to Excel Cells Using Aspose.Cells for Java - Complete Guide](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Merge Cells & Apply Styles in Excel using Aspose.Cells for Java - A Complete Guide](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Aspose.Cells for Java&#58; How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}