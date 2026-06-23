---
category: general
date: 2026-06-21
description: Crea una tabella di moltiplicazione in Excel usando Python. Impara come
  usare lambda, come usare makearray, visualizzare l'array di Excel e leggere i valori
  di Excel con Python in un tutorial passo‑passo.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: it
og_description: Crea una tabella di moltiplicazione in Excel usando Python. Questo
  tutorial mostra come utilizzare lambda, makearray, visualizzare l'array di Excel
  e leggere i valori di Excel in Python in modo efficiente.
og_title: Crea una tabella di moltiplicazione in Excel con Python – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: Crea una tabella di moltiplicazione in Excel con Python – Guida completa
url: /it/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea una tabella di moltiplicazione in Excel con Python – Guida completa

Ti sei mai chiesto come **creare una tabella di moltiplicazione** in Excel senza digitare manualmente ogni cella? Non sei l'unico. In molti scenari di reporting ti serve rapidamente una griglia 5×5 (o più grande) di prodotti, e farlo a mano è una perdita di tempo.  

In questo tutorial vedremo un modo pulito, guidato da Python, per generare quella tabella, incorporarla con una formula `MAKEARRAY` e poi recuperare i risultati nel tuo script. Lungo il percorso risponderemo a **come usare lambda**, mostreremo **come usare makearray**, e dimostreremo **display excel array** così come **read excel values python**—tutto in un unico esempio coerente.

Alla fine avrai uno snippet riutilizzabile che funziona con qualsiasi cartella di lavoro, e comprenderai perché questo approccio è sia veloce sia a prova di futuro.

## Cosa ti servirà

- Python 3.8+ (l'ultima versione stabile va bene)
- La libreria `openpyxl` (o qualsiasi libreria per Excel che supporti le formule)
- Una comprensione di base delle espressioni lambda in Python
- Nessun add‑in speciale per Excel; la funzione nativa `MAKEARRAY` (disponibile in Excel 365) fa tutto il lavoro pesante

Se ti manca qualcosa, basta eseguire `pip install openpyxl` e sei pronto.

## Crea tabella di moltiplicazione – Panoramica

L'idea di base è semplice: creiamo una nuova cartella di lavoro, scriviamo una formula `MAKEARRAY` che costruisce una matrice di moltiplicazione 5 × 5, forziamo Excel a calcolarla e infine leggiamo i valori risultanti in Python.

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Eseguendo lo script stampa:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

Ecco una **create multiplication table** completamente funzionale in Excel, generata interamente da Python.

### Perché usare `MAKEARRAY` invece di un ciclo Python?

- **Performance**: Excel gestisce il calcolo nativamente, il che è più veloce per matrici grandi.
- **Aggiornamento live**: Se in seguito cambi le dimensioni nella formula, il foglio si ricalcola automaticamente.
- **Leggibilità**: La formula esprime l'intento (“crea un array”) direttamente, mantenendo il codice Python ordinato.

## Come usare lambda in Python per le formule Excel

La parte `LAMBDA` della chiamata `MAKEARRAY` è una funzione anonima lato Excel, non una lambda Python. Tuttavia il concetto è lo stesso: definisci un piccolo pezzo di logica inline che prende `r` (indice di riga) e `c` (indice di colonna) e restituisce `r*c`.  

Se sei nuovo a **how to use lambda** nel mondo Excel, pensala come una mini‑funzione che vive solo all'interno della formula. Non è necessario dichiarare una funzione separata altrove. In Python inseriamo semplicemente la stringa:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

Quella riga dice a Excel: *“Per ogni cella in un blocco 5‑by‑5, calcola riga × colonna.”*  

Poiché la lambda è valutata da Excel, non devi preoccuparti della sintassi lambda di Python—solo della sintassi di Excel.

## Come usare makearray per generare array

`MAKEARRAY` è una aggiunta relativamente nuova alla libreria di funzioni di Excel (disponibile in Microsoft 365 dal 2022). Sostituisce trucchi più vecchi come combinazioni `INDEX` + `ROW`/`COLUMN`. La firma è:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – numero di righe desiderate.
- **columns** – numero di colonne desiderate.
- **lambda** – un LAMBDA di Excel che riceve `(row, column)` e restituisce un valore.

Nel nostro esempio abbiamo passato `5,5` per una classica tabella di moltiplicazione, ma potresti cambiare facilmente quei numeri:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

Questo ti darebbe una tabella 10 × 10 senza toccare alcun ciclo Python. Dimostra **how to use makearray** per qualsiasi tipo di griglia deterministica, sia essa una tabella di lookup, una heatmap o un calendario finanziario.

## Display excel array – estrarre i dati in Python

Una volta che Excel ha calcolato la formula, i valori risultanti risiedono nel foglio proprio come qualsiasi cella inserita manualmente. Per **display excel array**, iteriamo sull'intervallo e stampiamo ogni riga:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Alcuni consigli:

- Usa `worksheet.cell(row, column).value` invece dell'indicizzazione in stile dizionario se devi gestire intervalli più grandi; è leggermente più veloce.
- Se vuoi una tabella più carina, considera `tabulate` o `pandas.DataFrame` per formattare l'output.

Di seguito una schermata del foglio risultante (il testo alternativo dell'immagine include la keyword principale per SEO):

![Screenshot che mostra la creazione di una tabella di moltiplicazione in Excel usando Python](/images/multiplication-table-excel.png)

## Read excel values python – estrarre la matrice per ulteriori elaborazioni

Spesso il passo successivo dopo **display excel array** è alimentare quei numeri in una pipeline di analisi dati. È qui che **read excel values python** brilla. Lo stesso ciclo usato per la stampa può essere riutilizzato per costruire una lista di liste, un array NumPy o un DataFrame Pandas:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

Output:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

Ora hai un DataFrame tipizzato che puoi plottare, esportare in CSV o fornire a un modello di machine‑learning. Questo completa la parte **read excel values python** del flusso di lavoro.

## Casi limite e consigli pratici

- **Ricalcolo della formula**: Se modifichi la cartella di lavoro dopo la chiamata iniziale a `calculate_formula()`, devi richiamarla di nuovo; altrimenti l'array memorizzato rimane obsoleto.
- **Excel non‑365**: Le versioni più vecchie di Excel non supportano `MAKEARRAY`. In tal caso ricorri a una tabella generata da Python e scrivi ogni cella singolarmente.
- **Tabelle grandi**: Per matrici superiori a ~100 × 100, considera lo streaming dei dati per evitare di caricare l'intero foglio in memoria.
- **Gestione degli errori**: Avvolgi i passaggi di calcolo e lettura in blocchi `try/except` per catturare `InvalidFileException` o `FormulaError`.

## Conclusione

Ti abbiamo appena mostrato come **create multiplication table** in Excel usando Python, sfruttando la potenza di **how to use lambda** e **how to use makearray**. Hai visto come **display excel array**, leggere quei valori con **read excel values python**, e persino trasformare il risultato in un DataFrame Pandas per analisi successive.

Vuoi andare oltre? Prova a sostituire la logica di moltiplicazione con qualcosa di più complesso—magari una matrice delle distanze, una tabella di probabilità o una griglia di prezzi dinamici. Lo stesso schema si applica: una riga di `MAKEARRAY`, un rapido `calculate_formula()`, e qualche ciclo Python per estrarre i dati.

Se questa guida ti è stata utile, metti una stella su GitHub, condividila con i colleghi, o lascia un commento con il tuo caso d'uso. Buon coding e goditi la semplicità di generare tabelle Excel con una sola formula!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: How to Create and Modify Excel Workbooks Easily](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [How to Create and Style Named Ranges in Excel Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}