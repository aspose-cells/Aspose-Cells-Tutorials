---
category: general
date: 2026-03-27
description: Hur man skapar en pivottabell i C# med Aspose.Cells – lär dig att lägga
  till data, aktivera uppdatering och spara arbetsboken som xlsx i en enda handledning.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: sv
og_description: Hur man skapar en pivottabell i C# med Aspose.Cells. Den här guiden
  visar hur du lägger till data, aktiverar uppdatering och sparar arbetsboken som
  xlsx.
og_title: Hur man skapar en pivottabell i C# – Komplett Aspose.Cells-handledning
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur du skapar en pivottabell i C# – Fullständig guide med Aspose.Cells
url: /sv/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så skapar du pivottabell i C# – Komplett Aspose.Cells-handledning

Har du någonsin funderat **hur man skapar pivottabell** i C# utan att kämpa med COM-interoperabilitet? Du är inte ensam. I många datadrivna appar behöver vi ett snabbt sätt att omvandla råa försäljningssiffror till en snygg sammanfattning, och Aspose.Cells gör det till en barnlek.  

I den här handledningen går vi igenom varje steg: lägga till data, bygga pivottabellen, aktivera automatisk uppdatering och slutligen **spara arbetsbok som xlsx** så att dina användare kan öppna den i Excel omedelbart. I slutet har du en färdig `PivotRefresh.xlsx`-fil och en gedigen förståelse för varför varje rad är viktig.

## Förutsättningar

- .NET 6+ (eller .NET Framework 4.7.2 och senare) – någon nyare runtime fungerar.  
- Aspose.Cells för .NET – du kan hämta det från NuGet (`Install-Package Aspose.Cells`).  
- En grundläggande kunskap om C#-syntax – ingen djup Excel‑kunskap krävs.  

> **Proffstips:** Om du använder en företagsdator, se till att Aspose‑licensen är tillämpad; annars får du ett vattenmärke på den genererade filen.

## Steg 1 – Hur man lägger till data i en ny arbetsbok

Innan en pivottabell kan existera måste det finnas en källtabell. Vi skapar en ny arbetsbok, namnger det första kalkylbladet *SalesData* och lägger till några rader som efterliknar en verklig försäljningsdump.

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**Varför detta är viktigt:**  
- Att använda `PutValue` sätter automatiskt celltypen, så du behöver inte oroa dig för sträng‑ vs numeriska mismatchar senare.  
- Att definiera rubriker i rad 1 ger pivottabell‑motorn något att referera till när du mappar fält.

## Steg 2 – Skapa ett kalkylblad som ska innehålla pivottabellen

En pivottabell ligger på ett eget blad, vilket håller källdata rena och rapporten prydlig.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **Vad händer om du redan har ett blad?** Referera bara till det med index (`workbook.Worksheets["MySheet"]`) istället för att lägga till ett nytt.

## Steg 3 – Definiera källintervallet (Hur man lägger till data → Definiera intervall)

Aspose.Cells behöver ett `CellArea` eller en intervallsträng som omfattar både rubriker och data. Här antar vi högst 100 rader; justera vid behov.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Specialfall:**  
Om din dataset är dynamisk kan du beräkna den sista använda raden med `salesDataSheet.Cells.MaxDataRow` och bygga intervallet därefter.

## Steg 4 – Hur man skapar pivottabell – Infoga pivottabellen

Nu blir det roligt: vi instruerar Aspose.Cells att skapa en pivottabell kopplad till intervallet vi just definierat.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

Observera formel‑stilen referensen (`=SalesData!A1:D100`). Det är samma syntax som du skulle skriva in i Excel, vilket gör API:et intuitivt.

## Steg 5 – Konfigurera rad‑, kolumn‑ och datafält (Hur man lägger till data → Fält)

Vi placerar *Region* på rader, *Product* på kolumner och summerar både *Units* och *Revenue*.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**Varför dessa index?**  
Aspose.Cells indexerar kolumner med start 0, så `0` pekar på *Region*. Metoden `DataFields.Add` låter dig byta namn på fältet (t.ex. “Sum of Units”) och välja en aggregeringstyp – `Sum` är den vanligaste för numerisk data.

## Steg 6 – Hur man aktiverar uppdatering – Gör så att pivottabellen automatiskt uppdateras vid öppning

Om källdata ändras senare vill du förmodligen att pivottabellen automatiskt återspeglar dessa förändringar. Det är där `RefreshDataOnOpen` kommer in.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **Obs:** Denna flagga fungerar bara när arbetsboken öppnas i Excel; den kommer inte att omberäkna i Aspose.Cells om du inte manuellt anropar `pivotTable.RefreshData()`.

## Steg 7 – Spara arbetsbok som XLSX (Hur man sparar arbetsbok som XLSX)

Till sist sparar vi filen på disk. `.xlsx`‑formatet är den moderna, zip‑baserade Excel‑filtypen som fungerar överallt.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

När programmet körs skapas en fil med namnet **PivotRefresh.xlsx** i körningsmappen. Öppna den i Excel så ser du en prydligt uppställd pivottabell med *Region*-rader, *Product*-kolumner och summerade *Units*- och *Revenue*-värden. Eftersom vi aktiverade uppdatering kommer alla ändringar du gör i *SalesData*-bladet automatiskt att uppdatera pivottabellen nästa gång du öppnar arbetsboken.

### Förväntat resultat

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Summa** | **120** | **85** |   |

*(Numren kan variera beroende på vilka rader du lägger till.)*

---

## Vanliga frågor & varianter

### Vad händer om jag behöver flera pivottabeller?

Du kan upprepa **Steg 4** med ett annat namn och en annan plats. Varje anrop till `PivotTables.Add` returnerar ett nytt index som du kan använda för att hämta tabellobjektet.

### Hur ändrar jag aggregeringen till *Average* istället för *Sum*?

Byt ut `PivotTableDataAggregationType.Sum` mot `PivotTableDataAggregationType.Average` i anropen till `DataFields.Add`.

### Kan jag styla pivottabellen (typsnitt, färger)?

Ja. Efter att pivottabellen skapats kan du komma åt dess `Style`‑egenskap eller applicera cellformatering på intervallet som innehåller pivottabellen. Till exempel:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### Är det möjligt att lägga till fler rader efter att arbetsboken sparats?

Absolut. Läs in filen med `new Workbook("PivotRefresh.xlsx")`, lägg till rader i *SalesData*-bladet och anropa `pivotTable.RefreshData()` innan du sparar igen.

## Fullt fungerande exempel (Klar att kopiera‑klistra in)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Spara filen, kör den och öppna den genererade **PivotRefresh.xlsx** – du har just bemästrat **hur man skapar pivottabell** i C#.

## Avslutning

Vi har gått igenom **hur man skapar pivottabeller** programatiskt, hur man **lägger till data**, hur man **aktiverar uppdatering**, och slutligen hur man **sparar arbetsbok som xlsx** med Aspose.Cells. Koden

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}