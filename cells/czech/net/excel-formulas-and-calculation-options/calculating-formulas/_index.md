---
title: Výpočet vzorců v Excelu programově
linktitle: Výpočet vzorců v Excelu programově
second_title: Aspose.Cells .NET Excel Processing API
description: Automatizujte své úkoly v Excelu pomocí Aspose.Cells pro .NET. Naučte se programově vypočítat vzorce v tomto komplexním kurzu.
weight: 11
url: /cs/net/excel-formulas-and-calculation-options/calculating-formulas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Výpočet vzorců v Excelu programově

## Zavedení
dnešním světě založeném na datech může automatizace úloh ušetřit čas a zvýšit efektivitu, zejména při práci s tabulkami. Pokud jste někdy žonglovali se složitými vzorci v Excelu, víte, jak důležité je mít to správně. Pomocí Aspose.Cells for .NET můžete programově vypočítat vzorce a snadno spravovat soubory aplikace Excel. V tomto tutoriálu si projdeme každý krok při vytváření souboru aplikace Excel, přidávání hodnot a vzorců a poté výpočet těchto vzorců s trochou jazyka C#. Pojďme se ponořit!
## Předpoklady
Než začneme, měli byste se ujistit, že máte připraveno několik věcí:
1. Vývojové prostředí: Ujistěte se, že máte Visual Studio nebo jakékoli jiné prostředí C#, kde můžete spouštět aplikace .NET.
2.  Aspose.Cells for .NET: Stáhněte a nainstalujte knihovnu Aspose.Cells. Můžete to získat z[Aspose webové stránky](https://releases.aspose.com/cells/net/).
3. Základní porozumění C#: Základní znalost C# vám pomůže pochopit koncepty a úryvky kódu, které budeme používat.
4. .NET Framework: Ujistěte se, že je na vašem počítači nainstalována vhodná verze .NET Framework.
5.  Licence Aspose.Cells: Pokud ji chcete používat nad rámec bezplatné zkušební verze, zvažte získání a[dočasná licence](https://purchase.aspose.com/temporary-license/).
Nyní, když máme vše připraveno, vrhneme se na kód a rozebereme ho krok za krokem!
## Importujte balíčky
Před napsáním jakéhokoli kódu se ujistěte, že jste do souboru C# importovali potřebné jmenné prostory pro Aspose.Cells:
```csharp
using System.IO;
using Aspose.Cells;
```
To vám umožní přístup k funkcím poskytovaným knihovnou Aspose.Cells pro manipulaci se soubory aplikace Excel.
## Krok 1: Nastavte adresář dokumentů
Začněte definováním cesty, kam chcete dokument Excel uložit. Je nezbytné zajistit, aby tento adresář existoval, nebo jej vytvořit, pokud neexistuje.
```csharp
// Cesta k adresáři dokumentů
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
V tomto kroku zkontrolujete, zda adresář existuje. Pokud ne, vytváříte to vy. Tento jednoduchý krok pomáhá vyhnout se chybám při pozdějším pokusu o uložení souboru Excel.
## Krok 2: Vytvořte instanci objektu sešitu
## Vytvoření nového sešitu
Nyní, když je váš adresář nastaven, vytvořte objekt Workbook, který představuje váš soubor Excel:
```csharp
// Vytvoření instance objektu sešitu
Workbook workbook = new Workbook();
```
Tento řádek jednoduše vytvoří nový sešit v paměti. Představte si to jako otevření prázdného souboru aplikace Excel, do kterého můžete začít přidávat data a vzorce.
## Krok 3: Přidejte nový list
## Práce s pracovními listy
V našem sešitu chceme přidat nový list, kde můžeme manipulovat s našimi daty. Zde je návod, jak se to dělá:
```csharp
// Přidání nového listu do objektu aplikace Excel
int sheetIndex = workbook.Worksheets.Add();
// Získání odkazu na nově přidaný list předáním jeho indexu listu
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Nejprve přidáte nový list, který vám automaticky poskytne rejstřík tohoto listu. Dále tento list načtete podle jeho indexu. Je to jako otevřít novou kartu v excelovém sešitu!
## Krok 4: Vložte hodnoty do buněk
## Naplňování dat
Nyní, když jsme vytvořili náš list, musíme do něj přidat některá data:
```csharp
// Přidání hodnoty do buňky "A1".
worksheet.Cells["A1"].PutValue(1);
// Přidání hodnoty do buňky "A2".
worksheet.Cells["A2"].PutValue(2);
// Přidání hodnoty do buňky "A3".
worksheet.Cells["A3"].PutValue(3);
```
V tomto kroku vkládáte hodnoty do prvních tří buněk (A1, A2, A3) listu. Tato akce je podobná psaní hodnot přímo do listu aplikace Excel. 
## Krok 5: Přidejte vzorec
## Shrnutí hodnot
Po zadání hodnot je čas přidat vzorec, který vypočítá součet těchto buněk. Zde je postup:
```csharp
// Přidání vzorce SUM do buňky "A4".
worksheet.Cells["A4"].Formula = "=SUM(A1:A3)";
```
Tento řádek kódu připojí k buňce A4 vzorec SUM, který sečte hodnoty od A1 do A3. Je to jako napsat vzorec v Excelu, ale programově!
## Krok 6: Vypočítejte vzorec
## Provádění výpočtu
Nyní přichází okamžik pravdy! Musíme vypočítat výsledky vzorců, které jsme zadali:
```csharp
// Výpočet výsledků vzorců
workbook.CalculateFormula();
```
 Zavoláním`CalculateFormula()`, říkáte sešitu, aby zpracoval všechny vzorce v něm. Je to podobné, jako když po zadání vzorce do buňky aplikace Excel stisknete "Enter".
## Krok 7: Načtěte vypočítanou hodnotu
## Čtení výsledku
Jakmile jsou vzorce vypočteny, můžeme získat hodnotu z A4:
```csharp
// Získejte vypočítanou hodnotu buňky
string value = worksheet.Cells["A4"].Value.ToString();
```
tomto kroku získáte výsledek našeho vzorce SUM. To by vám dalo celkem 1 + 2 + 3, což je 6!
## Krok 8: Uložte soubor Excel
## Zápis na disk
Nakonec uložte sešit do určeného adresáře, abyste k němu měli přístup později:
```csharp
// Uložení souboru Excel
workbook.Save(dataDir + "output.xls");
```
Tento kód uloží váš soubor Excel s názvem "output.xls" do adresáře, který jste zadali. Je to jako kliknout na „Uložit jako“ v Excelu a vybrat si, kam soubor uložit.
## Závěr
V tomto tutoriálu jsme se zabývali tím, jak vytvořit soubor aplikace Excel programově pomocí Aspose.Cells pro .NET. Od přidávání hodnot a vzorců po výpočet a ukládání konečného výstupu jsme prošli každým kritickým krokem, abychom vám zajistili pevný základ pro budoucí automatizaci.
## FAQ
### Co je Aspose.Cells pro .NET?
Aspose.Cells for .NET je knihovna, která umožňuje vývojářům programově manipulovat s dokumenty Excelu v aplikacích .NET.
### Mohu vyhodnocovat vzorce v Excelu pomocí Aspose.Cells?
Ano! Aspose.Cells můžete použít k výpočtu a vyhodnocení vzorců stejně jako v Excelu.
### Je k dispozici bezplatná zkušební verze pro Aspose.Cells?
Absolutně! Můžete získat bezplatnou zkušební verzi[zde](https://releases.aspose.com/).
### Mohu pomocí Aspose.Cells manipulovat se stávajícími soubory aplikace Excel?
Ano, Aspose.Cells umožňuje načíst existující soubory Excel a upravit je podle potřeby.
### Kde najdu další dokumentaci k Aspose.Cells pro .NET?
Můžete najít komplexní dokumentaci[zde](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
