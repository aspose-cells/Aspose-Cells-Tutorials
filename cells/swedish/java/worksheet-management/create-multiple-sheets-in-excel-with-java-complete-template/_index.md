---
category: general
date: 2026-06-21
description: Skapa flera blad i Excel med Java. Lär dig hur du exporterar data till
  blad, använder en mallbaserad Excel‑metod och sparar arbetsboken xlsx effektivt.
draft: false
keywords:
- create multiple sheets
- export data to sheets
- template based excel
- save workbook xlsx
- insert index worksheet
language: sv
og_description: Skapa flera blad i Excel med Java. Denna guide visar hur du exporterar
  data till blad, tillämpar ett mallbaserat Excel‑arbetsflöde och sparar arbetsboken
  som xlsx.
og_title: Skapa flera blad i Excel med Java – Steg för steg
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiple sheets in Excel using Java. Learn how to export data
    to sheets, use a template based Excel approach, and save workbook xlsx efficiently.
  headline: Create Multiple Sheets in Excel with Java – Complete Template‑Based Guide
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
- Automation
title: Skapa flera blad i Excel med Java – komplett mallbaserad guide
url: /sv/java/worksheet-management/create-multiple-sheets-in-excel-with-java-complete-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa flera blad i Excel med Java – Komplett mallbaserad guide

Har du någonsin behövt **skapa flera blad** i en Excel-arbetsbok från en Java-applikation men varit osäker på var du ska börja? Du är inte ensam. Oavsett om du bygger en rapporteringsmotor, ett data‑exportverktyg, eller bara försöker automatisera en tråkig kalkylbladsuppgift, så kan behärskning av hur man *exporterar data till blad* spara dig timmar av manuellt arbete.

I den här handledningen går vi igenom en **mallbaserad Excel**-lösning som låter dig infoga ett indexarbetsblad, generera ett blad per dataobjekt och slutligen **spara arbetsbok xlsx** med ett enda metodanrop. Inga onödiga detaljer, bara ett praktiskt, end‑to‑end‑exempel som du kan lägga in i ditt projekt idag.

## Vad du kommer att lära dig

- Hur man initierar en arbetsbok som kommer att hålla **flera blad**.
- Använda Aspose.Cells Smart Marker‑syntax för att automatiskt upprepa arbetsblad.
- Förbereda en datakälla (lista med mappar, POJOs eller någon samling) för mallen.
- Applicera mallen med `SmartMarkerProcessor`.
- Spara resultatet som en **xlsx**‑fil.
- Valfria tips för att infoga ett indexarbetsblad och hantera kantfall.

*Förutsättningar*: Java 8+, Maven eller Gradle, och Aspose.Cells för Java-biblioteket (den fria provversionen fungerar bra för testning). Om du är ny på Aspose, oroa dig inte—vi håller installationsstegen korta.

---

## Steg 1: Initiera arbetsboken – Duken för **Create Multiple Sheets**

Innan några blad visas behöver du en `Workbook`‑instans. Tänk på den som en tom duk som senare kommer att hålla varje genererat arbetsblad.

```java
import com.aspose.cells.*;

public class MultiSheetExporter {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty workbook that will hold the generated worksheets
        Workbook workbook = new Workbook();
        // ... we'll add more code here later
    }
}
```

> **Varför detta är viktigt:** `Workbook`‑objektet abstraherar hela Excel‑filen. Genom att börja med en tom arbetsbok behåller du full kontroll över bladskapande, formatering och slutgiltig sparning.

---

## Steg 2: Definiera en **Template Based Excel**‑markör – Ritningen för varje blad

Aspose.Cells Smart Marker‑motor låter dig bädda in platshållare direkt i en strängmall. Den speciella `${#WorksheetRepeat}`‑markören instruerar processorn att starta ett **nytt arbetsblad** för varje objekt i datainsamlingen.

```java
// Step 2: Define a Smart Marker template.
// ${#WorksheetRepeat} starts a new worksheet for each item in the data collection.
// ${Index} inserts the current item index, and ${Data} inserts the item value.
String template = "${#WorksheetRepeat}Sheet${Index}\n${Data}";
```

**Proffstips:** Tecknet `\n` skapar en ny rad efter bladnamnet, så den första raden i varje blad kommer att innehålla det faktiska datavärdet. Justera mallen för att inkludera rubriker, formler eller formatering efter behov.

---

## Steg 3: Förbered din datakälla – **Export Data to Sheets** gjort enkelt

Mallen fungerar med vilken samling som helst som Aspose kan iterera över. I detta exempel använder vi en `List<Map<String,Object>>`, men du kan lika lätt skicka en lista med POJOs.

```java
// Step 3: Prepare the data source (a list of maps, objects, etc.).
// Replace this with your actual data collection.
List<Map<String, Object>> dataList = getData(); // placeholder for your data
```

Här är en snabb mock‑implementation som du kan kopiera‑klistra in under testning:

```java
private static List<Map<String, Object>> getData() {
    List<Map<String, Object>> list = new ArrayList<>();
    for (int i = 1; i <= 5; i++) {
        Map<String, Object> row = new HashMap<>();
        row.put("Data", "Row value " + i);
        list.add(row);
    }
    return list;
}
```

**Varför en map?** Att använda en map ger dig nyckel‑värde‑par som matchar `${Data}`‑platshållaren. Om du föredrar POJOs, se bara till att fältnamnen stämmer överens med dina markörer.

---

## Steg 4: Initiera **SmartMarkerProcessor** – Motorn bakom magin

Nu när vi har en arbetsbok och en mall, behöver vi processorn som ska sammanfoga dem.

```java
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

Processorn läser mallen, itererar över `dataList` och skapar ett nytt arbetsblad för varje post. Ingen manuell loopning behövs.

---

## Steg 5: Applicera mallen – **Insert Index Worksheet** och generera blad

I det här skedet kan du helt enkelt anropa `processor.apply(template, dataList);`. Många användare vill dock också ha ett **indexarbetsblad** som listar alla genererade bladnamn med klickbara länkar. Nedan är ett tvåstegstillvägagångssätt:

1. **Generera datasbladen** med hjälp av mallen.
2. **Skapa ett indexblad** och fyll det med hyperlänkar.

```java
// Step 5a: Apply the template to the data.
// A new worksheet is created for each element in dataList.
processor.apply(template, dataList);

// Step 5b (optional): Insert an index worksheet at the beginning.
Worksheet indexSheet = workbook.getWorksheets().add("Index");
int row = 0;
indexSheet.getCells().setColumnWidth(0, 25);
indexSheet.getCells().setColumnWidth(1, 30);
indexSheet.getCells().setRowHeight(row, 20);
indexSheet.getCells().get(row, 0).setValue("Sheet Name");
indexSheet.getCells().get(row, 1).setValue("Link");

// Loop through generated sheets and add a hyperlink entry.
for (int i = 0; i < dataList.size(); i++) {
    String sheetName = "Sheet" + (i + 1);
    row++;
    indexSheet.getCells().get(row, 0).setValue(sheetName);
    // Create a hyperlink that points to the generated worksheet.
    Hyperlink link = indexSheet.getHyperlinks().add(row, 1, 1, 1,
            "'" + sheetName + "'!A1", "Go to " + sheetName);
    indexSheet.getCells().get(row, 1).setValue("Open");
}
```

**Förklaring:**  
- Loopen bygger en prydlig tabell där varje rad länkar till motsvarande blad.  
- Genom att använda `Hyperlink.add` säkerställs en klickbar referens i Excel.  
- Detta steg demonstrerar **insert index worksheet** i praktiken, vilket gör navigeringen smidig för slutanvändare.

---

## Steg 6: **Save Workbook Xlsx** – Ett anrop, redo för distribution

Till sist, skriv arbetsboken till disk. `save`‑metoden upptäcker automatiskt filformatet från filändelsen.

```java
// Step 6: Save the workbook to a file
workbook.save("YOUR_DIRECTORY/output.xlsx");
System.out.println("Workbook saved successfully!");
```

**Tips:** Om du behöver strömma filen direkt till ett HTTP‑svar (t.ex. i en Spring‑controller), använd `workbook.save(outputStream, SaveFormat.XLSX);` istället.

---

## Fullständigt fungerande exempel – Kopiera‑klistra redo

Nedan är det kompletta programmet som sätter ihop alla delar. Byt bara ut `"YOUR_DIRECTORY"` mot en riktig sökväg på din maskin.

```java
import com.aspose.cells.*;
import java.util.*;

public class MultiSheetExporter {
    public static void main(String[] args) throws Exception {
        // Initialise an empty workbook (Step 1)
        Workbook workbook = new Workbook();

        // Define the Smart Marker template (Step 2)
        String template = "${#WorksheetRepeat}Sheet${Index}\n${Data}";

        // Prepare data (Step 3)
        List<Map<String, Object>> dataList = getData();

        // Initialise the processor (Step 4)
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // Apply template (Step 5a)
        processor.apply(template, dataList);

        // Optional: Insert an index worksheet (Step 5b)
        Worksheet indexSheet = workbook.getWorksheets().add("Index");
        int row = 0;
        indexSheet.getCells().setColumnWidth(0, 25);
        indexSheet.getCells().setColumnWidth(1, 30);
        indexSheet.getCells().setRowHeight(row, 20);
        indexSheet.getCells().get(row, 0).setValue("Sheet Name");
        indexSheet.getCells().get(row, 1).setValue("Link");

        for (int i = 0; i < dataList.size(); i++) {
            String sheetName = "Sheet" + (i + 1);
            row++;
            indexSheet.getCells().get(row, 0).setValue(sheetName);
            Hyperlink link = indexSheet.getHyperlinks().add(row, 1, 1, 1,
                    "'" + sheetName + "'!A1", "Go to " + sheetName);
            indexSheet.getCells().get(row, 1).setValue("Open");
        }

        // Save the workbook (Step 6)
        workbook.save("YOUR_DIRECTORY/output.xlsx");
        System.out.println("Workbook saved successfully!");
    }

    // Mock data generator
    private static List<Map<String, Object>> getData() {
        List<Map<String, Object>> list = new ArrayList<>();
        for (int i = 1; i <= 5; i++) {
            Map<String, Object> row = new HashMap<>();
            row.put("Data", "Row value " + i);
            list.add(row);
        }
        return list;
    }
}
```

**Förväntad output:**  
- En `output.xlsx`‑fil som innehåller sex arbetsblad (`Index`, `Sheet1` … `Sheet5`).  
- `Index`‑bladet listar varje genererat bladnamn med en klickbar “Open”‑länk.  
- Varje `SheetX` innehåller en enda cell (`A1`) med “Row value X”.

---

## Vanliga frågor & kantfall

| Question | Answer |
|----------|--------|
| **Kan jag använda en CSV- eller JSON‑källa istället för en `List<Map>`?** | Absolut. Aspose’s Smart Marker fungerar med vilken `Iterable`‑samling som helst. Mappa bara dina JSON‑fält till markörnamnen. |
| **Vad händer om min datalista är tom?** | Processorn kommer inte att skapa några extra arbetsblad, men indexbladet kommer fortfarande att läggas till (du kanske vill skydda mot det). |
| **Hur lägger jag till rubriker eller formatering på varje genererat blad?** | Utöka mallen: `${#WorksheetRepeat}Sheet${Index}\nHeader1,Header2\n${Data}`. Du kan också applicera en stil programatiskt efter `apply`. |
| **Finns det en gräns för antalet blad?** | I praktiken begränsar Excel till 1 048 576 rader per blad; antalet blad begränsas bara av minnet. |
| **Behöver jag en licens för Aspose.Cells?** | En gratis utvärdering fungerar för utveckling. För produktion tar en licens bort utvärderingsvattenstämpeln och låser upp alla funktioner. |

---

## Slutsats

Du har nu ett robust **create multiple sheets**‑arbetsflöde i Java som utnyttjar en **template based Excel**‑metod, **exporterar data till blad**, valfritt **infogar ett indexarbetsblad**, och slutligen **sparar workbook xlsx** med en enda kodrad. Detta mönster skalar smidigt—från några få rader till massiva dataexporter—och håller din kod ren och underhållbar.

Redo för nästa steg? Prova att lägga till villkorlig formatering, bädda in diagram, eller slå ihop indexet med en sammanfattande dashboard. Samma Smart Marker‑motor kan hantera dessa scenarier med bara några extra markörer.

Om du stöter på problem, lämna en kommentar nedan eller utforska Aspose.Cells omfattande dokumentation. Lycka till med kodandet, och njut av att automatisera dessa kalkylblad!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Create & Access Excel Sheets, Add PDF Bookmarks Using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Export Excel Sheets to Images Using Aspose.Cells for Java - A Comprehensive Guide](/cells/english/java/workbook-operations/export-excel-sheets-images-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}