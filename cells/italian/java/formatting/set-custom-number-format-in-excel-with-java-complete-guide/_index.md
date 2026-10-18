---
category: general
date: 2026-06-30
description: Imposta un formato numerico personalizzato in Excel usando Java. Scopri
  come creare una cartella di lavoro Excel in Java, ottenere data e ora da una cella,
  calcolare le formule della cartella di lavoro e restituire il valore della data
  e ora.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: it
og_description: Imposta un formato numerico personalizzato in Excel usando Java. Questa
  guida mostra come creare una cartella di lavoro Excel in Java, ottenere data e ora
  da una cella, calcolare le formule della cartella di lavoro e restituire il valore
  della data e ora.
og_title: Imposta Formato Numerico Personalizzato in Excel con Java – Tutorial Completo
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: Imposta formato numerico personalizzato in Excel con Java – Guida completa
url: /it/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Imposta un formato numerico personalizzato in Excel con Java – Guida completa

Ti è mai capitato di **impostare un formato numerico personalizzato** in un foglio Excel mentre lavori in Java? Non sei l’unico. Che tu stia costruendo un motore di reportistica o semplicemente cercando di visualizzare correttamente le date dell’era giapponese, padroneggiare questo trucco ti fa risparmiare ore di post‑processing. In questo tutorial percorreremo un esempio reale che **crea un workbook Excel in Java**, applica un formato specifico per locale, ricalcola le formule e infine **ottiene il DateTime dalla cella** per **stampare il valore datetime**.

Useremo la popolare libreria Aspose.Cells per Java perché gestisce formati numerici e date sensibili alla cultura fin da subito. Alla fine della guida avrai un programma autonomo, eseguibile, che potrai inserire in qualsiasi progetto Maven o Gradle. Niente scorciatoie “vedi la documentazione” — solo codice solido e spiegazioni chiare.

---

## Cosa imparerai

- Come **creare un workbook Excel in Java** programmaticamente.  
- I passaggi esatti per **impostare un formato numerico personalizzato** per le date dell’era giapponese.  
- Perché chiamare **calculate workbook formulas** è essenziale prima di estrarre il valore.  
- Il modo corretto per **ottenere il datetime dalla cella** e **stampare il valore datetime**.  
- Problemi comuni (locale mancante, formule obsolete) e soluzioni rapide.

---

## Prerequisiti

- Java 8 o versione più recente installata sulla tua macchina.  
- Aspose.Cells per Java 23.11 (o qualsiasi versione recente).  
- Un IDE o editor di testo di base — IntelliJ IDEA, Eclipse, VS Code, quello che preferisci.  

Se non hai ancora aggiunto Aspose.Cells al tuo progetto, incolla il seguente snippet Maven nel tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

Gli utenti Gradle possono aggiungere:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

Ora che l’ambiente è pronto, immergiamoci nel codice.

---

## Passo 1: Imposta un formato numerico personalizzato – Panoramica

Prima di scrivere qualsiasi riga di Java, è utile visualizzare ciò che vogliamo ottenere. Immagina una cella Excel che dovrebbe mostrare **“令和2年4月1日”** invece della stringa ISO‑8601 “2020‑04‑01”. Il valore sottostante rimane una vera data (quindi le formule funzionano ancora), ma la *visualizzazione* segue il formato dell’era giapponese. È esattamente ciò che realizza l’operazione **set custom number format**.

Di seguito trovi il file sorgente completo. Sentiti libero di copiarlo e incollarlo in `src/main/java/SetCustomNumberFormatDemo.java`.

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### Perché funziona

- **`setNumberFormat`** indica a Excel come *visualizzare* il valore numerico sottostante. La stringa di formato `[$-ja-JP]ggge年m月d日` è la chiave; `ggg` seleziona il nome dell’era, `e` l’anno all’interno dell’era, seguito da mese e giorno letterali.  
- **`calculateFormula`** costringe Aspose.Cells a interpretare il testo “R02-04-01” come una data basata sul calendario giapponese. Saltare questo passaggio lascia la cella come semplice testo, e `getDateTime()` genererebbe un’eccezione.  
- **`getDateTime`** estrae infine il vero oggetto `java.util.Calendar`, che puoi manipolare, formattare o memorizzare altrove.

---

## Passo 2: Crea un workbook Excel in Java – Analisi più approfondita

Quando **crei un workbook Excel in Java**, non stai solo allocando memoria; stai anche stabilendo stili predefiniti, un foglio di lavoro predefinito e una cultura predefinita (di solito il locale di sistema). Se ti serve un locale predefinito diverso, puoi passare un oggetto `LoadOptions`:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

Per la maggior parte degli scenari il costruttore semplice è sufficiente, ma è utile conoscere l’alternativa — soprattutto quando gestisci più locale nella stessa applicazione.

*Consiglio professionale:* mantieni il workbook in memoria finché non hai finito di formattare. Scrivere su disco dopo ogni modifica comporta un inutile overhead di I/O.

---

## Passo 3: Ottieni il DateTime dalla cella – Gestione del risultato

La riga `java.util.Calendar dt = cellA1.getDateTime();` fa il lavoro pesante. Dietro le quinte Aspose.Cells converte il numero seriale interno (il numero di giorni dal 31‑12‑1899) in un `Calendar`. Questa conversione rispetta il locale del workbook, così ottieni la data gregoriana corretta anche se la visualizzazione usa l’era giapponese.

Se ti serve un `java.time.LocalDate` (la nuova API), converti così:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

Questo soddisfa il requisito **output datetime value** rimanendo aggiornato con le API moderne.

---

## Passo 4: Calcola le formule del workbook – Quando è importante

Ti starai chiedendo: *“Devo davvero chiamare `calculateFormula()`?”* La risposta è un sì deciso, a meno che tu non stia inserendo nella cella un oggetto `Date` nativo Java fin dall’inizio. Quando **imposti un formato numerico personalizzato** su una stringa di testo, Excel (e Aspose.Cells) la trattano come un’espressione tipo formula che necessita di valutazione. Senza ricalcolo, `getDateTime()` restituirà il valore predefinito `1900‑01‑00` o lancerà una `CellValueException`.

Se il tuo workbook contiene già formule complesse che fanno riferimento alla cella appena formattata, chiama `calculateFormula()` *una sola volta* dopo tutte le modifiche. Chiamate ripetute sono costose.

---

## Passo 5: Stampa il valore DateTime – Verifica del risultato

Eseguendo il demo otterrai qualcosa del genere:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

Quella riga conferma tre cose:

1. Il **set custom number format** è stato applicato (puoi aprire il `.xlsx` generato in Excel per vedere “令和2年4月1日”).  
2. Il passo **calculate workbook formulas** è riuscito, trasformando la stringa dell’era in una data reale.  
3. La chiamata **get datetime from cell** ha restituito un `Calendar` corretto, che poi **output datetime value** è stato stampato sulla console.

Se apri il workbook con un programma di fogli di calcolo, vedrai il testo formattato, ma il valore sottostante rimane il numero seriale `43831` (rappresentazione Excel di 2020‑04‑01). Questa dualità è ciò che rende Excel così potente.

---

## Problemi comuni e casi limite

| Problema | Perché accade | Soluzione |
|----------|---------------|-----------|
| `cellA1.getDateTime()` genera `CellValueException` | La cella è ancora una stringa perché `calculateFormula()` è stato omesso. | Invoca sempre `workbook.calculateFormula()` dopo aver impostato una data testuale che necessita di conversione. |
| L’era giapponese non viene visualizzata correttamente | Codice locale mancante o errato. | Usa `[$-ja-JP]` nella stringa di formato, o imposta il locale del workbook tramite `LoadOptions`. |
| Il formato mostra “#VALUE!” in Excel | La stringa di formato è malformata. | Ricontrolla parentesi e caratteri; il pattern `ggge年m月d日` è necessario per l’anno dell’era. |
| Viene mostrata la componente oraria (es. “00:00:00”) | La stringa di origine include l’orario o lo stile della cella lo aggiunge. | Rimuovi l’orario dalla stringa di origine o aggiusta il formato a `ggge年m月d日;@`. |

---

## Esempio completo funzionante – Esecuzione con un click

Se preferisci un unico file senza commenti aggiuntivi, ecco la versione minimale:



## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea un workbook Excel usando Aspose.Cells in Java: Guida passo‑passo](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)  
- [Padroneggiare la presentazione dei dati in Excel: Formattazione numerica e data personalizzata con Aspose.Cells per Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)  
- [Come creare e formattare celle Excel usando Aspose.Cells per Java: Guida passo‑passo](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}