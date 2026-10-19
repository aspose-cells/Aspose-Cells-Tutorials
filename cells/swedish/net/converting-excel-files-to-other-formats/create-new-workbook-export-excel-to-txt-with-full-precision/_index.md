---
category: general
date: 2026-03-18
description: Skapa en ny arbetsbok och exportera Excel till TXT samtidigt som du bevarar
  numerisk precision. Lär dig hur du sparar kalkylblad som txt och konverterar kalkylblad
  till txt på ett effektivt sätt.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: sv
og_description: Skapa en ny arbetsbok och exportera Excel till TXT med precision.
  Denna handledning visar hur man sparar ett kalkylblad som txt och konverterar ett
  kalkylblad till txt med C#.
og_title: Skapa ny arbetsbok – Guide för att exportera Excel till TXT
tags:
- Aspose.Cells
- C#
- Excel automation
title: Skapa ny arbetsbok – Exportera Excel till TXT med full precision
url: /sv/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ny arbetsbok – Exportera Excel till TXT med full precision

Har du någonsin behövt **create new workbook** i C# bara för att dumpa data till en ren textfil? Kanske hämtar du en rapport från ett gammalt system och verktyget nedströms bara accepterar ett `.txt`‑flöde. De goda nyheterna? Du behöver inte offra numerisk precision, och du behöver definitivt inte hand‑koda CSV‑strängar.

I den här guiden går vi igenom hela processen för **export excel to txt**, från att initiera arbetsboken till att bevara efterföljande nollor när du **save worksheet as txt**. I slutet har du ett färdigt kodsnutt som du kan klistra in i vilket .NET‑projekt som helst—utan extra verktyg.

## Vad du behöver

- **ASP.NET/ .NET 6+** (koden fungerar även på .NET Framework 4.6+)  
- **Aspose.Cells for .NET** – biblioteket som driver klasserna `Workbook`, `Worksheet` och `TxtSaveOptions`. Du kan hämta det från NuGet med `Install-Package Aspose.Cells`.  
- Grundläggande kunskap i C# (om du är bekväm med `using`‑satser, är du redo att köra).  

Det är allt—ingen Excel‑interop, inga COM‑objekt, och definitivt ingen manuell strängkonkatenering.  

---

## Steg 1: Initiera en ny arbetsbok (Primärt nyckelord)

Det första du måste göra är **create new workbook**. Tänk på arbetsboken som en tom duk där du senare kan klistra in siffror, text eller formler.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **Varför detta är viktigt:** Att instansiera `Workbook` utan att ladda en fil ger dig en ren start. Du kan sedan lägga till data programatiskt, vilket är perfekt för **convert worksheet to txt**‑scenarier där du inte har en befintlig `.xlsx`.

---

## Steg 2: Fyll i celler – behåll efterföljande nollor

En vanlig fallgrop när man dumpar siffror till text är att förlora efterföljande nollor (`123.45000` blir `123.45`). Om nedströmsystemen förlitar sig på fält med fast bredd kan den förlusten förstöra allt.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Proffstips:** `PutValue` infererar automatiskt datatypen. Om du behöver en sträng som ser ut som ett tal, använd `PutValue("123.45000")` istället.

---

## Steg 3: Konfigurera TXT‑sparaalternativ – bevara numerisk precision

Här händer magin. Genom att slå på `PreserveNumericPrecision` instruerar du Aspose.Cells att skriva exakt det värde du angav, inklusive eventuella obetydliga efterföljande nollor.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **Varför aktivera detta?** När du **save excel as txt** tar standardbeteendet bort onödiga decimaler. Att sätta `PreserveNumericPrecision = true` garanterar att utdata speglar cellens visade värde, vilket är kritiskt för finansiella rapporter eller vetenskapliga data.

---

## Steg 4: Spara arbetsbladet som TXT – den slutgiltiga exporten

Nu sparar vi faktiskt **save worksheet as txt**. Du kan ange sökvägen var du än har skrivbehörighet; exemplet använder en relativ mapp som heter `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Förväntad utdata** (`num-preserve.txt`):

```
123.45000
```

Observera att de efterföljande nollorna är intakta—precis som du begärde.

---

## Steg 5: Verifiera resultatet – snabb kontroll

När programmet har körts, öppna `num-preserve.txt` i någon textredigerare. Du bör se den enda raden `123.45000`. Om du ser `123.45` istället, dubbelkolla att `PreserveNumericPrecision` är satt till `true` och att du använder en nyare version av Aspose.Cells (v23.10+).

---

## Vanliga variationer & kantfall

### Exportera flera celler eller områden

Om du behöver **export excel to txt** för ett helt område, fyll helt enkelt fler celler innan du sparar:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose kommer som standard att skriva varje cell på en ny rad. Du kan också ändra avgränsaren (tab, komma) via `txtSaveOptions.Separator`.

### Konvertera arbetsblad till TXT med olika kodningar

Ibland kräver nedströmsystem UTF‑8 BOM eller ASCII. Justera kodningen så här:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Hantera stora arbetsböcker

När du hanterar enorma blad (hundratusentals rader), överväg att strömma utdata:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## Proffstips & fallgropar

- **Glöm inte att skapa output‑katalogen** innan du anropar `Save`, annars får du ett `DirectoryNotFoundException`.  
- **Var uppmärksam på localespecifika decimalavgränsare**. Om din miljö använder kommatecken (`1,23`), sätt `txtSaveOptions.DecimalSeparator = '.'` för att tvinga en punkt.  
- **Versionskompatibilitet**: Flaggan `PreserveNumericPrecision` introducerades i Aspose.Cells 20.6. Om du använder en äldre version finns inte flaggan och du måste formatera cellen som text innan du sparar.

---

![Exempel på att skapa ny arbetsbok](excel-to-txt.png "Skapa ny arbetsbok")

*Bildtext: "Skapa ny arbetsbok och exportera Excel till TXT med numerisk precision bevarad"*

---

## Sammanfattning – Vad vi gick igenom

- **Create new workbook** med Aspose.Cells.  
- Fyll en cell med ett tal som innehåller efterföljande nollor.  
- Sätt `TxtSaveOptions.PreserveNumericPrecision = true` för att **save excel as txt** utan att förlora precision.  
- Skriv filen till disk och verifiera att utdata matchar det ursprungliga värdet.  

Det är hela **convert worksheet to txt**‑arbetsflödet på under 50 rader C#.

---

## Nästa steg & relaterade ämnen

Nu när du kan **export excel to txt** med perfekt precision kanske du vill utforska:

- **Exportera till CSV** med anpassade avgränsare (`TxtSaveOptions.Separator`).  
- **Spara som andra ren‑textformat** som TSV (`SaveFormat.TabDelimited`).  
- **Batch‑bearbetning** av flera arbetsböcker i en mapp med `Directory.GetFiles`.  
- **Integrera med Azure Functions** för konvertering på begäran i molnet.

Var och en av dessa bygger på samma `Workbook` → `Worksheet` → `TxtSaveOptions`‑mönster, så du kommer känna dig hemma.

---

### Avslutande tanke

Om du har följt med, vet du nu exakt hur du **create new workbook**, fyller den och **save worksheet as txt** samtidigt som du behåller varje decimal som du bryr dig om. Det är en liten kodbit, men den löser ett förvånansvärt vanligt huvudvärk när äldre pipelines kräver ren‑text‑indata.

Prova det, justera alternativen, och låt data flöda precis som du vill. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}