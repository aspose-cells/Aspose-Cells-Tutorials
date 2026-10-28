---
category: general
date: 2026-10-04
description: Lär dig hur du skapar en Excel‑arbetsbok i C# och använder EXPAND, tvingar
  formelberäkning och sparar arbetsboken som XLSX samtidigt som du fyller en kolumn
  med siffror.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- how to use expand
- force formula calculation
- save workbook as xlsx
- populate column with numbers
language: sv
lastmod: 2026-10-04
og_description: Skapa Excel-arbetsbok i C# med Aspose.Cells. Denna handledning visar
  hur du använder EXPAND, tvingar formelberäkning och sparar arbetsboken som XLSX
  samtidigt som du fyller en kolumn med siffror.
og_image_alt: Screenshot of a C# program that creates an Excel workbook and applies
  the EXPAND function
og_title: Skapa Excel-arbetsbok i C# – fullständig guide med EXPAND och XLSX-sparning
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to create Excel workbook in C# and use EXPAND, force formula
    calculation, and save workbook as XLSX while populating a column with numbers.
  headline: How to create Excel workbook in C# with the EXPAND function
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Hur man skapar en Excel‑arbetsbok i C# med EXPAND‑funktionen
url: /sv/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-with-the-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar en Excel-arbetsbok i C# med EXPAND‑funktionen

Om du behöver **skapa en Excel‑arbetsbok** programatiskt visar den här guiden en komplett, färdig‑att‑köra lösning. Du får se hur du **fyller en kolumn med tal**, använder **EXPAND**‑funktionen för att spilla data horisontellt, **tvingar formelberäkning**, och slutligen **sparar arbetsboken som XLSX**.  

Denna handledning täcker varje steg du behöver, från initiering av arbetsboken till verifiering av resultatet. Ingen extern dokumentation krävs – kopiera bara koden, kör den, så har du en fullt fungerande Excel‑fil.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.6+)
- Aspose.Cells för .NET NuGet‑paket (`Install-Package Aspose.Cells`)
- Grundläggande kunskap om C#‑syntax
- En IDE såsom Visual Studio eller VS Code

## Steg 1: Skapa Excel‑arbetsbok och få åtkomst till det första kalkylbladet

Det första steget är att **skapa en Excel‑arbetsbok** och hämta en referens till dess standardkalkylblad. Aspose.Cells lägger automatiskt till ett kalkylblad på index 0, så du kan börja arbeta med det direkt.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();          // create Excel workbook
        Worksheet sheet = workbook.Worksheets[0];   // first (default) worksheet
```

*Varför detta är viktigt:* Att instansiera `Workbook` allokerar den interna filstrukturen, och att hämta `Worksheets[0]` ger dig ett konkret `Worksheet`‑objekt att manipulera rader, kolumner och celler med.

## Steg 2: Fyll kolumnen med tal

Fyll därefter en vertikal lista i kolumn A. Detta demonstrerar **populate column with numbers** och ger källintervallet för EXPAND‑funktionen.

```csharp
        // Step 2: Fill a vertical list of values in column A
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);
```

*Proffstips:* Använd `PutValue` för råa tal, strängar, datum eller någon .NET‑primitiv. Metoden bestämmer automatiskt celltypen.

## Steg 3: Så här använder du EXPAND – spilla listan horisontellt

Delavsnittet **how to use expand** är kärnan i den här handledningen. `EXPAND`‑funktionen expanderar ett källintervall till en ny form. Här expanderar vi det vertikala intervallet `A1:A3` till en enda rad som sträcker sig över tre kolumner, med start i `B1`.

```csharp
        // Step 3: Apply the EXPAND function to spill the list horizontally starting at B1
        // The formula expands the range A1:A3 into 1 row and 3 columns (B1:D1)
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";
```

*Förklaring:*  
- Det första argumentet (`A1:A3`) är källintervallet.  
- Det andra argumentet (`1`) tvingar resultatet att ha **1** rad.  
- Det tredje argumentet (`3`) tvingar resultatet att ha **3** kolumner.  

När arbetsboken räknas om kommer cellerna `B1`, `C1` och `D1` att innehålla `1`, `2` respektive `3`.

## Steg 4: Tvinga formelberäkning

Aspose.Cells utvärderar inte automatiskt formler efter att du har ställt in dem, så du måste **force formula calculation** innan du sparar. Detta säkerställer att EXPAND‑resultatet materialiseras i filen.

```csharp
        // Step 4: Force calculation of all formulas in the workbook
        workbook.CalculateFormula();   // triggers calculation engine
```

*Varför du behöver det:* Utan att anropa `CalculateFormula` skulle den sparade filen innehålla den råa formelsträngen, och Excel skulle bara beräkna om när filen öppnas. För automatiserade pipelines vill du vanligtvis ha värdena skrivna omedelbart.

## Steg 5: Spara arbetsboken som XLSX

Nu när arbetsboken är helt färdig, **save workbook as XLSX** till en plats du själv väljer. Filändelsen bestämmer utdataformatet; `.xlsx` skapar en Office Open XML‑arbetsbok.

```csharp
        // Step 5: Save the workbook to a file
        string outputPath = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(outputPath);   // save workbook as XLSX
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

*Tips:* Om du behöver ett annat format (CSV, PDF osv.) ändrar du bara filändelsen eller använder `workbook.Save(outputPath, SaveFormat.Xls)` för äldre Excel‑versioner.

## Fullt, körbart exempel

När alla bitar sätts ihop får du ett självständigt program som **creates Excel workbook**, fyller en kolumn, använder **EXPAND**, tvingar beräkning och **saves workbook as XLSX**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create Excel workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2. Populate column with numbers
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // 3. How to use EXPAND – spill horizontally
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";

        // 4. Force formula calculation
        workbook.CalculateFormula();

        // 5. Save workbook as XLSX
        string path = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(path);
        System.Console.WriteLine($"Workbook saved to {path}");
    }
}
```

### Förväntat resultat

Efter att programmet har körts, öppna `ExpandFunction.xlsx` i Excel. Du bör se:

| A | B | C | D |
|---|---|---|---|
| 1 | 1 | 2 | 3 |
| 2 |   |   |   |
| 3 |   |   |   |

Värdena `1`, `2`, `3` i cellerna `B1:D1` bekräftar att **EXPAND**‑funktionen fungerade och att steget **force formula calculation** framgångsrikt materialiserade resultaten.

## Vanliga variationer och kantfall

| Scenario | Anpassning |
|----------|------------|
| **Dynamiskt källintervall** | Använd `=EXPAND(A1:INDEX(A:A, COUNTA(A:A)), 1, 0)` för att expandera så många rader som är fyllda. |
| **Olika utdata‑dimensioner** | Ändra de andra och tredje argumenten i `EXPAND` för att styra rader och kolumner. |
| **Flera kalkylblad** | Loopa igenom `workbook.Worksheets` och applicera samma logik på varje blad. |
| **Stora datamängder** | Anropa `workbook.CalculateFormula()` en gång efter att alla formler satts för att undvika upprepade omräkningar. |
| **Spara till minnesström** | Ersätt `workbook.Save(path)` med `workbook.Save(stream, SaveFormat.Xlsx)` när du behöver filen i ett web‑API‑svar. |

## Felsökningschecklista

- **Formeln expanderar inte:** Kontrollera att `CalculateFormula()` anropas *efter* att formeln satts.  
- **Filen hittas inte vid sparning:** Säkerställ att målkatalogen finns och att processen har skrivrättigheter.  
- **Fel datatyp:** Använd `PutValue` för tal; för datum, använd `PutValue(DateTime.Now)` eller `PutDateTime`.  
- **Versionskonflikt:** EXPAND‑funktionen kräver en Excel 365‑kompatibel beräkningsmotor; Aspose.Cells 23.9+ stödjer den.

## Slutsats

Du vet nu hur du **creates Excel workbook** i C#, **populate column with numbers**, använder **EXPAND**‑funktionen, **force formula calculation**, och **saves workbook as XLSX**. Detta end‑to‑end‑exempel kan anpassas för rapportering, datatransformation eller någon automatiseringssituation som kräver dynamisk Excel‑utdata.

### Nästa steg

- Utforska andra dynamiska array‑funktioner såsom `FILTER`, `SORT` och `UNIQUE`.  
- Integrera arbetsboksgenereringen i ett ASP.NET Core‑API för att leverera Excel‑filer på begäran.  
- Ersätt de hårdkodade siffrorna med data läst från en databas eller CSV‑fil för verklig rapportering.

Känn dig fri att experimentera med olika intervall, bladnamn och utdataformat. Lycka till med kodandet!


## Vad bör du lära dig härnäst?


Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [How to Calculate Cotangent in Excel with C# – Create Workbook, Use EXPAND,](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}