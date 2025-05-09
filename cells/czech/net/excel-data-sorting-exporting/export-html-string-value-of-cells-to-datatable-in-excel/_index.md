---
"description": "Naučte se, jak exportovat řetězcové hodnoty HTML z buněk aplikace Excel do DataTable pomocí Aspose.Cells pro .NET v jednoduchém podrobném tutoriálu."
"linktitle": "Export HTML řetězcových hodnot buněk do DataTable v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Export HTML řetězcových hodnot buněk do DataTable v Excelu"
"url": "/cs/net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Export HTML řetězcových hodnot buněk do DataTable v Excelu

## Zavedení

Při práci se soubory Excelu v prostředí .NET se může stát, že budete potřebovat extrahovat informace z buněk, a to nejen jako prostý text, ale spíše jako řetězce HTML. To může být docela užitečné, pokud pracujete s daty ve formátu RTF nebo pokud chcete zachovat formátování. V této příručce vás provedu exportem hodnot řetězce HTML z buněk do DataTable pomocí Aspose.Cells pro .NET. 

## Předpoklady

Než se pustíme do kódu, ujistěte se, že máte vše potřebné připravené. Zde je stručný kontrolní seznam:

1. Základní znalost C# a .NET: Než se pustíte do programování, ujistěte se, že znáte programování v C# a základy frameworku .NET.
2. Aspose.Cells pro .NET: Pokud jste tak ještě neučinili, musíte si nainstalovat Aspose.Cells pro .NET. Bezplatnou zkušební verzi si můžete stáhnout z [zde](https://releases.aspose.com/).
3. Visual Studio nebo IDE dle vašeho výběru: Nastavte si prostředí pro psaní kódu C#. Visual Studio se doporučuje pro širokou škálu funkcí a snadné použití.
4. Ukázkový soubor Excel: Budete potřebovat ukázkový soubor Excel (`sampleExportTableAsHtmlString.xlsx`) s nímž chcete pracovat. Ujistěte se, že je umístěn v adresáři, který je přístupný.
5. Správce balíčků NuGet: Ujistěte se, že máte ve svém projektu přístup ke Správci balíčků NuGet, abyste mohli snadno přidat knihovnu Aspose.Cells.

S těmito předpoklady pod kontrolou se pojďme pustit do programování!

## Importovat balíčky

Než začneme pracovat s Aspose.Cells, musíme importovat potřebné balíčky. To obvykle zahrnuje přidání NuGet balíčku Aspose.Cells do vašeho projektu. Zde je návod, jak to udělat:

### Otevřete Správce balíčků NuGet

V aplikaci Visual Studio klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení a vyberte možnost Spravovat balíčky NuGet.

### Hledat Aspose.Cells

Ve Správci balíčků NuGet zadejte `Aspose.Cells` ve vyhledávacím řádku.

### Nainstalujte balíček

Jakmile najdete Aspose.Cells, klikněte na tlačítko Instalovat. Tím se knihovna přidá do vašeho projektu a umožní vám ji importovat do kódu.

### Importovat jmenný prostor

Přidejte následující direktivu using na začátek souboru s kódem:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

Nyní, když máme vše nastavené, se pojďme ponořit do podrobného procesu exportu řetězcových hodnot HTML ze souboru aplikace Excel do datové tabulky (DataTable). 

## Krok 1: Definování zdrojového adresáře

Začnete definováním adresáře, kde je uložen váš vzorový soubor Excelu. To je klíčové, protože to vaší aplikaci říká, kde má soubor najít. Zde je kód pro tento účel:

```csharp
string sourceDir = "Your Document Directory";
```

Nezapomeňte vyměnit `"Your Document Directory"` se skutečnou cestou k vašemu souboru aplikace Excel.

## Krok 2: Načtěte ukázkový soubor Excel

Dalším krokem je načtení sešitu aplikace Excel. Použijete `Workbook` třída z Aspose.Cells, která to udělá. Soubor načtete takto:

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

Tento jednoduchý řádek kódu inicializuje sešit a načte zadaný soubor aplikace Excel.

## Krok 3: Přístup k prvnímu pracovnímu listu

Jakmile je sešit načten, budete chtít přistupovat ke konkrétnímu listu, který obsahuje data, která vás zajímají. Obecně začnete s prvním listem:

```csharp
Worksheet ws = wb.Worksheets[0];
```

Zde pracujeme s prvním listem (index 0). Ujistěte se, že vaše data jsou na správném listu.

## Krok 4: Zadejte možnosti exportu tabulky

Chcete-li ovládat způsob exportu dat, je třeba nastavit `ExportTableOptions`tomto případě chcete zajistit, aby názvy sloupců nebyly exportovány, a chcete, aby data buněk byla exportována jako řetězce HTML:

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

Tato konfigurace umožňuje zachovat bohaté formátování dat buněk při exportu.

## Krok 5: Export buněk do DataTable

Nyní přichází klíčová část, kdy data skutečně exportujete. Pomocí `ExportDataTable` metodu, můžete data z listu načíst do `DataTable`Zde je návod, jak to udělat:

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

Tento kód exportuje zadaný rozsah buněk (od řádku 0, sloupce 0 do řádku 3, sloupce 3) do objektu DataTable s použitím dříve zadaných možností.

## Krok 6: Výpis hodnoty řetězce HTML

Nakonec si vytiskněme hodnotu HTML řetězce z konkrétní buňky v tabulce DataTable, abychom viděli, co se nám podařilo exportovat. Pokud například chcete vytisknout hodnotu ze třetího řádku a druhého sloupce, postupujte takto:

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

Tento řádek vypíše požadovaný řetězec HTML z DataTable do konzole. 

## Závěr 

tady to máte! Úspěšně jste exportovali řetězcové hodnoty HTML z buněk v souboru aplikace Excel do datové tabulky pomocí Aspose.Cells pro .NET. Tato funkce nejen obohacuje vaše dovednosti v oblasti manipulace s daty, ale také rozšiřuje vaše možnosti při práci s formátovaným obsahem přímo z souborů aplikace Excel. 

## Často kladené otázky

### Mohu použít Aspose.Cells pro jiné formáty souborů než Excel?  
Ano, Aspose.Cells je primárně pro Excel, ale Aspose nabízí i další knihovny pro různé formáty.

### Potřebuji licenci pro Aspose.Cells?  
Ano, pro produkční použití je vyžadována platná licence. Můžete získat dočasnou licenci. [zde](https://purchase.aspose.com/temporary-license/).

### Co když můj soubor Excelu obsahuje vzorce? Budou exportovány správně?  
Ano, Aspose.Cells umí pracovat se vzorci a při exportu budou vyhodnoceny na výsledné hodnoty.

### Je možné změnit možnosti exportu?  
Rozhodně! Můžete si to přizpůsobit `ExportTableOptions` aby vyhovovaly vašim specifickým potřebám.

### Kde najdu podrobnější dokumentaci k Aspose.Cells?  
Rozsáhlou dokumentaci najdete [zde](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}