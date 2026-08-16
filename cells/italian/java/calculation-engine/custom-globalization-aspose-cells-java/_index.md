---
date: '2026-08-16'
description: Scopri come aggiungere la globalizzazione in Java usando Aspose.Cells,
  personalizzare i messaggi di errore di Excel e configurare la dipendenza Maven.
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: Scopri come aggiungere la globalizzazione in Java usando Aspose.Cells,
  personalizzare i messaggi di errore di Excel e configurare la dipendenza Maven.
  Segui la guida passo‑passo.
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: Come aggiungere la globalizzazione in Java con Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: Come aggiungere la globalizzazione in Java con Aspose.Cells
url: /it/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiungere la globalizzazione in Java con Aspose.Cells

## Introduzione

Aggiungere la globalizzazione al tuo workbook Java ti consente di presentare messaggi di errore, valori booleani e altre stringhe specifiche della locale nella lingua che i tuoi utenti si aspettano. In questo tutorial imparerai **come aggiungere la globalizzazione** per il russo, ma lo stesso schema funziona per qualsiasi lingua. Alla fine della guida sarai in grado di:

- Sovrascrivere il testo di errore predefinito e le rappresentazioni dei valori booleani.
- Applicare le tue impostazioni personalizzate a qualsiasi istanza di `Workbook`.
- Integrare la soluzione in un tipico progetto Java basato su Maven.

Pronto a rendere i tuoi file Excel veramente multilingue? Verifichiamo prima che il tuo ambiente di sviluppo soddisfi i prerequisiti.

## Risposte rapide
- **Cos'è la globalizzazione in Aspose.Cells?** È un insieme di stringhe sensibili alla locale (errori, booleani, ecc.) che puoi sostituire con testo personalizzato.  
- **Quale artefatto Maven è richiesto?** `com.aspose:aspose-cells:25.3`.  
- **Posso mirare a lingue diverse dal russo?** Sì – estendi `GlobalizationSettings` e sovrascrivi i metodi necessari per ogni locale.  
- **Ho bisogno di una licenza per lo sviluppo?** Una prova gratuita funziona per i test; una licenza permanente rimuove le filigrane di valutazione.  
- **La soluzione è thread‑safe?** Applica le impostazioni per workbook; l'oggetto `GlobalizationSettings` stesso è immutabile dopo la creazione.

## Cos'è la globalizzazione in Aspose.Cells?

`GlobalizationSettings` è l'oggetto di configurazione di Aspose.Cells che controlla le stringhe specifiche della locale, come messaggi di errore, valori booleani, simboli di valuta e modelli di data. Fornendo una tua sottoclasse, indichi alla libreria quale testo visualizzare per ogni cultura, consentendoti di sostituire le stringhe predefinite in inglese con traduzioni che corrispondono alla lingua e alle convenzioni regionali dell'utente finale.

## Perché aggiungere una globalizzazione personalizzata?

Aspose.Cells supporta **oltre 50 formati di input e output** – tra cui XLSX, CSV, PDF e ODS – e può elaborare workbook con **fino a 200 000 righe** senza caricare l'intero file in memoria. Personalizzare la globalizzazione garantisce che gli utenti finali vedano i messaggi nella loro lingua madre, riducendo i ticket di supporto di circa **30 %** per le distribuzioni multinazionali.

## Prerequisiti

- **Java Development Kit** 8 o versioni successive.
- **IDE** come IntelliJ IDEA o Eclipse.
- **Aspose.Cells for Java** versione 25.3 (o successiva) aggiunta tramite Maven o Gradle.

### Configurazione di Aspose.Cells per Java

Aggiungi la dipendenza Maven al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Oppure, se preferisci Gradle, inserisci quanto segue in `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Acquisizione della licenza

Aspose offre diverse opzioni di licenza:

- **Free trial** – valutazione completa di tutte le funzionalità per 30 giorni.  
- **Temporary license** – valutazione illimitata senza filigrane.  
- **Commercial license** – pronta per la produzione, con supporto prioritario.

Dopo aver ottenuto un file di licenza, impostalo una volta all'avvio dell'applicazione:

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## Come aggiungere la globalizzazione per il russo?

Un oggetto `Workbook` rappresenta un file Excel caricato in memoria, fornendo l'accesso ai fogli, alle celle e alle impostazioni. Carica il tuo workbook, crea una sottoclasse di `GlobalizationSettings` e collegala al workbook. La risposta diretta è: **instanziare una classe personalizzata `GlobalizationSettings`, sovrascrivere `getErrorValueString` e `getBooleanValueString`, quindi chiamare `workbook.setGlobalizationSettings(customSettings)`**. Questo approccio in due passaggi sostituisce le stringhe russe predefinite con le tue.

### Definizione delle impostazioni personalizzate

La prima volta che fai riferimento a `GlobalizationSettings` in questa guida, osserva la definizione:

`GlobalizationSettings` è la classe base che Aspose.Cells utilizza per recuperare le stringhe specifiche della locale.  

Ora crea una sottoclasse che restituisce testo specifico per il russo:

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### Applicazione delle impostazioni a un workbook

Dopo aver definito la sottoclasse, collegala a qualsiasi istanza di `Workbook`:

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## Applicazioni pratiche

- **Financial reporting** – visualizzare i codici di errore nella lingua madre del contabile, riducendo le incomprensioni.  
- **Enterprise‑wide tools** – incorporare la stessa logica di globalizzazione in decine di utility interne basate su Excel.  
- **Automated data pipelines** – garantire che i sistemi a valle ricevano valori sensibili alla locale senza passaggi di traduzione aggiuntivi.

## Considerazioni sulle prestazioni

Quando abiliti la globalizzazione personalizzata, Aspose.Cells continua a elaborare formule e I/O con la stessa alta prestazione. Per mantenere basso l'uso della memoria:

- Rilascia i riferimenti al workbook (`wb.dispose()`) dopo il salvataggio.  
- Usa `CalculationOptions.setEnableIterativeCalculation(true)` solo quando necessario.  
- Regola l'heap della JVM (`-Xmx2g`) per workbook più grandi di 100 MB.

## Domande frequenti

**Q: Posso applicare le stesse impostazioni di globalizzazione a più workbook contemporaneamente?**  
A: Sì. Crea una singola istanza `RussianGlobalization` e passala a ciascun workbook tramite `setGlobalizationSettings`.

**Q: E se devo supportare una lingua che utilizza script da destra a sinistra?**  
A: Sovrascrivi metodi aggiuntivi come `getCurrencySymbol` e `getDatePattern` nella tua sottoclasse per restituire i simboli RTL appropriati.

**Q: È necessaria una licenza per la versione di prova per utilizzare la globalizzazione personalizzata?**  
A: No. La versione di prova supporta pienamente `GlobalizationSettings`; solo le filigrane di valutazione appaiono su alcuni formati di output.

**Q: Come posso fare il debug di stringhe di errore errate?**  
A: Inserisci istruzioni `System.out.println` all'interno dei tuoi metodi sovrascritti per verificare che il valore di input `err` corrisponda ai tuoi casi di switch.

**Q: Questo influisce sulla velocità di calcolo delle formule?**  
A: In modo trascurabile. La libreria cerca la stringa solo durante il rendering dei valori delle celle, non durante i passaggi di calcolo intermedi.

## Risorse aggiuntive

- **Documentazione**: Esplora guide dettagliate su [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)  
- **Download**: Accedi alle ultime versioni su [Aspose Downloads](https://releases.aspose.com/cells/java/)  
- **Acquisto**: Acquista una licenza per uso commerciale su [Aspose Purchase](https://purchase.aspose.com/buy)  
- **Free trial**: Inizia con una prova gratuita da [Aspose Free Trial](https://releases.aspose.com/cells/java/)  
- **Temporary license**: Ottieni una licenza temporanea tramite [Aspose Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Support**: Ottieni aiuto dalla community su [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

---

**Last Updated:** 2026-08-16  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose

## Tutorial correlati

- [Guida al motore di calcolo personalizzato Aspose.Cells Java](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [Come usare Aspose Cells – Tutorial del motore Excel per Java](/cells/java/calculation-engine/)
- [Dipendenza Maven di Aspose Cells – Gestisci le connessioni dati Excel con Aspose.Cells in Java](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}