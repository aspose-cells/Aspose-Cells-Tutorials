---
category: general
date: 2026-02-21
description: Spara Excel som txt med exakt kontroll över signifikanta siffror. Exportera
  Excel till txt i C# och ange signifikanta siffror enkelt.
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: sv
og_description: Spara Excel som txt snabbt. Lär dig hur du exporterar Excel till txt,
  anger signifikanta siffror och styr textutmatning med C#.
og_title: Spara Excel som txt – Exportera tal med signifikanta siffror i C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Spara Excel som txt – Komplett C#‑guide för att exportera tal med signifikanta
  siffror
url: /sv/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spara Excel som txt – Komplett C#‑guide för att exportera tal med signifikanta siffror

Har du någonsin behövt **spara Excel som txt** men oroat dig för att siffrorna skulle förlora sin precision? Du är inte ensam. Många utvecklare fastnar när de försöker exportera Excel till txt och får antingen för många decimaler eller ett avrundat kaos.  

I den här handledningen visar vi dig ett enkelt sätt att **exportera Excel till txt** samtidigt som du **anger signifikanta siffror** så att resultatet ser exakt ut som du vill. När du är klar har du ett färdigt C#‑exempel som sparar en arbetsbok som text, exporterar tal till txt och ger dig full kontroll över talformatet.

## Vad du kommer att lära dig

- Hur du skapar en ny arbetsbok och skriver numerisk data.
- Det korrekta sättet att **ange signifikanta siffror** med `TxtSaveOptions`.
- Hur du **sparar arbetsboken som text** och verifierar resultatet.
- Hantering av kantfall (stora tal, negativa värden, lokala problem).
- Snabba tips för att finjustera utskriften ytterligare (ändra avgränsare, kodning).

### Förutsättningar

- .NET 6.0 eller senare (koden fungerar även på .NET Framework 4.6+).
- **Aspose.Cells**‑NuGet‑paketet (`Install-Package Aspose.Cells`).
- Grundläggande förståelse för C#‑syntax – ingen djup Excel‑interop‑kunskap krävs.

> **Proffstips:** Om du använder Visual Studio, aktivera *nullable reference types* (`<Nullable>enable</Nullable>`) för att fånga potentiella null‑buggar tidigt.

---

## Steg 1: Initiera arbetsboken och skriv ett tal

Först behöver vi ett arbetsboksobjekt. Tänk på det som den minnesbaserade representationen av en Excel‑fil.  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**Varför detta är viktigt:**  
Att skapa arbetsboken programatiskt undviker COM‑interop‑overhead, och `PutValue` upptäcker automatiskt datatypen, så att cellen behandlas som ett tal – inte en sträng.

---

## Steg 2: Konfigurera TxtSaveOptions för att styra signifikanta siffror

Klassen `TxtSaveOptions` är där magin händer. Genom att sätta `SignificantDigits` talar du om för Aspose.Cells hur många meningsfulla siffror som ska behållas när filen skrivs ut.

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**Varför du bör sätta detta:**  
När du **exporterar tal till txt** behöver du ofta en koncis representation (t.ex. för rapporteringssystem som bara accepterar en viss precision). `SignificantDigits`‑egenskapen garanterar enhetlig avrundning oavsett det ursprungliga talets längd.

---

## Steg 3: Spara arbetsboken som en textfil

Nu skriver vi arbetsboken till disk med de alternativ vi just definierat.

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**Vad du kommer att se:**  
Öppna `Numbers.txt` så får du en enda rad:

```
12350
```

Det ursprungliga `12345.6789` har avrundats till **fyra signifikanta siffror**, exakt som begärt.

---

## Steg 4: Verifiera resultatet (valfritt men rekommenderat)

Automatiska tester är en bra vana. Här är en snabb kontroll du kan köra direkt efter sparandet:

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

När du kör detta block skrivs en grön bock ut om allt stämmer, vilket ger dig förtroende för att **spara excel som txt**‑operationen fungerade som avsett.

---

## Vanliga varianter & kantfall

### Exportera flera celler eller områden

Om du behöver **exportera excel till txt** för ett helt område, fyll bara i fler celler innan du sparar:

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

Samma `TxtSaveOptions` kommer att tillämpa 4‑siffrig regel på varje värde och producera:

```
12350
0.0001235
-98800
```

### Ändra avgränsare

Vissa nedströmsystem förväntar sig tab‑separerade värden. Ändra avgränsaren så här:

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

Nu separeras varje cell i en rad med ett tab‑tecken.

### Hantera lokalspecifika decimalavgränsare

Om din målgrupp använder kommatecken för decimaler, sätt kulturen:

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

Utskriften kommer att respektera lokalen och omvandla `12350` till `12 350` (mellanslag som tusentalsavgränsare i franska).

---

## Fullt fungerande exempel (Kopiera‑klistra‑klart)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**Förväntat innehåll i `Numbers.txt` (standardavgränsare, 4 signifikanta siffror):**

```
12350	0.0001235	-98800
```

Tab‑tecknet (`\t`) visas eftersom vi behöll standardavgränsaren (tab) i exemplet; ändra det till ett komma om du föredrar CSV.

---

## Slutsats

Du vet nu exakt **hur du sparar Excel som txt** samtidigt som du styr antalet signifikanta siffror. Stegen – skapa en arbetsbok, sätt `TxtSaveOptions.SignificantDigits` och spara – är allt du behöver för att **exportera excel till txt** på ett pålitligt sätt.  

Härifrån kan du:

- **Exportera tal till txt** för större dataset.
- Finjustera avgränsare, kodning eller kulturinställningar för att matcha vilket nedströmsystem som helst.
- Kombinera detta tillvägagångssätt med andra Aspose.Cells‑funktioner (format, formler) innan export.

Prova, justera `SignificantDigits` till 2 eller 6, och se hur utskriften förändras. Flexibiliteten i **spara arbetsbok som text** gör den till ett praktiskt verktyg i alla data‑utbytespipeline.

---

### Relaterade ämnen du kanske vill utforska härnäst

- **Exportera Excel till CSV** med anpassad kolumnordning.
- **Läsa txt‑filer tillbaka till en arbetsbok** (`Workbook.Load` med `LoadOptions`).
- **Batch‑behandling** av flera kalkylblad och konsolidering till en txt‑fil.
- **Prestandaoptimering** för storskaliga exporter (streaming vs. minne).

Känn dig fri att lämna en kommentar om du stöter på problem, eller dela hur du har anpassat exporten för dina egna projekt. Lycka till med kodningen!  

---  

*Bild: En skärmdump av den genererade `Numbers.txt`‑filen som visar avrundade värden.*  
*Alt‑text: “Numbers.txt‑fil som visar 12350, 0.0001235 och -98800 efter att ha sparat Excel som txt med 4 signifikanta siffror.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}