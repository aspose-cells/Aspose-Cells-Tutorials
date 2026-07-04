---
category: general
date: 2026-07-03
description: Skapa en Excel-arbetsbok i C# och ange cellformel, beräkna pi‑formeln,
  sedan exportera Excel med formler. Följ den här snabba, praktiska handledningen.
draft: false
keywords:
- create excel workbook
- set cell formula
- calculate pi formula
- how to set formula
- export excel with formulas
language: sv
og_description: Skapa en Excel-arbetsbok i C# och ange cellformel, beräkna pi‑formeln
  och exportera sedan Excel med formler. Lär dig hela processen på några minuter.
og_title: Skapa Excel-arbetsbok med formler – Komplett guide
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Create Excel workbook in C# and set cell formula, calculate pi formula,
    then export Excel with formulas. Follow this quick, practical tutorial.
  headline: Create Excel Workbook with Formulas – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create Excel workbook in C# and set cell formula, calculate pi formula,
    then export Excel with formulas. Follow this quick, practical tutorial.
  name: Create Excel Workbook with Formulas – Full Step‑by‑Step Guide
  steps:
  - name: Does the workbook keep the formulas after saving?
    text: Yes. Aspose.Cells writes both the formula string (`Formula`) and the evaluated
      value (`Value`). When you open the file, Excel will re‑evaluate the formulas
      on load, but the saved formula remains intact—perfect for later edits.
  - name: What if I need to set a formula that references another sheet?
    text: Just use the typical Excel notation, e.g., `=Sheet2!C3*2`. Aspose.Cells
      parses it correctly as long as the target sheet exists.
  - name: How to handle large data sets without blowing memory?
    text: Use `WorkbookDesigner` or stream the workbook directly to a `MemoryStream`
      and then to a response object. This avoids loading the entire file into RAM
      when you only need to push it to a client.
  - name: Can I protect the sheet while still allowing formula evaluation?
    text: 'Absolutely. After setting formulas, call:'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Skapa Excel-arbetsbok med formler – Fullständig steg‑för‑steg‑guide
url: /sv/net/excel-formulas-and-calculation-options/create-excel-workbook-with-formulas-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok med formler – Komplett guide

Har du någonsin funderat på hur du **skapar excel workbook** programatiskt och får formlerna att förbli aktiva när du öppnar filen? Du är inte ensam. Oavsett om du bygger en rapporteringsmotor, en fakturagenerator eller bara automatiserar en daglig dump, sparar det dig timmar av manuellt finjusterande att kunna sätta cellformel, beräkna pi‑formel och sedan **exportera excel med formler**.

I den här handledningen går vi igenom ett praktiskt exempel med Aspose.Cells för .NET‑biblioteket. Vi börjar med att skapa arbetsboken, visar dig sedan **hur du sätter formel** för dynamiska arrayer, beräknar ett trigonometriskt värde med π, räknar om bladet och sparar slutligen filen så att Excel visar resultaten omedelbart.

## Vad du behöver

- .NET 6 (eller någon nyare .NET‑runtime) – koden kompileras även med .NET Core.  
- Aspose.Cells för .NET – ett kraftfullt, licensfritt NuGet‑paket för vår demo (`Install-Package Aspose.Cells`).  
- En IDE du gillar (Visual Studio, Rider, VS Code – välj vad som känns bekvämt).  

Inga andra beroenden. Om du aldrig har rört Aspose.Cells tidigare, oroa dig inte; API‑et är enkelt och kodsnuttarna nedan är redo att kopieras och klistras in.

## Skapa Excel-arbetsbok – Initial setup

Först och främst. Vi behöver ett färskt workbook‑objekt som ska hysa våra kalkylblad. Tänk på det som en tom Excel‑fil som väntar på innehåll.

```csharp
using Aspose.Cells;

 // Step 1: Create a workbook and obtain the first worksheet
Workbook workbook = new Workbook();               // <-- creates a new .xlsx in memory
Worksheet ws = workbook.Worksheets[0];           // the default first sheet
```

*Varför detta är viktigt:* `Workbook`‑klassen är startpunkten för varje operation – utan den kan du inte lägga till blad, sätta formler eller exportera någonting. Genom att hämta `Worksheets[0]` får vi en referens till standardfliken som heter “Sheet1”.

> **Proffstips:** Om du behöver flera blad, anropa bara `workbook.Worksheets.Add()` och behåll den returnerade `Worksheet`‑referensen.

## Sätt cellformel – Dynamisk arrayexpansion

Nu ska vi **sätta cell formula** som expanderar ett område dynamiskt. `EXPAND`‑funktionen är en ny Excel 365‑funktion som sprider källarrayen till en angiven storlek.

```csharp
// Step 2: Apply a dynamic array formula that expands A2:A5 to 4 rows, 1 column
ws.Cells["A1"].Formula = "=EXPAND(A2:A5,4,1)";
```

Vad händer under huven?  

- `A2:A5` är källområdet (fyra celler).  
- Det andra argumentet (`4`) säger åt Excel att skapa **4 rader**.  
- Det tredje argumentet (`1`) tvingar **1 kolumn**.  

När du öppnar den sparade filen kommer cellerna A1:A4 automatiskt att innehålla värdena från A2:A5. Om du senare ändrar någon av dessa källceller uppdateras spill‑värdena omedelbart – ingen makro behövs.

> **Edge case:** `EXPAND` fungerar bara i Excel‑versioner som stödjer dynamiska arrayer (Office 365, Excel 2021+). Äldre versioner visar ett `#NAME?`‑fel.

## Beräkna pi‑formel – Trigonometriskt exempel

Nästa steg visar **calculate pi formula** genom att använda den inbyggda `PI()`‑funktionen tillsammans med `COT`. Detta demonstrerar hur vilket Excel‑kompatibelt uttryck som helst kan injiceras från kod.

```csharp
// Step 3: Apply a trigonometric formula to compute the cotangent of π/4
ws.Cells["B1"].Formula = "=COT(PI()/4)";
```

Varför `COT(PI()/4)`? Cotangenten av 45° (π/4 radianer) är 1, så cellen bör visa **1** efter beräkning. Det är en praktisk kontroll – om du ser något annat har sannolikt återberäkningssteget missats.

## Räkna om kalkylbladet – Säkerställ att formler utvärderas

Aspose.Cells utvärderar inte automatiskt formler när du sätter dem. Du måste explicit trigga en beräkningspass.

```csharp
// Step 4: Recalculate the worksheet so the formulas are evaluated
ws.CalculateFormula();
```

Genom att anropa `CalculateFormula()` går du igenom varje cell som innehåller en formel, beräknar resultatet och lagrar det i cellens `Value`‑egenskap. Detta steg garanterar att arbetsboken du sparar redan innehåller de beräknade siffrorna, vilket är praktiskt när du senare öppnar filen i en huvudlös miljö (t.ex. en rapporttjänst).

## Exportera Excel med formler – Spara filen

Till sist **exporterar vi excel med formulas** till en fysisk fil. Formatet är standard‑`.xlsx`, fullt kompatibelt med alla moderna kalkylprogram.

```csharp
// Step 5: Save the workbook to view the results
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);
```

Öppna `output.xlsx` i Excel så ser du:

| A | B |
|---|---|
| (värde från A2) | 1 |
| (värde från A3) |   |
| (värde från A4) |   |
| (värde från A5) |   |

Cell **B1** visar **1**, vilket bekräftar vår `COT(PI()/4)`‑beräkning. Cellerna **A1:A4** visar de spridda värdena från **A2:A5** tack vare `EXPAND`‑formeln.

> **Snabb verifiering:** Ändra värdet i `A2` till `99`, kör programmet igen och öppna filen på nytt. Spill‑värdet i kolumn A bör nu ha `99` högst upp i intervallet.

## Vanliga frågor & fallgropar

### Behåller arbetsboken formlerna efter sparning?

Ja. Aspose.Cells skriver både formelsträngen (`Formula`) och det beräknade värdet (`Value`). När du öppnar filen kommer Excel att utvärdera formlerna igen, men den sparade formeln förblir intakt – perfekt för senare redigeringar.

### Vad gör jag om jag måste sätta en formel som refererar till ett annat blad?

Använd den vanliga Excel‑notationen, t.ex. `=Sheet2!C3*2`. Aspose.Cells tolkar den korrekt så länge målbladet finns.

### Hur hanterar jag stora datamängder utan att spräcka minnet?

Använd `WorkbookDesigner` eller streama arbetsboken direkt till ett `MemoryStream` och sedan till ett svarobjekt. Detta undviker att hela filen laddas in i RAM när du bara behöver skicka den till en klient.

### Kan jag skydda bladet samtidigt som formler får beräknas?

Absolut. Efter att du har satt formlerna, anropa:

```csharp
ws.Protect(ProtectionType.All);
```

Skyddsflaggan hindrar inte beräkning; den begränsar bara användarredigeringar.

## Fullt fungerande exempel

Nedan är det kompletta, körklara programmet. Klistra in det i ett nytt konsolprojekt, lägg till Aspose.Cells‑NuGet‑paketet och tryck **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelFormulaDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and grab the first worksheet
            Workbook workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];

            // Populate source cells A2:A5 so the EXPAND formula has something to spill
            ws.Cells["A2"].PutValue(10);
            ws.Cells["A3"].PutValue(20);
            ws.Cells["A4"].PutValue(30);
            ws.Cells["A5"].PutValue(40);

            // 2️⃣ Set a dynamic array formula in A1
            ws.Cells["A1"].Formula = "=EXPAND(A2:A5,4,1)";

            // 3️⃣ Compute cotangent of π/4 in B1
            ws.Cells["B1"].Formula = "=COT(PI()/4)";

            // 4️⃣ Force calculation so values are stored
            ws.CalculateFormula();

            // 5️⃣ Save the workbook – this exports the Excel with formulas intact
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to: {outputPath}");
        }
    }
}
```

**Förväntat resultat** (när du öppnar `output.xlsx`):

- **A1:A4** innehåller `10, 20, 30, 40` respektive (spill‑värdena från A2:A5).  
- **B1** visar `1` (resultatet av `COT(PI()/4)`).  

Allt annat förblir tomt, precis som vi programmerade det.

## Sammanfattning

Vi har just **skapat excel workbook**, **satt cell formula** för en dynamisk array, **beräknat pi‑formel** med en trigonometrisk funktion, tvingat en återberäkning och slutligen **exporterat excel med formulas** till disk. Hela flödet ryms i ett fåtal rader, men visar de grundläggande funktionerna du behöver för automation i verkliga projekt.

Vad blir nästa steg? Prova att byta `EXPAND` mot `FILTER`, bädda in bilder via `Picture`‑objekt eller generera diagram i farten. Aspose.Cells‑API:t täcker allt från enkla cellskrivningar till komplexa pivottabeller, så möjligheterna är oändliga.

Känn dig fri att experimentera, bryta saker och sedan återkomma med dina egna justeringar. Om du stöter på problem, lämna en kommentar nedan – glad kodning! 

![Skapa Excel-arbetsbok exempel skärmbild](excel-workbook-example.png "Skapa Excel-arbetsbok exempel som visar formler i A1 och B1")


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Excel Automation with Aspose.Cells .NET&#58; Mastering Workbook & Formula Calculations](/cells/english/net/formulas-functions/excel-automation-aspose-cells-net-workbook-formulas/)
- [Excel Automation with Aspose.Cells .NET&#58; Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}