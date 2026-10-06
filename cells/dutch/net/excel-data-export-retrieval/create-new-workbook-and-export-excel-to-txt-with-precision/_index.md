---
category: general
date: 2026-02-15
description: Maak een nieuw werkboek en exporteer Excel naar TXT terwijl je de numerieke
  precisie instelt. Leer hoe je significante cijfers instelt en het aantal significante
  cijfers beperkt in C#.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: nl
og_description: Maak een nieuw werkboek en exporteer Excel naar TXT, waarbij je het
  aantal significante cijfers voor numerieke precisie instelt. Een stapsgewijze C#‑handleiding.
og_title: Nieuw Werkboek Maken – Exporteer Excel naar TXT met Precisie
tags:
- C#
- Aspose.Cells
- Excel automation
title: Maak nieuw werkboek en exporteer Excel naar TXT met precisie
url: /nl/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak nieuw werkboek – Exporteer Excel naar TXT met precieze numerieke opmaak

Heb je je ooit afgevraagd hoe je **nieuw werkboek** objecten in C# kunt **maken** en direct kunt wegschrijven naar een platte‑tekst‑bestand? Je bent niet de enige. In veel data‑pipeline‑scenario’s moeten we **Excel naar TXT exporteren** terwijl we cijfers leesbaar houden, wat betekent dat we het aantal cijfers achter de decimale komma moeten beperken.  

In deze tutorial lopen we het volledige proces door: van het aanmaken van een nieuw werkboek, tot het configureren van de export zodat deze **significante cijfers instelt** (oftewel het beperken van significante cijfers), en uiteindelijk het schrijven van het bestand naar schijf. Aan het einde heb je een kant‑klaar code‑fragment dat voldoet aan je **numerieke precisie**‑eisen—zonder extra libraries, zonder magie.

> **Pro tip:** Als je al Aspose.Cells gebruikt, maken de hieronder getoonde klassen deel uit van die bibliotheek. Als je op een ander platform werkt, blijven de concepten van toepassing; vervang gewoon de API‑aanroepen.

---

## Wat je nodig hebt

- .NET 6+ (de code compileert zowel op .NET Core als .NET Framework)  
- Aspose.Cells voor .NET (gratis proefversie of gelicentieerde versie) – installeren via NuGet: `dotnet add package Aspose.Cells`  
- Elke IDE die je wilt (Visual Studio, Rider, VS Code)  

Dat is alles. Geen extra configuratiebestanden, geen verborgen stappen.

---

## Stap 1: Maak een nieuw werkboek

Het allereerste wat je moet doen is **een nieuw werkboek maken**. Beschouw de `Workbook`‑klasse als een leeg Excel‑bestand dat wacht op bladen, cellen en data.

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

> **Waarom dit belangrijk is:** Door te beginnen met een schoon werkboek vermijd je verborgen opmaak die later de precisie‑instellingen kan verstoren.

---

## Stap 2: Configureer tekst‑opslaan‑opties – Stel significante cijfers in

Nu vertellen we Aspose.Cells hoeveel **significante cijfers** we willen wanneer we naar een `.txt`‑bestand schrijven. De `TxtSaveOptions`‑klasse biedt een `SignificantDigits`‑eigenschap die precies dat doet.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Uitleg:** `SignificantDigits = 5` betekent dat de exporter de vijf belangrijkste cijfers van elk getal behoudt, ongeacht waar de decimale komma staat. Het is een handige manier om **numerieke precisie** in te stellen zonder elke cel handmatig te formatteren.

---

## Stap 3: Sla het werkboek op als een platte‑tekst‑bestand

Met het werkboek en de opties klaar, **exporteren we Excel naar txt**. De `Save`‑methode neemt het bestandspad en het opties‑object dat we zojuist hebben geconfigureerd.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

Het uitvoeren van het programma levert een bestand op dat er zo uitziet:

```
12346
0.00012346
3.1416
```

Let op hoe elk getal de **limiet voor significante cijfers** die we eerder hebben ingesteld respecteert.

---

## Stap 4: Controleer het resultaat (optioneel maar aanbevolen)

Het is eenvoudig om het gegenereerde `numbers.txt` in elke editor te openen, maar je wilt misschien de controle‑stap automatiseren, vooral in CI‑pipelines.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

Als de console de drie regels hierboven toont, heb je met succes **significante cijfers ingesteld** en werkt de export zoals bedoeld.

---

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| Getallen verschijnen met te veel decimalen | `SignificantDigits` bleef op de standaardwaarde (0) | Stel `SignificantDigits` expliciet in op het gewenste aantal |
| Leeg bestand wordt aangemaakt | Werkboek kreeg geen data voordat het werd opgeslagen | Vul cellen **vóór** het aanroepen van `Save` |
| Bestandspad geeft `UnauthorizedAccessException` | Proberen te schrijven naar een beschermde map | Gebruik een map waarvoor je schrijfrechten hebt (bijv. `C:\Temp` of `%USERPROFILE%\Documents`) |
| Precisie lijkt onjuist voor zeer kleine getallen | Het aantal significante cijfers omvat leidende nullen na de komma | Onthoud dat “significant” leidende nullen negeert; 0.000123456 met 5 cijfers wordt `0.00012346` |

---

## Volledig werkend voorbeeld (Klaar om te kopiëren)

Hieronder staat het complete, zelfstandige programma. Plak het in een nieuw console‑project en klik op **Run**.

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

**Verwachte console‑output**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

En het bestand `numbers.txt` zal de drie hierboven getoonde regels bevatten.

---

## Volgende stappen: Verder gaan dan de basis

- **Exporteer andere formaten** – Aspose.Cells ondersteunt ook CSV, HTML en PDF. Vervang `TxtSaveOptions` door `CsvSaveOptions` of `PdfSaveOptions` indien nodig.  
- **Dynamische precisie** – je kunt `SignificantDigits` berekenen tijdens runtime op basis van gebruikersinvoer of configuratiebestanden.  
- **Meerdere werkbladen** – iterate over `workbook.Worksheets` en exporteer elk naar een eigen `.txt`‑bestand.  
- **Lokalisatie** – beheer het decimale scheidingsteken (`.` vs `,`) via `CultureInfo` als je moet voldoen aan regionale instellingen.  

Al deze uitbreidingen bouwen nog steeds voort op het kernidee dat we hebben behandeld: **nieuw werkboek maken**, de export configureren, en **numerieke precisie instellen** om te voldoen aan je rapportage‑eisen.

---

## Samenvatting

We hebben een vers **nieuw werkboek**‑instance genomen, deze gevuld met data, en laten zien hoe je **Excel naar TXT exporteert** terwijl je **significante cijfers** instelt om de uitvoerprecisie te beperken. Het volledige voorbeeld werkt direct out‑of‑the‑box, en de uitleg behandelt het *waarom* achter elke regel zodat je het kunt aanpassen aan je eigen projecten.

Voel je vrij om te experimenteren—verander de waarde van `SignificantDigits`, voeg meer bladen toe, of wissel het uitvoerformaat. Als je ergens vastloopt, raadpleeg dan de Aspose.Cells‑documentatie of laat een reactie achter hieronder. Veel programmeerplezier!

---

![Voorbeeld nieuw werkboek](/images/create-new-workbook.png "Schermafbeelding van een C#‑IDE met de code voor het maken van een nieuw werkboek")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}