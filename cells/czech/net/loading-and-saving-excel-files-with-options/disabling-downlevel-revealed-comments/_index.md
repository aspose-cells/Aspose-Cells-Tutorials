---
"description": "Naučte se, jak zakázat odhalené komentáře nižší úrovně při ukládání sešitu aplikace Excel do HTML pomocí Aspose.Cells pro .NET v tomto podrobném návodu krok za krokem."
"linktitle": "Zakázání odhalených komentářů nižší úrovně při ukládání do HTML"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Zakázání odhalených komentářů nižší úrovně při ukládání do HTML"
"url": "/cs/net/loading-and-saving-excel-files-with-options/disabling-downlevel-revealed-comments/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zakázání odhalených komentářů nižší úrovně při ukládání do HTML

## Zavedení
Potřebovali jste někdy převést sešit aplikace Excel do formátu HTML a chtěli jste se ujistit, že se během procesu nezobrazí žádné zbytečné komentáře ani skrytý obsah? V takovém případě se hodí zakázání odhalených komentářů nižší úrovně. Pokud používáte Aspose.Cells pro .NET, máte plnou kontrolu nad tím, jak se vaše sešity aplikace Excel vykreslují jako soubory HTML. V tomto tutoriálu vás provedeme jednoduchým podrobným návodem, který vám pomůže zakázat odhalené komentáře nižší úrovně při ukládání sešitu do formátu HTML. 
Do konce tohoto článku budete mít jasnou představu o tom, jak tuto funkci používat a jak zajistit, aby váš HTML výstup byl čistý a bez komentářů.
## Předpoklady
Než se pustíme do podrobného návodu, pojďme si probrat několik věcí, které budete potřebovat k hladkému průběhu:
1. Aspose.Cells pro .NET: Budete muset mít nainstalovanou knihovnu Aspose.Cells. Pokud ji ještě nemáte nainstalovanou, můžete si ji stáhnout. [zde](https://releases.aspose.com/cells/net/).
2. IDE: Vývojové prostředí, jako je Visual Studio, pro psaní a spouštění kódu v C#.
3. Základní znalost C#: Znalost syntaxe C# a objektově orientovaného programování vám pomůže sledovat kód.
4. Dočasná nebo licencovaná verze: Můžete buď využít bezplatnou zkušební verzi, nebo požádat o dočasnou licenci od [zde](https://purchase.aspose.com/temporary-license/)Díky tomu knihovna funguje bez jakýchkoli omezení.
Teď, když jste připraveni, pojďme se rovnou do toho pustit!
## Importovat jmenné prostory
Než se pustíme do příkladů kódu, je nezbytné zahrnout potřebné jmenné prostory pro Aspose.Cells. Bez nich váš kód nebude mít přístup k metodám a vlastnostem potřebným pro manipulaci s excelovými soubory.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ujistěte se, že tento řádek umístíte na začátek souboru C#, abyste importovali jmenný prostor Aspose.Cells.
## Krok 1: Nastavení cest k adresářům
Především musíme nastavit zdrojový adresář (kam bude uložen váš soubor Excel) a výstupní adresář (kam bude uložen váš soubor HTML). To je zásadní, protože Aspose.Cells vyžaduje přesné cesty k souborům pro přístup k souborům a jejich ukládání.
```csharp
// Zdrojový adresář, kde se nachází váš soubor Excel
string sourceDir = "Your Document Directory";
// Výstupní adresář, kam bude uložen výsledný HTML soubor
string outputDir = "Your Document Directory";
```
V tomto kroku nahraďte `"Your Document Directory"` se skutečnými cestami k souborům ve vašem systému. Můžete si také vytvořit vlastní adresáře pro lepší organizaci vstupních a výstupních souborů.
## Krok 2: Načtení sešitu aplikace Excel
V tomto kroku načteme sešit aplikace Excel do paměti, abychom s ním mohli manipulovat. Pro demonstrační účely použijeme ukázkový soubor s názvem `"sampleDisableDownlevelRevealedComments.xlsx"`Můžete použít libovolný sešit.
```csharp
// Načtěte ukázkový sešit ze zdrojového adresáře
Workbook wb = new Workbook(sourceDir + "sampleDisableDownlevelRevealedComments.xlsx");
```
Tím se vytvoří objekt Workbook, který obsahuje všechna data a strukturu vašeho souboru aplikace Excel. Odtud jej můžete upravovat, aplikovat nastavení a nakonec jej uložit v jiném formátu.
## Krok 3: Nastavení možností ukládání HTML
Nyní musíme nakonfigurovat objekt HtmlSaveOptions tak, aby zakázal zobrazování komentářů nižší úrovně. Tato možnost zajistí, že žádné komentáře ani skrytý obsah nebudou ve výsledném souboru HTML zobrazeny.
```csharp
// Vytvořte nový objekt HtmlSaveOptions pro konfiguraci možností ukládání.
HtmlSaveOptions opts = new HtmlSaveOptions();
// Zakázat komentáře odhalené nižší úrovní
opts.DisableDownlevelRevealedComments = true;
```
Nastavením `DisableDownlevelRevealedComments` na `true`, zajistíte, že při uložení sešitu jako souboru HTML budou zakázány všechny komentáře nižší úrovně.
## Krok 4: Uložení sešitu ve formátu HTML
Jakmile je objekt HtmlSaveOptions nakonfigurován, dalším krokem je uložení sešitu do HTML s použitím zadaných možností. Zde probíhá skutečná konverze souboru.
```csharp
// Uložit sešit jako soubor HTML se zadanými možnostmi uložení
wb.Save(outputDir + "outputDisableDownlevelRevealedComments_true.html", opts);
```
V tomto řádku kódu ukládáme sešit do výstupního adresáře, který jste zadali dříve, a používáme nastavení DisableDownlevelRevealedComments. Výsledkem bude čistý soubor HTML bez nežádoucích komentářů.
## Krok 5: Ověření a spuštění
Nakonec, abyste se ujistili, že vše fungovalo podle očekávání, můžete do konzole vypsat zprávu o úspěchu.
```csharp
// Vypsat zprávu o úspěchu do konzole
Console.WriteLine("DisableDownlevelRevealedCommentsWhileSavingToHTML executed successfully.");
```
Díky tomu víte, že operace proběhla bez chyb.
## Závěr
A tady to máte! Úspěšně jste se naučili, jak zakázat odhalení komentářů nižší úrovně při ukládání sešitu aplikace Excel do HTML pomocí Aspose.Cells pro .NET. Díky této funkci nyní můžete ovládat, jak se vaše sešity vykreslují jako HTML, a vyhnout se odhalení jakéhokoli nepotřebného obsahu. Ať už vyvíjíte webovou aplikaci, nebo jednoduše potřebujete čistý výstup HTML, tato metoda zajistí, že konverze vašich sešitů budou přesné a bezpečné.
Pokud vám tento tutoriál pomohl, zvažte prozkoumání dalších funkcí Aspose.Cells, které vám pomohou dále vylepšit vaše možnosti zpracování v Excelu.
## Často kladené otázky
### Co jsou to komentáře odhalené na nižší úrovni?
Odhalené komentáře nižší úrovně se obvykle používají ve vývoji webových stránek k poskytnutí dalších informací pro starší prohlížeče, které nepodporují určité funkce HTML. Při převodech z Excelu do HTML mohou někdy odhalit skrytý obsah nebo komentáře, a proto může být jejich zakázání užitečné.
### Mohu povolit komentáře nižší úrovně, pokud je potřebuji?
Ano, jednoduše nastavte `DisableDownlevelRevealedComments` majetek `false` Pokud chcete při ukládání sešitu ve formátu HTML povolit komentáře nižší úrovně.
### Jak získám dočasnou licenci pro Aspose.Cells?
O dočasnou licenci si můžete snadno požádat na adrese [Webové stránky Aspose](https://purchase.aspose.com/temporary-license/).
### Ovlivňuje zakázání komentářů nižší úrovně vzhled HTML?
Ne, zakázání odhalených komentářů nižší úrovně neovlivní vizuální vzhled HTML výstupu. Pouze zabrání zobrazení dodatečných informací určených pro starší prohlížeče.
### Mohu sešit uložit i v jiných formátech než HTML?
Ano, Aspose.Cells podporuje různé výstupní formáty, jako například PDF, CSV a TXT. Další možnosti si můžete prohlédnout v [dokumentace](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}