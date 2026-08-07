---
category: general
date: 2026-07-03
description: Hur man formaterar Excel-filer med Java. Lär dig att formatera datumkolumn
  i Excel, tillämpa talformat i Excel, exportera DataTable till XLSX och importera
  DataTable till Excel med Aspose Cells.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: sv
og_description: Hur man formaterar Excel-filer i Java. Denna handledning visar hur
  man formaterar datumkolumn i Excel, tillämpar talformat i Excel, exporterar DataTable
  till XLSX och importerar DataTable till Excel.
og_title: Hur du stylar Excel – Java‑guide för anpassad kolumnformatering
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Hur man formaterar Excel – Importera DataTable med anpassad formatering i Java
url: /sv/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man formaterar Excel – Importera DataTable med anpassad formatering i Java

Har du någonsin undrat **how to style Excel** blad programatiskt utan att öppna filen manuellt? Du är inte ensam. Många utvecklare behöver generera rapporter där den första kolumnen är fet, den andra visar datum, och resten följer en ren layout. I den här guiden går vi igenom ett komplett, körbart exempel som **imports a DataTable into Excel**, applicerar ett fet rubrik, formaterar en datumkolumn och slutligen **exports DataTable to XLSX**.  

Vi kommer att använda Aspose.Cells for Java, men koncepten kan överföras till vilket bibliotek som helst som låter dig arbeta med stilar. I slutet kommer du att ha ett återanvändbart mönster för **apply number format Excel** celler, **format column date Excel**, och leverera en polerad arbetsbok till dina användare.

## Förutsättningar

- Java 17 (eller någon nyare JDK)  
- Aspose.Cells for Java 23.9 eller nyare (gratis provversion fungerar bra)  
- En `DataTable`‑liknande struktur (exemplet använder en enkel mock)  
- Din favorit‑IDE (IntelliJ IDEA, Eclipse, VS Code…)

Inga extra Maven‑plugin behövs; lägg bara till Aspose.Cells‑JAR‑filen i din classpath.

---

## Steg 1: Hämta käll‑DataTable – “Export DataTable to XLSX” förberedelse

Innan vi kan **import datatable into excel**, behöver vi ett `DataTable`‑objekt som representerar de data du vill exportera. I riktiga projekt kan du hämta detta från en databas, CSV‑fil eller ett API. För den här tutorialen kommer vi att mocka en liten tabell:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Varför detta är viktigt:** Att få data rätt från början betyder att resten av stil‑logiken kan fokusera enbart på presentation, inte datamanipulation.

---

## Steg 2: Skapa en array för att hålla stildefinitioner för varje kolumn

Aspose.Cells låter dig skicka en **Style[]**‑array när du importerar en `DataTable`. Varje post motsvarar en kolumn och bestämmer hur den kolumnen kommer att se ut efter importen. Låt oss allokera arrayen baserat på antalet kolumner:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Tips:** Om du har många kolumner, överväg att bygga arrayen i en loop och återanvända ett enda `Style`‑objekt där formateringen är identisk. Detta minskar minnesbelastningen.

---

## Steg 3: Definiera stilarna – Fet rubrik & datumformatering

Nu svarar vi på den klassiska **format column date excel**‑frågan och demonstrerar också **apply number format excel** för andra kolumner.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**Vad händer här?**  
- `StyleNumberFormat.DATE` talar om för Excel att behandla cellens värde som ett kort datum (t.ex. *01/31/2024*).  
- `StyleNumberFormat.CURRENCY_USD` lägger automatiskt till `$`‑symbolen och två decimaler.  
- Att sätta teckensnittet till fet i den första kolumnen får rubriken att sticka ut, vilket är ett vanligt krav när du **how to style excel** kalkylblad för läsbarhet.

> **Edge case:** Om dina källdata redan innehåller formaterade strängar kan du behöva konvertera dem till `java.util.Date`‑objekt innan import; annars kommer Excel att behandla dem som vanlig text.

---

## Steg 4: Skapa en ny arbetsbok och få åtkomst till dess första kalkylblad

En ny arbetsbok ger oss en ren canvas. Vi hämtar det första kalkylbladet, där importen kommer att hamna.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Varför en ny arbetsbok?** Att börja från början garanterar att inga kvarvarande stilar eller dolda rader stör slutresultatet—viktigt när du **how to style excel** filer konsekvent över flera körningar.

---

## Steg 5: Importera DataTable med kolumnstilar

Här är kärnan i operationen: mata in `DataTable` i bladet samtidigt som vi applicerar stil‑arrayen vi byggde.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Förklaring:**  
- `importDataTable` kopierar både rubrikraden och dataraderna.  
- `columnStyles`‑arrayen matchar varje kolumn, så den första kolumnens rubrik blir fet, den andra kolumnen visar datum, och den tredje kolumnen visas som valuta.  
- Denna enda rad ersätter dussintals manuella cell‑för‑cell formateringssteg, vilket visar ett rent sätt att **apply number format excel** programatiskt.

---

## Steg 6: Spara den formaterade arbetsboken – Slutför “Export DataTable to XLSX”

Till slut sparar vi arbetsboken till disk. Justera sökvägen till en skrivbar mapp på din maskin.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Öppna filen i Excel så bör du se:

- Kolumn **ID** rubrik i fet stil.  
- **OrderDate** kolumn formaterad som datum (t.ex. *04/27/2024*).  
- **Total** kolumn visas med dollartecken och två decimaler.

> **Pro tip:** Om du behöver stödja äldre Excel‑versioner, anropa `workbook.save(outputPath, SaveFormat.XLS)` istället för standard‑XLSX.

---

## Steg 7: Verifiera resultatet & valfria justeringar

Det är god praxis att dubbelkolla den genererade filen, särskilt när du automatiserar rapporter för intressenter.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

Om `isBold` skriver ut `true`, har din **how to style excel**‑rutin fungerat som avsett. Härifrån kan du:

- Lägg till villkorsstyrd formatering (t.ex. markera totals > $200).  
- Frys den översta raden för enklare scrollning.  
- Infoga ett diagram som refererar till de importerade data.

---

## Vanliga frågor & edge‑cases

| Fråga | Svar |
|----------|--------|
| **Kan jag formatera mer än en kolumn på samma sätt?** | Ja—återanvänd ett enda `Style`‑instans för alla kolumner som delar samma formatering. |
| **Vad händer om min DataTable har fler kolumner än stilar?** | Alla kolumner utan motsvarande post i `columnStyles` kommer att använda standardstilen. |
| **Hur ändrar jag datumformatet till “dd‑MMM‑yyyy”?** | Använd `columnStyles[1].setCustom("#dd-MMM-yyyy#");` istället för den inbyggda `DATE`. |
| **Finns det ett sätt att automatiskt anpassa kolumnbredd efter import?** | Anropa `worksheet.autoFitColumns();` efter `importDataTable`. |
| **Fungerar detta på Linux/macOS?** | Absolut—Aspose.Cells är plattformsoberoende så länge du har en kompatibel JDK. |

---

## Slutsats

Du har nu ett gediget, end‑to‑end‑exempel på **how to style Excel** arbetsböcker genom att **importing datatable into excel**, **format column date excel**, och **apply number format excel** med Java. Koden visar hela flödet från **export datatable to xlsx** till att öppna filen i Excel, och täcker både *vad* och *varför* bakom varje steg.  

Prova det: justera stil‑arrayen, lägg till fler kolumner, eller anslut en riktig databasfråga. Samma mönster låter dig generera professionellt utseende rapporter med ett knapptryck, utan manuell formatering.

---

![Styled Excel worksheet generated by the tutorial code](https://example.com/images/styled-worksheet.png "Screenshot of styled Excel worksheet created using Java and Aspose.Cells")

*Image alt text: “Formaterat Excel‑arbetsblad skapat med Java och Aspose.Cells, visar fet rubrik och formaterad datumkolumn.”*

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man skapar och formaterar Excel‑celler med Aspose.Cells för Java: En steg‑för‑steg‑guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Hur man formaterar Excel‑celler och lägger till hyperlänkar med Aspose.Cells för Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells för Java: Hur man skapar och formaterar Excel‑arbetsböcker effektivt](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}