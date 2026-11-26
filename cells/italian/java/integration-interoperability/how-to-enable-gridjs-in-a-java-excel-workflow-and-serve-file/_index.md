---
category: general
date: 2026-11-25
description: come abilitare GridJS in Java rapidamente – caricare un workbook Excel
  in Java, abilitare la modalità collaborativa e salvare Excel per il web in una guida
  unica
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gridjs
- load excel workbook java
- save excel for web
- GridJS collaborative mode
- Aspose.Cells Java example
language: it
lastmod: 2026-11-25
og_description: come abilitare GridJS in Java. Impara a caricare una cartella di lavoro
  Excel in Java, attivare la modalità collaborativa di GridJS e salvare Excel per
  il web con Aspose.Cells.
og_image_alt: Screenshot showing how to enable GridJS while loading an Excel workbook
  Java and saving it for web
og_title: Come abilitare GridJS in Java – caricare e salvare Excel per il web
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: how to enable GridJS in Java quickly – load Excel workbook Java, enable
    collaborative mode, and save Excel for web in a single guide
  headline: How to enable GridJS in a Java Excel workflow and serve files for the
    web
  type: TechArticle
tags:
- GridJS
- Java
- Excel
- Web integration
title: Come abilitare GridJS in un flusso di lavoro Java Excel e servire i file per
  il web
url: /it/java/integration-interoperability/how-to-enable-gridjs-in-a-java-excel-workflow-and-serve-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare GridJS in un flusso di lavoro Java Excel e servire i file per il web

Se hai bisogno di **how to enable GridJS** per un foglio di calcolo che verrà visualizzato in un browser, questa guida ti mostra esattamente come fare. Imparerai a **load Excel workbook Java**, attivare il flag collaborativo di GridJS e **save Excel for web** in un formato che GridJS può consumare immediatamente.

Lavorare con file Excel sul server spesso significa gestire formati di file e librerie lato client. Utilizzando Aspose.Cells per Java eviti conversioni manuali e ottieni una pipeline affidabile e ad alte prestazioni. Dopo aver seguito questi passaggi avrai un file `*.gridjs` pronto per qualsiasi componente JavaScript GridJS.

## Prerequisiti

- Java 17 o versioni successive (il codice si compila anche con JDK 8+)
- Maven o Gradle per gestire le dipendenze
- Aspose.Cells per Java (versione 23.12 o successiva) – aggiungi la coordinata Maven `com.aspose:aspose‑cells:23.12`
- Conoscenze di base della gestione delle eccezioni Java
- Una directory sul server dove risiederanno il workbook di origine (`GridJsDemo.xlsx`) e il file di output

> **Consiglio:** Memorizza il percorso del workbook in un file di configurazione o in una variabile d'ambiente per mantenere il tuo codice portabile tra ambienti.

## Passo 1: Configura il progetto e importa le classi necessarie

Crea un progetto Maven standard (o aggiungi le dipendenze al tuo build esistente). Le seguenti importazioni sono tutto ciò di cui hai bisogno per il flusso di lavoro principale:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import com.aspose.cells.SaveFormat;
import com.aspose.cells.LoadOptions;
import java.io.IOException;
```

## Passo 2: Carica il workbook Excel Java

Caricare il workbook è la prima azione concreta nel nostro processo di **how to enable GridJS**. Il costruttore `Workbook` legge il file in memoria e ne valida automaticamente il formato.

```java
public class GridJsExporter {

    private static final String INPUT_PATH = "YOUR_DIRECTORY/GridJsDemo.xlsx";

    public static Workbook loadWorkbook() throws IOException {
        // Load the workbook from the file system
        Workbook workbook = new Workbook(INPUT_PATH);
        System.out.println("Workbook loaded successfully: " + INPUT_PATH);
        return workbook;
    }
}
```

> **Perché è importante:** Caricare il workbook con Aspose.Cells preserva tutte le formule, gli stili e gli oggetti incorporati, che GridJS renderà successivamente senza perdita.

## Passo 3: Abilita la modalità collaborativa di GridJS

La modalità collaborativa indica ad Aspose.Cells di incorporare metadati aggiuntivi richiesti dalla libreria JavaScript GridJS (come ID delle celle e informazioni di tracciamento delle modifiche). Questo è il nucleo di **how to enable GridJS**.

```java
private static void enableGridJsMode(Workbook workbook) {
    WorkbookSettings settings = workbook.getSettings();
    // Turn on collaborative features for GridJS
    settings.setCollaborativeMode(true);
    System.out.println("GridJS collaborative mode enabled.");
}
```

> **Spiegazione:** `WorkbookSettings.setCollaborativeMode(true)` inietta una struttura JSON leggera nel file esportato. Quando il componente GridJS legge il file, può sincronizzare le modifiche tra più utenti in tempo reale.

## Passo 4: Salva Excel per il web in formato GridJS

Ora convertiamo il workbook in memoria nel formato `GRID_JS`, che è essenzialmente un bundle JSON che la libreria front‑end consuma direttamente. Questo completa la parte **save Excel for web** del tutorial.

```java
private static final String OUTPUT_PATH = "YOUR_DIRECTORY/GridJsReady.xlsx";

private static void saveForWeb(Workbook workbook) throws IOException {
    // Save the workbook in the special GridJS format
    workbook.save(OUTPUT_PATH, SaveFormat.GRID_JS);
    System.out.println("Workbook saved for web at: " + OUTPUT_PATH);
}
```

> **Cosa ottieni:** `GridJsReady.xlsx` non è un file XLSX tradizionale; contiene JSON che il visualizzatore GridJS analizza istantaneamente, eliminando la necessità di conversione lato server al momento della richiesta.

## Passo 5: Assembla l'esempio completo eseguibile

Mettere tutto insieme produce una classe Java autonoma che puoi eseguire dalla riga di comando o integrare in un servizio Spring Boot.

```java
public class GridJsExporter {

    private static final String INPUT_PATH = "YOUR_DIRECTORY/GridJsDemo.xlsx";
    private static final String OUTPUT_PATH = "YOUR_DIRECTORY/GridJsReady.xlsx";

    public static void main(String[] args) {
        try {
            // 1. Load the Excel workbook Java
            Workbook workbook = new Workbook(INPUT_PATH);
            System.out.println("Workbook loaded successfully.");

            // 2. Enable GridJS collaborative mode (how to enable GridJS)
            WorkbookSettings settings = workbook.getSettings();
            settings.setCollaborativeMode(true);
            System.out.println("GridJS collaborative mode enabled.");

            // 3. Save Excel for web in GridJS format
            workbook.save(OUTPUT_PATH, SaveFormat.GRID_JS);
            System.out.println("Workbook saved for web at: " + OUTPUT_PATH);
        } catch (Exception e) {
            System.err.println("Error during GridJS export: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Output previsto

Eseguendo il programma stampa:

```
Workbook loaded successfully.
GridJS collaborative mode enabled.
Workbook saved for web at: YOUR_DIRECTORY/GridJsReady.xlsx
```

Il file `GridJsReady.xlsx` ora risiede nella directory di destinazione e può essere servito direttamente tramite un server di file statici o CDN. Quando è referenziato in un componente GridJS front‑end, la tabella viene renderizzata istantaneamente con pieno supporto di modifica.

## Gestione dei casi limite comuni

| Situazione                               | Gestione consigliata                                                                        |
|------------------------------------------|---------------------------------------------------------------------------------------------|
| **File non trovato**                     | Verifica `INPUT_PATH` e cattura `java.io.FileNotFoundException` per restituire un errore amichevole. |
| **Versione Excel non supportata**        | Utilizza `LoadOptions` per specificare il formato esatto, ad esempio `new LoadOptions(LoadFormat.XLSX)`.   |
| **Workbook di grandi dimensioni ( > 50 MB )** | Abilita la modalità streaming: `workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` |
| **Necessità di preservare macro**        | Salva come `SaveFormat.XLSM` dopo l'esportazione GridJS se hai anche bisogno di un file con macro abilitate.      |

Anticipando questi scenari garantisci che la tua pipeline **save Excel for web** rimanga solida in produzione.

## Riepilogo passo‑per‑passo (riferimento rapido)

| Passo | Azione | Snippet di codice |
|------|--------|--------------|
| 1 | Carica workbook | `Workbook workbook = new Workbook(INPUT_PATH);` |
| 2 | Abilita GridJS | `workbook.getSettings().setCollaborativeMode(true);` |
| 3 | Salva per il web | `workbook.save(OUTPUT_PATH, SaveFormat.GRID_JS);` |

Puoi copiare questa tabella nella tua documentazione o README per un rapido onboarding.

## Prossimi passi e argomenti correlati

- **Integra con Spring MVC** – servi il file `*.gridjs` tramite un endpoint `@GetMapping`.
- **Configurazione GridJS lato client** – esplora le opzioni di paginazione, ordinamento e sincronizzazione in tempo reale.
- **Esporta nuovamente in XLSX** – dopo le modifiche collaborative, usa `workbook.save("final.xlsx", SaveFormat.XLSX);`.
- **Ottimizzazione delle prestazioni** – abilita `MemorySetting` per fogli di calcolo massivi o usa `Workbook.calculateFormula()` per pre‑valutare le formule prima dell'esportazione.

Queste estensioni ti permettono di costruire una soluzione spreadsheet full‑stack che funziona senza problemi dal back‑end Java al front‑end JavaScript.

## Conclusione

Ora sai **how to enable GridJS** in un'applicazione Java, come **load Excel workbook Java**, e come **save Excel for web** usando Aspose.Cells. L'esempio completo e eseguibile dimostra ogni passaggio necessario, spiega il ragionamento dietro ogni chiamata e copre i casi limite che incontrerai nei progetti reali. Distribuisci il `GridJsReady.xlsx` generato su qualsiasi server web, punta il tuo componente GridJS verso di esso e goditi esperienze spreadsheet collaborative e istantanee.

![Diagramma che illustra come abilitare GridJS durante il caricamento di un workbook Excel Java e salvarlo per il web](/assets/images/gridjs-workflow.png){: .align-center width="600" alt="Diagramma che mostra come abilitare GridJS in un flusso di lavoro Java Excel"}

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come creare ed esportare Excel in HTML usando Aspose.Cells Java \| Guida alle operazioni sul workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Come salvare file Excel in vari formati usando Aspose.Cells Java](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)
- [Come caricare e salvare Excel come CSV usando Aspose.Cells per Java&#58; Guida completa](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}