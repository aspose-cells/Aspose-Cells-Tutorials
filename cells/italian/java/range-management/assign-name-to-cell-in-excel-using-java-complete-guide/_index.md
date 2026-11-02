---
category: general
date: 2026-06-18
description: Assegna un nome a una cella in Excel con Java – guida passo passo per
  aggiungere un intervallo denominato in Excel, creare una cella denominata, definire
  un nome per la cella e salvare la cartella di lavoro come XLSX.
draft: false
keywords:
- assign name to cell
- add named range excel
- save workbook as xlsx
- create named cell
- define name for cell
language: it
og_description: Assegna un nome a una cella in Excel con Java. Scopri come aggiungere
  un intervallo denominato in Excel, creare una cella denominata, definire un nome
  per la cella e salvare la cartella di lavoro come XLSX.
og_title: Assegna un nome a una cella in Excel usando Java – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Assign name to cell in Excel with Java – step-by-step guide to add
    named range Excel, create named cell, define name for cell, and save workbook
    as XLSX.
  headline: Assign Name to Cell in Excel Using Java – Complete Guide
  type: TechArticle
- description: Assign name to cell in Excel with Java – step-by-step guide to add
    named range Excel, create named cell, define name for cell, and save workbook
    as XLSX.
  name: Assign Name to Cell in Excel Using Java – Complete Guide
  steps:
  - name: Creates a workbook.
    text: Creates a workbook.
  - name: Assigns three different names (single cell, range, local name).
    text: Assigns three different names (single cell, range, local name).
  - name: Populates a few cells with sample data.
    text: Populates a few cells with sample data.
  - name: Saves the result as `named_cells_demo.xlsx`.
    text: Saves the result as `named_cells_demo.xlsx`.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Assegna un nome a una cella in Excel usando Java – Guida completa
url: /it/java/range-management/assign-name-to-cell-in-excel-using-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Assegna un Nome a una Cella in Excel con Java – Guida Completa

Ti sei mai chiesto come **assign name to cell** in un foglio di lavoro Excel senza aprire l'interfaccia? Non sei solo. Molti sviluppatori hanno bisogno di un modo programmatico per etichettare una singola cella in modo che formule e altro codice possano riferirsi ad essa con un identificatore leggibile. In questo tutorial ti guideremo attraverso una soluzione Java pulita che non solo assegna un nome a una cella, ma ti mostra anche come **add named range Excel**, **create named cell**, e infine **save workbook as XLSX**.

Immagina di costruire un motore di reporting che estrae i totali delle vendite da *Sheet1!A1* ogni notte. Codificare l'indirizzo in modo statico è fragile; una cella nominata rende la logica resiliente a futuri cambiamenti di layout. Alla fine di questa guida avrai uno snippet riutilizzabile da inserire in qualsiasi progetto Java che utilizza Aspose.Cells.

## Prerequisiti

- Java 17 (o qualsiasi JDK recente) installato.
- Libreria Aspose.Cells for Java (versione 23.9 o successiva) aggiunta al classpath del tuo progetto.
- Una comprensione di base della sintassi Java—non è richiesto nulla di complesso.

Se ti manca la libreria, scaricala da Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Ora, mettiamoci al lavoro.

![Assign name to cell diagram](assign-name-cell.png)

## Assegna un Nome a una Cella con Aspose.Cells (Java)

Il nucleo dell'operazione è costituito da sole tre righe, ma ognuna svolge un ruolo cruciale. Di seguito trovi l'esempio completo e eseguibile che crea un nuovo workbook, assegna un nome alla cella **A1**, e salva il file come **output.xlsx**.

```java
import com.aspose.cells.*;

public class AssignNameToCellDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // empty workbook
        Worksheet ws = workbook.getWorksheets().get(0);   // first (default) sheet

        // Step 2: Define a name that points to cell A1 on Sheet1
        // This is the “assign name to cell” operation.
        // If a name called "Sales" already exists, an exception will be thrown.
        ws.getNames().add("Sales", "=Sheet1!$A$1");

        // Optional: put a value in the cell so you can see it later
        ws.getCells().get("A1").putValue(12345);

        // Step 3: Save the workbook as an XLSX file
        workbook.save("output.xlsx", SaveFormat.XLSX);
    }
}
```

### Perché funziona

- **Workbook & Worksheet** – `Workbook` è il contenitore di tutti i fogli. Per impostazione predefinita crea *Sheet1*, motivo per cui la formula `=Sheet1!$A$1` funziona immediatamente.
- **Names collection** – `ws.getNames()` restituisce la collezione di nomi definiti limitati al foglio di lavoro. Chiamare `add` crea sia il nome **Sales** sia lo associa al riferimento assoluto `A1`. Questa è l'essenza di **define name for cell**.
- **Save format** – Passare `SaveFormat.XLSX` indica ad Aspose.Cells di scrivere un file Office Open XML moderno, soddisfacendo il requisito **save workbook as xlsx**.

Se esegui il programma, vedrai `output.xlsx` nella tua directory di lavoro. Aprilo in Excel, vai su *Formule → Gestione Nomi*, e troverai **Sales** che punta a *Sheet1!$A$1*. Semplice, vero?

## Aggiungi Intervallo Nominato Excel – Oltre una Singola Cella

Un intervallo nominato non è limitato a un singolo indirizzo. Supponiamo che in seguito tu debba fare riferimento a un blocco di dati (ad esempio *B2:C10*). La stessa chiamata API funziona; devi solo modificare la stringa della formula:

```java
ws.getNames().add("QuarterlyData", "=Sheet1!$B$2:$C$10");
```

Quella riga **adds named range Excel** per un blocco multi‑cella, dimostrando la flessibilità del metodo `add`. Puoi anche limitare il nome all'intero workbook invece che a un singolo foglio usando `workbook.getWorksheets().getNames()`.

## Salva Workbook come XLSX – E la Compatibilità?

Mentre l'esempio utilizza `SaveFormat.XLSX`, Aspose.Cells supporta molti formati: `XLS`, `CSV`, `ODS`, `PDF` e altri. Scegliere XLSX garantisce la massima compatibilità con le versioni moderne di Office e servizi cloud come OneDrive. Se devi forzare una versione specifica di Excel, puoi anche impostare `WorkbookSettings`:

```java
workbook.getSettings().setExcelVersion(ExcelVersion.EXCEL_2016);
```

Questa piccola modifica garantisce che il file si apra senza avvisi nelle versioni più vecchie di Excel.

## Crea Cella Nominata – Problemi Comuni

Quando **create named cell** programmaticamente, fai attenzione a questi inconvenienti:

| Problema | Perché è importante | Soluzione |
|----------|---------------------|-----------|
| Nome duplicato | Aspose.Cells genera `ArgumentException` se l'identificatore esiste già. | Controlla `ws.getNames().contains("MyName")` prima di aggiungere, oppure avvolgi in un try/catch e rinomina. |
| Riferimento foglio errato | Usare `Sheet2` nella formula mentre la cella si trova su `Sheet1` porta a errori #REF!. | Costruisci la formula dinamicamente: `String formula = "=Sheet1!$" + column + "$" + row;` |
| Problemi di locale | Alcuni locali usano le virgole invece dei punti e virgola nelle formule. | Usa lo stile universale A1 (`=Sheet1!$A$1`) che Aspose.Cells normalizza. |

Prevedendo questi, la tua logica di **assign name to cell** diventa a prova di errore.

## Definisci Nome per Cella – Consigli Avanzati

Se hai bisogno che il nome sia *locale* a un foglio (visibile solo quando quel foglio è attivo), usa la collezione `Names` a livello di workbook e imposta esplicitamente lo scope:

```java
Name localName = workbook.getWorksheets().getNames().add("LocalTotal");
localName.setRefersToFormula("=Sheet1!$A$1");
localName.setScope(ws); // limits visibility to Sheet1
```

Questo approccio è utile quando hai molti fogli, ognuno con la propria cella “Total”—nessuna collisione di nomi, e ogni foglio può riferirsi al proprio **define name for cell** senza ambiguità.

## Esempio Completo End‑to‑End

Mettendo tutto insieme, ecco un programma autonomo che:

1. Crea un workbook.
2. Assegna tre nomi diversi (cella singola, intervallo, nome locale).
3. Popola alcune celle con dati di esempio.
4. Salva il risultato come `named_cells_demo.xlsx`.

```java
import com.aspose.cells.*;

public class NamedCellDemo {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook();
        Worksheet ws = wb.getWorksheets().get(0);
        Cells cells = ws.getCells();

        // Populate sample data
        cells.get("A1").putValue(5000);          // Sales total
        cells.get("B2").putValue(120);
        cells.get("C2").putValue(130);
        cells.get("B3").putValue(140);
        cells.get("C3").putValue(150);

        // 1️⃣ Assign name to a single cell (Sales)
        ws.getNames().add("Sales", "=Sheet1!$A$1");

        // 2️⃣ Add named range for a block of data (QuarterlyData)
        ws.getNames().add("QuarterlyData", "=Sheet1!$B$2:$C$3");

        // 3️⃣ Define a local name visible only on Sheet1 (LocalTotal)
        Name local = wb.getWorksheets().getNames().add("LocalTotal");
        local.setRefersToFormula("=Sheet1!$A$1");
        local.setScope(ws);

        // Save the workbook
        wb.save("named_cells_demo.xlsx", SaveFormat.XLSX);
    }
}
```

**Risultato atteso:** Apri `named_cells_demo.xlsx` → *Formule → Gestione Nomi* → vedrai tre voci: **Sales**, **QuarterlyData** e **LocalTotal**. Selezionando ciascuna verranno evidenziate le celle di riferimento sul foglio.

## Consigli Pro & Casi Limite

- **Consiglio di performance:** Se aggiungi decine di nomi in un ciclo, disabilita l'aggiornamento dello schermo: `wb.getSettings().setScreenUpdating(false);` e riabilitalo dopo il batch.
- **Sicurezza dei thread:** Gli oggetti Aspose.Cells **non** sono thread‑safe. Crea un'istanza `Workbook` separata per ogni thread.
- **Riferimenti cross‑workbook:** Per puntare un nome a un altro workbook, usa la sintassi di riferimento esterno: `=‘[OtherBook.xlsx]Sheet1’!$A$1`. Questo funziona quando entrambi i file sono salvati nella stessa cartella.
- **Nomi Unicode:** Puoi usare caratteri non ASCII (ad esempio “销售额”) purché la versione di Excel sottostante li supporti. Testa con un rapido apertura in Excel per confermare.

## Conclusione

In questa guida abbiamo

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come Convertire i Nomi delle Celle Excel in Indici Usando Aspose.Cells per Java: Guida Passo‑Passo](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [Padroneggia la Manipolazione delle Celle del Workbook con Aspose.Cells in Java: Guida Completa all'Automazione di Excel](/cells/english/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Iterazione di Workbook e Celle Excel con Aspose.Cells Java: Guida per Sviluppatori](/cells/english/java/workbook-operations/excel-operations-aspose-cells-java-workbook-cell-iteration/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}