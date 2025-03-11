---
title: Stoppen Sie die Konvertierung oder das Laden mit dem Interrupt-Monitor
linktitle: Stoppen Sie die Konvertierung oder das Laden mit dem Interrupt-Monitor
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie mithilfe des Interrupt Monitors, wie Sie die Arbeitsmappenkonvertierung in Aspose.Cells für .NET stoppen – mit einem ausführlichen Schritt-für-Schritt-Tutorial.
weight: 26
url: /de/net/workbook-operations/stop-conversion-or-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Stoppen Sie die Konvertierung oder das Laden mit dem Interrupt-Monitor

## Einführung
Die Arbeit mit großen Excel-Dateien ist oft mit langwierigen Prozessen verbunden, die Zeit und Ressourcen verschlingen können. Aber was wäre, wenn Sie den Konvertierungsprozess mittendrin stoppen könnten, wenn Sie feststellen, dass etwas geändert werden muss? Aspose.Cells für .NET verfügt über eine Funktion namens Interrupt Monitor, mit der Sie die Konvertierung einer Arbeitsmappe in ein anderes Format wie PDF unterbrechen können. Dies kann lebensrettend sein, insbesondere bei der Arbeit mit umfangreichen Datendateien. In dieser Anleitung erfahren Sie, wie Sie den Konvertierungsprozess mithilfe des Interrupt Monitors in Aspose.Cells für .NET unterbrechen.
## Voraussetzungen
Stellen Sie vor dem Eintauchen sicher, dass Sie Folgendes eingerichtet haben:
1.  Aspose.Cells für .NET - Laden Sie es herunter[Hier](https://releases.aspose.com/cells/net/).
2. .NET-Entwicklungsumgebung – wie Visual Studio.
3. Grundkenntnisse der C#-Programmierung – Die Vertrautheit mit der C#-Syntax wird Ihnen beim Folgen helfen.
## Pakete importieren
Lassen Sie uns zunächst die erforderlichen Pakete importieren. Zu diesen Importen gehören:
- Aspose.Cells: Die Hauptbibliothek zur Bearbeitung von Excel-Dateien.
- System.Threading: Zur Verwaltung von Threads, da in diesem Beispiel zwei Prozesse parallel ausgeführt werden.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
Lassen Sie uns den Prozess in detaillierte Schritte unterteilen. Jeder Schritt hilft Ihnen, die Bedeutung der Einrichtung und Verwendung des Interrupt-Monitors für die Verwaltung der Excel-Arbeitsmappenkonvertierung zu verstehen.
## Schritt 1: Erstellen Sie die Klasse und legen Sie das Ausgabeverzeichnis fest
Zuerst benötigen wir eine Klasse zum Kapseln unserer Funktionen sowie ein Verzeichnis, in dem die Ausgabedatei gespeichert wird.
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
 Ersetzen`"Your Document Directory"` durch den tatsächlichen Pfad, in dem die PDF-Datei gespeichert werden soll.
## Schritt 2: Instanziieren des Interrupt-Monitors
Erstellen Sie als Nächstes ein InterruptMonitor-Objekt. Dieser Monitor hilft bei der Steuerung des Prozesses, indem er die Möglichkeit einrichtet, ihn jederzeit zu unterbrechen.
```csharp
InterruptMonitor im = new InterruptMonitor();
```
Dieser Interrupt-Monitor wird an unsere Arbeitsmappe angehängt und ermöglicht uns die Verwaltung des Konvertierungsprozesses.
## Schritt 3: Einrichten der Arbeitsmappe für die Konvertierung
Lassen Sie uns nun ein Arbeitsmappenobjekt erstellen, ihm den InterruptMonitor zuweisen und dann auf das erste Arbeitsblatt zugreifen, um Beispieltext einzufügen.
```csharp
void CreateWorkbookAndConvertItToPdfFormat()
{
    Workbook wb = new Workbook();
    wb.InterruptMonitor = im;
    Worksheet ws = wb.Worksheets[0];
    Cell cell = ws.Cells["J1000000"];
    cell.PutValue("This is text.");
}
```
Der obige Code erstellt eine Arbeitsmappe, setzt den InterruptMonitor dafür und platziert Text in einer entfernten Zelle (`J1000000`). Durch die Platzierung von Text an dieser Zellenposition wird sichergestellt, dass die Verarbeitung der Arbeitsmappe zeitaufwändiger ist und der InterruptMonitor genügend Zeit hat, einzugreifen.
## Schritt 4: Arbeitsmappe als PDF speichern und Unterbrechungen behandeln
 Versuchen wir nun, die Arbeitsmappe als PDF zu speichern. Wir verwenden ein`try-catch` Block, um eventuell auftretende Unterbrechungen zu bewältigen.
```csharp
try
{
    wb.Save(outputDir + "output_InterruptMonitor.pdf");
}
catch (Aspose.Cells.CellsException ex)
{
    Console.WriteLine("Process Interrupted - Message: " + ex.Message);
}
```
Wenn der Vorgang unterbrochen wird, wird dies durch die Ausnahme erkannt und eine entsprechende Meldung angezeigt. Andernfalls wird die Arbeitsmappe als PDF gespeichert.
## Schritt 5: Unterbrechen Sie den Konvertierungsprozess
 Das Hauptmerkmal hier ist die Möglichkeit, den Prozess zu unterbrechen. Wir fügen eine Verzögerung hinzu mit`Thread.Sleep` und rufen Sie dann die`Interrupt()` Methode, um die Konvertierung nach 10 Sekunden zu stoppen.
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
Diese Verzögerung gibt der Arbeitsmappe Zeit, mit der Konvertierung ins PDF-Format zu beginnen, bevor das Unterbrechungssignal gesendet wird.
## Schritt 6: Führen Sie die Threads gleichzeitig aus
Um alles zusammenzuführen, müssen wir beide Funktionen in separaten Threads starten. Auf diese Weise können die Arbeitsmappenkonvertierung und das Warten auf die Unterbrechung gleichzeitig erfolgen.
```csharp
public void TestRun()
{
    ThreadStart ts1 = new ThreadStart(this.CreateWorkbookAndConvertItToPdfFormat);
    Thread t1 = new Thread(ts1);
    t1.Start();
    ThreadStart ts2 = new ThreadStart(this.WaitForWhileAndThenInterrupt);
    Thread t2 = new Thread(ts2);
    t2.Start();
    t1.Join();
    t2.Join();
}
```
 Der obige Code wird ausgeführt`CreateWorkbookAndConvertItToPdfFormat` Und`WaitForWhileAndThenInterrupt` in parallelen Threads und verbindet sie, sobald beide Prozesse abgeschlossen sind.
## Schritt 7: Endgültige Ausführung
 Zum Schluss fügen wir ein`Run()` Methode zum Ausführen des Codes.
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
 Das`Run` Die Methode ist der Einstiegspunkt, um die Unterbrechung der Aktion zu starten und zu beobachten.
## Abschluss
In diesem Tutorial haben wir untersucht, wie der Konvertierungsprozess in Aspose.Cells für .NET unterbrochen werden kann. Der Interrupt Monitor ist ein hilfreiches Tool bei der Arbeit mit großen Excel-Dateien, mit dem Sie Prozesse stoppen können, ohne auf deren Abschluss warten zu müssen. Dies ist besonders in Szenarien nützlich, in denen Zeit und Ressourcen kostbar sind und schnelles Feedback erforderlich ist.
## Häufig gestellte Fragen
### Was ist ein Interrupt-Monitor in Aspose.Cells für .NET?  
Mit dem Interrupt-Monitor können Sie die Konvertierung oder den Ladevorgang einer Arbeitsmappe mittendrin anhalten.
### Kann ich Interrupt Monitor für andere Formate außer PDF verwenden?  
Ja, Sie können Konvertierungen auch in andere unterstützte Formate unterbrechen.
### Wie wirkt sich Thread.Sleep() auf das Interrupt-Timing aus?  
Thread.Sleep() erzeugt eine Verzögerung, bevor der Interrupt ausgelöst wird, und gibt so Zeit, mit der Konvertierung zu beginnen.
### Kann ich den Vorgang vor Ablauf der 10 Sekunden unterbrechen?  
 Ja, ändern Sie die Verzögerung in`WaitForWhileAndThenInterrupt()` auf eine kürzere Zeit.
### Wird der Interrupt-Prozess die Leistung beeinträchtigen?  
Die Auswirkungen sind minimal und es ist äußerst vorteilhaft für die Verwaltung lang andauernder Prozesse.
 Weitere Informationen finden Sie im[Aspose.Cells für .NET-Dokumentation](https://reference.aspose.com/cells/net/) Wenn Sie Hilfe benötigen, besuchen Sie die[Support Forum](https://forum.aspose.com/c/cells/9)oder erhalten Sie eine[Kostenlose Testversion](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
