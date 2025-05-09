---
"description": "Snadno rozdělte sloučené buňky v Excelu pomocí Aspose.Cells pro .NET. Postupujte podle našeho podrobného návodu a vytvořte lepší tabulky."
"linktitle": "Zrušení sloučení buněk v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Zrušení sloučení buněk v Excelu"
"url": "/cs/net/excel-merging-unmerging-cells/unmerge-merged-cells/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zrušení sloučení buněk v Excelu

## Zavedení

Už vás nebaví pracovat se sloučenými buňkami v excelových tabulkách? Nejste sami! Sloučené buňky mohou být užitečnou funkcí pro formátování, ale často mohou vést k bolestem hlavy, pokud jde o manipulaci s daty a jejich analýzu. Ale víte co? Rozdělení těchto otravných buněk je snazší, než si myslíte – zvláště když používáte Aspose.Cells pro .NET. V tomto článku vás krok za krokem provedu tím, jak rozdělit sloučené buňky a zajistit, aby vaše data byla úhledná, přehledná a připravená k akci! Takže, vezměte si programátorskou čepici a pojďme se ponořit do světa Aspose.Cells.

## Předpoklady

Než se do toho pustíme, je tu několik nezbytných věcí, které budete potřebovat:

### Základní znalost C# a .NET Frameworku
Pokud jste obeznámeni s programováním v C# a máte základní znalosti frameworku .NET, máte skvělý začátek. Pokud ne, nebojte se! Tento tutoriál je navržen tak, aby byl srozumitelný, takže si potřebné koncepty osvojíte za pochodu.

### Knihovna Aspose.Cells
Ujistěte se, že máte ve svém prostředí .NET nainstalovanou knihovnu Aspose.Cells. Tuto knihovnu snadno získáte na adrese [Stránka pro stažení Aspose.Cells](https://releases.aspose.com/cells/net/).

### Nastavení IDE
Měli byste mít nastavené vývojové prostředí, například Visual Studio, kde můžete psát a spouštět kód v C#.

### Ukázkový soubor Excelu
Vezměte si ukázkový soubor aplikace Excel, který obsahuje několik sloučených buněk – tento soubor použijete k procvičení oddělování buněk.

Po splnění všech těchto předpokladů se nyní můžeme pustit do té vzrušující části – kódování našeho řešení!

## Importovat balíčky

Nejdříve si importujme potřebné balíčky. S Aspose.Cells budete interagovat s různými třídami, abyste mohli efektivně spravovat soubory aplikace Excel. Zde je to, co je třeba zahrnout na začátek souboru C#:

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

Zahrnutím tohoto balíčku získáte přístup ke všem funkcím, které Aspose.Cells nabízí.

Rozdělme si proces oddělování do zvládnutelných kroků. Každý krok bude jasně definován, abyste ho mohli snadno sledovat.

## Krok 1: Definování adresářů

Prvním krokem je definování adresářů, kde se nachází váš vstupní soubor aplikace Excel (ten se sloučenými buňkami) a výstupní soubor (ten, kam budou uložena nesloučená data). Zde je návod, jak to nastavit:

```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory"; 

// Výstupní adresář
string outputDir = "Your Document Directory"; 
```

Nezapomeňte vyměnit `"Your Document Directory"` se skutečnou cestou k vašim souborům.

## Krok 2: Vytvořte sešit

Nyní, když jste nastavili adresáře, je čas vytvořit objekt Workbook. Tento objekt vám umožní manipulovat s excelovým souborem. Můžete to provést pomocí následujícího kódu:

```csharp
// Vytvořte si sešit
Workbook wbk = new Aspose.Cells.Workbook(sourceDir + "sampleUnMergingtheMergedCells.xlsx");
```

Tento řádek kódu přečte váš ukázkový soubor aplikace Excel a připraví ho ke zpracování. 

## Krok 3: Přístup k pracovnímu listu

Každý sešit se skládá z listů. Musíte otevřít konkrétní list, ve kterém chcete buňky sloučit. Postupujte takto:

```csharp
// Vytvořte pracovní list a získejte první list
Worksheet worksheet = wbk.Worksheets[0];
```

Tento kód načte první list. Pokud se sloučené buňky nacházejí na jiném listu, aktualizujte index odpovídajícím způsobem.

## Krok 4: Přístup k buňkám v pracovním listu

Dále budete potřebovat získat odkaz na buňky ve vašem listu. Toho lze dosáhnout pomocí:

```csharp
// Vytvořte objekt Cells pro načtení všech buněk
Cells cells = worksheet.Cells;
```

Díky tomuto řádku máte nyní přístup ke všem buňkám na listu, což vám umožňuje s nimi manipulovat podle potřeby.

## Krok 5: Zrušte sloučení buněk

tady přichází klíčový krok – sloučení buněk! Budete chtít určit rozsah sloučených buněk, které chcete sloučení zrušit. Použijte následující kód:

```csharp
// Zrušit sloučení buněk
cells.UnMerge(5, 2, 2, 3);
```

V tomto příkladu `UnMerge` Metoda přijímá čtyři parametry: index počátečního řádku (5), index počátečního sloupce (2), počet řádků, které se mají sloučit (2), a počet sloupců, které se mají sloučit (3). Upravte tyto parametry tak, aby odpovídaly konkrétním sloučeným buňkám v souboru aplikace Excel.

## Krok 6: Uložení sešitu

Po zrušení sloučení budete chtít uložit změny do nového souboru aplikace Excel. Postupujte takto:

```csharp
// Uložte soubor
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

Tento řádek uloží vaše nesloučená data do zadaného výstupního adresáře. Je to jednoduché!

## Krok 7: Potvrďte proces

Nakonec je dobré potvrdit, že vše proběhlo hladce. Do konzole můžete vypsat zprávu, která vás informuje o úspěšném provedení operace:

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

A tady to máte! Úspěšně jste rozdělili buňky v souboru aplikace Excel pomocí Aspose.Cells for .NET.

## Závěr

Rozdělování buněk se může zdát zdlouhavé, zvláště pokud pracujete s velkými tabulkami, ale s Aspose.Cells pro .NET je to hračka! Tento tutoriál vás provede vším od nastavení prostředí až po spuštění kódu potřebného k efektivnímu rozdělení buněk. Flexibilita, kterou nabízí knihovna Aspose.Cells, vám umožňuje efektivně zpracovávat tabulky, což z ní činí ideální volbu pro vývojáře pracující se soubory Excelu. Takže se do toho pusťte a začněte si užívat čistší a lépe spravovatelné tabulky.

## Často kladené otázky

### Co je Aspose.Cells?  
Aspose.Cells je výkonná knihovna pro vytváření, manipulaci s dokumenty aplikace Excel a jejich převod v aplikacích .NET.

### Potřebuji licenci k používání Aspose.Cells?  
Ačkoli Aspose.Cells nabízí bezplatnou zkušební verzi, pro plné využití je vyžadována licence. Můžete získat [dočasná licence zde](https://purchase.aspose.com/temporary-license/).

### Mohu rozdělit buňky ve více listech najednou?  
Ano, v sešitu můžete procházet více pracovních listů a podle potřeby sloučit buňky.

### Je Aspose.Cells kompatibilní s .NET Core?  
Ano, Aspose.Cells je kompatibilní s .NET Core, takže je všestranný pro různé .NET aplikace.

### Kde najdu další dokumentaci k Aspose.Cells?  
Kompletní dokumentaci si můžete prohlédnout na [Referenční stránka Aspose.Cells](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}