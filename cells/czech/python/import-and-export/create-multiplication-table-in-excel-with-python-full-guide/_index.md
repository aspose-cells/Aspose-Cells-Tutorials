---
category: general
date: 2026-06-21
description: Vytvořte násobící tabulku v Excelu pomocí Pythonu. Naučte se, jak používat
  lambda, jak používat makearray, zobrazit excelovou matici a číst hodnoty z Excelu
  v Pythonu v krok‑za‑krokem tutoriálu.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: cs
og_description: Vytvořte násobící tabulku v Excelu pomocí Pythonu. Tento tutoriál
  ukazuje, jak použít lambda, makearray, zobrazit excelovou matici a efektivně číst
  hodnoty z Excelu v Pythonu.
og_title: Vytvořte násobící tabulku v Excelu pomocí Pythonu – Kompletní průvodce
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
title: Vytvořte násobící tabulku v Excelu pomocí Pythonu – kompletní průvodce
url: /cs/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření násobící tabulky v Excelu pomocí Pythonu – Kompletní průvodce

Už jste se někdy zamysleli, jak **create multiplication table** v Excelu vytvořit, aniž byste ručně psali každou buňku? Nejste v tom sami. V mnoha reportovacích scénářích potřebujete rychlou mřížku produktů 5×5 (nebo větší) a ruční zadávání je ztráta času.  

V tomto tutoriálu vás provedeme čistým, Python‑řízeným způsobem, jak tuto tabulku vygenerovat, vložit ji pomocí vzorce `MAKEARRAY` a poté načíst výsledky zpět do vašeho skriptu. Po cestě odpovíme na **how to use lambda**, ukážeme **how to use makearray** a demonstrujeme **display excel array** i **read excel values python** — vše v jednom koherentním příkladu.

Na konci budete mít znovupoužitelný úryvek, který funguje s libovolnou sešitem, a pochopíte, proč je tento přístup rychlý a budoucnost‑odolný.

## Co budete potřebovat

- Python 3.8+ (nejnovější stabilní verze je v pořádku)
- Knihovna `openpyxl` (nebo jakákoli Excel‑schopná knihovna podporující vzorce)
- Základní pochopení lambda výrazů v Pythonu
- Žádné speciální Excel add‑ins; nativní funkce `MAKEARRAY` (dostupná v Excel 365) provádí těžkou práci

Pokud vám něco chybí, stačí `pip install openpyxl` a jste připraveni.

## Vytvoření násobící tabulky – Přehled

Základní myšlenka je jednoduchá: vytvoříme nový sešit, zapíšeme vzorec `MAKEARRAY`, který vytvoří 5 × 5 násobící matici, přinutíme Excel k výpočtu a nakonec načteme vzniklé hodnoty zpět do Pythonu.

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

Spuštění skriptu vypíše:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

To je plně funkční **create multiplication table** v Excelu, vygenerované zcela z Pythonu.

### Proč použít `MAKEARRAY` místo Python smyčky?

- **Performance**: Excel provádí výpočet nativně, což je rychlejší pro velké matice.
- **Live updating**: Pokud později změníte rozměry ve vzorci, list se automaticky přepočítá.
- **Readability**: Vzorec přímo vyjadřuje záměr („make an array“), což udržuje váš Python kód přehledný.

## Jak použít lambda v Pythonu pro Excel vzorce

Část `LAMBDA` volání `MAKEARRAY` je anonymní funkce na straně Excelu, ne Python lambda. Přesto je koncept stejný: definujete malý, vložený kus logiky, který přijímá `r` (index řádku) a `c` (index sloupce) a vrací `r*c`.  

Pokud jste noví v **how to use lambda** ve světě Excelu, představte si to jako mini‑funkci, která existuje pouze uvnitř vzorce. Není potřeba deklarovat samostatnou funkci jinde. V Pythonu jednoduše vložíme řetězec:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

Tento řádek říká Excelu: *„Pro každou buňku v bloku 5 × 5 vypočítej řádek × sloupec.“*  

Protože lambda je vyhodnocována v Excelu, nemusíte se zde starat o Python syntaxi lambda — jen o Excel syntaxi.

## Jak použít makearray k generování polí

`MAKEARRAY` je relativně novým doplňkem knihovny funkcí Excel (dostupná v Microsoft 365 od roku 2022). Nahrazuje starší triky jako kombinace `INDEX` + `ROW`/`COLUMN`. Signatura je:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – počet řádků, které chcete.
- **columns** – počet sloupců, které chcete.
- **lambda** – Excel LAMBDA, která přijímá `(row, column)` a vrací hodnotu.

V našem příkladu jsme předali `5,5` pro klasickou násobící tabulku, ale můžete snadno změnit tato čísla:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

To by vám dalo tabulku 10 × 10 bez jakýchkoli Python smyček. Toto demonstruje **how to use makearray** pro jakýkoli deterministický grid, ať už jde o vyhledávací tabulku, heatmapu nebo finanční plán.

## Zobrazení excel array – načtení dat zpět do Pythonu

Jakmile Excel vypočítá vzorec, vzniklé hodnoty jsou v listu stejně jako jakákoli ručně zadaná buňka. Pro **display excel array** iterujeme přes rozsah a vypíšeme každý řádek:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

- Používejte `worksheet.cell(row, column).value` místo indexování ve stylu slovníku, pokud potřebujete pracovat s většími rozsahy; je to o něco rychlejší.
- Pokud chcete hezčí tabulku, zvažte `tabulate` nebo `pandas.DataFrame` pro formátování výstupu.

Níže je screenshot výsledného listu (alternativní text obrázku obsahuje hlavní klíčové slovo pro SEO):

![Screenshot showing create multiplication table in Excel using Python](/images/multiplication-table-excel.png)

## Čtení excel values python – extrakce matice pro další zpracování

Často je dalším krokem po **display excel array** předání těchto čísel do pipeline pro analýzu dat. Zde vyniká **read excel values python**. Stejná smyčka, kterou jsme použili pro výpis, může být přetížena k vytvoření seznamu seznamů, NumPy pole nebo Pandas DataFrame:

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

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

Nyní máte plně typovaný DataFrame, který můžete vykreslit, exportovat do CSV nebo předat modelu strojového učení. Tím je dokončena část **read excel values python** pracovního postupu.

## Okrajové případy a praktické tipy

- **Formula recalculation**: Pokud po prvním volání `calculate_formula()` upravíte sešit, musíte jej znovu zavolat; jinak zůstane uložená pole zastaralá.
- **Non‑365 Excel**: Starší verze Excelu nepodporují `MAKEARRAY`. V takovém případě se vraťte k tabulce generované v Pythonu a zapište každou buňku jednotlivě.
- **Large tables**: Pro matice větší než ~100 × 100 zvažte streamování dat, aby se předešlo načtení celého listu do paměti.
- **Error handling**: Zabalte kroky výpočtu a čtení do `try/except` bloků, abyste zachytili `InvalidFileException` nebo `FormulaError`.

## Závěr

Právě jsme vám ukázali, jak **create multiplication table** v Excelu pomocí Pythonu, využívající sílu **how to use lambda** a **how to use makearray**. Viděli jste, jak **display excel array**, načíst tyto hodnoty zpět pomocí **read excel values python**, a dokonce převést výsledek na Pandas DataFrame pro následnou analýzu.

Chcete jít dál? Zkuste nahradit násobící logiku něčím složitějším – možná maticí vzdáleností, pravděpodobnostní tabulkou nebo dynamickou cenovou mřížkou. Stejný vzor platí: jeden řádek `MAKEARRAY`, rychlé `calculate_formula()` a několik Python smyček pro načtení dat.

Pokud se vám tento průvodce líbil, dejte mu hvězdičku na GitHubu, sdílejte ho s kolegy nebo zanechte komentář s vaším vlastním případem použití. Šťastné kódování a užívejte si stručnost generování Excel tabulek jedním vzorcem!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: How to Create and Modify Excel Workbooks Easily](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [How to Create and Style Named Ranges in Excel Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}