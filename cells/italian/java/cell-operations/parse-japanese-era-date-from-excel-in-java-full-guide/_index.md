---
category: general
date: 2026-10-07
description: Leggi la data da Excel in Java con Aspose.Cells. Questa guida mostra
  come analizzare le date dell'era giapponese, leggere la data dalle celle di Excel
  e estrarre datetime dalle celle di Excel rapidamente.
draft: false
keywords:
- read date from excel
- extract datetime from excel
- java excel date conversion
- japanese era date parsing
- aspose.cells java
lastmod: 2026-10-07
og_description: Leggi la data da Excel in Java con Aspose.Cells. Questa guida mostra
  come analizzare le date dell'era giapponese, leggere la data dalle celle di Excel
  e estrarre datetime dalle celle di Excel in pochi passaggi.
og_image_alt: 'Developer guide: Read date from Excel in Java using Aspose.Cells'
og_title: Leggi la data da Excel in Java con Aspose.Cells – guida completa
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  headline: Read date from Excel in Java with Aspose.Cells – full guide
  type: TechArticle
- description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  name: Read date from Excel in Java with Aspose.Cells – full guide
  steps:
  - name: Multiple Eras
    text: Japan has had several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). The `setParseDateUsingJapaneseEra(true)`
      flag covers all of them automatically, but be aware that older dates may fall
      outside the library’s supported range (typically 1868‑present). If you encounter
      a date like “昭和45年12月31日”, the sam
  - name: Blank or Invalid Cells
    text: 'If a cell is empty or contains a malformed string, `cell.getDateTime()`
      throws a `CellsException`. Guard against this with a simple check:'
  - name: Time Component
    text: The example only includes a date, but if your Excel file also stores time
      (e.g., “令和3年5月10日 14:30”), Aspose.Cells will preserve the time portion. The
      `LocalDateTime` you receive will include hours, minutes, and seconds.
  type: HowTo
tags:
- Java
- Excel
- DateTime
- read date from excel
- java excel date conversion
title: Leggi la data da Excel in Java con Aspose.Cells – guida completa
url: /it/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Leggi data da Excel in Java con Aspose.Cells – guida completa

Se hai bisogno di **leggere data da Excel** fogli di lavoro che contengono stringhe di era giapponese, sei nel posto giusto. In molti fogli di calcolo legacy di contabilità o governativi la data è memorizzata come “令和3年5月10日”, e convertirla in un `LocalDateTime` gregoriano standard può essere soggetto a errori. Questo tutorial ti mostra, passo dopo passo, come abilitare il parsing sensibile all'era, leggere il valore della cella e **estrarre data e ora da Excel** usando Aspose.Cells per Java.

## Risposte rapide
- **Quale libreria gestisce le date dell'era giapponese?** Aspose.Cells for Java.
- **Quale versione di Java è richiesta?** Java 17 o più recente (Java 8 funziona comunque).
- **È necessaria una licenza per i test?** Una prova gratuita è sufficiente per lo sviluppo.
- **Il medesimo codice può leggere date gregoriane?** Sì, l'API rileva automaticamente il formato.
- **Le informazioni sull'ora vengono preservate?** Assolutamente – ore, minuti e secondi sopravvivono alla conversione.

## Che cosa significa leggere data da Excel?
La frase “leggere data da Excel” si riferisce al recuperare il valore di data di una cella e convertirlo in un oggetto data‑ora Java come `java.time.LocalDateTime`. Aspose.Cells astrae il formato binario di Excel a basso livello, così puoi lavorare con le date senza dover analizzare manualmente le stringhe.

## Perché usare Aspose.Cells per il parsing dell'era giapponese?
Aspose.Cells supporta **oltre 50 formati di input e output** e può elaborare cartelle di lavoro di centinaia di pagine senza caricare l'intero file in memoria. Il suo parser integrato sensibile all'era converte ogni era giapponese (Meiji, Taishō, Shōwa, Heisei, Reiwa) in date gregoriane con una singola chiamata API, eliminando il codice fragile basato su espressioni regolari.

## Prerequisiti
- Java 17 (o Java 8+) installato sulla tua macchina.
- Sistema di build Maven o Gradle.
- Familiarità di base con i file Excel.
- Libreria Aspose.Cells per Java (versione di prova o con licenza).

Se qualcuno di questi ti è sconosciuto, non preoccuparti—vedrai esattamente come aggiungere la libreria nel passo successivo.

## Come leggere data da Excel in Java?

Carica la tua cartella di lavoro, abilita il parsing sensibile all'era e richiedi alla cella il suo valore `DateTime`. L'intero processo richiede **due righe di codice funzionale** una volta che la libreria è nel classpath.

### Passo 1: aggiungi Aspose.Cells al tuo progetto

**Maven**:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for latest version -->
</dependency>
```

**Gradle**:

```groovy
implementation 'com.aspose:aspose-cells:24.9'
```

Dopo che la dipendenza è risolta, puoi iniziare a usare l'API per **leggere data da Excel** nelle celle.

### Passo 2: crea una cartella di lavoro e seleziona il primo foglio

La classe `Workbook` rappresenta un intero file Excel in memoria. Creare una nuova istanza garantisce un ambiente pulito per i successivi passaggi di parsing.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

### Passo 3: inserisci una stringa di data dell'era giapponese nella cella A1

Per dimostrazione scriviamo noi stessi la stringa dell'era; in produzione caricheresti un `.xlsx` esistente.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

Il testo segue il consueto schema giapponese: *Era* + *Anno* + *Mese* + *Giorno*.

### Passo 4: abilita il parsing sensibile all'era

Indica ad Aspose.Cells di trattare le stringhe dell'era come date impostando il flag `ParseDateUsingJapaneseEra`.  
`ParseDateUsingJapaneseEra` è una proprietà che, quando vera, abilita la conversione automatica delle stringhe dell'era giapponese in date gregoriane.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Senza questo flag la libreria tratterebbe “令和3年5月10日” come semplice testo, e perderesti la conversione automatica.

### Passo 5: recupera il valore DateTime analizzato

Ora richiedi alla cella la sua rappresentazione di data. `cell.getDateTime()` restituisce il valore della cella come oggetto `java.util.Date`. Il metodo restituisce un `java.util.Date`, che convertiamo immediatamente nel moderno `java.time.LocalDateTime`. `LocalDateTime` è una classe Java che rappresenta data e ora senza fuso orario.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Questo soddisfa il requisito di **estrarre data e ora da Excel** in modo tipizzato.

### Passo 6: verifica il risultato

Stampa la data gregoriana per confermare che la conversione è riuscita.

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

Quando esegui il programma dovresti vedere:

```
2021-05-10T00:00
```

L'output dimostra che abbiamo letto con successo **data da Excel**, analizzato l'era giapponese e **estratto data e ora da Excel** in un unico flusso.

## Gestione dei casi limite reali

### Multiple ere

Il Giappone ha avuto diverse ere (Meiji, Taishō, Shōwa, Heisei, Reiwa). Il flag `setParseDateUsingJapaneseEra(true)` le copre tutte automaticamente, ma tieni presente che le date più vecchie potrebbero trovarsi al di fuori dell'intervallo supportato dalla libreria (tipicamente 1868‑presente). Se incontri una data come “昭和45年12月31日”, lo stesso codice la convertirà in 1970‑12‑31.

### Celle vuote o non valide

Se una cella è vuota o contiene una stringa malformata, `cell.getDateTime()` lancia una `CellsException`. Proteggiti da questo con un semplice controllo:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Componente ora

L'esempio include solo una data, ma se il tuo file Excel memorizza anche l'ora (ad esempio “令和3年5月10日 14:30”), Aspose.Cells preserverà la parte dell'ora. Il `LocalDateTime` che ricevi includerà ore, minuti e secondi.

## Esempio completo funzionante

Mettendo tutto insieme, ecco il programma completo, pronto per il copia‑incolla:

```java
import com.aspose.cells.*;
import java.time.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Insert Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日");

        // Enable era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);

        // Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime();
        LocalDateTime dateTime = javaDate.toInstant()
                                         .atZone(ZoneId.systemDefault())
                                         .toLocalDateTime();

        // Output the Gregorian date
        System.out.println(dateTime); // 2021-05-10T00:00
    }
}
```

Salva questo come `JapaneseEraDateParser.java`, compila con `javac` e esegui con `java`. Se tutto è configurato correttamente, vedrai la data gregoriana stampata sulla console.

## Consigli professionali e ostacoli comuni

- **Consiglio:** Abilita `setParseDateUsingJapaneseEra(true)` **prima** di leggere qualsiasi valore di cella. Modificare il flag in seguito non convertirà retroattivamente le celle già lette.
- **Nota sulla locale:** Il parser funziona sui caratteri Unicode stessi, quindi non è necessario impostare esplicitamente una locale giapponese.
- **Prestazioni:** Il parsing dell'era aggiunge un overhead trascurabile. Se ne hai bisogno solo per poche celle, attiva il flag solo per quelle letture.
- **Test:** Usa la prova gratuita di Aspose per convalidare con una cartella di lavoro reale che mescola date gregoriane e di era. Questo garantisce che il codice di produzione si comporti come previsto.

## Domande frequenti

**D: Posso usare questo approccio con un file .xlsx esistente?**  
R: Sì. Carica il file con `new Workbook("path/to/file.xlsx")` e lo stesso flag analizzerà qualsiasi stringa di era che trovi.

**D: Cosa succede se la cella contiene una data gregoriana?**  
R: La libreria restituisce il valore gregoriano invariato; il parsing dell'era influisce solo sulle stringhe che corrispondono al modello dell'era.

**D: Aspose.Cells supporta date precedenti a Meiji (1868)?**  
R: No. Le date precedenti al 1868 sono al di fuori dell'intervallo supportato e saranno trattate come semplice testo.

**D: Come gestire cartelle di lavoro grandi senza esaurire la memoria?**  
R: Usa il costruttore `Workbook` che accetta `LoadOptions` con `setMemorySetting(MemorySetting.MemoryPreference)` per trasmettere i dati in streaming invece di caricare tutto in una volta.

**D: È necessaria una licenza commerciale per l'uso in produzione?**  
R: Sì, una licenza valida di Aspose.Cells rimuove le limitazioni di valutazione e abilita le prestazioni complete.

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑a‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Padroneggia il sistema di data 1904 in Excel usando Aspose.Cells Java per operazioni di cella efficaci](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Converti efficientemente Excel in PDF con formati di data personalizzati usando Aspose.Cells per Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Come selezionare intervalli di celle in Excel usando Aspose.Cells per Java (Guida 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

---

**Ultimo aggiornamento:** 2026-10-07  
**Testato con:** Aspose.Cells 24.12 per Java  
**Autore:** Aspose

## Tutorial correlati

- [Analizza data dell'era giapponese da Excel in Java Guida completa](/cells/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/)
- [Leggi file Excel Java con Aspose.Cells – Guida completa](/cells/java/automation-batch-processing/aspose-cells-java-excel-manipulation/)
- [Salva cartella di lavoro Excel con Aspose.Cells per Java – Guida completa](/cells/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}