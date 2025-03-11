---
title: Zrušit sloučení sloučených buněk v Excelu
linktitle: Zrušit sloučení sloučených buněk v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: Snadno zrušte sloučení sloučených buněk v aplikaci Excel pomocí Aspose.Cells pro .NET. Chcete-li vytvářet lepší tabulky, postupujte podle našeho podrobného průvodce.
weight: 10
url: /cs/net/excel-merging-unmerging-cells/unmerge-merged-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zrušit sloučení sloučených buněk v Excelu

## Zavedení

Už vás nebaví řešit sloučené buňky v excelových tabulkách? Nejsi sám! Sloučené buňky mohou být užitečnou funkcí pro formátování, ale často mohou vést k bolestem hlavy, pokud jde o manipulaci a analýzu dat. Ale hádejte co? Zrušení sloučení těchto otravných buněk je snazší, než si myslíte – zvláště když používáte Aspose.Cells pro .NET. V tomto článku vás provedu krok za krokem, jak zrušit sloučení sloučených buněk a zajistit, aby vaše data byla čistá, uklizená a připravená k akci! Popadněte tedy svůj kódovací klobouk a pojďme se ponořit do světa Aspose.Cells.

## Předpoklady

Než si ušpiníme ruce, je potřeba mít připraveno několik náležitostí:

### Základní znalost C# a .NET Framework
Pokud jste obeznámeni s programováním v C# a máte základní znalosti o frameworku .NET, jste již na skvělém začátku. Pokud ne, nebojte se! Tento tutoriál je navržen tak, aby byl přímočarý, takže si potřebné koncepty osvojíte během cesty.

### Knihovna Aspose.Cells
Ujistěte se, že máte ve svém prostředí .NET nainstalovanou knihovnu Aspose.Cells. Můžete to snadno získat návštěvou[Stránka ke stažení Aspose.Cells](https://releases.aspose.com/cells/net/).

### Nastavení IDE
Měli byste mít nastavené vývojové prostředí, jako je Visual Studio, kde můžete psát a spouštět svůj kód C#.

### Ukázkový soubor Excel
Vezměte si ukázkový soubor aplikace Excel, který obsahuje nějaké sloučené buňky – tento soubor budete používat k procvičování zrušení sloučení.

Se všemi těmito předpoklady se nyní můžeme vrhnout na vzrušující část – kódování našeho řešení!

## Importujte balíčky

Nejprve naimportujme potřebné balíčky. S Aspose.Cells budete komunikovat s různými třídami, abyste mohli efektivně spravovat své soubory Excel. Zde je to, co musíte zahrnout do horní části souboru C#:

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

Zahrnutím tohoto balíčku budete mít přístup ke všem funkcím, které Aspose.Cells nabízí.

Rozdělme proces rozpojování do zvládnutelných kroků. Každý krok bude jasně definován, takže jej můžete snadno sledovat.

## Krok 1: Definujte adresáře

Prvním krokem je definování adresářů, kde se nachází váš vstupní soubor Excel (ten se sloučenými buňkami) a váš výstupní soubor (ten, kam budou uložena nesloučená data). Zde je návod, jak to nastavit:

```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory"; 

// Výstupní adresář
string outputDir = "Your Document Directory"; 
```

 Nezapomeňte vyměnit`"Your Document Directory"` se skutečnou cestou k vašim souborům.

## Krok 2: Vytvořte sešit

Nyní, když jste nastavili adresáře, je čas vytvořit objekt Workbook. Tento objekt vám umožní manipulovat se souborem Excel. Můžete to udělat pomocí následujícího kódu:

```csharp
// Vytvořte sešit
Workbook wbk = new Aspose.Cells.Workbook(sourceDir + "sampleUnMergingtheMergedCells.xlsx");
```

Tento řádek kódu přečte váš ukázkový soubor aplikace Excel a připraví jej ke zpracování. 

## Krok 3: Otevřete sešit

Každý sešit se skládá z listů. Potřebujete přístup ke konkrétnímu listu, kde chcete zrušit sloučení buněk. Postup:

```csharp
// Vytvořte pracovní list a získejte první list
Worksheet worksheet = wbk.Worksheets[0];
```

Tento kód uchopí první list. Pokud jsou vaše sloučené buňky na jiném listu, aktualizujte odpovídajícím způsobem index.

## Krok 4: Přístup k buňkám v listu

Dále budete muset získat odkaz na buňky v listu. To lze provést pomocí:

```csharp
//Vytvořte objekt Cells pro načtení všech buněk
Cells cells = worksheet.Cells;
```

S tímto řádkem máte nyní přístup ke všem buňkám na listu, což vám umožňuje s nimi manipulovat podle potřeby.

## Krok 5: Zrušte sloučení buněk

Zde přichází zásadní krok — rozpojení buněk! Budete chtít určit rozsah sloučených buněk, které chcete zrušit. Použijte následující kód:

```csharp
// Zrušte sloučení buněk
cells.UnMerge(5, 2, 2, 3);
```

 V tomto příkladu je`UnMerge` metoda přebírá čtyři parametry: index počátečního řádku (5), index počátečního sloupce (2), počet řádků k zrušení sloučení (2) a počet sloupců k zrušení sloučení (3). Upravte tyto parametry tak, aby odpovídaly konkrétním sloučeným buňkám v souboru aplikace Excel.

## Krok 6: Uložte sešit

Po zrušení sloučení budete chtít uložit změny do nového souboru aplikace Excel. Postup:

```csharp
// Uložte soubor
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

Tento řádek uloží vaše nesloučená data do určeného výstupního adresáře. Jak jednoduché!

## Krok 7: Potvrďte proces

Nakonec je dobré potvrdit, že vše proběhlo hladce. Můžete vytisknout zprávu do konzole, abyste věděli, že operace byla úspěšně provedena:

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

tady to máte! Úspěšně jste zrušili sloučení buněk v souboru aplikace Excel pomocí Aspose.Cells for .NET.

## Závěr

Rozpojování buněk se může zdát zdlouhavé, zvláště pokud pracujete s velkými tabulkami, ale s Aspose.Cells pro .NET je to hračka! Tento tutoriál vás provede vším od nastavení vašeho prostředí až po spuštění kódu potřebného k efektivnímu zrušení sloučení buněk. Flexibilita, kterou nabízí knihovna Aspose.Cells, umožňuje efektivně zpracovávat tabulky, takže je ideální volbou pro vývojáře pracující se soubory Excel. Ponořte se do toho a začněte si užívat čistší a lépe ovladatelné tabulky.

## FAQ

### Co je Aspose.Cells?  
Aspose.Cells je výkonná knihovna pro vytváření, manipulaci a konverzi dokumentů aplikace Excel v aplikacích .NET.

### Potřebuji licenci k používání Aspose.Cells?  
 Zatímco Aspose.Cells nabízí bezplatnou zkušební verzi, pro plné použití je vyžadována licence. Můžete získat a[dočasná licence zde](https://purchase.aspose.com/temporary-license/).

### Mohu zrušit sloučení buněk ve více listech najednou?  
Ano, můžete procházet více listy v sešitu a podle potřeby zrušit sloučení buněk.

### Je Aspose.Cells kompatibilní s .NET Core?  
Ano, Aspose.Cells je kompatibilní s .NET Core, takže je univerzální pro různé aplikace .NET.

### Kde najdu další dokumentaci na Aspose.Cells?  
 Kompletní dokumentaci si můžete prohlédnout na[Referenční stránka Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
