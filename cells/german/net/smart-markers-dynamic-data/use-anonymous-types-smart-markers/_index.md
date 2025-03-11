---
title: Verwenden Sie anonyme Typen mit intelligenten Markierungen Aspose.Cells
linktitle: Verwenden Sie anonyme Typen mit intelligenten Markierungen Aspose.Cells
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie anonyme Typen mit intelligenten Markierungen in Aspose.Cells für die dynamische Excel-Berichterstellung in .NET verwenden. Folgen Sie unserer einfachen Anleitung.
weight: 17
url: /de/net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Verwenden Sie anonyme Typen mit intelligenten Markierungen Aspose.Cells

## Einführung
Wenn es um die Generierung dynamischer Excel-Berichte in .NET-Anwendungen geht, ist Aspose.Cells ein leistungsstarkes Tool. Eine seiner besten Funktionen ist die Möglichkeit, mit intelligenten Markierungen und anonymen Typen zu arbeiten. Wenn Sie mit diesem Konzept noch nicht vertraut sind, machen Sie sich keine Sorgen! In diesem Handbuch erfahren Sie alles, was Sie wissen müssen, von den Voraussetzungen bis hin zu praktischen Beispielen. Dabei ist es spannend und leicht verständlich.
## Voraussetzungen
Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie alles haben, was Sie zum reibungslosen Ausführen der Beispiele in diesem Tutorial benötigen.
### 1. .NET-Umgebung
Stellen Sie sicher, dass auf Ihrem lokalen Computer eine funktionierende .NET-Umgebung eingerichtet ist. Sie können Visual Studio oder eine andere IDE Ihrer Wahl verwenden.
### 2. Aspose.Cells-Bibliothek
 Sie benötigen die Aspose.Cells-Bibliothek. Wenn Sie sie noch nicht heruntergeladen haben, finden Sie sie ganz einfach[Hier](https://releases.aspose.com/cells/net/) Sie können es auch mit einer kostenlosen Testversion ausprobieren, die unter verfügbar ist[dieser Link](https://releases.aspose.com/).
### 3. Grundkenntnisse in C#
Grundlegende Kenntnisse der C#-Programmierung erleichtern Ihnen die Navigation durch das Tutorial. Wenn Ihnen Begriffe wie Klassen, Objekte und Eigenschaften vertraut sind, können Sie loslegen!
## Pakete importieren
Um die Aspose.Cells-Bibliothek in Ihrem Projekt zu verwenden, müssen Sie die zugehörigen Namespaces importieren. Fügen Sie oben in Ihrer C#-Datei die folgenden using-Direktiven hinzu:
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
Über diese Namespaces erhalten Sie Zugriff auf alle erforderlichen Klassen und Methoden, die später besprochen werden.
Kommen wir nun zum Kern des Tutorials! Sie erfahren, wie Sie mithilfe einer benutzerdefinierten Klasse eine Excel-Datei mit intelligenten Markierungen erstellen. Keine Sorge, wir unterteilen alles in überschaubare Schritte!
## Schritt 1: Erstellen Sie eine benutzerdefinierte Klasse
Zunächst benötigen wir eine einfache Klasse zur Darstellung der Daten, die wir unserer Excel-Datei hinzufügen möchten. Diese Klasse enthält Informationen über eine Person.
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
 Hier definieren wir eine Klasse namens`Person` mit zwei Eigenschaften,`Name` Und`Age`. Der Konstruktor initialisiert diese Eigenschaften. 
## Schritt 2: Einrichten des Arbeitsmappen-Designers
 Als nächstes erstellen wir eine Instanz des`WorkbookDesigner`Klasse, die wir verwenden, um unsere Excel-Datei mit intelligenten Markierungen zu gestalten.
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
// Instanziieren Sie das Arbeitsmappen-Designerobjekt.
WorkbookDesigner report = new WorkbookDesigner();
```
 Ersetzen`"Your Document Directory"` durch Ihren tatsächlichen Dateipfad, in dem Sie die Excel-Datei speichern möchten.`WorkbookDesigner` Die Klasse ist das Herzstück dieser Operation. Hier definieren Sie Ihre Vorlage.
## Schritt 3: Markierungen zu Zellen hinzufügen
Jetzt müssen wir dem Arbeitsblatt Smartmarker hinzufügen. Diese Marker dienen als Platzhalter für die Daten, die wir später eingeben.
```csharp
// Holen Sie sich das erste Arbeitsblatt aus der Arbeitsmappe.
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
// Geben Sie den Zellen einige Markierungen ein.
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
 Wir bestimmen das erste Arbeitsblatt und legen Werte für die Kopfzellen fest. Die Smartmarker erhalten das Präfix`&=` Dies teilt Aspose mit, dass es sich hierbei um Platzhalter für später einzufügende Daten handelt.
## Schritt 4: Erstellen Sie eine Personenliste
 Erstellen wir nun eine Liste von Personen mit unserem`Person` Klasse, die wir zum Auffüllen der Smartmarker verwenden werden.
```csharp
// Instanziieren Sie die Listensammlung basierend auf der benutzerdefinierten Klasse.
IList<Person> list = new List<Person>();
// Geben Sie mithilfe des benutzerdefinierten Klassenobjekts Werte für die Markierungen an.
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
 Wir erstellen eine Liste und fügen Instanzen von hinzu`Person`dazu. Diese Liste dient uns als Datenquelle beim Ausfüllen der Excel-Vorlage.
## Schritt 5: Datenquelle und Prozessmarkierungen festlegen
 Nachdem wir unsere Liste fertig haben, müssen wir sie als Datenquelle für unsere`WorkbookDesigner` Instanz und verarbeiten Sie dann die Markierungen.
```csharp
// Legen Sie die Datenquelle fest.
report.SetDataSource("MyProduct", list);
// Verarbeiten Sie die Markierungen.
report.Process(false);
```
 Der`SetDataSource` Methode verknüpft unsere zuvor definierte Liste mit den Markern. Die`Process` Methode ersetzt die Smartmarker im Arbeitsbuch durch tatsächliche Werte aus unseren Objekten.
## Schritt 6: Speichern Sie die Excel-Datei
Abschließend speichern wir die geänderte Arbeitsmappe in unserem angegebenen Verzeichnis.
```csharp
// Speichern Sie die Excel-Datei.
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
Diese Zeile speichert die Arbeitsmappe im angegebenen Dateipfad. Sie können diese Datei mit Excel öffnen, um die eingefügten Daten anzuzeigen.
## Abschluss
Und da haben Sie es! Sie haben erfolgreich eine Excel-Datei mit intelligenten Markierungen in Aspose.Cells mit Ihrer eigenen benutzerdefinierten Klasse erstellt. Diese Methode macht nicht nur Ihre Datenverwaltung dynamischer, sondern hält auch Ihren Code sauber und organisiert.
Egal, ob Sie Berichte für Analysen, Tracking-Informationen oder andere datenbezogene Aufgaben erstellen, intelligente Markierungen sind Ihr Verbündeter, um Excel-Berichte handlicher und flexibler zu gestalten!
## Häufig gestellte Fragen
### Was sind Smartmarker in Aspose.Cells?
Smartmarker sind spezielle Platzhalter in Ihrem Excel-Dokument, die Ihnen das dynamische Einfügen von Daten zur Laufzeit ermöglichen.
### Kann ich anonyme Typen für Smartmarker verwenden?
Ja! Smartmarker können mit jedem Objekttyp verwendet werden, einschließlich anonymer Typen, solange sie der erwarteten Datenstruktur entsprechen.
### Ist die Nutzung von Aspose.Cells kostenlos?
Aspose.Cells ist ein kostenpflichtiges Produkt, aber Sie können mit einer kostenlosen Testversion beginnen, um seine Funktionen kennenzulernen.
### Welche Dateiformate unterstützt Aspose.Cells?
Es unterstützt eine Vielzahl von Dateiformaten, darunter XLS, XLSX, CSV und mehr.
### Wo finde ich weitere Informationen zu Aspose.Cells?
 Weitere Einzelheiten finden Sie im[Dokumentation](https://reference.aspose.com/cells/net/) oder besuchen Sie die[Support-Forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
