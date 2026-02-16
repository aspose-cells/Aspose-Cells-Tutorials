---
category: general
date: 2026-02-15
description: Hur man använder WRAPCOLS för att skapa en tvåkolumnslayout, lägga till
  en formel och generera en sekvensarray i C#‑arbetsblad – steg‑för‑steg‑guide.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: sv
og_description: Så använder du WRAPCOLS för att skapa en tvåkolumnslayout, lägga till
  formler och generera en sekvensarray i ett C#‑arbetsblad – komplett guide.
og_title: 'Hur du använder WRAPCOLS: Tvåkolumnslayout i C#'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'Hur du använder WRAPCOLS: Skapa en tvåkolumnslayout i C#'
url: /sv/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

placeholders unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder WRAPCOLS: Skapa en två‑kolumnslayout i C#

Har du någonsin undrat **hur man använder WRAPCOLS** när du behöver en snabb två‑kolumnsvy i ett Excel‑liknande kalkylblad? Du är inte ensam. Många utvecklare stöter på problem när de försöker dela upp en genererad lista i snygga kolumner utan att skriva en loop för varje cell. De goda nyheterna? Med `WRAPCOLS`‑funktionen kan du placera en enda formel i `A1` och låta Excel (eller en kompatibel motor) göra det tunga arbetet.

I den här handledningen går vi igenom **hur man lägger till formel** som skapar en **två‑kolumnslayout**, visar dig **hur man skapar kolumner** dynamiskt, och även **genererar sekvensarray**‑värden i farten. I slutet har du ett fullt körbart C#‑snutt som du kan klistra in i ditt projekt, köra och se ett prydligt två‑kolumnsblock visas omedelbart.

## Vad du kommer att lära dig

- Syftet med `WRAPCOLS` och varför det är ett bättre alternativ än manuell loopning.  
- Hur man **lägger till en formel** i en kalkylblads cell med C#.  
- Hur man genererar en sekvensarray med `SEQUENCE` och matar in den i `WRAPCOLS`.  
- Tips för att omberäkna bladet så att formeln löser sig omedelbart.  
- Hantering av kantfall (t.ex. tomma kalkylblad, anpassade kolumnantal).

Inga externa bibliotek utöver ett standard Excel‑bearbetningspaket krävs – vi kommer att använda **ClosedXML** för dess enkla API, men koncepten kan överföras till EPPlus, SpreadsheetGear eller till och med Google Sheets via dess API.

---

## Förutsättningar

- .NET 6.0 eller senare (koden kompileras på .NET Core och .NET Framework).  
- En referens till **ClosedXML** (`dotnet add package ClosedXML`).  
- Grundläggande C#‑kunskaper – du bör vara bekväm med `using`‑satser och objektinitialisering.  

Om du redan har en arbetsbok öppen kan du hoppa över delen för att skapa filen och gå direkt till formeldelen.

## Steg 1: Ställ in kalkylbladet (Hur man skapar kolumner)

Först behöver vi ett `Worksheet`‑objekt att arbeta med. I ClosedXML får du det från en `XLWorkbook`. Kodsnutten nedan skapar en ny arbetsbok, lägger till ett blad som heter *Demo*, och hämtar en referens som heter `worksheet` för tydlighet.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **Varför byta namn?**  
> Att hålla variabelnamnet kort (`worksheet`) gör den efterföljande koden lättare att läsa, särskilt när du kedjar flera operationer. Det speglar också den namngivningsstil du ser i de flesta dokumentationer, vilket minskar den kognitiva belastningen.

## Steg 2: Skriv formeln (Hur man lägger till formel + Generera sekvensarray)

Nu kommer den magiska raden. Vi placerar en formel i cell **A1** som gör två saker:

1. **Generera en sekvensarray** med sex tal (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Wrapa de siffrorna i två kolumner** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **Vad händer?**  
> `SEQUENCE(6)` skapar en vertikal array `{1;2;3;4;5;6}`. `WRAPCOLS` tar sedan den arrayen och “wrapar” den till det angivna antalet kolumner – i detta fall **2**. Resultatet är ett 3‑rad × 2‑kolumnsblock som ser ut så här:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Om du ändrar det andra argumentet till **3** får du istället en tre‑kolumnslayout. Det är kärnan i **hur man skapar kolumner** i farten utan manuella loopar.

## Steg 3: Omberäkna kalkylbladet (Säkerställa att formeln utvärderas)

ClosedXML kommer inte automatiskt att utvärdera formler när du skriver dem. Du måste anropa `Calculate()` på arbetsboken (eller på det specifika kalkylbladet) för att tvinga en utvärdering.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Proffstips:** Om du arbetar med stora arbetsböcker, anropa `Calculate()` endast på de blad som faktiskt har ändrats. Detta sparar minne och snabbar upp bearbetningen.

När du öppnar `WrapColsDemo.xlsx` kommer du att se den två‑kolumnslayout som prydligt fylls i **A1:B3**. Ingen extra kod krävdes för att loopa genom rader eller kolumner – `WRAPCOLS` hanterade allt.

## Steg 4: Verifiera resultatet (Vad du kan förvänta dig)

Efter att programmet har körts, öppna den genererade filen. Du bör se:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Om siffrorna visas vertikalt (dvs. alla i kolumn A), dubbelkolla att du anropade `worksheet.Calculate()` **efter** att formeln satts. Vissa motorer kräver även `workbook.Calculate()`; kodsnutten ovan fungerar för ClosedXML:s inbyggda evaluator.

## Vanliga variationer & kantfall

### Ändra antalet kolumner

För att **skapa två‑kolumnslayout** med ett annat radantal, justera helt enkelt `SEQUENCE`‑storleken eller det andra argumentet i `WRAPCOLS`:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

Detta ger ett 4‑rad × 3‑kolumnsblock (12 siffror fördelade på tre kolumner).

### Använda ett dynamiskt kolumnantal

Om ditt kolumnantal kommer från en variabel, bädda in det med stränginterpolering:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Nu har du **hur man lägger till formel** som anpassar sig vid körning.

### Tomma kalkylblad

Om kalkylbladet är tomt fungerar `Calculate()` fortfarande – formeln kommer att fylla celler med start i A1. Men om du senare tar bort rader/kolumner som skär igenom utskriftsområdet kan du få `#REF!`‑fel. För att undvika det, rensa målområdet först:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Kompatibilitet

`WRAPCOLS` och `SEQUENCE` är en del av Excels **Dynamic Array**‑funktioner, introducerade i Office 365. Om du riktar dig mot äldre Excel‑versioner finns inte funktionerna, och du måste använda en manuell loop. ClosedXML:s evaluator speglar det senaste Excel‑beteendet, så den är säker för moderna miljöer.

## Fullt fungerande exempel (Klar att kopiera och klistra in)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Förväntat resultat:** När du öppnar *WrapColsDemo.xlsx* visas en prydlig två‑kolumnslayout med siffrorna 1‑6 arrangerade som beskrivits tidigare.

## Slutsats

Vi har gått igenom **hur man använder WRAPCOLS** för att **skapa en två‑kolumnslayout**, demonstrerat **hur man lägger till formel** programatiskt, och sett hur `SEQUENCE` låter dig **generera sekvensarray**‑värden utan en loop. Genom att utnyttja Excels dynamiska array‑funktioner från C# kan du hålla din kod kortfattad, läsbar och underhållbar.

Nästa steg kan du utforska:

- **Skapa dynamiska radantal** med `ROWS` eller `COUNTA`.  
- **Styling av utskriften** (ramar, talformat) med ClosedXML:s styling‑API.  
- **Exportera till CSV** efter att layouten är byggd, för efterföljande bearbetning.

Prova, justera kolumnantalet, och se hur snabbt du kan prototypa komplexa kalkylblad. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}