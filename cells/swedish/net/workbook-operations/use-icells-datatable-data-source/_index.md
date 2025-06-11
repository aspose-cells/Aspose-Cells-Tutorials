---
"description": "Lär dig använda ICellsDataTableDataSource med Aspose.Cells för .NET för att dynamiskt fylla i Excel-ark. Perfekt för att automatisera kunddata i arbetsböcker."
"linktitle": "Använd ICellsDataTableDataSource för arbetsboksdesignern"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Använd ICellsDataTableDataSource för arbetsboksdesignern"
"url": "/sv/net/workbook-operations/use-icells-datatable-data-source/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Använd ICellsDataTableDataSource för arbetsboksdesignern

## Introduktion
Att skapa avancerade kalkylblad med automatiserad dataintegration kan vara banbrytande, särskilt i affärsapplikationer. I den här handledningen går vi in på hur man använder `ICellsDataTableDataSource` för en arbetsboksdesigner i Aspose.Cells för .NET. Vi guidar dig genom hur du bygger en enkel, läsbar lösning för att dynamiskt ladda anpassad data till en Excel-fil. Så om du arbetar med kundlistor, försäljningsdata eller något liknande är den här guiden för dig!
## Förkunskapskrav
För att komma igång, se till att du har följande:
- Aspose.Cells för .NET-biblioteket – Du kan ladda ner det från [här](https://releases.aspose.com/cells/net/) eller hämta en gratis provversion.
- .NET-utvecklingsmiljö – Visual Studio är ett bra val.
- Grundläggande förståelse för C# – Bekantskap med klasser och datahantering hjälper dig att hänga med.
Innan vi fortsätter, se till att din utvecklingsmiljö är konfigurerad med nödvändiga paket.
## Importera paket
För att använda Aspose.Cells effektivt måste du importera viktiga paket. Nedan följer en snabbreferens för de namnrymder som krävs:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Steg 1: Definiera en kunddataklass
För att börja, skapa en enkel `Customer` klass. Den här klassen kommer att innehålla grundläggande kundinformation som `FullName` och `Address`Tänk på det som ett sätt att definiera "formen" på dina data.
```csharp
public class Customer
{
    public Customer(string aFullName, string anAddress)
    {
        FullName = aFullName;
        Address = anAddress;
    }
    public string FullName { get; set; }
    public string Address { get; set; }
}
```
## Steg 2: Konfigurera kundlisteklassen
Definiera sedan en `CustomerList` klass som sträcker sig `ArrayList`Den här anpassade listan kommer att innehålla instanser av `Customer` och tillåta indexerad åtkomst till varje post.
```csharp
public class CustomerList : ArrayList
{
    public new Customer this[int index]
    {
        get { return (Customer)base[index]; }
        set { base[index] = value; }
    }
}
```
I det här steget paketerar vi in våra data i ett format som Aspose.Cells kan känna igen och bearbeta.
## Steg 3: Skapa kunddatakällklassen
Det är här det blir intressant. Vi skapar en `CustomerDataSource` klassimplementering `ICellsDataTable` för att göra våra data kompatibla med Aspose.Cells arbetsboksdesigner.
```csharp
public class CustomerDataSource : ICellsDataTable
{
    internal string[] m_Columns;
    internal ICollection m_DataSource;
    private Hashtable m_PropHash;
    private IEnumerator m_IEnumerator;
    private PropertyInfo[] m_Properties;
    public CustomerDataSource(CustomerList customers)
    {
        this.m_DataSource = customers;
        this.m_Properties = customers[0].GetType().GetProperties();
        this.m_Columns = new string[this.m_Properties.Length];
        this.m_PropHash = new Hashtable(this.m_Properties.Length);
        for (int i = 0; i < m_Properties.Length; i++)
        {
            this.m_Columns[i] = m_Properties[i].Name;
            this.m_PropHash.Add(m_Properties[i].Name, m_Properties[i]);
        }
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public string[] Columns => this.m_Columns;
    public int Count => this.m_DataSource.Count;
    public void BeforeFirst()
    {
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public object this[int index] => this.m_Properties[index].GetValue(this.m_IEnumerator.Current, null);
    public object this[string columnName] => ((PropertyInfo)this.m_PropHash[columnName]).GetValue(this.m_IEnumerator.Current, null);
    public bool Next()
    {
        if (this.m_IEnumerator == null)
            return false;
        return this.m_IEnumerator.MoveNext();
    }
}
```
Denna sedvänja `CustomerDataSource` klassen gör det möjligt för Aspose.Cells att tolka varje `Customer` objektet som en rad i Excel-filen.
## Steg 4: Initiera kunddata
Nu ska vi lägga till några kunder i vår lista. Det är här vi laddar in data som ska skrivas in i arbetsboken. Lägg gärna till fler poster efter behov.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
det här exemplet arbetar vi med en liten datamängd. Du kan dock enkelt utöka listan genom att ladda data från en databas eller andra källor.
## Steg 5: Läs in arbetsboken
Nu ska vi öppna en befintlig Excel-arbetsbok som innehåller de nödvändiga smarta markörerna. Arbetsboken kommer att fungera som vår mall, och Aspose.Cells kommer dynamiskt att ersätta smarta markörer med kunddata.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
Se till att `"SmartMarker1.xlsx"` innehåller platsmarkörer som `&=Customer.FullName` och `&=Customer.Address` var uppgifterna ska fyllas i.
## Steg 6: Konfigurera arbetsboksdesignern
Nu ska vi konfigurera arbetsboksdesignern för att länka vår kunddatakälla till arbetsbokens smarta markörer.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
De `SetDataSource` metoden binder vår `CustomerDataSource` till de smarta markörerna i arbetsboken. Varje markör är märkt `&=Customer` i Excel kommer nu att ersättas av motsvarande kunddata.
## Steg 7: Bearbeta och spara arbetsboken
Slutligen, låt oss bearbeta arbetsboken för att fylla i data och spara resultaten.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Den här koden utlöser bearbetningen av den smarta markern, ersätter alla platshållare med data och sparar resultatet som `dest.xlsx`.
## Slutsats
Grattis! Du har implementerat `ICellsDataTableDataSource` för en arbetsboksdesigner som använder Aspose.Cells för .NET. Denna metod är idealisk för att automatisera datainsamling i kalkylblad, särskilt när man hanterar dynamisk data som kundlistor eller produktlager. Med dessa färdigheter är du på god väg att bygga datadrivna applikationer som gör Excel-baserad rapportering till en barnlek!
## Vanliga frågor
### Vad är `ICellsDataTable` i Aspose.Cells?  
Det är ett gränssnitt som gör det möjligt att länka anpassade datakällor med Aspose.Cells Smart Markers för dynamisk datapopulation.
### Hur kan jag anpassa data i arbetsboksmallen?  
Platshållare som kallas smarta markörer, till exempel `&=Customer.FullName`, används. Dessa markörer ersätts med verkliga data under bearbetningen.
### Är Aspose.Cells för .NET gratis?  
Aspose.Cells erbjuder en gratis provperiod, men fullständig åtkomst kräver en betald licens. Kolla deras [gratis provperiod](https://releases.aspose.com/) eller [köpa](https://purchase.aspose.com/buy) alternativ.
### Kan jag lägga till mer kunddata dynamiskt?  
Absolut! Fyll bara i `CustomerList` med ytterligare poster innan programmet körs.
### Var kan jag få hjälp om jag har kört fast?  
Aspose har en [supportforum](https://forum.aspose.com/c/cells/9) där användare kan ställa frågor och få hjälp från communityn och Aspose-teamet.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}