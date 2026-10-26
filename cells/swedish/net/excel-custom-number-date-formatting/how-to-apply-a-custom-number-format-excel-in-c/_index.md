---
category: general
date: 2026-10-26
description: Lär dig hur du ställer in ett anpassat talformat i en Excel‑fil i C#
  genom att konfigurera signifikanta siffror, skapa en Excel‑arbetsbok och spara den
  som ett XLSX‑dokument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format excel
- set significant digits
- how to set number format
- create excel workbook c#
- save workbook xlsx
language: sv
lastmod: 2026-10-26
og_description: Anpassat talformat i Excel med C# låter dig kontrollera signifikanta
  siffror, skapa en Excel‑arbetsbok och spara den som XLSX. Följ den här kompletta
  handledningen.
og_image_alt: Excel cell A1 displaying a number formatted with 4 significant digits
  using C#
og_title: Anpassat talformat i Excel med C# – steg‑för‑steg guide
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  headline: How to apply a custom number format excel in C#
  type: TechArticle
- description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  name: How to apply a custom number format excel in C#
  steps:
  - name: Using a custom format string instead of global options
    text: 'If you need a format that applies only to a single range, you can assign
      a format string directly:'
  - name: Applying the setting to an entire column
    text: '```csharp // Apply the same significant‑digit rule to column B ws.Cells.Columns[1].ApplyNumberFormatOptions(
      new NumberFormatOptions { SignificantDigits = 4 }); ```'
  - name: Dealing with negative numbers
    text: 'The global `SignificantDigits` option works uniformly for positive and
      negative numbers. If you want a different display for negatives, combine it
      with a custom format:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Hur man använder ett anpassat talformat i Excel med C#
url: /sv/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur du använder ett anpassat talformat i Excel med C#

Om du behöver ett **anpassat talformat i Excel** som visar ett specifikt antal signifikanta siffror, visar den här guiden exakt hur du gör det i C#. Du får se hur du ställer in signifikanta siffror, skapar en Excel-arbetsbok och sparar arbetsboken som en XLSX‑fil – allt med några få kodrader.

Att arbeta med Excel‑filer programatiskt innebär ofta att du måste kontrollera hur siffror visas. Med Aspose.Cells för .NET kan du definiera ett globalt tal‑formatalternativ som tvingar varje numerisk cell att följa ett givet antal signifikanta siffror. Denna handledning täcker hela arbetsflödet, från projektuppsättning till verifiering av resultatet i Excel.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 eller senare installerat (koden fungerar också med .NET Framework 4.7.2+)
* Visual Studio 2022 eller någon annan C#‑IDE du föredrar
* **Aspose.Cells**‑NuGet‑paketet (`Install-Package Aspose.Cells`) – ett fullständigt hanterat bibliotek för Excel‑manipulation
* Grundläggande kunskaper i C#‑syntax

## Steg 1: Skapa en Excel‑arbetsbok i C#

Den första operationen är att instansiera ett nytt `Workbook`‑objekt. Detta objekt representerar hela Excel‑filen i minnet.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook wb = new Workbook();

        // The workbook now contains a default worksheet named "Sheet1"
        // You can access it via the Worksheets collection.
        Worksheet ws = wb.Worksheets[0];
```

**Varför detta är viktigt:** `Workbook` är ingångspunkten för varje Excel‑operation. Genom att skapa den först får du en ren fil som du senare kan spara som XLSX.

## Steg 2: Konfigurera talformatet för att ange signifikanta siffror

Aspose.Cells erbjuder en global inställning som heter `NumberFormatOptions`. Genom att tilldela `SignificantDigits = 4` kommer varje numerisk cell att visa upp till fyra signifikanta siffror om inte ett mer specifikt format åsidosätter det.

```csharp
        // Step 2: Set the global number‑format option to 4 significant digits
        WorkbookSettings.SetNumberFormatOptions(
            new NumberFormatOptions { SignificantDigits = 4 });
```

**Varför detta är viktigt:** Med `SetNumberFormatOptions` kan du definiera ett **anpassat talformat i Excel** utan att skriva en formatsträng för varje cell. Det motsvarar alternativet “Significant Digits” som du hittar under Excels *Format Cells → Number → Custom*-dialog.

## Steg 3: Skriv värden och verifiera det anpassade talformatet

Placera nu ett numeriskt värde i en cell. Den globala inställningen kommer automatiskt att tillämpa 4‑siffrors‑regeln.

```csharp
        // Step 3: Write a numeric value into cell A1 (row 0, column 0)
        ws.Cells[0, 0].PutValue(123.456789);

        // Optional: Add a label so you can see the effect in Excel
        ws.Cells[0, 1].PutValue("Original value:");
        ws.Cells[0, 2].PutValue(123.456789);
```

När du öppnar den sparade filen kommer cell **A1** att visa `123.5` (avrundat till fyra signifikanta siffror). Det ursprungliga värdet förblir oförändrat i den underliggande datan, vilket du kan bekräfta genom att titta i formelfältet.

**Tips för kantfall:** Om du lagrar ett mycket stort tal som `12345678.9`, kommer samma inställning att visa `1.235E+07` (vetenskaplig notation) eftersom Excel väljer den mest kompakta representationen samtidigt som fyra signifikanta siffror bevaras.

## Steg 4: Spara arbetsboken som XLSX

Till sist, skriv arbetsboken till disk. `Save`‑metoden väljer automatiskt filformatet baserat på filändelsen.

```csharp
        // Step 4: Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\SigDigits.xlsx";
        wb.Save(outputPath);

        // Inform the user
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Varför detta är viktigt:** Att spara som **XLSX** (`save workbook xlsx`) säkerställer maximal kompatibilitet med moderna versioner av Excel, Office 365 och andra kalkylbladsverktyg.

## Förväntat resultat

Öppna *C:\Temp\SigDigits.xlsx* i Microsoft Excel. Du bör se:

| A          | B               | C               |
|------------|-----------------|-----------------|
| **123.5**  | Originalvärde: | **123.456789**  |

*Cell A1* visar talet avrundat till fyra signifikanta siffror, medan *C1* behåller full precision för jämförelse.

## Vanliga variationer och hur du ställer in talformat för specifika celler

### Använda en anpassad formatsträng istället för globala alternativ

Om du behöver ett format som endast gäller för ett enda område kan du tilldela en formatsträng direkt:

```csharp
ws.Cells["D1"].PutValue(0.0012345);
Style style = wb.CreateStyle();
style.Custom = "0.####"; // shows up to 4 decimal places, not significant digits
ws.Cells["D1"].SetStyle(style);
```

### Tillämpa inställningen på en hel kolumn

```csharp
// Apply the same significant‑digit rule to column B
ws.Cells.Columns[1].ApplyNumberFormatOptions(
    new NumberFormatOptions { SignificantDigits = 4 });
```

### Hantera negativa tal

Den globala `SignificantDigits`‑inställningen fungerar enhetligt för både positiva och negativa tal. Om du vill ha en annan visning för negativa tal, kombinera den med ett anpassat format:

```csharp
Style negStyle = wb.CreateStyle();
negStyle.Custom = "#,##0.###;[Red]-#,##0.###";
ws.Cells["E1"].PutValue(-9876.54321);
ws.Cells["E1"].SetStyle(negStyle);
```

## Pro‑tips och fallgropar

* **Pro‑tips:** Ställ in tal‑formatalternativen **innan** du skriver någon data. Att ändra alternativet efter att cellerna har fyllts omformaterar inte befintliga värden retroaktivt.
* **Se upp för:** Att använda `PutValue` med en **string** som ser ut som ett tal (t.ex. `"123.45"`). Excel behandlar det som text, och det anpassade formatet tillämpas inte.
* **Prestanda‑notering:** Globala inställningar är resurssnåla, men att applicera en stil på miljontals celler kan öka minnesanvändningen. Använd kolumn‑nivåformatering när det är möjligt.

## Nästa steg

Nu när du kan **anpassa talformat i Excel** med signifikanta siffror, kan du utforska:

* **Hur du ställer in talformat** för datum och valutor med `Style.Custom`.
* **Skapa diagram** som respekterar dina anpassade format.
* **Exportera till CSV** samtidigt som du bevarar numerisk precision (`save workbook xlsx` → `wb.Save("file.csv", SaveFormat.Csv)`).

Dessa ämnen bygger vidare på samma `Workbook`‑ och `Worksheet`‑koncept som demonstrerats här.

---

**Sammanfattning**

Du har lärt dig hur du **anpassar talformat i Excel** genom att konfigurera `NumberFormatOptions` för att **ange signifikanta siffror**, skapa en Excel‑arbetsbok i C#, skriva värden och **spara arbetsboken som en XLSX‑fil**. Den kompletta, körbara koden ovan visar varje steg, förklarar varför varje del är nödvändig och ger tips för vanliga variationer. Anpassa gärna kodsnuttarna till dina egna projekt och experimentera med andra formateringsscenarier.

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Custom Number Format Excel in C# – Complete Guide](/cells/english/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/)
- [Create Excel Workbook C# – Limit Significant Digits Excel](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-c-limit-significant-digits-excel/)
- [How to apply number format excel with Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}