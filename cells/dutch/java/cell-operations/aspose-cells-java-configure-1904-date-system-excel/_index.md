---
date: '2026-02-22'
description: Leer hoe u het Excel‑datumsysteem naar 1904 wijzigt met Aspose.Cells
  voor Java, het Excel‑datumformaat instelt en het Excel‑1904‑systeem efficiënt converteert.
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: Wijzig het Excel-datumsysteem naar 1904 met Aspose.Cells Java
url: /nl/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Verander Excel‑datumsysteem naar 1904 met Aspose.Cells Java

Het beheren van historische gegevens in Excel kan uitdagend zijn omdat Excel twee verschillende datumsystemen ondersteunt. **In deze tutorial leer je hoe je het Excel‑datumsysteem naar het 1904‑formaat wijzigt met Aspose.Cells voor Java**, waardoor het omgaan met legacy‑datums moeiteloos wordt. We lopen door het initialiseren van een werkmap, het inschakelen van het 1904‑datumsysteem en het opslaan van de wijziging.

## Quick Answers
- **Wat doet het 1904‑datumsysteem?** Het telt dagen vanaf 1 januari 1904, waardoor alle datums 1462 dagen verschuiven ten opzichte van het standaard 1900‑systeem.  
- **Waarom Aspose.Cells gebruiken om het datumsysteem te wijzigen?** Het biedt een eenvoudige API die werkt zonder Excel geïnstalleerd te hebben en ondersteunt grote bestanden.  
- **Welke Java‑versies worden ondersteund?** JDK 8 of nieuwer.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor evaluatie; een licentie verwijdert gebruikslimieten.  
- **Kan ik later terugschakelen naar het 1900‑systeem?** Ja, stel gewoon `setDate1904(false)` in.

## Wat is het 1904‑datumsysteem in Excel?
Het 1904‑datumsysteem werd oorspronkelijk gebruikt door vroege Macintosh‑versies van Excel. Het telt dagen vanaf 1 januari 1904, wat nuttig is voor compatibiliteit met oudere spreadsheets en sommige financiële modellen.

## Waarom het Excel‑datumsysteem wijzigen met Aspose.Cells?
- **Cross‑platform compatibiliteit** – werkt op Windows, Linux en macOS.  
- **Geen Excel‑installatie vereist** – ideaal voor server‑side verwerking.  
- **Hoge prestaties** – verwerkt grote werkmappen met minimale geheugenbelasting.  

## Vereisten
- Java Development Kit (JDK) 8 of hoger.  
- Maven of Gradle voor dependency‑beheer.  
- Basiskennis van Java‑programmeren.  

## Instellen van Aspose.Cells voor Java

### Maven
Voeg de volgende dependency toe aan je `pom.xml`‑bestand:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Voeg deze regel toe aan je `build.gradle`‑bestand:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Licentie‑acquisitie
Aspose biedt een gratis proefversie, een tijdelijke licentie en volledige commerciële licenties. Je kunt beginnen met de [gratis proefversie](https://releases.aspose.com/cells/java/) of een tijdelijke licentie verkrijgen via de [pagina voor tijdelijke licentie](https://purchase.aspose.com/temporary-license/).

## Verander Excel‑datumsysteem met Aspose.Cells Java

Hieronder vind je de stap‑voor‑stap‑gids die daadwerkelijk **het Excel‑datumsysteem wijzigt**. Elke stap bevat een korte uitleg gevolgd door de exacte code die je nodig hebt.

### Stap 1: Initialiseer en laad de werkmap
Maak eerst een `Workbook`‑instantie die verwijst naar je bestaande Excel‑bestand.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Stap 2: Schakel het 1904‑datumsysteem in
Gebruik de werkmap‑instellingen om het datumsysteem te wijzigen.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Pro tip:** Je kunt later ook `setDate1904(false)` aanroepen als je wilt terugkeren.

### Stap 3: Sla de gewijzigde werkmap op
Schrijf tenslotte de wijzigingen naar een nieuw bestand (of overschrijf het origineel).

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Opmerking:** De bovenstaande code gebruikt de klassenaam `tWorkbook` zoals oorspronkelijk opgegeven. Zorg ervoor dat deze typefout overeenkomt met de naamgevingsconventies van je project of corrigeer deze naar `Workbook` indien nodig.

## Excel‑datum programmatisch instellen (secundaire zoekterm)
Als je individuele celwaarden moet aanpassen nadat je het systeem hebt gewijzigd, kun je `Cells.get(i, j).putValue(Date)` gebruiken; de datum wordt geïnterpreteerd volgens het actieve datumsysteem.

## Excel‑1904‑systeem terugzetten naar 1900 (secundaire zoekterm)
Om terug te keren, roep je simpelweg aan:

```java
workbook.getSettings().setDate1904(false);
```

Sla vervolgens de werkmap opnieuw op.

## Praktische toepassingen
1. **Data‑archivering** – Behoud legacy‑tijdstempels bij het migreren van oude Mac‑gebaseerde spreadsheets.  
2. **Cross‑platform rapportage** – Genereer rapporten die zowel op Windows als macOS geopend kunnen worden zonder datumverschillen.  
3. **Financiële modellering** – Stem datum‑berekeningen af op legacy‑financiële modellen die het 1904‑systeem verwachten.

## Prestatie‑overwegingen
- Beperk werkmap‑bewerkingen in één sessie om het geheugenverbruik laag te houden.  
- Gebruik Java‑garbage‑collection‑tuning voor zeer grote bestanden.  

## Veelgestelde vragen

**Q: Wat is het verschil tussen de 1900‑ en 1904‑datumsystemen?**  
A: Het 1900‑systeem start op 1 januari 1900, terwijl het 1904‑systeem start op 1 januari 1904, waardoor alle datums 1462 dagen verschuiven.

**Q: Kan ik het datumsysteem van een werkmap wijzigen die momenteel in Excel geopend is?**  
A: Ja, maar je moet het bestand eerst in Excel sluiten; anders zal de opslaan‑bewerking mislukken.

**Q: Heb ik een licentie nodig om `setDate1904` te gebruiken?**  
A: De methode werkt in de gratis proefversie, maar een volledige licentie verwijdert de evaluatie‑beperkingen.

**Q: Is het mogelijk om het datumsysteem alleen voor één werkblad te wijzigen?**  
A: Nee, het datumsysteem is een instelling op werkmapniveau; het geldt voor alle werkbladen.

**Q: Hoe kan ik verifiëren dat het datumsysteem is gewijzigd?**  
A: Open het opgeslagen bestand in Excel, ga naar **Bestand → Opties → Geavanceerd**, en controleer het vakje **"Gebruik 1904‑datumsysteem"**.

## Conclusie
Je weet nu hoe je het **Excel‑datumsysteem** naar 1904 wijzigt met Aspose.Cells voor Java, hoe je Excel‑datumnotaties instelt en hoe je terugschakelt indien nodig. Integreer deze fragmenten in je data‑verwerkings‑pijplijnen om datum‑compatibiliteit over platformen te garanderen.

---

**Laatst bijgewerkt:** 2026-02-22  
**Getest met:** Aspose.Cells 25.3 voor Java  
**Auteur:** Aspose  

**Resources**
- **Documentatie:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Download:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Licentie aanschaffen:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Gratis proefversie:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Tijdelijke licentie:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Supportforum:** [Aspose Support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}