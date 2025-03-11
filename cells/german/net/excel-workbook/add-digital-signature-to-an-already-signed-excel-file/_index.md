---
title: Einer bereits signierten Excel-Datei eine digitale Signatur hinzufügen
linktitle: Einer bereits signierten Excel-Datei eine digitale Signatur hinzufügen
second_title: Aspose.Cells für .NET API-Referenz
description: Erfahren Sie in dieser ausführlichen Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.Cells für .NET einer bereits signierten Excel-Datei eine digitale Signatur hinzufügen.
weight: 30
url: /de/net/excel-workbook/add-digital-signature-to-an-already-signed-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Einer bereits signierten Excel-Datei eine digitale Signatur hinzufügen

## Einführung

In der heutigen digitalen Welt ist die Sicherung von Dokumenten wichtiger denn je. Digitale Signaturen bieten eine Möglichkeit, die Authentizität und Integrität Ihrer Dateien sicherzustellen, insbesondere beim Umgang mit vertraulichen Informationen. Wenn Sie mit Excel-Dateien arbeiten und einer bereits signierten Arbeitsmappe eine neue digitale Signatur hinzufügen möchten, sind Sie hier richtig! In dieser Anleitung führen wir Sie durch den Prozess des Hinzufügens einer digitalen Signatur zu einer bereits signierten Excel-Datei mit Aspose.Cells für .NET. Also, legen wir los!

## Voraussetzungen

Bevor wir uns in die Einzelheiten der Codierung stürzen, müssen Sie einige Dinge vorbereitet haben:

1.  Aspose.Cells für .NET: Stellen Sie sicher, dass die Aspose.Cells-Bibliothek in Ihrem .NET-Projekt installiert ist. Sie können sie von der[Website](https://releases.aspose.com/cells/net/).
2.  Zertifikatsdatei: Sie benötigen eine gültige Zertifikatsdatei (normalerweise eine`.pfx`Datei), die Ihr digitales Zertifikat enthält. Stellen Sie sicher, dass Sie das Kennwort für diese Datei kennen.
3. Entwicklungsumgebung: Richten Sie Ihre Entwicklungsumgebung mit Visual Studio oder einer anderen IDE ein, die .NET unterstützt.
4. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie problemlos mitmachen.
5. Beispieldateien: Halten Sie eine Excel-Beispieldatei bereit, die bereits digital signiert ist. Dies ist die Datei, der Sie eine neue Signatur hinzufügen.

Nachdem wir nun alles vorbereitet haben, können wir mit dem Programmieren beginnen!

## Pakete importieren

Um zu beginnen, müssen Sie die erforderlichen Pakete in Ihre C#-Datei importieren. So geht's:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Diese Namespaces ermöglichen Ihnen die Arbeit mit Excel-Dateien und die nahtlose Handhabung digitaler Signaturen.

## Schritt 1: Richten Sie Ihre Quell- und Ausgabeverzeichnisse ein

Bevor Sie Ihre Excel-Dateien bearbeiten können, müssen Sie festlegen, wo sich Ihre Quelldateien befinden und wo Sie die Ausgabedatei speichern möchten. So geht's:

```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory";
// Ausgabeverzeichnis
string outputDir = "Your Document Directory";
```

In diesem Schritt verwenden wir eine Methode, um die Pfade für die Quell- und Ausgabeverzeichnisse abzurufen. Stellen Sie sicher, dass diese Verzeichnisse vorhanden sind und die erforderlichen Dateien enthalten.

## Schritt 2: Laden Sie die bereits signierte Arbeitsmappe

 Als nächstes müssen Sie die Excel-Arbeitsmappe laden, die Sie ändern möchten. Dies geschieht durch Erstellen einer Instanz des`Workbook` Klasse und Übergabe des Pfads der signierten Datei.

```csharp
// Laden Sie die Arbeitsmappe, die bereits digital signiert ist
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```

 Hier laden wir die Arbeitsmappe mit dem Namen`sampleDigitallySignedByCells.xlsx`. Stellen Sie sicher, dass diese Datei bereits signiert ist.

## Schritt 3: Erstellen Sie eine digitale Signaturensammlung

Lassen Sie uns nun eine Sammlung digitaler Signaturen erstellen. Diese Sammlung enthält alle digitalen Signaturen, die Sie der Arbeitsmappe hinzufügen möchten.

```csharp
// Erstellen der digitalen Signaturensammlung
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```

Dieser Schritt ist entscheidend, da Sie dadurch bei Bedarf mehrere Signaturen verwalten können.

## Schritt 4: Neues Zertifikat erstellen

 Um eine neue digitale Signatur zu erstellen, müssen Sie Ihre Zertifikatsdatei laden. Geben Sie hier den Pfad zu Ihrer`.pfx` Datei und ihr Passwort.

```csharp
// Zertifikatsdatei und ihr Passwort
string certFileName = sourceDir + "AsposeDemo.pfx";
string password = "aspose";

// Neues Zertifikat erstellen
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```

 Ersetzen Sie unbedingt`AsposeDemo.pfx`und das Kennwort durch Ihren tatsächlichen Zertifikatsdateinamen und Ihr Kennwort.

## Schritt 5: Erstellen der digitalen Signatur

Mit dem Zertifikat in der Hand können Sie nun eine digitale Signatur erstellen. Geben Sie außerdem einen Grund für die Signatur sowie das aktuelle Datum und die Uhrzeit an.

```csharp
// Neue digitale Signatur erstellen und zur Sammlung digitaler Signaturen hinzufügen
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
```

Dieser Schritt fügt Ihrer Sammlung die neue Signatur hinzu, die Sie später auf die Arbeitsmappe anwenden.

## Schritt 6: Hinzufügen der digitalen Signatursammlung zur Arbeitsmappe

Jetzt ist es an der Zeit, die Sammlung digitaler Signaturen zur Arbeitsmappe hinzuzufügen. Hier geschieht die Magie!

```csharp
// Fügen Sie der Arbeitsmappe eine Sammlung digitaler Signaturen hinzu
workbook.AddDigitalSignature(dsCollection);
```

Durch Ausführen dieser Zeile fügen Sie die neue digitale Signatur effektiv an die bereits signierte Arbeitsmappe an.

## Schritt 7: Speichern und Entsorgen der Arbeitsmappe

Abschließend möchten Sie die geänderte Arbeitsmappe in Ihrem Ausgabeverzeichnis speichern und alle verwendeten Ressourcen freigeben.

```csharp
//Speichern und entsorgen Sie die Arbeitsmappe.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```

Durch diesen Schritt wird sichergestellt, dass Ihre Änderungen gespeichert und die Arbeitsmappe ordnungsgemäß gelöscht wird, um Ressourcen freizugeben.

## Schritt 8: Ausführung bestätigen

Zum Abschluss sollten Sie bestätigen, dass Ihr Code erfolgreich ausgeführt wurde. Dies können Sie mit einer einfachen Konsolennachricht tun.

```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```

Dadurch erhalten Sie die Rückmeldung, dass Ihr Vorgang erfolgreich war, was immer schön zu sehen ist!

## Abschluss

Und da haben Sie es! Sie haben erfolgreich eine neue digitale Signatur zu einer bereits signierten Excel-Datei hinzugefügt, indem Sie Aspose.Cells für .NET verwenden. Digitale Signaturen sind eine leistungsstarke Methode, um die Authentizität Ihrer Dokumente sicherzustellen, und jetzt wissen Sie, wie Sie sie programmgesteuert verwalten können. Ganz gleich, ob Sie an Finanzdokumenten, Verträgen oder vertraulichen Informationen arbeiten, die Implementierung digitaler Signaturen kann die Sicherheit und das Vertrauen erhöhen.

## Häufig gestellte Fragen

### Was ist eine digitale Signatur?
Eine digitale Signatur ist eine kryptografische Methode, mit der die Authentizität und Integrität einer Nachricht oder eines Dokuments überprüft wird.

### Kann ich derselben Excel-Datei mehrere digitale Signaturen hinzufügen?
Ja, Sie können eine Sammlung digitaler Signaturen erstellen und derselben Arbeitsmappe mehrere Signaturen hinzufügen.

### Welche Formate unterstützt Aspose.Cells für digitale Signaturen?
 Aspose.Cells unterstützt verschiedene Formate, darunter`.pfx` für Zertifikate.

### Benötige ich eine bestimmte Version von .NET, um Aspose.Cells zu verwenden?
 Überprüfen Sie die[Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) für die Kompatibilität mit Ihrer .NET-Version.

### Wie kann ich eine temporäre Lizenz für Aspose.Cells erhalten?
 Sie können eine temporäre Lizenz anfordern bei[Aspose's Kaufseite](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
