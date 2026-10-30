---
category: general
date: 2026-07-03
description: Skapa master‑detail‑arbetsbok med Aspose.Cells smart marker – automatisera
  skapandet av Excel‑blad utan ansträngning och öka produktiviteten.
draft: false
keywords:
- create master detail workbook
- automate excel sheet creation
- aspose.cells smart marker
language: sv
og_description: Skapa master‑detail‑arbetsbok med Aspose.Cells smart marker. Lär dig
  hur du automatiserar skapandet av Excel‑ark på några minuter.
og_title: Skapa master‑detail‑arbetsbok – Aspose.Cells Smart Marker‑guide
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Create master detail workbook using Aspose.Cells smart marker – automate
    Excel sheet creation effortlessly and boost productivity.
  headline: Create Master Detail Workbook with Aspose.Cells Smart Marker
  type: TechArticle
tags:
- Aspose.Cells
- Excel
- SmartMarker
- C#
title: Skapa master‑detailarbetsbok med Aspose.Cells Smart Marker
url: /sv/net/smart-markers-dynamic-data/create-master-detail-workbook-with-aspose-cells-smart-marker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Master‑Detail‑arbetsbok med Aspose.Cells Smart Marker

Har du någonsin behövt **skapa en master‑detail‑arbetsbok** men känt dig fast när du måste duplicera blad för varje datarad? Du är inte ensam. I många rapporteringsscenarier slutar du med att skriva repetitiv VBA eller göra manuella kopiera‑och‑klistra, vilket både är felbenäget och tidskrävande.  

Den goda nyheten är att Aspose.Cells smart‑marker‑teknik låter dig **automatisera skapandet av Excel‑blad** med bara några rader C#‑kod. I den här handledningen går vi igenom hela processen—från att ladda en mall‑arbetsbok till att generera detaljblad och spara den slutgiltiga filen—så att du kan fokusera på affärslogiken istället för att trixa med Excel‑gränssnittet.

När du är klar med guiden kommer du exakt att kunna:

* Ladda en befintlig arbetsbok som innehåller en master‑detail‑smart‑marker‑layout.  
* Koppla vilken .NET‑datakälla som helst (DataTable, List<T> osv.) till processorn.  
* Definiera ett namngivningsmönster för de nyss skapade detaljbladen.  
* Köra smart‑marker‑motorn och producera en polerad master‑detail‑arbetsbok redo för distribution.

Ingen extern verktyg, inga makron—bara ren kod som körs på .NET 6 (eller senare). Låt oss dyka ner.

## Förutsättningar

Innan vi börjar, se till att du har:

| Krav | Varför det är viktigt |
|------|-----------------------|
| **Aspose.Cells for .NET** (senaste versionen) | Tillhandahåller `SmartMarkerProcessor`‑klassen som används i hela exemplet. |
| **.NET 6 SDK** (eller nyare) | Exemplet är skrivet i modern C#; äldre ramverk fungerar fortfarande med mindre justeringar. |
| **En Excel‑mall** (`input.xlsx`) som innehåller en smart marker som `&=MasterData!A1` i masterbladet och en detalj‑platshållare som `&=DetailData!A2` i ett dolt mallblad. | Processorn ersätter dessa markörer med verkliga data vid körning. |
| **En datakälla** (t.ex. `DataTable`, `List<Customer>`) | Här kommer de faktiska raderna för master och detail ifrån. |

Om någon av dessa saknas, hämta Aspose.Cells från NuGet (`Install-Package Aspose.Cells`) och skapa en enkel Excel‑fil med markörerna ovan.

## Steg 1: Skapa projektet och importera namnrymder

Börja med att skapa en konsolapp (eller vilket .NET‑projekt som helst) och importera de nödvändiga namnrymderna. Detta steg är enkelt men avgörande—utan rätt `using`‑direktiv klagar kompilatorn.

```csharp
using System;
using System.Data;               // For DataTable example
using Aspose.Cells;              // Core Aspose.Cells API
using Aspose.Cells.SmartMarkers; // Smart marker processor
```

*Varför detta är viktigt:* `Aspose.Cells` ger dig möjligheter att manipulera arbetsböcker, medan `Aspose.Cells.SmartMarkers` innehåller motorn som analyserar och expanderar markörerna.

## Steg 2: Ladda mall‑arbetsboken

Mall‑arbetsboken (`input.xlsx`) innehåller master‑detail‑layouten med platshållarmarkörer. Att ladda den är en endaste rad, men vi omsluter den också med ett `try/catch` för att tidigt visa eventuella filrelaterade problem.

```csharp
Workbook wb;
try
{
    wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load template workbook: {ex.Message}");
    return;
}
```

*Proffstips:* Håll mallen i en skrivskyddad mapp eller bädda in den som en resurs om du planerar att distribuera den körbara filen.

## Steg 3: Förbered datakällan

Aspose.Cells smart markers kan konsumera i princip vilken enumerabel objekt som helst. För illustration bygger vi en `DataTable` som efterliknar ett master‑detail‑förhållande: en `Customers`‑tabell (master) och en `Orders`‑tabell (detail). `SmartMarkerProcessor` länkar automatiskt rader baserat på en gemensam nyckel.

```csharp
// Master table
DataTable customers = new DataTable("Customers");
customers.Columns.Add("CustomerID", typeof(int));
customers.Columns.Add("CompanyName", typeof(string));
customers.Rows.Add(1, "Acme Corp");
customers.Rows.Add(2, "Globex Ltd");

// Detail table
DataTable orders = new DataTable("Orders");
orders.Columns.Add("CustomerID", typeof(int));
orders.Columns.Add("OrderID", typeof(int));
orders.Columns.Add("Product", typeof(string));
orders.Columns.Add("Quantity", typeof(int));
orders.Rows.Add(1, 101, "Widget", 5);
orders.Rows.Add(1, 102, "Gadget", 2);
orders.Rows.Add(2, 201, "Doohickey", 7);

// Combine into a DataSet (the processor can accept DataSet directly)
DataSet ds = new DataSet();
ds.Tables.Add(customers);
ds.Tables.Add(orders);

// The object we pass to the processor – could also be a List<T> or custom collection
object dataSource = ds;
```

*Varför detta är viktigt:* Genom att använda ett `DataSet` kan processorn lösa relationer automatiskt (t.ex. `Orders`‑rader vars `CustomerID` matchar den aktuella master‑raden). Om du har en annan källa (JSON, EF Core osv.) ersätter du bara `DataSet` med ditt eget objekt.

## Steg 4: Konfigurera SmartMarkerProcessor

Nu instansierar vi processorn och talar om hur vi vill att de nygenererade detaljbladen ska namnges. Platshållaren `{0}` ersätts med ett inkrementellt index som börjar på 1.

```csharp
SmartMarkerProcessor sm = new SmartMarkerProcessor
{
    // Naming pattern for detail sheets: Detail_1, Detail_2, …
    DetailSheetNewName = "Detail_{0}"
};
```

*Edge case‑varning:* Om din arbetsbok redan innehåller blad med namn `Detail_1`, `Detail_2` osv., hoppar processorn automatiskt över dessa namn för att undvika kollisioner.

## Steg 5: Bearbeta arbetsboken

När allt är kopplat sker själva arbetet i ett enda anrop till `Process`. Denna metod skannar arbetsboken efter smart markers, klonar detaljmallsbladet för varje master‑rad och fyller cellerna med data från `dataSource`.

```csharp
try
{
    sm.Process(wb, dataSource);
}
catch (Exception ex)
{
    Console.WriteLine($"Smart marker processing failed: {ex.Message}");
    return;
}
```

*Vad händer under huven?*  
- Processorn läser masterbladet, hittar markören `&=Customers!` och skapar ett nytt blad för varje kund.  
- För varje nytt blad letar den efter `&=Orders!`‑markörer, filtrerar `Orders`‑tabellen efter `CustomerID` och fyller i raderna.  
- Namnmönstret vi satte tidigare säkerställer att varje blad får ett unikt, förutsägbart namn.

## Steg 6: Spara den resulterande arbetsboken

Till sist skriver vi den uppdaterade arbetsboken till disk. Du kan välja vilket format som helst som stöds av Aspose.Cells (`.xlsx`, `.xls`, `.csv` osv.). Här håller vi oss till det moderna `.xlsx`.

```csharp
string outputPath = "YOUR_DIRECTORY/output.xlsx";
wb.Save(outputPath);
Console.WriteLine($"Workbook saved successfully to {outputPath}");
```

*Tips:* Om du behöver streama filen direkt till ett webbsvar, använd overload‑metoden `wb.Save(Stream, SaveFormat.Xlsx)`.

## Fullständigt fungerande exempel

När vi sätter ihop alla bitar får du ett självständigt konsolprogram som du kan kopiera‑klistra in och köra (byt bara ut `YOUR_DIRECTORY` mot en riktig sökväg).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace MasterDetailDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            Workbook wb;
            try
            {
                wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to load template: {ex.Message}");
                return;
            }

            // 2️⃣ Build the data source (DataSet with master & detail tables)
            DataTable customers = new DataTable("Customers");
            customers.Columns.Add("CustomerID", typeof(int));
            customers.Columns.Add("CompanyName", typeof(string));
            customers.Rows.Add(1, "Acme Corp");
            customers.Rows.Add(2, "Globex Ltd");

            DataTable orders = new DataTable("Orders");
            orders.Columns.Add("CustomerID", typeof(int));
            orders.Columns.Add("OrderID", typeof(int));
            orders.Columns.Add("Product", typeof(string));
            orders.Columns.Add("Quantity", typeof(int));
            orders.Rows.Add(1, 101, "Widget", 5);
            orders.Rows.Add(1, 102, "Gadget", 2);
            orders.Rows.Add(2, 201, "Doohickey", 7);

            DataSet ds = new DataSet();
            ds.Tables.Add(customers);
            ds.Tables.Add(orders);
            object dataSource = ds;

            // 3️⃣ Configure the processor (detail sheet naming)
            SmartMarkerProcessor sm = new SmartMarkerProcessor
            {
                DetailSheetNewName = "Detail_{0}"
            };

            // 4️⃣ Run the smart‑marker engine
            try
            {
                sm.Process(wb, dataSource);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Processing error: {ex.Message}");
                return;
            }

            // 5️⃣ Save the output workbook
            string outPath = "YOUR_DIRECTORY/output.xlsx";
            wb.Save(outPath);
            Console.WriteLine($"Successfully created master‑detail workbook at {outPath}");
        }
    }
}
```

**Förväntad utdata:**  
- `output.xlsx` innehåller det ursprungliga masterbladet plus två nya detaljblad med namn `Detail_1` och `Detail_2`.  
- Varje detaljblad listar beställningarna som tillhör den motsvarande kunden, helt ifyllda utan någon manuell kopiera‑och‑klistra.

## Vanliga frågor & Edge Cases

| Fråga | Svar |
|-------|------|
| *Vad händer om min mall redan har ett blad med namn `Detail_1`?* | Processorn ökar automatiskt indexet (`Detail_2`, `Detail_3`, …) tills ett ledigt namn hittas. |
| *Kan jag styra ordningen på de genererade bladen?* | Ja—sätt `sm.DetailSheetNewName` till ett prefix som sorteras alfabetiskt, t.ex. `"01_Detail_{0}"`. |
| *Behöver jag avlasta `Workbook`‑objektet?* | `Workbook` implementerar `IDisposable`; omslut det med en `using`‑block om du är orolig för resurser som inte hanteras. |
| *Är det möjligt att använda en JSON‑sträng som datakälla?* | Konvertera JSON till ett `DataSet` eller en lista av POCO‑objekt först; processorn fungerar med vilken enumerabel som helst. |
| *Hur hanterar jag stora datamängder (10 000+ rader)?* | Aspose.Cells strömmar data effektivt, men du kan öka `Workbook.Settings.MemorySetting` till `MemorySetting.MemoryPreference` för bättre prestanda. |

## Avslutning


## Vad bör du lära dig härnäst?


Följande handledningar täcker nära besläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Skapa en Excel‑arbetsbok med Aspose.Cells i Java: En steg‑för‑steg‑guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Master Excel‑filhantering med Aspose.Cells för Java | Workbook Operations Guide](/cells/english/java/workbook-operations/master-excel-manipulation-aspose-cells-java/)
- [Excel‑automatisering med Aspose.Cells Java: Skapa master‑arbetsbok och kontrollera kolumn‑/rad‑synlighet](/cells/english/java/workbook-operations/excel-automation-aspose-cells-java-workbook-visibility/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}