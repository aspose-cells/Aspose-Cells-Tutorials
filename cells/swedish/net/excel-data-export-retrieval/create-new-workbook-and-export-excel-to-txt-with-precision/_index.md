---
category: general
date: 2026-02-15
description: Skapa en ny arbetsbok och exportera Excel till TXT samtidigt som du ställer
  in numerisk precision. Lär dig att ange signifikanta siffror och begränsa signifikanta
  siffror i C#.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: sv
og_description: Skapa en ny arbetsbok och exportera Excel till TXT, med inställning
  av signifikanta siffror för numerisk precision. En steg‑för‑steg C#‑guide.
og_title: Skapa ny arbetsbok – Exportera Excel till TXT med precision
tags:
- C#
- Aspose.Cells
- Excel automation
title: Skapa ny arbetsbok och exportera Excel till TXT med precision
url: /sv/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ny arbetsbok – Exportera Excel till TXT med exakt numerisk formatering

Har du någonsin funderat på hur man **skapar ny arbetsbok**‑objekt i C# och omedelbart sparar dem till en ren textfil? Du är inte ensam. I många datapipeline‑scenarier behöver vi **exportera Excel till TXT** samtidigt som siffrorna förblir läsbara, vilket innebär att begränsa antalet siffror efter decimaltecknet.  

I den här handledningen går vi igenom hela processen: från att skapa en ny arbetsbok, till att konfigurera exporten så att den **sätter signifikanta siffror** (dvs. begränsar signifikanta siffror), och slutligen skriva filen till disk. När du är klar har du ett färdigt kodexempel som respekterar dina **numeriska precision**‑krav—utan extra bibliotek, utan magi.

> **Pro tip:** Om du redan använder Aspose.Cells är klasserna nedan en del av det biblioteket. Om du är på en annan plattform gäller koncepten fortfarande; byt bara ut API‑anropen.

---

## Vad du behöver

- .NET 6+ (koden kompileras på .NET Core och .NET Framework lika väl)  
- Aspose.Cells för .NET (gratis provversion eller licensierad version) – installera via NuGet: `dotnet add package Aspose.Cells`  
- Valfri IDE (Visual Studio, Rider, VS Code)  

Det är allt. Inga extra konfigurationsfiler, inga dolda steg.

---

## Steg 1: Skapa en ny arbetsbok

Det allra första är att **skapa ny arbetsbok**. Tänk på `Workbook`‑klassen som en tom Excel‑fil som väntar på blad, celler och data.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Varför detta är viktigt:** Genom att börja med en ren arbetsbok undviker du dold formatering som kan störa precision‑inställningarna senare.

---

## Steg 2: Konfigurera Text‑spara‑alternativ – Sätt signifikanta siffror

Nu talar vi om för Aspose.Cells hur många **signifikanta siffror** vi vill ha när vi skriver till en `.txt`‑fil. Klassen `TxtSaveOptions` har en egenskap `SignificantDigits` som gör exakt det.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Förklaring:** `SignificantDigits = 5` betyder att exportören behåller de fem viktigaste siffrorna i varje tal, oavsett var decimaltecknet ligger. Det är ett smidigt sätt att **sätta numerisk precision** utan att manuellt formatera varje cell.

---

## Steg 3: Spara arbetsboken som en ren textfil

Med arbetsboken och alternativen klara, **exporterar vi Excel till txt**. Metoden `Save` tar filvägen och alternativ‑objektet vi just konfigurerat.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

När programmet körs får du en fil som ser ut så här:

```
12346
0.00012346
3.1416
```

Lägg märke till hur varje tal följer regeln **begränsa signifikanta siffror** som vi satte tidigare.

---

## Steg 4: Verifiera resultatet (valfritt men rekommenderat)

Det är enkelt att öppna den genererade `numbers.txt` i vilken editor som helst, men du kanske vill automatisera verifieringssteget, särskilt i CI‑pipelines.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

Om konsolen visar de tre raderna ovan har du lyckats **sätta signifikanta siffror** och exporten fungerar som den ska.

---

## Vanliga fallgropar & hur du undviker dem

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| Tal visas med för många decimaler | `SignificantDigits` lämnades på standardvärdet (0) | Sätt explicit `SignificantDigits` till önskat antal |
| Tom fil skapas | Arbetsboken fick ingen data innan den sparades | Fyll i celler **innan** du anropar `Save` |
| Filvägen kastar `UnauthorizedAccessException` | Försök att skriva till en skyddad mapp | Använd en mapp du har skrivbehörighet till (t.ex. `C:\Temp` eller `%USERPROFILE%\Documents`) |
| Precisionen verkar fel för mycket små tal | Antalet signifikanta siffror inkluderar ledande nollor efter decimalen | Kom ihåg att “signifikant” ignorerar ledande nollor; 0.000123456 med 5 siffror blir `0.00012346` |

---

## Fullt fungerande exempel (Kopiera‑klistra‑klart)

Nedan är det kompletta, självständiga programmet. Klistra in det i ett nytt konsolprojekt och kör **Run**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Förväntad konsolutskrift**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

Och filen `numbers.txt` kommer att innehålla de tre rader som visas ovan.

---

## Nästa steg: Gå längre än grunderna

- **Exportera andra format** – Aspose.Cells stödjer även CSV, HTML och PDF. Byt ut `TxtSaveOptions` mot `CsvSaveOptions` eller `PdfSaveOptions` efter behov.  
- **Dynamisk precision** – du kan beräkna `SignificantDigits` vid körning baserat på användarinput eller konfigurationsfiler.  
- **Flera arbetsblad** – iterera över `workbook.Worksheets` och exportera varje blad till sin egen `.txt`‑fil.  
- **Lokalisering** – styr decimalseparatorn (`.` vs `,`) via `CultureInfo` om du behöver anpassa till regionala inställningar.  

Alla dessa tillägg bygger fortfarande på kärnidén vi gick igenom: **skapa ny arbetsbok**, konfigurera exporten, och **sätt numerisk precision** för att matcha dina rapporteringskrav.

---

## Sammanfattning

Vi har tagit en ny **skapa ny arbetsbok**‑instans, fyllt den med data, och demonstrerat hur man **exporterar Excel till TXT** samtidigt som man **sätter signifikanta siffror** för att begränsa utskriftens precision. Exemplet körs direkt, och förklaringen täckte *varför* varje rad finns så att du kan anpassa det till dina egna projekt.

Känn dig fri att experimentera—ändra värdet på `SignificantDigits`, lägg till fler blad, eller byt ut utdataformatet. Om du stöter på problem, kolla Aspose.Cells‑dokumentationen eller lämna en kommentar nedan. Lycka till med kodandet!

---

![Create new workbook example](/images/create-new-workbook.png "Screenshot showing a C# IDE with the create new workbook code")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}