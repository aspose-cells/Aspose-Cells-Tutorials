---
category: general
date: 2026-07-14
description: Copia una tabella pivot tra cartelle di lavoro usando Java. Scopri come
  copiare la pivot, copiare l’intervallo Excel e esportare la tabella pivot in pochi
  minuti.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- copy range between workbooks
- export pivot table
language: it
lastmod: 2026-07-14
og_description: Copia rapidamente una tabella pivot in Java. Questa guida mostra come
  copiare la pivot, copiare l’intervallo Excel ed esportare la tabella pivot con Aspose.Cells.
og_image_alt: Diagram illustrating copy pivot table process between two Excel workbooks
og_title: Copia Tabella Pivot tra Cartelle di Lavoro – Tutorial di Automazione Java
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Copy pivot table between workbooks using Java. Learn how to copy pivot,
    copy Excel range, and export pivot table in minutes.
  headline: Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Copia Tabella Pivot tra Cartelle di Lavoro – Guida Java Passo‑passo
url: /it/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copia Tabella Pivot Tra Cartelle di Lavoro – Tutorial Java Completo

Ti è mai capitato di dover **copiare una tabella pivot** da una cartella di lavoro a un'altra e chiederti perché i soliti trucchi di copia‑incolla rompono sempre il layout? Non sei solo. In molti flussi di reporting la pivot vive in un file master, ma i processi a valle richiedono una copia leggera.  

In questa guida vedremo un modo pulito e programmatico per duplicare una pivot—senza alcuna manipolazione manuale. Alla fine saprai **come copiare una pivot**, come **copiare un intervallo Excel** in modo sicuro, e persino come **esportare una tabella pivot** in un nuovo file, il tutto con Aspose.Cells per Java.

## Cosa Costruirai

- Caricare una cartella di lavoro sorgente che contiene già una tabella pivot.  
- Creare (o aprire) una cartella di lavoro di destinazione.  
- Definire l'intervallo esatto che contiene la pivot.  
- Copiare quell'intervallo—includendo la definizione della pivot—nel nuovo workbook.  
- Salvare il risultato in modo che altre app possano aprirlo senza perdere alcun calcolo.

Nessuno strumento esterno, nessun VBA, solo puro codice Java che puoi inserire in qualsiasi progetto Maven o Gradle.

## Prerequisiti

- Java 17 o successivo (il codice funziona su Java 8+, ma le JDK più recenti offrono migliori prestazioni).  
- Aspose.Cells per Java 23.9 o più recente – aggiungi la dipendenza da Maven Central.  
- Due file Excel: `SourceWithPivot.xlsx` (contiene la pivot) e un segnaposto vuoto per la copia.

Se sei nuovo a Aspose.Cells, la libreria astrae i dettagli OOXML di basso livello, permettendoti di trattare i fogli di lavoro come normali oggetti Java.

## Passo 1: Configura il tuo progetto

Per prima cosa, aggiungi l'artifact Maven di Aspose.Cells al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust if you use a different JDK -->
</dependency>
```

Oppure, per Gradle:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

> **Consiglio:** Se stai usando un IDE come IntelliJ, lascia che importi automaticamente la libreria; ti fa risparmiare molto tempo di digitazione.

## Passo 2: Carica la Cartella di Lavoro Sorgente

Abbiamo bisogno di un'istanza `Workbook` che punti al file contenente la pivot. Il costruttore legge l'intero file in memoria, così puoi lavorare offline.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {

        // Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

Perché caricarlo prima? Perché la cache della pivot, l'elenco dei campi e il layout sono tutti memorizzati all'interno del foglio. Caricare la cartella di lavoro in memoria garantisce che copiamo la *definizione* e non solo i valori renderizzati.

## Passo 3: Crea o Apri la Cartella di Lavoro di Destinazione

Hai due opzioni: iniziare con una cartella di lavoro nuova di zecca, o aprire un modello esistente. Qui creeremo una vuota, che è lo scenario più comune quando ti serve una copia pulita.

```java
        // Create an empty destination workbook (or open an existing one)
        Workbook destinationWorkbook = new Workbook(); // blank workbook with a default sheet
```

Se in seguito decidi di copiare in un foglio specifico, sostituisci semplicemente `getWorksheets().get(0)` con l'indice o il nome appropriato.

## Passo 4: Definisci l'Intervallo Esatto Che Contiene la Pivot

Una tabella pivot di solito occupa un blocco rettangolare. L'approccio più sicuro è specificare esplicitamente le celle in alto‑sinistra e in basso‑destra. Nel nostro esempio la pivot si estende da **A1** a **H30**.

```java
        // Define the range in the source sheet that includes the pivot table
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)                     // first worksheet
                                          .getCells()
                                          .createRange("A1:H30");
```

> **Perché non usare `copyRows`?**  
> `copyRows` copia i valori grezzi delle celle ma scarta la cache della pivot sottostante. Copiando l'intero intervallo, Aspose.Cells preserva i metadati della pivot, consentendo alla destinazione di mantenere la piena interattività.

## Passo 5: Copia l'Intervallo (Inclusa la Pivot) nella Destinazione

Ora avviene la magia. Il metodo `copy` clona tutto—valori, formule, formati e l'oggetto pivot stesso—nella posizione di destinazione.

```java
        // Copy the defined range (with the pivot table) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)               // destination sheet
                                            .getCells()
                                            .createRange("A1"));
```

Se devi incollare in una cella diversa, basta cambiare `"A1"` in `"C5"` o qualsiasi altro indirizzo tu desideri. Il metodo regola automaticamente i riferimenti interni così la pivot continua a funzionare.

## Passo 6: Salva la Cartella di Lavoro di Destinazione

Infine, scrivi la nuova cartella di lavoro su disco. Il file risultante può essere aperto in Excel, LibreOffice o qualsiasi altro visualizzatore di fogli di calcolo, e la pivot si comporterà esattamente come nella sorgente.

```java
        // Save the destination workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

### Risultato Atteso

- `CopyPivotResult.xlsx` si apre con una tabella pivot pienamente funzionale identica all'originale.  
- Tutti i slicer, i filtri e i campi calcolati rimangono intatti.  
- Nessuna perdita di dati—i valori vengono calcolati al volo quando aggiorni la pivot.

## Varianti Comuni & Casi Limite

| Situazione | Cosa Modificare |
|------------|-----------------|
| **Copia in una cartella di lavoro esistente** | Carica la cartella di lavoro di destinazione invece di crearne una nuova: `new Workbook("ExistingFile.xlsx")`. |
| **La pivot copre una dimensione sconosciuta** | Usa `Worksheet.getPivotTables().get(0).getPivotTableRange()` per recuperare programmaticamente l'indirizzo esatto. |
| **Preserva le connessioni dati** | Dopo la copia, chiama `destinationWorkbook.getWorksheets().get(0).getPivotTables().get(0).setRefreshOnLoad(true);` per mantenere attive le connessioni dati esterne. |
| **Esporta la tabella pivot come CSV** | Una volta copiata, puoi chiamare `destinationWorkbook.save("PivotExport.csv", SaveFormat.CSV);` – questo appiattisce solo i valori della pivot. |

> **Attenzione:** Quando le cartelle di lavoro sorgente e destinazione usano impostazioni locali diverse, i formati numerici possono cambiare. Imposta esplicitamente il `setLocale` del workbook se hai bisogno di coerenza.

## Esempio Completo (Tutte le Importazioni Incluse)

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load source workbook containing the pivot
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

        // 2️⃣ Create (or open) destination workbook
        Workbook destinationWorkbook = new Workbook(); // blank workbook

        // 3️⃣ Identify the range that encloses the pivot table
        //    If you don't know the range, you can retrieve it via:
        //    PivotTable pt = sourceWorkbook.getWorksheets().get(0).getPivotTables().get(0);
        //    String address = pt.getPivotTableRange().getRefersTo();
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:H30");

        // 4️⃣ Copy the range (pivot included) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)
                                            .getCells()
                                            .createRange("A1"));

        // 5️⃣ Persist the result
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully!");
    }
}
```

Esegui il programma, apri `CopyPivotResult.xlsx` e vedrai la stessa pivot con cui hai iniziato—pronta per ulteriori analisi o distribuzione.

## Riepilogo

Abbiamo appena dimostrato **come copiare una pivot** da una cartella di lavoro a un'altra usando Aspose.Cells per Java. I passaggi hanno coperto il caricamento della sorgente, la definizione dell'esatto **intervallo Excel da copiare**, l'esecuzione della copia e infine **l'esportazione della tabella pivot** in un nuovo file. Gestendo l'intervallo anziché le singole celle, garantiamo che la cache interna della pivot viaggi con esso, mantenendo il report dinamico.

## Cosa Esplorare Dopo

- **Automatizza l'aggiornamento**: Pianifica l'operazione di copia con un job Quartz così i file a valle rimangono aggiornati.  
- **Copia più pivot**: Itera su `sourceWorkbook.getWorksheets().get(0).getPivotTables()` e copia ciascuna in fogli separati.  
- **Applica lo styling**: Usa oggetti `Style` per armonizzare font e colori nel workbook di destinazione.  

Se hai domande su come gestire cartelle di lavoro di grandi dimensioni o preservare fonti dati esterne, lascia un commento qui sotto. Buona programmazione e goditi la libertà dell'automazione programmatica di Excel!

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Manipolazione della Tabella Pivot Excel con Aspose.Cells Java: Guida Completa](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Come Aggiornare la Sorgente della Tabella Pivot Excel con Aspose.Cells per Java: Guida Completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automatizza lo Styling e il Salvataggio della Tabella Pivot Excel con Aspose.Cells per Java: Guida Completa](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}