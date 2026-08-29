---
category: general
date: 2026-07-16
description: Crea una nuova cartella di lavoro e copia la tabella pivot usando Aspose.Cells
  per Java. Scopri come duplicare la tabella pivot e copiare l’intervallo Excel in
  pochi minuti.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- duplicate pivot table
- how to copy pivot
- copy excel range
language: it
lastmod: 2026-07-16
og_description: Crea una nuova cartella di lavoro e copia la tabella pivot con Aspose.Cells
  per Java. Questa guida mostra come duplicare la tabella pivot e copiare l'intervallo
  Excel in modo efficiente.
og_image_alt: Screenshot of Java code that creates a new workbook and copies a pivot
  table using Aspose.Cells
og_title: Crea una nuova cartella di lavoro e copia la tabella pivot in Java – Tutorial
  completo
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  headline: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  name: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  steps:
  - name: What if the source pivot spans more than one sheet?
    text: Aspose.Cells can only copy ranges within a single worksheet at a time. If
      your pivot stretches across sheets, you’ll need to copy each relevant range
      separately and then re‑link them manually.
  - name: Does this method preserve custom number formats?
    text: Yes. The `copy` method copies cell styles, including number formats, fonts,
      and colors. However, if you have conditional formatting that references external
      ranges, double‑check those references after the copy.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot pulls data from an external connection (e.g., a SQL query),
      the connection information is **not** transferred by `copy`. You’ll need to
      recreate the data source in the destination workbook or embed the source data
      beforehand.
  - name: Can I copy only the pivot layout without the underlying data?
    text: You can achieve that by first clearing the data cells in the source range,
      then copying only the pivot’s layout. This is a more advanced scenario and usually
      not required for a simple **duplicate pivot table** task.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Crea una nuova cartella di lavoro e copia la tabella pivot in Java – Guida
  completa passo passo
url: /it/java/excel-pivot-tables/create-new-workbook-and-copy-pivot-table-in-java-full-step-b/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un nuovo workbook e copia la tabella pivot in Java – Guida completa passo‑passo

Ti sei mai chiesto come **create new workbook** mantenendo una tabella pivot complessa da un file esistente? Se ti sei mai trovato davanti a un foglio Excel, pensando “Ho bisogno di questa pivot in un altro workbook”, e ti sei grattato la testa, non sei solo. La buona notizia è che con Aspose.Cells per Java puoi duplicare una tabella pivot in poche righe.

In questo tutorial percorreremo i passaggi esatti per **copy pivot table** i dati, **duplicate pivot table** le strutture e **copy Excel range** i contenuti—tutto mentre creiamo un nuovo workbook da zero. Alla fine avrai un programma Java pronto‑all'uso che fa esattamente quello che hai richiesto.

## Cosa imparerai

- Come **create new workbook** programmaticamente con Aspose.Cells.
- Il modo preciso per definire l'intervallo che contiene una tabella pivot.
- Tecniche per **copy pivot table** e **duplicate pivot table** senza perdere formattazione o connessioni dati.
- Come **copy Excel range** in modo efficiente e salvare il risultato.
- Problemi comuni e consigli per gestire tabelle pivot di grandi dimensioni.

Non sono necessari riferimenti esterni—tutto è autonomo, eseguibile e spiegato.

---

## Prerequisiti

Prima di immergerci, assicurati di avere:

1. **Java Development Kit (JDK) 11+** – qualsiasi versione recente funziona.
2. **Aspose.Cells for Java** library (the latest version as of 2026‑07‑16). Puoi scaricarla da Maven Central:

   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-cells</artifactId>
       <version>23.12</version>
   </dependency>
   ```

3. Un file Excel di origine (`SourceWithPivot.xlsx`) che contiene già una tabella pivot che desideri copiare.
4. Un IDE o un semplice editor di testo—IntelliJ IDEA, Eclipse o VS Code vanno bene.

Hai tutto? Ottimo—iniziamo.

---

## Passo 1: **Create New Workbook** e carica il file di origine

La prima cosa di cui abbiamo bisogno è un nuovo oggetto workbook che conterrà alla fine la pivot duplicata. Allo stesso tempo dobbiamo caricare il workbook originale così da poter fare riferimento al suo intervallo della tabella pivot.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that already contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Grab the first worksheet where the pivot lives
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

> **Perché è importante:**  
> Caricare il workbook di origine ci dà accesso all'oggetto `Range` sottostante che racchiude la pivot. Se salti questo passaggio non avrai nulla da copiare, e l'operazione **duplicate pivot table** fallirà silenziosamente.

---

## Passo 2: Definisci il **Copy Excel Range** che contiene la Pivot

Una tabella pivot non è una singola cella—si estende su un blocco rettangolare. Dobbiamo indicare ad Aspose.Cells esattamente quali celle copiare.

```java
        // Define the cell range that includes the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

> **Suggerimento:**  
> Se non sei sicuro dell'intervallo esatto, apri il workbook di origine in Excel, seleziona la pivot e guarda la casella del nome. Mostrerà qualcosa come `A1:G20`. Usare l'intervallo esatto garantisce che tutte le impostazioni dei campi, i filtri e i calcoli vengano mantenuti quando **copy pivot table** più tardi.

---

## Passo 3: **Create New Workbook** che riceverà la Pivot copiata

Ora creiamo un workbook nuovissimo—qui vivrà la nostra **duplicate pivot table**.

```java
        // Create a completely empty workbook for the destination
        Workbook dstWb = new Workbook(); // this automatically creates one empty worksheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);
```

> **Cosa succede dietro le quinte?**  
> Il costruttore predefinito crea un workbook con un unico foglio vuoto. Questa è la tela pulita di cui abbiamo bisogno per uno scenario **create new workbook**. Nessuno stile residuo o fogli nascosti di cui preoccuparsi.

---

## Passo 4: **Copy Pivot Table** – Copia effettivamente l'Intervallo Excel definito

Con sia la sorgente che la destinazione pronte, eseguiamo l'operazione di copia. Questo passaggio completa la parte **how to copy pivot** del puzzle.

```java
        // Copy the defined range (which includes the pivot) to the destination worksheet
        srcRange.copy(dstWs.getCells().createRange("A1"));
```

> **Perché `copy` funziona per le pivot:**  
> Aspose.Cells tratta la pivot come parte della collezione di celle. Quando copi l'intervallo, porta con sé la cache della pivot, l'elenco dei campi e il layout. Il risultato è una **duplicate pivot table** pienamente funzionale nel nuovo workbook.

---

## Passo 5: Salva il risultato e verifica l'operazione **Copy Pivot Table**

Infine, salva il workbook di destinazione su disco. Apri il file in Excel per confermare che la pivot appare esattamente come nella sorgente.

```java
        // Save the destination workbook with the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

**Risultato atteso:**  
- `CopyPivotResult.xlsx` si apre con un foglio contenente la stessa tabella pivot vista in `SourceWithPivot.xlsx`.  
- Tutte le etichette di righe/colonne, i filtri e i campi calcolati sono intatti.  
- Ora puoi modificare i dati di origine in modo indipendente, e il nuovo workbook manterrà la sua cache della pivot.

---

## Casi limite e domande comuni

### E se la pivot di origine si estende su più di un foglio?
Aspose.Cells può copiare intervalli solo all'interno di un singolo foglio alla volta. Se la tua pivot si estende su più fogli, dovrai copiare ogni intervallo pertinente separatamente e poi ricollegarli manualmente.

### Questo metodo preserva i formati numerici personalizzati?
Sì. Il metodo `copy` copia gli stili delle celle, inclusi formati numerici, caratteri e colori. Tuttavia, se hai formattazione condizionale che fa riferimento a intervalli esterni, verifica nuovamente quei riferimenti dopo la copia.

### Come copiare una pivot che utilizza una fonte dati esterna?
Quando la pivot estrae dati da una connessione esterna (ad esempio, una query SQL), le informazioni di connessione **non** vengono trasferite da `copy`. Dovrai ricreare la fonte dati nel workbook di destinazione o incorporare i dati di origine in anticipo.

### Posso copiare solo il layout della pivot senza i dati sottostanti?
Puoi ottenerlo cancellando prima le celle dei dati nell'intervallo di origine, poi copiando solo il layout della pivot. Questo è uno scenario più avanzato e di solito non necessario per un semplice compito di **duplicate pivot table**.

---

## Esempio completo funzionante (tutti i passaggi combinati)

Di seguito trovi la classe Java completa, pronta‑all'uso. Sostituisci `YOUR_DIRECTORY` con il percorso reale della cartella sul tuo computer.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the exact range that holds the pivot table
        // Adjust "A1:G20" to match your pivot's size
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a brand‑new workbook that will receive the copy
        Workbook dstWb = new Workbook(); // creates an empty workbook with one sheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);

        // Step 4: Copy the pivot (and any surrounding data) to the new workbook
        srcRange.copy(dstWs.getCells().createRange("A1"));

        // Step 5: Save the destination file – now it contains the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully! Check CopyPivotResult.xlsx.");
    }
}
```

Esegui il programma (`java CopyPivotTableDemo`) e vedrai il messaggio nella console che conferma il successo.

---

## Consigli professionali e best practice

- **Valida l'intervallo** prima di copiare. Usa `srcWs.getCells().maxDisplayRange` per scoprire programmaticamente l'area utilizzata se non vuoi codificare manualmente `"A1:G20"`.
- **Disattiva il calcolo** temporaneamente per workbook enormi per velocizzare la copia:

  ```java
  srcWb.getSettings().setCalculateFormulaOnOpen(false);
  ```

- **Rilascia le risorse** (`srcWb.dispose(); dstWb.dispose();`) nei servizi a lunga esecuzione per evitare perdite di memoria.
- **Compatibilità di versione:** Il codice funziona con Aspose.Cells 23.12 e successive. Versioni più vecchie potrebbero richiedere `srcRange.copyTo` invece di `copy`.

---

## Prossimi passi

Ora che hai padroneggiato **create new workbook** e **copy pivot table**, potresti esplorare:

- **How to copy pivot** su più fogli di lavoro in un job batch.
- Aggiungere **copy excel range** per tabelle di dati regolari accanto alla pivot.
- Automatizzare la creazione di **duplicate pivot table** per il report di ogni mese usando un ciclo.
- Esportare la pivot duplicata in PDF o HTML con i renderer integrati di Aspose.Cells.

Ognuno di questi argomenti si basa sulle fondamenta poste qui, e tutti beneficiano dello stesso approccio pulito e programmatico.

---

## Conclusione

Abbiamo percorso l'intero processo di **create new workbook**, definito il **copy excel range** di origine e **copy pivot table** per produrre una **duplicate pivot table** in Java usando Aspose.Cells. La soluzione è concisa, completamente funzionale e pronta per l'uso in produzione. Sentiti libero di modificare l'intervallo, sperimentare con file di origine diversi, o incorporare questa logica in un pipeline di reporting più ampio.

Se incontri problemi o hai idee per ampliare questo tutorial, lascia un commento qui sotto. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}