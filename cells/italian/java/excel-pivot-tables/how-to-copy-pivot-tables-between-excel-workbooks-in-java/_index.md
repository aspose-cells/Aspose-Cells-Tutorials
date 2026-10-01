---
category: general
date: 2026-10-01
description: Scopri come copiare le tabelle pivot tra cartelle di lavoro Excel usando
  Java. Questa guida passo passo mostra anche come copiare intervalli tra cartelle
  di lavoro e duplicare gli intervalli Excel in modo sicuro.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range between workbooks
- how to copy excel
- duplicate excel range
- copy range to workbook
language: it
lastmod: 2026-10-01
og_description: Come copiare le tabelle pivot tra cartelle di lavoro Excel usando
  Java. Segui questa guida per copiare l’intervallo nella cartella di lavoro, duplicare
  gli intervalli Excel e preservare i dati pivot.
og_image_alt: Screenshot of Java code that copies a pivot table from one Excel workbook
  to another
og_title: Come copiare le tabelle pivot tra cartelle di lavoro Excel in Java – guida
  completa
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  headline: How to copy pivot tables between Excel workbooks in Java
  type: TechArticle
- description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  name: How to copy pivot tables between Excel workbooks in Java
  steps:
  - name: Expected output
    text: '* Console: `Pivot table copied successfully.` * `destination.xlsx` opens
      in Excel with a pivot table identical to the one in `source.xlsx`. Refreshing
      the pivot shows the same data source, proving that **how to copy pivot** works
      as intended.'
  - name: Copying multiple worksheets
    text: If your project requires copying several sheets, loop through the workbook’s
      worksheets and repeat steps 2‑4 for each sheet. The pivot in each sheet will
      be preserved independently.
  - name: Preserving external data connections
    text: Pivot tables that rely on external data sources keep the connection string
      after copying. However, the destination file must have access to the same data
      source. Verify the connection by opening the pivot and checking the **Data**
      tab.
  - name: Dealing with merged cells
    text: If the source range contains merged cells, Aspose.Cells copies the merge
      layout automatically. Still, validate the result if the destination workbook
      uses a different default column width.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Pivot table
- Data manipulation
title: Come copiare le tabelle pivot tra cartelle di lavoro Excel in Java
url: /it/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare tabelle pivot tra cartelle di lavoro Excel in Java

Se hai bisogno di **how to copy pivot** tabelle da un file Excel a un altro, questa guida ti fornisce una soluzione pronta all'uso. Alla fine delle prime due frasi saprai esattamente quali chiamate API preservano la definizione della pivot durante la copia dell'intervallo di dati.

Imparerai anche come **copy range between workbooks**, **duplicate Excel range** oggetti, e in modo sicuro **copy range to workbook** senza perdere formule o formattazione. Non sono necessari script esterni—basta un singolo progetto Java che utilizza Aspose.Cells for Java.

## Prerequisiti

* Java Development Kit 17 o successivo.
* Maven o Gradle per gestire le dipendenze.
* Una licenza valida di Aspose.Cells for Java (la valutazione gratuita funziona per i test).
* Due file Excel: `source.xlsx` (contiene la tabella pivot) e un `destination.xlsx` vuoto (oppure lascia che il codice lo crei).

## Passo 1: Configurare il progetto Maven

Crea un `pom.xml` che includa Aspose.Cells. Questa dipendenza ti fornisce le classi `Workbook`, `Worksheet` e `Range` utilizzate nell'esempio.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>excel-pivot-copy</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest at time of writing -->
        </dependency>
    </dependencies>
</project>
```

> **Consiglio:** Mantieni la versione di Aspose.Cells aggiornata; le versioni più recenti aggiungono un migliore supporto per strutture di cache pivot complesse.

## Passo 2: Caricare la cartella di lavoro sorgente che contiene la tabella pivot

Il primo blocco di codice dimostra **how to copy excel** dati caricando il file sorgente. Il costruttore `Workbook` legge l'intero file in memoria, preservando tutti gli oggetti foglio, incluse le pivot.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Access the first worksheet (index 0) where the pivot resides
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Perché è importante:* Aspose.Cells memorizza le tabelle pivot come parte del modello interno del foglio di lavoro. Caricare la cartella di lavoro garantisce che la cache della pivot sia disponibile per la successiva copia.

## Passo 3: Definire l'intervallo che include la tabella pivot

Una tabella pivot può estendersi su più righe e colonne. Nella maggior parte dei casi è possibile copiare l'intero intervallo utilizzato del foglio. Il metodo `createRange` crea un oggetto `Range` che l'operazione di copia gestirà.

```java
        // Define the range to copy – includes the pivot table and its source data
        // Adjust the address if your pivot occupies a different block
        Range srcRange = srcWs.getCells().createRange("A1:H20");
```

Se la pivot si estende oltre `H20`, basta modificare la stringa dell'indirizzo. Questo passo è il fulcro della gestione di **duplicate excel range**; l'oggetto range conosce formule, stili e righe nascoste.

## Passo 4: Creare una nuova cartella di lavoro che riceverà l'intervallo copiato

Puoi iniziare con una cartella di lavoro vuota o caricare un file di destinazione esistente. Qui creiamo una nuova cartella di lavoro, che è il modo più pulito per **copy range to workbook**.

```java
        // Create a new workbook for the destination
        Workbook destWb = new Workbook(); // starts with one default sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

> **Nota:** Se devi copiare la pivot in un nome di foglio specifico, rinomina `destWs` con `destWs.setName("Report")` prima di incollare.

## Passo 5: Copiare l'intervallo – Aspose.Cells preserva automaticamente la pivot

Il metodo `copy` trasferisce tutto all'interno dell'intervallo sorgente, inclusa la definizione della pivot, la cache e la formattazione. Non è necessario alcun codice aggiuntivo per mantenere la pivot funzionante.

```java
        // Copy the range to the destination worksheet; pivot tables are preserved automatically
        srcRange.copy(destWs.getCells().createRange("A1"));
```

*Perché funziona:* Aspose.Cells tratta la pivot come una collezione di celle nascoste e metadati associati all'intervallo. Quando chiami `copy`, la libreria replica quei metadati nella cartella di lavoro di destinazione.

## Passo 6: Salvare la cartella di lavoro di destinazione

Infine, scrivi il risultato su disco. Il file salvato contiene una tabella pivot identica che puoi aggiornare o modificare proprio come l'originale.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");

        System.out.println("Pivot table copied successfully.");
    }
}
```

Eseguendo il programma stampa una conferma e genera `destination.xlsx` con una pivot pienamente funzionale.

## Esempio completo, eseguibile

Unendo tutti i passaggi, la classe Java completa appare così:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load source workbook with pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot and its source data
        Range srcRange = srcWs.getCells().createRange("A1:H20");

        // 3️⃣ Prepare destination workbook (blank by default)
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // 4️⃣ Copy range – pivot table is kept intact
        srcRange.copy(destWs.getCells().createRange("A1"));

        // 5️⃣ Save the new file
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

### Output previsto

* Console: `Pivot table copied successfully.`
* `destination.xlsx` si apre in Excel con una tabella pivot identica a quella in `source.xlsx`. Aggiornare la pivot mostra la stessa origine dati, dimostrando che **how to copy pivot** funziona come previsto.

## Gestire variazioni comuni

### Copiare più fogli di lavoro

Se il tuo progetto richiede la copia di diversi fogli, itera attraverso i fogli della cartella di lavoro e ripeti i passi 2‑4 per ciascun foglio. La pivot in ogni foglio sarà preservata in modo indipendente.

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet src = srcWb.getWorksheets().get(i);
    Worksheet dest = destWb.getWorksheets().add();
    src.getCells().copy(dest.getCells());
}
```

### Conservare le connessioni dati esterne

Le tabelle pivot che si basano su fonti dati esterne mantengono la stringa di connessione dopo la copia. Tuttavia, il file di destinazione deve avere accesso alla stessa fonte dati. Verifica la connessione aprendo la pivot e controllando la scheda **Data**.

### Gestire celle unite

Se l'intervallo sorgente contiene celle unite, Aspose.Cells copia automaticamente il layout di unione. Tuttavia, valida il risultato se la cartella di lavoro di destinazione utilizza una larghezza di colonna predefinita diversa.

## Best practice per una copia affidabile

| Pratica | Motivo |
|----------|--------|
| Usa l'intervallo effettivamente usato (`srcWs.getCells().getMaxDisplayRange()`) invece di un indirizzo hard‑coded | Garantisce che l'intera pivot e i suoi dati di origine siano inclusi. |
| Applica una licenza prima di operazioni pesanti | Previene la filigrana di valutazione e migliora le prestazioni. |
| Aggiorna la pivot dopo la copia (`pivotTable.refresh()`) se i dati di origine sono cambiati | Assicura che la destinazione rifletta i valori più recenti. |
| Scrivi test unitari che aprano la cartella di lavoro di destinazione e verifichino che `pivotTable.getPivotFields().size()` corrisponda a quello della sorgente | Rileva la perdita accidentale di campi durante future modifiche al codice. |

## Conclusione

Ora sai **how to copy pivot** tabelle tra cartelle di lavoro Excel in Java, così come **copy range between workbooks**, **duplicate excel range**, e **copy range to workbook** preservando tutta la formattazione e le formule. L'esempio utilizza Aspose.Cells, che astrae la gestione XML a basso livello richiesta dall'OpenXML SDK.

Successivamente, esplora argomenti correlati come **updating pivot cache programmatically**, **exporting pivot data to CSV**, o **creating pivot tables from scratch**. Ognuno di questi si basa sugli stessi concetti mostrati qui.

Buon coding, e sentiti libero di sperimentare con intervalli più grandi, più pivot o stili personalizzati – lo stesso schema si applica a tutti gli scenari.

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come creare tabelle pivot in Excel usando Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Come copiare più colonne in Excel usando Aspose.Cells Java: Guida completa](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Copiare immagini tra fogli in Excel usando Aspose.Cells per Java: Guida completa](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}