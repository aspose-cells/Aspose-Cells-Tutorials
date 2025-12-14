---
date: '2025-12-14'
description: Erfahren Sie, wie Sie Excel mit Aspose.Cells für Java in PNG konvertieren,
  indem Sie einen benutzerdefinierten Stream‑Provider implementieren. Verwalten Sie
  verknüpfte Bilder und externe Ressourcen effizient.
keywords:
- Aspose.Cells Java custom stream provider
- custom stream provider implementation in Java
- Excel workbook linked images management
title: 'Meistern von Aspose.Cells Java: Excel in PNG mit einem benutzerdefinierten
  Stream‑Provider konvertieren'
url: /de/java/advanced-features/aspose-cells-java-custom-stream-provider/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Meistern von Aspose.Cells Java: Excel in PNG konvertieren mit einem benutzerdefinierten Stream Provider

In der heutigen digitalen Landschaft ist das effiziente **Excel in PNG konvertieren** bei gleichzeitiger Verwaltung externer Ressourcen für Entwickler und Unternehmen unerlässlich. Dieses Tutorial führt Sie durch die Implementierung eines benutzerdefinierten Stream Providers mit Aspose.Cells für Java, sodass Sie nahtlos **Bild‑Stream in Java lesen** Ressourcen in Ihre Excel-Arbeitsmappen integrieren und sie als hochwertige PNG‑Dateien exportieren können.

**Was Sie lernen werden:**
- Wie man Aspose.Cells für Java einrichtet und verwendet
- Implementierung eines benutzerdefinierten Stream Providers in Java
- Konfiguration einer Excel-Arbeitsmappe zum Umgang mit verknüpften Bildern
- Praxisbeispiele, bei denen das Konvertieren von Excel in PNG Mehrwert schafft

## Schnelle Antworten
- **Was macht ein benutzerdefinierter Stream Provider?** Er ermöglicht Ihnen die Kontrolle darüber, wie externe Ressourcen (wie Bilder) während der Verarbeitung der Arbeitsmappe geladen und gespeichert werden.  
- **Warum Excel in PNG konvertieren?** Die PNG‑Ausgabe liefert ein leichtgewichtiges, web‑freundliches Bild Ihres Arbeitsblatts, ideal für Reporting‑Dashboards.  
- **Welche Aspose‑Version wird benötigt?** Aspose.Cells 25.3 oder höher.  
- **Kann ich einen Bild‑Stream in Java lesen?** Ja – Ihre `IStreamProvider`‑Implementierung kann die Bilddatei in einen Stream einlesen (siehe Code).  
- **Benötige ich eine Lizenz für die Produktion?** Eine Voll‑Lizenz ist erforderlich; ein kostenloser Testzeitraum ist für Evaluierungen verfügbar.

## Voraussetzungen

Um diesem Tutorial zu folgen, stellen Sie sicher, dass Sie Folgendes haben:
- **Aspose.Cells für Java**: Version 25.3 oder höher.
- Grundlegendes Verständnis der Java‑Programmierung und der Arbeit mit Bibliotheken.
- Eine IDE (wie IntelliJ IDEA oder Eclipse), die für die Java‑Entwicklung eingerichtet ist.
- Maven oder Gradle zur Verwaltung von Abhängigkeiten bereit.

## Einrichtung von Aspose.Cells für Java

Um Aspose.Cells in Ihrem Java‑Projekt zu verwenden, installieren Sie es über Maven oder Gradle. Nachfolgend finden Sie die Konfigurationen für beide:

**Maven:**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**

```gradle
implementation('com.aspose:aspose-cells:25.3')
```

### Lizenzbeschaffung

Aspose.Cells bietet eine kostenlose Testversion, temporäre Lizenzen für die Evaluierung und Vollkauf‑Optionen:
- **Free Trial**: Laden Sie die Bibliothek von [releases](https://releases.aspose.com/cells/java/) herunter.
- **Temporary License**: Erhalten Sie sie über die [temporary license page](https://purchase.aspose.com/temporary-license/), um ohne Einschränkungen zu evaluieren.
- **Purchase**: Für vollen Zugriff besuchen Sie die [Aspose purchase page](https://purchase.aspose.com/buy).

Sobald Sie Ihre Einrichtung fertiggestellt haben, gehen wir zur Implementierung des benutzerdefinierten Stream Providers über.

## Implementierungs‑Leitfaden

### Was ist ein benutzerdefinierter Stream Provider?

Ein benutzerdefinierter Stream Provider gibt Ihnen die vollständige Kontrolle darüber, wie externe Ressourcen – wie verknüpfte Bilder – gelesen und geschrieben werden. Durch die Implementierung von `IStreamProvider` können Sie **Bild‑Stream in Java lesen** Objekte direkt von der Festplatte, einer Datenbank oder einer anderen Quelle einlesen und sie dann während des Konvertierungsprozesses an Aspose.Cells übergeben.

### Schritt 1: Definieren der StreamProvider‑Klasse

Zuerst erstellen Sie eine Klasse, die `IStreamProvider` implementiert. Dieses Interface erfordert Methoden zum Initialisieren und Schließen von Streams.

```java
import java.io.File;
import java.io.FileInputStream;
import java.io.ByteArrayOutputStream;
import com.aspose.cells.IStreamProvider;
import com.aspose.cells.StreamProviderOptions;

class SP implements IStreamProvider {
    private String dataDir = "YOUR_DATA_DIRECTORY";

    // Initializes the stream for a given resource.
    public void initStream(StreamProviderOptions options) throws Exception {
        File imgFile = new File(dataDir + "/sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
        byte[] bts = new byte[(int) imgFile.length()];

        // Read the image file into a byte array.
        try (FileInputStream fin = new FileInputStream(imgFile)) {
            fin.read(bts);
        }
        
        // Convert the byte array to an output stream and set it in options.
        ByteArrayOutputStream baout = new ByteArrayOutputStream();
        baout.write(bts);
        options.setStream(baout);
    }

    // Method to close the stream if necessary (not utilized here).
    public void closeStream(StreamProviderOptions arg0) throws Exception {
    }
}
```

**Erklärung:**  
- `initStream` liest eine Bilddatei in ein Byte‑Array ein und verpackt es anschließend in einen `ByteArrayOutputStream`. So **lesen Sie Bild‑Stream in Java** und übergeben ihn an Aspose.Cells.  
- `closeStream` ist ein Platzhalter für zukünftige Aufräum‑Logik.

### Schritt 2: Konfigurieren der Arbeitsmappen‑Einstellungen

Als Nächstes konfigurieren Sie die Arbeitsmappe, um Ihren benutzerdefinierten Stream Provider zu nutzen. Dieser Schritt zeigt auch, wie man **Excel in PNG konvertieren** kann, nachdem die Ressourcen geladen wurden.

```java
import com.aspose.cells.*;

public class ControlExternalResourcesUsingWorkbookSetting {
    private String dataDir = "YOUR_DATA_DIRECTORY";
    private String outDir = "YOUR_OUTPUT_DIRECTORY";

    // Runs the main process of configuring and saving an image from a workbook.
    public void Run() throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.xlsx");

        // Set the custom resource provider for handling linked images.
        wb.getSettings().setResourceProvider(new SP());

        Worksheet ws = wb.getWorksheets().get(0);

        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setOnePagePerSheet(true);
        opts.setImageType(ImageType.PNG);

        SheetRender sr = new SheetRender(ws, opts);
        sr.toImage(0, outDir + "/outputControlExternalResourcesUsingWorkbookSettingStreamProvider.png");
    }
}
```

**Erklärung:**  
- Die Arbeitsmappe lädt eine Excel‑Datei, die verknüpfte Bilder enthält.  
- `setResourceProvider(new SP())` weist Aspose.Cells an, den von uns definierten benutzerdefinierten Provider zu verwenden.  
- `ImageOrPrintOptions` ist so konfiguriert, dass ein PNG ausgegeben wird, wodurch der **Excel in PNG konvertieren**‑Workflow abgeschlossen wird.

### Praktische Anwendungen

Die Implementierung eines benutzerdefinierten Stream Providers kann in mehreren Szenarien vorteilhaft sein:

1. **Automated Reporting** – Dynamisch Diagramme oder Logos in Excel‑Berichten aktualisieren und sie sofort als PNGs für Web‑Dashboards exportieren.  
2. **Data Visualization Tools** – Bilder von einem CDN oder einer Datenbank abrufen, in Excel einbinden und hochauflösende PNGs für Präsentationen rendern.  
3. **Collaborative Projects** – Arbeitsmappengrößen klein halten, indem Bilder extern gespeichert werden, und sie bei Bedarf rendern, ohne die Datei aufzublähen.

## Leistungs‑Überlegungen

Wenn Sie mit großen Datensätzen oder zahlreichen Ressourcen arbeiten:

- Optimieren Sie die Speichernutzung, indem Sie Streams nach Möglichkeit wiederverwenden.  
- Schließen Sie stets Streams in `closeStream`, wenn Sie Ressourcen öffnen, die eine explizite Freigabe benötigen.  
- Nutzen Sie die integrierten Rendering‑Optionen von Aspose.Cells (z. B. DPI‑Einstellung), um Qualität und Geschwindigkeit auszubalancieren.

## Häufige Probleme & Fehlersuche

| Problem | Ursache | Lösung |
|-------|-------|----------|
| **Image not displayed** | Falscher Pfad in `dataDir` oder fehlende Datei | Stellen Sie sicher, dass die Bilddatei existiert und der Pfad korrekt ist. |
| **OutOfMemoryError** | Große Bilder werden auf einmal geladen | Verarbeiten Sie Bilder einzeln oder erhöhen Sie die JVM‑Heap‑Größe. |
| **PNG output is blank** | `ImageOrPrintOptions` ist nicht auf PNG eingestellt | Stellen Sie sicher, dass `opts.setImageType(ImageType.PNG)` aufgerufen wird. |

## Häufig gestellte Fragen

**Q1: Kann ich Aspose.Cells mit anderen Java‑Frameworks verwenden?**  
A: Ja, Aspose.Cells funktioniert mit Spring Boot, Jakarta EE und anderen Java‑Ökosystemen. Binden Sie einfach die Maven/Gradle‑Abhängigkeit ein.

**Q2: Wie gehe ich mit Fehlern in `initStream` um?**  
A: Wickeln Sie den Datei‑Lese‑Code in try‑catch‑Blöcke und protokollieren oder werfen Sie aussagekräftige Ausnahmen erneut, damit der Aufrufer angemessen reagieren kann.

**Q3: Gibt es ein Limit für die Anzahl verknüpfter Ressourcen?**  
A: Aspose.Cells kann viele Ressourcen verarbeiten, aber extrem große Mengen können die Leistung beeinträchtigen. Überwachen Sie die Speichernutzung und erwägen Sie das Batching.

**Q4: Kann dieser Ansatz für Nicht‑Bild‑Ressourcen verwendet werden?**  
A: Absolut. Sie können `SP` anpassen, um PDFs, XML oder beliebige Binärdaten zu streamen, indem Sie den MIME‑Typ und die Verarbeitungslogik anpassen.

**Q5: Wo finde ich weiterführende Aspose.Cells‑Funktionen?**  
A: Erkunden Sie Themen wie Datenvalidierung, Diagramme und Pivot‑Tabellen in der offiziellen Dokumentation unter [Aspose Documentation](https://reference.aspose.com/cells/java/).

## Fazit

Durch die Implementierung eines benutzerdefinierten Stream Providers erhalten Sie eine feinkörnige Kontrolle über externe Ressourcen und können effizient **Excel in PNG konvertieren** in Java‑Anwendungen. Experimentieren Sie mit verschiedenen Ressourcentypen, integrieren Sie den Provider in größere Workflows und nutzen Sie die leistungsstarke Rendering‑Engine von Aspose.Cells, um hochwertige visuelle Assets zu liefern.

Wenn Sie weitere Unterstützung benötigen, besuchen Sie das [Aspose support forum](https://forum.aspose.com/c/cells/9) für Community‑Hilfe und Experten‑Beratung.

**Ressourcen**
- **Documentation**: Detaillierte Anleitungen und Referenzen unter [Aspose Documentation](https://reference.aspose.com/cells/java/)
- **Download Library**: Laden Sie die neueste Version von der [Releases Page](https://releases.aspose.com/cells/java/) herunter
- **Purchase License**: Sichern Sie Ihre Lizenz auf der [Aspose Purchase Page](https://purchase.aspose.com/buy)
- **Free Trial**: Beginnen Sie die Evaluierung mit einem kostenlosen Testzeitraum

---

**Zuletzt aktualisiert:** 2025-12-14  
**Getestet mit:** Aspose.Cells 25.3 (Java)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}