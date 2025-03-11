---
title: Använd ICellsDataTableDataSource för Workbook Designer
linktitle: Använd ICellsDataTableDataSource för Workbook Designer
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig att använda ICellsDataTableDataSource med Aspose.Cells för .NET för att dynamiskt fylla i Excel-ark. Perfekt för att automatisera kunddata i arbetsböcker.
weight: 21
url: /sv/net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Använd ICellsDataTableDataSource för Workbook Designer

## Introduktion
 Att skapa avancerade kalkylblad med automatiserad dataintegration kan vara en förändring, särskilt i affärsapplikationer. I den här handledningen kommer vi att dyka in i hur man använder`ICellsDataTableDataSource`för en arbetsboksdesigner i Aspose.Cells för .NET. Vi guidar dig genom att bygga en enkel, läsbar lösning för att ladda anpassade data till en Excel-fil dynamiskt. Så om du arbetar med kundlistor, försäljningsdata eller något liknande är den här guiden för dig!
## Förutsättningar
För att komma igång, se till att du har följande:
-  Aspose.Cells för .NET Library – Du kan ladda ner det från[här](https://releases.aspose.com/cells/net/) eller få en gratis testversion.
- .NET-utvecklingsmiljö – Visual Studio är ett utmärkt val.
- Grundläggande förståelse för C# – Förtrogenhet med klasser och datahantering hjälper dig att följa med.
Innan vi fortsätter, se till att din utvecklingsmiljö är konfigurerad med nödvändiga paket.
## Importera paket
För att använda Aspose.Cells effektivt måste du importera viktiga paket. Nedan finns en snabbreferens för de nödvändiga namnrymden:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Steg 1: Definiera en kunddataklass
 För att börja, skapa en enkel`Customer` klass. Denna klass kommer att innehålla grundläggande kundinformation som`FullName` och`Address`Se det som ett sätt att definiera "formen" på din data.
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
## Steg 2: Ställ in kundlistaklassen
 Därefter definierar du a`CustomerList` klass som sträcker sig`ArrayList` . Denna anpassade lista kommer att innehålla instanser av`Customer` och tillåt indexerad åtkomst till varje post.
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
I det här steget lindar vi in vår data i ett format som Aspose.Cells kan känna igen och bearbeta.
## Steg 3: Skapa klassen Customer Data Source
 Det är här saker och ting blir intressanta. Vi skapar en`CustomerDataSource` klass genomförande`ICellsDataTable` för att göra våra data kompatibla med Aspose.Cells arbetsboksdesigner.
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
 Denna sed`CustomerDataSource` klass gör det möjligt för Aspose.Cells att tolka var och en`Customer` objekt som en rad i Excel-filen.
## Steg 4: Initiera kunddata
Nu ska vi lägga till några kunder till vår lista. Det är här vi laddar in data som ska skrivas in i arbetsboken. Lägg gärna till fler poster vid behov.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
det här exemplet arbetar vi med en liten datauppsättning. Du kan dock enkelt utöka listan genom att ladda data från en databas eller andra källor.
## Steg 5: Ladda arbetsboken
Låt oss nu öppna en befintlig Excel-arbetsbok som innehåller de nödvändiga smarta markörerna. Den här arbetsboken kommer att fungera som vår mall, och Aspose.Cells kommer dynamiskt att ersätta Smart Markers med kunddata.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
 Se till att`"SmartMarker1.xlsx"` innehåller platshållare som`&=Customer.FullName` och`&=Customer.Address` där uppgifterna ska fyllas i.
## Steg 6: Konfigurera arbetsboksdesignern
Låt oss nu konfigurera arbetsboksdesignern för att länka vår kunddatakälla med arbetsbokens smarta markeringar.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
 De`SetDataSource` metod binder vår`CustomerDataSource` till de smarta markörerna i arbetsboken. Varje markör märkt`&=Customer` i Excel kommer nu att ersättas av motsvarande kunddata.
## Steg 7: Bearbeta och spara arbetsboken
Låt oss slutligen bearbeta arbetsboken för att fylla i data och spara resultaten.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Denna kod utlöser Smart Marker-bearbetningen, ersätter alla platshållare med data och sparar resultatet som`dest.xlsx`.
## Slutsats
 Grattis! Du har framgångsrikt implementerat`ICellsDataTableDataSource` för en arbetsboksdesigner som använder Aspose.Cells för .NET. Det här tillvägagångssättet är idealiskt för att automatisera datapopulationen i kalkylblad, särskilt när det handlar om dynamiska data som kundlistor eller produktlager. Med dessa färdigheter är du på god väg att bygga datadrivna applikationer som gör Excel-baserad rapportering till en vind!
## FAQ's
###  Vad är`ICellsDataTable` in Aspose.Cells?  
Det är ett gränssnitt som gör att anpassade datakällor kan länkas med Aspose.Cells Smart Markers för dynamisk datapopulation.
### Hur kan jag anpassa data i arbetsboksmallen?  
 Platshållare som kallas smarta markörer, som t.ex`&=Customer.FullName`, används. Dessa markörer ersätts med riktiga data under bearbetningen.
### Är Aspose.Cells för .NET gratis?  
 Aspose.Cells erbjuder en gratis provperiod, men full åtkomst kräver en betald licens. Kolla deras[gratis provperiod](https://releases.aspose.com/) eller[köpa](https://purchase.aspose.com/buy) alternativ.
### Kan jag lägga till mer kunddata dynamiskt?  
 Absolut! Befolka helt enkelt`CustomerList`med ytterligare poster innan programmet körs.
### Var kan jag få hjälp om jag kör fast?  
 Aspose har en[supportforum](https://forum.aspose.com/c/cells/9) där användare kan ställa frågor och få hjälp från communityn och Aspose-teamet.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
