---
category: general
date: 2026-01-14
description: Exportera tabell till CSV i C# och lär dig hur du ställer in anpassat
  talformat, skriver CSV till fil och aktiverar automatisk beräkning – allt i en tutorial.
draft: false
keywords:
- export table to csv
- set custom number format
- write csv to file
- enable automatic calculation
- how to format numbers
language: sv
og_description: Exportera tabell till CSV med anpassade talformat, skriv CSV till
  fil och aktivera automatisk beräkning med Aspose.Cells i C#.
og_title: Exportera tabell till CSV – Fullständig C#‑genomgång
tags:
- Aspose.Cells
- C#
- CSV export
- Excel automation
title: Exportera tabell till CSV – Komplett C#‑guide med anpassade talformat
url: /sv/net/csv-file-handling/export-table-to-csv-complete-c-guide-with-custom-number-form/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera tabell till CSV – Komplett C#‑guide med anpassade talformat

Har du någonsin behövt **exportera tabell till CSV** men varit osäker på hur du får siffrorna att se prydliga ut? Du är inte ensam. I många data‑export‑scenarier vill du ha siffrorna formaterade snyggt, CSV‑filen skriven till disk och arbetsboken hålls i synk med eventuella formler. Den här handledningen visar exakt **hur du exporterar tabell till CSV**, hur du **ställer in ett anpassat talformat**, hur du **skriver CSV till fil** och hur du **aktiverar automatisk beräkning** så att allt förblir uppdaterat.

Vi går igenom ett verkligt exempel med Aspose.Cells för .NET. När du är klar har du ett komplett, körbart C#‑program som:

* Formaterar en cell med ett anpassat numeriskt mönster (delen “hur man formaterar tal”).
* Exporterar den första arbetsbladstabellen till en CSV‑sträng med en avgränsare du väljer.
* Sparar den CSV‑strängen till en fil på disk.
* Tolkar ett japanskt era‑datum och skriver tillbaka det till bladet.
* Slår på automatisk beräkning så dynamiska‑array‑formler alltid räknas om.

Inga externa referenser behövs – bara kopiera, klistra in och kör.

![Export table to CSV illustration](export-table-to-csv.png "Exportera tabell till CSV-diagram"){: alt="Exportera tabell till CSV-diagram som visar arbetsbok, tabell och CSV-utdata"}

---

## Vad du behöver

* **Aspose.Cells för .NET** (NuGet‑paket `Aspose.Cells`). Koden fungerar med version 23.9 eller senare.
* En .NET‑utvecklingsmiljö (Visual Studio, Rider eller `dotnet CLI`).
* Grundläggande kunskap om C#‑syntax – inget avancerat, bara vanliga `using`‑satser och `Main`‑metoden.

---

## Steg 1 – Ställ in anpassat talformat (Hur man formaterar tal)

Innan vi exporterar någonting, låt oss se till att siffrorna visas som vi vill. `Custom`‑egenskapen på ett `Style`‑objekt låter dig definiera ett mönster som `"0.####"` för att visa upp till fyra decimaler och samtidigt ta bort onödiga nollor.

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Put a raw double value into cell A1
        worksheet.Cells[0, 0].PutValue(123.456789);

        // 3️⃣ Define a custom number format – this is the “how to format numbers” piece
        Style numberStyle = workbook.CreateStyle();
        numberStyle.Custom = "0.####"; // up to 4 significant digits
        worksheet.Cells[0, 0].SetStyle(numberStyle);
```

**Varför detta är viktigt:**  
När du senare exporterar tabellen till CSV skulle det råa `double`‑värdet `123.456789` visas som `123.456789`. Med det anpassade formatet blir CSV‑filen `123.4568` (avrundat till fyra decimaler) – exakt vad de flesta rapportverktyg förväntar sig.

---

## Steg 2 – Exportera tabell till CSV (Huvudmålet)

Aspose.Cells behandlar ett dataområde som en `Table`. Även om du inte explicit har skapat en, innehåller alltid det första arbetsbladet en standardtabell på index 0. Att exportera den tabellen är en endaste rad när du har dina `ExportTableOptions` konfigurerade.

```csharp
        // 4️⃣ Grab the first table in the worksheet
        Table firstTable = worksheet.Tables[0];

        // 5️⃣ Configure export options – we want a CSV string, comma‑delimited
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            Delimiter = ","
        };

        // 6️⃣ Export to a CSV string
        string csvContent = firstTable.ExportToString(exportOptions);

        // Show what we got (optional debug output)
        Console.WriteLine("=== CSV CONTENT ===");
        Console.WriteLine(csvContent);
```

**Förväntad CSV‑utdata** (givet det anpassade formatet från Steg 1):

```
123.4568
```

Lägg märke till hur siffran följer mönstret `"0.####"` som vi satte tidigare. Det är magin med **exportera tabell till CSV** kombinerat med ett anpassat numeriskt format.

---

## Steg 3 – Skriv CSV till fil (Spara data)

Nu när vi har en CSV‑sträng måste vi spara den. Metoden `File.WriteAllText` gör jobbet, och vi kan placera filen var vi vill – ersätt bara `"YOUR_DIRECTORY"` med en riktig sökväg.

```csharp
        // 7️⃣ Define where to save the CSV file
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "table.csv");

        // 8️⃣ Write the CSV string to disk – this is the “write csv to file” step
        File.WriteAllText(outputPath, csvContent);
        Console.WriteLine($"CSV file written to: {outputPath}");
```

**Tips:** Om du behöver en annan avgränsare (semikolon, tabb, pipe) ändrar du bara `Delimiter` i `ExportTableOptions`. Resten av koden förblir densamma, vilket gör det enkelt att anpassa.

---

## Steg 4 – Tolka ett japanskt era‑datum (Extra kul)

Ofta måste du hantera lokalspecifika datum. Aspose.Cells levereras med en `DateTimeParser` som förstår japanska era‑strängar som `"R02/04/01"` (Reiwa 2 = 2020). Låt oss lägga in det datumet i nästa rad.

```csharp
        // 9️⃣ Set up a parser for Japanese‑era dates
        DateTimeParser eraParser = new DateTimeParser { Calendar = CalendarType.JapaneseEra };
        DateTime reiwaDate = eraParser.Parse("R02/04/01"); // 2020‑04‑01

        // 10️⃣ Write the parsed date into cell A2
        worksheet.Cells[1, 0].PutValue(reiwaDate);
```

Cellen innehåller nu ett riktigt `DateTime`‑värde, som Excel (eller någon annan visare) kommer att visa enligt arbetsbokens regionala inställningar.

---

## Steg 5 – Aktivera automatisk beräkning (Håll formler uppdaterade)

Om din arbetsbok innehåller formler – särskilt dynamiska‑array‑formler – vill du att de räknas om automatiskt efter att vi ändrat data. Att byta beräkningsläge är en enkel egenskapsändring.

```csharp
        // 11️⃣ Turn on automatic calculation so formulas stay up‑to‑date
        workbook.Settings.CalcMode = CalculationMode.Automatic;

        // 12️⃣ Force a calculation pass (optional but ensures everything is up‑to‑date now)
        workbook.CalculateFormula();

        // Cleanup: save the workbook if you want to inspect it later
        string xlsPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "demo.xlsx");
        workbook.Save(xlsPath);
        Console.WriteLine($"Workbook saved to: {xlsPath}");
    }
}
```

**Varför aktivera automatisk beräkning?**  
När du senare öppnar `demo.xlsx` i Excel kommer alla formler som refererar till det anpassade talet eller det japanska era‑datumet redan att visa de senaste värdena. Detta är delen “aktivera automatisk beräkning” i vår handledning.

---

## Fullt fungerande exempel (Alla steg tillsammans)

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet. Inga delar saknas; kör det bara så ser du konsolutdata och filer dyka upp på ditt skrivbord.

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Set a number with a custom format (how to format numbers)
        worksheet.Cells[0, 0].PutValue(123.456789);
        Style numberStyle = workbook.CreateStyle();
        numberStyle.Custom = "0.####";
        worksheet.Cells[0, 0].SetStyle(numberStyle);

        // Export the first table to CSV (export table to csv)
        Table firstTable = worksheet.Tables[0];
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            Delimiter = ","
        };
        string csvContent = firstTable.ExportToString(exportOptions);
        Console.WriteLine("=== CSV CONTENT ===");
        Console.WriteLine(csvContent);

        // Write CSV to file (write csv to file)
        string csvPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "table.csv");
        File.WriteAllText(csvPath, csvContent);
        Console.WriteLine($"CSV file written to: {csvPath}");

        // Parse a Japanese‑era date and write it to the sheet
        DateTimeParser eraParser = new DateTimeParser { Calendar = CalendarType.JapaneseEra };
        DateTime reiwaDate = eraParser.Parse("R02/04/01");
        worksheet.Cells[1, 0].PutValue(reiwaDate);

        // Enable automatic calculation (enable automatic calculation)
        workbook.Settings.CalcMode = CalculationMode.Automatic;
        workbook.CalculateFormula();

        // Save the workbook for inspection
        string xlsPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "demo.xlsx");
        workbook.Save(xlsPath);
        Console.WriteLine($"Workbook saved to: {xlsPath}");
    }
}
```

**Resultat‑checklista**

| ✅ | Vad du bör se |
|---|----------------------|
| CSV‑fil `table.csv` på ditt skrivbord som innehåller `123.4568` |
| Excel‑fil `demo.xlsx` på ditt skrivbord med det anpassade talet i A1 och det japanska era‑datumet (2020‑04‑01) i A2 |
| Konsolutdata som bekräftar varje steg |

---

## Vanliga frågor & kantfall

**Q: Vad händer om min tabell har rubriker?**  
A: `ExportTableOptions` respekterar tabellens `ShowHeaders`‑egenskap. Sätt `firstTable.ShowHeaders = true;` innan du exporterar, så inkluderas rubrikraden automatiskt i CSV‑filen.

**Q: Kan jag exportera flera tabeller på en gång?**  
A: Absolut. Loopa igenom `worksheet.Tables` och slå ihop CSV‑strängarna, eller spara varje till en separat fil. Kom ihåg att justera `Delimiter` om du behöver en annan separator per fil.

**Q: Mina siffror behöver en tusentalsseparator (t.ex. `1,234.56`).**  
A: Ändra det anpassade formatet till `"#,##0.##"` så kommer den exporterade CSV‑filen att innehålla kommatecken. Tänk på att vissa CSV‑tolkare behandlar kommatecken som avgränsare, så du kan byta till ett semikolon (`Delimiter = ";"`) för att undvika förvirring.

**Q: Jag siktar på .NET 6 – några kompatibilitetsproblem?**  
A: Nej. Aspose.Cells 23.9+ riktar sig mot .NET Standard 2.0+, så det fungerar bra med .NET 6, .NET 7 och även .NET Framework 4.8.

---

## Sammanfattning

Vi har gått igenom hur du **exporterar tabell till CSV** samtidigt som du bevarar ett **anpassat talformat**, hur du **skriver CSV till fil**, och hur du **aktiverar automatisk beräkning** så att din arbetsbok hålls i synk. Vi har dessutom snabbt demonstrerat hur du tolkar ett japanskt era‑datum.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}