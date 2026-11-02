---
category: general
date: 2026-06-08
description: Vytvořte příklad v Pythonu pro Excel sešit, který ukazuje, jak používat
  lambda v Excelu, sčítat řádky pomocí BYROW a automatizovat výpočty během několika
  kroků.
draft: false
keywords:
- create excel workbook python
- how to use lambda
- how to sum rows
- use lambda excel
language: cs
og_description: Vytvořte Excel sešit v Pythonu a naučte se, jak použít lambda v Excelu
  k efektivnímu sčítání řádků pomocí vzorců BYROW.
og_title: Vytvořte Excel sešit v Pythonu – Kompletní průvodce
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
title: Vytvoření Excel sešitu v Pythonu – Kompletní průvodce s Lambda
url: /cs/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel sešitu v Pythonu – Kompletní průvodce s Lambda

Už jste se někdy zamýšleli, jak **create Excel workbook Python** skripty, které automatizují nudné počítání čísel? Nejste sami – mnoho vývojářů narazí na problém, když potřebují vygenerovat list, vložit do něj vzorec a načíst výsledky zpět do svého kódu.  

V tomto tutoriálu také ukážeme **how to use lambda** v Excelu, vysvětlíme **how to sum rows** pomocí moderní funkce `BYROW` a poskytneme vám přehledný, end‑to‑end příklad, který můžete dnes zkopírovat a spustit.

## Co se naučíte

- Vytvořit nový sešit v Pythonu, aniž byste ručně otevírali Excel.  
- Vyplnit oblast 3 × 3 maticí čísel.  
- Vložit `BYROW` vzorec, který využívá syntaxi **use lambda excel** pro součet každého řádku.  
- Přepočítat list, aby se vzorec vyhodnotil, a poté načíst výsledky zpět do Pythonu.  

Na konci tohoto průvodce budete mít samostatný skript, který můžete přizpůsobit pro faktury, skórovací karty nebo jakoukoli situaci, kde potřebujete **sum rows** za běhu.

### Požadavky

- Nainstalovaný Python 3.8+.  
- Knihovna `openpyxl` (nebo `xlwings`, pokud dáváte přednost COM‑založenému přístupu). Použijeme `openpyxl`, protože je čistě v Pythonu a funguje na všech platformách.  
- Aktuální verze Microsoft Excel (365 nebo 2021), která podporuje funkci `BYROW` a Lambda vzorce.  

Install the library with:

```bash
pip install openpyxl
```

> **Pro tip:** Pokud narazíte na problémy s oprávněním ve Windows, použijte `python -m pip install --user openpyxl`.

## Vytvoření Excel sešitu v Pythonu – Inicializace sešitu

Prvním, co potřebujeme, je zcela nový objekt sešitu, který existuje výhradně v paměti. S `openpyxl` je to jednorázový řádek:

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and grab the first worksheet
wb = Workbook()
ws = wb.active   # .active is the first sheet by default
```

Proč používáme `wb.active` místo indexování `Worksheets[0]`? `openpyxl` přímo zpřístupňuje aktivní list, což je přehlednější a vyhýbá se dalšímu vyhledávání v seznamu. Pokud někdy potřebujete pracovat s více listy, můžete je vždy přidat pomocí `wb.create_sheet(title="MySheet")`.

## Vyplnění listu daty – Jednoduchá 3×3 matice

Dále naplníme list malou maticí. To odráží klasický příklad „součet každého řádku“ a udržuje kód stručný.

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

Možná se ptáte, proč cyklíme ručně místo použití `ws.append()` nebo `ws.values`. Explicitní smyčky nám poskytují plnou kontrolu nad počáteční buňkou a usnadňují pozdější úpravu offsetů – užitečné, když chcete nechat prázdný řádek nebo sloupec s hlavičkou.

## Jak použít Lambda ve vzorcích Excelu

Funkce Excelu **use lambda excel** vám umožňuje psát anonymní funkce přímo v buňce. Představte si to jako Python `lambda`, ale fungující uvnitř enginu tabulky. Syntaxe je:

```
=LAMBDA(parameter1, parameter2, …, calculation)
```

Když je spárována s `BYROW`, můžete tuto lambda funkci aplikovat na každý řádek rozsahu, což vytvoří sloupec výsledků. To je jádro našeho triku **how to sum rows**.

```python
# Step 3: Insert a BYROW formula that sums each row using a Lambda
ws["D1"] = "=BYROW(A1:C3, LAMBDA(r, SUM(r)))"
```

What’s happening under the hood?

- `A1:C3` je zdrojový rozsah (naše matice).  
- `LAMBDA(r, SUM(r))` definuje dočasnou funkci, která přijímá jeden řádek (`r`) a vrací jeho součet.  
- `BYROW` spouští tuto lambda funkci pro **každý řádek** a rozlévá výsledky do sloupce D, počínaje `D1`.  

Protože `BYROW` je funkce *dynamic array*, Excel automaticky vyplní `D1:D3` třemi součty.

> **Poznámka:** `BYROW` a Lambda vzorce jsou k dispozici pouze v Excelu 365/2021 a novějším. Pokud používáte starší verzi, budete muset přejít na tradiční `SUM` vzorce nebo VBA.

## Jak součíst řádky pomocí BYROW a Lambda

Nyní, když je vzorec v listu, musíme Excelu říct, aby jej vyhodnotil. `openpyxl` sám nepočítá vzorce; pouze je čte/zapisuje. Pro spuštění výpočtu můžeme buď:

1. Uložit sešit a otevřít jej v Excelu (ručně).  
2. Použít COM engine `xlwings` k vynucení přepočtu (vyžaduje nainstalovaný Excel).  

Pro čistě Python řešení použijeme `xlwings` jen pro krok výpočtu – nic víc.

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

Proč nevolat `wb.calculate()`? `openpyxl` postrádá nativní engine, takže se spoléháme na samotný Excel přes `xlwings`. Zátěž je minimální pro malé listy a poskytuje přesný výsledek, který by Excel zobrazil.

## Přepočítat a získat výsledky – Načíst součty zpět do Pythonu

Nakonec načteme rozlévané výsledky ze sloupce D. `openpyxl` to dělá přímočarě:

```python
# Step 5: Load the recalculated workbook and grab the results
wb = Workbook()  # re‑open the saved file
wb = xw.Book(temp_path).api  # alternative: use xlwings again to read values

# Using xlwings to fetch the range values as a Python list
results = xw.Range('D1:D3').value
print(results)   # Expected output: [6, 15, 24]
```

Pokud raději zůstáváte v `openpyxl`, můžete po přepočtu v Excelu načíst buňky:

```python
from openpyxl import load_workbook

wb = load_workbook(temp_path, data_only=True)  # data_only reads calculated values
ws = wb.active
results = [ws[f"D{row}"].value for row in range(1, 4)]
print(results)   # -> [6, 15, 24]
```

Oba přístupy vám vrátí stejný seznam `[6, 15, 24]`, což potvrzuje, že **how to sum rows** s `BYROW` + Lambda funguje podle očekávání.

## Okrajové případy a časté úskalí

| Situace | Na co si dát pozor | Řešení |
|-----------|-------------------|-----|
| Verze Excelu starší než 365 | `BYROW` a `LAMBDA` se zobrazí jako `#NAME?` | Použijte klasický `=SUM(A1:C1)` zkopírovaný dolů ručně, nebo aktualizujte Excel. |
| Velké matice (10 k+ řádků) | Přepočet může být pomalý | Zavolejte `book.api.CalculateFullRebuild()` jen jednou, nebo rozdělte sešit. |
| Běh na headless serveru bez Excelu | `xlwings` nemůže spustit Excel | Přepněte na čistě Python knihovnu jako `pandas` + `numpy` pro výpočty a pak zapište výsledky. |
| Problémy s locale (čárka vs. středník) | Vzorec může být odmítnut | Použijte `ws["D1"].value = "=BYROW(A1:C3; LAMBDA(r; SUM(r)))"` pro locale, které používají `;`. |

## Kompletní funkční příklad (připravený ke kopírování a vložení)

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


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvoření Excel sešitu s Aspose.Cells Java – Kompletní průvodce](/cells/english/java/automation-batch-processing/excel-automation-aspose-cells-java-guide/)
- [Vytvoření Excel sešitu a automatizace reportů s Aspose.Cells](/cells/english/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/)
- [Jak vytvořit a uložit Excel sešit jako ODS pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}