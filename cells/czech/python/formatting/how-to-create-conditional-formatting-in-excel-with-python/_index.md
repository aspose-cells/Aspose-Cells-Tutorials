---
category: general
date: 2026-11-16
description: Vytvořte podmíněné formátování v Excelu pomocí Pythonu. Naučte se přidat
  oblast podmíněného formátování, zvýraznit data a programově vytvořit sešit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: cs
lastmod: 2026-11-16
og_description: Vytvořte podmíněné formátování v Excelu pomocí Pythonu. Tento tutoriál
  ukazuje, jak přidat oblast podmíněného formátování, zvýraznit data a vytvořit sešit.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Vytvořte podmíněné formátování v Excelu pomocí Pythonu – krok za krokem
  průvodce
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Jak vytvořit podmíněné formátování v Excelu pomocí Pythonu
url: /cs/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit podmíněné formátování v Excelu pomocí Pythonu

Pokud potřebujete **vytvořit podmíněné formátování** v souboru Excel při práci v Pythonu, tento návod vám ukáže přesně, jak na to. Naučíte se **vytvořit excel workbook python**‑styl, definovat rozsah formátování a zvýraznit data, aniž byste opustili IDE.

Podmíněné formátování vám umožní vizuálně označit buňky, které splňují konkrétní kritéria — ideální pro dashboardy, reporty nebo listy s validací dat. Na konci tohoto tutoriálu budete mít plně funkční sešit, který buňky s datem „Yesterday“ zbarví růžově, zatímco zbytek rozsahu zůstane zelený.

## Co dosáhnete

* Vytvoříte nový sešit od nuly.  
* Přidáte kolekci podmíněného formátování pro konkrétní blok buněk.  
* Aplikujete pravidlo **TIME_PERIOD**, které zvýrazní data (scénář „jak zvýraznit data“).  
* Soubor uložíte jako XLSX sešit připravený pro další zpracování.

**Předpoklady**  
* Python 3.8+  
* Python‑balíček `aspose-cells` (`pip install aspose-cells`)  
* Základní znalost modulu `datetime` v Pythonu  

---

## Jak vytvořit podmíněné formátování v Pythonu

Prvním krokem je nastavit sešit a list, který bude hostit pravidla formátování.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Proč je to důležité** — `Workbook` je vstupní bod pro všechny operace s Excelem. Vytvoření sešitu programově nahrazuje ruční krok „Soubor → Nový“ a umožňuje automatizované pipeline reportů.

---

## Příprava kolekce podmíněného formátování — přidání rozsahu

Dále definujeme blok buněk, který bude pravidlo přijímat. V tomto příkladu je rozsah **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Vysvětlení** — `conditional_formattings.add` zaregistruje novou kolekci svázanou s řetězcem adresy. První podmínka (`conds[0]`) funguje jako „výchozí“ styl; pozdější pravidlo ji přepíše, když budou splněna jeho kritéria.

---

## Přidání podmínky TIME_PERIOD — jak zvýraznit data

Nyní přidáme samotnou logiku, která identifikuje data „Yesterday“ a obarví je růžově.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Proč použít TIME_PERIOD?** — Aspose.Cells poskytuje vestavěné výčty jako `YESTERDAY`, `TODAY` a `LAST_WEEK`. Porovnávají hodnotu buňky s aktuálním systémovým datem, takže není potřeba psát vlastní vzorce.

---

## Naplnění ukázkových dat — demonstrování pravidla

Abychom viděli formátování v akci, vložíme datum, které pravidlo splňuje, a další, které ne.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Poznámka k okrajovým případům** — Pravidlo `TIME_PERIOD` funguje pouze s *reálnými* daty. Pokud buňka obsahuje text (např. „N/A“), pravidlo se ignoruje a nedojde k neočekávaným změnám barvy.

---

## Uložení sešitu — add conditional formatting python

Nakonec zapíšeme sešit na disk. Soubor lze otevřít v libovolném tabulkovém programu a ověřit barvy.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Očekávaný výsledek**  

| I19 (zelená → růžová) | J19 (zelená) | K19 (zelená) |
|-----------------------|-------------|-------------|
| 7/30/2008 (yesterday) | – | – |
| **I20**: “Yesterday” label | – | – |
| I21‑K21 (zelená) | – | – |

Buňka **I19** se zobrazí s růžovým pozadím, protože její datum odpovídá období „Yesterday“, zatímco **K20** zůstane zelená.

---

## Často kladené otázky a praktické tipy

* **Mohu místo vestavěného období použít vlastní rozsah dat?**  
  Ano. Nahraďte `condition.time_period` výrazem `condition.formula1 = "TODAY()-1"` a nastavte `condition.type = FormatConditionType.FORMULA`.

* **Co když můj sešit už obsahuje data?**  
  Použijte `worksheet.cells.import_data` pro hromadné načtení dat před přidáním kolekce podmíněného formátování.

* **Výkon u velkých listů?**  
  Přidání mnoha podmínek může zpomalit vykreslování. Seskupte buňky se stejným pravidlem do jednoho rozsahu (např. „A1:C1000”), aby se počet podmínek udržel nízko.

* **Kompatibilita napříč platformami?**  
  Vygenerovaný soubor XLSX dodržuje standard Office Open XML, takže funguje ve Windows, macOS i Linuxových tabulkových aplikacích.

---

## Závěr

Nyní víte, jak **vytvořit podmíněné formátování** v Excel sešitu pomocí Pythonu. Tutoriál pokryl vytvoření sešitu, definování **add conditional formatting range**, aplikaci pravidla **how to highlight dates** a uložení souboru — vše pomocí přístupu **add conditional formatting python**, který poskytuje Aspose.Cells.

Dále můžete:

* Rozšířit sadu pravidel o další hodnoty `TimePeriodType` (např. `TODAY`, `LAST_MONTH`).  
* Kombinovat více podmínek na stejném rozsahu pro bohatší vizuální náznaky.  
* Integrovat tento workflow do automatizovaných reportingových pipeline nebo webových služeb.

Šťastné programování a nebojte se experimentovat s různými barvami, rozsahy a logikou dat, aby vyhovovaly vašim reportingovým potřebám!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}