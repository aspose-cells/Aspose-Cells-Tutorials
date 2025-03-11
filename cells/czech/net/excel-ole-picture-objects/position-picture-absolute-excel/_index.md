---
title: Umístěte obrázek (absolutně) v aplikaci Excel
linktitle: Umístěte obrázek (absolutně) v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak absolutně umístit obrázky v Excelu pomocí Aspose.Cells for .NET pomocí tohoto komplexního podrobného tutoriálu.
weight: 13
url: /cs/net/excel-ole-picture-objects/position-picture-absolute-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Umístěte obrázek (absolutně) v aplikaci Excel

## Zavedení
Stalo se vám někdy, že jste se potýkali se správným umístěním obrázků v excelové tabulce? Nejsi sám! Mnoho uživatelů čelí této výzvě, zejména když jejich potřeby vizualizace dat vyžadují absolutní umístění pro lepší estetiku nebo přehlednost. Nehledejte dál; tato příručka vás provede přímočarým procesem umístění obrázků absolutně do listu aplikace Excel pomocí Aspose.Cells pro .NET. Ať už jste vývojář pracující na manipulaci s Excelem, nebo datový analytik, který chce vylepšit své sestavy, náš podrobný návod je zde, aby vám zjednodušil práci s Excelem pomocí obrázků!
## Předpoklady
Než se ponoříte do kódu a specifikací, musíte mít připraveno několik věcí:
1.  Knihovna Aspose.Cells: Ujistěte se, že máte nejnovější verzi knihovny Aspose.Cells for .NET. Můžete si jej stáhnout z[stránka vydání](https://releases.aspose.com/cells/net/).
2. Vývojové prostředí: Ujistěte se, že máte nastavené funkční vývojové prostředí .NET. Můžete použít Visual Studio nebo jakékoli jiné IDE dle vašeho výběru.
3. Základní znalost C#: Pro pochopení úryvků kódu vám pomůže znalost programovacího jazyka C#.
4. Soubor obrázku: Uložte soubor obrázku (např. „logo.jpg“) ve vámi určeném adresáři dokumentů, který chcete vložit do listu aplikace Excel.

## Importujte balíčky
Abychom mohli začít, ujistěte se, že importujeme potřebné balíčky pro náš projekt. Váš projektový soubor by měl obsahovat následující jmenné prostory:
```csharp
using System.IO;
using Aspose.Cells;
```
Importem těchto jmenných prostorů zajišťujeme, že náš program může využívat funkce poskytované Aspose.Cells.
Pojďme si to pro přehlednost rozdělit na zvládnutelné kroky.
## Krok 1: Nastavte adresář dokumentů
tomto úvodním kroku musíte definovat adresář, kde jsou umístěny vaše dokumenty. To je nezbytné, aby program věděl, kam uložit nebo načíst soubory. Můžete to nastavit takto:
```csharp
string dataDir = "Your Document Directory";
```
 Jednoduše vyměnit`"Your Document Directory"` se skutečnou cestou, kde se nachází váš soubor obrázku. Může to být něco podobného`"C:\\Users\\YourUsername\\Documents\\"`.
## Krok 2: Vytvoření instance objektu sešitu
 Dále musíte vytvořit novou instanci souboru`Workbook` třída. Tento objekt představuje váš soubor Excel:
```csharp
Workbook workbook = new Workbook();
```
V tomto okamžiku máte sešit připravený k naplnění daty a obrázky.
## Krok 3: Přidání nového listu
Nyní, když máte sešit, musíte k němu přidat list. Zde se stane kouzlo přidávání a umísťování obrázků:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
 Tento řádek vytvoří nový list ve vašem sešitu a vrátí jeho index, který uložíme do proměnné`sheetIndex`.
## Krok 4: Získání nového listu
Podívejme se na nově vytvořený pracovní list. Pomocí indexu, který jsme právě získali, můžeme přistupovat k listu a manipulovat s ním:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
 Nyní můžete pracovat s`worksheet` objekt pro přidání obsahu, včetně obrázků.
## Krok 5: Přidání obrázku
Nyní k té vzrušující části! Zde přidáme obrázek do našeho pracovního listu. Určíme indexy řádků a sloupců, kam chceme obrázek ukotvit (v tomto případě do buňky „F6“, což je řádek 5 a sloupec 5):
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Tento řádek efektivně uzamkne obrázek na určeném místě vzhledem k celému listu. V současné době však stále podléhá změně velikosti spolu s buňkami.
## Krok 6: Přístup k nově přidanému obrázku
Chcete-li s obrázkem dále manipulovat, musíte získat přístup k jeho vlastnostem:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Díky tomu získáte přístup k vlastnostem obrázku, který jsme právě přidali!
## Krok 7: Nastavení absolutní polohy pro obrázek
 Chcete-li umístit obrázek absolutně (v pixelech), budete muset definovat jeho polohu pomocí`Left` a`Top` vlastnosti. Zde budete mít kontrolu nad tím, kde se obrázek zobrazí:
```csharp
picture.Left = 60;
picture.Top = 10;
```
Obě hodnoty můžete upravit podle potřeby; představují horizontální a vertikální umístění obrazu.
## Krok 8: Uložení souboru Excel
Nakonec, po provedení všech úprav, je čas sešit uložit:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
 Tím se vytvoří soubor aplikace Excel s názvem`book1.out.xls` ve vašem dříve definovaném adresáři dokumentů, který obsahuje váš pracovní list s absolutně umístěným obrázkem.

## Závěr
A tady to máte! Úspěšně jste umístili obrázek do listu aplikace Excel s absolutním umístěním pomocí Aspose.Cells for .NET. Tento přímočarý proces nejen vylepšuje vizuální prezentaci vašich dokumentů aplikace Excel, ale také zajišťuje, že obrázky zůstanou přesně tam, kde je chcete – bez ohledu na jakékoli změny velikosti buněk a výšek řádků. Nyní, ať už připravujete zprávu nebo vytváříte řídicí panel, můžete zajistit, aby byly vaše obrázky pokaždé perfektně umístěny.
## FAQ
### Co je Aspose.Cells pro .NET?
Aspose.Cells for .NET je knihovna .NET, která umožňuje vývojářům vytvářet, manipulovat a převádět tabulky aplikace Excel programově bez potřeby aplikace Microsoft Excel.
### Mohu pomocí Aspose.Cells provádět jiné manipulace s obrázky?
Ano, kromě umístění můžete také měnit velikost, otáčet a upravovat obrázky v tabulkách aplikace Excel pomocí knihovny Aspose.Cells.
### Je Aspose.Cells zdarma k použití?
 Aspose.Cells je komerční produkt, ale můžete začít s bezplatnou zkušební verzí, která je na nich k dispozici[zkušební stránka zdarma](https://releases.aspose.com/).
### Jak získám dočasnou licenci pro Aspose.Cells?
 O dočasnou licenci můžete požádat prostřednictvím[dočasná licenční stránka](https://purchase.aspose.com/temporary-license/) poskytuje Aspose.
### Kde najdu další příklady a dokumentaci?
 The[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/) obsahuje rozsáhlé zdroje, včetně příkladů kódu a podrobnějších funkcí.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
