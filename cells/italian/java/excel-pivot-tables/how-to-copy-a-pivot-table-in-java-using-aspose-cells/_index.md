---
category: general
date: 2026-09-27
description: Copia tabella pivot in Java con Aspose.Cells – una guida passo‑passo
  che mostra come copiare l’intervallo e preservare le definizioni della pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: it
lastmod: 2026-09-27
og_description: Copia la tabella pivot in Java usando Aspose.Cells. Segui questo tutorial
  completo per copiare l’intervallo con Aspose.Cells e mantenere intatte le definizioni
  della tabella pivot.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: Copia una tabella pivot in Java – Guida rapida di Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Come copiare una tabella pivot in Java usando Aspose.Cells
url: /it/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare una tabella pivot in Java usando Aspose.Cells

Se hai bisogno di **copiare una tabella pivot** da una cartella di lavoro a un'altra, questa guida ti mostra esattamente come farlo con Aspose.Cells per Java. La soluzione funziona per qualsiasi pivot che hai creato e preserva la definizione della pivot senza ricreazione manuale.

Imparerai come caricare il file di origine, definire l'intervallo che contiene la pivot, copiare quell'intervallo in una nuova cartella di lavoro e infine salvare il risultato. Il tutorial copre anche le difficoltà più comuni, come preservare le fonti dati e gestire cartelle di lavoro di grandi dimensioni.

## Cosa ti servirà

* Java 17 o successivo (il codice si compila anche con JDK 8+)
* Aspose.Cells per Java 23.9 o più recente – l'ultima versione offre il supporto più affidabile per **copy range aspose cells**
* Un file Excel di origine che contiene una tabella pivot (ad es., `SourceWithPivot.xlsx`)
* Un IDE o uno strumento di build (Maven/Gradle) che possa fare riferimento al JAR di Aspose.Cells

## Passo 1: Carica la cartella di lavoro di origine che contiene la tabella pivot

La prima azione è aprire la cartella di lavoro che contiene la pivot che desideri duplicare. Il caricamento del file crea una rappresentazione in memoria di tutti i fogli, le celle e le cache delle pivot.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Perché è importante:**  
Aspose.Cells legge l'intera cartella di lavoro, incluse le foglie di cache delle pivot nascoste. Se salti questo passaggio, l'operazione successiva di **copy pivot table** perderebbe la fonte dati sottostante.

## Passo 2: Crea una cartella di lavoro di destinazione vuota

Successivamente, istanzia una nuova cartella di lavoro che riceverà la pivot copiata. Partire da una cartella di lavoro pulita evita sovrascritture accidentali.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Suggerimento:** La cartella di lavoro predefinita contiene un foglio vuoto, perfetto per una copia semplice. Se devi copiare in un foglio con nome specifico, rinomina `destWs` con `destWs.setName("TargetSheet")`.

## Passo 3: Definisci l'intervallo di origine che include la tabella pivot

Una tabella pivot occupa un blocco rettangolare di celle. Devi specificare l'intervallo esatto; altrimenti verranno copiate solo i dati grezzi. In questo esempio assumiamo che la pivot occupi **A1:G20**, ma puoi regolare l'indirizzo per adattarlo al tuo file.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Perché funziona:**  
Quando chiami `createRange` sulla collezione `Cells` del foglio, Aspose.Cells include la definizione della pivot, la sua cache e qualsiasi formattazione. Questo è il fulcro di **how to copy pivot table** correttamente.

## Passo 4: Copia l'intervallo definito nel foglio di destinazione

Ora usa il metodo `copy` per duplicare l'intervallo. Il metodo copia tutto ciò che è dentro l'intervallo, inclusa la definizione della pivot, le formule e gli stili.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**Nota importante:**  
Se ti servono solo i dati senza la pivot, potresti usare `srcRange.copyData`. Tuttavia, per una vera **copy pivot table** devi copiare l'intero intervallo come mostrato sopra.

## Passo 5: Salva la cartella di lavoro di destinazione

Infine, scrivi la nuova cartella di lavoro su disco. Il file risultante conterrà una tabella pivot pienamente funzionale identica a quella di origine.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

L'esecuzione del programma produce `CopyPivotResult.xlsx` con lo stesso layout della pivot, filtri e calcoli del file originale.

## Output previsto

Quando apri `CopyPivotResult.xlsx` in Excel:

* La tabella pivot appare in **A1:G20** sul primo foglio.
* Tutti i campi di riga/colonna, i filtri e i campi valore sono intatti.
* Aggiornare la pivot aggiorna la stessa origine dati della cartella di lavoro di origine (se i dati di origine sono incorporati).

## Casi limite e consigli pratici

| Situazione | Come gestirlo |
|-----------|------------------|
| **La pivot si estende su più colonne del previsto** | Usa `srcWs.getPivotTables().get(0).getPivotTableArea()` per ottenere l'indirizzo esatto programmaticamente. |
| **La cartella di lavoro di origine contiene più pivot** | Itera su `srcWs.getPivotTables()` e copia ogni intervallo singolarmente, regolando gli indirizzi di destinazione. |
| **Le cartelle di lavoro grandi causano pressione sulla memoria** | Abilita `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` prima di caricare l'origine. |
| **Hai bisogno di copiare solo la definizione della pivot, non i dati** | Dopo la copia, elimina le righe di dati di origine nella destinazione con `destWs.getCells().deleteRows(startRow, count)`. |
| **Il file di destinazione deve mantenere la formattazione originale** | Imposta `CopyOptions` con `options.setPasteType(PasteType.ALL)` per una copia a piena fedeltà. |

**Consiglio professionale:** Verifica sempre la pivot copiata chiamando programmaticamente `destWs.getPivotTables().get(0).refresh()`. Questo garantisce che la cache sia aggiornata, soprattutto quando i dati di origine risiedono in una connessione esterna.

## Esempio completo eseguibile

Di seguito trovi l'intero programma che puoi copiare‑incollare nel tuo IDE. Sostituisci `YOUR_DIRECTORY` con il percorso reale sul tuo computer.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

L'esecuzione di questo codice **copia la tabella pivot** esattamente come descritto e dimostra il modo più diretto per **copy range aspose cells** preservando la funzionalità della pivot.

## Conclusione

Ora sai come **copiare una tabella pivot** in Java usando Aspose.Cells, dal caricamento della cartella di lavoro di origine al salvataggio del file di destinazione. La guida ha coperto i passaggi essenziali, spiegato perché ogni passaggio è importante e affrontato i casi limite più comuni.

Successivamente, potresti esplorare:

* **come copiare una tabella pivot** tra diversi fogli di lavoro nella stessa cartella
* Usare **copy range aspose cells** per duplicare grafici o formattazione condizionale
* Automatizzare l'aggiornamento della pivot dopo la copia per mantenere i dati aggiornati

Sentiti libero di sperimentare con intervalli più ampi, più pivot o di integrare questa logica in una pipeline più grande di elaborazione Excel. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Copia Tabella Pivot in Java – Preservala, Esporta in PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [Come aggiornare la fonte della tabella pivot di Excel con Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Manipolazione della tabella pivot di Excel con Aspose.Cells Java: Guida completa](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}