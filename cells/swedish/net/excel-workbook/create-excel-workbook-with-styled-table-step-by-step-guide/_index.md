---
category: general
date: 2026-03-21
description: Skapa en Excel‑arbetsbok och importera en datatabell till Excel samtidigt
  som du ställer in kolumnstil, exporterar data till Excel och formaterar Excel‑celler
  med datum i minuter.
draft: false
keywords:
- create excel workbook
- import datatable to excel
- set column style
- export data to excel
- format excel cells date
language: sv
og_description: Skapa Excel-arbetsbok snabbt. Lär dig att importera datatabell till
  Excel, sätta kolumnstil, exportera data till Excel och formatera datum i Excel-celler
  i en guide.
og_title: Skapa Excel-arbetsbok – Fullständig handledning för formatering och export
tags:
- C#
- Aspose.Cells
- Excel automation
title: Skapa Excel‑arbetsbok med formaterad tabell – Steg‑för‑steg‑guide
url: /sv/net/excel-workbook/create-excel-workbook-with-styled-table-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel‑arbetsbok – Komplett programmeringshandledning

Har du någonsin behövt **skapa excel workbook** som ser professionell ut direkt från koden? Kanske hämtar du data från en databas och vill att datumen ska visas i rätt format utan att behöva justera i Excel senare. Det är ett vanligt smärtpunkts‑scenario—särskilt när resultatet hamnar i en kunds inkorg och de förväntar sig att allt är färdigt att använda.

I den här guiden går vi igenom en enda, självständig lösning som **imports datatable to excel**, applicerar en **set column style**, och slutligen **export data to excel** som en snyggt formaterad fil. Du får se exakt hur du **format excel cells date** så att kalkylbladet läses som en professionell rapport, och du får ett komplett, körbart exempel i slutet. Inga saknade delar, inga “se dokumentationen”-genvägar—bara ren kod du kan klistra in i ditt projekt idag.

---

## Vad du kommer att lära dig

- Hur du **create excel workbook** med Aspose.Cells‑biblioteket (eller någon kompatibel API).
- Det snabbaste sättet att **import datatable to excel** utan manuella cell‑för‑cell‑loopar.
- Tekniker för att **set column style**, inklusive att applicera ett datumformat på en specifik kolumn.
- Hur du **export data to excel** med ett enda `Save`‑anrop.
- Vanliga fallgropar när du försöker **format excel cells date** och hur du undviker dem.

### Förutsättningar

- .NET 6+ (eller .NET Framework 4.6+).  
- Aspose.Cells för .NET installerat (`Install-Package Aspose.Cells`).  
- En `DataTable` redo att exporteras—din datakälla kan vara SQL, CSV eller vad som helst som kan omvandlas till en `DataTable`.

Om du redan är bekväm med C# och har dessa delar på plats, är du redo att köra. Annars ger avsnittet “Förutsättningar” ovan en snabb checklista.

---

## Steg 1 – Skapa Excel‑arbetsbok‑instansen

Det allra första du gör när du vill **create excel workbook** programatiskt är att instansiera arbetsboks‑objektet. Tänk på det som att öppna en tom anteckningsbok där du senare kommer att skriva in din data.

```csharp
using Aspose.Cells;
using System.Data;

// Step 1: Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();
```

> **Varför detta är viktigt:**  
> `Workbook`‑klassen är ingångspunkten för varje operation i Aspose.Cells. Att skapa den i förväg ger dig en ren canvas, och du kan senare ladda en befintlig fil om du behöver lägga till data istället för att börja från början.

---

## Steg 2 – Förbered DataTable för import

Innan vi kan **import datatable to excel** behöver vi en `DataTable`. I riktiga projekt kommer den ofta från `SqlDataAdapter.Fill` eller `DataTable.Load`. För tydlighetens skull stubbar vi en metod som returnerar en färdig tabell.

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

> **Tips:** Om dina datum lagras som strängar, konvertera dem till `DateTime` först—annars kommer steget **format excel cells date** inte att fungera som förväntat.

---

## Steg 3 – Definiera stilar för varje kolumn (Set Column Style)

Nu kommer delen där vi **set column style**. Vi skapar en array av `Style`‑objekt—ett per kolumn. Den första kolumnen får ett inbyggt datumformat (kod 14), medan de andra behåller det generella formatet (kod 0).

```csharp
// Step 3: Define a style for each column; apply a date format to the first column
Style[] columnStyles = new Style[3];
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = workbook.CreateStyle();
    columnStyles[i].Number = (i == 0) ? 14 : 0;   // 14 = date format, 0 = general
}
```

> **Varför använda stil‑objekt?**  
> Att applicera en stil en gång och återanvända den är mycket effektivare än att sätta formatet på varje cell individuellt. Det garanterar också att hela kolumnen följer samma **format excel cells date**‑regel, vilket är avgörande för konsistens när filen öppnas i olika språk‑ och regionsinställningar.

---

## Steg 4 – Importera DataTable med stilar till kalkylbladet

Med arbetsboken klar och stilarna definierade **import datatable to excel** nu. Metoden `ImportDataTable` gör det tunga lyftet: den skriver kolumnrubriker, rader och applicerar de stilar vi skickat med.

```csharp
// Step 4: Access the first worksheet and import the DataTable using the styles
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

> **Vad händer under huven?**  
> - `true` talar om för Aspose.Cells att inkludera kolumnnamn som den första raden.  
> - `0, 0` är start‑rad‑ och kolumnindex (övre‑vänstra hörnet).  
> - `columnStyles` matchar varje kolumn med den stil vi förberett, så att **format excel cells date**‑regeln appliceras på datumkolumnen.

---

## Steg 5 – Spara (exportera) arbetsboken till en fysisk fil

Till sist **export data to excel** genom att spara arbetsboken till disk. Du kan ändra sökvägen till vilken mapp du vill, eller till och med streama filen direkt till ett HTTP‑svar för ett web‑API.

```csharp
// Step 5: Save the workbook with the styled table
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

> **Pro‑tips:** Använd `workbook.Save(Stream, SaveFormat.Xlsx)` när du behöver skicka filen över nätverket utan att skriva till disk.

---

## Fullt fungerande exempel (alla steg kombinerade)

Nedan är det kompletta, körklara programmet. Kopiera‑klistra in det i en konsolapp, justera utsökvägen, så har du ett snyggt formaterat Excel‑dokument på några sekunder.

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

**Förväntad output:**  
När du öppnar `StyledTable.xlsx` visar kolumn A datum som `03/19/2026` (beroende på din lokala inställning), medan kolumn B och C visar produktnamn respektive kvantiteter som vanlig text/nummer. Inga extra formateringssteg behövs—din **create excel workbook**‑process är klar.

---

## Vanliga frågor & edge‑cases

### 1️⃣ Vad händer om min DataTable har fler än tre kolumner?
Lägg till fler `Style`‑objekt i `columnStyles`‑arrayen och justera `Number`‑egenskapen för varje kolumn som behöver ett speciellt format (t.ex. valuta, procent). `ImportDataTable`‑metoden matchar varje stil efter position.

### 2️⃣ Kan jag använda ett eget datumformat istället för den inbyggda 14?
Absolut. Ersätt `columnStyles[i].Number = 14;` med:

```csharp
columnStyles[i].Number = 22;               // built‑in custom format ID
columnStyles[i].Custom = "dd‑MMM‑yyyy";    // or any .NET date pattern you like
```

### 3️⃣ Hur **export data to excel** i ett web‑API utan att skriva till disk?
Använd en `MemoryStream`:

```csharp
using (var ms = new MemoryStream())
{
    workbook.Save(ms, SaveFormat.Xlsx);
    ms.Position = 0;
    // return File(ms.ToArray(), "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "Report.xlsx");
}
```

### 4️⃣ Vad om användarens locale förväntar ett annat datumseparator?
Det inbyggda datumformatet (ID 14) respekterar arbetsbokens språk‑/regioninställningar. Om du behöver ett fast format oavsett locale, använd `Custom`‑egenskapen som visas ovan.

### 5️⃣ Fungerar detta med .NET Core?
Ja—Aspose.Cells stödjer .NET Standard 2.0 och senare, så samma kod körs på .NET 6, .NET 7 eller någon annan kompatibel runtime.

---

## Bästa praxis‑tips (Pro‑tips)

- **Återanvänd stilar**: Att skapa en stil per kolumn är billigt, men att återanvända samma stilobjekt för identiska kolumner sparar minne.
- **Undvik cell‑för‑cell‑loopar**: `ImportDataTable` är starkt optimerad; manuella loopar är långsammare och mer felbenägna.
- **Sätt arbetsbokskultur tidigt** om du behöver enhetliga tal‑/datumsseparatorer över miljöer:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

- **Validera DataTable** innan import—null‑datum kastar ett undantag när datumstilen appliceras.
- **Aktivera beräkning** om du lägger till formler efter import:

```csharp
workbook.CalculateFormula();
```

---

## Slutsats

Du har nu ett komplett, end‑to‑end‑recept för att **create excel workbook**, **import datatable to excel**, **set column style**, **export data to excel** och **format excel cells date**—allt på under ett dussin rader C#‑kod. Metoden är snabb, pålitlig och håller formateringsaspekterna i koden, så att det färdiga kalkylbladet är redo för affärsanvändare så snart de öppnar det.

Redo för nästa utmaning? Prova att lägga till villkorsstyrd formatering, infoga diagram, eller konvertera 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}