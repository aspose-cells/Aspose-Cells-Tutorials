---
category: general
date: 2026-06-21
description: Crea un array dinamico usando Python e la funzione SEQUENCE in Excel.
  Impara a leggere il risultato della formula, a ricalcolare le formule di Excel e
  a vedere un esempio di SEQUENCE in Excel.
draft: false
keywords:
- create dynamic array
- sequence function excel
- read formula result
- recalculate excel formulas
- excel sequence example
language: it
og_description: Crea un array dinamico in Excel usando Python. Questo tutorial mostra
  come utilizzare la funzione SEQUENCE, ricalcolare le formule di Excel e leggere
  il risultato della formula.
og_title: Crea un array dinamico in Excel con Python – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create dynamic array using Python and the SEQUENCE function in Excel.
    Learn to read formula result, recalculate Excel formulas, and see an Excel SEQUENCE
    example.
  headline: Create Dynamic Array in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
tags:
- excel
- python
- xlwings
- dynamic arrays
title: Crea un array dinamico in Excel con Python – Guida passo‑passo
url: /it/python/import-and-export/create-dynamic-array-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un Array Dinamico in Excel con Python – Guida Completa

Ti sei mai chiesto come **creare formule di array dinamico** in Excel senza uscire dal tuo script Python? Non sei l'unico. Che tu stia automatizzando un report mensile o costruendo un motore dati leggero, poter inserire una formula `SEQUENCE` in una cartella di lavoro, ricalcolare e recuperare l’intervallo di spill back in Python è una vera rivoluzione.

In questo tutorial percorreremo un **esempio pratico di sequenza Excel**, ti mostreremo come **leggere il risultato della formula** e spiegheremo il modo migliore per **ricalcolare le formule Excel** dopo aver iniettato nuova logica. Alla fine avrai uno script autonomo che potrai copiare‑incollare, eseguire e adattare alle tue esigenze.

## Cosa Imparerai

- Come funziona la funzione `SEQUENCE` e perché è perfetta per generare matrici.
- La differenza tra un valore di cella normale e l’indirizzo di un intervallo di spill.
- Uso di `wb.calculate_formula()` (o equivalente) per forzare Excel a valutare le nuove formule.
- Estrarre l’indirizzo di un array dinamico con `ANCHORARRAY`.
- Un esempio Python completo, eseguibile, che puoi inserire in qualsiasi progetto.

Non è necessaria alcuna esperienza pregressa con il nuovo motore di array dinamici di Excel—basta una conoscenza di base di Python e una libreria come **xlwings** che possa parlare con Excel.

---

## Come Creare un Array Dinamico con SEQUENCE in Excel Usando Python

Il primo passo è scrivere una formula **array dinamico** direttamente in una cella del foglio. Nelle versioni moderne di Excel, la funzione `SEQUENCE` può generare una matrice di numeri al volo. Ecco la sintassi che utilizzeremo:

```python
# Step 1: Write a dynamic array formula that generates a 3×2 matrix starting at 10 with step 5
ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"   # Returns a 3×2 array
```

**Perché `SEQUENCE`?**  
Pensala come la versione integrata di `range()` di Excel per i fogli di calcolo. Ti permette di specificare righe, colonne, valore iniziale e incremento—tutto in un’unica riga ordinata. Nel nostro caso chiediamo 3 righe e 2 colonne, iniziando da 10 e avanzando di 5, ottenendo:

|   | A | B |
|---|---|---|
|1|10|15|
|2|20|25|
|3|30|35|

Poiché la formula vive in `A1`, Excel “spill” automaticamente il risultato nelle celle adiacenti `A1:B3`. Quello spill è ciò che recupereremo più tardi.

---

## Usare la Funzione SEQUENCE in Excel – Un Rapido Esempio di Sequenza Excel

Se apri Excel manualmente e digiti `=SEQUENCE(3,2,10,5)` in una cella, vedrai immediatamente apparire la stessa matrice. La funzione fa parte del motore **array dinamico** di Excel introdotto in Office 365, il che significa:

- Nessuna necessità di Ctrl+Shift+Enter.
- Il risultato può espandersi o contrarsi automaticamente.
- Puoi fare riferimento all’intero intervallo di spill con funzioni come `@` o `#`.

In Python, l’unica differenza è che assegniamo la formula come stringa alla proprietà `.formula` della cella. La libreria si occupa del resto.

---

## Recuperare l’Indirizzo dello Spill con ANCHORARRAY

Una volta che l’array dinamico è stato inserito, spesso è necessario sapere dove Excel ha effettivamente posizionato i valori. Qui entra in gioco `ANCHORARRAY`. Restituisce l’indirizzo della cella in alto‑a‑sinistra dell’intervallo di spill—esattamente ciò che ci serve per leggere nuovamente nello script.

```python
# Step 2: Retrieve the address of the spill range produced by the formula in A1
ws.cells["C1"].formula = "=ANCHORARRAY(A1)"      # Returns the address of the spill range
```

Inserendo questa formula in `C1` otteniamo una stringa di testo come `"A1:B3"`. Nota che **leggiamo il risultato della formula** come valore semplice, non come un’altra formula. Questo piccolo trucco evita di dover analizzare manualmente il foglio.

---

## Ricalcolare le Formule Excel e Leggere il Risultato

Excel non sempre ricalcola immediatamente quando una nuova formula viene iniettata da uno script esterno. Per garantire che la cartella di lavoro rifletta le ultime modifiche, attiviamo esplicitamente un passaggio di calcolo.

```python
# Step 3: Recalculate all formulas in the workbook and read the result
wb.calculate_formula()               # Forces Excel to evaluate pending formulas
print(ws.cells["C1"].value)          # → "A1:B3"
```

**Perché chiamare `calculate_formula()`?**  
Se salti questo passaggio, `ws.cells["C1"].value` potrebbe ancora restituire `None` o un indirizzo obsoleto perché Excel è ancora occupato ad aggiornare il suo albero di dipendenze. Forzando il ricalcolo assicuriamo che il **risultato della formula letta** sia aggiornato.

---

## Script Completo – Dall’Inizio alla Fine

Di seguito trovi un esempio completo, pronto all’esecuzione, che collega tutti i passaggi. Presuppone che tu abbia **xlwings** installato (`pip install xlwings`) e che Excel sia disponibile sulla tua macchina.

```python
import xlwings as xw

def create_dynamic_array_example():
    # Open a new workbook (or attach to an existing one)
    wb = xw.Book()               # Creates a fresh Excel workbook
    ws = wb.sheets[0]            # Grab the first worksheet

    # 1️⃣ Write the SEQUENCE formula – this creates a 3×2 matrix starting at 10, step 5
    ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"

    # 2️⃣ Use ANCHORARRAY to capture the spill range address in C1
    ws.cells["C1"].formula = "=ANCHORARRAY(A1)"

    # 3️⃣ Force Excel to recalculate so that the ANCHORARRAY result is current
    wb.calculate_formula()

    # 4️⃣ Read back the address – this is our **read formula result** step
    spill_address = ws.cells["C1"].value
    print(f"The dynamic array spills into: {spill_address}")

    # 5️⃣ Optionally, fetch the actual values from the spill range
    # xlwings can read a range by address, so we demonstrate that too
    data = ws.range(spill_address).value
    print("Matrix values:")
    for row in data:
        print(row)

    # Clean up – close without saving to keep the demo tidy
    wb.close(save=False)

if __name__ == "__main__":
    create_dynamic_array_example()
```

### Output Atteso

```
The dynamic array spills into: A1:B3
Matrix values:
[10, 15]
[20, 25]
[30, 35]
```

Eseguendo lo script si aprirà Excel, verrà inserita la formula `SEQUENCE`, verrà ricalcolato e poi verranno stampati sia l’indirizzo dello spill sia la matrice stessa. Nessun click manuale necessario.

---

## Errori Comuni e Pro Tips

- **Errore:** Dimenticare `wb.calculate_formula()`.  
  *Risultato:* `C1` rimane vuoto o mostra un indirizzo obsoleto.  
  *Correzione:* Attiva sempre un calcolo dopo aver scritto nuove formule.

- **Errore:** Usare una versione di Excel più vecchia che non supporta la funzione `SEQUENCE`.  
  *Risultato:* errore `#NAME?`.  
  *Correzione:* Assicurati di avere Office 365 o Excel 2021+.

- **Pro tip:** Se ti serve l’intervallo di spill per ulteriori elaborazioni (ad es. grafici), puoi passare direttamente l’indirizzo a `ws.range(spill_address)` come mostrato sopra.

- **Pro tip:** `ANCHORARRAY` funziona con qualsiasi array dinamico, non solo con `SEQUENCE`. Sostituisci con `=SORT(A2:A10)` o `=FILTER(...)` e otterrai comunque l’indirizzo corretto dello spill.

- **Caso limite:** Quando l’area di destinazione è già occupata, Excel restituisce un errore `#SPILL!`. In tal caso, cancella prima l’intervallo di destinazione o sposta la formula in un’altra cella.

---

## Estendere l’Esempio – Cosa Fare Dopo?

Ora che sai **creare formule di array dinamico**, **leggere il risultato della formula** e **ricalcolare le formule Excel**, puoi esplorare scenari più avanzati:

- **Dati dinamici per grafici** – alimenta un intervallo di spill come sorgente di un grafico e lascia che il grafico cresca automaticamente.
- **Formattazione condizionale** – applica regole all’intervallo di spill usando il suo indirizzo.
- **Riferimenti tra cartelle di lavoro** – scrivi un array dinamico in una cartella e recupera i dati in un’altra tramite collegamenti `xlwings`.

Ognuno di questi si basa sui concetti fondamentali trattati qui, quindi sentiti libero di sperimentare. L’unico limite è la tua immaginazione (e forse il numero massimo di righe/colonne di Excel).

---

## Conclusione

Abbiamo appena percorso un flusso di lavoro completo per **creare formule di array dinamico** in Excel da Python, usare la **funzione SEQUENCE**, recuperare l’intervallo di spill con **ANCHORARRAY**, **ricalcolare le formule Excel** e infine **leggere il risultato della formula** nel tuo script. L’esempio breve dimostra quanto potente possa essere il nuovo motore di array dinamici di Excel quando è abbinato a strumenti di automazione come **xlwings**.

Provalo nei tuoi progetti, modifica le dimensioni della matrice o sostituisci `SEQUENCE` con qualsiasi altra funzione dinamica. Man mano che ti sentirai più a tuo agio, scoprirai che automatizzare Excel diventa non solo possibile, ma anche piacevolmente semplice.

Hai domande o vuoi condividere come hai esteso questo modello? Lascia un commento qui sotto, e buona programmazione!

## Cosa Dovresti Imparare Dopo?


I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)
- [Create Dynamic Line Charts in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Create Dynamic Excel Charts with Aspose.Cells Java&#58; A Comprehensive Guide for Developers](/cells/english/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}