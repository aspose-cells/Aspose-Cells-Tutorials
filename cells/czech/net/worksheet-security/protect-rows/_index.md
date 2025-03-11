---
title: Chraňte řádky v listu pomocí Aspose.Cells
linktitle: Chraňte řádky v listu pomocí Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se chránit řádky v listu aplikace Excel pomocí Aspose.Cells for .NET. Zabezpečte svá data pomocí ochrany na úrovni řádků a zabraňte náhodným změnám.
weight: 18
url: /cs/net/worksheet-security/protect-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chraňte řádky v listu pomocí Aspose.Cells

## Zavedení
Programová práce se soubory Excelu je často úkol, který vyžaduje nejen manipulaci s daty, ale také ochranu dat. Ať už potřebujete chránit citlivá data nebo zabránit náhodným úpravám, ochrana řádků v listu může být zásadním krokem. V tomto tutoriálu se ponoříme do toho, jak chránit konkrétní řádky v listu aplikace Excel pomocí Aspose.Cells for .NET. Projdeme všemi nezbytnými kroky, od přípravy vašeho prostředí až po implementaci ochranných funkcí jednoduchým a srozumitelným způsobem.
## Předpoklady
Než budete moci začít chránit řádky v listu, musíte mít připraveno několik věcí:
1.  Aspose.Cells for .NET: Ujistěte se, že máte na svém vývojovém počítači nainstalovaný Aspose.Cells for .NET. Pokud jste to ještě neudělali, můžete si jej snadno stáhnout z[Stránka ke stažení Aspose Cells](https://releases.aspose.com/cells/net/).
2. Visual Studio nebo libovolné .NET IDE: Pro implementaci řešení je potřeba mít nastavené vývojové prostředí. Visual Studio je skvělá volba, ale bude fungovat jakékoli IDE kompatibilní s .NET.
3. Základní znalosti C#: Pochopení základů programování v C# vám pomůže postupovat společně s výukovým programem a upravit ukázkový kód tak, aby vyhovoval vašim potřebám.
4.  Aspose.Cells API dokumentace: Seznamte se s[Aspose.Cells pro dokumentaci .NET](https://reference.aspose.com/cells/net/) získat přehled o struktuře tříd a metodách používaných v knihovně.
Pokud máte všechny potřebné předpoklady, můžeme se vrhnout přímo na implementaci.
## Importujte balíčky
Chcete-li začít, musíte importovat požadované balíčky. Tyto knihovny jsou klíčové pro interakci se soubory aplikace Excel ve vašem projektu C#.
```csharp
using System.IO;
using Aspose.Cells;
```
Jakmile naimportujete potřebné balíčky, můžete začít kódovat. 
Nyní si tento proces rozdělíme na menší kroky, aby bylo pro vás velmi snadné jej sledovat. Každý krok se zaměří na určitou část implementace, což zajistí, že ji rychle pochopíte a použijete. 
## Krok 1: Vytvořte nový sešit a pracovní list
Než budete moci použít nastavení ochrany, musíte vytvořit nový sešit a vybrat list, se kterým chcete pracovat. Toto bude váš pracovní dokument.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Vytvořte nový sešit.
Workbook wb = new Workbook();
// Vytvořte objekt listu a získejte první list.
Worksheet sheet = wb.Worksheets[0];
```
V tomto příkladu vytváříme nový sešit s jedním listem (což je výchozí nastavení, když vytváříte nový sešit pomocí Aspose.Cells). Poté vezmeme první list v sešitu, který bude cílem naší ochrany řádku.
## Krok 2: Definujte objekty Styl a StyleFlag
Dalším krokem je definování objektů stylu a příznaku stylu. Tyto objekty umožňují upravit vlastnosti buňky, například zda je zamčená nebo odemčená.
```csharp
// Definujte objekt stylu.
Style style;
// Definujte objekt styleflag.
StyleFlag flag;
```
Tyto objekty použijete v pozdějších krocích k přizpůsobení vlastností buňky a jejich použití v listu.
## Krok 3: Odemkněte všechny sloupce v listu
Ve výchozím nastavení jsou všechny buňky v listu aplikace Excel uzamčeny. Když však chráníte list, je vynucován stav uzamčení. Chcete-li zajistit, aby byly chráněny pouze určité řádky nebo buňky, můžete nejprve odemknout všechny sloupce. Tento krok je nezbytný, pokud chcete chránit pouze určité řádky.
```csharp
// Projděte všechny sloupce v listu a odemkněte je.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
 V tomto kódu procházíme všech 256 sloupců v listu (tabulky Excelu mají maximálně 256 sloupců, indexovaných od 0 do 255) a nastavujeme jejich`IsLocked` majetek do`false`. Tato akce zajistí, že všechny sloupce budou odemčeny, ale určité řádky později zamkneme.
## Krok 4: Zamkněte první řadu
Po odemknutí sloupců je dalším krokem uzamčení konkrétních řádků, které chcete chránit. V tomto příkladu zamkneme první řádek. To zajišťuje, že jej uživatelé nemohou upravovat, zatímco ostatní řádky zůstanou odemčené.
```csharp
//Získejte styl první řady.
style = sheet.Cells.Rows[0].Style;
// Zamkněte to.
style.IsLocked = true;
//Vytvořte vlajku.
flag = new StyleFlag();
// Nastavte nastavení zámku.
flag.Locked = true;
// Použijte styl na první řádek.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Zde přistoupíme ke stylu prvního řádku a nastavíme jej`IsLocked` majetek do`true` . Poté použijeme`ApplyRowStyle()` metoda pro použití stylu zámku na celý řádek. Tento krok můžete opakovat a uzamknout další řádky, které chcete chránit.
## Krok 5: Chraňte list
Nyní, když jsme odemkli a zamkli potřebné řádky, je čas chránit list. Ochrana zajišťuje, že nikdo nemůže upravit zamčené řádky nebo buňky, pokud neodstraní heslo ochrany (je-li poskytnuto).
```csharp
// Chraňte list.
sheet.Protect(ProtectionType.All);
```
 V tomto kroku aplikujeme ochranu na celý list pomocí`ProtectionType.All`. Tento typ ochrany znamená, že jsou chráněny všechny aspekty listu, včetně zamčených řádků a buněk. Tuto ochranu můžete také přizpůsobit zadáním různých typů ochrany v případě potřeby.
## Krok 6: Uložte sešit
Nakonec musíme sešit uložit po použití potřebných stylů a ochrany. Sešit lze uložit v různých formátech, např. Excel 97-2003, Excel 2010 atd.
```csharp
// Uložte soubor aplikace Excel.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Tento řádek kódu uloží sešit ve formátu Excel 97-2003 s použitými změnami. Formát souboru můžete změnit podle svých potřeb výběrem z řady`SaveFormat` možnosti.
## Závěr
A tady to máte! Úspěšně jste se naučili, jak chránit řádky v listu pomocí Aspose.Cells for .NET. Podle výše uvedených kroků můžete podle potřeby odemknout nebo zamknout libovolné řádky nebo sloupce a použít ochranu pro zajištění integrity vašich dat.
## FAQ
### Jak mohu chránit více řádků najednou?  
 Můžete procházet více řádky a použít styl zamykání na každý jednotlivě. Jednoduše vyměnit`0` s indexem řádku, který chcete zamknout.
### Mohu nastavit heslo pro ochranu listu?  
 Ano! Můžete předat heslo do`sheet.Protect()` způsob vynucení ochrany heslem.
### Mohu odemknout buňky místo celých sloupců?  
Ano! Místo odemykání sloupců můžete odemknout jednotlivé buňky úpravou jejich vlastností stylu.
### Co se stane, když se pokusím upravit chráněný řádek?  
Když je řádek chráněný, Excel zabrání provádění jakýchkoli úprav v uzamčených buňkách, pokud nezrušíte ochranu listu.
### Mohu chránit konkrétní rozsahy v řadě?  
 Ano! Jednotlivé rozsahy v řadě můžete uzamknout nastavením`IsLocked` vlastnost pro konkrétní buňky v rozsahu.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
