---
"description": "Naučte se manipulovat s kontingenčními tabulkami v Excelu pomocí Aspose.Cells pro .NET, včetně aktualizací dat, nastavení kompatibility a formátování buněk."
"linktitle": "Programové určení kompatibility souboru Excel v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Programové určení kompatibility souboru Excel v .NET"
"url": "/cs/net/creating-and-configuring-pivot-tables/specifying-compatibility/"
"weight": 23
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Programové určení kompatibility souboru Excel v .NET

## Zavedení

V dnešním světě založeném na datech se programově stala správa a manipulace s excelovými soubory pro mnoho vývojářů nezbytnou. Pokud pracujete s Excelem v .NET, Aspose.Cells je výkonná knihovna, která usnadňuje vytváření, čtení, úpravy a ukládání excelových souborů. Jedna důležitá funkce této knihovny umožňuje programově specifikovat kompatibilitu excelových souborů. V tomto tutoriálu se podíváme na to, jak manipulovat s excelovými soubory, se zvláštním zaměřením na správu kompatibility pomocí Aspose.Cells pro .NET. Na konci pochopíte, jak nastavit kompatibilitu excelových souborů, zejména kontingenčních tabulek, a zároveň aktualizovat a spravovat data.

## Předpoklady

Než se pustíte do fáze kódování, ujistěte se, že máte následující:

1. Základní znalost jazyka C#: Protože budeme psát kód v jazyce C#, znalost tohoto jazyka vám pomůže lépe porozumět tutoriálu.
2. Knihovna Aspose.Cells pro .NET: Můžete si ji stáhnout z [Stránka s vydáním Aspose Cells](https://releases.aspose.com/cells/net/)Pokud jste tak ještě neučinili, zvažte nejprve bezplatnou zkušební verzi, abyste si prozkoumali jeho funkce.
3. Visual Studio: IDE, kde můžete efektivně psát a testovat kód v C#.
4. Ukázkový soubor Excel: Ujistěte se, že máte ukázkový soubor Excel, nejlépe takový, který obsahuje kontingenční tabulku pro ukázku. V našem příkladu použijeme `sample-pivot-table.xlsx`.

S těmito předpoklady pojďme začít s procesem kódování.

## Importovat balíčky

Než začnete psát aplikaci, musíte do kódu zahrnout potřebné jmenné prostory, abyste mohli efektivně využívat knihovnu Aspose.Cells. Zde je návod, jak to udělat.

### Importovat jmenný prostor Aspose.Cells

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Tento řádek kódu zajišťuje přístup ke všem třídám a metodám v knihovně Aspose.Cells.

Nyní si celý proces podrobně rozebereme, aby bylo vše jasné a srozumitelné.

## Krok 1: Nastavení adresáře

Nejprve si nastavte adresář, kde se nacházejí vaše soubory aplikace Excel. Je důležité zadat správnou cestu k souboru.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
```

Zde nahraďte `"Your Document Directory"` se skutečnou cestou k vašim souborům aplikace Excel. Zde by se měl nacházet váš vzorový soubor kontingenční tabulky.

## Krok 2: Načtěte zdrojový soubor Excel

Dále musíme načíst soubor aplikace Excel, který obsahuje vzorovou kontingenční tabulku. 

```csharp
// Načíst zdrojový soubor Excel obsahující vzorovou kontingenční tabulku
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

V tomto kroku vytvoříme instanci `Workbook` třída, která načte zadaný soubor aplikace Excel. 

## Krok 3: Přístup k pracovním listům

Nyní, když je sešit načten, musíte přistupovat k listu, který obsahuje data kontingenční tabulky.

```csharp
// Přístup k prvnímu listu, který obsahuje data kontingenční tabulky
Worksheet dataSheet = wb.Worksheets[0];
```

Zde se dostaneme k prvnímu listu, kde se nachází kontingenční tabulka. Můžete také procházet nebo specifikovat další listy na základě struktury vaší aplikace Excel.

## Krok 4: Manipulace s buněčnými daty

Dále upravíte některé hodnoty buněk v listu. 

### Krok 4.1: Úprava buňky A3

Začněme tím, že otevřeme buňku A3 a nastavíme její hodnotu.

```csharp
// Přístup k buňce A3 a nastavení jejích dat
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Tento úryvek kódu aktualizuje buňku A3 hodnotou „FooBar“.

### Krok 4.2: Úprava buňky B3 pomocí dlouhého řetězce

Nyní do buňky B3 vložme dlouhý řetězec, který překračuje standardní limity znaků v Excelu.

```csharp
// Přístup k buňce B3, nastavení jejích dat
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Tento kód je důležitý, protože nastavuje vaše očekávání ohledně datových limitů, zejména při práci s nastavením kompatibility v Excelu.

## Krok 5: Zkontrolujte délku buňky B3

Je také nezbytné potvrdit délku zadaného řetězce.

```csharp
// Vypište délku řetězce buňky B3
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Toto slouží pouze k ověření, kolik znaků má vaše buňka uloženo.

## Krok 6: Nastavení dalších hodnot buněk

Nyní zpřístupníme další buňky a nastavíme nějaké hodnoty.

```csharp
// Přístup k buňce C3 a nastavení jejích dat
cell = cells["C3"];
cell.PutValue("closed");

// Přístup k buňce D3 a nastavení jejích dat
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Každý z těchto úryvků aktualizuje několik dalších buněk v listu.

## Krok 7: Přístup k kontingenční tabulce

Dále se dostanete k druhému listu, který obsahuje data kontingenční tabulky.

```csharp
// Přístup k druhému listu, který obsahuje kontingenční tabulku
Worksheet pivotSheet = wb.Worksheets[1];

// Přístup k kontingenční tabulce
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Tento úryvek umožňuje manipulovat s kontingenční tabulkou pro nastavení kompatibility.

## Krok 8: Nastavení kompatibility pro Excel 2003

Je důležité nastavit, zda je vaše kontingenční tabulka kompatibilní s Excelem 2003. 

```csharp
// Vlastnost IsExcel2003Compatible při aktualizaci kontingenční tabulky určuje, zda je kontingenční tabulka kompatibilní s Excelem 2003.
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Zde začíná skutečná transformace. Nastavením `IsExcel2003Compatible` na `true`při aktualizaci omezíte délku znaků na 255.

## Krok 9: Zkontrolujte délku po nastavení kompatibility

Po nastavení kompatibility se podívejme, jak to ovlivní data.

```csharp
// Zkontrolujte hodnotu buňky B5 v pivotním listu.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Pokud počáteční data překročí 255 znaků, pravděpodobně se zobrazí výstup potvrzující efekt zkrácení.

## Krok 10: Změna nastavení kompatibility

Nyní změníme nastavení kompatibility a znovu to zkontrolujeme.

```csharp
// Nyní nastavte vlastnost IsExcel2003Compatible na hodnotu false a znovu obnovte
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Díky tomu si vaše data zachovají svou původní délku bez předchozích omezení.

## Krok 11: Znovu ověřte délku 

Ověřme, zda data nyní přesně odrážejí jejich skutečnou délku.

```csharp
// Nyní se vypíše původní délka dat buňky. Data nyní nebyla zkrácena.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

Měli byste vidět, že výstup potvrzuje odstranění zkrácení.

## Krok 12: Formátování buněk

Pro vylepšení vizuálního zážitku můžete buňky naformátovat. 

```csharp
// Nastavte výšku řádku a šířku sloupce buňky B5 a také zalomte její text
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Tyto řádky kódu usnadňují čtení dat úpravou rozměrů buněk a povolením zalamování textu.

## Krok 13: Uložení sešitu

Nakonec uložte sešit s provedenými změnami.

```csharp
// Uložit sešit ve formátu xlsx
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

Výběr vhodného formátu souboru je při ukládání souborů aplikace Excel klíčový. `Xlsx` Formát je široce používaný a kompatibilní s mnoha verzemi Excelu.

## Závěr

Gratulujeme! Právě jste naprogramovali nastavení kompatibility souborů Excelu pomocí Aspose.Cells pro .NET. Tento tutoriál popsal jednotlivé kroky, od nastavení prostředí až po změnu nastavení kompatibility pro kontingenční tabulky. Pokud jste někdy pracovali s daty, která vyžadovala specifická omezení nebo kompatibilitu, je to dovednost, kterou byste neměli přehlédnout.

## Často kladené otázky

### Co je Aspose.Cells?  
Aspose.Cells je knihovna .NET navržená tak, aby vývojářům pomohla bezproblémově vytvářet, manipulovat a převádět soubory Excelu.

### Proč je kompatibilita s Excelem důležitá?  
Kompatibilita s Excelem je klíčová pro zajištění toho, aby bylo možné soubory otevírat a používat v zamýšlených verzích Excelu, zejména pokud obsahují funkce nebo formáty, které nebyly v dřívějších verzích podporovány.

### Mohu programově vytvářet kontingenční tabulky pomocí Aspose.Cells?  
Ano, kontingenční tabulky můžete programově vytvářet a manipulovat s nimi pomocí knihovny Aspose.Cells. Knihovna nabízí různé metody pro přidávání zdrojů dat, polí a funkcí spojených s kontingenčními tabulkami.

### Jak zkontroluji délku řetězce v buňce aplikace Excel?  
Můžete použít `StringValue` majetek `Cell` objekt pro získání obsahu buňky a následné zavolání `.Length` vlastnost pro zjištění délky řetězce.

### Mohu přizpůsobit formátování buněk nad rámec výšky a šířky řádku?  
Rozhodně! Aspose.Cells umožňuje rozsáhlé formátování buněk. Můžete změnit styly písma, barvy, ohraničení, formáty čísel a mnoho dalšího prostřednictvím `Style` třída.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}