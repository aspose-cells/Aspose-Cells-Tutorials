---
category: general
date: 2026-03-18
description: Maak een nieuw werkboek en exporteer Excel naar TXT terwijl je de numerieke
  precisie behoudt. Leer hoe je een werkblad als txt opslaat en een werkblad efficiënt
  naar txt converteert.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: nl
og_description: Maak een nieuwe werkmap en exporteer Excel naar TXT met precisie.
  Deze tutorial laat zien hoe je een werkblad opslaat als txt en een werkblad converteert
  naar txt met C#.
og_title: Nieuw werkboek maken – Excel naar TXT exportgids
tags:
- Aspose.Cells
- C#
- Excel automation
title: Nieuw werkboek aanmaken – Excel exporteren naar TXT met volledige precisie
url: /nl/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nieuw werkboek maken – Export Excel naar TXT met volledige precisie

Heb je ooit **create new workbook** in C# nodig gehad alleen om wat gegevens in een platte‑tekstbestand te dumpen? Misschien haal je een rapport uit een legacy‑systeem en accepteert de downstream‑tool alleen een `.txt`‑feed. Het goede nieuws? Je hoeft geen numerieke precisie op te offeren, en je hoeft zeker geen CSV‑strings handmatig te maken.

In deze gids lopen we het volledige proces van **export excel to txt** door, van het initialiseren van het werkboek tot het behouden van de volgende nullen wanneer je **save worksheet as txt**. Aan het einde heb je een kant‑klaar fragment dat je in elk .NET‑project kunt plaatsen—geen extra hulpprogramma's nodig.

## Wat je nodig hebt

- **ASP.NET/ .NET 6+** (de code werkt ook op .NET Framework 4.6+)  
- **Aspose.Cells for .NET** – de bibliotheek die de `Workbook`, `Worksheet` en `TxtSaveOptions` klassen aandrijft. Je kunt het ophalen van NuGet met `Install-Package Aspose.Cells`.  
- Een basisbegrip van C# (als je vertrouwd bent met `using` statements, ben je klaar om te gaan).  

Dat is alles—geen Excel‑interop, geen COM‑objecten, en zeker geen handmatige tekenreeks‑concatenatie.

---

## Stap 1: Een nieuw werkboek initialiseren (Primaire trefwoord)

Het eerste wat je moet doen is **create new workbook**. Beschouw het werkboek als het lege canvas waarop je later cijfers, tekst of formules plakt.

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

> **Waarom dit belangrijk is:** Het instantieren van `Workbook` zonder een bestand te laden geeft je een schone lei. Je kunt vervolgens data programmatisch toevoegen, wat perfect is voor **convert worksheet to txt** scenario's waarin je geen bestaande `.xlsx` hebt.

## Stap 2: Cellen vullen – Houd die volgende nullen

Een veelvoorkomende valkuil bij het dumpen van cijfers naar tekst is het verliezen van volgende nullen (`123.45000` wordt `123.45`). Als downstream‑systemen afhankelijk zijn van vaste‑breedte velden, kan dat verlies alles breken.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Pro tip:** `PutValue` bepaalt automatisch het gegevenstype. Als je een tekenreeks nodig hebt die eruitziet als een getal, gebruik dan `PutValue("123.45000")` in plaats daarvan.

## Stap 3: TXT‑opslaan‑opties configureren – Numerieke precisie behouden

Hier gebeurt de magie. Door `PreserveNumericPrecision` in te schakelen, instrueer je Aspose.Cells om de exacte waarde die je hebt ingevoerd te schrijven, inclusief eventuele onbeduidende volgende nullen.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **Waarom dit inschakelen?** Wanneer je **save excel as txt**, verwijdert het standaardgedrag onnodige decimalen. Het instellen van `PreserveNumericPrecision = true` garandeert dat de output de weergegeven celwaarde weerspiegelt, wat cruciaal is voor financiële rapporten of wetenschappelijke data.

## Stap 4: Het werkblad opslaan als TXT – De uiteindelijke export

Nu slaan we daadwerkelijk **save worksheet as txt** op. Je kunt het pad overal aanwijzen waar je schrijfrechten hebt; het voorbeeld gebruikt een relatieve map genaamd `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Verwachte output** (`num-preserve.txt`):

```
123.45000
```

Merk op dat de volgende nullen intact zijn—precies wat je vroeg.

## Stap 5: Resultaat verifiëren – Snelle sanity‑check

Nadat het programma is uitgevoerd, open `num-preserve.txt` in een teksteditor. Je zou de enkele regel `123.45000` moeten zien. Als je in plaats daarvan `123.45` ziet, controleer dan dubbel of `PreserveNumericPrecision` op `true` staat en dat je een recente versie van Aspose.Cells gebruikt (v23.10+).

## Veelvoorkomende variaties & randgevallen

### Meerdere cellen of bereiken exporteren

Als je **export excel to txt** voor een heel bereik nodig hebt, vul dan simpelweg meer cellen voordat je opslaat:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose schrijft standaard elke cel op een nieuwe regel. Je kunt ook de scheidingsteken (tab, komma) wijzigen via `txtSaveOptions.Separator`.

### Werkblad converteren naar TXT met verschillende coderingen

Soms vereisen downstream‑systemen UTF‑8 BOM of ASCII. Pas de codering als volgt aan:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Grote werkboeken verwerken

Bij het omgaan met enorme bladen (honderdduizenden rijen), overweeg het streamen van de output:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

## Pro‑tips & valkuilen

- **Vergeet niet de output‑map te maken** voordat je `Save` aanroept, anders krijg je een `DirectoryNotFoundException`.  
- **Let op locale‑specifieke decimale scheidingstekens**. Als je omgeving komma’s gebruikt (`1,23`), stel `txtSaveOptions.DecimalSeparator = '.'` in om een punt af te dwingen.  
- **Versie‑compatibiliteit**: De `PreserveNumericPrecision`‑vlag werd geïntroduceerd in Aspose.Cells 20.6. Als je een oudere versie gebruikt, bestaat de vlag niet en moet je de cel als tekst formatteren vóór het opslaan.

![Voorbeeld nieuw werkboek](excel-to-txt.png "Nieuw werkboek")

*Afbeeldings‑alt‑tekst: "Nieuw werkboek maken en Excel exporteren naar TXT met behoud van numerieke precisie"*

## Samenvatting – Wat we hebben behandeld

- **Create new workbook** gebruiken met Aspose.Cells.  
- Een cel vullen met een getal dat volgende nullen bevat.  
- `TxtSaveOptions.PreserveNumericPrecision = true` instellen om **save excel as txt** uit te voeren zonder precisie te verliezen.  
- Het bestand naar schijf schrijven en verifiëren dat de output overeenkomt met de oorspronkelijke waarde.

## Volgende stappen & gerelateerde onderwerpen

Nu je **export excel to txt** met perfecte precisie kunt, wil je misschien het volgende verkennen:

- **Exporteren naar CSV** met aangepaste scheidingstekens (`TxtSaveOptions.Separator`).  
- **Opslaan als andere platte‑tekstformaten** zoals TSV (`SaveFormat.TabDelimited`).  
- **Batchverwerking** van meerdere werkboeken in een map met `Directory.GetFiles`.  
- **Integreren met Azure Functions** voor on‑demand conversie in de cloud.

Elk van deze bouwt voort op hetzelfde `Workbook` → `Worksheet` → `TxtSaveOptions`‑patroon, dus je voelt je meteen thuis.

### Laatste gedachte

Als je hebt gevolgd, weet je nu precies hoe je **create new workbook**, het kunt vullen, en **save worksheet as txt** terwijl je elke decimale cijfer behoudt die je nodig hebt. Het is een klein stukje code, maar het lost een verrassend veelvoorkomend probleem op wanneer legacy‑pijplijnen platte‑tekst invoer eisen.

Probeer het, pas de opties aan, en laat de data precies op de gewenste manier stromen. Veel programmeerplezier!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}