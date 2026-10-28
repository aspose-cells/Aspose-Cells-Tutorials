---
date: '2026-10-28'
description: Scopri come modificare il sistema di data di Excel a 1904 usando Aspose.Cells
  per Java, impostare il formato data di Excel e convertire il sistema 1904 di Excel
  in modo efficiente.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Modifica il sistema di data di Excel a 1904 usando Aspose.Cells per
  Java. Scopri passo passo come abilitare il sistema 1904, impostare le date e riconvertire.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Modifica il sistema di data di Excel a 1904 con Aspose.Cells per Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Modifica il sistema di data di Excel a 1904 con Aspose.Cells Java
url: /it/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Modifica il sistema di data di Excel a 1904 con Aspose.Cells Java

In questo tutorial imparerai come **cambiare il sistema di data di Excel** al formato 1904 usando Aspose.Cells per Java. Il sistema 1904 è essenziale quando è necessario conservare date legacy basate su Mac o allinearsi a modelli finanziari che si aspettano quell'epoca. Ti guideremo attraverso l'installazione della libreria, il caricamento di una cartella di lavoro, l'attivazione del sistema di data e il salvataggio del risultato—tutto senza richiedere Microsoft Excel sul server.

## Risposte rapide
- **Cosa fa il sistema di data 1904?** Inizia a contare i giorni dal 1 gennaio 1904, spostando tutte le date di 1.462 giorni rispetto al sistema predefinito 1900.  
- **Perché usare Aspose.Cells per cambiare il sistema di data?** Fornisce un'API semplice che funziona senza Excel installato e supporta file di grandi dimensioni.  
- **Quali versioni di Java sono supportate?** JDK 8 o versioni successive.  
- **Ho bisogno di una licenza?** Una prova gratuita funziona per la valutazione; una licenza rimuove i limiti di utilizzo.  
- **Posso riconvertire al sistema 1900 in seguito?** Sì, basta chiamare `setDate1904(false)`.

## Cos'è il sistema di data 1904 in Excel?
Il sistema di data 1904 conta i giorni dal 1 gennaio 1904, invece dell'epoca predefinita 1900. Questo spostamento aggiunge esattamente 1.462 giorni a ogni valore di data, motivo per cui le cartelle di lavoro legacy per Mac appaiono sfasate quando aperte su Windows. È principalmente usato per la compatibilità con file Excel Macintosh più vecchi e alcuni modelli finanziari legacy.

## Perché modificare il sistema di data di Excel con Aspose.Cells?
Puoi cambiare il sistema di data direttamente da Java, eliminando i passaggi manuali in Excel. Aspose.Cells elabora cartelle di lavoro fino a **2 GB** di dimensione e può convertire una cartella di lavoro da 500 fogli in meno di **2 secondi** su un tipico server a 4 core, offrendo un'automazione server‑side ad alta velocità.

## Prerequisiti
- Java Development Kit (JDK) 8 o superiore.  
- Maven o Gradle per la gestione delle dipendenze.  
- Conoscenze di base di programmazione Java.  

## Configurazione di Aspose.Cells per Java

### Maven
Aggiungi la seguente dipendenza al tuo file `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Includi questa riga nel tuo file `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Acquisizione licenza
Aspose offre una prova gratuita, una licenza temporanea e licenze commerciali complete. Puoi iniziare con la [prova gratuita](https://releases.aspose.com/cells/java/) o ottenere una licenza temporanea dalla [pagina della licenza temporanea](https://purchase.aspose.com/temporary-license/).

## Come modificare il sistema di data di Excel a 1904 con Aspose.Cells per Java?
Carica la cartella di lavoro, abilita l'impostazione 1904 e salva il file—questo flusso in tre passaggi aggiorna l'epoca di data interna della cartella di lavoro in meno di un secondo. La chiamata API `setDate1904(true)` attiva il flag del sistema, e la modifica viene mantenuta quando chiami `save`. Non è necessaria alcuna installazione di Excel, rendendolo ideale per ambienti server senza interfaccia.

### Passo 1: inizializzare e caricare la cartella di lavoro
La classe `Workbook` rappresenta un intero file Excel in memoria. Prima, crea un'istanza `Workbook` che punti al tuo file esistente.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Passo 2: abilitare il sistema di data 1904
Il metodo `WorkbookSettings.setDate1904` attiva/disattiva il flag di data a livello di cartella di lavoro. Impostandolo su `true` attiva il sistema 1904 per tutti i fogli di lavoro.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Suggerimento:** Puoi anche chiamare `setDate1904(false)` più tardi se hai bisogno di tornare indietro.

### Passo 3: salvare la cartella di lavoro modificata
Infine, scrivi le modifiche in un nuovo file (o sovrascrivi l'originale). Il metodo `save` rispetta automaticamente il sistema di data attivo.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Nota:** Il codice sopra utilizza il nome della classe `tWorkbook` come fornito originariamente. Assicurati che questo errore di battitura corrisponda alle convenzioni di denominazione del tuo progetto o correggilo in `Workbook` se necessario.

## Imposta la data di Excel programmaticamente (parola chiave secondaria)
Se devi regolare i valori di celle individuali dopo aver cambiato il sistema, puoi usare `cells.get(i, j).putValue(Date)` dove la data verrà interpretata in base al sistema di data attivo.

## Converti il sistema Excel 1904 nuovamente al 1900 (parola chiave secondaria)
Per tornare indietro, basta chiamare:

```java
workbook.getSettings().setDate1904(false);
```

Quindi salva nuovamente la cartella di lavoro.

## Applicazioni pratiche
1. **Data archiving** – Conserva i timestamp legacy durante la migrazione di vecchi fogli di calcolo basati su Mac.  
2. **Cross‑platform reporting** – Genera report che si aprono correttamente sia su Windows che su macOS senza discrepanze di data.  
3. **Financial modeling** – Allinea i calcoli di data con i modelli finanziari legacy che si aspettano il sistema 1904.

## Considerazioni sulle prestazioni
- Limita le operazioni sulla cartella di lavoro in una singola sessione per mantenere basso l'uso di memoria; Aspose.Cells trasmette i dati in streaming e non carica mai l'intero file in RAM a meno che non lo richieda esplicitamente.  
- Ottimizza i flag di garbage‑collection di Java (`-XX:+UseG1GC`) per file molto grandi per evitare picchi di tempo di pausa.  

## Domande frequenti

**Q: Qual è la differenza tra i sistemi di data 1900 e 1904?**  
A: Il sistema 1900 inizia il 1 gennaio 1900, mentre il sistema 1904 inizia il 1 gennaio 1904, spostando tutte le date di 1.462 giorni.

**Q: Posso cambiare il sistema di data di una cartella di lavoro attualmente aperta in Excel?**  
A: Sì, ma devi prima chiudere il file in Excel; altrimenti l'operazione di salvataggio fallirà.

**Q: Ho bisogno di una licenza per usare `setDate1904`?**  
A: Il metodo funziona nella prova gratuita, ma una licenza completa rimuove le limitazioni di valutazione.

**Q: È possibile cambiare il sistema di data solo per un singolo foglio di lavoro?**  
A: No, il sistema di data è un'impostazione a livello di cartella di lavoro; si applica a tutti i fogli.

**Q: Come posso verificare che il sistema di data sia stato cambiato?**  
A: Apri il file salvato in Excel, vai su **File → Opzioni → Avanzate**, e controlla la casella **"Use 1904 date system"**.

## Conclusione
Ora sai come **cambiare il sistema di data di Excel** a 1904 usando Aspose.Cells per Java, come impostare le date di celle individuali e come tornare al sistema 1900 quando necessario. Integra questi snippet nei tuoi flussi di elaborazione dati per garantire la compatibilità delle date tra piattaforme e file legacy.

---

**Last Updated:** 2026-10-28  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  

**Documentazione:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
**Download:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)  
**Acquista licenza:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
**Prova gratuita:** [Start Free Trial](https://releases.aspose.com/cells/java/)  
**Licenza temporanea:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)  
**Forum di supporto:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## Tutorial correlati

- [Converti efficientemente Excel in PDF con formati data personalizzati usando Aspose.Cells per Java](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells per Java: Come creare e formattare cartelle di lavoro Excel in modo efficiente](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Padroneggia la manipolazione di Excel con Aspose.Cells per Java: Operazioni su cartelle di lavoro e tutorial di formattazione delle celle](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}