---
category: general
date: 2026-06-08
description: Crea un esempio di workbook Excel in Python che mostra come utilizzare
  lambda in Excel, sommare le righe con BYROW e automatizzare i calcoli in pochi passaggi.
draft: false
keywords:
- create excel workbook python
- how to use lambda
- how to sum rows
- use lambda excel
language: it
og_description: Crea una cartella di lavoro Excel con Python e impara a usare lambda
  in Excel per sommare le righe in modo efficiente con le formule BYROW.
og_title: Crea una cartella di lavoro Excel con Python – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook Python example that shows how to use lambda in
    Excel, sum rows with BYROW, and automate calculations in a few steps.
  headline: Create Excel Workbook Python – Complete Guide with Lambda
  type: TechArticle
tags:
- python
- excel
- automation
title: Creare un workbook Excel con Python – Guida completa con Lambda
url: /it/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea Excel Workbook Python – Guida Completa con Lambda

Ti sei mai chiesto come **creare Excel workbook Python** script che automatizzano noiose operazioni di calcolo? Non sei solo—molti sviluppatori si trovano in difficoltà quando devono generare un foglio, inserire una formula e recuperare i risultati nel loro codice.  

In questo tutorial mostreremo anche **come usare lambda** in Excel, spiegheremo **come sommare le righe** con la moderna funzione `BYROW`, e ti forniremo un esempio completo, pronto da copiare‑incollare ed eseguire oggi.

## Cosa Imparerai

- Configurare una nuova cartella di lavoro da Python senza aprire Excel manualmente.  
- Riempire un intervallo con una matrice 3 × 3 di numeri.  
- Inserire una formula `BYROW` che utilizza la sintassi **use lambda excel** per sommare ogni riga.  
- Ricalcolare il foglio affinché la formula venga valutata, quindi leggere i risultati nuovamente in Python.  

Alla fine di questa guida avrai uno script autonomo che potrai adattare per fatture, schede di punteggio o qualsiasi situazione in cui sia necessario **sum rows** al volo.

### Prerequisiti

- Python 3.8+ installato.  
- La libreria `openpyxl` (o `xlwings` se preferisci un approccio basato su COM). Useremo `openpyxl` perché è pure‑Python e funziona su tutte le piattaforme.  
- Una versione recente di Microsoft Excel (365 o 2021) che supporta la funzione `BYROW` e le formule Lambda.  

Installa la libreria con:

```bash
pip install openpyxl
```

> **Suggerimento professionale:** Se riscontri problemi di permessi su Windows, usa `python -m pip install --user openpyxl`.

---

## Crea Excel Workbook Python – Inizializza Cartella di Lavoro

La prima cosa di cui abbiamo bisogno è un nuovo oggetto workbook che risiede interamente in memoria. Con `openpyxl` è una singola riga:

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and grab the first worksheet
wb = Workbook()
ws = wb.active   # .active is the first sheet by default
```

Perché usiamo `wb.active` invece di indicizzare `Worksheets[0]`? `openpyxl` espone direttamente il foglio attivo, il che è più chiaro ed evita una ricerca aggiuntiva nella lista. Se mai dovessi lavorare con più fogli, puoi sempre aggiungerli con `wb.create_sheet(title="MySheet")`.

---

## Riempire il Foglio di Lavoro con Dati – Una Semplice Matrice 3×3

Successivamente, popoliamo il foglio con una piccola matrice. Questo rispecchia l'esempio classico “somma ogni riga” e mantiene il codice compatto.

```python
# Step 2: Define a 3×3 matrix of numbers
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Import the matrix into the worksheet starting at cell A1
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, value in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=value)
```

Potresti chiederti perché iteriamo manualmente invece di usare `ws.append()` o `ws.values`. I loop espliciti ci danno il pieno controllo sulla cella di partenza e rendono facile regolare gli offset in seguito—utile quando vuoi lasciare una riga o colonna di intestazione vuota.

---

## Come Usare Lambda nelle Formule Excel

La funzionalità **use lambda excel** di Excel ti permette di scrivere funzioni anonime direttamente in una cella. Pensala come il `lambda` di Python, ma all'interno del motore del foglio di calcolo. La sintassi è:

```
=LAMBDA(parameter1, parameter2, …, calculation)
```

Quando combinata con `BYROW`, puoi applicare quel lambda a ogni riga di un intervallo, producendo una colonna di risultati. Questo è il fulcro del nostro trucco **how to sum rows**.

```python
# Step 3: Insert a BYROW formula that sums each row using a Lambda
ws["D1"] = "=BYROW(A1:C3, LAMBDA(r, SUM(r)))"
```

Cosa succede dietro le quinte?

- `A1:C3` è l'intervallo di origine (la nostra matrice).  
- `LAMBDA(r, SUM(r))` definisce una funzione temporanea che riceve una singola riga (`r`) e ne restituisce la somma.  
- `BYROW` esegue quel lambda per **ogni riga** e riversa i risultati nella colonna D, a partire da `D1`.  

Poiché `BYROW` è una funzione *array dinamico*, Excel riempie automaticamente `D1:D3` con le tre somme.

> **Nota:** `BYROW` e le formule Lambda sono disponibili solo in Excel 365/2021 e versioni successive. Se utilizzi una versione più vecchia, dovrai tornare alle tradizionali formule `SUM` o a VBA.

---

## Come Sommare le Righe con BYROW e Lambda

Ora che la formula è nel foglio, dobbiamo far valutare Excel. `openpyxl` di per sé non calcola le formule; si limita a leggerle/scriverle. Per avviare un calcolo possiamo:

1. Salvare la cartella di lavoro e aprirla in Excel (manuale).  
2. Usare il motore COM `xlwings` per forzare il ricalcolo (richiede Excel installato).  

Per una soluzione puramente Python useremo `xlwings` solo per il passo di calcolo—niente di più.

```python
import xlwings as xw

# Step 4: Recalculate the workbook so the BYROW formula is evaluated
# Save the workbook to a temporary file first
temp_path = "temp_workbook.xlsx"
wb.save(temp_path)

# Open the file with xlwings, force a calculation, then close
app = xw.App(visible=False)
book = app.books.open(temp_path)
book.api.CalculateFull()          # Full recalculation
book.save()
book.close()
app.quit()
```

Perché non chiamare `wb.calculate()`? `openpyxl` non ha un motore nativo, quindi ci affidiamo a Excel stesso tramite `xlwings`. L'overhead è minimo per fogli piccoli e ci fornisce il risultato esatto che Excel mostrerebbe.

---

## Ricalcola e Recupera i Risultati – Riporta le Somme in Python

Infine, leggiamo i risultati riversati dalla colonna D. `openpyxl` rende questo semplice:

```python
# Step 5: Load the recalculated workbook and grab the results
wb = Workbook()  # re‑open the saved file
wb = xw.Book(temp_path).api  # alternative: use xlwings again to read values

# Using xlwings to fetch the range values as a Python list
results = xw.Range('D1:D3').value
print(results)   # Expected output: [6, 15, 24]
```

Se preferisci rimanere all'interno di `openpyxl`, puoi leggere le celle dopo il ricalcolo di Excel:

```python
from openpyxl import load_workbook

wb = load_workbook(temp_path, data_only=True)  # data_only reads calculated values
ws = wb.active
results = [ws[f"D{row}"].value for row in range(1, 4)]
print(results)   # -> [6, 15, 24]
```

Entrambi gli approcci restituiscono la stessa lista `[6, 15, 24]`, confermando che **how to sum rows** con `BYROW` + Lambda funziona come descritto.

---

## Casi Limite e Problemi Comuni

| Situazione | Cosa Controllare | Soluzione |
|------------|-------------------|-----------|
| Versione di Excel precedente a 365 | `BYROW` e `LAMBDA` appaiono come `#NAME?` | Usa la classica `=SUM(A1:C1)` copiata manualmente, o aggiorna Excel. |
| Matrici grandi (10 k+ righe) | Il ricalcolo può diventare lento | Chiama `book.api.CalculateFullRebuild()` una sola volta, o dividi la cartella di lavoro. |
| Esecuzione su server headless senza Excel | `xlwings` non può avviare Excel | Passa a una libreria pure‑Python come `pandas` + `numpy` per i calcoli, poi scrivi i risultati. |
| Problemi di locale (virgola vs punto e virgola) | La formula potrebbe essere rifiutata | Usa `ws["D1"].value = "=BYROW(A1:C3; LAMBDA(r; SUM(r)))"` per i locali che usano `;`. |

---

## Esempio Completo (Pronto per Copia‑Incolla)

```python
# ------------------------------------------------------------
# create_excel_workbook_python – full script
# ------------------------------------------------------------
import os
from openpyxl import Workbook, load_workbook
import xlwings as xw

# 1️⃣ Initialize workbook
wb = Workbook()
ws = wb.active

# 2️⃣ Populate with a 3×3 matrix
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, val in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=val)

# 3️⃣ Insert BYROW + Lambda formula


## What Should You Learn Next?


I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea Excel Workbook con Aspose.Cells Java - Guida Completa](/cells/english/java/automation-batch-processing/excel-automation-aspose-cells-java-guide/)
- [Crea Excel Workbook & Automatizza Report con Aspose.Cells](/cells/english/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/)
- [Come Creare e Salvare un Excel Workbook come ODS Usando Aspose.Cells per .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}