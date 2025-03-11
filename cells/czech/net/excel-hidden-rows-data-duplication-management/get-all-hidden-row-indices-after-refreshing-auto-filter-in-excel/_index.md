---
title: Získejte indexy skrytých řádků po obnovení automatického filtru v Excelu
linktitle: Získejte indexy skrytých řádků po obnovení automatického filtru v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: Zjistěte, jak získat skryté indexy řádků po obnovení automatického filtru v aplikaci Excel pomocí Aspose.Cells for .NET. Zjednodušte si správu dat.
weight: 10
url: /cs/net/excel-hidden-rows-data-duplication-management/get-all-hidden-row-indices-after-refreshing-auto-filter-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Získejte indexy skrytých řádků po obnovení automatického filtru v Excelu

## Zavedení

Při práci se soubory aplikace Excel, zejména s velkými datovými sadami, může být filtrování záchranou. Pomáhá nám to zaměřit se na konkrétní datové body, ale co se stane, když chcete po použití filtru identifikovat skryté řádky? Pokud jste někdy byli zvědaví na vytažení těchto skrytých detailů, jste na správném místě! V této příručce prozkoumáme, jak získat skryté indexy řádků po obnovení automatického filtru v Excelu pomocí Aspose.Cells for .NET. Ať už jste ostřílený programátor nebo začátečník, shledáte proces přímočarý a poutavý. Pojďme se ponořit!

## Předpoklady

Než se pustíte do kódu, je třeba mít na paměti několik předpokladů:

### Porozumění Aspose.Cells pro .NET

Chcete-li pokračovat v tomto tutoriálu, musíte dobře rozumět tomu, co je Aspose.Cells. V podstatě se jedná o výkonnou knihovnu pro .NET, která vám umožňuje vytvářet, manipulovat a převádět soubory aplikace Excel bez nutnosti instalace aplikace Microsoft Excel. Je to nástroj, který bez problémů zvládne vše od jednoduchého zadávání dat až po komplexní analýzu dat.

### Nastavení vývojového prostředí

1.  Nainstalujte Visual Studio: Ujistěte se, že máte v počítači nainstalované Visual Studio. Můžete si jej stáhnout z[Web Visual Studio](https://visualstudio.microsoft.com/).

2. .NET Framework: Budete potřebovat kompatibilní verzi .NET Framework nebo .NET Core. Tato knihovna funguje dobře s oběma frameworky.

3.  Knihovna Aspose.Cells: Stáhněte a nainstalujte knihovnu Aspose.Cells z[tento odkaz](https://releases.aspose.com/cells/net/). Případně jej můžete nainstalovat přes NuGet. Stačí otevřít konzolu Správce balíčků a spustit:
```
Install-Package Aspose.Cells
```

4.  Ukázkový soubor aplikace Excel: Připravte ukázkový soubor aplikace Excel s názvem`sampleGetAllHiddenRowsIndicesAfterRefreshingAutoFilter.xlsx` pro testování. Nezapomeňte uvést některá data, která lze filtrovat.

## Importujte balíčky

Abyste se mohli pustit do této programovací cesty, budete muset importovat potřebné jmenné prostory. Toto je zásadní krok, protože umožňuje použití funkcí Aspose.Cells ve vašem projektu.

1. Otevřete projekt v sadě Visual Studio.
2. Do souboru kódu v horní části přidejte následující pomocí direktiv:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Tyto direktivy říkají vašemu kompilátoru, kde má hledat třídy a metody, které se chystáte použít.

V této části rozdělíme proces do snadno pochopitelných kroků. Budete mít přístup k listu aplikace Excel, použít filtr a identifikovat skryté řádky – to vše pomocí Aspose.Cells.

## Krok 1: Nastavte své prostředí

Než se vrhneme na kódování, nastavíme naše prostředí a deklarujeme potřebné proměnné. Toto nastavení přesměruje vše do vašeho vzorového souboru Excel a připraví sešit.

```csharp
string sourceDir = "Your Document Directory"; // zadejte svůj adresář
```

## Krok 2: Načtěte ukázkový soubor Excel

Dále musíme načíst váš soubor Excel do objektu sešitu. To nám umožňuje programově manipulovat. 

```csharp
Workbook wb = new Workbook(sourceDir + "sampleGetAllHiddenRowsIndicesAfterRefreshingAutoFilter.xlsx");
```

 Tady vytváříme nový`Workbook` objekt, který načte zadaný soubor Excel.

## Krok 3: Otevřete požadovaný pracovní list

Nyní budeme pracovat s prvním pracovním listem sešitu. Tento krok izoluje list obsahující data, která chceme filtrovat.

```csharp
Worksheet ws = wb.Worksheets[0]; // Přístup k prvnímu pracovnímu listu
```

## Krok 4: Použijte automatický filtr

Použití automatického filtru je místo, kde kouzlo začíná! Zadáme, který sloupec chceme filtrovat, a nastavíme kritéria. Zde filtrujeme „oranžovou“. 

```csharp
ws.AutoFilter.AddFilter(0, "Orange"); // Použijte automatický filtr pro první sloupec
```

## Krok 5: Obnovte automatický filtr a získejte skryté řádky

Následující řádek aktualizuje automatický filtr. Vrátí indexy řádků, které jsou po použití našeho filtru skryté. Nastavením parametru na true se filtr efektivně obnoví.

```csharp
int[] rowIndices = ws.AutoFilter.Refresh(true);
```

## Krok 6: Vytiskněte indexy skrytých řádků

Nyní, když máme naše skryté indexy řádků, vyšleme je do konzole. To poskytne jasno v tom, co bylo skryto díky našemu automatickému filtru.

```csharp
Console.WriteLine("Printing Rows Indices, Cell Names and Values Hidden By AutoFilter.");
Console.WriteLine("--------------------------");

for (int i = 0; i < rowIndices.Length; i++)
{
    int r = rowIndices[i];
    Cell cell = ws.Cells[r, 0];
    Console.WriteLine(r + "\t" + cell.Name + "\t" + cell.StringValue);
}

Console.WriteLine("GetAllHiddenRowsIndicesAfterRefreshingAutoFilter executed successfully.");
```

## Závěr

tady to máte! Po obnovení automatického filtru v Excelu pomocí Aspose.Cells for .NET jste úspěšně načetli indexy skrytých řádků. Docela pěkné, že? Tato funkce může dramaticky vylepšit vaše projekty analýzy dat, takže váš pracovní postup bude plynulejší a efektivnější.

## FAQ

### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna pro .NET, která umožňuje vývojářům vytvářet, manipulovat a exportovat soubory aplikace Excel, aniž by potřebovali Microsoft Excel.

### Mohu filtrovat data v Excelu pomocí Aspose.Cells?
Ano! Aspose.Cells má vestavěné funkce pro použití filtrů a efektivní práci s daty aplikace Excel.

### Je Aspose.Cells zdarma k použití?
 Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro další používání si budete muset zakoupit licenci. Zkontrolujte[nákupní stránku](https://purchase.aspose.com/buy) pro podrobnosti.

### Jak mohu získat podporu pro Aspose.Cells?
 Můžete hledat podporu od komunity Aspose prostřednictvím[Aspose fórum](https://forum.aspose.com/c/cells/9).

### Kde najdu dokumentaci k Aspose.Cells?
 K dispozici je kompletní dokumentace[zde](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
