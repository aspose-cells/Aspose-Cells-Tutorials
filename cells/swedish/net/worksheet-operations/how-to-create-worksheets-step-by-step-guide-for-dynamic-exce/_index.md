---
category: general
date: 2026-03-21
description: Lär dig hur du skapar kalkylblad, genererar Excel-filer med dynamiska
  kalkylbladsnamn och sparar arbetsboken som XLSX med Aspose.Cells i C#.
draft: false
keywords:
- how to create worksheets
- save workbook as xlsx
- generate excel sheets
- dynamic worksheet names
- process master sheet
language: sv
og_description: Hur man skapar kalkylblad i Excel med Aspose.Cells, genererar Excel-ark
  med dynamiska kalkylbladsnamn och sparar arbetsboken som XLSX.
og_title: Hur man skapar kalkylblad – Komplett C#-handledning
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur man skapar kalkylblad – Steg‑för‑steg guide för dynamisk Excel‑generering
url: /sv/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar arbetsblad – Komplett C#-handledning

Har du någonsin undrat **hur man skapar arbetsblad** i farten utan att manuellt öppna Excel varje gång? Du är inte ensam. Många utvecklare stöter på problem när de behöver **generera Excel‑blad** från datakällor och vill att varje blad ska ha ett meningsfullt, dynamiskt namn. Den goda nyheten? Med Aspose.Cells kan du automatisera hela processen, **process master sheet**, och slutligen **save workbook as XLSX** på bara några kodrader.

I den här handledningen går vi igenom ett verkligt scenario: vi börjar med en tom arbetsbok, infogar en smart‑marker‑token som talar om för Aspose vilka detaljblad som ska skapas, konfigurerar ett namnmönster så att varje blad får ett unikt namn, och slutligen sparar resultatet på disk. I slutet har du ett färdigt C#‑program som skapar arbetsblad, genererar Excel‑blad med dynamiska arbetsbladsnamn, och sparar arbetsboken som XLSX — utan att röra UI‑en.

> **Förutsättningar**  
> • .NET 6+ (or .NET Framework 4.6+).  
> • Aspose.Cells for .NET (the free trial works for this demo).  
> • Basic C# knowledge—no deep Excel interop tricks required.

---

## Översikt över vad vi kommer att bygga

- **Master sheet** som innehåller en smart‑marker‑platshållare (`«DetailSheetNewName:Dept»`).  
- **SmartMarkerProcessor** som läser en datakälla (t.ex. en `DataTable`) och skapar ett nytt arbetsblad för varje avdelning.  
- **Dynamic worksheet names** enligt mönstret `Dept_{0}` där `{0}` ersätts med avdelningsnamnet.  
- **Final XLSX file** sparas i en mapp du anger.

Det är allt. Enkelt, men ändå kraftfullt nog för fakturor, rapporter eller någon flik‑baserad Excel‑utmatning.

![Diagram som visar hur ett master sheet bearbetas för att generera flera dynamiska arbetsblad](/images/how-to-create-worksheets-diagram.png "Diagram för att skapa arbetsblad")

*Alt text: illustration av hur man skapar arbetsblad med dynamiska arbetsbladsnamn med Aspose.Cells.*

## Steg 1: Ställ in projektet och lägg till Aspose.Cells

### Varför detta är viktigt

Innan någon kod körs måste kompilatorn veta var klasserna `Workbook`, `Worksheet` och `SmartMarkerProcessor` finns. Att lägga till NuGet‑paketet säkerställer att du har den senaste, fullt utrustade API:n.

```csharp
// Install via CLI
// dotnet add package Aspose.Cells

using Aspose.Cells;
using System.Data;
```

> **Pro tip:** Om du använder Visual Studio, högerklicka på projektet → *Manage NuGet Packages* → sök efter *Aspose.Cells* och installera den senaste stabila versionen.

---

## Steg 2: Skapa en ny arbetsbok och master‑bladet

### Vad vi gör

Vi börjar med en tom arbetsbok och hämtar sedan det första arbetsbladet (index 0). Detta blad kommer att fungera som **master sheet** som innehåller smart‑marker‑tokenen.

```csharp
// Step 1: Create a new workbook and get the first worksheet (master sheet)
Workbook workbook = new Workbook();
Worksheet masterSheet = workbook.Worksheets[0];

// Optional: give the master sheet a friendly name
masterSheet.Name = "Master";
```

`Workbook`‑klassen är behållaren för alla arbetsblad. Som standard skapas ett blad som heter *Sheet1*; att byta namn till “Master” gör den slutliga filen enklare att navigera.

---

## Steg 3: Infoga en Smart‑Marker‑token för detaljbladens namn

### Varför använda en smart‑marker?

Smart markers låter Aspose.Cells ersätta platshållare med data vid körning. Token `«DetailSheetNewName:Dept»` talar om för processorn: *“När du ser detta, skapa ett nytt detaljblad för varje rad i `Dept`‑kolumnen.”*

```csharp
// Step 2: Place a smart‑marker token that will be replaced with detail sheet names
masterSheet.Cells["A1"].PutValue("«DetailSheetNewName:Dept»");
```

Du kan placera token var som helst; vi valde **A1** för tydlighet. När processorn körs kommer den att ersätta token med det faktiska avdelningsnamnet och generera ett motsvarande arbetsblad.

---

## Steg 4: Förbered datakällan

### Hur data styr skapandet av blad

Aspose.Cells fungerar med vilken `IEnumerable`‑datakälla som helst. För den här demonstrationen använder vi en `DataTable` med en enda kolumn som heter `Dept`.

```csharp
// Sample data source: list of departments
DataTable dataSource = new DataTable();
dataSource.Columns.Add("Dept", typeof(string));

// Populate with example rows
dataSource.Rows.Add("Finance");
dataSource.Rows.Add("HR");
dataSource.Rows.Add("IT");
dataSource.Rows.Add("Marketing");
```

> **Vad händer om du har fler kolumner?**  
> Processorn kommer att ignorera extra kolumner om du inte refererar till dem i ytterligare smart markers. Detta håller bladgenereringen lättviktig.

---

## Steg 5: Konfigurera SmartMarkerProcessor och namnmönstret

### Dynamiska arbetsbladsnamn i praktiken

Vi vill att varje nytt blad ska heta `Dept_Finance`, `Dept_HR` osv. `DetailSheetNewName`‑alternativet låter oss definiera ett mönster där `{0}` ersätts med det faktiska avdelningsnamnet.

```csharp
// Step 3: Initialise the SmartMarker processor and set the naming pattern for generated sheets
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.Options.DetailSheetNewName = "Dept_{0}";   // Aspose adds an index if needed
```

Om en avdelning förekommer två gånger kommer Aspose automatiskt att lägga till ett numeriskt suffix (t.ex. `Dept_Finance_1`) för att undvika duplicerade bladnamn.

---

## Steg 6: Bearbeta master‑bladet för att generera detaljblad

### Kärnan i **process master sheet**

Att anropa `Process` gör det tunga arbetet: den skannar master‑bladet efter smart markers, skapar nya arbetsblad, kopierar master‑layouten och fyller varje med radens data.

```csharp
// Step 4: Process the master sheet using the data source to create detail sheets
processor.Process(masterSheet, dataSource);
```

Efter detta anrop innehåller arbetsboken ett master‑blad plus fyra detaljblad — varje namn enligt vårt mönster och fyllt med avdelningsnamnet i cell A1.

---

## Steg 7: Spara arbetsboken som XLSX

### Sista steget—**save workbook as XLSX**

Nu när arbetsbladen finns skriver vi filen till disk. Du kan välja vilken sökväg som helst; se bara till att katalogen finns.

```csharp
// Step 5: Save the resulting workbook to a file
string outputPath = @"C:\Temp\DetailSheets.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Att öppna `DetailSheets.xlsx` visar:

| Bladnamn | Cell A1 (Innehåll) |
|----------|--------------------|
| Master   | «DetailSheetNewName:Dept» (unchanged) |
| Dept_Finance | Finance |
| Dept_HR      | HR |
| Dept_IT      | IT |
| Dept_Marketing | Marketing |

> **Edge case:** Om mål‑mappen inte finns, kastar `Save` ett `DirectoryNotFoundException`. Omge anropet med en try‑catch‑block eller skapa mappen i förväg.

---

## Fullt fungerande exempel

När vi sätter ihop allt, här är det kompletta programmet som du kan kopiera‑klistra in i en konsolapp:

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelDynamicSheetsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and master sheet
            Workbook workbook = new Workbook();
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Master";

            // 2️⃣ Insert smart‑marker token
            masterSheet.Cells["A1"].PutValue("«DetailSheetNewName:Dept»");

            // 3️⃣ Build data source (departments)
            DataTable dataSource = new DataTable();
            dataSource.Columns.Add("Dept", typeof(string));
            dataSource.Rows.Add("Finance");
            dataSource.Rows.Add("HR");
            dataSource.Rows.Add("IT");
            dataSource.Rows.Add("Marketing");

            // 4️⃣ Configure processor with dynamic naming
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Options.DetailSheetNewName = "Dept_{0}";

            // 5️⃣ Process master sheet → generate detail sheets
            processor.Process(masterSheet, dataSource);

            // 6️⃣ Save as XLSX
            string outputPath = @"C:\Temp\DetailSheets.xlsx";
            try
            {
                workbook.Save(outputPath, SaveFormat.Xlsx);
                Console.WriteLine($"✅ Workbook saved to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ Failed to save workbook: {ex.Message}");
            }
        }
    }
}
```

Kör programmet, öppna den resulterande filen, och du kommer att se exakt den layout som beskrevs tidigare. Ingen manuell kopiering, ingen COM‑interop — bara ren C#‑kod som **genererar Excel‑blad** med **dynamic worksheet names**.

---

## Vanliga frågor & fallgropar

| Fråga | Svar |
|-------|------|
| *Kan jag använda ett DataSet med flera tabeller?* | Ja. Skicka den lämpliga tabellen till `Process` eller använd en ordbok med tabeller. |
| *Vad händer om jag behöver mer än en smart‑marker på master‑bladet?* | Placera ytterligare token som `«DetailSheetNewName:Region»` och konfigurera ett separat namnmönster om det behövs. |
| *Behålls master‑bladet i den slutliga filen?* | Som standard, ja. Om du inte behöver det, anropa `workbook.Worksheets.RemoveAt(0)` efter bearbetning. |
| *Hur hanterar Aspose mycket stora datamängder?* | Den strömmar data effektivt, men du kan vilja öka `MemorySetting` om du når minnesgränser. |
| *Kan jag exportera till CSV istället för XLSX?* | Absolut — använd `workbook.Save("file.csv", SaveFormat.Csv)`. Samma logik för bladskapande gäller. |

---

## Nästa steg

Nu när du vet **hur man skapar arbetsblad** dynamiskt, kan du utforska:

- **Saving workbook as XLSX** med lösenordsskydd (`workbook.Protect("pwd")`).  
- **Generating Excel sheets** från JSON‑ eller XML‑källor med `JsonDataSource` eller `XmlDataSource`.  
- **Applying styles** till varje genererat blad (typsnitt, färger) via `Style`‑objekt.  
- **Merging cells** eller infoga formler automatiskt för sammanfattningsrapporter.

Var och en av dessa tillägg bygger på samma **process master sheet**‑koncept, så du kommer att finna övergången smärtfri.

---

## Slutsats

Vi har gått igenom hela kedjan: från att initiera en arbetsbok, infoga en smart‑marker, konfigurera **dynamic worksheet names**, bearbeta master‑bladet för att **generate Excel sheets**, och slutligen **save workbook as XLSX**. Exemplet är komplett, körbart och visar bästa praxis för både prestanda och underhållbarhet.  

Prova det, justera namnmönstret, mata in verkliga affärsdata, och se din Excel‑automation lyfta. Om du stöter på problem, lämna en kommentar nedan — glad kodning!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}