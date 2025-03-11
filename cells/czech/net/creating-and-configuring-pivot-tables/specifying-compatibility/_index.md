---
title: Určete kompatibilitu souboru aplikace Excel programově v .NET
linktitle: Určete kompatibilitu souboru aplikace Excel programově v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se manipulovat s kontingenčními tabulkami Excelu pomocí Aspose.Cells pro .NET, včetně aktualizací dat, nastavení kompatibility a formátování buněk.
weight: 23
url: /cs/net/creating-and-configuring-pivot-tables/specifying-compatibility/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Určete kompatibilitu souboru aplikace Excel programově v .NET

## Zavedení

dnešním světě založeném na datech se pro mnoho vývojářů stala programová správa a manipulace se soubory Excelu zásadní. Pokud pracujete s Excelem v .NET, Aspose.Cells je výkonná knihovna, která usnadňuje vytváření, čtení, úpravy a ukládání souborů Excel. Jedna důležitá funkce této knihovny umožňuje určit kompatibilitu souborů aplikace Excel programově. V tomto tutoriálu prozkoumáme, jak manipulovat se soubory aplikace Excel, zejména se zaměřením na správu kompatibility pomocí Aspose.Cells for .NET. Nakonec pochopíte, jak nastavit kompatibilitu pro soubory aplikace Excel, zejména pro kontingenční tabulky, při obnovování a správě dat.

## Předpoklady

Než se ponoříte do fáze kódování, ujistěte se, že máte následující:

1. Základní znalost C#: Vzhledem k tomu, že budeme psát kód v C#, znalost jazyka vám pomůže lépe pochopit tutoriál.
2.  Knihovna Aspose.Cells for .NET: Můžete si ji stáhnout z[Stránka vydání Aspose Cells](https://releases.aspose.com/cells/net/)Pokud jste to ještě neudělali, zvažte možnost získat bezplatnou zkušební verzi a nejprve prozkoumat její funkce.
3. Visual Studio: IDE, kde můžete efektivně psát a testovat svůj kód C#.
4.  Vzorový soubor Excel: Ujistěte se, že máte vzorový soubor Excel, nejlépe takový, který obsahuje kontingenční tabulku pro ukázku. Pro náš příklad použijeme`sample-pivot-table.xlsx`.

S těmito předpoklady začněme s procesem kódování.

## Importujte balíčky

Než začnete psát aplikaci, musíte do kódu zahrnout potřebné jmenné prostory, abyste mohli efektivně využívat knihovnu Aspose.Cells. Zde je návod, jak na to.

### Importujte jmenný prostor Aspose.Cells

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Tento řádek kódu zajišťuje, že máte přístup ke všem třídám a metodám v rámci knihovny Aspose.Cells.

Nyní si celý proces rozeberme podrobně, abychom zajistili, že je vše jasné a srozumitelné.

## Krok 1: Nastavte svůj adresář

Nejprve nastavte adresář, ve kterém jsou umístěny soubory aplikace Excel. Je důležité zadat správnou cestu k souboru.

```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```

 Tady, vyměňte`"Your Document Directory"`se skutečnou cestou k vašim souborům Excel. Zde by měl být umístěn váš vzorový soubor kontingenční tabulky.

## Krok 2: Načtěte zdrojový soubor Excel

Dále musíme načíst soubor Excel, který obsahuje ukázkovou kontingenční tabulku. 

```csharp
// Načtěte zdrojový soubor Excel obsahující ukázkovou kontingenční tabulku
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

 V tomto kroku vytvoříme instanci`Workbook` třídy, která načte zadaný soubor Excel. 

## Krok 3: Otevřete sešity

Nyní, když je sešit načten, máte přístup k listu, který obsahuje data kontingenční tabulky.

```csharp
// Otevřete první list, který obsahuje data kontingenční tabulky
Worksheet dataSheet = wb.Worksheets[0];
```

Zde se dostaneme k prvnímu listu, kde se nachází kontingenční tabulka. Můžete také procházet nebo zadat další listy na základě struktury aplikace Excel.

## Krok 4: Manipulujte s daty buněk

Dále upravíte některé hodnoty buněk v listu. 

### Krok 4.1: Upravte buňku A3

Začněme přístupem k buňce A3 a nastavením její hodnoty.

```csharp
// Otevřete buňku A3 a nastavte její data
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Tento fragment kódu aktualizuje buňku A3 hodnotou „FooBar“.

### Krok 4.2: Upravte buňku B3 pomocí dlouhého řetězce

Nyní nastavíme do buňky B3 dlouhý řetězec, který překračuje standardní limity Excelu.

```csharp
// Přístup k buňce B3, nastavení jejích dat
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Tento kód je důležitý, protože nastavuje vaše očekávání ohledně datových limitů, zejména při práci s nastavením kompatibility v Excelu.

## Krok 5: Zkontrolujte délku buňky B3

Je také nezbytné potvrdit délku řetězce, který jsme zadali.

```csharp
// Vytiskněte délku řetězce buňky B3
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Toto je pouze pro ověření, abyste ukázali, kolik znaků vaše buňka obsahuje.

## Krok 6: Nastavte další hodnoty buňky

Nyní přistoupíme k dalším buňkám a nastavíme některé hodnoty.

```csharp
// Otevřete buňku C3 a nastavte její data
cell = cells["C3"];
cell.PutValue("closed");

// Otevřete buňku D3 a nastavte její data
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Každý z těchto úryvků aktualizuje několik dalších buněk v listu.

## Krok 7: Otevřete kontingenční tabulku

Dále získáte přístup k druhému listu, který se skládá z dat kontingenční tabulky.

```csharp
//Otevřete druhý list, který obsahuje kontingenční tabulku
Worksheet pivotSheet = wb.Worksheets[1];

// Vstupte do kontingenční tabulky
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Tento fragment vám umožňuje manipulovat s kontingenční tabulkou pro nastavení kompatibility.

## Krok 8: Nastavte kompatibilitu pro Excel 2003

Je důležité nastavit, zda je vaše kontingenční tabulka kompatibilní s Excelem 2003 nebo ne. 

```csharp
// Vlastnost IsExcel2003Compatible sděluje, zda je kontingenční tabulka kompatibilní s Excel2003 při aktualizaci kontingenční tabulky
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

 Tady začíná skutečná transformace. Nastavením`IsExcel2003Compatible` na`true`, při obnovování omezíte délku znaků na 255.

## Krok 9: Zkontrolujte délku po nastavení kompatibility

Po nastavení kompatibility se podívejme, jak to ovlivní data.

```csharp
// Zkontrolujte hodnotu buňky B5 kontingenčního listu.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Pokud počáteční data překročí 255 znaků, pravděpodobně uvidíte výstup, který potvrdí efekt zkrácení.

## Krok 10: Změňte nastavení kompatibility

Nyní změňme nastavení kompatibility a znovu zkontrolujte.

```csharp
//Nyní nastavte vlastnost IsExcel2003Compatible na false a znovu aktualizujte
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

To umožňuje, aby vaše data odrážela svou původní délku bez předchozích omezení.

## Krok 11: Znovu ověřte délku 

Pojďme si ověřit, že data nyní přesně odrážejí svou skutečnou délku.

```csharp
// Nyní vytiskne původní délku dat buňky. Data nyní nebyla zkrácena.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

Měli byste vidět, že výstup potvrzuje odstranění zkrácení.

## Krok 12: Naformátujte buňky

Chcete-li zlepšit vizuální zážitek, můžete buňky naformátovat. 

```csharp
// Nastavte výšku řádku a šířku sloupce buňky B5 a také zalamujte její text
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Tyto řádky kódu usnadňují čtení dat tím, že upravují rozměry buněk a umožňují zalamování textu.

## Krok 13: Uložte sešit

Nakonec uložte sešit s provedenými změnami.

```csharp
// Uložte sešit ve formátu xlsx
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

 Výběr vhodného formátu souboru je při ukládání souborů Excel zásadní. The`Xlsx`formát je široce používaný a kompatibilní s mnoha verzemi aplikace Excel.

## Závěr

Gratuluji! Nyní jste naprogramovali nastavení kompatibility souborů aplikace Excel pomocí Aspose.Cells pro .NET. Tento kurz nastínil každý krok, od nastavení prostředí až po změnu nastavení kompatibility pro kontingenční tabulky. Pokud jste někdy pracovali s daty, která vyžadovala specifická omezení nebo kompatibilitu, je to dovednost, kterou nebudete chtít přehlédnout.

## FAQ

### Co je Aspose.Cells?  
Aspose.Cells je knihovna .NET navržená tak, aby pomáhala vývojářům bezproblémově vytvářet, manipulovat a převádět soubory aplikace Excel.

### Proč je kompatibilita s Excelem důležitá?  
Kompatibilita s Excelem je zásadní pro zajištění toho, že soubory lze otevřít a používat v zamýšlených verzích Excelu, zejména pokud obsahují funkce nebo formáty, které dřívější verze nepodporovaly.

### Mohu programově vytvářet kontingenční tabulky pomocí Aspose.Cells?  
Ano, kontingenční tabulky můžete vytvářet a manipulovat s nimi programově pomocí Aspose.Cells. Knihovna poskytuje různé metody pro přidávání zdrojů dat, polí a funkcí spojených s kontingenčními tabulkami.

### Jak zkontroluji délku řetězce v buňce aplikace Excel?  
Můžete použít`StringValue` majetek a`Cell` objekt získat obsah buňky a poté zavolat`.Length` vlastnost pro zjištění délky řetězce.

### Mohu přizpůsobit formátování buněk nad rámec výšky a šířky řádku?  
 Absolutně! Aspose.Cells umožňuje rozsáhlé formátování buněk. Můžete změnit styly písma, barvy, okraje, formáty čísel a mnoho dalšího prostřednictvím`Style` třída.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
