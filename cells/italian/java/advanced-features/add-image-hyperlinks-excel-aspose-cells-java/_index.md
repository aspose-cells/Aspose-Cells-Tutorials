---
date: '2026-09-02'
description: Scopri come creare cartelle di lavoro Excel con immagini cliccabili usando
  Aspose.Cells for Java, aggiungendo hyperlinks alle immagini per fogli di calcolo
  interattivi.
keywords:
- create clickable image
- add image hyperlink
- add hyperlink to picture
- interactive excel spreadsheet
- how to add hyperlink
lastmod: '2026-09-02'
og_description: Scopri come creare cartelle di lavoro Excel con immagini cliccabili
  usando Aspose.Cells for Java, aggiungendo hyperlinks, screen tips e ottimizzando
  le prestazioni in poche righe di codice.
og_image_alt: 'Developer guide: create clickable image Excel using Aspose.Cells for
  Java'
og_title: Crea un'immagine cliccabile in Excel usando Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  headline: Create clickable image Excel using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  name: Create clickable image Excel using Aspose.Cells for Java
  steps:
  - name: prepare your workbook
    text: We start by creating a new workbook and selecting the first sheet.
  - name: insert a label and adjust cell size
    text: Add a descriptive label and give the cell enough space for the picture.
  - name: add the image
    text: '`Picture` represents an image object placed on a worksheet. *Tip*: Replace
      `"path/to/aspose-logo.jpg"` with the actual path to your image file.'
  - name: configure placement and add the hyperlink
    text: '`Hyperlink` defines a link associated with a cell, shape, or picture, enabling
      navigation when clicked.'
  - name: set a screen tip and save the workbook
    text: Provide a helpful tooltip and write the workbook to disk.
  type: HowTo
- questions:
  - answer: Aspose.Cells for Java.
    question: What library is required?
  - answer: Yes – the API works with both .xls and .xlsx.
    question: Can I use .xlsx files?
  - answer: A trial works for evaluation; a permanent license is required for production.
    question: Do I need a license?
  - answer: About 20 lines to add a clickable image.
    question: How many lines of code?
  - answer: Workbook objects are not thread‑safe; create separate instances per thread.
    question: Is it thread‑safe?
  type: FAQPage
tags:
- create clickable image
- Aspose.Cells
- Java Excel automation
title: Crea un'immagine cliccabile in Excel usando Aspose.Cells for Java
url: /it/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea immagine Excel cliccabile usando Aspose.Cells per Java

## Introduzione

Se desideri **creare immagini Excel cliccabili** nei cartelle di lavoro che consentono agli utenti di passare a siti web, documenti o altre risorse con un solo clic, sei nel posto giusto. In questo tutorial vedremo come Aspose.Cells per Java ti permette di **aggiungere oggetti immagine Excel con hyperlink**, configurare suggerimenti a comparsa e mantenere i tuoi fogli di calcolo sia belli che funzionali.

### Cosa imparerai
- Inizializzare una cartella di lavoro Aspose.Cells in Java.  
- Inserire un'immagine e trasformarla in un hyperlink cliccabile.  
- Metodi chiave come `addHyperlink`, `setPlacement` e `setScreenTip`.  
- Best practice per prestazioni e licenze.

## Risposte rapide
- **Quale libreria è necessaria?** Aspose.Cells for Java.  
- **Posso usare file .xlsx?** Sì – l'API funziona sia con .xls che con .xlsx.  
- **Ho bisogno di una licenza?** Una versione di prova funziona per la valutazione; è necessaria una licenza permanente per la produzione.  
- **Quante righe di codice?** Circa 20 righe per aggiungere un'immagine cliccabile.  
- **È thread‑safe?** Gli oggetti Workbook non sono thread‑safe; crea istanze separate per thread.  
- **Posso aggiungere un suggerimento a comparsa in Excel?** Sì – usa `Hyperlink.setScreenTip()` per mostrare un testo di aiuto al passaggio del mouse.

## Come creare un'immagine Excel cliccabile con Aspose.Cells per Java

Crei una cartella di lavoro Excel con immagine cliccabile caricando o creando un `Workbook`, inserendo un oggetto `Picture`, collegando un `Hyperlink` a quell'immagine, impostando facoltativamente un suggerimento a comparsa e infine salvando il file. L'API gestisce tutto l'XML di Excel a basso livello, così scrivi solo poche righe di codice Java semplici.

### Prerequisiti
Prima di iniziare, assicurati di avere:

- **Aspose.Cells for Java** (v25.3 o successiva).  
- **JDK 8+** installato.  
- Un IDE (IntelliJ IDEA, Eclipse o NetBeans) e Maven o Gradle per la gestione delle dipendenze.  

### Librerie richieste
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

### Acquisizione della licenza
Aspose.Cells è commerciale, ma puoi iniziare con una prova gratuita o richiedere una licenza temporanea:

- Prova gratuita: scarica da [Aspose Downloads](https://releases.aspose.com/cells/java/).  
- Licenza temporanea: richiedi tramite la [Temporary License page](https://purchase.aspose.com/temporary-license/).  
- Acquisto: per un uso a lungo termine, visita [Aspose Purchase](https://purchase.aspose.com/buy).

### Inizializzazione di base
La classe `Workbook` rappresenta un intero file Excel in memoria. La istanzi, poi ottieni un riferimento al primo foglio di lavoro. `Worksheet` rappresenta un singolo foglio all'interno della cartella di lavoro.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

## Implementazione passo‑passo

### Passo 1: prepara la tua cartella di lavoro
Iniziamo creando una nuova cartella di lavoro e selezionando il primo foglio.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

### Passo 2: inserisci un'etichetta e regola la dimensione della cella
Aggiungi un'etichetta descrittiva e concedi alla cella spazio sufficiente per l'immagine.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```  

### Passo 3: aggiungi l'immagine
`Picture` rappresenta un oggetto immagine posizionato su un foglio di lavoro.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```  
*Suggerimento*: Sostituisci `"path/to/aspose-logo.jpg"` con il percorso reale del tuo file immagine.

### Passo 4: configura il posizionamento e aggiungi l'hyperlink
`Hyperlink` definisce un collegamento associato a una cella, forma o immagine, abilitando la navigazione al clic.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```  

### Passo 5: imposta un suggerimento a comparsa e salva la cartella di lavoro
Fornisci un tooltip utile e scrivi la cartella di lavoro su disco.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```  

## Perché aggiungere un hyperlink a un'immagine Excel?
Incorporare un'immagine cliccabile ti consente di trasformare elementi di branding, icone o diagrammi in punti di navigazione diretti, riducendo il numero di clic necessari per raggiungere contenuti correlati. Questo approccio aumenta l'efficienza dell'utente in dashboard di marketing, manuali tecnici e fogli di lavoro educativi.

## Come aggiungere un suggerimento a comparsa in Excel
Aggiungi un suggerimento a comparsa chiamando `hyperlink.setScreenTip("Your tip here")` sull'oggetto `Hyperlink` collegato all'immagine. Il suggerimento appare quando il cursore passa sopra l'immagine, fornendo agli utenti indicazioni contestuali senza ingombrare il foglio.

## Suggerimenti per la risoluzione dei problemi
- **Errori di percorso dell'immagine** – verifica il percorso del file e assicurati che l'applicazione abbia i permessi di lettura.  
- **Licenza non applicata** – se la prova scade, gli hyperlink potrebbero smettere di funzionare; applica una licenza valida con `License.setLicense`.  
- **Hyperlink non cliccabile** – verifica che il `PlacementType` dell'immagine sia impostato su `FREE_FLOATING`.

## Applicazioni pratiche
1. **Report di marketing** – collega i loghi del brand alle pagine prodotto.  
2. **Documentazione tecnica** – allega diagrammi che aprono schemi dettagliati.  
3. **Fogli di lavoro educativi** – trasforma le icone in scorciatoie per video supplementari.  
4. **Dashboard di progetto** – fai aprire le icone di stato ai tracker di attività correlati.

## Considerazioni sulle prestazioni
- Mantieni le dimensioni dei file immagine ragionevoli; immagini grandi aumentano l'uso di memoria della cartella di lavoro.  
- Elimina gli oggetti non usati (`workbook.dispose()`) quando elabori molti file in un ciclo.  
- Aggiorna alla versione più recente di Aspose.Cells per miglioramenti delle prestazioni e correzioni di bug.

## Conclusione
Ora sai come aggiungere un hyperlink alle immagini in Excel usando Aspose.Cells per Java, consentendoti di **creare cartelle di lavoro Excel con immagini cliccabili** più ricche e interattive. Sperimenta con URL diversi, suggerimenti a comparsa e posizionamenti delle immagini per adattarli alle tue esigenze di reporting. Successivamente, potresti esplorare l'aggiunta di hyperlink a forme o l'automazione dell'inserimento di immagini in blocco su più fogli di lavoro.

## Domande frequenti

**Q:** Qual è la dimensione massima dell'immagine supportata da Aspose.Cells per Java?  
**A:** Non c'è un limite rigido, ma immagini molto grandi possono influire sulle prestazioni e aumentare la dimensione del file.

**Q:** Posso usare questa funzionalità con file .xlsx?  
**A:** Sì, l'API funziona sia con i formati `.xls` che `.xlsx`.

**Q:** Come dovrei gestire le eccezioni quando aggiungo hyperlink?  
**A:** Avvolgi il codice in un blocco try‑catch e registra i dettagli dell'`Exception` per diagnosticare problemi di percorso o licenza.

**Q:** È possibile rimuovere un hyperlink da un'immagine dopo averlo aggiunto?  
**A:** Sì – recupera l'oggetto `Picture` e chiama `pic.getHyperlink().remove()` o elimina l'immagine dalla collezione.

**Q:** Perché il mio hyperlink potrebbe non funzionare come previsto?  
**A:** Le cause comuni includono una stringa URL errata, mancanza del prefisso `http://`/`https://`, o una versione di prova non licenziata che disabilita alcune funzionalità.

## Risorse aggiuntive
- **Documentazione:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Acquisto e prova:** Visita [Aspose Purchase](https://purchase.aspose.com/buy) o [Temporary License Page](https://purchase.aspose.com/temporary-license/) per opzioni di licenza.  
- **Forum di supporto:** Per assistenza, consulta il [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**Last updated:** 2026-09-02  
**Tested with:** Aspose.Cells for Java 25.3  
**Author:** Aspose

## Tutorial correlati

- [Come creare hyperlink in Excel usando Aspose.Cells per Java - Guida passo‑passo](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [Come formattare le celle Excel e aggiungere hyperlink usando Aspose.Cells per Java](/cells/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aggiungere immagine a commento Excel con Aspose.Cells per Java: Guida completa](/cells/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}