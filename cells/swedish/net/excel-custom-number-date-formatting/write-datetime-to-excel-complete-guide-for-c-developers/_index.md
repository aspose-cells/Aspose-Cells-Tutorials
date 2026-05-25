---
category: general
date: 2026-04-07
description: Skriv datum och tid till Excel med C#. Lär dig hur du infogar datum i
  ett kalkylblad, hanterar Excel-cells datumvärde och konverterar japanska kalenderdatum
  på bara några steg.
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: sv
og_description: Skriv datum och tid till Excel snabbt. Den här guiden visar hur du
  infogar datum i ett kalkylblad, hanterar Excel-cells datumvärde och konverterar
  japanskt kalenderdatum med C#.
og_title: Skriv datum och tid till Excel – Steg‑för‑steg C#-handledning
tags:
- C#
- Excel automation
- Aspose.Cells
title: Skriv datum och tid till Excel – Komplett guide för C#‑utvecklare
url: /sv/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skriv datum/tid till Excel – Komplett guide för C#‑utvecklare

Har du någonsin behövt **skriva datum/tid till Excel** men varit osäker på vilken API‑anrop som faktiskt lagrar ett riktigt Excel‑datum? Du är inte ensam. I många företagsverktyg måste vi släppa in ett C# `DateTime` i ett kalkylblad, och resultatet ska fungera som ett riktigt Excel‑datum—sorterbart, filtrerbart och redo för pivottabeller.  

I den här handledningen går vi igenom exakt hur du *infogar datum i ett kalkylblad* med Aspose.Cells, förklarar varför kulturinställningen är viktig, och visar även hur du **konverterar japanskt kalenderdatum** till ett vanligt `DateTime` innan du skriver det. När du är klar har du ett självständigt kodexempel som du kan kopiera och klistra in i vilket .NET‑projekt som helst.

## Vad du behöver

- **.NET 6+** (eller någon annan aktuell .NET‑version; koden fungerar även på .NET Framework)  
- **Aspose.Cells for .NET** – ett NuGet‑paket som låter dig manipulera Excel‑filer utan att Office är installerat.  
- Grundläggande kunskap om C# `DateTime` och kulturer.  

Inga extra bibliotek, ingen COM‑interop och ingen Excel‑installation krävs. Om du redan har en kalkylbladsinstans (`ws`) är du redo att köra.

## Steg 1: Ställ in japansk kultur (konvertera japanskt kalenderdatum)

När du får ett datum som `"R02/05/01"` (Reiwa 2, 1 maj) måste du tala om för .NET hur era‑symbolerna ska tolkas. Den japanska kalendern är inte standard‑Gregoriansk kalender, så vi skapar en `CultureInfo` som byter dess kalender till `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**Varför detta är viktigt:**  
Om du parsar strängen med standardkulturen kastar .NET ett format‑exception eftersom den inte kan matcha `R` (Reiwa‑eran) till ett år. Genom att byta till `JapaneseCalendar` förstår parsern era‑symbolerna och översätter dem till rätt Gregorianskt år.

## Steg 2: Parsa den era‑baserade strängen till ett `DateTime`

Nu när kulturen är klar kan vi säkert anropa `DateTime.ParseExact`. Formatsträngen `"ggyy/MM/dd"` talar om för parsern:

- `gg` – era‑designator (t.ex. `R` för Reiwa)  
- `yy` – tvåsiffrigt år inom eran  
- `MM/dd` – månad och dag.

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**Proffstips:** Om du kan få datum i andra format (t.ex. `"Heisei 30/12/31"`), omslut parsningen med en `try/catch` och falla tillbaka på `DateTime.TryParseExact`. Det förhindrar att hela importjobbet kraschar på en enda felaktig rad.

## Steg 3: Skriv `DateTime` till en Excel‑cell (Excel‑cellens datumvärde)

Aspose.Cells behandlar ett .NET `DateTime` som ett inbyggt Excel‑datum när du använder `PutValue`. Biblioteket konverterar automatiskt ticken till Excels serienummer (antalet dagar sedan 1900‑01‑00). Detta innebär att cellen visar ett riktigt **excel‑cellens datumvärde** och du kan formatera den senare med Excels inbyggda datumstilar.

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**Vad du ser i Excel:**  
Cell C1 innehåller nu serienumret `44796`, vilket Excel visar som `2020‑05‑01` (eller vilket format du har använt). Det underliggande värdet är ett riktigt datum, inte en sträng, så sortering fungerar som förväntat.

## Steg 4: Spara arbetsboken (avslut)

Om du ännu inte har sparat arbetsboken, gör det nu. Detta steg handlar inte strikt om att skriva datum/tid, men det fullbordar arbetsflödet.

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

Det var allt—fyra koncisa steg, och du har framgångsrikt **skrivit datum/tid till Excel**, samtidigt som du hanterat ett japanskt era‑datum.

---

![write datetime to excel example](/images/write-datetime-to-excel.png "Screenshot showing a C# project writing a DateTime into Excel cell C1")

*Bilden ovan illustrerar den färdiga Excel‑filen med datumet korrekt visat i cell C1.*

## Vanliga frågor & kantfall

### Vad händer om variabeln för kalkylbladet ännu inte är klar?

Du kan skapa en ny arbetsbok i farten:

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### Hur bevarar jag den ursprungliga japanska era‑strängen i bladet?

Om du behöver både den ursprungliga strängen och det parsade datumet, skriv dem till intilliggande celler:

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### Fungerar detta med äldre .NET‑versioner?

Ja. `JapaneseCalendar` finns sedan .NET 2.0, och Aspose.Cells stödjer .NET Framework 4.5+. Se bara till att referera rätt assembly.

### Vad händer med tidszoner?

`DateTime.ParseExact` returnerar en **Kind** av `Unspecified`. Om dina källdatum är i UTC, konvertera dem först:

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### Kan jag ange ett eget datumformat (t.ex. “yyyy年MM月dd日”)?

Absolut. Använd egenskapen `Style.Custom`:

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

Nu visar Excel `2020年05月01日` samtidigt som det lagrar ett riktigt datumvärde.

## Sammanfattning

Vi har gått igenom allt du behöver för att **skriva datum/tid till Excel** från C#:

1. **Konfigurera** en japansk kultur med `JapaneseCalendar` för att **konvertera japanskt kalenderdatum**.  
2. **Parsa** den era‑baserade strängen med `DateTime.ParseExact`.  
3. **Infoga** det resulterande `DateTime` i en cell, vilket ger ett korrekt **excel‑cellens datumvärde**.  
4. **Spara** arbetsboken så att data sparas.

Med dessa fyra steg kan du säkert **infoga datum i kalkylblad** oavsett källformat. Koden är fullt körbar, kräver bara Aspose.Cells och fungerar på alla moderna .NET‑miljöer.

## Vad blir nästa?

- **Massimport:** Loop över rader i en CSV, parsa varje japanskt datum och skriv dem till på varandra följande celler.  
- **Styling:** Applicera villkorlig formatering för att markera förfallna datum.  
- **Prestanda:** Använd `WorkbookDesigner` eller cache‑ade `CellStyle` när du hanterar tusentals rader.  

Känn dig fri att experimentera—byt ut den japanska eran mot den gregorianska kalendern, ändra mål‑cellen eller exportera till ett annat filformat (CSV, ODS). Grundidén är densamma: parsa, konvertera och **skriva datum/tid till Excel** med självförtroende.

Lycka till med kodandet, och må dina kalkylblad alltid sorteras korrekt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}