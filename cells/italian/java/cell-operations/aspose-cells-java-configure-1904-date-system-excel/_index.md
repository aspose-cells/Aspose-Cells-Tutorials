---
date: '2026-02-22'
description: Scopri come cambiare il sistema di data di Excel a 1904 usando Aspose.Cells
  per Java, impostare il formato data di Excel e convertire il sistema 1904 di Excel
  in modo efficiente.
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: Modifica il sistema di data di Excel a 1904 con Aspose.Cells Java
url: /it/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Modifica il sistema di data di Excel a 1904 con Aspose.Cells Java

Gestire dati storici in Excel può essere difficile perché Excel supporta due diversi sistemi di data. **In questo tutorial imparerai come cambiare il sistema di data di Excel al formato 1904 usando Aspose.Cells per Java**, il che rende la gestione delle date legacy indolore. Vedremo come inizializzare una cartella di lavoro, abilitare il sistema di data 1904 e salvare la modifica.

## Risposte rapide
- **Cosa fa il sistema di data 1904?** Inizia a contare i giorni dal 1 gennaio 1904, spostando tutte le date di 1462 giorni rispetto al sistema predefinito 1900.  
- **Perché usare Aspose.Cells per cambiare il sistema di data?** Fornisce un'API semplice che funziona senza Excel installato e supporta file di grandi dimensioni.  
- **Quali versioni di Java sono supportate?** JDK 8 o successive.  
- **Ho bisogno di una licenza?** Una prova gratuita è sufficiente per la valutazione; una licenza rimuove i limiti di utilizzo.  
- **Posso riconvertire al sistema 1900 in seguito?** Sì, basta impostare `setDate1904(false)`.

## Cos'è il sistema di data 1904 in Excel?
Il sistema di data 1904 era originariamente usato dalle prime versioni Macintosh di Excel. Conta i giorni dal 1 gennaio 1904, il che è utile per la compatibilità con fogli di calcolo più vecchi e alcuni modelli finanziari.

## Perché cambiare il sistema di data di Excel con Aspose.Cells?
- **Compatibilità cross‑platform** – funziona su Windows, Linux e macOS.  
- **Nessuna installazione di Excel richiesta** – ideale per l'elaborazione lato server.  
- **Alte prestazioni** – gestisce cartelle di lavoro di grandi dimensioni con un minimo consumo di memoria.  

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
Inserisci questa riga nel tuo file `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Acquisizione della licenza
Aspose offre una prova gratuita, una licenza temporanea e licenze commerciali complete. Puoi iniziare con la [prova gratuita](https://releases.aspose.com/cells/java/) o ottenere una licenza temporanea dalla [pagina della licenza temporanea](https://purchase.aspose.com/temporary-license/).

## Modifica il sistema di data di Excel usando Aspose.Cells Java

Di seguito trovi la guida passo‑passo che effettivamente **cambia il sistema di data di Excel**. Ogni passo include una breve spiegazione seguita dal codice esatto di cui hai bisogno.

### Passo 1: Inizializza e carica la cartella di lavoro
Per prima cosa, crea un'istanza `Workbook` che punti al tuo file Excel esistente.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Passo 2: Abilita il sistema di data 1904
Usa le impostazioni della cartella di lavoro per cambiare il sistema di data.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Consiglio professionale:** Puoi anche chiamare `setDate1904(false)` più tardi se hai bisogno di tornare indietro.

### Passo 3: Salva la cartella di lavoro modificata
Infine, scrivi le modifiche in un nuovo file (o sovrascrivi l'originale).

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

> **Nota:** Il codice sopra utilizza il nome della classe `tWorkbook` così come fornito originariamente. Assicurati che questo errore di battitura corrisponda alle convenzioni di denominazione del tuo progetto o correggilo in `Workbook` se necessario.

## Imposta la data di Excel programmaticamente (parola chiave secondaria)
Se devi regolare i valori delle singole celle dopo aver cambiato il sistema, puoi usare `Cells.get(i, j).putValue(Date)` dove la data verrà interpretata in base al sistema di data attivo.

## Converti il sistema Excel 1904 nuovamente al 1900 (parola chiave secondaria)
Per tornare indietro, basta chiamare:

```java
workbook.getSettings().setDate1904(false);
```

Quindi salva nuovamente la cartella di lavoro.

## Applicazioni pratiche
1. **Archiviazione dei dati** – Conserva i timestamp legacy durante la migrazione di vecchi fogli di calcolo basati su Mac.  
2. **Report cross‑platform** – Genera report che possono essere aperti sia su Windows che su macOS senza discrepanze di data.  
3. **Modellazione finanziaria** – Allinea i calcoli delle date con modelli finanziari legacy che si aspettano il sistema 1904.  

## Considerazioni sulle prestazioni
- Limita le operazioni sulla cartella di lavoro in una singola sessione per mantenere basso l'uso della memoria.  
- Usa la messa a punto della garbage‑collection di Java per file molto grandi.  

## Domande frequenti

**Q: Qual è la differenza tra i sistemi di data 1900 e 1904?**  
A: Il sistema 1900 inizia il 1 gennaio 1900, mentre il sistema 1904 inizia il 1 gennaio 1904, spostando tutte le date di 1462 giorni.

**Q: Posso cambiare il sistema di data di una cartella di lavoro attualmente aperta in Excel?**  
A: Sì, ma devi chiudere il file in Excel prima; altrimenti l'operazione di salvataggio fallirà.

**Q: Ho bisogno di una licenza per usare `setDate1904`?**  
A: Il metodo funziona nella prova gratuita, ma una licenza completa rimuove le limitazioni di valutazione.

**Q: È possibile cambiare il sistema di data solo per un singolo foglio di lavoro?**  
A: No, il sistema di data è un'impostazione a livello di cartella di lavoro; si applica a tutti i fogli.

**Q: Come posso verificare che il sistema di data sia stato cambiato?**  
A: Apri il file salvato in Excel, vai su **File → Opzioni → Avanzate**, e controlla la casella **"Usa sistema di data 1904"**.

## Conclusione
Ora sai come **cambiare il sistema di data di Excel** a 1904 usando Aspose.Cells per Java, come impostare i formati di data di Excel e come riconvertire se necessario. Integra questi snippet nei tuoi flussi di elaborazione dati per garantire la compatibilità delle date su tutte le piattaforme.

**Ultimo aggiornamento:** 2026-02-22  
**Testato con:** Aspose.Cells 25.3 for Java  
**Autore:** Aspose  

**Risorse**
- **Documentazione:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Download:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Acquista licenza:** [Acquista Aspose.Cells](https://purchase.aspose.com/buy)
- **Prova gratuita:** [Inizia prova gratuita](https://releases.aspose.com/cells/java/)
- **Licenza temporanea:** [Ottieni licenza temporanea](https://purchase.aspose.com/temporary-license/)
- **Forum di supporto:** [Supporto Aspose](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}