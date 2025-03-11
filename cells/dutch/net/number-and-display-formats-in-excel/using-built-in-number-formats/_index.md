---
title: Ingebouwde getalnotaties in Excel programmatisch gebruiken
linktitle: Ingebouwde getalnotaties in Excel programmatisch gebruiken
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Automatiseer getalnotatie in Excel met Aspose.Cells voor .NET. Leer hoe u datum-, percentage- en valutaformaten programmatisch toepast.
weight: 10
url: /nl/net/number-and-display-formats-in-excel/using-built-in-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ingebouwde getalnotaties in Excel programmatisch gebruiken

## Invoering
In deze tutorial laten we je zien hoe je ingebouwde getalnotaties in Excel gebruikt met Aspose.Cells voor .NET. We behandelen alles van het instellen van je omgeving tot het toepassen van verschillende formaten zoals datums, percentages en valuta's. Of je nu een doorgewinterde professional bent of net begint met het .NET-ecosysteem, met deze gids kun je Excel-cellen heel eenvoudig formatteren.
## Vereisten
Voordat u begint, moet u ervoor zorgen dat u het volgende bij de hand hebt:
-  Aspose.Cells voor .NET-bibliotheek geïnstalleerd. U kunt[download het hier](https://releases.aspose.com/cells/net/).
- Kennis van C# en basiskennis van .NET-programmering.
- Visual Studio of een andere .NET IDE op uw computer geïnstalleerd.
-  Een geldige Aspose-licentie of[tijdelijke licentie](https://purchase.aspose.com/temporary-license/).
- .NET Framework geïnstalleerd (versie 4.0 of hoger).
  
Als je een van de bovenstaande dingen mist, volg dan de links om alles in te stellen. Klaar? Laten we beginnen met het leuke gedeelte!
## Pakketten importeren
Voordat we met de tutorial beginnen, moet u ervoor zorgen dat u de benodigde naamruimten voor het werken met Aspose.Cells voor .NET importeert:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Zodra u deze hebt geïmporteerd, bent u helemaal klaar om Excel-bestanden programmatisch te manipuleren. Laten we nu in de stapsgewijze handleiding duiken!
## Stap 1: Maak of open uw Excel-werkmap
In deze stap maakt u een nieuwe werkmap. Zie dit als het openen van een nieuw Excel-bestand, maar dan via code!
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Een werkmapobject instantiëren
Workbook workbook = new Workbook();
```
 Hier instantiëren we eenvoudigweg een nieuwe`Workbook` object. Dit fungeert als uw Excel-bestand, klaar voor gegevensmanipulatie. U kunt ook een bestaand bestand laden door het pad ervan op te geven.
## Stap 2: Toegang tot het werkblad
Excel-werkmappen kunnen meerdere werkbladen bevatten. In deze stap openen we het eerste werkblad in uw werkmap:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
We hebben nu toegang tot het eerste werkblad in de werkmap. Als u extra werkbladen moet manipuleren, kunt u ernaar verwijzen met behulp van hun index of naam.
## Stap 3: Gegevens toevoegen aan cellen
Laten we beginnen met het toevoegen van wat data aan specifieke cellen. Eerst voegen we de huidige systeemdatum toe aan cel "A1":
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Deze regel voegt de huidige datum in cel A1 in. Best cool, toch? Stel je voor dat je dit handmatig voor honderden cellen zou doen, dat zou een nachtmerrie zijn. Nu gaan we verder met opmaken!
## Stap 4: Datum opmaken in cel "A1"
Laten we die datum vervolgens opmaken in een beter leesbaar formaat, zoals "15-okt-24". Dit is waar Aspose.Cells echt schittert:
1. Haal de stijl van de cel op:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Hier pakken we de stijl van cel A1. Zie dit als het pakken van de "mode" van de cel voordat we aanpassingen maken.
2. Stel de datumnotatie in:
```csharp
style.Number = 15;
```
 Het instellen van de`Number` eigenschap tot 15 past de gewenste datumnotatie toe. Dit is een ingebouwde getalnotatiecode voor het weergeven van datums in de notatie "d-mmm-jj".
3. Pas de stijl toe op de cel:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Deze regel past de stijlwijzigingen toe op de cel. Nu ziet u in plaats van een standaarddatumnotatie iets dat veel gebruiksvriendelijker is, zoals "15-okt-24."
## Stap 5: Een percentage toevoegen en opmaken in cel "A2"
Laten we verder gaan met het formatteren van percentages. Stel dat u een waarde wilt invoeren en deze wilt weergeven als een percentage. In deze stap voegen we een numerieke waarde toe aan cel "A2" en formatteren deze als een percentage:
1. Numerieke waarde invoegen:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Hiermee wordt het getal 20 in cel A2 ingevoegd. U denkt misschien: "Dat is gewoon een gewoon getal, hoe verander ik het in een percentage?" Nou, daar komen we zo aan.
2. Haal de stijl op en stel het percentageformaat in:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Formaat als percentage
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Hier voegen we 2546 toe aan cel A3. Vervolgens formatteren we dit getal zodat het als valuta wordt weergegeven.
2. Haal de stijl op en stel de valuta-indeling in:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Formaat als valuta
worksheet.Cells["A3"].SetStyle(style);
```
 Het instellen van de`Number` eigenschap op 6 past de valuta-indeling toe. Nu wordt de waarde in cel A3 weergegeven als "2.546,00", compleet met komma's en twee decimalen.
## Stap 7: Sla het Excel-bestand op
Nu we alle opmaakvaardigheden hebben toegepast, is het tijd om het bestand op te slaan:
```csharp
// Het Excel-bestand opslaan
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 Deze regel slaat het Excel-bestand op in de Excel 97-2003-indeling. U kunt de`SaveFormat`aan uw behoeften aan te passen. En zo heeft u een Excel-bestand programmatisch gemaakt en geformatteerd!
## Conclusie
Gefeliciteerd! U hebt succesvol geleerd hoe u Aspose.Cells voor .NET kunt gebruiken om ingebouwde getalnotaties toe te passen op cellen in een Excel-bestand. Van datums tot percentages en valuta's, we hebben enkele van de meest voorkomende opmaakbehoeften voor Excel-gegevensverwerking behandeld. Nu kunt u, in plaats van cellen handmatig op te maken, het hele proces automatiseren, waardoor u tijd bespaart en fouten vermindert.
## Veelgestelde vragen
### Kan ik aangepaste getalnotaties toepassen met Aspose.Cells voor .NET?
 Ja! Naast ingebouwde formaten ondersteunt Aspose.Cells ook aangepaste getalformaten. U kunt zeer specifieke formaten maken met behulp van de`Custom` eigendom in de`Style` klas.
### Hoe kan ik een cel opmaken als valuta met een specifiek symbool?
 Om een specifiek valutasymbool toe te passen, kunt u aangepaste opmaak gebruiken door de`Style.Custom` eigendom.
### Kan ik hele rijen of kolommen opmaken?
 Absoluut! U kunt stijlen toepassen op hele rijen of kolommen met behulp van de`Rows` of`Columns`collecties in de`Worksheet` voorwerp.
### Hoe kan ik meerdere cellen tegelijk opmaken?
 kunt de`Range` object om meerdere cellen te selecteren en stijlen op alle cellen tegelijk toe te passen.
### Moet ik Microsoft Excel geïnstalleerd hebben om Aspose.Cells te kunnen gebruiken?
Nee, Aspose.Cells werkt onafhankelijk van Microsoft Excel. U hoeft Excel dus niet op uw computer te hebben geïnstalleerd.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
