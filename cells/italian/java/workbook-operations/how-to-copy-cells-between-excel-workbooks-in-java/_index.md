---
category: general
date: 2026-11-16
description: Come copiare celle tra cartelle di lavoro Excel in Java – caricare una
  cartella di lavoro, copiare un intervallo tra cartelle di lavoro (inclusa una tabella
  pivot) e salvare il file della cartella di lavoro.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: it
lastmod: 2026-11-16
og_description: Come copiare le celle tra cartelle di lavoro Excel in Java. Impara
  a caricare una cartella di lavoro Excel, copiare un intervallo (inclusa una tabella
  pivot) tra le cartelle di lavoro e salvare il file della cartella di lavoro.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: Come copiare celle tra cartelle di lavoro Excel in Java – guida completa
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: Come copiare le celle tra cartelle di lavoro Excel in Java
url: /it/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare celle tra cartelle di lavoro Excel in Java

Se devi **copiare celle** da una cartella di lavoro Excel a un'altra usando Java, questa guida ti mostra un modo affidabile per farlo. Imparerai come **caricare una cartella di lavoro Excel con Java**, copiare un intervallo che può contenere una tabella pivot e, infine, **salvare il file della cartella di lavoro** con i dati copiati.

Questo tutorial copre:

* Caricamento di una cartella di lavoro sorgente e selezione di un foglio di lavoro.  
* Definizione dell’intervallo esatto da spostare (inclusa una tabella pivot).  
* Creazione di una cartella di lavoro di destinazione e copia dell’intervallo.  
* Salvataggio del file di destinazione.  

L’esempio utilizza la libreria Aspose.Cells per Java, che lavora con i file Excel senza richiedere Microsoft Office. Il codice funziona su Java 8+ e su qualsiasi IDE moderno (IntelliJ IDEA, Eclipse, VS Code, ecc.).

---

## Prerequisiti

Prima di iniziare, assicurati di avere:

| Requisito | Motivo |
|-------------|--------|
| Java Development Kit (JDK) 8 o più recente | Necessario per compilare ed eseguire il codice. |
| Maven o Gradle build tool | Semplifica l’aggiunta della dipendenza Aspose.Cells. |
| Aspose.Cells for Java library (latest version) | Fornisce le classi `Workbook`, `Worksheet` e `Range` usate nell’esempio. |
| Due file Excel (`source.xlsx` e una cartella vuota per `dest.xlsx`) | Il file sorgente deve contenere i dati e, facoltativamente, una tabella pivot da copiare. |

Aggiungi la dipendenza Aspose.Cells al tuo `pom.xml` (Maven) o `build.gradle` (Gradle). Esempio per Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## Come copiare celle con Aspose.Cells

I passaggi seguenti ti guidano attraverso l’intero processo. Ogni passaggio include il codice Java, una spiegazione del **perché** è importante e un suggerimento per evitare problemi comuni.

### Passo 1: Carica la cartella di lavoro sorgente

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Perché?**  
`Workbook` rappresenta l’intero file Excel. Caricandolo ottieni l’accesso a tutti i fogli, celle e oggetti come le tabelle pivot. Usare il primo foglio è comune, ma puoi selezionare qualsiasi foglio per nome (`srcWb.getWorksheets().get("Sheet2")`).

**Suggerimento professionale:**  
Se il file sorgente è grande, considera di caricarlo in modalità *memory‑efficient*: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }})`

### Passo 2: Definisci l’intervallo che include la tabella pivot

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Perché?**  
Un oggetto `Range` astrae un blocco rettangolare di celle. Specificando `"A1:G20"` indichi ad Aspose.Cells esattamente quali celle—inclusa l’eventuale tabella pivot—copiare. La libreria copia automaticamente dati sottostanti, stili e definizioni della pivot.

**Caso limite:**  
Se la tabella pivot si estende oltre l’intervallo definito, amplia l’indirizzo (ad es., `"A1:Z100"`). Puoi anche usare `srcWs.getCells().getMaxDataColumn()` e `getMaxDataRow()` per calcolare dinamicamente l’area utilizzata.

### Passo 3: Crea la cartella di lavoro di destinazione

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Perché?**  
Una nuova cartella di lavoro garantisce che nessuna formattazione indesiderata o foglio nascosto interferisca con il contenuto copiato. La cartella di lavoro predefinita contiene già un foglio, che useremo come destinazione.

### Passo 4: Copia l’intervallo nella cartella di lavoro di destinazione

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Perché?**  
`copyRange` gestisce tutti gli attributi delle celle: valori, formule, formattazione e persino le cache delle pivot. Copiando su `"A1"` posizioni l’intervallo nell’angolo in alto a sinistra del foglio di destinazione, preservando il layout originale.

**Domanda comune:** *La tabella pivot rimarrà funzionale?*  
Sì. Aspose.Cells copia la definizione della pivot e la sua cache, quindi la pivot funziona esattamente come nella cartella di lavoro sorgente.

### Passo 5: Salva la cartella di lavoro di destinazione

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Perché?**  
Invocare `save` scrive la cartella di lavoro in memoria su un file fisico `.xlsx`. Puoi anche salvare in altri formati (`.xls`, `.csv`, `.pdf`) cambiando l’estensione del file o usando `SaveOptions`.

**Suggerimento:**  
Se devi inviare il file in risposta a una richiesta web, usa `destWb.save(OutputStream, SaveFormat.XLSX);` invece di un percorso file.

---

## Copia intervallo tra cartelle di lavoro – codice sorgente completo

Di seguito trovi la classe Java completa, pronta per l’esecuzione. Sostituisci `YOUR_DIRECTORY` con la cartella reale sul tuo computer.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Risultato atteso:**  
`dest.xlsx` contiene una replica esatta dell’intervallo `A1:G20` di `source.xlsx`. Se l’intervallo sorgente conteneva una tabella pivot, il file di destinazione mostra la stessa pivot con la fonte dati correttamente collegata alle celle copiate.

Puoi aprire `dest.xlsx` in Excel, LibreOffice o qualsiasi visualizzatore che supporti `.xlsx` per verificare che valori, formattazione e funzionalità della pivot siano preservati.

---

## Copia tabella pivot – cosa devi sapere

* **La cache della pivot viene copiata automaticamente.** La libreria trasferisce la cache sottostante, quindi non è necessario aggiornare manualmente la pivot.
* **Le fonti dati esterne non vengono trasferite.** Se la pivot estrae dati da un database esterno, devi assicurarti che la cartella di lavoro di destinazione possa accedere alla stessa fonte, oppure ricreare la cache localmente.
* **Le tabelle pivot molto grandi possono aumentare l’uso di memoria.** Per cartelle di lavoro molto grandi, considera di aumentare l’heap JVM (`-Xmx2g`) per evitare `OutOfMemoryError`.

---

## Salva il file della cartella di lavoro in formati diversi

Aspose.Cells ti consente di salvare il risultato in molti formati senza modificare il codice:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

Scegli il formato che corrisponde al tuo processo successivo. La stessa logica `copyRange` funziona indipendentemente dal formato finale.

---

## Caricamento di una cartella di lavoro Excel con Java – consigli aggiuntivi

* **Caricamento di file criptati:** Usa `LoadOptions` con una password:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Lettura di fogli specifici:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

Queste opzioni possono velocizzare il passaggio **load excel workbook java**, soprattutto per file di grandi dimensioni.

---

## Conclusione

Ora sai **come copiare celle** tra cartelle di lavoro Excel in Java, come **copiare un intervallo tra cartelle di lavoro** che contiene una **tabella pivot**, e come **salvare il file della cartella di lavoro** nel formato necessario. Seguendo i passaggi sopra, puoi integrare la manipolazione dei dati Excel in qualsiasi applicazione Java—che tu stia costruendo un motore di reporting, una pipeline ETL o un semplice utility di conversione file.

**Prossimi passi** che potresti esplorare:

* Usa **copy range between workbooks** per unire più report in


## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell’API e a esplorare approcci alternativi nei tuoi progetti.

- [Save New Workbook in Java – Copy Range Between Workbooks Tutorial](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [How to copy pivot tables between Excel workbooks in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [How to copy range in Java – Copy Pivot Table with Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}