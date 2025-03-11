---
title: Digitale handtekening toevoegen aan een reeds ondertekend Excel-bestand
linktitle: Digitale handtekening toevoegen aan een reeds ondertekend Excel-bestand
second_title: Aspose.Cells voor .NET API-referentie
description: Leer hoe u een digitale handtekening toevoegt aan een reeds ondertekend Excel-bestand met Aspose.Cells voor .NET met deze gedetailleerde stapsgewijze handleiding.
weight: 30
url: /nl/net/excel-workbook/add-digital-signature-to-an-already-signed-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Digitale handtekening toevoegen aan een reeds ondertekend Excel-bestand

## Invoering

In de digitale wereld van vandaag is het beveiligen van documenten belangrijker dan ooit. Digitale handtekeningen bieden een manier om de authenticiteit en integriteit van uw bestanden te garanderen, vooral bij het omgaan met gevoelige informatie. Als u met Excel-bestanden werkt en een nieuwe digitale handtekening wilt toevoegen aan een werkmap die al is ondertekend, bent u hier aan het juiste adres! In deze gids leiden we u door het proces van het toevoegen van een digitale handtekening aan een al ondertekend Excel-bestand met behulp van Aspose.Cells voor .NET. Dus laten we erin duiken!

## Vereisten

Voordat we in de details van het coderen duiken, zijn er een paar dingen die je moet regelen:

1.  Aspose.Cells voor .NET: Zorg ervoor dat u de Aspose.Cells-bibliotheek in uw .NET-project hebt geïnstalleerd. U kunt deze downloaden van de[plaats](https://releases.aspose.com/cells/net/).
2.  Certificaatbestand: U hebt een geldig certificaatbestand nodig (meestal een`.pfx`bestand) dat uw digitale certificaat bevat. Zorg ervoor dat u het wachtwoord voor dit bestand weet.
3. Ontwikkelomgeving: stel uw ontwikkelomgeving in met Visual Studio of een andere IDE die .NET ondersteunt.
4. Basiskennis van C#: Kennis van C#-programmering helpt u de cursus soepel te volgen.
5. Voorbeeldbestanden: Heb een voorbeeld Excel-bestand dat al digitaal is ondertekend. Dit is het bestand waaraan u een nieuwe handtekening toevoegt.

Nu alles op zijn plaats staat, kunnen we beginnen met coderen!

## Pakketten importeren

Om te beginnen moet u de benodigde pakketten importeren in uw C#-bestand. Dit is hoe u dat doet:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Met deze naamruimten kunt u naadloos met Excel-bestanden werken en digitale handtekeningen verwerken.

## Stap 1: Stel uw bron- en uitvoermappen in

Voordat u uw Excel-bestanden kunt bewerken, moet u definiëren waar uw bronbestanden zich bevinden en waar u het uitvoerbestand wilt opslaan. Dit is hoe u dat doet:

```csharp
// Bron directory
string sourceDir = "Your Document Directory";
// Uitvoermap
string outputDir = "Your Document Directory";
```

In deze stap gebruiken we een methode om de paden voor de bron- en uitvoerdirectory's te verkrijgen. Zorg ervoor dat deze directory's bestaan en de vereiste bestanden bevatten.

## Stap 2: Laad de reeds ondertekende werkmap

 Vervolgens moet u de Excel-werkmap laden die u wilt wijzigen. Dit doet u door een exemplaar van de`Workbook` klasse en het pad van het ondertekende bestand doorgeven.

```csharp
// Laad de werkmap die al digitaal is ondertekend
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```

 Hier laden we de werkmap met de naam`sampleDigitallySignedByCells.xlsx`Zorg ervoor dat dit bestand al ondertekend is.

## Stap 3: Maak een digitale handtekeningencollectie

Laten we nu een digitale handtekeningencollectie maken. Deze collectie bevat alle digitale handtekeningen die u aan de werkmap wilt toevoegen.

```csharp
// Creëer de digitale handtekeningencollectie
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```

Deze stap is cruciaal omdat u hiermee indien nodig meerdere handtekeningen kunt beheren.

## Stap 4: Maak een nieuw certificaat

 U moet uw certificaatbestand laden om een nieuwe digitale handtekening te maken. Hier geeft u het pad naar uw`.pfx` bestand en het wachtwoord.

```csharp
// Certificaatbestand en het wachtwoord ervan
string certFileName = sourceDir + "AsposeDemo.pfx";
string password = "aspose";

// Nieuw certificaat aanmaken
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```

 Zorg ervoor dat u vervangt`AsposeDemo.pfx`en het wachtwoord met uw werkelijke certificaatbestandsnaam en wachtwoord.

## Stap 5: De digitale handtekening maken

Met het certificaat in de hand kunt u nu een digitale handtekening maken. U wilt ook een reden voor de handtekening opgeven en de huidige datum en tijd.

```csharp
// Maak een nieuwe digitale handtekening en voeg deze toe aan de digitale handtekeningenverzameling
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
```

Met deze stap voegt u de nieuwe handtekening toe aan uw verzameling. Deze handtekening past u later toe op de werkmap.

## Stap 6: Voeg de digitale handtekeningenverzameling toe aan de werkmap

Nu is het tijd om de digitale handtekeningencollectie toe te voegen aan de werkmap. Dit is waar de magie gebeurt!

```csharp
// Digitale handtekeningenverzameling toevoegen in de werkmap
workbook.AddDigitalSignature(dsCollection);
```

Door deze regel uit te voeren, koppelt u de nieuwe digitale handtekening feitelijk aan de reeds ondertekende werkmap.

## Stap 7: Sla de werkmap op en gooi deze weg

Tot slot wilt u de gewijzigde werkmap opslaan in uw uitvoermap en alle gebruikte bronnen vrijgeven.

```csharp
//Sla de werkmap op en gooi deze weg.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```

Met deze stap zorgt u ervoor dat uw wijzigingen worden opgeslagen en dat de werkmap op de juiste manier wordt verwijderd om bronnen vrij te maken.

## Stap 8: Bevestig de uitvoering

Om het af te ronden, is het een goed idee om te bevestigen dat uw code succesvol is uitgevoerd. U kunt dit doen met een eenvoudig consolebericht.

```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```

Hiermee krijgt u de feedback dat uw operatie succesvol is verlopen, en dat is altijd fijn om te zien!

## Conclusie

En daar heb je het! Je hebt succesvol een nieuwe digitale handtekening toegevoegd aan een reeds ondertekend Excel-bestand met Aspose.Cells voor .NET. Digitale handtekeningen zijn een krachtige manier om de authenticiteit van je documenten te garanderen, en nu weet je hoe je ze programmatisch kunt beheren. Of je nu werkt aan financiële documenten, contracten of gevoelige informatie, het implementeren van digitale handtekeningen kan de beveiliging en het vertrouwen verbeteren.

## Veelgestelde vragen

### Wat is een digitale handtekening?
Een digitale handtekening is een cryptografische methode waarmee de authenticiteit en integriteit van een bericht of document wordt gevalideerd.

### Kan ik meerdere digitale handtekeningen aan hetzelfde Excel-bestand toevoegen?
Ja, u kunt een verzameling digitale handtekeningen maken en meerdere handtekeningen aan dezelfde werkmap toevoegen.

### Welke formaten ondersteunt Aspose.Cells voor digitale handtekeningen?
 Aspose.Cells ondersteunt verschillende formaten, waaronder`.pfx` voor certificaten.

### Heb ik een specifieke versie van .NET nodig om Aspose.Cells te gebruiken?
 Controleer de[Aspose.Cells-documentatie](https://reference.aspose.com/cells/net/) voor compatibiliteit met uw .NET-versie.

### Hoe kan ik een tijdelijke licentie voor Aspose.Cells krijgen?
 U kunt een tijdelijke vergunning aanvragen bij[De aankooppagina van Aspose](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
