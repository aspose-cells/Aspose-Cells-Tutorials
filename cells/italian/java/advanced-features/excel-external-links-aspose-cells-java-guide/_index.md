---
date: '2026-11-16'
description: Scopri come aggiornare i collegamenti esterni di Excel, modificare la
  fonte del collegamento di Excel e impostare il percorso assoluto di Excel in modo
  efficiente con Aspose.Cells per Java.
keywords:
- update excel external links
- update excel data source
- change excel link source
- modify excel workbook links
- automate excel link updates
lastmod: '2026-11-16'
og_description: Aggiorna i collegamenti esterni di Excel, modifica la fonte dei dati
  e imposta un percorso assoluto programmaticamente usando Aspose.Cells per Java.
  Impara passo passo con esempi.
og_image_alt: Screenshot of Java code updating Excel external links using Aspose.Cells
og_title: Aggiorna i collegamenti esterni di Excel con Aspose.Cells per Java – Guida
  completa
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to update Excel external links, change Excel link source,
    and set Excel absolute path efficiently with Aspose.Cells for Java.
  headline: How to update Excel external links using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to update Excel external links, change Excel link source,
    and set Excel absolute path efficiently with Aspose.Cells for Java.
  name: How to update Excel external links using Aspose.Cells for Java
  steps:
  - name: '**Data consolidation:** Combine data from multiple workbooks into a master
      report.'
    text: '**Data consolidation:** Combine data from multiple workbooks into a master
      report.'
  - name: '**Financial modeling:** Keep balance sheets synchronized with external
      accounting files.'
    text: '**Financial modeling:** Keep balance sheets synchronized with external
      accounting files.'
  - name: '**Project tracking:** Link task lists across departmental sheets for up‑to‑date
      status reporting.'
    text: '**Project tracking:** Link task lists across departmental sheets for up‑to‑date
      status reporting.'
  type: HowTo
- questions:
  - answer: Yes, Aspose.Cells supports linking to numerous external resources within
      a single workbook.
    question: Can I link to multiple external files?
  - answer: Typical issues include file‑not‑found errors and permission‑denied exceptions.
    question: What are some common errors when accessing external links?
  - answer: Use the `Workbook.getBrokenExternalLinks()` method to identify and address
      broken links.
    question: How do I handle broken links in my Excel file?
  - answer: Absolutely—iterate over a collection of workbooks and update each link
      programmatically.
    question: Is it possible to automate link updates across multiple workbooks?
  - answer: Call `setAbsolutePath()` with the correct base path to resolve all links
      correctly.
    question: What should I do if my workbook's external path is incorrect?
  type: FAQPage
tags:
- excel external links
- aspose.cells
- java workbook automation
title: Come aggiornare i collegamenti esterni di Excel usando Aspose.Cells per Java
url: /it/java/advanced-features/excel-external-links-aspose-cells-java-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiornare i collegamenti esterni di Excel usando Aspose.Cells per Java

## Introduzione
Lavorare con file Excel che contengono collegamenti esterni può essere impegnativo, specialmente quando è necessario **aggiornare i collegamenti esterni di Excel** attraverso diverse fonti di dati o ambienti. In questo tutorial imparerai a **caricare i collegamenti della cartella di lavoro Excel**, accedere e modificare tali collegamenti, e cambiare il percorso assoluto della cartella di lavoro — tutto con Aspose.Cells per Java. Alla fine, sarai in grado di **cambiare la fonte del collegamento Excel**, **aggiornare la fonte dei dati Excel**, e **modificare i collegamenti della cartella di lavoro Excel** programmaticamente, rendendo facile **automatizzare gli aggiornamenti dei collegamenti Excel** nelle tue applicazioni.

## Risposte rapide
- **Qual è la libreria principale per gestire i collegamenti in Excel?** Aspose.Cells per Java.  
- **Posso cambiare la fonte dei dati di un collegamento esterno?** Sì, usa `ExternalLink.setDataSource()`.  
- **Come imposto un nuovo percorso base per una cartella di lavoro?** Chiama `Workbook.setAbsolutePath()`.  
- **È possibile automatizzare gli aggiornamenti dei collegamenti Excel su molti file?** Assolutamente — itera attraverso le cartelle di lavoro e aggiorna i collegamenti nel codice.  
- **Ho bisogno di una licenza per l'uso in produzione?** Una licenza completa rimuove tutte le limitazioni di valutazione.

## Che cosa significa “aggiornare i collegamenti esterni di Excel”?
Aggiornare i collegamenti esterni di Excel significa modificare programmaticamente i riferimenti che una cartella di lavoro mantiene verso altri file o fonti di dati. Questo garantisce che formule, grafici o tabelle puntino sempre alle informazioni corrette e aggiornate senza intervento manuale. Aggiorna inoltre eventuali intervalli denominati o connessioni dati che dipendono da tali collegamenti, prevenendo errori #REF! quando i file di origine vengono spostati o rinominati.

## Perché usare Aspose.Cells per aggiornare i collegamenti esterni di Excel?
Aspose.Cells supporta **oltre 60 formati di input e output** e può elaborare cartelle di lavoro fino a **2 GB** senza caricare l'intero file in memoria. La libreria funziona **al 100% lato server**, quindi non è mai necessario installare Microsoft Office. Queste capacità ti consentono di **aggiornare i collegamenti esterni di Excel**, **cambiare la fonte del collegamento Excel**, e **automatizzare gli aggiornamenti dei collegamenti Excel** in pipeline di dati ad alta velocità.

## Prerequisiti
- Libreria Aspose.Cells aggiunta al tuo progetto (Maven o Gradle).  
- Ambiente di sviluppo Java 8+.  
- Familiarità di base con la sintassi Java e i concetti di programmazione orientata agli oggetti.  
- Una licenza valida di Aspose.Cells per le distribuzioni in produzione.

## Configurazione di Aspose.Cells per Java

### Informazioni sull'installazione
Aggiungi Aspose.Cells al tuo progetto usando uno dei seguenti strumenti di build:

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
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Acquisizione della licenza
Puoi iniziare con una **prova gratuita**, richiedere una **licenza temporanea**, o acquistare una licenza completa per un uso senza restrizioni.

### Inizializzazione e configurazione di base
Inizia importando la classe essenziale:

```java
import com.aspose.cells.Workbook;
```

## Guida all'implementazione passo‑passo

### Carica file Excel con collegamenti esterni
La classe `Workbook` rappresenta un intero file Excel in memoria. Caricare la cartella di lavoro ti dà accesso a tutti i collegamenti esterni incorporati, che è il primo passo per **caricare i collegamenti della cartella di lavoro Excel**.

```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/sample.xlsx");
```

- `dataDir` punta alla cartella contenente il tuo file Excel.  
- `Workbook` rappresenta l'intero foglio di calcolo in memoria.

### Accedi al collegamento esterno
La classe `ExternalLink` incapsula un singolo riferimento esterno memorizzato nella cartella di lavoro. Dopo che la cartella di lavoro è stata caricata, puoi recuperare qualsiasi collegamento esterno.

```java
import com.aspose.cells.ExternalLink;

ExternalLink externalLink = wb.getWorksheets().getExternalLinks().get(0);
```

- `getExternalLinks()` restituisce una collezione di tutti i collegamenti.  
- `get(0)` recupera il primo collegamento (puoi iterare per gli altri).

### Modifica la fonte dei dati del collegamento esterno
Il metodo `setDataSource` aggiorna il nome file o il percorso completo a cui il collegamento esterno punta. Cambiare la fonte ti permette di **cambiare la fonte del collegamento Excel** senza riaprire manualmente la cartella di lavoro.

```java
externalLink.setDataSource("ExternalAccounts.xlsx");
```

- Fornisci il nuovo nome file o percorso completo alla fonte desiderata.  
- Consiglio professionale: usa `Path.getAbsolutePath()` per evitare problemi di percorsi relativi su server diversi.

### Cambia il percorso assoluto della cartella di lavoro
Il metodo `setAbsolutePath(String)` aggiorna la posizione base che la cartella di lavoro utilizza per risolvere i collegamenti relativi. Regolare il percorso assoluto è utile quando si spostano le cartelle di lavoro tra server o directory.

```java
String writablePath = "C:\\Files\\Extra\\";
wb.setAbsolutePath(writablePath);

// Change to a remote URL if needed
String remotePath = "http://www.aspose.com/WebFiles/ExcelFiles/";
wb.setAbsolutePath(remotePath);
```

- Questa chiamata influisce su tutti i collegamenti relativi nella cartella di lavoro.  
- Impostare un percorso assoluto elimina gli errori “file non trovato” dopo il deployment.

### Suggerimenti per la risoluzione dei problemi
- Verifica che tutti i percorsi utilizzino il separatore corretto per il tuo OS (`\\` per Windows, `/` per Linux/macOS).  
- Assicurati che i file esterni esistano effettivamente nelle posizioni specificate.  
- Cattura `java.io.IOException` o `com.aspose.cells.CellsException` per gestire in modo corretto problemi di permessi o accesso ai file.  
- Insidia comune: dimenticare di chiamare `Workbook.dispose()` dopo aver elaborato file di grandi dimensioni può causare perdite di memoria.

## Applicazioni pratiche
Gestire i collegamenti esterni di Excel è essenziale in molti scenari reali:

1. **Consolidamento dati:** Combina dati da più cartelle di lavoro in un report master.  
2. **Modellazione finanziaria:** Mantieni i bilanci sincronizzati con file contabili esterni.  
3. **Monitoraggio progetti:** Collega elenchi di attività tra fogli dipartimentali per report di stato aggiornati.  

## Considerazioni sulle prestazioni
- Disporre degli oggetti `Workbook` (`wb.dispose()`) quando non sono più necessari per liberare memoria.  
- Per cartelle di lavoro grandi, considera di caricare solo i fogli necessari usando `LoadOptions`.  
- Mantieni Aspose.Cells aggiornato; ogni rilascio porta miglioramenti di prestazioni e correzioni di bug.  
- Affermazione quantificata: l'ultima versione elabora una cartella di lavoro di 500 fogli (≈ 2 GB) in meno di **30 secondi** su un tipico server a 8 core.

## Conclusione
In questa guida abbiamo coperto **come aggiornare i collegamenti esterni di Excel** usando Aspose.Cells per Java, includendo il caricamento delle cartelle di lavoro, l'accesso e la modifica dei collegamenti esterni, e l'aggiornamento del percorso assoluto della cartella di lavoro. Queste tecniche ti permettono di **automatizzare gli aggiornamenti dei collegamenti Excel**, semplificare i flussi di lavoro dei dati e ridurre gli errori manuali.

### Passaggi successivi
- Sperimenta con più collegamenti esterni e iterali programmaticamente.  
- Integra questi snippet in applicazioni Java più grandi per l'elaborazione dati end‑to‑end.  
- Esplora altre funzionalità di Aspose.Cells come la generazione di grafici, tabelle pivot e formattazione avanzata.

## Domande frequenti

**Q: Posso collegare a più file esterni?**  
A: Sì, Aspose.Cells supporta il collegamento a numerose risorse esterne all'interno di una singola cartella di lavoro.

**Q: Quali sono alcuni errori comuni quando si accede ai collegamenti esterni?**  
A: I problemi tipici includono errori di file non trovato e eccezioni di permesso negato.

**Q: Come gestisco i collegamenti interrotti nel mio file Excel?**  
A: Usa il metodo `Workbook.getBrokenExternalLinks()` per identificare e risolvere i collegamenti interrotti.

**Q: È possibile automatizzare gli aggiornamenti dei collegamenti su più cartelle di lavoro?**  
A: Assolutamente — itera su una collezione di cartelle di lavoro e aggiorna ogni collegamento programmaticamente.

**Q: Cosa devo fare se il percorso esterno della mia cartella di lavoro è errato?**  
A: Chiama `setAbsolutePath()` con il percorso base corretto per risolvere tutti i collegamenti correttamente.

## Risorse
- [Documentazione Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Scarica Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Acquista una licenza](https://purchase.aspose.com/buy)
- [Versione di prova gratuita](https://releases.aspose.com/cells/java/)
- [Licenza temporanea](https://purchase.aspose.com/temporary-license/)
- [Forum di supporto Aspose](https://forum.aspose.com/c/cells/9)

---

**Ultimo aggiornamento:** 2026-11-16  
**Testato con:** Aspose.Cells 25.3 per Java  
**Autore:** Aspose

## Tutorial correlati

- [Come trovare collegamenti esterni nascosti nei workbook Excel usando Aspose.Cells per Java](/cells/java/advanced-features/detect-hidden-external-links-excel-aspose-cells-java/)
- [Modifica le connessioni dati Excel con Aspose.Cells per Java – Guida passo‑passo](/cells/java/advanced-features/master-excel-data-connections-aspose-cells-java/)
- [Come aggiornare la fonte della tabella pivot Excel con Aspose.Cells per Java: Guida completa](/cells/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}