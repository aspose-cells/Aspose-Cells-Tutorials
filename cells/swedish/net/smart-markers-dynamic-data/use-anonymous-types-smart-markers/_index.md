---
"description": "Lär dig hur du använder anonyma typer med smarta markörer i Aspose.Cells för dynamisk Excel-rapportgenerering i .NET. Följ vår enkla guide."
"linktitle": "Använd anonyma typer med smarta markörer Aspose.Cells"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Använd anonyma typer med smarta markörer Aspose.Cells"
"url": "/sv/net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Använd anonyma typer med smarta markörer Aspose.Cells

## Introduktion
När det gäller att generera dynamiska Excel-rapporter i .NET-applikationer är Aspose.Cells ett kraftfullt verktyg. En av dess bästa funktioner är möjligheten att arbeta med smarta markörer och anonyma typer. Om du är nybörjare på det här konceptet, oroa dig inte! Den här guiden kommer att bryta ner allt du behöver veta, från förkunskaper till praktiska exempel, samtidigt som den är engagerande och lätt att följa.
## Förkunskapskrav
Innan vi går in i koden, låt oss se till att du har allt du behöver för att smidigt köra exemplen i den här handledningen.
### 1. .NET-miljö
Se till att du har en fungerande .NET-miljö konfigurerad på din lokala dator. Du kan använda Visual Studio eller någon annan IDE som du väljer.
### 2. Aspose.Cells-biblioteket
Du behöver Aspose.Cells-biblioteket. Om du inte har laddat ner det än kan du enkelt hitta det. [här](https://releases.aspose.com/cells/net/)Du kan också prova det med en gratis provperiod tillgänglig på [den här länken](https://releases.aspose.com/).
### 3. Grundläggande kunskaper i C#
Grundläggande förståelse för C#-programmering kommer att hjälpa dig att navigera genom handledningen enklare. Om termer som klasser, objekt och egenskaper är bekanta för dig är du redo att köra!
## Importera paket
För att använda Aspose.Cells-biblioteket i ditt projekt måste du importera de relaterade namnrymderna. Lägg till följande using-direktiv högst upp i din C#-fil:
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
Dessa namnrymder ger dig tillgång till alla nödvändiga klasser och metoder som kommer att diskuteras senare.
Nu ska vi gå in på kärnan i handledningen! Du får se hur du skapar en Excel-fil med smarta markörer med hjälp av en anpassad klass. Oroa dig inte, vi delar upp allt i hanterbara steg!
## Steg 1: Skapa en anpassad klass
Först behöver vi en enkel klass som representerar de data vi vill lägga till i vår Excel-fil. Den här klassen kommer att innehålla information om en person.
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
Här definierar vi en klass som heter `Person` med två fastigheter, `Name` och `Age`Konstruktorn initierar dessa egenskaper. 
## Steg 2: Konfigurera arbetsboksdesignern
Låt oss nu skapa en instans av `WorkbookDesigner` klass, som vi ska använda för att designa vår Excel-fil med smarta markörer.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Instansiera arbetsboksdesignerobjektet.
WorkbookDesigner report = new WorkbookDesigner();
```
Ersätta `"Your Document Directory"` med din faktiska sökväg till den plats där du vill spara Excel-filen. `WorkbookDesigner` klassen är hjärtat i den här operationen, där du definierar din mall.
## Steg 3: Lägg till markörer i celler
Nu behöver vi lägga till smarta markörer i kalkylbladet. Dessa markörer kommer att fungera som platshållare för de data vi matar in senare.
```csharp
// Hämta det första arbetsbladet i arbetsboken.
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
// Mata in några markörer i cellerna.
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
Vi anger det första kalkylbladet och anger värden för rubrikcellerna. De smarta markörerna har prefixet `&=` vilket berättar för Aspose att dessa är platshållare för data som ska infogas senare.
## Steg 4: Skapa en lista över personer
Nu ska vi skapa en lista över personer som använder vår `Person` klass som vi kommer att använda för att fylla i de smarta markörerna.
```csharp
// Instansiera listsamlingen baserat på den anpassade klassen.
IList<Person> list = new List<Person>();
// Ange värden för markörerna med hjälp av det anpassade klassobjektet.
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
Vi skapar en lista och lägger till instanser av `Person` till den. Den här listan fungerar som vår datakälla när vi fyller i Excel-mallen.
## Steg 5: Ställ in datakälla och processmarkörer
När vi har vår lista klar måste vi ställa in den som datakälla för vår `WorkbookDesigner` instans och sedan bearbeta markörerna.
```csharp
// Ange datakällan.
report.SetDataSource("MyProduct", list);
// Bearbeta markörerna.
report.Process(false);
```
De `SetDataSource` Metoden länkar vår tidigare definierade lista till markörerna. `Process` Metoden ersätter de smarta markörerna i arbetsboken med faktiska värden från våra objekt.
## Steg 6: Spara Excel-filen
Slutligen sparar vi den modifierade arbetsboken i vår angivna katalog.
```csharp
// Spara Excel-filen.
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
Den här raden sparar arbetsboken till den angivna sökvägen. Du kan öppna filen med Excel för att se den infogade informationen.
## Slutsats
Och där har du det! Du har skapat en Excel-fil med smarta markörer i Aspose.Cells och din egen anpassade klass. Den här metoden gör inte bara din datahantering mer dynamisk utan håller också din kod ren och organiserad.
Så oavsett om du genererar rapporter för analys, spårningsinformation eller någon annan datarelaterad uppgift, är smarta markörer din allierade för att göra Excel-rapporter mer hanterbara och flexibla!
## Vanliga frågor
### Vad är smarta markörer i Aspose.Cells?
Smarta markörer är speciella platshållare i ditt Excel-dokument som låter dig dynamiskt infoga data under körning.
### Kan jag använda anonyma typer för smarta markörer?
Ja! Smarta markörer kan användas med alla objekttyper, inklusive anonyma typer, så länge de matchar den förväntade datastrukturen.
### Är Aspose.Cells gratis att använda?
Aspose.Cells är en betalprodukt, men du kan börja med en gratis provperiod för att utforska dess funktioner.
### Vilka filformat stöder Aspose.Cells?
Den stöder ett brett utbud av filformat, inklusive XLS, XLSX, CSV och mer.
### Var kan jag hitta mer information om Aspose.Cells?
För mer information, kolla in [dokumentation](https://reference.aspose.com/cells/net/) eller besök [supportforum](https://forum.aspose.com/c/cells/9).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}