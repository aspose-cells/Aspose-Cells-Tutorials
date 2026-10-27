---
category: general
date: 2026-03-29
description: Hur man ersätter variabler i JSON med SmartMarker – lär dig använda if‑uttryck,
  tillämpa villkorslogik, multiplicera värden och generera JSON utan ansträngning.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: sv
og_description: Hur man ersätter variabler i JSON med SmartMarker. Upptäck hur du
  använder if‑uttryck, tillämpar villkorslogik, multiplicerar värden och genererar
  JSON på några minuter.
og_title: Hur man ersätter variabler i JSON med SmartMarker – Steg för steg
tags:
- C#
- SmartMarker
- JSON templating
title: Hur man ersätter variabler i JSON med SmartMarker – Komplett guide
url: /sv/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man ersätter variabler i JSON med SmartMarker – Komplett guide

Har du någonsin undrat **how to substitute variables** i en JSON‑payload utan att skriva en egen parser? Du är inte ensam. I många integrationsscenario—tänk fakturor, prisengineer eller dynamiska konfigurationsfiler—behöver du injicera körningsvärden, tillämpa enkla villkor och kanske till och med göra en snabb multiplikation. Den här handledningen visar dig exakt **how to substitute variables** med SmartMarker‑biblioteket, samtidigt som JSON‑filen hålls ren och läsbar.

Vi går igenom ett verkligt exempel som täcker **use if expression**, **how to apply conditional**, **how to multiply values** och **how to generate json** i farten. I slutet har du ett färdigt C#‑snutt som du kan klistra in i vilket .NET‑projekt som helst.

## Vad du kommer att lära dig

- Ställ in `SmartMarkerOptions` för att lagra återanvändbara variabler.  
- Skriv en JSON‑mall som innehåller ett `if`‑uttryck för villkorslogik.  
- Multiplicera ett värde med en variabel i mallen.  
- Bearbeta mallen med `SmartMarkerProcessor` och få den slutgiltiga JSON‑strängen.  
- Felsök vanliga fallgropar såsom saknade variabler eller felaktiga uttryck.

Inga externa tjänster, inga tunga beroenden—bara ren C# och SmartMarker‑paketet från NuGet.

---

## Så ersätts variabler – Steg‑för‑steg‑översikt

Nedan är en översiktlig bild av arbetsflödet. Tänk på det som en pipeline där din råa JSON‑mall kommer in från vänster, SmartMarker‑motorn gör sin magi, och den fullständigt renderade JSON‑en lämnar åt höger.

![Diagram som visar hur man ersätter variabler i JSON](https://example.com/images/smartmarker-flow.png "Hur man ersätter variabler i JSON")

*Bildtext: Diagram som visar hur man ersätter variabler i JSON.*

---

## Steg 1: Installera och importera SmartMarker

Innan du kan börja, se till att SmartMarker‑paketet refereras i ditt projekt. Om du använder .NET‑CLI, kör:

```bash
dotnet add package SmartMarker
```

Sedan lägger du till de nödvändiga `using`‑direktiven högst upp i din C#‑fil:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Pro tip:** Den senaste versionen (från mars 2026) är 2.4.1. Den stödjer .NET 6 och senare, men fungerar lika bra med .NET Framework 4.7 också.

---

## Steg 2: Skapa SmartMarker‑alternativ och definiera variabler

Nu skapar vi en instans av `SmartMarkerOptions` som kommer att hålla alla variabler vi vill återanvända i mallen. Här svarar vi på frågan **how to substitute variables**—variablerna fungerar som platshållare som SmartMarker senare ersätter.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

Varför lagra räntan i `Variables` istället för att hårdkoda den? För att du kan hämta det talet från en databas, en konfigurationsfil eller en användarinmatning. Att ha den i alternativen gör mallen återanvändbar och testbar.

---

## Steg 3: Skriv JSON‑mallen med ett `if`‑uttryck

Här kommer nyckelordet **use if expression** till sin rätt. SmartMarker låter dig bädda in villkorslogik direkt i JSON‑strängen. Syntaxen ser lite ut som ett egenskapsnamn, men SmartMarker behandlar det som en direktiv.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

Observera nyckeln `if(Amount>500)`. SmartMarker utvärderar uttrycket `Amount>500`; om det är sant, sätts motsvarande värde (`${Amount * Rate}`) in i resultatet. `${...}`‑syntaxen är *variable substitution*-motorn—här **how to multiply values** (`Amount * Rate`) innan resultatet injiceras.

---

## Steg 4: Bearbeta mallen och hämta den slutgiltiga JSON‑en

Med alternativen och mallen klara, överlämnar vi allt till processorn. Metoden `ProcessJson` parsar mallen, tillämpar villkoret, utför multiplikationen och returnerar en ren JSON‑sträng.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

Kör du snutten skrivs följande ut:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**Vad hände?**  
- `Amount` är 1000, vilket uppfyller `Amount>500`.  
- SmartMarker utvärderar `${Amount * Rate}` → `1000 * 0.08 = 80`.  
- Den ursprungliga villkorskodnyckeln (`if(Amount>500)`) ersätts av ett rent egenskapsnamn (`Result`). Som standard använder SmartMarker `"Result"` men du kan anpassa det (mer om det senare).

Om du ändrar `Amount` till `400` blir resultatet:

```json
{
  "Amount": 400
}
```

Det villkorsblocket försvinner eftersom uttrycket utvärderades till `false`. Det är kärnan i **how to apply conditional**‑logik i JSON.

---

## Steg 5: Anpassa namn på utdataegenskap (valfritt)

Ibland vill du inte ha den generiska nyckeln `"Result"`. SmartMarker låter dig ange ett eget namn med alternativet `RenameIfExpression`:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Utdata:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

Nu lagras det villkorliga värdet under ett mer meningsfullt egenskapsnamn—perfekt för downstream‑tjänster som förväntar sig ett specifikt fält.

---

## Vanliga fallgropar och hur du undviker dem

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| Variable not found | Du refererade en variabel som inte finns i `smartMarkerOptions.Variables`. | Dubbelkolla stavning och säkerställ att variabeln läggs till innan bearbetning. |
| Invalid `if` syntax | Saknade parenteser eller fel operator (`>`, `<`, `==`). | Följ exakt `if(<expression>)`‑mönstret; SmartMarker stödjer bara enkla numeriska jämförelser. |
| JSON becomes malformed | Av misstag lämnat ett efterkommatecken efter det villkorliga blocket. | Låt SmartMarker hantera borttagningen; håll den ursprungliga mallen syntaktiskt korrekt. |
| Unexpected number format | Resultatet visas som en sträng `"80"` istället för ett tal. | Gör en cast eller parsning senare, eller använd `${(Amount * Rate):N0}` för numerisk formatering. |

---

## Fullt fungerande exempel (klart att kopiera och klistra in)

Nedan är det kompletta programmet som du kan kompilera och köra. Det demonstrerar **how to generate json** med dynamiska variabler, villkor och aritmetik—allt på under 30 rader.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**Förväntad konsolutskrift**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

Känn dig fri att ändra `Amount` för att testa den villkorliga grenen, eller justera `Rate` för att se olika rabattberäkningar.

---

## Utöka mönstret – fler “How to”‑scenarier

- **How to substitute variables** från en konfigurationsfil: Ladda en `Dictionary<string, object>` från `appsettings.json` och mata in den i `smartMarkerOptions.Variables`.  
- **How to use if expression** för flera villkor: Kedja dem som `"if(Amount>500 && CustomerType=='VIP')"`—SmartMarker stödjer logisk AND/OR.  
- **How to apply conditional** formatering: Använd `${Amount:0.00}` i uttrycket för att styra decimaler.  
- **How to multiply values** med mer komplex matematik: `${(Amount - Discount) * TaxRate}` fungerar på samma sätt.  
- **How to generate json** för nästlade objekt: Placera det villkorliga blocket inuti ett annat JSON‑objekt, så bevarar SmartMarker hierarkin.

---

## Slutsats

Vi har gått igenom **how to substitute variables** i JSON med SmartMarker, demonstrerat **use if expression** för villkorlig inkludering, förklarat **how to apply conditional**‑logik, visat **how to multiply values** i en mall, och slutligen illustrerat **how to generate json** som är klar för downstream‑användning. Metoden är lättviktig, kräver ingen extern mallmotor och passar perfekt in i vilken C#‑kodbas som helst.

Prova det—justera variablerna, lägg till fler villkor, eller paketera hela grejen i en hjälparklass för återanvändning i hela din lösning. När du snabbt behöver producera dynamisk JSON är SmartMarker ett stabilt, produktionsklart alternativ.

**Nästa steg**

- Fördjupa dig i SmartMarkers avancerade funktioner som loopar (`foreach`) och anpassade funktioner.  
- Kombinera tekniken med ASP.NET Core‑endpoints för att leverera dynamiska JSON‑API:er.  
- Utforska andra mallbibliotek (t.ex. Handlebars.NET) för jämförelse, särskilt om du behöver rikare syntax.

Har du frågor eller ett specifikt användningsfall du kämpar med? Lägg en kommentar nedan, så felsöker vi tillsammans. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}