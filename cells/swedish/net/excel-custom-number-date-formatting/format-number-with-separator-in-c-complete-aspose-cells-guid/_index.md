---
category: general
date: 2026-03-30
description: Lär dig hur du formaterar tal med avgränsare med Aspose.Cells i C#. Inkluderar
  att sätta anpassat talformat, lägga till tusentalsavgränsare, formatera decimaler
  och hur du formaterar en cell.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: sv
og_description: Formatera tal med separator i C#. Denna guide visar hur du ställer
  in ett anpassat talformat, lägger till tusentalsseparator, formaterar decimalplatser
  och hur du formaterar en cell med Aspose.Cells.
og_title: Formatera tal med avgränsare i C# – Aspose.Cells-handledning
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Formatera tal med avgränsare i C# – Komplett Aspose.Cells-guide
url: /sv/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formatera tal med avgränsare i C# – Komplett Aspose.Cells-guide

Har du någonsin behövt **formatera tal med avgränsare** i ett kalkylblad men varit osäker på vilken API‑anrop du ska använda? Du är inte ensam—utvecklare kämpar ständigt med tusentalsavgränsare, decimaler och anpassade mönster när de exporterar data.  

God nyhet: Aspose.Cells gör det enkelt. I den här handledningen går vi igenom ett verkligt exempel som **sätter ett anpassat talformat**, **lägger till en tusentalsavgränsare**, **formaterar decimaler**, och visar **hur man formaterar cell**‑utdata som en sträng. I slutet har du ett färdigt kodexempel som du kan klistra in i vilket .NET‑projekt som helst.

## Vad den här guiden täcker

* Den exakta NuGet‑paketet du behöver och hur du installerar det.  
* Steg‑för‑steg‑kod som skapar en arbetsbok, skriver ett numeriskt värde och tillämpar ett anpassat format.  
* Varför `ExportTableOptions.ExportAsString` är det föredragna sättet att hämta ett formaterat värde.  
* Vanliga fallgropar—som att glömma att aktivera `ExportAsString` eller använda fel formatmask.  
* Hur du justerar formatmasken om du behöver ett annat antal decimaler eller en annan avgränsningstyp.

Ingen extern dokumentationslänkar behövs; allt du behöver finns här. Låt oss dyka in.

---

## Förutsättningar

| Krav | Orsak |
|-------------|--------|
| .NET 6.0 eller senare | Aspose.Cells 23.10+ riktar sig mot .NET Standard 2.0+, så .NET 6 är säkert och aktuellt. |
| Visual Studio 2022 (eller någon C#‑IDE) | Gör felsökning och paketshantering smidig. |
| Aspose.Cells för .NET NuGet‑paket | Tillhandahåller klasserna `Workbook`, `Worksheet` och `ExportTableOptions` som vi kommer att använda. |

Du kan installera paketet via Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

Det är allt—inga extra DLL‑filer, ingen COM‑interop, bara en enda NuGet‑referens.

## Steg 1: Initiera en ny arbetsbok (Hur man formaterar cell)

Det första vi gör är att skapa en ny `Workbook`‑instans. Tänk på den som en tom Excel‑fil som är redo att ta emot data.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Varför detta är viktigt:** `Workbook` är ingångspunkten för varje operation i Aspose.Cells. Genom att hämta det första kalkylbladet (`Worksheets[0]`) får vi en ren canvas utan att behöva namnge ett blad.

## Steg 2: Skriv ett numeriskt värde i mål‑cellen

Därefter placerar vi ett rått tal i cell **A1**. Värdet är ännu inte formaterat—det är bara en double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Proffstips:** Använd `PutValue` istället för `PutString` när du avser att applicera numerisk formatering senare. Detta bevarar den underliggande datatypen, vilket möjliggör Excel‑kompatibla beräkningar.

## Steg 3: Sätt anpassat talformat (Lägg till tusentalsavgränsare & formatera decimaler)

Nu kommer hjärtat i handledningen: definiera en formatmask som talar om för Aspose.Cells hur talet ska visas. Masken `#,##0.00` gör tre saker:

1. **`#,##0`** – lägger till en tusentalsavgränsare (komma som standard).  
2. **`.00`** – tvingar exakt två decimaler.  

Om du behöver ett annat antal decimaler, ändra bara antalet `0` efter decimaltecknet.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Varför vi använder `ExportAsString`**: Som standard returnerar `ExportString` det råa värdet. Genom att sätta `ExportAsString = true` tvingas API‑et att tillämpa `NumberFormat`‑masken innan konvertering till text. Detta är avgörande när du behöver den exakta strängrepresentationen för rapporter, JSON‑payloads eller UI‑visning.

## Steg 4: Exportera den formaterade texten (Hur man formaterar cell)

Med alternativen klara anropar vi `ExportString` på samma cell. Metoden respekterar masken vi just definierade och returnerar en snyggt formaterad sträng.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

När programmet körs skrivs **`12,345.68`** till konsolen—exakt det format vi begärde.

> **Edge case:** Om källtalet har mer än två decimaler, avrundar masken det. Om du behöver trunkering istället för avrundning måste du förbehandla värdet med `Math.Truncate` innan du anropar `PutValue`.

## Steg 5: Justera formatet – Vanliga variationer

### 5.1 Ändra decimalprecision

Vill du ha tre decimaler? Byt bara ut masken:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Använd en annan tusentalsavgränsare

Vissa regioner föredrar ett mellanslag eller en punkt. Du kan bädda in tecknet direkt:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Eller förlita dig på arbetsbokens kulturinställningar:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Prefix eller suffix (Valuta, Procent)

Lägg till ett dollartecken eller ett procenttecken direkt i masken:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Obs:** Masken är skiftlägeskänslig. `$` och `%` är bokstavliga symboler; de påverkar inte det underliggande numeriska värdet.

## Steg 6: Fullt fungerande exempel (Kopiera‑klistra redo)

Nedan är det kompletta programmet som du kan kopiera in i en ny konsolapp. Det innehåller alla steg, kommentarer och den slutgiltiga utdata‑verifieringen.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Kör programmet (`dotnet run` från terminalen eller tryck F5 i Visual Studio) så ser du det formaterade talet skrivet exakt som visas.

## Vanliga frågor (FAQ)

**Q: Fungerar detta med äldre versioner av Excel?**  
A: Ja. Formatmasken följer Excels inbyggda talformat‑syntax, så varje version som förstår `#,##0.00` kommer att rendera samma sträng.

**Q: Vad händer om jag behöver formatera ett område av celler?**  
A: Loopa över det önskade området och tillämpa samma `ExportTableOptions` på varje cell, eller sätt `Style.Custom`‑egenskapen på området och anropa sedan `ExportString` på en enda cell.

**Q: Kan jag exportera direkt till CSV med dessa format tillämpade?**  
A: Absolut. Använd `Workbook.Save("output.csv", SaveFormat.CSV);` efter att du har satt formatet på varje cell. Aspose.Cells respekterar cellens `Style` när CSV genereras.

## Slutsats

Vi har just visat hur man **formaterar tal med avgränsare** i C# med Aspose.Cells, och täckt allt från **sätta anpassat talformat** till **lägga till tusentalsavgränsare**, **formatera decimaler**, och den väsentliga **hur man formaterar cell** för strängexport. Koden är helt självständig, fungerar med .NET 6+ och kan anpassas för vilken region eller precision som helst.

Nästa steg du kan utforska:

* Applicera samma teknik på datum och tider (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Automatisera massexport där varje kolumn behöver en annan mask.  
* Integrera de formaterade strängarna i PDF‑rapporter med Aspose.Words.

Prova dem, så blir du snabbt go‑to‑personen för kalkylbladsformatering i ditt team. Lycka till med kodandet!   (Image: ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="Formaterat tal med avgränsare visas i Aspose.Cells‑utdata"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}