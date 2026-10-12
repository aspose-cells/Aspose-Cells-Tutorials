---
category: general
date: 2026-03-01
description: Hur man snabbt skapar en arbetsbok i C# — lär dig att skriva värde till
  en cell, sätta cellens talformat och formatera cellens tal med enkla steg.
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: sv
og_description: Hur skapar man en arbetsbok i C#? Den här guiden visar hur du skriver
  ett värde till en cell, sätter cellens talformat och formaterar cellens tal med
  bara några få rader kod.
og_title: Hur man skapar en arbetsbok i C# – Skriv värde och formatera tal
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Hur man skapar en arbetsbok i C# – Skriva värde och formatera tal
url: /sv/net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så skapar du en arbetsbok i C# – Skriv värde & formatera tal

Att skapa en arbetsbok i C# är en vanlig uppgift när du behöver generera Excel‑filer i farten. I den här guiden går vi igenom hur du skriver ett värde till en cell och formaterar cellens tal så att det färdiga bladet ser professionellt ut.

Om du någonsin har stirrat på ett tomt kalkylblad och undrat varför siffrorna alltid visas med för många decimaler, är du inte ensam. Vi täcker allt från att initiera arbetsboks‑objektet till att sätta ett anpassat talformat, och vi ger några tips för kantfall du kan stöta på senare.

## Vad du kommer att lära dig

- **Initiera** en ny `Workbook`‑instans.  
- **Skriva värde till cell** med metoden `PutValue`.  
- **Sätta cellens talformat** med ett `Style`‑objekt för att få en ren två‑siffrig visning.  
- Verifiera resultatet genom att läsa tillbaka cellen eller öppna filen i Excel.  

Inga externa bibliotek behövs utöver standard‑Aspose.Cells (eller motsvarande API), och koden körs på .NET 6+ utan extra konfiguration.

---

## Så skapar du en arbetsbok – Initiera objektet

Först och främst: du behöver ett arbetsboks‑objekt som håller dina blad. Tänk på `Workbook` som hela Excel‑filen, medan varje `Worksheet` är en enskild flik.

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*Varför detta är viktigt:* Att skapa arbetsboken allokerar de interna strukturerna som senare håller rader, kolumner och formatering. Utan detta objekt finns ingen plats att skriva ett värde till en cell.

> **Proffstips:** Om du planerar att arbeta med en befintlig fil, ersätt `new Workbook()` med `new Workbook("template.xlsx")` för att ladda en mall och bevara dess stilar.

## Skriv värde till cell

Nu när vi har en arbetsbok, låt oss lägga in ett tal i cell **A1** på det första kalkylbladet.

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*Varför vi använder `PutValue`*: Denna metod upptäcker automatiskt datatypen, så du slipper kasta eller konvertera manuellt. Den respekterar också cellens befintliga stil, vilket är praktiskt när du senare **sätter cellens talformat**.

### Snabb kontroll

Om du läser tillbaka cellen ser du det råa värdet:

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

Det är talet innan någon formatering har tillämpats.

## Sätt cellens talformat

Att visa ett rått double‑värde med många decimaler är inte alltid användarvänligt. Låt oss begränsa det till två signifikanta siffror.

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

`Number`‑egenskapen motsvarar Excels inbyggda talformat‑ID:n. `2` betyder “Tal med två decimaler”. Om du behöver ett annat format – till exempel valuta eller datum – använder du ett annat ID eller en anpassad formatsträng.

### Alternativ: Anpassad formatsträng

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*Varför välja en anpassad stil?* Den ger dig full kontroll, särskilt när de inbyggda ID:n inte täcker dina regionala inställningar.

## Verifiera resultatet (valfritt men rekommenderat)

Efter att ha tillämpat stilen kan du spara arbetsboken och öppna den i Excel för att bekräfta utseendet.

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

Du bör se **123,46** i cell A1 – exakt två decimaler, tack vare formatet vi satte.

---

### Fullt fungerande exempel

Sätter vi ihop allt får du ett självständigt program som du kan kopiera och klistra in i en konsolapp.

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**Förväntad utskrift när du kör programmet:**

```
Cell A1 shows: 123.46
```

Öppna `FormattedWorkbook.xlsx` i Excel så ser du samma formaterade värde.

---

## Vanliga varianter & kantfall

### 1. Olika talformat

| Mål | Format‑ID | Kodsnutt |
|------|-----------|--------------|
| Valuta (två decimaler) | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| Procent (inga decimaler) | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| Vetenskaplig notation | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

Om inget av de inbyggda ID:n passar, återgå till en anpassad sträng som visades tidigare.

### 2. Kulturspecifika decimalavgränsare

Vissa språk använder kommatecken för decimaler. Du kan tvinga fram ett kulturanpassat format:

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. Skriva text istället för tal

När du behöver **hur man skriver cell** med en sträng, skicka bara en sträng till `PutValue`:

```csharp
cellA1.PutValue("Total Revenue");
```

Inget talformat krävs, men du kan fortfarande tillämpa teckensnittsstyling.

### 4. Stora datamängder

Om du fyller i tusentals rader är batch‑inmatning (`Cells.ImportArray`) snabbare än att loopa `PutValue`. Formateringsmetoden är densamma; du applicerar bara stilen på ett område:

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## Vanliga frågor

**Q: Fungerar detta med .NET Core?**  
A: Absolut. Aspose.Cells stödjer .NET Standard 2.0 och senare, så du kan rikta in dig på .NET 5, .NET 6 eller .NET 7 utan ändringar.

**Q: Vad händer om jag behöver fler än två decimaler?**  
A: Ändra `Number`‑egenskapen till rätt inbyggt ID (t.ex. `3` för tre decimaler) eller justera den anpassade formatsträngen (`"#,##0.000"`).

**Q: Kan jag applicera formatet på en hel kolumn på en gång?**  
A: Ja. Använd `Cells["A:A"]` för att hämta hela kolumnen och sedan `SetStyle`.

---

## Slutsats

Du vet nu **hur man skapar arbetsboks**‑objekt i C#, **skriva värde till cell** och **sätta cellens talformat** så att siffrorna visas exakt som du vill. Genom att behärska dessa grunder kan du generera professionella Excel‑rapporter, fakturor eller dataexporter med minimal ansträngning.

Nästa steg kan vara att utforska **format cell number** för datum, procent eller villkorsstyrd formatering – varje del bygger på samma principer som vi gått igenom. Dyka djupare i Aspose.Cells‑dokumentationen för mer avancerade stylingalternativ, eller prova att kombinera flera kalkylblad i en enda arbetsbok för rikare rapporter.

Lycka till med kodningen, och kom ihåg: ett välformaterat kalkylblad är bara

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}