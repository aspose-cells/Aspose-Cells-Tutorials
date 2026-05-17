---
category: general
date: 2026-03-21
description: Maak een Excel-werkmap en importeer een datatabel naar Excel terwijl
  je de kolomstijl instelt, exporteer gegevens naar Excel en formatteer de datum van
  Excel-cellen in minuten.
draft: false
keywords:
- create excel workbook
- import datatable to excel
- set column style
- export data to excel
- format excel cells date
language: nl
og_description: Maak snel een Excel-werkmap. Leer hoe je een datatable naar Excel
  importeert, kolomstijlen instelt, gegevens exporteert naar Excel en datums in Excel-cellen
  formatteert, allemaal in één gids.
og_title: Maak een Excel‑werkboek – Volledige tutorial voor opmaak en export
tags:
- C#
- Aspose.Cells
- Excel automation
title: Maak Excel-werkmap met gestylede tabel – Stapsgewijze handleiding
url: /nl/net/excel-workbook/create-excel-workbook-with-styled-table-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-werkmap maken – Complete programmeertutorial

Heb je ooit moeten **create excel workbook** die er direct uit de code professioneel uitziet? Misschien haal je gegevens uit een database en wil je dat de datums in het juiste formaat verschijnen zonder later in Excel te moeten sleutelen. Dat is een veelvoorkomend pijnpunt—vooral wanneer de output in de inbox van een klant belandt en zij verwachten dat alles direct bruikbaar is.

In deze gids lopen we stap voor stap door een enkele, zelfstandige oplossing die **imports datatable to excel**, een **set column style** toepast en uiteindelijk **export data to excel** als een mooi opgemaakt bestand. Je ziet precies hoe je **format excel cells date** kunt toepassen zodat het spreadsheet eruitziet als een professioneel rapport, en je krijgt aan het einde een volledig werkend voorbeeld. Geen ontbrekende onderdelen, geen “zie de docs” shortcuts—gewoon pure code die je vandaag nog in je project kunt gebruiken.

---

## Wat je zult leren

- Hoe je **create excel workbook** gebruikt met de Aspose.Cells bibliotheek (of een andere compatibele API).
- De snelste manier om **import datatable to excel** uit te voeren zonder handmatige cel‑voor‑cel lussen.
- Technieken om **set column style** toe te passen, inclusief het toepassen van een datumformaat op een specifieke kolom.
- Hoe je **export data to excel** doet met één `Save`‑aanroep.
- Veelvoorkomende valkuilen wanneer je probeert **format excel cells date** en hoe je ze kunt vermijden.

### Vereisten

- .NET 6+ (of .NET Framework 4.6+).  
- Aspose.Cells voor .NET geïnstalleerd (`Install-Package Aspose.Cells`).  
- Een `DataTable` klaar om te exporteren—je gegevensbron kan SQL, CSV of iets anders zijn dat omgezet kan worden naar een `DataTable`.

Als je al vertrouwd bent met C# en die onderdelen klaar hebt, kun je direct aan de slag. Anders geeft de “Prerequisites” sectie hierboven je een snelle checklist.

---

## Stap 1 – Maak de Excel-werkmap instantie

Het eerste wat je doet wanneer je **create excel workbook** programmatically wilt maken, is het workbook‑object instantieren. Beschouw dit als het openen van een leeg notitieboek waarin je later je gegevens schrijft.

```csharp
using Aspose.Cells;
using System.Data;

// Step 1: Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();
```

> **Waarom dit belangrijk is:**  
> De `Workbook`‑klasse is het toegangspunt voor elke bewerking in Aspose.Cells. Het vooraf aanmaken geeft je een schoon canvas, en je kunt later een bestaand bestand laden als je gegevens wilt toevoegen in plaats van vanaf nul te beginnen.

---

## Stap 2 – Bereid de DataTable voor om te importeren

Voordat we **import datatable to excel** kunnen uitvoeren, hebben we een `DataTable` nodig. In echte projecten komt deze vaak van `SqlDataAdapter.Fill` of `DataTable.Load`. Voor de duidelijkheid zullen we een methode stubben die een kant‑klaar tabel retourneert.

```csharp
// Step 2: Obtain the data to be written – a DataTable with three columns
DataTable dataTable = GetData();   // assume GetData() returns the required table

// Example implementation (you can replace this with your own data source)
DataTable GetData()
{
    DataTable dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Quantity", typeof(int));

    dt.Rows.Add(DateTime.Today.AddDays(-2), "Apples", 120);
    dt.Rows.Add(DateTime.Today.AddDays(-1), "Bananas", 85);
    dt.Rows.Add(DateTime.Today, "Cherries", 60);
    return dt;
}
```

> **Tip:** Als je datums als strings zijn opgeslagen, converteer ze dan eerst naar `DateTime`—anders werkt de **format excel cells date** stap niet zoals verwacht.

---

## Stap 3 – Definieer stijlen voor elke kolom (Set Column Style)

Nu volgt het deel waar we **set column style** toepassen. We maken een array van `Style`‑objecten—één per kolom. De eerste kolom krijgt een ingebouwd datumformaat (code 14), terwijl de andere de algemene indeling behouden (code 0).

```csharp
// Step 3: Define a style for each column; apply a date format to the first column
Style[] columnStyles = new Style[3];
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = workbook.CreateStyle();
    columnStyles[i].Number = (i == 0) ? 14 : 0;   // 14 = date format, 0 = general
}
```

> **Waarom stijl‑objecten gebruiken?**  
> Een stijl één keer toepassen en hergebruiken is veel efficiënter dan het formaat per cel afzonderlijk instellen. Het garandeert ook dat de hele kolom dezelfde **format excel cells date**‑regel volgt, wat essentieel is voor consistentie wanneer het bestand in verschillende regio‑instellingen wordt geopend.

---

## Stap 4 – Importeer de DataTable met stijlen in het werkblad

Met het workbook klaar en de stijlen gedefinieerd, **import datatable to excel** nu. De `ImportDataTable`‑methode doet het zware werk: hij schrijft de kolomkoppen, rijen en past de stijlen toe die we hebben meegegeven.

```csharp
// Step 4: Access the first worksheet and import the DataTable using the styles
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

> **Wat er onder de motorkap gebeurt:**  
> - `true` vertelt Aspose.Cells om kolomnamen op te nemen als de eerste rij.  
> - `0, 0` zijn de start‑rij‑ en kolom‑indexen (linkerbovenhoek).  
> - `columnStyles` koppelt elke kolom aan de stijl die we hebben voorbereid, waardoor de **format excel cells date**‑regel op de datumkolom wordt toegepast.

---

## Stap 5 – Sla (export) de werkmap op naar een fysiek bestand

Tot slot **export data to excel** door het workbook op te slaan op schijf. Je kunt het pad aanpassen naar elke gewenste map, of het bestand direct streamen naar een HTTP‑response voor een web‑API.

```csharp
// Step 5: Save the workbook with the styled table
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

> **Pro tip:** Gebruik `workbook.Save(Stream, SaveFormat.Xlsx)` wanneer je het bestand via het netwerk wilt verzenden zonder naar schijf te schrijven.

---

## Volledig werkend voorbeeld (Alle stappen gecombineerd)

Hieronder staat het volledige, kant‑klaar programma. Kopieer‑en‑plak het in een console‑app, pas het uitvoerpad aan, en je hebt binnen enkele seconden een mooi opgemaakt Excel‑bestand.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Get the data (replace GetData with your own source if needed)
        DataTable dataTable = GetData();

        // 3️⃣ Prepare column styles – date format for the first column
        Style[] columnStyles = new Style[3];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            columnStyles[i] = workbook.CreateStyle();
            columnStyles[i].Number = (i == 0) ? 14 : 0;   // 14 = date, 0 = general
        }

        // 4️⃣ Import the DataTable with the styles
        Worksheet worksheet = workbook.Worksheets[0];
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 5️⃣ Save the file
        workbook.Save("StyledTable.xlsx");

        Console.WriteLine("Excel workbook created successfully!");
    }

    // Sample data generator – replace with real data source
    static DataTable GetData()
    {
        DataTable dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(DateTime.Today.AddDays(-2), "Apples", 120);
        dt.Rows.Add(DateTime.Today.AddDays(-1), "Bananas", 85);
        dt.Rows.Add(DateTime.Today, "Cherries", 60);
        return dt;
    }
}
```

**Verwachte output:**  
Wanneer je `StyledTable.xlsx` opent, toont kolom A datums zoals `03/19/2026` (afhankelijk van je locale), terwijl kolommen B en C de productnamen en hoeveelheden weergeven als platte tekst/getallen. Geen extra opmaakstappen nodig—je **create excel workbook** proces is voltooid.

---

## Veelgestelde vragen & randgevallen

### 1️⃣ Wat als mijn DataTable meer dan drie kolommen heeft?
Voeg meer `Style`‑objecten toe aan de `columnStyles`‑array, en pas de `Number`‑eigenschap aan voor elke kolom die een speciaal formaat nodig heeft (bijv. valuta, percentages). De `ImportDataTable`‑methode zal elke stijl op positie afstemmen.

### 2️⃣ Kan ik een aangepast datumformaat gebruiken in plaats van de ingebouwde 14?
Zeker. Vervang `columnStyles[i].Number = 14;` door:

```csharp
columnStyles[i].Number = 22;               // built‑in custom format ID
columnStyles[i].Custom = "dd‑MMM‑yyyy";    // or any .NET date pattern you like
```

### 3️⃣ Hoe **export data to excel** ik in een web‑API zonder naar schijf te schrijven?
Gebruik een `MemoryStream`:

```csharp
using (var ms = new MemoryStream())
{
    workbook.Save(ms, SaveFormat.Xlsx);
    ms.Position = 0;
    // return File(ms.ToArray(), "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "Report.xlsx");
}
```

### 4️⃣ Wat als de locale van de gebruiker een andere datum‑scheidingsteken verwacht?
Het ingebouwde datumformaat (ID 14) houdt rekening met de locale‑instellingen van het workbook. Als je een vast formaat nodig hebt ongeacht de locale, gebruik dan de `Custom`‑eigenschap zoals hierboven getoond.

### 5️⃣ Werkt dit met .NET Core?
Ja—Aspose.Cells ondersteunt .NET Standard 2.0 en hoger, dus dezelfde code draait op .NET 6, .NET 7, of elke compatibele runtime.

---

## Best‑practice tips (Pro tips)

- **Stijlen hergebruiken**: Een stijl per kolom aanmaken is goedkoop, maar hetzelfde stijl‑object hergebruiken voor identieke kolommen bespaart geheugen.
- **Vermijd cel‑voor‑cel lussen**: `ImportDataTable` is sterk geoptimaliseerd; handmatige lussen zijn trager en vatbaar voor fouten.
- **Stel workbook‑culture vroeg in** als je consistente getal‑/datum‑scheidingstekens nodig hebt over omgevingen heen:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

- **Valideer DataTable** vóór import—null‑datums veroorzaken een uitzondering wanneer de datumstijl wordt toegepast.
- **Schakel berekening in** als je formules toevoegt na import:

```csharp
workbook.CalculateFormula();
```

---

## Conclusie

Je hebt nu een complete, end‑to‑end recept om **create excel workbook**, **import datatable to excel**, **set column style**, **export data to excel**, en **format excel cells date** uit te voeren—alles in minder dan een dozijn C#‑regels. De aanpak is snel, betrouwbaar, en houdt opmaak‑zaken binnen de code, zodat het uiteindelijke spreadsheet klaar is voor zakelijke gebruikers op het moment dat ze het openen.

Klaar voor de volgende uitdaging? Probeer conditionele opmaak toe te voegen, grafieken in te voegen, of het te converteren naar

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}