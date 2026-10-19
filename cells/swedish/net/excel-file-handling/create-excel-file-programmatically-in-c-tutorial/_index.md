---
category: general
date: 2026-08-11
description: Skapa en Excel‑fil programatiskt i C# med Aspose.Cells. Tolka ett datum
  i japansk era, skriv det till en cell och spara arbetsboken.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel file programmatically
- datetime.parseexact custom format
- write date to excel cell
- how to save excel file c#
language: sv
lastmod: 2026-08-11
og_description: Skapa Excel-fil programatiskt i C# med Aspose.Cells. Lär dig hur du
  parsar ett japanskt era‑datum med DateTime.ParseExact anpassat format, skriver datumet
  till en Excel‑cell och sparar arbetsboken effektivt.
og_image_alt: Screenshot of an Excel workbook with a parsed Japanese era date in cell
  A1
og_title: Skapa Excel‑fil programatiskt i C# – fullständig handledning
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel file programmatically in C# using Aspose.Cells. Parse
    a Japanese era date, write it to a cell, and save the workbook.
  headline: Create excel file programmatically in C# – tutorial
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- DateTime parsing
title: Skapa Excel‑fil programatiskt i C# – handledning
url: /sv/net/excel-file-handling/create-excel-file-programmatically-in-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel‑fil programatiskt i C# – handledning

Om du behöver **skapa Excel‑fil programatiskt** kan du göra det med några få rader C#‑kod. Denna guide visar hur du genererar en Excel‑arbetsbok med Aspose.Cells, parsar ett japanskt era‑datum med en **DateTime.ParseExact‑anpassad format**, skriver det datumet till en kalkylblads‑cell och slutligen **sparar Excel‑filen i C#‑stil**. I slutet har du en färdig *.xlsx*-fil som innehåller ett korrekt konverterat gregorianskt datum.

Du kommer att lära dig hur du:

* Initierar en arbetsbok utan en mall.  
* Konverterar en era‑baserad sträng såsom `"R3/04/01"` till en `DateTime`.  
* Infogar `DateTime`‑värdet i en specifik cell (`A1`).  
* Sparar arbetsboken till disk med ett enda `Save`‑anrop.

Inga ytterligare bibliotek utöver Aspose.Cells och .NET:s grundklassbibliotek krävs.

---

## Förutsättningar

Innan du börjar, se till att du har:

* **.NET 6.0** eller senare installerat (koden fungerar även med .NET Framework 4.6+).  
* En giltig **Aspose.Cells**‑licens eller en gratis utvärderingskopi.  
* Grundläggande kunskap om C#‑syntax och Visual Studio (eller någon IDE du föredrar).

---

## Skapa Excel‑fil programatiskt – initiera arbetsbok

Det första steget är att skapa ett tomt arbetsboksobjekt. Aspose.Cells tillhandahåller en `Workbook`‑klass som representerar en hel Excel‑fil i minnet.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();               // creates an empty .xlsx structure
        var worksheet = workbook.Worksheets[0];      // the default first sheet is named "Sheet1"
```

**Varför detta är viktigt:**  
Att skapa arbetsboken programatiskt eliminerar behovet av en fysisk mallfil, vilket håller din distributionsfotavtryck litet och låter dig generera filer i farten för rapporter, fakturor eller dataexport.

---

## Använd DateTime.ParseExact‑anpassat format för japanska era‑datum

Datumsträngar som innehåller japanska era‑symboler (t.ex. `"R"` för Reiwa) kan inte parsas med standard‑`DateTime.Parse`. Du måste ange ett **anpassat format** och en japansk kultur som känner igen era‑designatorn.

```csharp
        // Step 2: Define the era‑based date string (Reiwa 3, April 1)
        string eraDate = "R3/04/01";

        // Step 3: Create a CultureInfo that knows Japanese eras
        var japaneseCulture = new CultureInfo("ja-JP");

        // Step 4: Parse the era date using a custom format string
        //   "g"  = era designator (R, H, etc.)
        //   "yy" = two‑digit year within the era
        //   "MM" = month (01‑12)
        //   "dd" = day of month (01‑31)
        DateTime parsedDate = DateTime.ParseExact(
            eraDate,
            "ggy/MM/dd",
            japaneseCulture,
            DateTimeStyles.None);
```

**Varför detta är viktigt:**  
`DateTime.ParseExact` garanterar att indata matchar det mönster du anger, vilket förhindrar lokalt beroende tvetydigheter. Mönstret `"ggy/MM/dd"` talar om för .NET att behandla det första tecknet som en era (`g`), följt av ett tvåsiffrigt år (`yy`), månad och dag. Genom att använda `japaneseCulture` säkerställs att era‑symbolerna tolkas korrekt, vilket ger ett gregorianskt `DateTime` (`2021‑04‑01` i exemplet).

---

## Skriv datum till Excel‑cell med Aspose.Cells

När du har en `DateTime`‑instans kan du placera den i vilken kalkylblads‑cell som helst. Aspose.Cells formaterar automatiskt cellen enligt arbetsbokens standarddatumstil.

```csharp
        // Step 5: Write the DateTime value into cell A1
        worksheet.Cells["A1"].PutValue(parsedDate);

        // Optional: Apply a custom number format if you want a specific display
        worksheet.Cells["A1"].Style.Number = 14; // 14 = "m/d/yyyy" in Excel
```

**Varför detta är viktigt:**  
Genom att använda `PutValue` låter du Aspose.Cells härleda celltypen (datum, tal, text) från den .NET‑typ du tillhandahåller. Detta tillvägagångssätt är säkrare än att skriva en formaterad sträng, eftersom Excel behåller datumsemantiken—vilket möjliggör sortering, filtrering eller beräkningar på kolumnen senare.

---

## Hur man sparar Excel‑fil i C# – avslutar arbetsboken

Det sista steget är att spara den minnes‑arbetsboken till en fysisk fil. Aspose.Cells stödjer många format; här använder vi det moderna `.xlsx`‑formatet.

```csharp
        // Step 6: Save the workbook to the desired location
        string outputPath = @"C:\Temp\JapaneseEra.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Varför detta är viktigt:**  
Att anropa `Save` med `SaveFormat.Xlsx` skriver en standard‑kompatibel Office Open XML‑fil som kan öppnas i Excel, LibreOffice eller någon annan visare som stödjer formatet. Metoden hanterar också all underliggande komprimering och paketering, så du behöver inte hantera zip‑strömmar själv.

---

## Förväntat resultat

När du kör programmet:

| Cell | Värde (visning) | Underliggande typ |
|------|-----------------|-------------------|
| A1   | 4/1/2021        | Date (DateTime)   |

Filen `JapaneseEra.xlsx` kommer att innehålla ett enda blad med namnet **Sheet1** med det gregorianska datumet `2021‑04‑01` i cell **A1**. Excel kommer att behandla cellen som ett datum, vilket möjliggör vidare beräkningar såsom `=A1+30` för att lägga till 30 dagar.

---

## Vanliga variationer och kantfall

| Situation | Lösning |
|-----------|----------|
| **Olika era** (t.ex. Heisei `H30/12/31`) | Ändra inmatningssträngen; samma `"ggy/MM/dd"`‑mönster fungerar eftersom den japanska `CultureInfo` känner till alla eror. |
| **Fyrsiffrigt år** (t.ex. `"R2023/04/01`") | Använd `"ggyyyy/MM/dd"` som formatsträng. |
| **Saknad era‑symbol** | Tillhandahåll ett reservformat som `"yyyy/MM/dd"` och försök med `DateTime.TryParseExact` med flera mönster. |
| **Ogiltigt datum** (t.ex. `"R3/13/01`") | Omge `ParseExact` med ett `try/catch`‑block eller använd `DateTime.TryParseExact` för att hantera parsningsfel på ett smidigt sätt. |

**Proffstips:** Validera alltid det parsade `DateTime` innan du skriver det till kalkylbladet, särskilt när källdata kommer från användarinmatning eller externa filer.

---

## Sammanfattning

* Du **skapade Excel‑fil programatiskt** med Aspose.Cells.  
* Du parsade en japansk era‑sträng med **DateTime.ParseExact‑anpassat format**.  
* Du **skrev datum till Excel‑cell** med `PutValue`.  
* Du lärde dig **hur man sparar Excel‑fil i C#** med ett enda `Save`‑anrop.

Dessa fyra steg utgör ett återanvändbart mönster för alla scenarier där du behöver importera kultur‑specifika datum till Excel‑rapporter.

---

## Nästa steg

* Utforska **cellformatering** (typsnitt, färger, kanter) för att göra dina rapporter snygga.  
* Använd **Workbook.Save** med andra format (`Csv`, `Pdf`) för att exportera data till olika målgrupper.  
* Kombinera denna teknik med **massinmatning av data** (`Cells.ImportDataTable`) för storskaliga import.

Känn dig fri att experimentera med olika era‑symboler, anpassade talformat eller flera kalkylblad. Samma grundlogik—skapa, pars, skriv, spara—gäller för alla Excel‑automatiseringsuppgifter i C#.

---

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man skapar och sparar en Excel‑arbetsbok som ODS med Aspose.Cells för .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Hur man sparar specifika sidor i en Excel‑fil som PDF med Aspose.Cells för .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Hur man skapar och sparar en Excel‑arbetsbok som SVG med Aspose.Cells för Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}