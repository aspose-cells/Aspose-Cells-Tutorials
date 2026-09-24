---
category: general
date: 2026-03-27
description: Hoe maak je een draaitabel in C# met Aspose.Cells – leer gegevens toe
  te voegen, verversen in te schakelen en de werkmap als xlsx op te slaan in één tutorial.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: nl
og_description: Hoe een draaitabel te maken in C# met Aspose.Cells. Deze gids laat
  zien hoe je gegevens toevoegt, verversen inschakelt en de werkmap opslaat als xlsx.
og_title: Hoe een draaitabel te maken in C# – Complete Aspose.Cells-tutorial
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hoe maak je een draaitabel in C# – Volledige gids met Aspose.Cells
url: /nl/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een draaitabel te maken in C# – Complete Aspose.Cells‑handleiding

Heb je je ooit afgevraagd **hoe je een draaitabel maakt** in C# zonder te worstelen met COM‑interop? Je bent niet de enige. In veel data‑gedreven apps hebben we een snelle manier nodig om ruwe verkoopcijfers om te zetten in een nette samenvatting, en Aspose.Cells maakt dat een eitje.  

In deze tutorial lopen we elke stap door: gegevens toevoegen, de draaitabel bouwen, automatische verversing inschakelen en uiteindelijk **werkmap opslaan als xlsx** zodat je gebruikers deze direct in Excel kunnen openen. Aan het einde heb je een kant‑klaar `PivotRefresh.xlsx`‑bestand en een solide begrip van waarom elke regel belangrijk is.

## Vereisten

- .NET 6+ (of .NET Framework 4.7.2 en later) – elke recente runtime werkt.
- Aspose.Cells for .NET – je kunt het van NuGet halen (`Install-Package Aspose.Cells`).
- Een basiskennis van C#‑syntaxis – geen diepgaande Excel‑kennis vereist.

> **Pro tip:** Als je op een bedrijfscomputer werkt, zorg er dan voor dat de Aspose‑licentie is toegepast; anders krijg je een watermerk op het gegenereerde bestand.

## Stap 1 – Hoe gegevens toe te voegen aan een nieuwe werkmap

Voordat een draaitabel kan bestaan, moet er een bron‑tabel zijn. We maken een nieuwe werkmap, noemen het eerste werkblad *SalesData* en voegen een handvol rijen toe die een real‑world verkoopdump nabootsen.

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

**Waarom dit belangrijk is:**  
- Met `PutValue` wordt automatisch het celtype ingesteld, zodat je later geen zorgen hebt over string‑ versus numerieke mismatches.  
- Het definiëren van koppen in rij 1 geeft de draaitabel‑engine iets om naar te verwijzen wanneer je velden toewijst.

## Stap 2 – Een werkblad maken dat de draaitabel host

Een draaitabel staat op een eigen blad, waardoor de brongegevens schoon blijven en het rapport overzichtelijk.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **Wat als je al een blad hebt?** Verwijs er dan naar via de index (`workbook.Worksheets["MySheet"]`) in plaats van een nieuw blad toe te voegen.

## Stap 3 – Het bronbereik definiëren (Hoe gegevens toe te voegen → Bereik definiëren)

Aspose.Cells heeft een `CellArea` of een bereik‑string nodig die zowel de koppen als de gegevens omvat. Hier gaan we uit van maximaal 100 rijen; pas dit aan naar behoefte.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Randgeval:** Als je dataset dynamisch is, kun je de laatst gebruikte rij berekenen met `salesDataSheet.Cells.MaxDataRow` en het bereik dienovereenkomstig opbouwen.

## Stap 4 – Hoe een draaitabel te maken – De draaitabel invoegen

Nu het leuke deel: we vertellen Aspose.Cells een draaitabel te maken die gekoppeld is aan het bereik dat we zojuist hebben ingesteld.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

Let op de formule‑achtige referentie (`=SalesData!A1:D100`). Dat is dezelfde syntaxis die je in Excel zou typen, waardoor de API intuïtief aanvoelt.

## Stap 5 – Rijen‑, kolom‑ en gegevensvelden configureren (Hoe gegevens toe te voegen → Velden)

We plaatsen *Region* op rijen, *Product* op kolommen en sommeren zowel *Units* als *Revenue*.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**Waarom deze indexen?**  
Aspose.Cells telt kolommen vanaf 0, dus `0` wijst naar *Region*. De `DataFields.Add`‑methode laat je het veld hernoemen (bijv. “Sum of Units”) en een aggregatietype kiezen – `Sum` is het meest gebruikelijk voor numerieke data.

## Stap 6 – Hoe verversing in te schakelen – De draaitabel automatisch laten bijwerken bij openen

Als de brongegevens later veranderen, wil je waarschijnlijk dat de draaitabel die wijzigingen automatisch weergeeft. Daar komt `RefreshDataOnOpen` van pas.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **Opmerking:** Deze vlag werkt alleen wanneer de werkmap in Excel wordt geopend; hij wordt niet opnieuw berekend binnen Aspose.Cells tenzij je handmatig `pivotTable.RefreshData()` aanroept.

## Stap 7 – Werkmap opslaan als XLSX (Hoe werkmap opslaan als XLSX)

Tot slot slaan we het bestand op schijf op. Het `.xlsx`‑formaat is het moderne, zip‑gebaseerde Excel‑bestandstype dat overal werkt.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Het uitvoeren van het programma levert een bestand op genaamd **PivotRefresh.xlsx** in de uitvoermap. Open het in Excel en je ziet een netjes opgemaakte draaitabel met *Region*-rijen, *Product*-kolommen en gesommeerde *Units*‑ en *Revenue*-waarden. Omdat we verversing hebben ingeschakeld, worden eventuele bewerkingen die je maakt in het *SalesData*-blad automatisch bijgewerkt de volgende keer dat je de werkmap opent.

### Verwachte uitvoer

| Regio | Widget | Gadget | … |
|-------|--------|--------|---|
| Oost  | 120    | 0      |   |
| West  | 0      | 85     |   |
| **Totaal** | **120** | **85** |   |

*(Cijfers variëren afhankelijk van de toegevoegde rijen.)*

---

## Veelgestelde vragen & Variaties

### Wat als ik meerdere draaitabellen nodig heb?

Je kunt **Stap 4** herhalen met een andere naam en locatie. Elke aanroep van `PivotTables.Add` geeft een nieuwe index terug die je kunt gebruiken om het tabelobject op te halen.

### Hoe wijzig ik de aggregatie naar *Gemiddelde* in plaats van *Som*?

Vervang `PivotTableDataAggregationType.Sum` door `PivotTableDataAggregationType.Average` in de `DataFields.Add`‑aanroepen.

### Kan ik de draaitabel stijlen (lettertypen, kleuren)?

Ja. Na het maken van de draaitabel kun je de `Style`‑eigenschap benaderen of celopmaak toepassen op het bereik dat de draaitabel bevat. Bijvoorbeeld:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### Is het mogelijk om later meer rijen toe te voegen nadat de werkmap is opgeslagen?

Absoluut. Laad het bestand met `new Workbook("PivotRefresh.xlsx")`, voeg rijen toe aan het *SalesData*-blad en roep `pivotTable.RefreshData()` aan voordat je opnieuw opslaat.

---

## Volledig werkend voorbeeld (Klaar om te kopiëren)

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

Sla het bestand op, voer het uit en open de gegenereerde **PivotRefresh.xlsx** – je hebt zojuist **hoe een draaitabel te maken** in C# onder de knie.

---

## Afronding

We hebben behandeld **hoe je draaitabellen** programmatically maakt, hoe je **gegevens toevoegt**, hoe je **verversing inschakelt**, en uiteindelijk hoe je **werkmap opslaat als xlsx** met Aspose.Cells. De code

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}