---
"description": "Leer hoe u specifieke cellen in een Excel-werkblad kunt beveiligen met Aspose.Cells voor .NET. Beveilig gevoelige gegevens en voorkom onbedoelde wijzigingen in slechts een paar stappen."
"linktitle": "Specifieke cellen in een werkblad beveiligen met Aspose.Cells"
"second_title": "Aspose.Cells .NET Excel-verwerkings-API"
"title": "Specifieke cellen in een werkblad beveiligen met Aspose.Cells"
"url": "/nl/net/worksheet-security/protect-specific-cells/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Specifieke cellen in een werkblad beveiligen met Aspose.Cells

## Invoering
In deze tutorial laten we je zien hoe je specifieke cellen in een Excel-werkblad kunt beveiligen. Uiteindelijk kun je cellen veilig en professioneel vergrendelen, zodat je ongeoorloofde wijzigingen kunt voorkomen en je werkblad flexibel blijft waar nodig.
## Vereisten
Voordat we in de details duiken, willen we ervoor zorgen dat je alles hebt wat je nodig hebt om deze tutorial soepel te kunnen volgen:
1. Visual Studio – Download en installeer Visual Studio als u dat nog niet hebt gedaan. Dit wordt de primaire omgeving waarin u uw .NET-applicaties uitvoert.
2. Aspose.Cells voor .NET – Je hebt de Aspose.Cells-bibliotheek nodig om met Excel-bestanden in je .NET-toepassingen te werken. Als je deze nog niet hebt geïnstalleerd, kun je de nieuwste versie downloaden via de [Aspose-website](https://releases.aspose.com/cells/net/).
3. .NET Framework of .NET Core – Deze tutorial werkt met zowel .NET Framework als .NET Core. Zorg er wel voor dat je project compatibel is met Aspose.Cells.
Zodra u dit op orde hebt, kunt u aan de slag.
## Pakketten importeren
Voordat u met de stapsgewijze handleiding begint, moet u ervoor zorgen dat u de benodigde naamruimten importeert voor het werken met Aspose.Cells. Neem de volgende importinstructies bovenaan uw bestand op in uw project:
```csharp
using System.IO;
using Aspose.Cells;
```
Met deze naamruimten kunt u werken met Excel-bestanden en de klassen die nodig zijn voor de opmaak en beveiliging van werkbladcellen.
Laten we nu in eenvoudige stappen specifieke cellen in je werkblad beveiligen met Aspose.Cells voor .NET. We beveiligen de cellen A1, B1 en C1, terwijl de rest van het werkblad open blijft voor bewerkingen.
## Stap 1: Een nieuwe werkmap en werkblad maken
Allereerst moet je een nieuwe werkmap (Excel-bestand) en een werkblad daarin aanmaken. Hier ga je de celbeveiliging toepassen.
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
// Maak een nieuwe werkmap.
Workbook wb = new Workbook();
// Maak een werkbladobject en verkrijg het eerste werkblad.
Worksheet sheet = wb.Worksheets[0];
```
In deze stap maakt u ook een map aan om het resulterende Excel-bestand op te slaan, als dit nog niet bestaat. `Workbook` klasse initialiseert een nieuw Excel-bestand en `Worksheets[0]` Hiermee kunnen we met het eerste blad van de werkmap werken.
## Stap 2: Alle kolommen ontgrendelen
Vervolgens ontgrendel je alle kolommen in het werkblad. Dit zorgt ervoor dat standaard alle cellen in het werkblad bewerkbaar zijn. Later vergrendelen we alleen de cellen die we willen beveiligen.
```csharp
// Definieer het stijlobject.
Style style;
// Definieer het styleflag-object
StyleFlag styleflag;
// Doorloop alle kolommen in het werkblad en ontgrendel ze.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    styleflag = new StyleFlag();
    styleflag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, styleflag);
}
```
In dit codeblok itereren we door alle kolommen (tot 255) en stellen we de `IsLocked` eigendom van `false`Dit ontgrendelt in feite alle cellen in die kolommen, waardoor ze standaard bewerkbaar zijn. Vervolgens passen we de stijl toe op de kolom met de `ApplyStyle()` methode.
## Stap 3: Specifieke cellen vergrendelen (A1, B1, C1)
Nu alle kolommen ontgrendeld zijn, gaan we ons richten op het vergrendelen van specifieke cellen, namelijk A1, B1 en C1. We passen de celstijlen aan en stellen hun waarden in. `IsLocked` eigendom van `true`.
```csharp
// Vergrendel de drie cellen...d.w.z. A1, B1, C1.
style = sheet.Cells["A1"].GetStyle();
style.IsLocked = true;
sheet.Cells["A1"].SetStyle(style);
style = sheet.Cells["B1"].GetStyle();
style.IsLocked = true;
sheet.Cells["B1"].SetStyle(style);
style = sheet.Cells["C1"].GetStyle();
style.IsLocked = true;
sheet.Cells["C1"].SetStyle(style);
```
Met deze stap worden de cellen A1, B1 en C1 vergrendeld. Dit zijn de cellen die beveiligd zijn en niet meer te bewerken zijn zodra de werkbladbeveiliging is toegepast.
## Stap 4: Bescherm het werkblad
Nadat de benodigde cellen zijn vergrendeld, is de volgende stap het beveiligen van het hele werkblad. Deze stap zorgt ervoor dat de vergrendelde cellen (A1, B1, C1) niet meer te bewerken zijn, terwijl andere cellen open blijven voor bewerkingen.
```csharp
// Bescherm ten slotte het blad.
sheet.Protect(ProtectionType.All);
```
De `Protect` De methode wordt aangeroepen op het werkblad en geeft aan dat alle aspecten van het werkblad beveiligd moeten zijn. Dit vergrendelt de specifieke cellen die gemarkeerd zijn met `IsLocked = true` en zorgt ervoor dat deze niet door gebruikers gewijzigd kunnen worden.
## Stap 5: Sla de werkmap op
Zodra de cellen zijn vergrendeld en het werkblad is beveiligd, kunt u de werkmap op de gewenste locatie opslaan.
```csharp
// Sla het Excel-bestand op.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Met deze stap wordt de werkmap opgeslagen in de `dataDir` map met de bestandsnaam `output.out.xls`U kunt de bestandsnaam en map naar wens aanpassen. Het bestand wordt opgeslagen in Excel 97-2003-indeling, maar u kunt dit naar wens aanpassen.
## Conclusie
Het beveiligen van specifieke cellen in uw Excel-werkblad met Aspose.Cells voor .NET is een eenvoudig proces. Door de bovenstaande stappen te volgen, kunt u bepaalde cellen vergrendelen terwijl andere bewerkbaar blijven. Deze functie is zeer nuttig wanneer u werkmappen met anderen deelt, omdat u hiermee kunt bepalen welke gegevens mogen worden gewijzigd en welke gegevens beschermd moeten blijven. Of u nu met gevoelige gegevens werkt of gewoon onbedoelde wijzigingen wilt voorkomen, Aspose.Cells biedt een flexibele en krachtige oplossing.
## Veelgestelde vragen
### Hoe kan ik een specifiek cellenbereik beschermen in plaats van slechts een paar?
U kunt de code aanpassen, zodat deze door een specifiek bereik van cellen of kolommen heen loopt en deze vergrendelt, in plaats van dat u handmatig afzonderlijke cellen vergrendelt.
### Kan ik wachtwoorden toevoegen om het werkblad te beveiligen?
Ja, u kunt een wachtwoord opgeven wanneer u de `Protect()` Methode om te voorkomen dat gebruikers de beveiliging van het werkblad opheffen zonder het juiste wachtwoord.
### Kan ik specifieke rijen of kolommen beschermen in plaats van cellen?
Ja, met Aspose.Cells kunt u hele rijen of kolommen vergrendelen door de `IsLocked` eigenschap voor de rijen of kolommen, vergelijkbaar met de manier waarop we cellen hebben vergrendeld.
### Hoe kan ik de beveiliging van een werkblad opheffen?
Om de beveiliging van een werkblad op te heffen, gebruikt u de `Unprotect()` methode, waarbij optioneel het wachtwoord wordt verstrekt als er een wachtwoord is ingesteld tijdens de beveiliging.
### Kan ik Aspose.Cells gebruiken voor andere Excel-bewerkingen, zoals het toevoegen van formules of grafieken?
Absoluut! Aspose.Cells is een robuuste bibliotheek waarmee u een breed scala aan Excel-bewerkingen kunt uitvoeren, waaronder het toevoegen van formules, het maken van grafieken en nog veel meer.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}