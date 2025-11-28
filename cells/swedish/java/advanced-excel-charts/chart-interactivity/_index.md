---
date: 2025-11-28
description: Lär dig hur du lägger till verktygstips, datamärkningar och drill‑down‑funktioner
  för att skapa ett interaktivt diagram i Java med Aspose.Cells.
language: sv
linktitle: How to Add Tooltips in Interactive Charts
second_title: Aspose.Cells Java Excel Processing API
title: Hur man lägger till verktygstips i interaktiva diagram (Aspose.Cells Java)
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Hur man lägger till verktygstips i interaktiva diagram (Aspose.Cells Java)

## Introduktion

Interaktiva diagram låter användare utforska data genom att hovra, klicka eller gräva ner i detaljer. I den här handledningen lär du dig **hur man lägger till verktygstips** i ett diagram, samt hur du **lägger till data labels**, och implementerar **drill‑down**‑navigation – allt med Aspose.Cells för Java. I slutet kommer du kunna bygga ett fullt utrustat, interaktivt diagram som gör dina datapresentationer mer engagerande och insiktsfulla.

## Snabba svar
- **Vilket bibliotek behövs?** Aspose.Cells for Java (senaste versionen).  
- **Vilken primär funktion täcker den här guiden?** Att lägga till verktygstips i diagram.  
- **Kan jag också lägga till data labels?** Ja – se avsnittet “Lägg till data labels”.  
- **Stöds drill‑down?** Ja, via hyperlänkar på datapunkter.  
- **Vilket filformat produceras?** En Excel‑arbetsbok (`.xlsx`) med ett interaktivt diagram.

## Vad är att lägga till verktygstips?

Ett verktygstips är ett litet popup‑fönster som visas när en användare hovrar över ett diagram‑element och visar ytterligare information såsom exakt värde eller ett anpassat meddelande. Verktygstips förbättrar dataläsbarheten utan att röras upp det visuella layoutet.

## Varför skapa interaktiva diagram i Java?

- **Bättre beslutsfattande:** Användare kan omedelbart se exakta värden.  
- **Professionella rapporter:** Interaktiva element får instrumentpaneler att se moderna ut.  
- **Återanvändbara komponenter:** När du behärskar API‑et kan du tillämpa det på alla Excel‑baserade rapportlösningar.

## Förutsättningar

Innan vi dyker ner, se till att du har:

- En Java‑utvecklingsmiljö (JDK 8 eller nyare).  
- Aspose.Cells for Java‑biblioteket (ladda ner från [here](https://releases.aspose.com/cells/java/)).  
- En exempel‑Excel‑fil med namnet **data.xlsx** som innehåller den data du vill visualisera.

## Steg 1: Ställa in ditt Java‑projekt

1. Skapa ett nytt Java‑projekt i din föredragna IDE (IntelliJ IDEA, Eclipse, osv.).  
2. Lägg till Aspose.Cells‑JAR‑filen i projektets classpath.

## Steg 2: Ladda data

För att skapa ett interaktivt diagram behöver du först ett arbetsblad med data. Koden nedan laddar det första arbetsbladet från **data.xlsx**.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Steg 3: Skapa ett diagram

Nu lägger vi till ett stapeldiagram i arbetsbladet. Diagrammet kommer att uppta cellerna F6 till K16.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Steg 4: Lägga till interaktivitet

### 4.1. Hur man lägger till verktygstips

Följande kodsnutt aktiverar verktygstips för den första serien i diagrammet. Varje datapunkt visar sitt värde när man hovrar.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Lägg till data labels i diagrammet

Om du också vill ha synliga etiketter bredvid varje stapel, använd **add data labels chart**‑metoden som visas nedan. Detta uppfyller det sekundära nyckelordet *add data labels chart*.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Hur man gör drill‑down (implementering av drill‑down)

Drill‑down låter användare klicka på en datapunkt och hoppa till en detaljerad vy (t.ex. en webbsida). Här bifogar vi en hyperlänk till den första punkten i serien.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Pro tip:** Du kan generera URL‑en dynamiskt baserat på punktens värde för att skapa en verkligt datadriven drill‑down‑upplevelse.

## Steg 5: Spara arbetsboken

Efter att ha konfigurerat diagrammet, spara arbetsboken. Den resulterande filen innehåller ett interaktivt diagram som är redo att öppnas i Excel.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Vanliga problem och lösningar

| Problem | Orsak | Lösning |
|---------|-------|---------|
| Verktygstips visas inte | Data labels är inte aktiverade | Se till att `setHasDataLabels(true)` anropas innan `ShowValue` sätts. |
| Hyperlänk är inte klickbar | Fel punktindex | Verifiera att du refererar till rätt punkt (`get(0)` är den första punkten). |
| Diagrammet ser felplacerat ut | Fel cellintervall | Justera rad-/kolumnindexen i `add(ChartType.COLUMN, row1, col1, row2, col2)`. |

## Vanliga frågor

**Q: Hur kan jag ändra diagramtyp?**  
A: Byt ut `ChartType.COLUMN` mot ett annat enum‑värde såsom `ChartType.LINE` eller `ChartType.PIE` när du anropar `worksheet.getCharts().add(...)`.

**Q: Kan jag anpassa utseendet på verktygstips?**  
A: Ja. Använd `DataLabel`‑objektets formaterings‑egenskaper (teckenstorlek, bakgrundsfärg osv.) för att styla verktygstips‑texten.

**Q: Hur hanterar jag användarinteraktioner i en webbapplikation?**  
A: Exportera arbetsboken till ett webb‑kompatibelt format (t.ex. HTML) och använd JavaScript för att fånga klick‑händelser på diagram‑element.

**Q: Var kan jag hitta fler exempel och dokumentation?**  
A: Utforska den officiella API‑referensen på [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/).

**Q: Är det möjligt att lägga till flera drill‑down‑länkar i samma diagram?**  
A: Absolut. Loopa igenom seriernas punkter och tilldela en unik URL till varje punkts `Hyperlinks`‑samling.

## Slutsats

I den här guiden lärde du dig **hur man lägger till verktygstips**, **lägger till data labels** och **implementerar drill‑down**‑funktionalitet för att skapa en **create interactive chart java**‑lösning med Aspose.Cells. Dessa funktioner förvandlar statiska Excel‑diagram till dynamiska, användarvänliga visualiseringar som hjälper intressenter att utforska data med lätthet.

---

**Senast uppdaterad:** 2025-11-28  
**Testad med:** Aspose.Cells for Java 24.12  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}