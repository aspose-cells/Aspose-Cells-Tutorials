---
date: '2026-05-23'
description: Scopri come modificare i collegamenti ipertestuali Excel Java usando
  Aspose.Cells, caricare una cartella di lavoro Excel Java e rimuovere i collegamenti
  Excel interrotti in modo efficiente.
keywords:
- edit excel hyperlinks java
- load excel workbook java
- remove broken excel links
- maven dependency aspose cells
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Learn how to edit Excel hyperlinks Java using Aspose.Cells, load Excel
    workbook Java, and remove broken Excel links efficiently.
  headline: Edit Excel Hyperlinks Java – Process Multiple Files
  type: TechArticle
- description: Learn how to edit Excel hyperlinks Java using Aspose.Cells, load Excel
    workbook Java, and remove broken Excel links efficiently.
  name: Edit Excel Hyperlinks Java – Process Multiple Files
  steps:
  - name: '**Updating Web Links:** Automatically refresh outdated URLs in quarterly
      financial reports.'
    text: '**Updating Web Links:** Automatically refresh outdated URLs in quarterly
      financial reports.'
  - name: '**Consistency Across Documents:** Enforce a corporate branding policy by
      standardizing hyperlink destinations across dozens of departmental spreadsheets.'
    text: '**Consistency Across Documents:** Enforce a corporate branding policy by
      standardizing hyperlink destinations across dozens of departmental spreadsheets.'
  - name: '**Data Integration:** Point hyperlinks to new API endpoints or internal
      data portals after a system migration.'
    text: '**Data Integration:** Point hyperlinks to new API endpoints or internal
      data portals after a system migration.'
  type: HowTo
- questions:
  - answer: Yes, iterate through `workbook.getWorksheets()` and apply hyperlink changes
      to each worksheet.
    question: Can I edit multiple worksheets at once?
  - answer: Use error‑handling techniques such as try‑catch blocks and the removal
      logic shown in the editing example.
    question: How do I handle broken links with Aspose.Cells Java?
  - answer: Absolutely. Use `worksheet.getHyperlinks().add()` to insert new links
      into your worksheet.
    question: Is it possible to add new hyperlinks using Aspose.Cells Java?
  - answer: Yes, Aspose.Cells is available for .NET, C++, and more. Check out the
      [official website](https://www.aspose.com/) for language‑specific guides.
    question: Can I use Aspose.Cells with other programming languages besides Java?
  - answer: Regularly check your subscription status on the Aspose dashboard and renew
      or update your license as needed.
    question: How can I ensure my license remains active when using Aspose.Cells?
  type: FAQPage
title: Modifica collegamenti ipertestuali Excel Java – Elabora più file
url: /it/java/advanced-features/edit-excel-hyperlinks-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Modifica collegamenti ipertestuali Excel Java – Elabora più file

Quando devi **modificare i collegamenti ipertestuali Excel Java** su un batch di cartelle di lavoro, farlo manualmente è soggetto a errori e richiede molto tempo. Che tu stia migrando un sito web aziendale, correggendo URL obsoleti o pulendo collegamenti interrotti dopo una migrazione dei dati, Aspose.Cells for Java ti consente di caricare programmaticamente oggetti workbook Excel Java, modificare gli URL dei collegamenti ipertestuali e rimuovere in modo sicuro i collegamenti Excel interrotti—tutto in un'unica esecuzione automatizzata. Questa guida ti accompagna attraverso l'intero flusso di lavoro, dalla configurazione del progetto al salvataggio dei file aggiornati.

## Risposte rapide
- **Di cosa tratta questo tutorial?** Modifica e aggiornamento dei collegamenti ipertestuali in uno o più file Excel utilizzando Aspose.Cells for Java.  
- **È necessaria una licenza?** Una prova gratuita è sufficiente per i test; è necessaria una licenza commerciale per la produzione.  
- **Posso elaborare più file contemporaneamente?** Sì – basta iterare sui file in una directory.  
- **Come rimuovo i collegamenti interrotti?** Rileva URL non validi nel ciclo e cancellali con `worksheet.getHyperlinks().remove(i)`.  
- **Quale versione di Java è richiesta?** Java 8 o superiore.

## Cos'è edit excel hyperlinks java?
Edit Excel hyperlinks Java è il processo di modifica programmatica della proprietà `address` degli oggetti Hyperlink all'interno di una cartella di lavoro Excel utilizzando la libreria Aspose.Cells. Questo approccio elimina la modifica manuale, garantisce la coerenza e può essere applicato a migliaia di file in pochi secondi.

## Perché usare Aspose.Cells per la modifica dei collegamenti ipertestuali?
Aspose.Cells supporta **oltre 50 formati di input e output**—inclusi XLSX, XLS, CSV e ODS—e può elaborare cartelle di lavoro con fino a **1 milione di righe** senza caricare l'intero file in memoria, grazie alla sua API di streaming. La libreria conserva anche la formattazione delle celle, le formule e i dati dei grafici, garantendo che solo la destinazione del collegamento ipertestuale venga modificata mentre il resto del foglio rimane intatto.

## Prerequisiti
- **Aspose.Cells for Java** versione 25.3 o successiva (vedi snippet Maven/Gradle sotto).  
- JDK 8 o successivo installato sulla tua macchina di sviluppo.  
- Un IDE come IntelliJ IDEA o Eclipse.  
- Conoscenze di base di Java e familiarità con i concetti di Excel.

## Come caricare Excel workbook Java?
`Workbook` è la classe di Aspose.Cells che rappresenta un intero file Excel, fornendo accesso a fogli di lavoro, celle e proprietà a livello di documento.  
Carica il tuo workbook creando un'istanza `Workbook` che punta al file Excel su disco. Questa singola riga legge il file in memoria, pronto per la manipolazione dei collegamenti ipertestuali. Una volta istanziato, puoi navigare tra i suoi fogli, leggere i valori delle celle e modificare oggetti come collegamenti ipertestuali, grafici o formule secondo necessità.

```text
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```
```

### Ancoraggio della definizione
La classe `Workbook` è l'oggetto principale di Aspose.Cells che rappresenta un intero file Excel, esponendo fogli di lavoro, celle e proprietà a livello di documento per l'accesso programmatico.

## Configurazione di Aspose.Cells per Java
Aggiungi la libreria al tuo progetto usando uno degli strumenti di build supportati.

**Maven:**
```text
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```
```

**Gradle:**
```text
```java
import com.aspose.cells.Workbook;

public class InitializeAsposeCells {
    public static void main(String[] args) throws Exception {
        // Set the license (optional if you have a valid temporary or purchased license)
        // License license = new License();
        // license.setLicense("path_to_your_license_file");

        // Create a Workbook object to work with an Excel file
        Workbook workbook = new Workbook();
    }
}
```
```

### Passaggi per l'acquisizione della licenza
Per utilizzare Aspose.Cells, puoi iniziare con una prova gratuita o richiedere una licenza temporanea per scopi di valutazione:
- **Free Trial:** Scarica da [Aspose Releasers](https://releases.aspose.com/cells/java/).  
- **Temporary License:** Richiedi una [qui](https://purchase.aspose.com/temporary-license/) per sbloccare tutte le funzionalità senza limitazioni.  
- **Purchase:** Per uso commerciale, acquista una licenza su [Aspose Purchase](https://purchase.aspose.com/buy).

#### Inizializzazione e configurazione di base
```text
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class LoadWorkbook {
    public static void main(String[] args) throws Exception {
        // Specify the directory path for your data files
        String dataDir = "path_to_your_data_directory/";

        // Open an existing workbook from the specified file path
        Workbook workbook = new Workbook(dataDir + "source.xlsx");

        // Access the first worksheet in the workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);
    }
}
```
```

## Come modificare i collegamenti ipertestuali nei fogli Excel?
`Hyperlink` è l'oggetto di Aspose.Cells che rappresenta un collegamento cliccabile in una cella, esponendo metodi per ottenere e impostare il suo indirizzo.  
Itera attraverso la collezione di collegamenti ipertestuali di ciascun foglio, aggiorna la proprietà `address` e, facoltativamente, rimuovi le voci che puntano a URL non validi. Il modello seguente gestisce entrambi i compiti in un ciclo conciso, garantendo che tutti i collegamenti siano aggiornati in modo coerente preservando gli altri dati delle celle.

```text
```java
import com.aspose.cells.Hyperlink;

public class EditHyperlinks {
    public static void main(String[] args) throws Exception {
        String dataDir = "path_to_your_data_directory/";
        
        // Load the workbook and get the first worksheet
        Workbook workbook = new Workbook(dataDir + "source.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Iterate through each hyperlink in the worksheet
        for (int i = 0; i < worksheet.getHyperlinks().getCount(); i++) {
            Hyperlink hl = worksheet.getHyperlinks().get(i);
            
            // Example: change hyperlink URL Excel to a new address
            hl.setAddress("http://www.aspose.com");
            
            // Optional: remove if the URL is empty or malformed
            if (hl.getAddress() == null || hl.getAddress().trim().isEmpty()) {
                worksheet.getHyperlinks().remove(i);
                i--; // adjust index after removal
            }
        }

        // Save the changes to a new file
        workbook.save(dataDir + "EHOfWorksheet_out.xlsx");
    }
}
```
```

### Ancoraggio della definizione
La classe `Hyperlink` rappresenta un collegamento cliccabile in una cella; il suo metodo `setAddress(String)` aggiorna l'URL, mentre `getAddress()` restituisce la destinazione corrente.

#### Spiegazione dei frammenti di codice
- **Accesso al collegamento ipertestuale:** `worksheet.getHyperlinks().get(i)` recupera ogni oggetto hyperlink.  
- **Aggiornamento dei collegamenti ipertestuali:** `hl.setAddress("http://www.aspose.com")` cambia il collegamento a un nuovo indirizzo, soddisfacendo il requisito **change hyperlink url excel**.  
- **Rimozione dei collegamenti interrotti:** Il blocco condizionale dimostra come **remove broken excel links** in modo sicuro.

## Come rimuovere i collegamenti Excel interrotti?
Rileva un collegamento interrotto verificando se l'URL inizia con `http://` o `https://` e soddisfa un semplice pattern regex. Se non supera la convalida, rimuovilo dalla collezione per mantenere pulita la cartella di lavoro. Questo approccio impedisce agli utenti di incontrare collegamenti morti e mantiene l'aspetto professionale del documento.

```text
```java
// Save the updated workbook
dataDir + "EHOfWorksheet_out.xlsx";
```
```

## Salvataggio della cartella di lavoro aggiornata
Dopo tutte le modifiche, persisti la cartella di lavoro su disco. Aspose.Cells scrive il file nello stesso formato in cui è stato caricato, preservando tutti i dati non‑collegamento ipertestuale.

```text
```java
// Save the updated workbook
dataDir + "EHOfWorksheet_out.xlsx";
```
```

## Applicazioni pratiche
Ecco alcuni scenari reali in cui potresti applicare la modifica dei collegamenti ipertestuali con Aspose.Cells Java:
1. **Updating Web Links:** Aggiorna automaticamente gli URL obsoleti nei report finanziari trimestrali.  
2. **Consistency Across Documents:** Applica una politica di branding aziendale standardizzando le destinazioni dei collegamenti ipertestuali in decine di fogli di calcolo dipartimentali.  
3. **Data Integration:** Reindirizza i collegamenti ipertestuali a nuovi endpoint API o a portali dati interni dopo una migrazione di sistema.

## Considerazioni sulle prestazioni
Quando **process multiple Excel files**, tieni presente questi consigli di ottimizzazione:
- **Efficient Memory Management:** Usa i try‑with‑resources di Java per garantire che le cartelle di lavoro vengano chiuse prontamente.  
- **Batch Processing:** Itera su una directory di file in un'unica esecuzione JVM anziché avviare processi separati.  
- **Minimize Loop Work:** Esegui la convalida degli URL al di fuori del ciclo interno dei collegamenti ipertestuali per ridurre il carico CPU.

## Conclusione
Modificare i collegamenti ipertestuali in Excel con Aspose.Cells Java semplifica la gestione efficiente dei collegamenti nei documenti. Seguendo questa guida, hai imparato a **process multiple Excel files**, modificare gli URL dei collegamenti ipertestuali e rimuovere i collegamenti interrotti—tutto integrato senza soluzione di continuità nelle tue applicazioni Java.  

Pronto a mettere in pratica queste competenze? Esplora funzionalità più avanzate approfondendo la [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/).

## Domande frequenti

**Q: Posso modificare più fogli di lavoro contemporaneamente?**  
A: Sì, itera attraverso `workbook.getWorksheets()` e applica le modifiche ai collegamenti ipertestuali a ciascun foglio.

**Q: Come gestisco i collegamenti interrotti con Aspose.Cells Java?**  
A: Utilizza tecniche di gestione degli errori come blocchi try‑catch e la logica di rimozione mostrata nell'esempio di modifica.

**Q: È possibile aggiungere nuovi collegamenti ipertestuali usando Aspose.Cells Java?**  
A: Assolutamente. Usa `worksheet.getHyperlinks().add()` per inserire nuovi collegamenti nel tuo foglio.

**Q: Posso usare Aspose.Cells con altri linguaggi di programmazione oltre a Java?**  
A: Sì, Aspose.Cells è disponibile per .NET, C++ e altri. Consulta il [official website](https://www.aspose.com/) per guide specifiche per linguaggio.

**Q: Come posso garantire che la mia licenza rimanga attiva quando uso Aspose.Cells?**  
A: Controlla regolarmente lo stato della tua sottoscrizione sulla dashboard di Aspose e rinnova o aggiorna la licenza secondo necessità.

## Risorse aggiuntive
- [Aspose Releasers](https://releases.aspose.com/cells/java/)
- [Aspose Downloads](https://releases.aspose.com/cells/java/)
- [the releases page](https://releases.aspose.com/cells/java/)
- [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)
- [Aspose Purchase](https://purchase.aspose.com/buy)
- [here](https://purchase.aspose.com/buy)
- [Aspose Temporary License](https://purchase.aspose.com/temporary-license/)
- [here](https://purchase.aspose.com/temporary-license/)
- [official website](https://www.aspose.com/)
- [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

---

**Ultimo aggiornamento:** 2026-05-23  
**Testato con:** Aspose.Cells 25.3 for Java  
**Autore:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutorial correlati

- [Master Aspose.Cells per Java&#58; Carica e modifica cartelle di lavoro Excel in modo efficiente](/cells/java/workbook-operations/aspose-cells-java-load-modify-excel/)
- [Padroneggiare Aspose.Cells per Java&#58; Carica e salva file Excel in modo efficiente](/cells/java/workbook-operations/aspose-cells-java-load-save-excel-files/)
- [Estrai URL da Excel con Aspose.Cells per Java – Carica connessioni dati](/cells/java/advanced-features/aspose-cells-java-excel-data-connections/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}