---
category: general
date: 2026-06-08
description: Odstraňte řádky v tabulce Word pomocí Aspose.Words. Naučte se, jak odstranit
  řádky, odstranit více řádků ve Wordu, a ovládněte úpravy tabulek během několika
  minut.
draft: false
keywords:
- delete rows word table
- how to delete rows
- delete multiple rows word
language: cs
og_description: Odstraňte řádky tabulky Word pomocí Aspose.Words. Tento tutoriál ukazuje,
  jak odstranit řádky, jak odstranit více řádků ve Wordu a udržet vaše tabulky přehledné.
og_title: Smazat řádky tabulky Word – kompletní průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  headline: Delete rows word table – Complete C# Guide
  type: TechArticle
- description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  name: Delete rows word table – Complete C# Guide
  steps:
  - name: 3.1 How to delete rows (single row)
    text: 'To remove a single row, call `DeleteRows(startIndex, count)` where `startIndex`
      is zero‑based. Skipping the header row (index 0) is common:'
  - name: 3.2 Delete multiple rows word – batch removal
    text: 'When you need to drop a range—say rows 2‑6—you pass the start index and
      the number of rows to erase. This is the **delete multiple rows word** pattern:'
  - name: Expected output
    text: '- `output.docx` contains the original table **without** rows 2‑6. - All
      remaining rows shift up, preserving cell formatting and column widths. - The
      header row stays intact, keeping your column titles visible.'
  type: HowTo
- questions:
  - answer: Absolutely. Loop through `table.Rows`, inspect `row.Cells[i].GetText()`,
      and collect matching indices. Then call `DeleteRows` with the smallest index
      and total count, or delete rows in reverse order to avoid re‑indexing.
    question: Can I delete rows based on cell content instead of index?
  - answer: Yes. Aspose.Words supports both `.doc` and `.docx`. Just change the file
      extension in the `Document` constructor and `Save` call.
    question: Does this work with .doc files?
  - answer: 'Retrieve it via `doc.FirstSection.HeadersFooters` collection, then apply
      the same `DeleteRows` logic. ## Conclusion You now have a solid, end‑to‑end
      solution for **delete rows word table** using C#. The example shows *how to
      delete rows* individually and how to **delete multiple rows word** in a sin'
    question: What if the table is inside a header/footer?
  type: FAQPage
tags:
- C#
- Aspose.Words
- Word automation
title: Odstranit řádky tabulky Word – kompletní průvodce C#
url: /cs/net/tables-and-lists/delete-rows-word-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Odstranění řádků tabulky Word – Kompletní průvodce C#

Už jste někdy potřebovali **delete rows word table**, ale nevedeli ste, kde začít? Nejste sami; mnoho vývojářů narazí na tento problém při čištění generovaných reportů nebo zmenšování tabulek řízených daty. Dobrá zpráva? S několika řádky C# a Aspose.Words můžete snadno odstranit nechtěné řádky, ať už jde o jeden řádek nebo jejich dávku. V tomto průvodci si projdeme *how to delete rows* a dokonce se podíváme na složitější případ **delete multiple rows word** najednou.

Probereme vše, co potřebujete vědět: přesný kód, proč je každý krok důležitý, běžné úskalí a připravený příklad. Na konci budete schopni odstranit řádky z libovolné tabulky Word, aniž byste narušili strukturu dokumentu. Žádné zbytečnosti, jen praktické, osvědčené techniky.

## Požadavky

Než se pustíme dál, ujistěte se, že máte:

- **Aspose.Words for .NET** (verze 23.12 nebo novější). Získáte jej z NuGet: `Install-Package Aspose.Words`.
- Vývojové prostředí .NET (Visual Studio, Rider nebo VS Code s rozšířením C#).
- Vstupní soubor Word (`input.docx`), který obsahuje alespoň jednu tabulku s řádkem záhlaví.

To je vše – žádné další knihovny, žádný COM interop, jen čistý spravovaný kód.

## Krok 1: Načtení dokumentu Word

První věc, kterou uděláte, je otevřít dokument. Aspose.Words zachází se souborem Word jako s objektem `Document`, který vám poskytuje plný přístup k sekcím, tělem, tabulkám a dalším částem.

```csharp
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // Load the source .docx file
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        // Continue with table manipulation…
```

*Proč je to důležité:* Načtení dokumentu vytvoří jeho reprezentaci v paměti, takže všechny změny jsou rychlé a nedotýkají se souborového systému, dokud je výslovně neuložíte.

## Krok 2: Získání cílové tabulky

Ve většině scénářů víte, kterou tabulku chcete upravit – často první. Aspose.Words to umožňuje jednoduše získat pomocí vlastnosti `FirstSection`.

```csharp
        // Access the first table in the first section
        Table table = doc.FirstSection.Body.Tables[0];
```

Pokud má váš dokument více tabulek, můžete projít `doc.GetChildNodes(NodeType.Table, true)` a vybrat tu správnou podle indexu nebo vlastního značkování.

## Krok 3: Odstranění řádků – jeden nebo více

### 3.1 Jak odstranit řádek (jediný řádek)

Pro odebrání jediného řádku zavolejte `DeleteRows(startIndex, count)`, kde `startIndex` je nulový index. Přeskočení řádku záhlaví (index 0) je běžné:

```csharp
        // Delete just the second row (index 1)
        table.DeleteRows(1, 1);
```

### 3.2 Delete multiple rows word – hromadné odstranění

Když potřebujete odstranit rozsah – například řádky 2‑6 – předáte počáteční index a počet řádků, které chcete smazat. Toto je vzor **delete multiple rows word**:

```csharp
        // Delete rows 2‑6 (skip header at index 0)
        // startIndex = 1 (second row), count = 5 rows
        table.DeleteRows(1, 5);
```

*Proč použít jeden volání?* Mazání řádků po jednom nutí tabulku přepočítat index po každém odstranění, což může být náchylné k chybám a pomalejší. Hromadná metoda udržuje interní strukturu tabulky konzistentní.

#### Okrajový případ: Mazání mimo velikost tabulky

Pokud `startIndex + count` přesáhne skutečný počet řádků, Aspose.Words vyhodí `ArgumentOutOfRangeException`. Ochranný kód vypadá takto:

```csharp
        int rowsToDelete = Math.Min(5, table.Rows.Count - 1); // never delete the header
        if (rowsToDelete > 0)
            table.DeleteRows(1, rowsToDelete);
```

Tento úryvek zajišťuje, že se nikdy nepokusíte smazat více řádků, než kolik existuje.

## Krok 4: Uložení upraveného dokumentu

Jakmile jsou řádky pryč, uložení změn je jediný řádek:

```csharp
        // Save the cleaned document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

Metoda `Save` automaticky zvolí formát podle přípony souboru, takže můžete výstup směřovat do PDF, HTML nebo dokonce ODT s jinou příponou.

## Kompletní funkční příklad

Spojením všech částí získáte kompletní, připravený k běhu program:

```csharp
using System;
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // 2️⃣ Access the first table (adjust index if needed)
        Table table = doc.FirstSection.Body.Tables[0];

        // 3️⃣ Delete rows 2‑6 (skip header row at index 0)
        //    This demonstrates delete multiple rows word in one call.
        if (table.Rows.Count > 1) // ensure there is at least a header + one data row
        {
            int rowsToDelete = Math.Min(5, table.Rows.Count - 1);
            table.DeleteRows(1, rowsToDelete);
        }

        // 4️⃣ Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");

        Console.WriteLine("Rows removed successfully. Output saved to output.docx");
    }
}
```

### Očekávaný výstup

- `output.docx` obsahuje původní tabulku **bez** řádků 2‑6.
- Všechny zbývající řádky se posunou nahoru, zachovají formátování buněk i šířky sloupců.
- Řádek záhlaví zůstane nedotčen, takže názvy sloupců zůstanou viditelné.

## Proč tento přístup převyšuje alternativy

| Přístup | Výhody | Nevýhody |
|----------|------|------|
| **Aspose.Words `DeleteRows`** | Jednořádkové hromadné mazání, zachovává styly, žádné COM závislosti | Vyžaduje komerční knihovnu (k dispozici zkušební verze) |
| Office Interop | Funguje s nativním Wordem | Vyžaduje instalaci Wordu na serveru, pomalé, problémy s úklidem COM |
| Open XML SDK | Zdarma, open source | Manuální manipulace s XML; bezpečné mazání řádků je obtížné |

Pokud už používáte Aspose.Words pro jiné úkoly s dokumenty, setrvání u `DeleteRows` udrží váš kód čistý a konzistentní.

## Pro tipy a časté úskalí

- **Pro tip:** Vždy nechte řádek záhlaví (index 0) nedotčený, pokud ho opravdu nechcete odstranit. Smazání záhlaví může rozbít následné zpracování, které očekává názvy sloupců.
- **Dejte pozor na sloučené buňky.** Pokud řádek obsahuje vertikálně sloučenou buňku, která zasahuje do řádku, který mažete, Aspose.Words automaticky upraví rozsah sloučení, ale vizuální výsledek vždy zkontrolujte.
- **Poznámka o výkonu:** Mazání velkého počtu řádků z masivní tabulky (tisíce řádků) je stále rychlé, ale pokud zpracováváte stovky dokumentů ve smyčce, zvažte opětovné použití objektu `Document`, kde je to možné, aby se snížila režie alokací.

## Často kladené otázky

**Q: Můžu mazat řádky na základě obsahu buňky místo indexu?**  
A: Rozhodně. Projděte `table.Rows`, podívejte se na `row.Cells[i].GetText()` a shromážděte odpovídající indexy. Pak zavolejte `DeleteRows` s nejmenším indexem a celkovým počtem, nebo mažte řádky v opačném pořadí, abyste se vyhnuli přepočítávání indexů.

**Q: Funguje to i s .doc soubory?**  
A: Ano. Aspose.Words podporuje jak `.doc`, tak `.docx`. Stačí změnit příponu v konstruktoru `Document` a volání `Save`.

**Q: Co když je tabulka uvnitř záhlaví/pati?**  
A: Získejte ji přes kolekci `doc.FirstSection.HeadersFooters` a použijte stejnou logiku `DeleteRows`.

## Závěr

Nyní máte solidní, end‑to‑end řešení pro **delete rows word table** pomocí C#. Příklad ukazuje *how to delete rows* jednotlivě i **delete multiple rows word** v jediném, efektivním volání. S Aspose.Words získáte čisté API, žádné COM komplikace a plnou kontrolu nad dokumenty Word.

Jste připraveni na další výzvu? Zkuste přidat nový řádek s vypočtenými součty, nebo exportujte oříznutou tabulku do CSV pomocí `Table.ToTxt`. Možnosti jsou neomezené, když ovládáte manipulaci s tabulkami.

Šťastné programování a ať jsou vaše tabulky Word vždy úhledné!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vlastních projektech.

- [Jak odstranit řádky v Excelu pomocí Aspose.Cells pro Java | Průvodce a tutoriál](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [Jak odstranit prázdné řádky v Excelu pomocí Aspose.Cells .NET pro čištění dat](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)
- [Jak vložit a odstranit řádky v Excelu s Aspose.Cells pro .NET: Kompletní průvodce](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}