---
category: general
date: 2026-07-06
description: Come copiare una tabella pivot in Java con Aspose.Cells – guida passo‑passo
  per duplicare programmaticamente le tabelle pivot di Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: it
lastmod: 2026-07-06
og_description: Come copiare una tabella pivot in Java usando Aspose.Cells ti consente
  di duplicare rapidamente e in modo affidabile le tabelle pivot di Excel.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: Come copiare una tabella pivot in Java – Guida completa ad Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: Come copiare una tabella pivot in Java usando Aspose.Cells
url: /it/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare una tabella pivot in Java usando Aspose.Cells

Ti sei mai chiesto **come copiare le pivot** all'interno di un file Excel senza aprire manualmente la cartella di lavoro? Non sei l'unico. In molti flussi di reporting è necessario **duplicare le tabelle pivot di Excel** al volo—magari per creare uno snapshot, spostarla in un nuovo foglio, o generare un modello per gli utenti downstream.

In questo tutorial percorreremo un esempio completo e eseguibile che mostra esattamente questo. Utilizzando la libreria Aspose.Cells per Java caricheremo una cartella di lavoro, individueremo l'intervallo pivot di origine, lo copieremo in una nuova posizione e salveremo il risultato. Nessun riferimento vago, solo una soluzione concreta che puoi inserire nel tuo progetto oggi.

---

## Prerequisiti

* **Java Development Kit (JDK) 8+** – il codice si compila con qualsiasi JDK recente.  
* **Aspose.Cells for Java** versione 25.11 o successiva – il metodo `Range.copy` che supporta le tabelle pivot è stato introdotto in questa versione.  
* Un file **input.xlsx** che contiene già una tabella pivot (puoi crearne una in Excel per i test).  
* Uno strumento di build a tua scelta (Maven, Gradle o semplice `javac`). Mostreremo la dipendenza Maven per una rapida partenza.  

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## Passo 1: Caricare la cartella di lavoro di origine

La prima cosa che facciamo è aprire il file Excel che contiene la tabella pivot originale. Aspose.Cells tratta la cartella di lavoro come un oggetto in memoria, così puoi manipolarla senza avviare Excel.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Perché è importante:** Caricare la cartella di lavoro ci dà accesso ai fogli di lavoro, alle celle e, soprattutto, alla cache pivot che supporta la tabella pivot. Senza questo passaggio la libreria non ha nulla da copiare.

---

## Passo 2: Ottenere il foglio di lavoro che contiene la pivot

Se la tua cartella di lavoro ha più fogli, devi puntare a quello corretto. Qui semplicemente prendiamo il primo foglio, ma puoi anche usare `get("SheetName")` per una ricerca per nome.

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Consiglio professionale:** Quando gestisci molti fogli, memorizza l'indice o il nome in un file di configurazione per evitare di codificare a mano i numeri.

---

## Passo 3: Definire l'intervallo di origine che include la tabella pivot

A partire dalla versione 25.11 Aspose.Cells ti permette di trattare una tabella pivot come un intervallo di celle normale. Specifica le celle in alto‑a‑sinistra e in basso‑a‑destra che racchiudono l'intera pivot.

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **Caso limite:** Se la tua pivot si espande dinamicamente (ad esempio, vengono aggiunte righe in seguito), considera l'uso di `worksheet.getPivotTables().get(0).getDataRange()` per recuperare l'intervallo esatto in modo programmatico.

---

## Passo 4: Definire l'intervallo di destinazione dove la pivot sarà copiata

Scegli una cella vuota dove vuoi che la pivot duplicata appaia. In questa demo iniziamo da **F1**, lasciando uno spazio tra l'originale e la copia.

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **Perché non un nuovo foglio?** Puoi anche creare un nuovo foglio di lavoro (`workbook.getWorksheets().add("Copy")`) e usare le sue celle come destinazione. Lo stesso metodo `copy` funziona tra fogli.

---

## Passo 5: Copiare la tabella pivot nella nuova posizione

Ora avviene la magia. Il metodo `copy` clona la pivot, la sua cache, la formattazione e anche eventuali slicer associati (nella versione più recente).

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **Importante:** L'operazione di copia è *profonda*; non crea un riferimento alla pivot originale. Puoi modificare la nuova pivot in modo indipendente senza influenzare la sorgente.

---

## Passo 6: Salvare la cartella di lavoro con la pivot duplicata

Infine, scrivi la cartella di lavoro modificata su disco. Puoi sovrascrivere l'originale o creare un nuovo file; qui scegliamo quest'ultimo per mantenere intatta la sorgente.

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

Quando apri **output.xlsx** in Excel, vedrai la pivot originale nelle colonne A‑D e una copia perfetta che inizia nella colonna F. Entrambe le pivot possono essere aggiornate separatamente.

---

## Esempio completo funzionante

Mettendo tutto insieme, ecco la classe Java completa che puoi compilare ed eseguire direttamente:

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Risultato atteso:** Aprendo `output.xlsx` si vede la pivot originale (A1:D20) e una pivot identica che inizia a F1. Entrambe le tabelle mantengono i loro filtri, stili e campi calcolati.

---

## Gestione delle variazioni comuni

| Situazione | Cosa modificare |
|------------|-----------------|
| **Pivot multiple** sullo stesso foglio | Itera su `worksheet.getPivotTables()` e copia ciascuna con il proprio intervallo di destinazione. |
| **Intervallo dati dinamico** | Usa `worksheet.getPivotTables().get(0).getDataRange()` per rilevare automaticamente l'area di origine. |
| **Copia in un altro workbook** | Carica una seconda istanza di `Workbook`, crea un foglio di destinazione, quindi chiama `sourceRange.copy(destWorksheet.getCells().createRange("A1"))`. |
| **Preservare i slicer** | A partire da 25.12, i slicer vengono copiati automaticamente quando l'intervallo li include. Verifica in Excel dopo il salvataggio. |

---

## Consigli professionali e insidie

* **Controllo versione:** Il metodo `copy` che supporta le pivot è stato aggiunto in **Aspose.Cells 25.11**. Se usi una versione più vecchia otterrai un'eccezione. Verifica sempre la versione di `aspose-cells` nel tuo `pom.xml`.  
* **Prestazioni:** Copiare pivot di grandi dimensioni può richiedere molta memoria. Se ti servono solo i dati, considera l'esportazione della pivot in una tabella piatta invece di clonare l'intero oggetto.  
* **Comportamento di aggiornamento:** La pivot duplicata conserva la propria cache. Se modifichi i dati sottostanti, chiama `pivotTable.refresh()` sulla nuova pivot per ricalcolare.  
* **Particolarità di formattazione:** Alcuni formati numerici personalizzati potrebbero non sopravvivere alla copia su versioni molto vecchie di Excel (<2007). Testa con la versione di Excel del tuo pubblico di destinazione.  

---

## Conclusione

Ora hai una risposta solida, end‑to‑end, a **come copiare le pivot** usando Aspose.Cells per Java, e hai visto come **duplicare le tabelle pivot di Excel** in poche righe di codice. L'approccio funziona per pivot singole o multiple, tra fogli di lavoro e persino tra cartelle di lavoro.

I prossimi passi potrebbero includere:

* Automatizzare la copia per ogni pivot in un job batch.  
* Aggiungere codice per rinominare la pivot duplicata (ad esempio, `pivotTable.setName("Copy_of_Sales")`).  
* Integrare la routine in un servizio di reporting più ampio che genera PDF o esportazioni CSV.  

Provalo, adatta gli intervalli per corrispondere ai tuoi dati reali, e lascia che la libreria gestisca il lavoro pesante. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come creare tabelle pivot in Excel usando Aspose.Cells per Java&#58; Guida completa](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Manipolazione delle tabelle pivot di Excel con Aspose.Cells Java&#58; Guida completa](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Come aggiornare l'origine della tabella pivot di Excel con Aspose.Cells per Java&#58; Guida completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}