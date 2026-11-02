---
category: general
date: 2026-09-27
description: Crea un intervallo denominato in Excel usando Aspose.Cells, imposta il
  nome della tabella, aggiungi l'intervallo denominato, crea una tabella Excel e rileva
  gli errori di nome duplicato.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create named range
- set table name
- create excel table
- add named range
- detect duplicate name
language: it
lastmod: 2026-09-27
og_description: Crea un intervallo denominato in Excel con Aspose.Cells, quindi imposta
  il nome della tabella, aggiungi l'intervallo denominato, crea una tabella Excel
  e rileva gli errori di nome duplicato.
og_image_alt: Screenshot showing how to create a named range in Excel with Aspose.Cells
og_title: Crea un intervallo denominato e rileva i nomi duplicati in Excel
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create a named range in Excel using Aspose.Cells, set table name, add
    named range, create Excel table, and detect duplicate name errors.
  headline: Create a named range and detect duplicate name in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Crea un intervallo denominato e rileva nomi duplicati in Excel
url: /it/java/range-management/create-a-named-range-and-detect-duplicate-name-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un intervallo denominato e rileva nomi duplicati in Excel

Se devi **creare un intervallo denominato** in una cartella di lavoro Excel e vuoi evitare collisioni di nomi, questa guida ti mostra esattamente come farlo con Aspose.Cells per Java. Imparerai a **aggiungere un intervallo denominato**, **creare una tabella Excel**, **impostare il nome della tabella** e **rilevare errori di nome duplicato** in un unico esempio autonomo.

Lavorare con gli intervalli denominati è una necessità comune quando costruisci strumenti di reporting, fogli di convalida dati o dashboard dinamiche. Alla fine di questo tutorial avrai un programma eseguibile che crea in modo sicuro un intervallo denominato, costruisce una tabella e gestisce elegantemente eventuali eccezioni di conflitto di nome.

## Prerequisiti

- Java 17 o versioni successive installate
- Maven o Gradle per la gestione delle dipendenze
- Aspose.Cells per Java (ultima versione; coordinate Maven `com.aspose:aspose-cells:23.9` al momento della stesura)
- Familiarità di base con i concetti di Excel come fogli di lavoro, intervalli e tabelle

## Passo 1: Crea un intervallo denominato nella cartella di lavoro

Il primo passo è istanziare un oggetto `Workbook` e aggiungere un intervallo denominato che punti a un blocco di celle specifico.

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the default first worksheet (named "Sheet1")
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Define a named range called "MyRange" that covers A1:C5
        // This demonstrates the "add named range" operation.
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");
```

**Perché è importante:**  
Un intervallo denominato funge da riferimento riutilizzabile a cui formule e tabelle possono fare riferimento. Aggiungerlo subito garantisce che i passaggi successivi possano riutilizzare lo stesso identificatore senza codificare manualmente gli indirizzi delle celle.

## Passo 2: Crea una tabella Excel che utilizza l'intervallo denominato

Successivamente, creiamo una tabella strutturata (ListObject) che occupa la stessa area dell'intervallo denominato. Questo illustra il concetto di **creare tabella Excel**.

```java
        // Create an Excel table (ListObject) that spans the same area as the named range.
        // The parameters (0,0,4,2) represent the top‑left cell (A1) and bottom‑right cell (C5).
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);
```

**Perché è importante:**  
Le tabelle forniscono ordinamento, filtro e formattazione integrati. Allineando la tabella con l'intervallo denominato, mantieni coerente il modello dei dati.

## Passo 3: Imposta il nome della tabella e gestisci un possibile conflitto

Ora tentiamo di assegnare alla tabella un nome che corrisponda all'intervallo denominato creato in precedenza. Questo passaggio dimostra **impostare il nome della tabella** e attiva intenzionalmente un conflitto di denominazione.

```java
        try {
            // Attempt to set the table name to "MyRange".
            // Because a named range with the same identifier already exists,
            // Aspose.Cells will throw an exception.
            table.setName("MyRange"); // <-- conflict expected
        } catch (Exception e) {
            // Step 4: Detect duplicate name and respond appropriately
            System.out.println("Name conflict detected: " + e.getMessage());
        }
```

**Perché è importante:**  
Excel non consente a una tabella e a un intervallo denominato di condividere lo stesso identificatore. Rilevare il conflitto in anticipo evita cartelle di lavoro corrotte e semplifica il debug.

## Passo 4: Rileva il nome duplicato e risolvilo

Quando l'eccezione viene catturata, puoi rinominare la tabella o rimuovere l'intervallo denominato in conflitto. Di seguito è riportata una semplice strategia di risoluzione che rinomina la tabella aggiungendo un suffisso.

```java
            // Resolve the conflict by appending a numeric suffix
            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the workbook to verify the result
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**Punti chiave della risoluzione:**

- **rileva nome duplicato** – il blocco `catch` conferma il conflitto.
- Il ciclo verifica la collezione dei nomi della cartella di lavoro per assicurarsi che il nuovo identificatore sia unico.
- Infine, la cartella di lavoro viene salvata così da poterla aprire in Excel e verificare che la tabella abbia un nome distinto mentre l'intervallo denominato originale rimane intatto.

## Esempio completo, eseguibile

Unendo tutti i pezzi, il programma completo è il seguente:

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Add a named range called "MyRange" covering A1:C5
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");

        // Create an Excel table that occupies the same cells
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);

        try {
            // Try to set the table name to the same identifier
            table.setName("MyRange");
        } catch (Exception e) {
            // Detect duplicate name and resolve it
            System.out.println("Name conflict detected: " + e.getMessage());

            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the file for inspection
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**Output previsto quando esegui il programma:**

```
Name conflict detected: A name with the specified identifier already exists.
Table renamed to: MyRange_1
```

Aprendo `NamedRangeDemo.xlsx` in Excel vedrai:

- Un intervallo denominato **MyRange** che fa riferimento alle celle A1:C5.
- Una tabella denominata **MyRange_1** che copre le stesse celle.
- Nessun errore di denominazione quando aggiungi formule che fanno riferimento a `MyRange`.

## Problemi comuni e migliori pratiche

- **Non riutilizzare gli identificatori**: verifica sempre che un nome non esista già prima di assegnarlo a una tabella.  
- **Preferisci controlli espliciti**: `workbook.getNames().get("Name")` restituisce `null` se il nome è libero, il che è più sicuro rispetto a catturare un'eccezione generica.  
- **Mantieni coerenti le convenzioni di denominazione**: usare un prefisso come `tbl_` per le tabelle e `rng_` per gli intervalli riduce la probabilità di collisioni.  
- **Compatibilità di versione**: il codice funziona con Aspose.Cells 23.9 e successive; versioni precedenti potrebbero avere messaggi di eccezione diversi.

## Conclusione

Ora sai come **creare un intervallo denominato**, **aggiungere un intervallo denominato**, **creare una tabella Excel**, **impostare il nome della tabella** e **rilevare conflitti di nome duplicato** usando Aspose.Cells per Java. Gestendo proattivamente le collisioni di denominazione, mantieni le tue cartelle di lavoro pulite e i tuoi script di automazione robusti.

**Passi successivi**

- Esplora ulteriormente l'API **set table name** per applicare opzioni di formattazione.  
- Usa il modello **detect duplicate name** quando generi più tabelle programmaticamente.  
- Combina gli intervalli denominati con formule o convalide dei dati per report dinamici.

Buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Create Style Named Range Excel Aspose Cells Java](/cells/hindi/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [Create Style Named Range Excel Aspose Cells Java](/cells/german/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [Create Style Named Range Excel Aspose Cells Java](/cells/french/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}