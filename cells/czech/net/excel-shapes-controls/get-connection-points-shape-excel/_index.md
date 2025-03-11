---
title: Získejte spojovací body tvaru v aplikaci Excel
linktitle: Získejte spojovací body tvaru v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak získat spojovací body tvaru v Excelu pomocí Aspose.Cells pro .NET. Postupujte podle našeho podrobného průvodce, abyste mohli snadno extrahovat a programově zobrazovat body tvaru.
weight: 11
url: /cs/net/excel-shapes-controls/get-connection-points-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Získejte spojovací body tvaru v aplikaci Excel

## Zavedení
Při programové práci se soubory Excelu často potřebujeme pracovat s tvary vloženými do listů. Jedním z pokročilejších úkolů, které můžete provést, je extrahování spojovacích bodů z tvaru. Spojovací body se používají k připojení tvarů pomocí spojek a přesnější správě jejich rozložení. Pokud chcete získat spojovací body tvaru v aplikaci Excel, Aspose.Cells for .NET je nástroj, který potřebujete. V tomto tutoriálu vás krok za krokem provedeme procesem, jak toho dosáhnout.
## Předpoklady
Než se ponoříte do kódu, ujistěte se, že máte následující předpoklady:
- Aspose.Cells for .NET: Budete muset mít Aspose.Cells nainstalované ve svém vývojovém prostředí. Pokud ho ještě nemáte, můžete[stáhněte si nejnovější verzi zde](https://releases.aspose.com/cells/net/).
- Vývojové prostředí: Ujistěte se, že máte funkční instalaci sady Visual Studio nebo jiného IDE kompatibilního s .NET.
- Základní znalost C#: Tento tutoriál předpokládá, že máte základní znalosti o programování v C# a objektově orientovaných principech.
 Můžete se také přihlásit do a[bezplatná zkušební verze Aspose.Cells](https://releases.aspose.com/) pokud jste to ještě neudělali. To vám umožní přístup ke všem funkcím požadovaným pro tuto příručku.

## Importujte balíčky
Chcete-li ve svém projektu pracovat s Aspose.Cells, musíte zahrnout potřebné jmenné prostory. Následující příkazy importu by měly být umístěny v horní části kódu:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Tyto jmenné prostory vám umožňují přístup k základním funkcím Aspose.Cells a umožňují vám manipulovat s listy a tvary.

## Průvodce krok za krokem k získání spojovacích bodů tvaru
této části vás provedeme tím, jak extrahovat spojovací body tvaru v listu aplikace Excel. Pečlivě dodržujte každý krok pro jasné pochopení.
## Krok 1: Vytvořte nový sešit
 Nejprve musíme vytvořit instanci`Workbook` třída. To představuje soubor aplikace Excel v Aspose.Cells. Pokud nemáte existující soubor, žádný problém – můžete začít s prázdným sešitem.
```csharp
// Vytvořte nový sešit
Workbook workbook = new Workbook();
```
 V tomto kroku jsme vytvořili prázdný sešit aplikace Excel, ale můžete také načíst existující sešit tak, že předáte cestu k souboru`Workbook` konstruktér.
## Krok 2: Otevřete první list
Dále musíme přistoupit k listu, kde chceme pracovat s tvary. V tomto případě použijeme první list sešitu.
```csharp
// Získejte první pracovní list v sešitu
Worksheet worksheet = workbook.Worksheets[0];
```
 Tento řádek přistupuje k prvnímu listu z kolekce listů v sešitu. Pokud pracujete s konkrétním listem, můžete index nahradit`0` s požadovaným indexem.
## Krok 3: Přidejte nové textové pole (tvar)
Nyní do listu přidáme nový tvar. Vytvoříme textové pole, což je typ tvaru. Můžete také přidat jiné typy tvarů, ale pro jednoduchost v tomto tutoriálu zůstaneme u textového pole.
```csharp
// Přidejte do kolekce nové textové pole
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Zde je to, co jsme udělali:
-  Přidáno textové pole na řádek`2` , sloupec`1`.
-  Nastavte rozměry textového pole na`160` jednotky na šířku a`200` jednotky na výšku.
## Krok 4: Přístup k Shape z kolekce Shapes
 Jakmile přidáme textové pole, stane se součástí kolekce tvarů listu. Nyní k tomuto tvaru přistoupíme pomocí`Shapes`sbírka.
```csharp
// Přístup k tvaru (textovému poli) z kolekce tvarů
Shape shape = workbook.Worksheets[0].Shapes[0];
```
V tomto kroku načteme první tvar (naše textové pole) z kolekce. Pokud máte více tvarů, můžete určit index nebo dokonce najít tvar podle názvu.
## Krok 5: Načtěte spojovací body
Nyní, když máme svůj tvar, pojďme extrahovat jeho spojovací body. Tyto body se používají pro připojení konektorů ke tvaru. The`ConnectionPoints` vlastnost tvaru vrátí všechny dostupné spojovací body.
```csharp
// Získejte všechny spojovací body v tomto tvaru
var connectionPoints = shape.ConnectionPoints;
```
To nám dává sbírku všech spojovacích bodů dostupných pro daný tvar.
## Krok 6: Zobrazte body připojení
Nakonec chceme zobrazit souřadnice každého bodu připojení. Zde procházíme body připojení a vytiskneme je do konzole.
```csharp
// Zobrazte všechny body tvaru
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
 Tato smyčka iteruje přes každý bod připojení a vytiskne`X` a`Y` souřadnice. To může být užitečné pro ladění nebo vizuální potvrzení spojovacích bodů tvaru.
## Krok 7: Proveďte a dokončete
Jakmile nastavíte všechny výše uvedené kroky, můžete spustit kód. Zde je poslední řádek, který zajišťuje úspěšné dokončení procesu:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Tento řádek jednoduše zaznamená do konzole zprávu o dokončení procesu.

## Závěr
V tomto tutoriálu jsme se zabývali tím, jak načíst spojovací body tvaru v aplikaci Excel pomocí Aspose.Cells pro .NET. Rozdělením úkolu na malé, stravitelné kroky jsme prozkoumali proces vytváření sešitu, přidání tvaru a extrahování spojovacích bodů.
Když pochopíte, jak programově manipulovat s tvary, odemknete svět možností vytváření dynamických a interaktivních tabulek Excelu. Ať už vytváříte sestavy, navrhujete řídicí panely nebo vytváříte diagramy, tyto znalosti se vám budou hodit.
## FAQ
### Co je spojovací bod ve tvaru?
Spojovací bod je konkrétní bod na tvaru, ke kterému můžete připojit konektory nebo jej propojit s jinými tvary.
### Mohu načíst spojovací body pro všechny obrazce v listu?
Ano, Aspose.Cells vám umožňuje získat spojovací body pro jakýkoli tvar, který je podporuje. Jednoduše procházejte kolekci tvarů v listu.
### Potřebuji licenci k používání Aspose.Cells?
Ano, i když to můžete vyzkoušet zdarma, pro plné funkce je vyžadována licence. Můžete[koupit licenci zde](https://purchase.aspose.com/buy)nebo získat a[dočasná licence](https://purchase.aspose.com/temporary-license/).
### Jak mohu do Aspose.Cells přidat různé typy tvarů?
Můžete použít`Add` metoda pro tvary, jako jsou obdélníky, elipsy a další. Každý tvar má specifické parametry, které si můžete přizpůsobit.
### Jak načtu stávající soubor aplikace Excel namísto vytvoření nového?
 Chcete-li načíst existující soubor, předejte cestu k souboru`Workbook` konstruktor, takto:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
