---
title: Zakázání Odhalených komentářů nižší úrovně při ukládání do HTML
linktitle: Zakázání Odhalených komentářů nižší úrovně při ukládání do HTML
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak deaktivovat odhalené komentáře nižší úrovně při ukládání sešitu aplikace Excel do HTML pomocí Aspose.Cells for .NET, pomocí tohoto podrobného průvodce krok za krokem.
weight: 11
url: /cs/net/loading-and-saving-excel-files-with-options/disabling-downlevel-revealed-comments/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zakázání Odhalených komentářů nižší úrovně při ukládání do HTML

## Zavedení
Potřebovali jste někdy převést excelový sešit do HTML a chtěli jste zajistit, aby během procesu nebyly odhaleny žádné zbytečné komentáře nebo skrytý obsah? Zde se hodí deaktivace odhalených komentářů nižší úrovně. Pokud používáte Aspose.Cells pro .NET, máte plnou kontrolu nad tím, jak se sešity aplikace Excel vykreslují jako soubory HTML. V tomto tutoriálu vás provedeme jednoduchým průvodcem krok za krokem, který vám pomůže zakázat odhalené komentáře nižší úrovně při ukládání sešitu do HTML. 
Na konci tohoto článku budete mít jasno v tom, jak tuto funkci používat, a zajistit, aby byl váš výstup HTML čistý a bez komentářů.
## Předpoklady
Než se ponoříme do podrobného průvodce, pojďme si pokrýt pár věcí, které budete muset mít na místě, abyste mohli plynule pokračovat:
1. Aspose.Cells for .NET: Budete muset mít nainstalovanou knihovnu Aspose.Cells. Pokud jste jej ještě nenainstalovali, můžete si jej stáhnout[zde](https://releases.aspose.com/cells/net/).
2. IDE: Vývojové prostředí jako Visual Studio pro psaní a spouštění vašeho kódu C#.
3. Základní znalost C#: Znalost syntaxe C# a objektově orientovaného programování vám pomůže sledovat kód.
4.  Dočasná nebo licencovaná verze: Můžete buď použít bezplatnou zkušební verzi, nebo požádat o dočasnou licenci od[zde](https://purchase.aspose.com/temporary-license/). To zajišťuje, že knihovna funguje bez jakýchkoliv omezení.
Nyní, když jste připraveni, pojďme se do toho pustit!
## Importovat jmenné prostory
Než se pustíme do příkladů kódu, je nezbytné zahrnout potřebné jmenné prostory pro Aspose.Cells. Bez nich váš kód nebude mít přístup k metodám a vlastnostem požadovaným pro manipulaci se soubory Excel.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ujistěte se, že jste tento řádek umístili na začátek souboru C#, abyste importovali jmenný prostor Aspose.Cells.
## Krok 1: Nastavte cesty k adresáři
Nejprve musíme nastavit zdrojový adresář (kde je uložen váš soubor Excel) a výstupní adresář (kam bude uložen váš soubor HTML). To je zásadní, protože Aspose.Cells vyžaduje přesné cesty k souborům pro přístup a ukládání souborů.
```csharp
// Zdrojový adresář, kde se nachází váš soubor Excel
string sourceDir = "Your Document Directory";
// Výstupní adresář, kam bude uložen výsledný HTML soubor
string outputDir = "Your Document Directory";
```
 V tomto kroku vyměňte`"Your Document Directory"` se skutečnými cestami k souborům ve vašem systému. Můžete také vytvořit vlastní adresáře pro lepší uspořádání vstupních a výstupních souborů.
## Krok 2: Načtěte sešit aplikace Excel
 V tomto kroku načteme sešit aplikace Excel do paměti, abychom s ním mohli manipulovat. Pro demonstrační účely použijeme ukázkový soubor s názvem`"sampleDisableDownlevelRevealedComments.xlsx"`. Můžete použít jakýkoli sešit, který preferujete.
```csharp
// Načtěte ukázkový sešit ze zdrojového adresáře
Workbook wb = new Workbook(sourceDir + "sampleDisableDownlevelRevealedComments.xlsx");
```
Tím se vytvoří objekt Workbook, který obsahuje všechna data a strukturu vašeho souboru Excel. Odtud jej můžete upravit, použít nastavení a nakonec uložit v jiném formátu.
## Krok 3: Nastavte možnosti uložení HTML
Nyní musíme nakonfigurovat objekt HtmlSaveOptions, aby zakázal odhalené komentáře nižší úrovně. Tato možnost zajišťuje, že ve výsledném souboru HTML nebudou odhaleny žádné komentáře nebo skrytý obsah.
```csharp
// Vytvořte nový objekt HtmlSaveOptions pro konfiguraci možností uložení
HtmlSaveOptions opts = new HtmlSaveOptions();
// Zakázat odhalené komentáře nižší úrovně
opts.DisableDownlevelRevealedComments = true;
```
 Nastavením`DisableDownlevelRevealedComments` na`true`, zajistíte, že když uložíte sešit jako soubor HTML, všechny komentáře nižší úrovně budou zakázány.
## Krok 4: Uložte sešit jako HTML
Po nakonfigurování objektu HtmlSaveOptions je dalším krokem uložení sešitu do HTML pomocí zadaných možností. Zde dochází ke skutečné konverzi souborů.
```csharp
// Uložte sešit jako soubor HTML se zadanými možnostmi uložení
wb.Save(outputDir + "outputDisableDownlevelRevealedComments_true.html", opts);
```
V tomto řádku kódu ukládáme sešit do výstupního adresáře, který jste zadali dříve, a aplikujeme nastavení DisableDownlevelRevealedComments. Výsledkem bude čistý HTML soubor bez nežádoucích komentářů.
## Krok 5: Ověřte a spusťte
Nakonec, abyste zajistili, že vše fungovalo podle očekávání, můžete odeslat zprávu o úspěchu do konzoly.
```csharp
// Odešlete zprávu o úspěchu do konzoly
Console.WriteLine("DisableDownlevelRevealedCommentsWhileSavingToHTML executed successfully.");
```
To vám dává vědět, že operace proběhla bez chyb.
## Závěr
A tady to máte! Úspěšně jste se naučili, jak zakázat odhalené komentáře nižší úrovně při ukládání sešitu aplikace Excel do HTML pomocí Aspose.Cells for .NET. Pomocí této funkce nyní můžete řídit, jak se sešity vykreslují jako HTML, a vyhnout se odhalení jakéhokoli zbytečného obsahu. Ať už vyvíjíte webovou aplikaci nebo prostě potřebujete čistý výstup HTML, tato metoda zajistí, že převody sešitu budou přesné a bezpečné.
Pokud vám tento návod pomohl, zvažte prozkoumání dalších funkcí Aspose.Cells, abyste dále vylepšili své možnosti zpracování Excelu.
## FAQ
### Co jsou odhalené komentáře nižší úrovně?
Odhalené komentáře nižší úrovně se obvykle používají při vývoji webu k poskytování dalších informací pro starší prohlížeče, které nepodporují určité funkce HTML. V převodech Excel do HTML mohou někdy odhalit skrytý obsah nebo komentáře, a proto může být užitečné je zakázat.
### Mohu povolit komentáře nižší úrovně, pokud je potřebuji?
 Ano, stačí nastavit`DisableDownlevelRevealedComments` majetek do`false` pokud chcete povolit komentáře nižší úrovně při ukládání sešitu jako HTML.
### Jak získám dočasnou licenci pro Aspose.Cells?
 Můžete snadno požádat o dočasnou licenci na adrese[Aspose webové stránky](https://purchase.aspose.com/temporary-license/).
### Ovlivňuje zakázání komentářů nižší úrovně vzhled kódu HTML?
Ne, deaktivace odhalených komentářů nižší úrovně neovlivní vizuální vzhled výstupu HTML. Zabraňuje pouze vystavení dalších informací určených pro starší prohlížeče.
### Mohu uložit sešit v jiných formátech než HTML?
 Ano, Aspose.Cells podporuje různé výstupní formáty, jako je PDF, CSV a TXT. Další možnosti můžete prozkoumat v[dokumentace](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
