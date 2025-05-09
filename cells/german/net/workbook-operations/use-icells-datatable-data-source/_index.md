---
"description": "Erfahren Sie, wie Sie ICellsDataTableDataSource mit Aspose.Cells für .NET verwenden, um Excel-Tabellen dynamisch zu füllen. Perfekt für die Automatisierung von Kundendaten in Arbeitsmappen."
"linktitle": "Verwenden von ICellsDataTableDataSource für den Workbook Designer"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Verwenden von ICellsDataTableDataSource für den Workbook Designer"
"url": "/de/net/workbook-operations/use-icells-datatable-data-source/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Verwenden von ICellsDataTableDataSource für den Workbook Designer

## Einführung
Die Erstellung komplexer Tabellenkalkulationen mit automatisierter Datenintegration kann insbesondere bei Geschäftsanwendungen bahnbrechend sein. In diesem Tutorial erfahren Sie, wie Sie `ICellsDataTableDataSource` für einen Arbeitsmappen-Designer in Aspose.Cells für .NET. Wir führen Sie durch die Erstellung einer einfachen, lesbaren Lösung zum dynamischen Laden benutzerdefinierter Daten in eine Excel-Datei. Wenn Sie also mit Kundenlisten, Verkaufsdaten oder Ähnlichem arbeiten, ist dieser Leitfaden genau das Richtige für Sie!
## Voraussetzungen
Stellen Sie zunächst sicher, dass Sie über Folgendes verfügen:
- Aspose.Cells für .NET-Bibliothek – Sie können es herunterladen von [Hier](https://releases.aspose.com/cells/net/) oder holen Sie sich eine kostenlose Testversion.
- .NET-Entwicklungsumgebung – Visual Studio ist eine gute Wahl.
- Grundlegende Kenntnisse in C# – Kenntnisse in Klassen und Datenverarbeitung helfen Ihnen, den Schritten zu folgen.
Bevor wir fortfahren, stellen Sie sicher, dass Ihre Entwicklungsumgebung mit den erforderlichen Paketen eingerichtet ist.
## Pakete importieren
Um Aspose.Cells effektiv nutzen zu können, müssen Sie wichtige Pakete importieren. Nachfolgend finden Sie eine Kurzübersicht der erforderlichen Namespaces:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Schritt 1: Definieren einer Kundendatenklasse
Erstellen Sie zunächst eine einfache `Customer` Klasse. Diese Klasse enthält grundlegende Kundendaten wie `FullName` Und `Address`Betrachten Sie es als eine Möglichkeit, die „Form“ Ihrer Daten zu definieren.
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
## Schritt 2: Einrichten der Kundenlistenklasse
Definieren Sie als Nächstes eine `CustomerList` Klasse, die erweitert `ArrayList`Diese benutzerdefinierte Liste enthält Instanzen von `Customer` und erlauben Sie den indizierten Zugriff auf jeden Eintrag.
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
In diesem Schritt verpacken wir unsere Daten in ein Format, das Aspose.Cells erkennen und verarbeiten kann.
## Schritt 3: Erstellen der Kundendatenquellenklasse
Hier wird es interessant. Wir erstellen eine `CustomerDataSource` Klasse, die implementiert `ICellsDataTable` um unsere Daten mit dem Arbeitsmappen-Designer von Aspose.Cells kompatibel zu machen.
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
Dieser Brauch `CustomerDataSource` Klasse ermöglicht es Aspose.Cells, jede `Customer` Objekt als Zeile in der Excel-Datei.
## Schritt 4: Initialisieren der Kundendaten
Fügen wir nun einige Kunden zu unserer Liste hinzu. Hier laden wir die Daten, die in die Arbeitsmappe geschrieben werden sollen. Sie können bei Bedarf gerne weitere Einträge hinzufügen.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
In diesem Beispiel arbeiten wir mit einem kleinen Datensatz. Sie können diese Liste jedoch problemlos erweitern, indem Sie Daten aus einer Datenbank oder anderen Quellen laden.
## Schritt 5: Laden Sie die Arbeitsmappe
Öffnen wir nun eine vorhandene Excel-Arbeitsmappe, die die erforderlichen Smart Marker enthält. Diese Arbeitsmappe dient als Vorlage, und Aspose.Cells ersetzt die Smart Marker dynamisch durch die Kundendaten.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
Stellen Sie sicher, dass `"SmartMarker1.xlsx"` enthält Platzhalter wie `&=Customer.FullName` Und `&=Customer.Address` wo Daten eingetragen werden sollen.
## Schritt 6: Einrichten des Arbeitsmappen-Designers
Konfigurieren wir nun den Arbeitsmappen-Designer, um unsere Kundendatenquelle mit den Smart Markers der Arbeitsmappe zu verknüpfen.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
Der `SetDataSource` Methode verbindet unsere `CustomerDataSource` zu den Smart Markern in der Arbeitsmappe. Jeder Marker mit der Bezeichnung `&=Customer` in Excel werden nun durch die entsprechenden Kundendaten ersetzt.
## Schritt 7: Verarbeiten und Speichern der Arbeitsmappe
Lassen Sie uns abschließend die Arbeitsmappe verarbeiten, um die Daten einzutragen und die Ergebnisse zu speichern.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Dieser Code löst die Smart Marker-Verarbeitung aus, ersetzt alle Platzhalter durch Daten und speichert das Ergebnis als `dest.xlsx`.
## Abschluss
Herzlichen Glückwunsch! Sie haben erfolgreich implementiert `ICellsDataTableDataSource` für einen Arbeitsmappen-Designer mit Aspose.Cells für .NET. Dieser Ansatz eignet sich ideal für die Automatisierung der Datenbefüllung in Tabellenkalkulationen, insbesondere bei dynamischen Daten wie Kundenlisten oder Produktbeständen. Mit diesen Kenntnissen sind Sie auf dem besten Weg, datengesteuerte Anwendungen zu erstellen, die Excel-basiertes Reporting zum Kinderspiel machen!
## Häufig gestellte Fragen
### Was ist `ICellsDataTable` in Aspose.Cells?  
Es handelt sich um eine Schnittstelle, die die Verknüpfung benutzerdefinierter Datenquellen mit Aspose.Cells Smart Markers zur dynamischen Datenauffüllung ermöglicht.
### Wie kann ich Daten in der Arbeitsmappenvorlage anpassen?  
Platzhalter, sogenannte Smart Marker, wie zum Beispiel `&=Customer.FullName`, verwendet. Diese Markierungen werden bei der Verarbeitung durch echte Daten ersetzt.
### Ist Aspose.Cells für .NET kostenlos?  
Aspose.Cells bietet eine kostenlose Testversion an, für den vollständigen Zugriff ist jedoch eine kostenpflichtige Lizenz erforderlich. Überprüfen Sie deren [kostenlose Testversion](https://releases.aspose.com/) oder [kaufen](https://purchase.aspose.com/buy) Optionen.
### Kann ich dynamisch weitere Kundendaten hinzufügen?  
Absolut! Füllen Sie einfach die `CustomerList` mit zusätzlichen Einträgen vor dem Ausführen des Programms.
### Wo bekomme ich Hilfe, wenn ich nicht weiterkomme?  
Aspose hat eine [Support-Forum](https://forum.aspose.com/c/cells/9) Hier können Benutzer Fragen stellen und Unterstützung von der Community und dem Aspose-Team erhalten.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}