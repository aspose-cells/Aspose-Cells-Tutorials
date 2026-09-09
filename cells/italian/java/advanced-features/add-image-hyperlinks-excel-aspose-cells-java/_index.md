---
date: '2026-02-16'
description: Scopri come creare un Excel con immagini cliccabili usando Aspose.Cells
  per Java, aggiungendo collegamenti ipertestuali alle foto per fogli di calcolo interattivi.
keywords:
- image hyperlinks in Excel
- Aspose.Cells for Java
- interactive Excel spreadsheets
title: Crea un Excel con immagine cliccabile usando Aspose.Cells per Java
url: /it/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Crea un Excel con Immagine Cliccabile usando Aspose.Cells per Java

## Introduzione

Se vuoi **creare un workbook Excel con immagine cliccabile** che consenta agli utenti di passare a siti web, documenti o altre risorse con un solo clic, sei nel posto giusto. In questo tutorial vedremo come Aspose.Cells per Java ti permette di **aggiungere oggetti immagine Excel con hyperlink**, configurare i suggerimenti a comparsa e mantenere i tuoi fogli di calcolo sia belli che funzionali.

### Cosa Imparerai
- Inizializzare un workbook Aspose.Cells in Java.  
- Inserire un'immagine e trasformarla in un hyperlink cliccabile.  
- Metodi chiave come `addHyperlink`, `setPlacement` e `setScreenTip`.  
- Best practice per prestazioni e licenze.

## Risposte Rapide
- **Quale libreria è necessaria?** Aspose.Cells per Java.  
- **Posso usare file .xlsx?** Sì – l'API funziona sia con .xls che con .xlsx.  
- **È necessaria una licenza?** Una versione di prova funziona per la valutazione; è richiesta una licenza permanente per la produzione.  
- **Quante righe di codice?** Circa 20 righe per aggiungere un'immagine cliccabile.  
- **È thread‑safe?** Gli oggetti Workbook non sono thread‑safe; crea istanze separate per ogni thread.  
- **Posso aggiungere un suggerimento a comparsa in Excel?** Sì – usa `Hyperlink.setScreenTip()` per mostrare un testo di aiuto al passaggio del mouse.

## Come creare un Excel con immagine cliccabile usando Aspose.Cells per Java

### Prerequisiti
Prima di iniziare, assicurati di avere:

- **Aspose.Cells per Java** (v25.3 o successivo).  
- **JDK 8+** installato.  
- Un IDE (IntelliJ IDEA, Eclipse o NetBeans) e Maven o Gradle per la gestione delle dipendenze.  

### Librerie Richieste
Aggiungi Aspose.Cells al tuo progetto:

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

### Acquisizione della Licenza
Aspose.Cells è commerciale, ma puoi iniziare con una prova gratuita o richiedere una licenza temporanea:

- Prova gratuita: scarica da [Aspose Downloads](https://releases.aspose.com/cells/java/).  
- Licenza temporanea: richiedi tramite la [Temporary License page](https://purchase.aspose.com/temporary-license/).  
- Acquisto: per un utilizzo a lungo termine, visita [Aspose Purchase](https://purchase.aspose.com/buy).

### Inizializzazione di Base
Crea un workbook e ottieni il primo foglio di lavoro:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Implementazione Passo‑Passo

### Passo 1: Prepara il tuo Workbook
Iniziamo creando un nuovo workbook e selezionando il primo foglio.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Passo 2: Inserisci un'etichetta e regola la dimensione della cella
Aggiungi un'etichetta descrittiva e assegna alla cella spazio sufficiente per l'immagine.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```

### Passo 3: Aggiungi l'Immagine
Carica il file immagine e posizionalo sul foglio.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```
*Suggerimento*: sostituisci `"path/to/aspose-logo.jpg"` con il percorso reale del tuo file immagine.

### Passo 4: Configura il posizionamento e aggiungi l'hyperlink
Rendi l'immagine libera (free‑floating) e collega un hyperlink ad essa.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```

### Passo 5: Imposta un suggerimento a comparsa e salva il workbook
Fornisci un tooltip utile e scrivi il workbook su disco.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```

## Perché aggiungere un'immagine Excel con hyperlink?
Incorporare un'immagine cliccabile ti consente di trasformare elementi di branding, icone o diagrammi in punti di navigazione diretti. Questo migliora l'esperienza dell'utente in dashboard di marketing, manuali tecnici e fogli di lavoro educativi, riducendo il numero di clic necessari per raggiungere contenuti correlati.

## Come aggiungere un suggerimento a comparsa in Excel
Il metodo `setScreenTip` ti permette di definire il testo che appare quando l'utente posiziona il cursore sull'immagine. È ideale per fornire contesto, ad esempio “Visualizza dettagli prodotto” o “Apri video tutorial”.

## Suggerimenti per la Risoluzione dei Problemi
- **Errori nel percorso dell'immagine** – verifica il percorso del file e assicurati che l'applicazione abbia i permessi di lettura.  
- **Licenza non applicata** – se la versione di prova scade, gli hyperlink potrebbero smettere di funzionare; applica una licenza valida con `License.setLicense`.  
- **Hyperlink non cliccabile** – controlla che il `PlacementType` dell'immagine sia impostato su `FREE_FLOATING`.

## Applicazioni Pratiche
Incorporare immagini cliccabili è utile in molti scenari:

1. **Report di marketing** – collega i loghi del brand alle pagine prodotto.  
2. **Documentazione tecnica** – allega diagrammi che aprono schemi dettagliati.  
3. **Fogli di lavoro educativi** – trasforma le icone in scorciatoie per video supplementari.  
4. **Dashboard di progetto** – fai aprire icone di stato i tracker di attività correlati.

## Considerazioni sulle Prestazioni
- Mantieni le dimensioni dei file immagine ragionevoli; immagini molto grandi aumentano l'uso di memoria del workbook.  
- Dispone degli oggetti non più utilizzati (`workbook.dispose()`) quando elabori molti file in un ciclo.  
- Aggiorna alla versione più recente di Aspose.Cells per miglioramenti di prestazioni e correzioni di bug.

## Conclusione
Ora sai **come aggiungere hyperlink** alle immagini in Excel usando Aspose.Cells per Java, consentendoti di **creare workbook Excel con immagine cliccabile** più ricchi e interattivi. Sperimenta con URL diversi, suggerimenti a comparsa e posizionamenti delle immagini per adattarli alle tue esigenze di reporting. Successivamente, potresti esplorare l'aggiunta di hyperlink a forme o l'automazione dell'inserimento di immagini in blocco su più fogli di lavoro.

## Domande Frequenti

**D:** Qual è la dimensione massima dell'immagine supportata da Aspose.Cells per Java?  
**R:** Non esiste un limite rigido, ma immagini molto grandi possono influire sulle prestazioni e aumentare la dimensione del file.

**D:** Posso usare questa funzionalità con file .xlsx?  
**R:** Sì, l'API funziona sia con i formati `.xls` che `.xlsx`.

**D:** Come dovrei gestire le eccezioni quando aggiungo hyperlink?  
**R:** Avvolgi il codice in un blocco try‑catch e registra i dettagli dell'`Exception` per diagnosticare problemi di percorso o licenza.

**D:** È possibile rimuovere un hyperlink da un'immagine dopo averlo aggiunto?  
**R:** Sì – recupera l'oggetto `Picture` e chiama `pic.getHyperlink().remove()` oppure elimina l'immagine dalla collezione.

**D:** Perché il mio hyperlink potrebbe non funzionare come previsto?  
**R:** Le cause comuni includono una stringa URL errata, l'assenza del prefisso `http://`/`https://` o una versione di prova non licenziata che disabilita alcune funzionalità.

## Risorse Aggiuntive
- **Documentazione:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Acquisto e Prova:** visita [Aspose Purchase](https://purchase.aspose.com/buy) o [Temporary License Page](https://purchase.aspose.com/temporary-license/) per le opzioni di licenza.  
- **Forum di Supporto:** per assistenza, consulta il [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**Last Updated:** 2026-02-16  
**Tested With:** Aspose.Cells for Java 25.3  
**Author:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}