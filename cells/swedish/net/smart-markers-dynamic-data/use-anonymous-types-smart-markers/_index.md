---
title: Använd anonyma typer med smarta markörer Aspose.Cells
linktitle: Använd anonyma typer med smarta markörer Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du använder anonyma typer med smarta markörer i Aspose.Cells för dynamisk Excel-rapportgenerering i .NET. Följ vår enkla guide.
weight: 17
url: /sv/net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Använd anonyma typer med smarta markörer Aspose.Cells

## Introduktion
När det gäller att generera dynamiska Excel-rapporter i .NET-applikationer utmärker sig Aspose.Cells som ett kraftfullt verktyg. En av dess bästa funktioner är förmågan att arbeta med smarta markörer och anonyma typer. Om du är ny på detta koncept, oroa dig inte! Den här guiden kommer att dela upp allt du behöver veta, från förutsättningar till praktiska exempel, samtidigt som den håller den engagerande och lätt att följa.
## Förutsättningar
Innan vi dyker in i koden, låt oss se till att du har allt du behöver för att smidigt köra exemplen i denna handledning.
### 1. .NET-miljö
Se till att du har en fungerande .NET-miljö inställd på din lokala dator. Du kan använda Visual Studio eller vilken annan IDE du väljer.
### 2. Aspose.Cells Library
 Du behöver Aspose.Cells-biblioteket. Om du inte har laddat ner den än kan du enkelt hitta den[här](https://releases.aspose.com/cells/net/) . Du kan också prova det med en gratis provperiod tillgänglig på[denna länk](https://releases.aspose.com/).
### 3. Grundläggande kunskaper i C#
En grundläggande förståelse för C#-programmering hjälper dig att navigera genom handledningen lättare. Om termer som klasser, objekt och egenskaper är bekanta för dig, är du bra att gå!
## Importera paket
För att använda Aspose.Cells-biblioteket i ditt projekt måste du importera de relaterade namnrymden. Lägg till följande med hjälp av direktiv överst i din C#-fil:
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
Dessa namnrymder ger dig tillgång till alla nödvändiga klasser och metoder som kommer att diskuteras senare.
Låt oss nu gå in på själva handledningen! Du kommer att se hur du skapar en Excel-fil med smarta markörer med hjälp av en anpassad klass. Oroa dig inte; vi delar upp allt i hanterbara steg!
## Steg 1: Skapa en anpassad klass
Först och främst behöver vi en enkel klass för att representera de data vi vill lägga till i vår Excel-fil. Denna klass kommer att innehålla information om en person.
```csharp
public class Person
{
    private string m_Name;
    private int m_Age;
    public string Name
    {
        get { return m_Name; }
        set { m_Name = value; }
    }
    public int Age
    {
        get { return m_Age; }
        set { m_Age = value; }
    }
    internal Person(string name, int age)
    {
        this.m_Name = name;
        this.m_Age = age;
    }
}
```
 Här definierar vi en klass som heter`Person` med två fastigheter,`Name` och`Age`. Konstruktören initierar dessa egenskaper. 
## Steg 2: Konfigurera arbetsboksdesignern
 Låt oss sedan skapa en instans av`WorkbookDesigner`klass, som vi kommer att använda för att designa vår Excel-fil med smarta markörer.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Instantiera arbetsboksdesignerobjektet.
WorkbookDesigner report = new WorkbookDesigner();
```
 Ersätta`"Your Document Directory"` med din faktiska sökväg där du vill spara Excel-filen. De`WorkbookDesigner` klass är hjärtat i denna operation, där du definierar din mall.
## Steg 3: Lägg till markörer i celler
Nu måste vi lägga till smarta markörer i kalkylbladet. Dessa markörer kommer att vara platshållare för data som vi kommer att mata in senare.
```csharp
// Skaffa det första arbetsbladet i arbetsboken.
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
// Mata in några markörer till cellerna.
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
 Vi anger det första kalkylbladet och ställer in värden för rubrikcellerna. De smarta markörerna har prefixet`&=` som säger till Aspose att dessa är platshållare för data som ska infogas senare.
## Steg 4: Skapa en lista över personer
 Låt oss nu skapa en lista över personer som använder vår`Person` klass som vi kommer att använda för att fylla i de smarta markörerna.
```csharp
// Instantiera listsamlingen baserat på den anpassade klassen.
IList<Person> list = new List<Person>();
// Ange värden för markörerna med det anpassade klassobjektet.
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
 Vi skapar en lista och lägger till instanser av`Person`till det. Den här listan fungerar som vår datakälla när du fyller i Excel-mallen.
## Steg 5: Ställ in datakälla och processmarkörer
 När vi har vår lista klar måste vi ställa in den som datakälla för vår`WorkbookDesigner` instans och bearbeta sedan markörerna.
```csharp
// Ställ in datakällan.
report.SetDataSource("MyProduct", list);
// Bearbeta markörerna.
report.Process(false);
```
 De`SetDataSource` metoden länkar vår tidigare definierade lista till markörerna. De`Process` metod ersätter de smarta markörerna i arbetsboken med faktiska värden från våra objekt.
## Steg 6: Spara Excel-filen
Slutligen kommer vi att spara den ändrade arbetsboken i vår utsedda katalog.
```csharp
// Spara excel-filen.
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
Den här raden sparar arbetsboken till den angivna sökvägen. Du kan öppna den här filen med Excel för att se infogade data.
## Slutsats
Och där har du det! Du har framgångsrikt skapat en Excel-fil med hjälp av smarta markörer i Aspose.Cells med din egen anpassade klass. Denna metod gör inte bara din datahantering mer dynamisk utan håller också din kod ren och organiserad.
Så oavsett om du genererar rapporter för analys, spårningsinformation eller någon annan datarelaterad uppgift, är smarta markörer din allierade för att göra Excel-rapporter mer hanterbara och flexibla!
## FAQ's
### Vad är smarta markörer i Aspose.Cells?
Smarta markörer är speciella platshållare i ditt Excel-dokument som låter dig infoga data dynamiskt under körning.
### Kan jag använda anonyma typer för smarta markörer?
Ja! Smarta markörer kan användas med alla objekttyper, inklusive anonyma typer, så länge de matchar den förväntade datastrukturen.
### Är Aspose.Cells gratis att använda?
Aspose.Cells är en betalprodukt, men du kan börja med en gratis provperiod för att utforska dess funktioner.
### Vilka filformat stöder Aspose.Cells?
Den stöder ett brett utbud av filformat, inklusive XLS, XLSX, CSV och mer.
### Var kan jag hitta mer information om Aspose.Cells?
 För mer information, kolla in[dokumentation](https://reference.aspose.com/cells/net/) eller besöka[supportforum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
