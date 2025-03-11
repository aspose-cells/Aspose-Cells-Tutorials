---
title: Exportujte hodnotu řetězce HTML buněk do DataTable v Excelu
linktitle: Exportujte hodnotu řetězce HTML buněk do DataTable v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se exportovat hodnoty řetězce HTML z buněk aplikace Excel do tabulky DataTable pomocí Aspose.Cells for .NET v jednoduchém podrobném tutoriálu.
weight: 11
url: /cs/net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportujte hodnotu řetězce HTML buněk do DataTable v Excelu

## Zavedení

Při práci se soubory aplikace Excel v prostředí .NET můžete zjistit, že potřebujete extrahovat informace z buněk nejen jako prostý text, ale spíše jako řetězce HTML. To může být docela užitečné, když pracujete s daty ve formátu RTF nebo když chcete zachovat formátování. V této příručce vás provedu exportem hodnoty řetězce HTML buněk do tabulky DataTable pomocí Aspose.Cells for .NET. 

## Předpoklady

Než se ponoříte do kódu, ujistěte se, že máte vše, co potřebujete. Zde je rychlý kontrolní seznam:

1. Základní znalost C# a .NET: Než se pustíte do kódování, ujistěte se, že jste obeznámeni s programováním v C# a se základy .NET frameworku.
2.  Aspose.Cells for .NET: Pokud jste to ještě neudělali, musíte nainstalovat Aspose.Cells for .NET. Bezplatnou zkušební verzi si můžete stáhnout z[zde](https://releases.aspose.com/).
3. Visual Studio nebo IDE dle vašeho výběru: Nastavte své prostředí pro psaní kódu C#. Visual Studio se doporučuje pro jeho širokou škálu funkcí a snadné použití.
4. Vzorový soubor Excel: Budete potřebovat vzorový soubor Excel (`sampleExportTableAsHtmlString.xlsx`) pracovat. Ujistěte se, že je umístěn v adresáři, který je přístupný.
5. NuGet Package Manager: Ujistěte se, že máte ve svém projektu přístup k NuGet Package Manager, abyste mohli snadno přidat knihovnu Aspose.Cells.

Když máme tyto předpoklady pod kontrolou, ušpiněme si ruce nějakým kódováním!

## Importujte balíčky

Než začneme pracovat s Aspose.Cells, musíme naimportovat potřebné balíčky. To obvykle zahrnuje přidání balíčku Aspose.Cells NuGet do vašeho projektu. Jak na to:

### Otevřete Správce balíčků NuGet

V aplikaci Visual Studio klikněte pravým tlačítkem na svůj projekt v Průzkumníku řešení a vyberte Spravovat balíčky NuGet.

### Vyhledejte Aspose.Cells

 Ve Správci balíčků NuGet zadejte`Aspose.Cells` ve vyhledávací liště.

### Nainstalujte balíček

Jakmile najdete Aspose.Cells, klikněte na tlačítko Instalovat. Tím se knihovna přidá do vašeho projektu a umožní vám ji importovat do vašeho kódu.

### Importujte jmenný prostor

Přidejte následující direktivu using v horní části souboru kódu:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

Nyní, když jsme vše nastavili, pojďme se vrhnout na podrobný proces exportu hodnot řetězce HTML ze souboru aplikace Excel do tabulky DataTable. 

## Krok 1: Definujte zdrojový adresář

Začnete definováním adresáře, kde je uložen váš vzorový soubor Excel. To je zásadní, protože to říká vaší aplikaci, kde má soubor najít. Zde je kód:

```csharp
string sourceDir = "Your Document Directory";
```

 Nezapomeňte vyměnit`"Your Document Directory"` se skutečnou cestou k souboru Excel.

## Krok 2: Načtěte ukázkový soubor Excel

 Dalším krokem je načtení sešitu aplikace Excel. Budete používat`Workbook` třídy z Aspose.Cells. Soubor můžete načíst takto:

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

Tento jednoduchý řádek kódu inicializuje sešit a načte zadaný soubor aplikace Excel.

## Krok 3: Otevřete první pracovní list

Po načtení sešitu budete chtít získat přístup ke konkrétnímu listu, který obsahuje data, která vás zajímají. Obecně platí, že začnete prvním listem:

```csharp
Worksheet ws = wb.Worksheets[0];
```

Zde pracujeme s prvním listem (index 0). Ujistěte se, že jsou vaše data na správném listu.

## Krok 4: Zadejte možnosti exportu tabulky

Chcete-li ovládat, jak se data exportují, musíte nastavit`ExportTableOptions`. V tomto případě chcete zajistit, aby se názvy sloupců neexportovaly, a chcete exportovat data buněk jako řetězce HTML:

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

Tato konfigurace vám umožňuje zachovat bohaté formátování dat buněk při exportu.

## Krok 5: Export buněk do DataTable

 Nyní přichází zásadní část, kdy data skutečně exportujete. Pomocí`ExportDataTable` můžete vytáhnout data z listu do a`DataTable`. Postup:

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

Tento kód exportuje zadaný rozsah buněk (od řádku 0, sloupce 0 do řádku 3, sloupce 3) do DataTable pomocí možností zadaných dříve.

## Krok 6: Vytiskněte hodnotu řetězce HTML

Nakonec si vytiskneme hodnotu řetězce HTML z konkrétní buňky v DataTable, abychom viděli, co se nám podařilo exportovat. Pokud například chcete vytisknout hodnotu ze třetího řádku a druhého sloupce, postupujte takto:

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

Tento řádek vytiskne požadovaný řetězec HTML z DataTable do konzoly. 

## Závěr 

A tady to máte! Úspěšně jste exportovali hodnoty řetězce HTML z buněk v souboru aplikace Excel do DataTable pomocí Aspose.Cells for .NET. Tato schopnost nejen obohatí vaše dovednosti manipulace s daty, ale také rozšiřuje vaše možnosti při práci s formátovaným obsahem přímo ze souborů aplikace Excel. 

## FAQ

### Mohu použít Aspose.Cells pro jiné formáty souborů než Excel?  
Ano, Aspose.Cells je primárně pro Excel, ale Aspose nabízí další knihovny pro různé formáty.

### Potřebuji licenci pro Aspose.Cells?  
 Ano, pro produkční použití je vyžadována platná licence. Můžete získat dočasnou licenci[zde](https://purchase.aspose.com/temporary-license/).

### Co když můj soubor Excel obsahuje vzorce? Budou exportovat správně?  
Ano, Aspose.Cells si poradí se vzorci a při exportu se vyhodnotí na výsledné hodnoty.

### Je možné změnit možnosti exportu?  
 Absolutně! Můžete přizpůsobit`ExportTableOptions` aby vyhovoval vašim konkrétním potřebám.

### Kde najdu podrobnější dokumentaci k Aspose.Cells?  
 Můžete najít rozsáhlou dokumentaci[zde](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
