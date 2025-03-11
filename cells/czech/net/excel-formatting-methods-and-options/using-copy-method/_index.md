---
title: Použití metody kopírování programově v aplikaci Excel
linktitle: Použití metody kopírování programově v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se používat metodu kopírování v Aspose.Cells for .NET k efektivní manipulaci se soubory aplikace Excel. Včetně průvodce krok za krokem.
weight: 10
url: /cs/net/excel-formatting-methods-and-options/using-copy-method/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Použití metody kopírování programově v aplikaci Excel

## Zavedení
Pokud jde o programovou správu a manipulaci s tabulkami, Aspose.Cells for .NET je výkonný nástroj, který vám může ušetřit čas a zefektivnit váš pracovní postup. Jedním z běžných úkolů, kterým vývojáři čelí, je potřeba kopírovat rozsahy z jednoho listu do druhého v sešitu aplikace Excel. V tomto tutoriálu vás provedeme pomocí metody Copy v Aspose.Cells a provedeme vás každým krokem s jasnými vysvětleními a příklady kódu.
## Předpoklady
Než se vrhneme na kroky použití metody Kopírovat, musíte se ujistit, že máte splněny následující předpoklady:
1. .NET Framework: Ujistěte se, že máte na svém počítači nainstalované rozhraní .NET Framework. Aspose.Cells je kompatibilní s různými verzemi, takže je zkontrolujte[dokumentace](https://reference.aspose.com/cells/net/) pro upřesnění.
2. Visual Studio: Je nezbytné mít Visual Studio nebo jakékoli kompatibilní IDE nastavené pro vývoj .NET. To vám pomůže pohodlně vytvářet a spravovat vaše projekty.
3.  Knihovna Aspose.Cells: Stáhněte si knihovnu Aspose.Cells z[stránka vydání](https://releases.aspose.com/cells/net/) a přidejte na něj odkaz do svého projektu.
4.  Ukázkový soubor Excel: Vytvořte nebo mějte připravený soubor Excel (např.`Book1.xlsx`), se kterými budete pracovat v tomto tutoriálu.
5. Základní znalost C#: Znalost konceptů a syntaxe jazyka C#.
Jakmile jsou tyto předpoklady splněny, můžete začít kódovat!
## Importujte balíčky
Abyste mohli využívat funkce poskytované Aspose.Cells, musíte importovat potřebné balíčky. Ve svém projektu C# se ujistěte, že jste v horní části souboru kódu zahrnuli následující direktivu using:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
To vám umožní přístup ke třídám a metodám potřebným pro snadnou manipulaci se soubory aplikace Excel.
Nyní, když máte vše na svém místě, pojďme si rozdělit proces používání metody Copy do zvládnutelných kroků. Začneme načtením souboru aplikace Excel a poté zkopírujeme požadovaný rozsah.
## Krok 1: Nastavení streamování souborů
Prvním krokem je vytvořit souborový proud, který nám umožní otevřít a pracovat s naším souborem Excel. Postup je následující:
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvoření datového proudu souboru obsahujícího soubor Excel, který se má otevřít
FileStream fstream = new FileStream(dataDir + "Book1.xlsx", FileMode.Open);
```
 V tomto kódu musíte zadat cestu, kde je vaše`Book1.xlsx` soubor se nachází. The`FileMode.Open` parametr označuje, že chceme otevřít existující soubor.
## Krok 2: Otevření sešitu
Dále vytvoříme objekt Workbook pomocí streamu souborů, který jsme právě nastavili. To nám umožňuje přístup k obsahu souboru Excel.
```csharp
// Otevření souboru aplikace Excel prostřednictvím datového proudu souborů
Workbook workbook = new Workbook(fstream);
```
V tuto chvíli jsme sešit otevřeli a můžeme začít pracovat s jeho obsahem.
## Krok 3: Přístup k listu
Jakmile je sešit načten, musíme získat přístup ke konkrétnímu listu, se kterým chceme pracovat. Obvykle to bude první list v sešitu.
```csharp
// Přístup k prvnímu listu v souboru aplikace Excel
Worksheet worksheet = workbook.Worksheets[0];
```
 Zde,`Worksheets[0]` popadne první list. Pokud chcete získat přístup k jakémukoli jinému listu, jednoduše změňte index.
## Krok 4: Kopírování rozsahu
Nyní přichází hlavní část – kopírování rozsahu buněk. V tomto tutoriálu si ukážeme, jak zkopírovat nastavení podmíněného formátování z jedné buňky do druhé, a také jak zkopírovat celý rozsah listu aplikace Excel.
### Kopírování podmíněného formátování (příklad)
```csharp
// Kopírování nastavení podmíněného formátu z buňky "A1" do buňky "B1"
// list.CopyConditionalFormatting(0, 0, 0, 1);
```
Tento řádek je v původním kódu zakomentován, ale ukazuje, jak zkopírovat podmíněné formátování z buňky A1 do buňky B1 na stejném listu. Parametry představují řádkové a sloupcové indexy zdrojových a cílových buněk. Pokud tuto funkci potřebujete, můžete jej odkomentovat.
### Kopírování celého rozsahu (příklad)
Naši funkcionalitu kopírování můžeme dále rozšířit tak, aby zahrnovala kopírování celého rozsahu, u kterého pomocí smyčky projdeme všechny listy.
```csharp
int TotalRowCount = 0;
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    // Přístup ke každému listu
    Worksheet sourceSheet = workbook.Worksheets[i];
    // Získání rozsahu zobrazení v pracovním listu
    Range sourceRange = sourceSheet.Cells.MaxDisplayRange;
    // Vytvoření rozsahu v cílovém listu
    Range destRange = worksheet.Cells.CreateRange(
        sourceRange.FirstRow + TotalRowCount,
        sourceRange.FirstColumn,
        sourceRange.RowCount,
        sourceRange.ColumnCount);
    // Kopírování zdrojového rozsahu do cílového rozsahu
    destRange.Copy(sourceRange);
    // Aktualizace celkového počtu řádků pro další iteraci smyčky
    TotalRowCount += sourceRange.RowCount; 
}
```
## Krok 5: Uložení upraveného sešitu
Po zkopírování požadovaných rozsahů budete chtít upravený sešit uložit, abyste zachovali své změny. Zde je postup:
```csharp
// Uložení upraveného souboru Excel
workbook.Save(dataDir + "output.xls");
```
 Tento kód uloží váš upravený sešit jako`output.xls` ve vámi zadaném adresáři. Ujistěte se, že jste vybrali vhodný formát, který vyhovuje vašim potřebám. 
## Krok 6: Zavření streamu souborů
A konečně, abychom zajistili, že uvolníme systémové prostředky, musíme zavřít proud souborů, který jsme původně otevřeli.
```csharp
// Zavřením datového proudu souborů uvolníte všechny zdroje
fstream.Close();
```
právě tak jste úspěšně dokončili proces kopírování rozsahů a uložení aktualizovaného souboru Excel!
## Závěr
Použití metody Copy v Aspose.Cells for .NET vám poskytuje výkonné možnosti pro snadnou manipulaci se soubory aplikace Excel. Podle tohoto podrobného průvodce můžete efektivně kopírovat rozsahy buněk a podmíněné formátování z jednoho listu do druhého a zjednodušit tak své úlohy správy dat. 
## FAQ
### Co je Aspose.Cells pro .NET?
Aspose.Cells for .NET je knihovna, která umožňuje vývojářům vytvářet, manipulovat a spravovat soubory Excelu programově v aplikacích .NET.
### Mohu kopírovat formáty, vzorce a hodnoty pomocí Aspose.Cells?
Ano, Aspose.Cells umožňuje kopírovat nejen hodnoty, ale také formáty a vzorce mezi rozsahy.
### Je Aspose.Cells zdarma k použití?
 Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro další používání je nutné zakoupit licenci. Více informací naleznete[zde](https://purchase.aspose.com/buy).
### Jak mohu získat podporu, pokud narazím na problémy?
 Pomoc můžete vyhledat prostřednictvím nalezeného fóra podpory Aspose[zde](https://forum.aspose.com/c/cells/9).
### Kde si mohu stáhnout knihovnu Aspose.Cells?
 Knihovnu si můžete stáhnout ze stránky vydání[zde](https://releases.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
