---
date: '2025-12-10'
description: Scopri come aggiungere collegamenti ipertestuali alle immagini in Excel
  con Aspose.Cells per Java, trasformando le immagini statiche in link interattivi
  per fogli di calcolo più ricchi.
keywords:
- image hyperlinks in Excel
- Aspose.Cells for Java
- interactive Excel spreadsheets
title: Come aggiungere un collegamento ipertestuale alle immagini in Excel usando
  Aspose.Cells per Java
url: /it/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiungere collegamenti ipertestuali alle immagini in Excel usando Aspose.Cells per Java

## Introduzione

Se vuoi rendere i tuoi report Excel più interattivi, imparare **come aggiungere collegamenti ipertestuali** alle immagini è un ottimo punto di partenza. In questo tutorial vedrai come Aspose.Cells per Java ti consente di incorporare immagini cliccabili, trasformando visualizzazioni statiche in collegamenti funzionali che aprono pagine web, documenti o altre risorse direttamente dal foglio di calcolo.

### Cosa imparerai
- Inizializzare una cartella di lavoro Aspose.Cells in Java.  
- Inserire un'immagine e trasformarla in un collegamento ipertestuale.  
- Metodi chiave come `addHyperlink`, `setPlacement` e `setScreenTip`.  
- Best practice per le prestazioni e la licenza.

## Risposte rapide
- **Quale libreria è necessaria?** Aspose.Cells per Java.  
- **Posso usare file .xlsx?** Sì – l'API funziona sia con .xls che con .xlsx.  
- **Ho bisogno di una licenza?** Una versione di prova funziona per la valutazione; è necessaria una licenza permanente per la produzione.  
- **Quante righe di codice?** Circa 20 righe per aggiungere un'immagine cliccabile.  
- **È thread‑safe?** Gli oggetti Workbook non sono thread‑safe; crea istanze separate per ogni thread.

## Come aggiungere un collegamento ipertestuale a un'immagine in Excel

### Prerequisiti
Prima di iniziare, assicurati di avere:

- **Aspose.Cells per Java** (v25.3 o successiva).  
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
Aspose.Cells è commerciale, ma puoi iniziare con una versione di prova gratuita o richiedere una licenza temporanea:

- Versione di prova gratuita: scarica da [Aspose Downloads](https://releases.aspose.com/cells/java/).  
- Licenza temporanea: richiedi tramite la [pagina Licenza temporanea](https://purchase.aspose.com/temporary-license/).  
- Acquisto: per un utilizzo a lungo termine, visita [Aspose Purchase](https://purchase.aspose.com/buy).

### Inizializzazione di base
Crea una cartella di lavoro e ottieni il primo foglio di lavoro:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Implementazione passo‑passo

### Passo 1: Preparare la cartella di lavoro
Iniziamo creando una nuova cartella di lavoro e selezionando il primo foglio.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Passo 2: Inserire un'etichetta e regolare la dimensione della cella
Aggiungi un'etichetta descrittiva e assegna alla cella spazio sufficiente per l'immagine.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```

### Passo 3: Aggiungere l'immagine
Carica il file immagine e posizionalo sul foglio.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```
*Suggerimento*: sostituisci `"path/to/aspose-logo.jpg"` con il percorso reale del tuo file immagine.

### Passo 4: Configurare il posizionamento e aggiungere il collegamento ipertestuale
Rendi l'immagine libera e allega un collegamento ipertestuale.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```

### Passo 5: Impostare un suggerimento a comparsa e salvare la cartella di lavoro
Fornisci un tooltip utile e scrivi la cartella di lavoro su disco.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```

## Suggerimenti per la risoluzione dei problemi
- **Errori nel percorso dell'immagine** – verifica il percorso del file e assicurati che l'applicazione abbia i permessi di lettura.  
- **Licenza non applicata** – se la versione di prova scade, i collegamenti ipertestuali potrebbero non funzionare; applica una licenza valida con `License.setLicense`.  
- **Collegamento ipertestuale non cliccabile** – verifica che il `PlacementType` dell'immagine sia impostato su `FREE_FLOATING`.

## Applicazioni pratiche
1. **Report di marketing** – collega i loghi del brand alle pagine dei prodotti.  
2. **Documentazione tecnica** – allega diagrammi che aprono schemi dettagliati.  
3. **Fogli di lavoro educativi** – trasforma le icone in scorciatoie per video supplementari.  
4. **Dashboard di progetto** – fai aprire le icone di stato i tracker di attività correlati.

## Considerazioni sulle prestazioni
- Mantieni le dimensioni dei file immagine ragionevoli; le immagini grandi aumentano l'uso di memoria della cartella di lavoro.  
- Rilascia gli oggetti inutilizzati (`workbook.dispose()`) quando elabori molti file in un ciclo.  
- Aggiorna alla versione più recente di Aspose.Cells per miglioramenti delle prestazioni e correzioni di bug.

## Conclusione
Adesso sai **come aggiungere collegamenti ipertestuali** alle immagini in Excel usando Aspose.Cells per Java, consentendoti di creare fogli di calcolo più ricchi e interattivi. Sperimenta con URL diversi, suggerimenti a comparsa e posizionamenti delle immagini per adattarli alle tue esigenze di reporting. Successivamente, potresti esplorare l'aggiunta di collegamenti ipertestuali a forme o l'automazione dell'inserimento di immagini in blocco su più fogli.

## Domande frequenti

**Q:** Qual è la dimensione massima dell'immagine supportata da Aspose.Cells per Java?  
**A:** Non esiste un limite rigido, ma immagini molto grandi possono influire sulle prestazioni e aumentare la dimensione del file.

**Q:** Posso usare questa funzionalità con file .xlsx?  
**A:** Sì, l'API funziona sia con i formati `.xls` che `.xlsx`.

**Q:** Come dovrei gestire le eccezioni quando aggiungo collegamenti ipertestuali?  
**A:** Avvolgi il codice in un blocco try‑catch e registra i dettagli dell'`Exception` per diagnosticare problemi di percorso o licenza.

**Q:** È possibile rimuovere un collegamento ipertestuale da un'immagine dopo averlo aggiunto?  
**A:** Sì – recupera l'oggetto `Picture` e chiama `pic.getHyperlink().remove()` o elimina l'immagine dalla collezione.

**Q:** Perché il mio collegamento ipertestuale potrebbe non funzionare come previsto?  
**A:** Le cause comuni includono una stringa URL errata, mancanza del prefisso `http://`/`https://`, o una versione di prova non licenziata che disabilita alcune funzionalità.

## Risorse aggiuntive
- **Documentazione:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Acquisto e prova:** visita [Aspose Purchase](https://purchase.aspose.com/buy) o [Temporary License Page](https://purchase.aspose.com/temporary-license/) per le opzioni di licenza.  
- **Forum di supporto:** per assistenza, consulta il [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.Cells for Java 25.3  
**Author:** Aspose