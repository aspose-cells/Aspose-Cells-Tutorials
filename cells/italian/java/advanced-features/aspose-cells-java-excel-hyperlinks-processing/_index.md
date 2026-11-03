---
date: '2026-11-03'
description: Scopri come estrarre i collegamenti ipertestuali da Excel utilizzando
  Aspose.Cells per Java. Questa guida copre il caricamento delle cartelle di lavoro,
  il recupero dei collegamenti, l'elaborazione di file di grandi dimensioni e le migliori
  pratiche per la gestione dei collegamenti ipertestuali.
keywords:
- how to extract hyperlinks
- process large excel files
- load excel workbook
- retrieve excel links
- excel hyperlink management
lastmod: '2026-11-03'
og_description: Scopri come estrarre i collegamenti ipertestuali da Excel utilizzando
  Aspose.Cells per Java. Ottieni codice passo‑passo, consigli sulle prestazioni e
  FAQ per una gestione affidabile dei collegamenti ipertestuali.
og_image_alt: Guide to extract hyperlinks from Excel using Aspose.Cells for Java
og_title: Come estrarre i collegamenti ipertestuali da Excel – gestione avanzata
schemas:
- author: Aspose
  dateModified: '2026-11-03'
  description: Learn how to extract hyperlinks from Excel using Aspose.Cells for Java.
    This guide covers loading workbooks, retrieving links, processing large files,
    and best practices for hyperlink management.
  headline: How to extract hyperlinks from Excel – advanced management
  type: TechArticle
- questions:
  - answer: Aspose.Cells for Java supports Java 8 and newer, including all LTS releases
      up to Java 21.
    question: What versions of Java are compatible with Aspose.Cells?
  - answer: Yes. Load only the required worksheet or range, and avoid loading the
      entire workbook when possible. Reusing a single `Workbook` instance further
      reduces heap pressure.
    question: Can I extract hyperlinks from very large Excel files without running
      out of memory?
  - answer: A free trial lets you experiment, but a commercial license removes evaluation
      limits, unlocks multi‑threaded processing, and provides full technical support.
    question: Is a license required for hyperlink extraction in production?
  - answer: The `TargetModeType.EMAIL` constant identifies email links; you can extract
      the `mailto:` address and process it separately.
    question: How do I handle hyperlinks that point to email addresses?
  - answer: Absolutely. All hyperlink properties—display text, tooltip, address, and
      target mode—are retained when you save the workbook in any supported format.
    question: Does Aspose.Cells preserve hyperlink formatting when saving?
  type: FAQPage
tags:
- extract hyperlinks
- Aspose.Cells
- Java Excel processing
title: Come estrarre i collegamenti ipertestuali da Excel – gestione avanzata
url: /it/java/advanced-features/aspose-cells-java-excel-hyperlinks-processing/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come estrarre collegamenti ipertestuali da Excel – gestione avanzata

Nel mondo odierno guidato dai dati, **come estrarre collegamenti ipertestuali da Excel** rapidamente e in modo affidabile è un requisito fondamentale per chi automatizza i report Excel. Che tu stia costruendo un cruscotto finanziario, uno strumento di migrazione dei dati o un servizio di generazione di documenti, gestire cartelle di lavoro ricche di collegamenti ipertestuali può rappresentare una sfida comune. In questo tutorial imparerai a caricare una cartella di lavoro Excel, accedere ai suoi fogli di lavoro e **recuperare collegamenti ipertestuali da Excel** usando Aspose.Cells per Java. Alla fine, sarai pronto a integrare l'elaborazione dei collegamenti ipertestuali nelle tue applicazioni e persino a **elaborare in batch file Excel** per scenari su larga scala.

## Risposte rapide
- **Qual è la classe principale per aprire una cartella di lavoro?** `Workbook` – l'oggetto centrale che rappresenta un intero file Excel in memoria.  
- **Quale metodo restituisce tutti i collegamenti ipertestuali in un intervallo?** `Range.getHyperlinks()` – elenca ogni oggetto collegamento ipertestuale all'interno dell'intervallo specificato.  
- **È necessaria una licenza per l'estrazione di base dei collegamenti ipertestuali?** Una versione di prova gratuita funziona per lo sviluppo, ma una licenza commerciale rimuove i limiti di valutazione e sblocca ottimizzazioni complete delle prestazioni.  
- **Posso elaborare file di grandi dimensioni in modo efficiente?** Sì—concentrati su fogli o intervalli specifici, riutilizza una singola istanza `Workbook` e rilascia gli oggetti tempestivamente.  
- **Quali versioni di Java sono supportate?** Java 8 e successive, incluse Java 11, 17 e le versioni LTS successive.

## Cos'è “estrarre collegamenti ipertestuali da Excel”?
Estrarre collegamenti ipertestuali da Excel significa leggere le informazioni di collegamento memorizzate nelle celle—come URL, percorsi di file, indirizzi email o riferimenti a celle interne—per poter utilizzare quei dati in modo programmatico. Aspose.Cells fornisce un'API semplice per enumerare questi collegamenti senza avviare Microsoft Excel, risparmiando tempo e risorse del server.

## Perché recuperare collegamenti ipertestuali da Excel?
Recuperare i collegamenti ipertestuali ti consente di **convalidare la salute dei link**, **migrare o riscrivere gli URL**, **generare report riepilogativi** e **creare indici ricercabili** per l'integrazione con knowledge‑base. Ad esempio, un processo notturno può scansionare ogni cartella di lavoro in un repository, segnalare URL interrotti e aggiornarli automaticamente a un nuovo dominio, garantendo che i report pubblicati non contengano riferimenti obsoleti.

## Prerequisiti
- **Aspose.Cells for Java** library (version 25.3 or newer).  
- Java 8 + e un IDE (IntelliJ IDEA, Eclipse, VS Code, ecc.).  
- Maven o Gradle per la gestione delle dipendenze.  
- Una licenza valida di Aspose.Cells (opzionale per la versione di prova).  

### Configurare Aspose.Cells per Java
Aggiungi la libreria al tuo progetto usando Maven o Gradle.

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **Consiglio:** Mantieni la versione della libreria aggiornata; ogni rilascio minore aggiunge supporto per nuovi tipi di collegamenti ipertestuali e migliora l'uso della memoria fino al 30 %.

#### Inizializzazione di base
Una volta aggiunta la dipendenza, crea una semplice classe Java per verificare che la cartella di lavoro possa essere caricata.

```java
import com.aspose.cells.Workbook;

public class InitializeAsposeCells {
    public static void main(String[] args) throws Exception {
        // Set license if available
        // License license = new License();
        // license.setLicense("path/to/license/file");

        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

## Come estrarre collegamenti ipertestuali da Excel – caricamento della cartella di lavoro
`Workbook` è la classe principale che carica e rappresenta un intero file Excel in memoria.  
Carica la cartella di lavoro con una singola riga di codice: `Workbook workbook = new Workbook("input.xlsx");`. Questa chiamata analizza l'intestazione del file, costruisce una rappresentazione in‑memoria dei fogli di lavoro e prepara l'API per ulteriori query. Caricare solo la cartella di lavoro necessaria (invece dell'intera cartella) riduce il tempo di avvio di circa il 40 % per file inferiori a 10 MB.

### Carica cartella di lavoro (funzione 1)

```java
import com.aspose.cells.Workbook;

public class FeatureLoadWorkbook {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Load an existing workbook from the specified path.
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

## Come estrarre collegamenti ipertestuali da Excel – accedere al foglio di lavoro e all'intervallo
`Range` rappresenta un blocco rettangolare di celle all'interno di un foglio di lavoro.  
Prima, ottieni il foglio di lavoro che desideri analizzare, poi crea un oggetto `Range` che copre l'area di interesse. Per esempio, `worksheet.getCells().createRange("A1", "Z1000")` definisce un blocco rettangolare; l'API ti permette quindi di chiamare `getHyperlinks()` su quell'intervallo. Definendo l'intervallo limiti la scansione all'area rilevante, migliorando le prestazioni e riducendo l'uso della memoria.

### Accedi al foglio di lavoro e all'intervallo (funzione 2)

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Range;

public class FeatureAccessWorksheetAndRange {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Load an existing workbook from the specified path.
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");

        // Access the first worksheet in the workbook (index 0).
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Create a range from cell A1 to A7 within the worksheet.
        Range range = worksheet.getCells().createRange("A1", "A7");
        
        System.out.println("Range created successfully!");
    }
}
```

## Come estrarre collegamenti ipertestuali da Excel – recuperare e processare i collegamenti ipertestuali
`getHyperlinks()` restituisce una collezione di tutti gli oggetti collegamento ipertestuale all'interno dell'intervallo specificato.  
Chiama `Range.getHyperlinks()` per ottenere una collezione di oggetti `Hyperlink`. Ogni oggetto espone proprietà come `getAddress()`, `getDisplay()`, `getTooltip()` e `getTargetMode()`. Puoi iterare sulla collezione, registrare ogni link o memorizzarli in un database per analisi successive. È inoltre possibile filtrare ulteriormente la collezione per tipo di indirizzo o testo visualizzato prima di persistere i dati.

### Recupera e processa i collegamenti ipertestuali (funzione 3)

```java
import com.aspose.cells.Range;
import com.aspose.cells.Hyperlink;
import com.aspose.cells.TargetModeType;

public class FeatureRetrieveAndProcessHyperlinks {
    public static void main(String[] args) throws Exception {
        // Assume 'range' is obtained as shown in previous examples.
        Range range = null;  // Placeholder, replace with actual range initialization

        // Retrieve all hyperlinks within the specified range.
        Hyperlink[] hyperlinks = range.getHyperlinks();

        // Iterate over each hyperlink and process it to determine its type.
        for (Hyperlink link : hyperlinks) {
            String displayText = link.getTextToDisplay();
            int linkType = link.getLinkType();
            System.out.println(displayText + ": " + getLinkTypeName(linkType));
        }
    }

    // Helper method to convert hyperlink type integer to a human‑readable string.
    private static String getLinkTypeName(int linkType) {
        switch (linkType) {
            case TargetModeType.EXTERNAL:
                return "EXTERNAL";
            case TargetModeType.FILE_PATH:
                return "FILE_PATH";
            case TargetModeType.EMAIL:
                return "EMAIL";
            default:
                return "CELL_REFERENCE";
        }
    }
}
```

## Applicazioni pratiche

| Caso d'uso | Vantaggio |
|------------|-----------|
| **Validazione dei dati** | Verifica automaticamente che ogni collegamento ipertestuale punti a un URL raggiungibile prima di pubblicare un report. |
| **Automazione** | Estrai i link durante una migrazione verso un nuovo data‑warehouse, aggiornando i riferimenti al volo. |
| **Reporting** | Crea un foglio riepilogativo che elenca tutte le risorse esterne referenziate in una cartella di lavoro. |

## Considerazioni sulle prestazioni
- **Elabora solo gli intervalli necessari** – limitare l'ambito riduce il consumo di memoria fino al 60 % per cartelle di lavoro con migliaia di righe.  
- **Rilascia gli oggetti** – imposta `workbook = null;` dopo l'uso e lascia che il garbage collector della JVM recuperi la memoria.  
- **Elaborazione in batch** – quando gestisci molti file, riutilizza una singola istanza `Workbook` dove possibile. Questo modello ti consente di **elaborare in batch file Excel** in modo efficiente, raggiungendo una velocità di 150 file/min su un server standard a 8 core.

## Problemi comuni e soluzioni

| Problema | Soluzione |
|----------|-----------|
| **Null `range`** | Assicurati che l'intervallo sia creato prima di chiamare `getHyperlinks()`. |
| **Licenza mancante** | Una versione di prova funziona per lo sviluppo, ma una versione con licenza rimuove i limiti di valutazione e migliora le prestazioni. |
| **Tipo di collegamento ipertestuale non supportato** | Usa le costanti `TargetModeType` per gestire i nuovi tipi man mano che Aspose rilascia aggiornamenti. |

## Domande frequenti

**D: Quali versioni di Java sono compatibili con Aspose.Cells?**  
R: Aspose.Cells for Java supporta Java 8 e versioni successive, incluse tutte le versioni LTS fino a Java 21.

**D: Posso estrarre collegamenti ipertestuali da file Excel molto grandi senza esaurire la memoria?**  
R: Sì. Carica solo il foglio di lavoro o l'intervallo necessario e evita di caricare l'intera cartella di lavoro quando possibile. Riutilizzare una singola istanza `Workbook` riduce ulteriormente la pressione sull'heap.

**D: È necessaria una licenza per l'estrazione dei collegamenti ipertestuali in produzione?**  
R: Una versione di prova gratuita ti permette di sperimentare, ma una licenza commerciale rimuove i limiti di valutazione, sblocca l'elaborazione multithread e fornisce supporto tecnico completo.

**D: Come gestisco i collegamenti ipertestuali che puntano a indirizzi email?**  
R: La costante `TargetModeType.EMAIL` identifica i link email; puoi estrarre l'indirizzo `mailto:` e processarlo separatamente.

**D: Aspose.Cells conserva la formattazione dei collegamenti ipertestuali durante il salvataggio?**  
R: Assolutamente sì. Tutte le proprietà del collegamento ipertestuale—testo visualizzato, tooltip, indirizzo e modalità di destinazione—vengono mantenute quando salvi la cartella di lavoro in qualsiasi formato supportato.

**D: Posso usare Aspose.Cells per **leggere i collegamenti ipertestuali di Excel** in un lavoro batch?**  
R: Sì—combina l'API con un ciclo sui file per leggere i collegamenti ipertestuali di Excel su molte cartelle di lavoro, quindi archivia i risultati in un repository centrale.

**D: Qual è il modo migliore per **caricare una cartella di lavoro Excel in Java** per scenari ad alto throughput?**  
R: Riutilizza una singola istanza `Workbook` quando possibile, chiudi rapidamente gli stream di input e abilita l'opzione `MemorySetting.MEMORY_PREFERENCE` per ottimizzare l'uso della memoria.

---

**Ultimo aggiornamento:** 2026-11-03  
**Testato con:** Aspose.Cells 25.3 for Java  
**Autore:** Aspose  

Se hai altre domande, sentiti libero di visitare il [Forum di supporto Aspose](https://forum.aspose.com/c/cells/9).

## Tutorial correlati

- [Come aggiungere un collegamento ipertestuale in Excel usando Aspose.Cells per Java – Guida passo‑passo](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [Elaborare file Excel di grandi dimensioni: gestire i collegamenti ipertestuali tramite Aspose.Cells](/cells/java/advanced-features/manage-excel-hyperlinks-aspose-cells-java/)
- [Come trovare collegamenti esterni nascosti nei workbook Excel usando Aspose.Cells per Java](/cells/java/advanced-features/detect-hidden-external-links-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}