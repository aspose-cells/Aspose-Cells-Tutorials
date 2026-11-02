---
category: general
date: 2026-06-21
description: Povolte kontrolu pravopisu při exportu Excel JSON pomocí GridJs. Naučte
  se převádět xlsx na JSON, nastavit líné načítání a efektivně načíst Excel sešit.
draft: false
keywords:
- enable spell check
- export excel json
- convert xlsx to json
- configure lazy loading
- load excel workbook
language: cs
og_description: Povolte kontrolu pravopisu při exportu Excel JSON pomocí GridJs. Tento
  průvodce ukazuje, jak převést xlsx na JSON, nakonfigurovat lazy loading a načíst
  sešit Excel.
og_title: Povolit kontrolu pravopisu a exportovat Excel JSON pomocí GridJs
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Enable spell check while you export Excel JSON using GridJs. Learn
    to convert xlsx to JSON, configure lazy loading, and load Excel workbook efficiently.
  headline: Enable Spell Check & Export Excel JSON with GridJs
  type: TechArticle
tags:
- GridJs
- Excel
- JSON
- Python
title: Povolit kontrolu pravopisu a exportovat Excel JSON pomocí GridJs
url: /cs/python/import-and-export/enable-spell-check-export-excel-json-with-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Povolení kontroly pravopisu a export Excel JSON pomocí GridJs

Už jste někdy potřebovali **povolit kontrolu pravopisu** v webovém uživatelském rozhraní tabulky a přemýšleli, jak současně získat data jako JSON? Nejste v tom sami. Mnoho vývojářů narazí na stejný problém, když se snaží **exportovat Excel JSON** z sešitu a zároveň zachovat pokročilé funkce, jako je ověřování vzorců.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který vám ukáže, jak **načíst Excel workbook**, převést jej na JSON payload pomocí GridJs, **nastavit lazy loading** a samozřejmě **povolit kontrolu pravopisu**. Na konci budete schopni **převést xlsx na JSON** během několika řádků – žádná záhada, žádné chybějící kusy.

> **Co si z toho odnesete**  
> * Python skript, který načte soubor `.xlsx`, vytvoří objekt GridJs serveru a zapíše `grid_data.json`.  
> * Pochopení, proč každá volba má význam (kontrola pravopisu, kontrola vzorců, lazy loading).  
> * Tipy, jak škálovat řešení na větší sešity.

---

## Požadavky

Předtím, než se ponoříme, ujistěte se, že máte na svém počítači následující:

| Požadavek | Proč je důležité |
|-------------|----------------|
| Python 3.9+ | Vyžadováno pro balíček `cells` použitý níže. |
| `cells` library (`pip install cells`) | Poskytuje třídy `Workbook` a `GridJs`. |
| Vzorek Excel souboru (`sample.xlsx`) | Toto je zdroj, ze kterého **načteme excel workbook**. |
| Oprávnění k zápisu do výstupní složky | Potřebné pro krok `grid.save()`. |

Pokud některý z těchto bodů není vám známý, pozastavte se a nejprve jej nainstalujte – jinak skript vyvolá chybu importu.

---

## Krok 1: Načtení Excel workbook

První věc, kterou uděláte, když chcete **převést xlsx na json**, je otevřít workbook. Představte si to jako odemknutí dveří, než můžete pokoj vyzdobit.

```python
import cells

# Replace YOUR_DIRECTORY with the actual path on your system
workbook_path = "YOUR_DIRECTORY/sample.xlsx"

# Load the workbook – this is the entry point for all further operations
workbook = cells.Workbook(workbook_path)
print(f"Workbook loaded: {workbook_path}")
```

> **Tip:** Pokud je váš soubor obrovský, zvažte použití `cells.Workbook(..., read_only=True)`, aby se snížila spotřeba paměti.

---

## Krok 2: Vytvoření GridJs serverového objektu

Nyní, když je workbook v paměti, potřebujeme objekt **GridJs**, který přeloží listy do JSONu, který může koncové UI spotřebovat.

```python
# Create a GridJs instance linked to the workbook
grid = cells.GridJs(workbook)
print("GridJs server object created.")
```

Proměnná `grid` je v podstatě tenký obal kolem workbooku, který umí serializovat buňky, vzorce a dokonce i informace o stylování.

---

## Krok 3: Povolení kontroly pravopisu (a kontrola vzorců)

Zde se hlavní klíčové slovo ukáže v plné síle. Přepnutím příznaku `enableSpellCheck` poskytujete koncovým uživatelům bezpečnostní síť proti překlepům – stejně jako v desktopové verzi Excelu.

```python
# Turn on advanced validation features
grid.options["enableFormulaChecker"] = True   # optional but handy
grid.options["enableSpellCheck"] = True       # <-- enable spell check
print("Spell check and formula checker enabled.")
```

Proč povolit obojí? Kontrola pravopisu zachytí textové chyby, zatímco kontrola vzorců chrání před poškozenými výpočty. Společně dodávají webovému UI pocit takového sametového zážitku jako nativní Excel.

---

## Krok 4: Nastavení lazy loading

Pokud pracujete s tisíci řádky, odeslání celého datasetu v jednom payloadu přetíží prohlížeč. **Nastavte lazy loading**, aby se data posílala po menších kouscích (500 řádků na požadavek v našem příkladu).

```python
# Lazy loading improves performance for large sheets
grid.options["lazyLoading"] = {"pageSize": 500}
print("Lazy loading configured: 500 rows per request.")
```

`pageSize` můžete ladit podle podmínek vaší sítě. Menší stránky znamenají více round‑tripů, ale plynulejší UI; větší stránky snižují počet volání, ale mohou způsobit zpoždění.

---

## Krok 5: Export Excel JSON

Veškerá těžká práce proběhla na pozadí. Posledním krokem je **exportovat excel json** do souboru, který může váš front‑end požadovat.

```python
# Destination for the generated JSON
output_path = "YOUR_DIRECTORY/grid_data.json"

# Persist the JSON representation
grid.save(output_path)
print(f"JSON exported to: {output_path}")
```

Když metoda `save` dokončí, budete mít úhledný `grid_data.json`, který obsahuje:

* Názvy listů a jejich ID  
* Data řádků (hodnoty, vzorce a formátování)  
* Metadata o povolených funkcích (kontrola pravopisu, lazy loading, atd.)

Výstup můžete ověřit otevřením souboru v textovém editoru nebo načtením v konzoli prohlížeče:

```json
{
  "sheets": [
    {
      "name": "Sheet1",
      "rows": [
        {"c": [{"v": "Hello"}, {"v": 123}]},
        {"c": [{"v": "World"}, {"v": 456}]}
      ]
    }
  ],
  "options": {
    "enableSpellCheck": true,
    "enableFormulaChecker": true,
    "lazyLoading": {"pageSize": 500}
  }
}
```

To je **kompletní, samostatné řešení** pro převod Excel souboru na JSON payload při zachování kontroly pravopisu.

---

## Úplný skript – spojení všeho dohromady

Níže je celý program, který můžete zkopírovat, upravit cesty a spustit. Žádné skryté kroky, žádné externí skripty – jen jeden soubor.

```python
import cells

# ----------------------------------------------------------------------
# Configuration – adjust these variables to match your environment
# ----------------------------------------------------------------------
WORKBOOK_PATH = "YOUR_DIRECTORY/sample.xlsx"
OUTPUT_JSON = "YOUR_DIRECTORY/grid_data.json"
PAGE_SIZE = 500   # rows per lazy‑load request

# ----------------------------------------------------------------------
# 1️⃣ Load the Excel workbook
# ----------------------------------------------------------------------
workbook = cells.Workbook(WORKBOOK_PATH)
print(f"[✓] Loaded workbook from {WORKBOOK_PATH}")

# ----------------------------------------------------------------------
# 2️⃣ Create GridJs server object
# ----------------------------------------------------------------------
grid = cells.GridJs(workbook)
print("[✓] GridJs instance ready")

# ----------------------------------------------------------------------
# 3️⃣ Enable spell check + formula checking
# ----------------------------------------------------------------------
grid.options["enableFormulaChecker"] = True
grid.options["enableSpellCheck"] = True
print("[✓] Spell check and formula checker enabled")

# ----------------------------------------------------------------------
# 4️⃣ Configure lazy loading for performance
# ----------------------------------------------------------------------
grid.options["lazyLoading"] = {"pageSize": PAGE_SIZE}
print(f"[✓] Lazy loading set to {PAGE_SIZE} rows per request")

# ----------------------------------------------------------------------
# 5️⃣ Export the workbook as JSON
# ----------------------------------------------------------------------
grid.save(OUTPUT_JSON)
print(f"[✓] Exported JSON to {OUTPUT_JSON}")
```

Uložte tento soubor jako `export_gridjs.py` a spusťte:

```bash
python export_gridjs.py
```

Měli byste vidět sérii zpráv `[✓]`, které potvrzují úspěšné dokončení každého kroku.

---

## Časté otázky a okrajové případy

**Co když můj workbook obsahuje více listů?**  
GridJs automaticky iteruje přes každý list, takže výsledný JSON bude mít pole `sheets`. Na klientské straně můžete filtrovat, pokud potřebujete jen podmnožinu.

**Mohu zakázat kontrolu pravopisu pro konkrétní list?**  
Slovník `options` se aplikuje globálně. Pro přepínání na úrovni listu byste museli vytvořit samostatné objekty `GridJs` nebo provést post‑processing JSONu.

**Můj soubor je větší než 10 MB — pomůže lazy loading stále?**  
Rozhodně. Lazy loading funguje na úrovni API; server streamuje jen požadovanou stránku. Přesto zvažte zvýšení `pageSize` na 1000, pokud je latence sítě nízká.

**Musím se starat o Unicode znaky?**  
`cells` zvládá UTF‑8 přímo, takže znaky jako emoji nebo ne‑latinské skripty přežijí celý proces.

---

## Tipy pro produkci

* **Cache JSON** – Pokud se workbook mění jen zřídka, uložte `grid_data.json` do CDN pro bleskově rychlé načítání.  
* **Bezpečnost** – Nikdy neexponujte surový Excel soubor; poskytujte jen vygenerovaný JSON.  
* **Verzování** – Přidejte číslo verze do názvu JSON souboru (např. `grid_data_v2.json`), aby nedocházelo k zastaralým datům po aktualizacích.  
* **Testování** – Napište malý unit test, který načte JSON a ověří, že `enableSpellCheck` je `true`. Zachytí regresní chyby včas.

---

## Závěr

Nyní máte solidní end‑to‑end recept na **povolení kontroly pravopisu**, zatímco **exportujete Excel JSON** pomocí GridJs. Od **načtení excel workbook** po **nastavení lazy loading** a nakonec **převod xlsx na json** je proces přímočarý a připravený pro produkci.

Další kroky? Zkuste vložit vygenerovaný `grid_data.json` do jednoduché HTML stránky, která používá klientskou knihovnu GridJs, experimentujte s vlastním renderováním buněk nebo přidejte autentizaci kolem JSON endpointu. Možnosti jsou neomezené, když zkombinujete kontrolu pravopisu, lazy loading a plynulý převod Excel → JSON.

Máte další otázky nebo obtížný workbook, se kterým bojujete? Zanechte komentář níže a šťastné kódování!  

---

![Povolení kontroly pravopisu v GridJs](/images/enable-spell-check-gridjs.png "Snímek obrazovky ukazující povolenou kontrolu pravopisu v uživatelském rozhraní GridJs")

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další API funkce a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Exportovat Excel do JSON](/cells/english/java/excel-import-export/export-excel-to-json/)
- [Importovat JSON data do Excelu pomocí Aspose.Cells Java: Kompletní průvodce](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Jak efektivně filtrovat data při načítání Excel workbooků pomocí Aspose.Cells v Javě](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}