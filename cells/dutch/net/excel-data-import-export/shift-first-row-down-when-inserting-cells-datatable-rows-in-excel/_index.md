---
title: Eerste rij naar beneden verplaatsen bij het invoegen van DataTable-rijen in Excel
linktitle: Eerste rij naar beneden verplaatsen bij het invoegen van DataTable-rijen in Excel
second_title: Aspose.Cells .NET Excel-verwerkings-API
description: Leer hoe u DataTable-rijen in Excel invoegt zonder de eerste rij naar beneden te verschuiven met Aspose.Cells voor .NET. Stapsgewijze handleiding voor moeiteloze automatisering.
weight: 11
url: /nl/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eerste rij naar beneden verplaatsen bij het invoegen van DataTable-rijen in Excel

## Invoering

Bent u het zat om handmatig rijen te verschuiven bij het invoegen van nieuwe gegevens in uw Excel-spreadsheets? Dan heeft u geluk! In dit artikel duiken we in hoe u dit proces kunt automatiseren met Aspose.Cells voor .NET. Aan het einde van deze tutorial leert u niet alleen hoe u met gegevenstabellen in Excel kunt werken, maar ook hoe u de importopties kunt aanpassen aan uw behoeften. Geloof me; dit kan u veel tijd en gedoe besparen! Pak dus een kop koffie en laten we beginnen!

## Vereisten

Voordat we beginnen met coderen, willen we ervoor zorgen dat alles is ingesteld:

1. Visual Studio: Zorg ervoor dat u Visual Studio hebt geïnstalleerd (2017 of later zou prima moeten werken).
2.  Aspose.Cells voor .NET: U moet de Aspose.Cells-bibliotheek hebben. Als u dit nog niet hebt gedaan, kunt u deze downloaden[hier](https://releases.aspose.com/cells/net/).
3. Basiskennis van C# en Excel: Een basiskennis van C#-programmering en hoe Excel werkt, helpt u zeker om de cursus effectiever te volgen.

 U zult ook een voorbeeld van een Excel-bestand bij de hand willen hebben. In deze handleiding gebruiken we een voorbeeld genaamd`sampleImportTableOptionsShiftFirstRowDown.xlsx`. U kunt dit bestand aanmaken of een sjabloon zoeken die aan uw behoeften voldoet.

## Pakketten importeren

Voordat we in de codering duiken, moeten we ervoor zorgen dat we de benodigde pakketten importeren. Neem de volgende namespaces op in uw C#-project:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Deze pakketten zijn essentieel voor het werken met de werkmap, het werkblad en de tabellen.

## Stap 1: Stel uw project in

### Een nieuw C#-project maken

Begin met het maken van een nieuwe C# Console Application in Visual Studio. Geef uw project een geschikte naam, zoals “ExcelDataImport”.

### Aspose.Cells NuGet-pakket toevoegen

Om het Aspose.Cells-pakket toe te voegen, klikt u met de rechtermuisknop op uw project in Solution Explorer, selecteert u NuGet-pakketten beheren en zoekt u naar 'Aspose.Cells'. Installeer het pakket om er zeker van te zijn dat u toegang hebt tot alle functionaliteit die we nodig hebben.

## Stap 2: Definieer de gegevenstabel

 Vervolgens implementeren we de`ICellsDataTable` interface om een klasse te maken die de te importeren gegevens levert. Hier ziet u hoe u de`CellsDataTable` klas:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... Andere leden implementeren ...
}
```

Hier definiëren we de kolomnamen en de gegevens voor elke kolom, wat de structuur van onze geïmporteerde tabel zal vergemakkelijken.

## Stap 3: ICellsDataTable-interfaceleden implementeren

 Binnen de`CellsDataTable` klasse, moet u de leden van de implementeren`ICellsDataTable` interface. Dit is de vereiste implementatie:

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

Dit onderdeel van de klasse behandelt het ophalen van gegevens, het definiëren van het aantal rijen en kolommen en het beheren van de huidige indexstatus.

## Stap 4: Schrijf de hoofdfunctie

 Laten we nu de`Run`Methode om het gehele tabelimportproces te orkestreren:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## Stap 5: Importopties instellen

 Om het importgedrag te regelen, moet u een instantie van maken`ImportTableOptions` en stel de eigenschappen dienovereenkomstig in. Meer specifiek willen we instellen`ShiftFirstRowDown` naar`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // We willen de eerste rij niet naar beneden schuiven
```

## Stap 6: Importeer de DataTable

 Nu kunnen we de gegevens importeren uit onze`CellsDataTable` in het werkblad.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

Met deze opdracht wordt uw gegevenstabel rechtstreeks ingevoegd, beginnend bij de opgegeven rij en kolom.

## Stap 7: Sla de werkmap op

Ten slotte slaan we de aangepaste werkmap weer op in een bestand:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## Conclusie

En daar heb je het! Je hebt geleerd hoe je DataTable-rijen in een Excel-sheet kunt invoegen zonder de eerste rij te verplaatsen met Aspose.Cells voor .NET. Dit proces stroomlijnt niet alleen de gegevensmanipulatie in Excel, maar verbetert ook de prestaties van je applicatie door een doorgaans omslachtige taak te automatiseren. Met deze kennis in je toolkit ben je beter toegerust om Excel-automatiseringstaken uit te voeren, wat je tijd en moeite bespaart.

## Veelgestelde vragen

### Wat is Aspose.Cells voor .NET?
Aspose.Cells voor .NET is een programmeerbibliotheek waarmee ontwikkelaars Excel-bestanden in .NET-toepassingen kunnen maken, bewerken en converteren.

### Heb ik een licentie nodig om Aspose.Cells te gebruiken?
Ja, u hebt een geldige licentie nodig voor alle functies. Er is echter een gratis proefversie beschikbaar voor de eerste tests.

### Kan ik Aspose.Cells gebruiken in webapplicaties?
Absoluut! Aspose.Cells is perfect voor desktop-, web- en cloudgebaseerde applicaties die zijn ontwikkeld in .NET.

### Welke typen Excel-bestanden kan ik maken met Aspose.Cells?
U kunt verschillende Excel-bestandsindelingen maken, waaronder XLSX, XLS, CSV en meer.

### Waar kan ik ondersteuning krijgen voor Aspose.Cells?
 U kunt vragen stellen of hulp vinden in de[Aspose-forums](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
