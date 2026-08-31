---
category: general
date: 2026-02-23
description: Skapa en ny arbetsbok programatiskt i C# och lägg till en formel i en
  cell. Lär dig hur du använder EXPAND och spara sedan Excel‑arbetsboken utan ansträngning.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: sv
og_description: Skapa en ny arbetsbok programatiskt i C#. Lägg till en formel i en
  cell, lär dig hur du använder EXPAND och spara Excel‑arbetsboken på några sekunder.
og_title: Skapa ny arbetsbok i C# – Lägg till formel och spara Excel‑fil
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Skapa ny arbetsbok i C# – Lägg till formel och spara Excel‑fil
url: /sv/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

keep technical terms like EXPAND? Should keep as is. Table "Argument | Meaning". Translate to "Argument | Betydelse". Row values keep same.

Now produce final.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ny arbetsbok i C# – Lägg till formel och spara Excel‑fil

Har du någonsin funderat på hur man **create new workbook**‑objekt från kod utan att någonsin öppna Excel? Du är inte ensam. Många utvecklare fastnar när de måste generera ett kalkylblad i farten – kanske för en rapport, en export eller en snabb data‑dump.  

Den goda nyheten? I den här guiden får du se exakt hur du **create new workbook**, lägger till en **add formula to cell**, och sedan **save excel workbook** med bara några rader C#. Vi dyker också in i **how to use expand** så att du kan skapa dynamiska arrayer utan manuellt kopierande. När du är klar kan du **create excel file programmatically** och leverera den till användare eller downstream‑tjänster.

## Förutsättningar

- .NET 6.0 eller senare (någon aktuell .NET‑runtime fungerar)
- Aspose.Cells för .NET (gratis provversion eller licensierad version) – detta bibliotek ger oss klasserna `Workbook` och `Worksheet` som används nedan.
- Grundläggande förståelse för C#‑syntax – ingen djup Excel‑kunskap krävs.

Om du redan har detta, toppen! Om inte, hämta Aspose.Cells från NuGet (`Install-Package Aspose.Cells`) så är du redo att köra.

---

## Steg 1: Skapa ny arbetsbok – Grunden

För att börja måste vi instansiera ett nytt arbetsbok‑objekt. Tänk på det som att öppna en helt ny Excel‑fil som är helt tom.

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Varför detta är viktigt:** `Workbook`‑klassen är startpunkten för all Excel‑manipulation. Genom att skapa en ny instans allokerar vi minne för blad, stilar och formler – helt utan att röra filsystemet.

---

## Steg 2: Åtkomst till det första kalkylbladet

Varje ny arbetsbok kommer med ett standardkalkylblad (namnet *Sheet1*). Vi hämtar det så att vi kan placera data och formler.

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Proffstips:** Om du behöver flera blad, anropa helt enkelt `workbook.Worksheets.Add("MySheet")` och arbeta med det returnerade `Worksheet`‑objektet.

---

## Steg 3: Lägg till formel i cell – Använd EXPAND

Nu till den roliga delen: att infoga en formel. `EXPAND`‑funktionen är perfekt när du vill omvandla en statisk array till ett större, automatiskt fyllt område.

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### Så fungerar EXPAND‑formeln

| Argument | Betydelse |
|----------|-----------|
| `{1,2,3}` | Källarrayen (en horisontell lista med tre tal) |
| `5`       | Önskat antal rader i resultatet |
| `1`       | Önskat antal kolumner (håll den på 1 för att behålla vertikalt) |

När Excel utvärderar detta får du en **vertikal** lista:

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **Varför använda EXPAND?** Det eliminerar behovet av manuellt kopierande eller VBA‑loopar. Funktionen omformar data dynamiskt, vilket gör dina kalkylblad mer robusta och enklare att underhålla.

---

## Steg 4: Spara Excel‑arbetsbok – Skriv resultatet till disk

Med formeln på plats är sista steget att skriva arbetsboken till disk. Du kan välja vilken mapp du har skrivbehörighet till.

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **Vad du kommer att se:** Öppna `ExpandFormula.xlsx` i Excel, och cell `A1` visar den expanderade arrayen. Formeln själv finns kvar i cellen, så om du redigerar källarrayen uppdateras resultatet automatiskt.

---

## Valfritt: Verifiera resultatet programatiskt

Om du föredrar att inte öppna Excel manuellt kan du läsa tillbaka värdena för att bekräfta att de stämmer.

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

Kör ovanstående så skrivs följande ut:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## Vanliga frågor & kantfall

| Fråga | Svar |
|----------|--------|
| **Kan jag använda EXPAND med en större källarray?** | Absolut. Byt bara `{1,2,3}` mot någon konstant eller cellområde, t.ex. `EXPAND(A1:C1,10,1)`. |
| **Vad händer om jag vill ha ett horisontellt resultat?** | Byt plats på rad‑/kolumnargumenten: `EXPAND({1,2,3},1,5)` ger en 1‑rad, 5‑kolumn spridning. |
| **Fungerar detta i äldre versioner av Excel?** | `EXPAND` finns från och med Excel 365/2021. För äldre versioner måste du simulera arrayen med `INDEX`/`SEQUENCE`. |
| **Behöver jag anropa `workbook.CalculateFormula()`?** | Nej. Aspose.Cells utvärderar formler automatiskt vid sparande, så värdena visas omedelbart. |
| **Hur lägger jag till fler än ett blad innan sparning?** | Anropa `workbook.Worksheets.Add("SecondSheet")` och upprepa cell‑manipuleringsstegen på det nya bladet. |

---

## Fullständigt fungerande exempel

Nedan är det kompletta, körklara programmet. Kopiera‑klistra in i en konsolapp, justera sökvägen för utdata och tryck **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Förväntad konsolutskrift:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

Öppna den genererade filen så ser du samma siffror fyllda i kolumn **A**.

---

## Visuell sammanfattning

![Skapa ny arbetsbok exempel](create-new-workbook.png "Skärmbild som visar en ny arbetsbok skapad med create new workbook i C#")

*Bilden illustrerar den nyskapade arbetsboken med EXPAND‑resultatet.*

---

## Slutsats

Du vet nu hur du **create new workbook**, **add formula to cell**, och **save excel workbook** med C#. Genom att behärska **how to use expand** kan du generera dynamiska arrayer utan manuellt arbete, och hela processen låter dig **create excel file programmatically** för alla automatiseringsscenarier.

Vad blir nästa steg? Prova att byta ut den konstanta arrayen mot ett område, experimentera med olika `EXPAND`‑dimensioner, eller kedja flera formler över blad. Samma mönster fungerar för diagram, formatering och till och med pivottabeller – så fortsätt utforska.

Om du stöter på problem, lämna en kommentar nedan. Lycka till med kodandet, och njut av kraften i programmatisk Excel!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}