---
title: Rozdělit Panely Listu
linktitle: Rozdělit Panely Listu
second_title: Aspose.Cells for .NET API Reference
description: Naučte se, jak rozdělit panely listů v Aspose.Cells pro .NET pomocí našeho podrobného průvodce. Vylepšete navigaci v souborech Excel pomocí tohoto jednoduchého návodu.
weight: 130
url: /cs/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozdělit Panely Listu

## Zavedení

Jste připraveni rozdělit podokna listu aplikace Excel pomocí Aspose.Cells for .NET? Představte si toto: máte obrovský excelový list a už vás nebaví neustále se posouvat zpět k záhlavím, abyste si vzpomněli, se kterým sloupcem pracujete. Zadejte "Rozdělit panely". Tato užitečná funkce vám umožňuje zmrazit část listu, což výrazně usnadňuje navigaci. Ať už pracujete s finančními daty, správou zásob nebo rozsáhlými datovými sadami, rozdělení panelů může zvýšit vaši produktivitu desetkrát. 

## Předpoklady

Než začneme rozdělovat panely jako průvodce tabulkovým procesorem, udělejme si správné nastavení. Zde je to, co budete potřebovat:

-  Aspose.Cells for .NET: Ujistěte se, že jste si jej stáhli a nainstalovali. Pokud ještě nemáte, vezměte si to[zde](https://releases.aspose.com/cells/net/).
- .NET Framework: Tato příručka předpokládá, že pracujete v prostředí .NET.
- Sešit aplikace Excel: Použijeme vzorový soubor aplikace Excel, abychom ukázali, jak tato funkce funguje.
-  Dočasná nebo úplná licence: Aspose.Cells vyžaduje licenci. Pokud to jen zkoušíte, pořiďte si[dočasná licence zdarma](https://purchase.aspose.com/temporary-license/) abyste se vyhnuli omezením hodnocení.

## Importujte balíčky

Než se vrhneme na kód, nejprve naimportujeme potřebné jmenné prostory. Bez těchto zahrnutí nemůžete v Aspose.Cells dělat nic.

```csharp
using System.IO;
using Aspose.Cells;
```

Nyní, když jsme probrali to podstatné, přejděme k té vzrušující části – dělení tabulí!

## Krok 1: Vytvořte sešit

 Prvním krokem v tomto procesu je vytvoření a`Workbook` objekt, který bude reprezentovat soubor Excel, který chcete upravit. V tomto případě načteme soubor z adresáře. Toto je vaše plátno, list Excelu, na kterém budete kouzlit.

Než budeme moci rozdělit panely, potřebujeme sešit, se kterým budeme pracovat! Tento krok je stejně nezbytný jako otevření knihy, než ji začnete číst.

```csharp
// Cesta k adresáři dokumentů
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Vytvořte instanci nového sešitu a otevřete soubor šablony
Workbook book = new Workbook(dataDir + "Book1.xls");
```

 Ve výše uvedeném kódu nahraďte`"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou, kde se nachází váš soubor Excel. The`Workbook`třída načte soubor Excel do paměti.

## Krok 2: Nastavte aktivní buňku

 Po načtení sešitu je čas nastavit aktivní buňku. Z hlediska Excelu je aktivní buňka ta, která je aktuálně vybraná nebo aktivní. V tomto tutoriálu vybereme buňku`A20` v prvním pracovním listu.

Nastavení aktivní buňky je zásadní, protože rozdělení podokna začíná od této aktivní buňky. Je to jako vybírat si, kde uděláte první řez v pizze – vyberte si svůj plátek!

```csharp
// Nastavte aktivní buňku
book.Worksheets[0].ActiveCell = "A20";
```

 Tento kus kódu vytváří`A20` aktivní buňku. Je to důležité, protože k rozdělení dochází kolem tohoto bodu, stejně jako se vaše navigace v Excelu často soustředí kolem konkrétní buňky.

## Krok 3: Rozdělte pracovní list

Nyní, když je aktivní buňka nastavena, přejděme k zábavnější části – rozdělení listu! V tomto kroku se stane kouzlo. Pro snadnější prohlížení a navigaci budete moci list rozdělit do několika podoken.

Toto je jádro celého tutoriálu. Rozdělením listu vytvoříte samostatná podokna, která vám umožní procházet různými sekcemi listu aplikace Excel, aniž byste ztratili ze zřetele záhlaví nebo jiné důležité oblasti.

```csharp
// Rozdělte okno listu
book.Worksheets[0].Split();
```

 s`Split()` říkáte Aspose.Cells, aby rozdělil list v aktivní buňce (`A20` v tomto případě). Od tohoto okamžiku Excel vytvoří v listu rozdělení, které odděluje podokna, abyste mohli procházet nezávisle.

## Krok 4: Uložte sešit

Po rozdělení podoken už zbývá jen uložit práci. Tento poslední krok zajistí, že se vaše změny uloží do zadaného výstupního souboru.

K čemu je všechna vaše dřina, když si ji neušetříte? Úspora zajišťuje, že vaše krásně rozdělené tabule zůstanou neporušené pro budoucí použití.

```csharp
// Uložte soubor aplikace Excel
book.Save(dataDir + "output.xls");
```

 Tady,`Save()` metoda uloží sešit s nově rozdělenými panely do výstupního souboru aplikace Excel. Změny, které jste provedli, jsou nyní připraveny k použití vy nebo kdokoli jiný.

## Závěr

tady to máte! Právě jste se naučili, jak rozdělit podokna v listu aplikace Excel pomocí Aspose.Cells for .NET. Už žádné nekonečné posouvání nebo ztráta přehledu o vašich datech. Díky této metodě je manipulace s velkými soubory aplikace Excel mnohem méně zahlcující a mnohem efektivnější. Díky možnosti rozdělit panely můžete nyní sledovat kritické datové body při práci se složitými tabulkami.

## FAQ

### Mohu rozdělit více než dva panely?  
 Ano, list můžete rozdělit do více podoken zadáním různých aktivních buněk a voláním`Split()` metoda.

### Jaký je rozdíl mezi dělicími tabulemi a mrazicími tabulemi?  
Rozdělení panelů umožňuje posouvat se v obou panelech nezávisle. Ukotvení podoken uzamkne záhlaví nebo konkrétní řádky/sloupce, aby zůstaly viditelné při posouvání.

### Mohu rozštěp odstranit po jeho aplikaci?  
Ano, rozdělení můžete odstranit zavřením a opětovným otevřením sešitu nebo jeho programovým resetem.

### Fungují rozdělovací panely stejně pro různé formáty souborů Excel (XLS, XLSX)?  
 Ano,`Split()` metoda funguje pro formáty XLS i XLSX.

### Mohu používat Aspose.Cells bez licence?  
 Ano, ale přichází to s omezeními. Pro plnohodnotný zážitek je nejlepší použít a[dočasný](https://purchase.aspose.com/temporary-license/) nebo[placenou licenci](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
