---
"description": "Naučte se, jak získat body spojení tvarů v Excelu pomocí Aspose.Cells pro .NET. Postupujte podle našeho podrobného návodu, jak snadno programově extrahovat a zobrazit body tvarů."
"linktitle": "Získání spojovacího bodu tvaru v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Získání spojovacího bodu tvaru v Excelu"
"url": "/cs/net/excel-shapes-controls/get-connection-points-shape-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Získání spojovacího bodu tvaru v Excelu

## Zavedení
Při programově práci s excelovými soubory často potřebujeme interagovat s tvary vloženými v listech. Jedním z pokročilejších úkolů, které můžete provádět, je extrahování spojovacích bodů z tvaru. Spojovací body se používají k propojení tvarů pomocí spojnic a k přesnější správě jejich rozvržení. Pokud chcete v Excelu získat spojovací body tvaru, Aspose.Cells pro .NET je nástroj, který potřebujete. V tomto tutoriálu vás krok za krokem provedeme procesem, jak toho dosáhnout.
## Předpoklady
Než se ponoříte do kódu, ujistěte se, že máte následující předpoklady:
- Aspose.Cells pro .NET: Budete muset mít ve svém vývojovém prostředí nainstalovaný Aspose.Cells. Pokud ho ještě nemáte, můžete [stáhněte si nejnovější verzi zde](https://releases.aspose.com/cells/net/).
- Vývojové prostředí: Ujistěte se, že máte funkční instalaci Visual Studia nebo jiného IDE kompatibilního s .NET.
- Základní znalost jazyka C#: Tento tutoriál předpokládá, že máte základní znalosti programování v jazyce C# a principů objektově orientovaného jazyka.
Můžete se také přihlásit k [bezplatná zkušební verze Aspose.Cells](https://releases.aspose.com/) pokud jste tak ještě neučinili. Tím získáte přístup ke všem funkcím potřebným pro tuto příručku.

## Importovat balíčky
Abyste mohli ve svém projektu pracovat s Aspose.Cells, musíte zahrnout potřebné jmenné prostory. Následující příkazy importu by měly být umístěny na začátek kódu:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Tyto jmenné prostory vám poskytují přístup k základním funkcím Aspose.Cells a umožňují vám manipulovat s listy a tvary.

## Podrobný návod k získání spojovacího bodu tvaru
V této části si ukážeme, jak extrahovat spojovací body tvaru v listu aplikace Excel. Pro jasné pochopení pečlivě dodržujte každý krok.
## Krok 1: Vytvoření instance nového sešitu
Nejdříve musíme vytvořit instanci `Workbook` třída. Toto představuje soubor aplikace Excel v Aspose.Cells. Pokud nemáte existující soubor, žádný problém – můžete začít s prázdným sešitem.
```csharp
// Vytvořit instanci nového sešitu
Workbook workbook = new Workbook();
```
V tomto kroku jsme vytvořili prázdný sešit aplikace Excel, ale můžete také načíst existující sešit předáním cesty k souboru. `Workbook` konstruktér.
## Krok 2: Přístup k prvnímu pracovnímu listu
Dále potřebujeme přístup k listu, kde chceme pracovat s tvary. V tomto případě použijeme první list sešitu.
```csharp
// Získejte první list v sešitu
Worksheet worksheet = workbook.Worksheets[0];
```
Tento řádek přistupuje k prvnímu listu z kolekce listů v sešitu. Pokud pracujete s konkrétním listem, můžete nahradit index `0` s požadovaným indexem.
## Krok 3: Přidání nového textového pole (tvaru)
Nyní přidáme do listu nový tvar. Vytvoříme textové pole, což je typ tvaru. Můžete přidat i jiné typy tvarů, ale pro jednoduchost se v tomto tutoriálu držíme textového pole.
```csharp
// Přidat do kolekce nové textové pole
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Zde je to, co jsme udělali:
- Přidáno textové pole na řádek `2`, sloupec `1`.
- Nastavte rozměry textového pole na `160` jednotky na šířku a `200` jednotek na výšku.
## Krok 4: Získejte přístup k tvaru z kolekce tvarů
Jakmile přidáme textové pole, stane se součástí kolekce tvarů v listu. Nyní k tomuto tvaru budeme přistupovat pomocí `Shapes` sbírka.
```csharp
// Přístup k tvaru (textovému poli) z kolekce tvarů
Shape shape = workbook.Worksheets[0].Shapes[0];
```
V tomto kroku načteme první tvar (naše textové pole) z kolekce. Pokud máte více tvarů, můžete zadat index nebo dokonce vyhledat tvar podle názvu.
## Krok 5: Načtení bodů připojení
Nyní, když máme tvar, pojďme extrahovat jeho spojovací body. Tyto body se používají k připojení spojnic k tvaru. `ConnectionPoints` Vlastnost tvaru vrací všechny dostupné body připojení.
```csharp
// Získejte všechny spojovací body v tomto tvaru
var connectionPoints = shape.ConnectionPoints;
```
To nám dává kolekci všech dostupných spojovacích bodů pro daný tvar.
## Krok 6: Zobrazení bodů připojení
Nakonec chceme zobrazit souřadnice každého bodu připojení. Zde procházíme body připojení a vypíšeme je do konzole.
```csharp
// Zobrazit všechny body tvaru
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
Tato smyčka iteruje přes každý bod připojení a vypíše `X` a `Y` souřadnice. To může být užitečné pro ladění nebo vizuální potvrzení bodů spojení tvaru.
## Krok 7: Provést a dokončit
Jakmile nastavíte všechny výše uvedené kroky, můžete spustit kód. Zde je poslední řádek, který zajišťuje úspěšné dokončení procesu:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Tento řádek jednoduše zaznamená do konzole zprávu oznamující, že proces byl dokončen.

## Závěr
tomto tutoriálu jsme se popsali, jak načíst spojovací body tvaru v Excelu pomocí Aspose.Cells pro .NET. Rozdělením úkolu na malé, srozumitelné kroky jsme prozkoumali proces vytvoření sešitu, přidání tvaru a extrakce spojovacích bodů.
Pochopením toho, jak programově manipulovat s tvary, se vám otevírá svět možností pro vytváření dynamických a interaktivních excelových listů. Ať už vytváříte sestavy, navrhujete řídicí panely nebo diagramy, tyto znalosti se vám budou hodit.
## Často kladené otázky
### Co je to spojovací bod v obrazci?
Spojovací bod je konkrétní bod na tvaru, ke kterému můžete připojit spojnice nebo jej propojit s jinými tvary.
### Mohu načíst spojovací body pro všechny tvary v listu?
Ano, Aspose.Cells umožňuje načíst body připojení pro jakýkoli tvar, který je podporuje. Jednoduše projděte kolekci tvarů v pracovním listu.
### Potřebuji licenci k používání Aspose.Cells?
Ano, i když si to můžete vyzkoušet zdarma, pro všechny funkce je vyžadována licence. Můžete [koupit licenci zde](https://purchase.aspose.com/buy) nebo si pořiďte [dočasná licence](https://purchase.aspose.com/temporary-license/).
### Jak mohu do Aspose.Cells přidat různé typy tvarů?
Můžete použít `Add` metoda pro tvary jako obdélníky, elipsy a další. Každý tvar má specifické parametry, které si můžete přizpůsobit.
### Jak načtu existující soubor aplikace Excel místo vytvoření nového?
Chcete-li načíst existující soubor, předejte mu cestu k souboru. `Workbook` konstruktor, takto:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}