---
title: Voeg een opmerking met afbeelding toe in Excel
linktitle: Voeg een opmerking met afbeelding toe in Excel
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u opmerkingen aan afbeeldingen toevoegt in Excel met Aspose.Cells voor .NET. Verbeter uw spreadsheets met gepersonaliseerde annotaties.
weight: 10
url: /nl/net/excel-comment-annotation/add-comment-with-image-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Voeg een opmerking met afbeelding toe in Excel

## Invoering
Excel is een krachtig hulpmiddel voor gegevensbeheer en -analyse, maar soms moet u uw spreadsheets een persoonlijk tintje geven, toch? Misschien wilt u gegevens annoteren, feedback geven of zelfs een beetje flair toevoegen met afbeeldingen. Dan zijn opmerkingen handig! In deze tutorial gaan we onderzoeken hoe u een opmerking toevoegt aan een afbeelding in Excel met behulp van de Aspose.Cells-bibliotheek voor .NET. Deze aanpak kan met name handig zijn voor het maken van interactievere en visueel aantrekkelijkere spreadsheets.
## Vereisten
Voordat we dieper ingaan op het toevoegen van opmerkingen aan afbeeldingen in Excel, controleren we eerst of u alles bij de hand hebt om aan de slag te gaan:
1. Visual Studio: Zorg ervoor dat Visual Studio op uw computer is geïnstalleerd. Dit is waar u uw code schrijft en uitvoert.
2.  Aspose.Cells voor .NET: U moet de Aspose.Cells-bibliotheek hebben. Als u deze nog niet hebt geïnstalleerd, kunt u deze downloaden van[hier](https://releases.aspose.com/cells/net/).
3. Basiskennis van C#: Kennis van C#-programmering helpt u de codefragmenten beter te begrijpen.
4. Een afbeeldingsbestand: Zorg dat u een afbeeldingsbestand (zoals een logo) gereed hebt dat u in uw Excel-opmerking wilt insluiten. Voor deze tutorial gaan we ervan uit dat u een bestand met de naam`logo.jpg`.
5. .NET Framework: Zorg ervoor dat u .NET Framework hebt geïnstalleerd, aangezien Aspose.Cells dit nodig heeft om goed te kunnen functioneren.
Nu we de vereisten hebben besproken, kunnen we beginnen met het daadwerkelijke coderen!
## Pakketten importeren
Allereerst moeten we de benodigde pakketten importeren. Zorg ervoor dat u in uw C#-project een verwijzing naar de Aspose.Cells-bibliotheek toevoegt. U kunt dit doen met behulp van de NuGet Package Manager in Visual Studio. Dit doet u als volgt:
1. Open Visual Studio.
2. Maak een nieuw project of open een bestaand project.
3. Klik met de rechtermuisknop op uw project in de Solution Explorer.
4. Selecteer NuGet-pakketten beheren.
5. Zoek naar Aspose.Cells en installeer het.

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Zodra u de bibliotheek hebt geïnstalleerd, kunt u beginnen met het schrijven van uw code. Hier leest u hoe u dit stap voor stap doet.
## Stap 1: Stel uw documentenmap in
Om te beginnen moeten we een directory instellen waar we onze Excel-bestanden kunnen opslaan. Dit is een cruciale stap omdat we ons werk georganiseerd willen houden.
```csharp
// Het pad naar de documentenmap.
string dataDir = "Your Document Directory";
// Maak een map aan als deze nog niet bestaat.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Deze variabele bevat het pad naar uw documentenmap. Vervangen`"Your Document Directory"` met het daadwerkelijke pad waar u uw Excel-bestand wilt opslaan.
- Directory.Exists: Hiermee wordt gecontroleerd of de directory al bestaat.
- Directory.CreateDirectory: Als de directory niet bestaat, wordt deze hiermee aangemaakt.
## Stap 2: Een werkmap instantiëren
 Vervolgens moeten we een instantie van de maken`Workbook` klasse. Deze klasse vertegenwoordigt een Excel-werkmap in het geheugen.
```csharp
//Een werkmap instantiëren
Workbook workbook = new Workbook();
```
- Workbook: Dit is de hoofdklasse in Aspose.Cells waarmee u Excel-bestanden kunt maken en bewerken. Door het te instantiëren, maakt u in feite een nieuwe Excel-werkmap.
## Stap 3: Ontvang de opmerkingenverzameling
Nu we de werkmap hebben, gaan we de verzameling opmerkingen van het eerste werkblad openen.
```csharp
// Ontvang een referentie van de verzameling opmerkingen met het eerste blad
CommentCollection comments = workbook.Worksheets[0].Comments;
```
- Werkbladen[ 0]: Hiermee krijgt u toegang tot het eerste werkblad in de werkmap. Vergeet niet dat de index op nul is gebaseerd, dus`[0]` verwijst naar het eerste blad.
- Opmerkingen: Met deze eigenschap krijgen we toegang tot de verzameling opmerkingen in dat werkblad.
## Stap 4: Een opmerking toevoegen aan een cel
Laten we een opmerking toevoegen aan een specifieke cel. In dit geval voegen we een opmerking toe aan cel A1.
```csharp
// Voeg een opmerking toe aan cel A1
int commentIndex = comments.Add(0, 0);
Comment comment = comments[commentIndex];
comment.Note = "First note.";
comment.Font.Name = "Times New Roman";
```
- comments.Add(0, 0): Deze methode voegt een opmerking toe aan cel A1 (rij 0, kolom 0).
- opmerking.Let op: Hier stellen we de tekst van de opmerking in.
- comment.Font.Name: Hiermee stelt u het lettertype van de opmerkingtekst in.
## Stap 5: Laad een afbeelding in een stream
 Nu is het tijd om de afbeelding te laden die we in onze opmerking willen insluiten. We gebruiken een`MemoryStream` om de beeldgegevens vast te houden.
```csharp
// Een afbeelding in de stream laden
Bitmap bmp = new Bitmap(dataDir + "logo.jpg");
MemoryStream ms = new MemoryStream();
bmp.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
```
- Bitmap: Deze klasse wordt gebruikt om het afbeeldingsbestand te laden. Zorg ervoor dat het pad correct is.
- MemoryStream: Dit is een stream die we gebruiken om de afbeelding in het geheugen op te slaan.
- bmp.Save: Hiermee wordt de bitmapafbeelding in PNG-formaat in de geheugenstroom opgeslagen.
## Stap 6: Stel afbeeldingsgegevens in op de opmerkingenvorm
Nu moeten we de afbeeldingsgegevens instellen op de vorm die is gekoppeld aan de opmerking die we eerder hebben gemaakt.
```csharp
// Stel afbeeldingsgegevens in op de vorm die aan de opmerking is gekoppeld
comment.CommentShape.Fill.ImageData = ms.ToArray();
```
- comment.CommentShape.Fill.ImageData: Met deze eigenschap kunt u de afbeelding voor de opmerkingenvorm instellen. We converteren de`MemoryStream` naar een byte-array met behulp van`ms.ToArray()`.
## Stap 7: Sla de werkmap op
Laten we tot slot ons werkboek opslaan, inclusief de opmerkingen en de afbeelding.
```csharp
// Werkmap opslaan
workbook.Save(dataDir + "book1.out.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
- workbook.Save: Deze methode slaat de werkmap op naar het opgegeven pad. We slaan het op als een XLSX-bestand.
## Conclusie
En daar heb je het! Je hebt succesvol een opmerking met een afbeelding toegevoegd aan een Excel-bestand met Aspose.Cells voor .NET. Deze functie kan je spreadsheets informatiever en visueel aantrekkelijker maken. Of je nu gegevens annoteert, feedback geeft of gewoon een persoonlijk tintje toevoegt, opmerkingen met afbeeldingen kunnen de gebruikerservaring aanzienlijk verbeteren.
## Veelgestelde vragen
### Kan ik meerdere opmerkingen aan dezelfde cel toevoegen?
Nee, Excel staat niet meerdere opmerkingen toe in dezelfde cel. U kunt slechts één opmerking per cel hebben.
### Welke afbeeldingsformaten worden ondersteund?
Aspose.Cells ondersteunt verschillende afbeeldingsformaten, waaronder PNG, JPEG en BMP.
### Heb ik een licentie nodig om Aspose.Cells te gebruiken?
Aspose.Cells biedt een gratis proefversie aan, maar voor volledige functionaliteit moet u een licentie aanschaffen.
### Kan ik het uiterlijk van de opmerking aanpassen?
Ja, u kunt het lettertype, de grootte en de kleur van de opmerkingtekst aanpassen. U kunt ook de vorm en grootte van de opmerking zelf wijzigen.
### Waar kan ik meer documentatie over Aspose.Cells vinden?
 Uitgebreide documentatie vindt u op Aspose.Cells[hier](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
