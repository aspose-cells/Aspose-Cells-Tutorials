---
title: Enkelvoudig aanhalingsteken voorvoegsel van celwaarde of celbereik in Excel behouden
linktitle: Enkelvoudig aanhalingsteken voorvoegsel van celwaarde of celbereik in Excel behouden
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u enkele aanhalingstekens in Excel-cellen kunt behouden met Aspose.Cells voor .NET met deze eenvoudige stapsgewijze zelfstudie.
weight: 10
url: /nl/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Enkelvoudig aanhalingsteken voorvoegsel van celwaarde of celbereik in Excel behouden

## Invoering

Wanneer u met Excel-bestanden werkt, kunt u in situaties terechtkomen waarin u een enkel aanhalingsteken als voorvoegsel in celwaarden moet behouden. Dit kan met name cruciaal zijn wanneer de gegevens waarmee u werkt extra zorg nodig hebben, zoals in het geval van id's of strings waarvan u niet wilt dat Excel de waarde interpreteert. In deze handleiding gaan we dieper in op hoe u dit kunt bereiken met Aspose.Cells voor .NET. Pak dus uw favoriete drankje en laten we beginnen!

## Vereisten

Voordat we aan deze codeeravontuur beginnen, willen we ervoor zorgen dat je alles hebt wat je nodig hebt:

1. Visual Studio: U hebt een ontwikkelomgeving nodig om uw .NET-code uit te voeren.
2.  Aspose.Cells voor .NET: Zorg ervoor dat u deze bibliotheek hebt gedownload en in uw project hebt gerefereerd. U kunt de nieuwste versie ophalen van de[Downloadlink](https://releases.aspose.com/cells/net/).
3. Basiskennis van C#-programmering: het is handig om bekend te zijn met C#, vooral als u van plan bent de code te wijzigen.
4. Een Windows-besturingssysteem: Omdat Aspose.Cells primair gericht is op Windows, zal het installeren ervan alles soepeler laten verlopen.

Nu we de checklist hebben, kunnen we beginnen met het leukste gedeelte: coderen!

## Pakketten importeren

Om te beginnen moeten we de benodigde pakketten importeren in ons C#-project. Dit is het pakket waar je op moet letten:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Met deze regel krijgt u toegang tot alle klassen en methoden die de Aspose.Cells-bibliotheek biedt, zodat u moeiteloos Excel-bestanden kunt bewerken. 

Laten we nu de stappen uitleggen om het enkele aanhalingsteken als voorvoegsel in de celwaarden te behouden.

## Stap 1: De werkmap instellen

Eerst moeten we een nieuwe werkmap maken en de mappen voor de invoer- en uitvoerbestanden opgeven.

```csharp
// Bron directory
string sourceDir = "Your Document Directory/";

// Uitvoermap
string outputDir = "Your Document Directory/";

// Werkmap maken
Workbook wb = new Workbook();
```

 In deze stap initialiseren we onze werkmap, waar Excel-bestanden worden beheerd. Vervangen`"Your Document Directory"` met het daadwerkelijke pad waar u uw bestanden wilt opslaan.

## Stap 2: Toegang tot het werkblad

Vervolgens pakken we het eerste werkblad van de werkmap aan. Hier zal onze actie plaatsvinden.

```csharp
// Toegang tot eerste werkblad
Worksheet ws = wb.Worksheets[0];
```

Hiermee selecteert u eenvoudigweg het eerste werkblad, wat voor de meeste taken prima is, tenzij u specifieke behoeften hebt voor meerdere werkbladen.

## Stap 3: Toegang tot en wijziging van de celwaarde

Laten we nu met een specifieke cel werken: cel A1. 

```csharp
// Toegang tot cel A1
Cell cell = ws.Cells["A1"];

// Plaats wat tekst in de cel, er staat geen enkele aanhalingsteken aan het begin
cell.PutValue("Text");
```

In deze stap voeren we een waarde in cel A1 in zonder een enkele aanhalingsteken. Maar laten we de celstijl controleren!

## Stap 4: Controleer het citaatvoorvoegsel

Het is tijd om naar de stijl van onze cel te kijken en te zien of de waarde voor het aanhalingsteken is ingesteld.

```csharp
// Toegangsstijl van cel A1
Style st = cell.GetStyle();

// De waarde van Style.QuotePrefix van cel A1 afdrukken
Console.WriteLine("Quote Prefix of Cell A1: " + st.QuotePrefix);
```

Hier krijgen we toegang tot de stylinginformatie voor de cel. In eerste instantie zou het aanhalingsteken-voorvoegsel false moeten zijn, aangezien er geen enkel aanhalingsteken is.

## Stap 5: Voeg een enkelvoudig aanhalingsteken als voorvoegsel toe

Laten we nu experimenteren met het plaatsen van een enkele aanhalingsteken in de waarde van de cel.

```csharp
// Zet wat tekst in de cel, er staat een enkele aanhalingsteken aan het begin
cell.PutValue("'Text");

// Toegangsstijl van cel A1
st = cell.GetStyle();

// De waarde van Style.QuotePrefix van cel A1 afdrukken
Console.WriteLine("Quote Prefix of Cell A1: " + st.QuotePrefix);
```

Na deze stap ziet u dat het aanhalingsteken-voorvoegsel verandert in true! Dit toont aan dat onze Excel-cel nu is ingesteld om het enkele aanhalingsteken te herkennen.

## Stap 6: Begrijp StyleFlags

 Laten we nu eens kijken hoe de`StyleFlag` kan van invloed zijn op ons citaatvoorvoegsel.

```csharp
// Maak een lege stijl
st = wb.CreateStyle();

// Stijlvlag maken - StyleFlag.QuotePrefix instellen als false
StyleFlag flag = new StyleFlag();
flag.QuotePrefix = false;

// Maak een bereik bestaande uit één cel A1
Range rng = ws.Cells.CreateRange("A1");

// Pas de stijl toe op het bereik
rng.ApplyStyle(st, flag);
```

 Hier is de clou! Door te specificeren`flag.QuotePrefix = false`, we vertellen het programma: "Hé, raak het bestaande voorvoegsel niet aan." Dus wat gebeurt er?

## Stap 7: Controleer het citaatvoorvoegsel opnieuw

Laten we eens kijken hoe onze wijzigingen het bestaande aanhalingsteken-voorvoegsel beïnvloeden.

```csharp
// Toegang tot de stijl van cel A1
st = cell.GetStyle();

// De waarde van Style.QuotePrefix van cel A1 afdrukken
Console.WriteLine("Quote Prefix of Cell A1: " + st.QuotePrefix);
```

Nadat u deze stijl hebt toegepast, wordt de uitvoer nog steeds 'true' weergegeven, omdat we deze niet hebben bijgewerkt.

## Stap 8: Werk het citaatvoorvoegsel bij met StyleFlag

Oké, laten we eens kijken wat er gebeurt als we ons voorvoegsel willen bijwerken.

```csharp
// Maak een lege stijl
st = wb.CreateStyle();

// Stijlvlag maken - StyleFlag.QuotePrefix instellen als true
flag = new StyleFlag();
flag.QuotePrefix = true;

// Pas de stijl toe op het bereik
rng.ApplyStyle(st, flag);
```

In deze ronde stellen we in`flag.QuotePrefix = true`, wat betekent dat we het aanhalingsteken-voorvoegsel van de cel willen bijwerken.

## Stap 9: Laatste controle van het voorvoegsel van de offerte

Laten we afronden door te kijken hoe het aanhalingsteken er nu uitziet:

```csharp
// Toegang tot de stijl van cel A1
st = cell.GetStyle();

// De waarde van Style.QuotePrefix van cel A1 afdrukken
Console.WriteLine("Quote Prefix of Cell A1: " + st.QuotePrefix);
```

Op dit punt zou de uitvoer false moeten weergeven, omdat we expliciet hebben aangegeven dat we het voorvoegsel willen bijwerken.

## Conclusie

En daar heb je het! Door deze stappen te volgen, heb je geleerd hoe je het enkele aanhalingsteken in celwaarden kunt behouden terwijl je Aspose.Cells voor .NET gebruikt. Hoewel het misschien een klein detail lijkt, kan het behouden van de integriteit van je gegevens in Excel cruciaal zijn in veel toepassingen, vooral als je id's of geformatteerde strings verwerkt. 

## Veelgestelde vragen

### Wat is het doel van het enkele aanhalingsteken als voorvoegsel in Excel?  
Door het enkele aanhalingsteken als voorvoegsel te gebruiken, weet Excel dat de waarde als tekst moet worden behandeld. Zo wordt voorkomen dat de waarde als een getal of formule wordt geïnterpreteerd.

### Kan ik Aspose.Cells gebruiken in webapplicaties?  
Jazeker! Aspose.Cells voor .NET werkt goed met zowel desktop- als webtoepassingen.

### Zijn er prestatieoverwegingen bij het gebruik van Aspose.Cells?  
Over het algemeen is Aspose.Cells geoptimaliseerd voor prestaties, maar bij zeer grote datasets is het altijd verstandig om het geheugen en de snelheid te testen.

### Hoe kan ik hulp krijgen als ik problemen ondervind?  
 U kunt de[ondersteuningsforum](https://forum.aspose.com/c/cells/9) voor hulp van de gemeenschap en het Aspose-personeel.

### Kan ik Aspose.Cells uitproberen zonder te kopen?  
 Absoluut! Je kunt een gratis proefperiode krijgen[hier](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
