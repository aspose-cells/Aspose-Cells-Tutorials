---
category: general
date: 2026-07-20
description: Använd talformat i Excel med Java och Aspose.Cells. Lär dig hur du tillämpar
  valutastil i Excel, skapar en Excel-arbetsbok i Java och importerar en datatabell
  till Excel på ett effektivt sätt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- apply currency style excel
- create excel workbook java
- import datatable to excel
language: sv
lastmod: 2026-07-20
og_description: Applicera talformat i Excel med Java. Den här guiden visar hur du
  tillämpar valutastil i Excel, skapar en Excel‑arbetsbok i Java och importerar en
  datatabell till Excel steg för steg.
og_image_alt: Screenshot of an Excel workbook where apply number format excel has
  been applied to a currency column
og_title: Applicera talformat i Excel i Java – Fullständig Aspose.Cells‑handledning
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
title: Applicera talformat i Excel med Java – Komplett Aspose.Cells‑guide
url: /sv/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Applicera talformat i Excel med Java – Komplett Aspose.Cells‑guide

Har du någonsin funderat på hur du **apply number format excel** direkt från Java‑kod? Kanske skapar du finansiella rapporter eller behöver ett snabbt sätt att formatera en kolumn med belopp utan att öppna Excel manuellt. Den goda nyheten? Med Aspose.Cells kan du göra det på några få rader, och du får också lära dig hur du **apply currency style excel**, **create excel workbook java** och **import datatable to excel** i en enda smidig rutin.

I den här handledningen går vi igenom ett verkligt exempel: en lista med belopp lagrad i en Java `List<Map<String,Object>>` importeras till en ny arbetsbok, den första kolumnen får ett inbyggt valutaformat, och filen sparas klar för distribution. Redo att se hur enkelt det är? Låt oss dyka ner.

## Förutsättningar – Vad du behöver

Innan vi börjar, se till att du har:

- **Java Development Kit (JDK) 8+** – koden körs på vilken som helst nyare JDK.
- **Aspose.Cells for Java**‑biblioteket (Maven‑artefakten `com.aspose:aspose-cells`) – detta är motorn som låter oss manipulera Excel‑filer utan att Office är installerat.
- En **favorit‑IDE** (IntelliJ IDEA, Eclipse, VS Code…) – vilken editor som helst fungerar, men en IDE snabbar upp felsökning.
- Grundläggande kunskap om **Java collections** – vi kommer att använda en `List` av `Map`s för att efterlikna en DataTable.

Det är allt. Inga externa tjänster, ingen Excel‑installation, bara ren Java.

## Steg 1: Skapa Excel Workbook Java – Instansiera arbetsboken

Det första vi behöver är ett arbetsboksobjekt. Tänk på det som en tom duk där allt kommer att leva.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook(); // creates an in‑memory Excel file
```

Varför skapa arbetsboken först? Aspose.Cells arbetar helt i minnet, så du kan lägga till blad, stilar och data innan du någonsin rör disken. Detta tillvägagångssätt är snabbt och gör din kod testbar.

## Steg 2: Förbered data – Importera Datatable till Excel med en lista av mappar

I många företagsapplikationer kommer data från databaser som tabeller. Här simulerar vi det med en `List<Map<String,Object>>`. Varje karta representerar en rad, och nyckeln `"Amount"` mappar till ett numeriskt värde.

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

Du kanske undrar, “Varför inte använda en `ResultSet` eller POJOs?” Metoden `importDataTable` accepterar vilken samling som helst som beter sig som en DataTable, och en lista av mappar är det enklaste sättet att demonstrera konceptet utan att dra in extra beroenden.

## Steg 3: Definiera talformatet – Apply Currency Style Excel

Nu kommer hjärtat i handledningen: **apply number format excel**. Aspose.Cells levereras med inbyggda talformat; valutaformatet har index 5. Vi hämtar standardstilen från det första kalkylbladet, justerar dess talformat och sparar den för senare bruk.

```java
// Step 3: Get the default style and set a currency number format
Style currencyStyle = workbook.getWorksheets().get(0).getCells().getDefaultStyle();
currencyStyle.setNumber(5); // 5 = built‑in currency format ($#,##0.00)
```

Varför använda standardstilen som bas? Den innehåller redan arbetsbokens standardteckensnitt, justering och andra inställningar, så du behöver bara ändra det som är viktigt – i detta fall talformatet. Om du behövde ett eget format (t.ex. “€#,##0.00”) kunde du anropa `currencyStyle.setCustom("#,##0.00 €")` istället.

## Steg 4: Ställ in importalternativ – Länka stil‑arrayen

Aspose.Cells låter dig skicka en array av `Style`‑objekt som motsvarar de kolumner som importeras. Eftersom vår data bara har en kolumn, levererar vi en enklalement‑array som innehåller valutastilen.

```java
// Step 4: Configure import options with the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(new Style[] { currencyStyle });
```

Om du någonsin behöver formatera flera kolumner olika, utöka bara arrayen: `new Style[] { styleForCol1, styleForCol2, … }`. Ordningen på stilarna matchar ordningen på kolumnerna i källdata.

## Steg 5: Importera data – För in Datatable i kalkylbladet

Med arbetsboken klar, data förberedd och stilar definierade, importerar vi äntligen **import datatable to excel**. Vi börjar i cell `A1`, inkluderar kolumnrubriker (`true`) och överlämnar `ImportTableOptions`.

```java
// Step 5: Perform the import
Worksheet worksheet = workbook.getWorksheets().get(0);
worksheet.getCells().importDataTable(dataRows, true, "A1", importOptions);
```

Lägg märke till flaggan `true` – Aspose.Cells genererar automatiskt en rubrikrad baserat på kartnycklarna (`"Amount"`). Om du sätter den till `false` skulle rubriken utelämnas, vilket ger dig mer kontroll över den slutgiltiga layouten.

## Steg 6: Spara filen – Create Excel Workbook Java på disk

Den sista pusselbiten är att persistera den minnes‑arbetsboken till en fysisk fil. Du kan välja vilket format som helst som Aspose stödjer (`.xlsx`, `.xls`, `.csv`, …). Här sparar vi som en XLSX‑fil.

```java
// Step 6: Save the workbook to disk
String outputPath = "DataTableWithCurrencyStyle.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Efter att programmet har körts, öppna den genererade filen. Du kommer att se kolumnen `"Amount"` formaterad med ett dollartecken, två decimaler och korrekta tusentalsavgränsare – exakt vad du förväntar dig när du **apply number format excel** för valutavärden.

## Förväntat resultat

| Amount |
|--------|
| $1,234.56 |
| $7,890.12 |

Rubriken “Amount” visas i fet stil (standardstil), och varje cell under visar det valutaformat vi satte. Ingen manuell formatering i Excel behövs.

## Pro‑tips och vanliga fallgropar

- **Reuse Styles Wisely** – Stilar är lätta, men att skapa en ny `Style` för varje cell kan försämra prestandan. Återanvänd alltid ett stilobjekt när du applicerar samma format på många celler, precis som vi gjorde med `currencyStyle`.
- **Custom Formats** – Om ditt språk använder en annan valutasymbol, ersätt `currencyStyle.setNumber(5)` med `currencyStyle.setCustom("€#,##0.00")`. Testa formatet i Excel för att bekräfta att det fungerar som förväntat.
- **Large Datasets** – För tusentals rader, överväg att använda `importDataTable` med flaggan `ImportTableOptions.setImportDataOnly(true)` för att hoppa över rubrikgenerering och snabba upp importen.
- **Thread Safety** – Aspose.Cells‑objekt är **not** trådsäkra. Skapa en separat `Workbook` per tråd om du genererar rapporter parallellt.

## Vanliga frågor

**Q: Kan jag applicera talformatet på en befintlig arbetsbok?**  
A: Absolut. Öppna arbetsboken med `new Workbook("Existing.xlsx")`, hämta mål‑kalkylbladet och följ steg 3‑5 för att applicera stil‑arrayen på ny data.

**Q: Vad om jag behöver formatera datum istället för valuta?**  
A: Använd ett annat inbyggt tal‑index (`14` för kort datum, `22` för långt datum) eller ett eget format som `yyyy‑mm‑dd`. Arbetsflödet förblir detsamma.

**Q: Fungerar detta med äldre Excel‑versioner (.xls)?**  
A: Ja. Byt bara filändelsen i `workbook.save("MyFile.xls")`. Aspose byter automatiskt till det binära formatet.

## Sammanfattning – Vad vi uppnådde

Vi har **applied number format excel** på en kolumn med monetära värden, demonstrerat hur man **apply currency style excel**, visat det enklaste sättet att **create excel workbook java**, och använt Aspose.Cells för att **import datatable to excel** utan att röra UI‑delen. Allt detta gjordes i ett kort, självständigt program som du kan kopiera, klistra in och köra.

Vad blir nästa steg? Prova att utöka exemplet:

- Lägg till fler kolumner (t.ex. “Date”, “Description”) och tilldela olika stilar per kolumn.
- Exportera samma data till CSV och jämför hur talformat försvinner.
- Integrera koden i en Spring Boot‑tjänst som returnerar arbetsboken som ett nedladdningsbart HTTP‑svar.

Känn dig fri att experimentera, och om du stöter på problem, lämna en kommentar nedan. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närliggande ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man applicerar stilar på Excel-celler med Aspose.Cells för Java – Komplett guide](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Sammanfoga celler och applicera stilar i Excel med Aspose.Cells för Java – En komplett guide](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Aspose.Cells för Java: Hur man skapar och formaterar Excel-arbetsböcker effektivt](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}