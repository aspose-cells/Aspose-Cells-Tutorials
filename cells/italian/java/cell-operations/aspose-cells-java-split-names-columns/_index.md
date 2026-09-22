---
date: '2026-03-15'
description: Impara come suddividere i nomi in colonne separate e salvare la cartella
  di lavoro xlsx usando Aspose.Cells Java in un tutorial passo‑passo.
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: aspose cells java – Dividi i nomi in colonne
url: /it/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Padroneggiare **aspose cells java**: Dividere i Nomi in Colonne

Benvenuti al nostro completo tutorial su **aspose cells java**. In questa guida imparerete **come dividere i nomi** che sono memorizzati in una singola colonna di Excel in due colonne separate—nome e cognome—utilizzando la potente funzionalità testo‑in‑colonne. Che stiate pulendo una lista di contatti, preparando dati per un'importazione CRM, o semplicemente abbiate bisogno di un modo rapido per ristrutturare i fogli di calcolo, questo tutorial vi mostra esattamente come **save workbook xlsx** dopo la trasformazione.

## Risposte Rapide
- **Di cosa tratta questo tutorial?** Dividere le stringhe di nome completo in colonne nome e cognome con Aspose.Cells per Java.  
- **Quale versione della libreria è utilizzata?** L'ultima versione stabile (al 2026).  
- **Ho bisogno di una licenza?** Una prova gratuita funziona per lo sviluppo; è necessaria una licenza commerciale per la produzione.  
- **Posso dividere su altri delimitatori?** Sì—basta cambiare il separatore in `TxtLoadOptions`.  
- **L'output è un file .xlsx?** Assolutamente, la cartella di lavoro viene salvata in formato XLSX.

## Cos'è **aspose cells java**?
**Aspose.Cells java** è un'API Java ad alte prestazioni che consente agli sviluppatori di creare, modificare, convertire e renderizzare file Excel senza necessità di Microsoft Office. Supporta tutti i principali formati Excel e fornisce funzionalità avanzate come formule, grafici e manipolazione dei dati.

## Perché usare **aspose cells java** per dividere i nomi?
- **Zero‑install**: Funziona su qualsiasi ambiente Java lato server.  
- **Speed**: Gestisce grandi fogli di calcolo più velocemente rispetto all'interoperabilità nativa di Excel.  
- **Precision**: Controllo completo su delimitatori, intervalli di colonne e formati di output.  
- **Reliability**: Nessuna dipendenza da COM o Office, rendendolo ideale per distribuzioni cloud o container.

## Prerequisiti
- Java Development Kit (JDK) 8 o successivo.  
- Un IDE come IntelliJ IDEA o Eclipse (opzionale ma consigliato).  
- Maven o Gradle per la gestione delle dipendenze.  

### Configurazione Maven
Aggiungi la dipendenza Aspose.Cells al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Configurazione Gradle
Aggiungi la libreria al tuo `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **Suggerimento:** Usa una licenza temporanea dal portale Aspose per sbloccare tutte le funzionalità durante lo sviluppo.

## Implementazione Passo‑per‑Passo

### Passo 1: Creare una Cartella di Lavoro e Accedere al Primo Foglio di Lavoro
Innanzitutto, importa le classi principali e istanzia una nuova cartella di lavoro. Questo ti fornisce un file Excel pulito pronto per l'inserimento dei dati.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### Passo 2: Popolare il Foglio di Lavoro con Nomi di Esempio
Successivamente, aggiungi alcune stringhe di nome completo nella colonna **A**. In un progetto reale, le leggeresti da un database o da un file CSV.

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### Passo 3: Configurare le Opzioni di Caricamento Testo per la Divisione delle Colonne
La classe `TxtLoadOptions` indica ad Aspose.Cells come interpretare il testo. Qui usiamo uno spazio (`' '`) come delimitatore.

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### Passo 4: Dividere il Testo in Due Colonne
Ora chiama `textToColumns()` sull'area di celle che contiene i nomi. I parametri `(0, 0, 5, opts)` significano *inizia dalla riga 0, colonna 0, elabora 5 righe, usando le opzioni appena definite*.

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

Dopo questa chiamata, la colonna A contiene i nomi e la colonna B contiene i cognomi.

### Passo 5: Salvare la Cartella di Lavoro come File XLSX
Infine, scrivi la cartella di lavoro modificata su disco. L'enumerazione `SaveFormat` garantisce che il file sia salvato nel moderno formato XLSX.

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **Perché è importante:** Utilizzando **save workbook xlsx**, garantisci la compatibilità con le versioni più recenti di Excel, Google Sheets e altri strumenti di fogli di calcolo.

## Applicazioni Pratiche
- **Data Cleaning:** Pulizia dei Dati: Separare rapidamente i campi concatenati prima di caricarli nei pipeline di analisi.  
- **CRM Integration:** Integrazione CRM: Trasformare una lista di contatti piatta in una tabella strutturata per l'importazione.  
- **HR Systems:** Sistemi HR: Dividere i nomi completi dei dipendenti per la gestione di paghe o benefici.

## Considerazioni sulle Prestazioni
Quando si lavora con migliaia di righe:

1. **Batch Updates:** Aggiornamenti in Batch: Usa `ws.getCells().setRowHeight()` o metodi batch simili per ridurre l'overhead.  
2. **Memory Management:** Gestione della Memoria: Chiama `wb.calculateFormula()` solo quando necessario e libera rapidamente gli oggetti di grandi dimensioni.  
3. **Garbage Collection:** Garbage Collection: Esegui la JVM con impostazioni di heap appropriate (`-Xmx2g` per file grandi) per evitare errori OutOfMemory.

## Problemi Comuni e Soluzioni

| Issue | Solution |
|-------|----------|
| **I nomi contengono iniziali intermedie** (ad es., “John A. Doe”) | Regola il separatore o elabora la seconda colonna per estrarre il cognome. |
| **Celle vuote inaspettate** | Verifica che l'intervallo di origine (`textToColumns` parametri) corrisponda alle righe di dati effettive. |
| **Licenza non trovata** | Posiziona il file di licenza temporanea (`Aspose.Cells.lic`) nella radice del progetto o imposta la licenza programmaticamente. |

## Domande Frequenti

**Q: Cos'è Aspose.Cells Java?**  
A: Una potente libreria che consente di creare, modificare e convertire file Excel programmaticamente usando Java.

**Q: Posso dividere le colonne in base a delimitatori diversi dallo spazio?**  
A: Sì, personalizza il separatore `TxtLoadOptions` secondo le esigenze dei tuoi dati.

**Q: Come gestisco grandi dataset con Aspose.Cells?**  
A: Ottimizza le prestazioni gestendo la memoria e riducendo al minimo le operazioni sulla cartella di lavoro, come descritto sopra.

**Q: È disponibile supporto se incontro problemi?**  
A: Visita il [Aspose Forum](https://forum.aspose.com/c/cells/9) per assistenza della community o contatta direttamente il team di supporto Aspose.

**Q: In quali formati Aspose.Cells può salvare le cartelle di lavoro?**  
A: Supporta una vasta gamma di formati di file Excel, inclusi XLSX, XLS, CSV e altri.

## Risorse

- **Documentazione**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Download**: [Aspose.Cells Java Releases](https://releases.aspose.com/cells/java/)
- **Acquisto**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Prova Gratuita**: [Try Aspose.Cells for Free](https://releases.aspose.com/cells/java/)
- **Licenza Temporanea**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)

Buon coding, e goditi l'utilizzo della piena potenza di **aspose cells java** nei tuoi progetti!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Ultimo Aggiornamento:** 2026-03-15  
**Testato Con:** Aspose.Cells 25.3 for Java  
**Autore:** Aspose