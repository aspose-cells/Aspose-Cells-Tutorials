---
"description": "Leer hoe u weergaveformaten kunt aanpassen met Aspose.Cells voor .NET. Formatteer datums, percentages en valuta met behulp van deze stapsgewijze handleiding."
"linktitle": "Weergaveformaten aanpassen met door de gebruiker gedefinieerde getallen"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Weergaveformaten aanpassen met door de gebruiker gedefinieerde getallen"
"url": "/nl/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Weergaveformaten aanpassen met door de gebruiker gedefinieerde getallen

## Invoering
Werken met Excel-bestanden vereist vaak aangepaste celopmaak om gegevens op een betekenisvollere en gebruiksvriendelijkere manier te presenteren. Stel je voor dat je een Excel-bestand voor een rapport maakt. Je wilt niet alleen ruwe getallen. Je wilt toch ook dat datums, percentages en valuta's er strak en professioneel uitzien? Daar komen aangepaste weergaveformaten om de hoek kijken. In deze tutorial duiken we dieper in Aspose.Cells voor .NET om je te laten zien hoe je de weergave van getallen kunt aanpassen met behulp van door de gebruiker gedefinieerde instellingen.
## Vereisten
Voordat je begint, zorg ervoor dat je alles klaar hebt om deze tutorial te volgen. Dit heb je nodig:
- Aspose.Cells voor .NET geïnstalleerd. [Download het hier](https://releases.aspose.com/cells/net/).
- Basiskennis van C# en .NET Framework.
- Een geldige licentie voor Aspose.Cells. Als je die niet hebt, neem dan een [gratis proefperiode](https://releases.aspose.com/) of vraag een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/).
- Een IDE zoals Visual Studio.
- .NET Framework 4.0 of hoger.
Als je iets mist, maak je dan geen zorgen. Je kunt altijd deze links opnieuw bezoeken om de benodigde bestanden te downloaden of hulp te zoeken bij de [Aspose-ondersteuningsforum](https://forum.aspose.com/c/cells/9).
## Naamruimten importeren
Voordat u met de code aan de slag gaat, moet u de vereiste naamruimten importeren om toegang te krijgen tot alle benodigde Aspose.Cells-functionaliteiten.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Deze twee naamruimten vormen je belangrijkste tools in deze tutorial. Laten we nu verder gaan met het leuke gedeelte:
## Stap 1: De projectmap instellen
Eerst heb je een plek nodig om je bestanden op te slaan, toch? Laten we een map aanmaken om het Excel-uitvoerbestand op te slaan. In deze stap controleren we ook of de map bestaat voordat we iets opslaan.
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- We definiëren een `dataDir` variabele om het pad op te slaan waar het Excel-uitvoerbestand naartoe moet.
- Vervolgens controleren we of de directory bestaat met behulp van `System.IO.Directory.Exists()`.
- Als de map niet bestaat, wordt deze aangemaakt met behulp van `System.IO.Directory.CreateDirectory()`.
## Stap 2: Een nieuwe werkmap maken en een werkblad toevoegen
Nu we onze map hebben, kunnen we een nieuwe Excel-werkmap maken en er een werkblad aan toevoegen.
```csharp
// Een werkmapobject instantiëren
Workbook workbook = new Workbook();
// Een nieuw werkblad toevoegen aan het Excel-object
int i = workbook.Worksheets.Add();
// De referentie van het nieuw toegevoegde werkblad verkrijgen door de index van het werkblad door te geven
Worksheet worksheet = workbook.Worksheets[i];
```
- Eerst creëren we een nieuwe `Workbook` object. Beschouw dit als uw Excel-bestand.
- We voegen een nieuw werkblad toe aan deze werkmap met behulp van de `Add()` methode en sla de index op in een variabele `i`.
- We verwijzen naar dit werkblad met behulp van de `workbook.Worksheets[i]`.
## Stap 3: Datum toevoegen aan een cel en de opmaak aanpassen
Laten we nu de huidige datum in een cel invoegen en deze opmaken zodat deze op een aangepaste manier wordt weergegeven. In plaats van de standaard datumnotatie, gebruiken we een aangepaste notatie, zoals `d-mmm-yy`.
```csharp
// De huidige systeemdatum toevoegen aan cel "A1"
worksheet.Cells["A1"].PutValue(DateTime.Now);
// De stijl van cel A1 verkrijgen
Style style = worksheet.Cells["A1"].GetStyle();
// Het aangepaste weergaveformaat instellen om de datum weer te geven als "d-mmm-jj"
style.Custom = "d-mmm-yy";
// De stijl toepassen op cel A1
worksheet.Cells["A1"].SetStyle(style);
```
- We voegen de huidige systeemdatum toe aan cel `A1` gebruik makend van `PutValue(DateTime.Now)`.
- We halen de huidige stijl van de cel op `A1` gebruik makend van `GetStyle()`.
- We wijzigen de stijl van de cel door in te stellen `style.Custom = "d-mmm-yy"`, waarmee de datum wordt opgemaakt als de dag, afgekorte maand en jaar.
- Ten slotte passen we de nieuwe stijl toe op de cel met `SetStyle()`.
## Stap 4: Een cel opmaken als percentage
Laten we nu met getallen werken. We voegen een numerieke waarde toe aan een andere cel, bijvoorbeeld `A2`en formatteer het als een percentage.
```csharp
// Een numerieke waarde toevoegen aan cel "A2"
worksheet.Cells["A2"].PutValue(20);
// De stijl van cel A2 verkrijgen
style = worksheet.Cells["A2"].GetStyle();
// Het aangepaste weergaveformaat instellen om de waarde als percentage weer te geven
style.Custom = "0.0%";
// De stijl toepassen op cel A2
worksheet.Cells["A2"].SetStyle(style);
```
- Wij voegen waarde toe `20` naar de cel `A2`.
- We halen de stijl van de cel op `A2` en stel de aangepaste opmaak in op `0.0%` om de waarde als percentage weer te geven (bijv. 20%).
- Ten slotte passen we de stijl toe op de cel met behulp van `SetStyle()`.
## Stap 5: Een cel opmaken als valuta
Laten we nog een waarde toevoegen, bijvoorbeeld aan cel `A3`en formatteer het om het als valuta weer te geven. Om het interessanter te maken, gebruiken we een formaat dat positieve waarden als valuta in ponden en negatieve waarden in dollars weergeeft.
```csharp
// Een numerieke waarde toevoegen aan cel "A3"
worksheet.Cells["A3"].PutValue(2546);
// De stijl van A3-cel verkrijgen
style = worksheet.Cells["A3"].GetStyle();
// Het aangepaste weergaveformaat instellen om de waarde als valuta weer te geven
style.Custom = "£#,##0;[Red]$-#,##0";
// De stijl toepassen op A3-cel
worksheet.Cells["A3"].SetStyle(style);
```
- Wij voegen waarde toe `2546` naar de cel `A3`.
- Wij stellen een aangepast formaat in `£#,##0;[Red]$-#,##0`, waarbij positieve waarden met een pondteken worden weergegeven en negatieve waarden in rood met een dollarteken.
- We passen de stijl toe op de cel met behulp van `SetStyle()`.
## Stap 6: De werkmap opslaan
De laatste stap is het opslaan van de werkmap als Excel-bestand. We gebruiken de Excel 97-2003-indeling voor deze tutorial.
```csharp
// Het Excel-bestand opslaan
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
- De `Save()` methode slaat de werkmap op in de opgegeven directory.
- Wij kiezen `SaveFormat.Excel97To2003` om compatibiliteit met oudere versies van Excel te garanderen.
## Conclusie
Zo! We hebben zojuist een Excel-bestand gemaakt, aangepaste datum-, percentage- en valuta-indelingen aan specifieke cellen toegevoegd met Aspose.Cells voor .NET en het bestand opgeslagen. Aangepaste opmaak maakt uw Excel-bestanden veel leesbaarder en professioneler. Vergeet niet om de andere opmaakopties in Aspose.Cells te verkennen, zoals voorwaardelijke opmaak, voor nog meer controle over hoe uw gegevens eruitzien.
## Veelgestelde vragen
### Hoe kan ik complexere opmaakopties toepassen in Aspose.Cells?
U kunt verschillende opmaakstijlen, zoals tekstkleur, randen en achtergrondkleuren, combineren met aangepaste getalnotaties.
### Kan ik een aangepaste getalnotatie toepassen op een celbereik?
Ja, met Aspose.Cells kunt u een stijl toepassen op een cellenbereik met behulp van de `Range.SetStyle()` methode.
### In welke andere bestandsindelingen kan ik de werkmap opslaan?
Aspose.Cells ondersteunt vele formaten, waaronder XLSX, CSV en PDF. Verander eenvoudig de `SaveFormat` in de `Save()` methode.
### Kan ik negatieve getallen anders opmaken?
Absoluut! Je kunt aangepaste getalnotaties gebruiken om negatieve getallen met verschillende kleuren of symbolen weer te geven.
### Is Aspose.Cells voor .NET gratis?
Aspose.Cells biedt een gratis proefperiode aan, maar voor volledige functionaliteit heb je een geldige licentie nodig. Je kunt een [tijdelijke licentie hier](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}