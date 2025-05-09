---
"description": "Naučte se, jak extrahovat text z prvku SmartArt s ozubeným kolem v Excelu pomocí Aspose.Cells pro .NET. Součástí je podrobný návod a příklad kódu."
"linktitle": "Extrahování textu z inteligentního umění typu ozubeného kola v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Extrahování textu z inteligentního umění typu ozubeného kola v Excelu"
"url": "/cs/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z inteligentního umění typu ozubeného kola v Excelu

## Zavedení
Při práci s Excelem se můžete setkat s grafikami SmartArt, které vám pomohou sdělit vaše sdělení vizuálně přitažlivým způsobem. Mezi těmito grafikami je SmartArt ve tvaru ozubeného kola oblíbený pro své hierarchické a směrové toky a často se používá v projektovém řízení nebo modelování systémů. Co když ale potřebujete programově extrahovat text z těchto tvarů? A právě zde se hodí Aspose.Cells pro .NET! V tomto blogovém příspěvku vás provedeme podrobným návodem, jak extrahovat text z tvarů SmartArt ve tvaru ozubeného kola v Excelu pomocí Aspose.Cells pro .NET.
## Předpoklady
Než se do toho pustíme, je třeba splnit několik základních předpokladů. Nebojte se, je to jednoduché a já vás tím provedu.
### Prostředí .NET
Ujistěte se, že máte v počítači nainstalované vývojové prostředí .NET. Může se jednat o Visual Studio nebo jakékoli vámi zvolené vývojové prostředí (IDE), které podporuje vývoj v .NET.
### Aspose.Cells pro .NET
Dále budete muset nainstalovat knihovnu Aspose.Cells. Jedná se o výkonný nástroj, který vám umožní bezproblémově manipulovat s excelovými soubory. Můžete si ji stáhnout z [Stránka s vydáními Aspose](https://releases.aspose.com/cells/net/)Pokud si to chcete nejdříve prohlédnout, využijte [bezplatná zkušební verze](https://releases.aspose.com/).
### Základní znalost C#
Základní znalost programování v C# je přesně to, co potřebujete k tomuto tutoriálu. Pokud jste v tomto oboru nováčkem, žádný problém – kroky navrhnu tak, aby byly co nejpřívětivější pro začátečníky.
### Ukázkový soubor Excelu
Pro tento tutoriál budete také potřebovat vzorový soubor aplikace Excel, který obsahuje tvary SmartArt s ozubeným kolem. Můžete si snadno vytvořit jeden nebo najít šablonu online. Stačí se ujistit, že SmartArt obsahuje alespoň jeden tvar ozubeného kola.
## Importovat balíčky
Chcete-li začít s kódováním, budete muset importovat potřebné balíčky. Zde je návod, jak to udělat:
### Vytvořit nový projekt
1. Otevřete své vývojové prostředí .NET.
2. Vytvořte nový projekt. Například v možnostech .NET vyberte „Konzolová aplikace“.
3. Pojmenujte svůj projekt a nastavte požadovaný rámec. 
### Přidat reference
Chcete-li použít Aspose.Cells, budete muset do projektu přidat odkazy na knihovny:
1. Klikněte pravým tlačítkem myši na název projektu v Průzkumníku řešení.
2. Vyberte možnost „Spravovat balíčky NuGet“.
3. Vyhledejte „Aspose.Cells“ a nainstalujte jej.
Jakmile je instalace dokončena, můžete začít programovat!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Nyní si rozebereme kód, který použijete k extrakci textu. Uděláme to krok za krokem.
## Krok 1: Nastavení zdrojového adresáře
Začněte definováním adresáře, kde se nachází váš soubor Excel:
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
```
Nezapomeňte vyměnit `"Your Document Directory"` se skutečnou cestou k vašemu souboru aplikace Excel.
## Krok 2: Načtení sešitu aplikace Excel
Dále načteme sešit aplikace Excel. K jeho obsahu se dostaneme takto:
```csharp
// Načtěte ukázkový soubor Excelu obsahující tvar inteligentního grafiky typu ozubené kolo.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Tato část načte váš ukázkový sešit aplikace Excel.
## Krok 3: Přístup k prvnímu pracovnímu listu
Nyní, když jsme načetli sešit, přejděme k prvnímu listu, kde se nachází náš SmartArt:
```csharp
// Zpřístupněte první pracovní list.
Worksheet ws = wb.Worksheets[0];
```
Tím se načte první pracovní list pro další manipulaci.
## Krok 4: Získejte přístup k prvnímu tvaru
Dále potřebujeme přístup k prvnímu tvaru v našem listu. Tímto způsobem se můžeme pohybovat mezi obrázky SmartArt:
```csharp
// Zpřístupněte první tvar.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Zde se zaměřujeme na první tvar, o kterém předpokládáme, že je to SmartArt, který potřebujeme.
## Krok 5: Získejte tvar skupiny
Jakmile máme tvar, je čas získat výsledek naší reprezentace SmartArt:
```csharp
// Získejte výsledek tvaru inteligentního umění typu ozubeného kola ve formě skupinového tvaru.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Tím se náš SmartArt typu ozubeného kola načte jako seskupený tvar.
## Krok 6: Extrahování jednotlivých tvarů
Nyní si vyextrahujeme jednotlivé tvary, které tvoří náš SmartArt:
```csharp
// Získejte seznam jednotlivých tvarů sestávajících ze skupinových tvarů.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Toto pole bude obsahovat všechny jednotlivé tvary, kterými potřebujeme procházet.
## Krok 7: Extrakce a tisk textu
Nakonec můžeme projít pole tvarů a extrahovat text z libovolného tvaru ozubeného kola:
```csharp
// Extrahujte text tvarů typu ozubené kolo a vytiskněte je do konzole.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
V této smyčce kontrolujeme typ tvaru a pokud se jedná o tvar ozubeného kola, vypíšeme text.
## Krok 8: Potvrzení provedení
Nakonec můžete přidat potvrzovací zprávu po úspěšném dokončení procesu:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
Tímto je extrakce dokončena a v konzoli byste měli vidět textový výstup!
## Závěr
Gratulujeme! Právě jste se naučili, jak extrahovat text z tvarů SmartArt ve tvaru ozubeného kola v Excelu pomocí Aspose.Cells pro .NET. Tato šikovná technika otevírá dveře k automatizaci sestav nebo dokumentace, která se spoléhá na vizuální reprezentaci dat. Ať už jste zkušený vývojář, nebo s tím teprve začínáte, ovládání a extrakce informací ze SmartArt může zefektivnit váš pracovní postup a zefektivnit vás. Nezapomeňte si prohlédnout podrobné informace. [Dokumentace k Aspose.Cells](https://reference.aspose.com/cells/net/) pro další schopnosti.
## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET, která umožňuje vývojářům snadno vytvářet a manipulovat s Excelovými soubory.
### Mohu používat Aspose.Cells s jinými jazyky?
Ano! Aspose.Cells je k dispozici v několika programovacích jazycích, včetně Javy a Pythonu.
### Musím si zakoupit Aspose.Cells pro .NET?
Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro delší používání je nutný nákup. Možnosti nákupu naleznete zde [zde](https://purchase.aspose.com/buy).
### Je k dispozici podpora pro uživatele Aspose.Cells?
Rozhodně! Podporu komunity najdete na [Fórum Aspose.Cells](https://forum.aspose.com/c/cells/9).
### Mohu touto metodou extrahovat další typy obrázků SmartArt?
Ano, s drobnými úpravami můžete extrahovat text z různých tvarů SmartArt změnou podmínek v kódu.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}