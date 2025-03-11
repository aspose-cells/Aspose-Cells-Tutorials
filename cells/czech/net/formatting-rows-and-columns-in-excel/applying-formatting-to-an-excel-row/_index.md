---
title: Programové použití formátování na řádek aplikace Excel
linktitle: Programové použití formátování na řádek aplikace Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak programově použít formátování na řádek aplikace Excel pomocí Aspose.Cells for .NET. Tento podrobný průvodce krok za krokem pokrývá vše od zarovnání po okraje.
weight: 11
url: /cs/net/formatting-rows-and-columns-in-excel/applying-formatting-to-an-excel-row/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programové použití formátování na řádek aplikace Excel

## Zavedení
V tomto tutoriálu si projdeme, jak programově použít formátování na řádek Excelu pomocí Aspose.Cells for .NET. Pokryjeme vše od nastavení prostředí až po použití různých možností formátování, jako je barva písma, zarovnání a okraje – to vše při zachování jednoduchého a poutavého obsahu. Pojďme se ponořit!
## Předpoklady
Než začneme, ujistíme se, že spolu s tímto návodem máte vše, co potřebujete. Zde je to, co budete potřebovat:
1.  Aspose.Cells for .NET Library – Můžete si ji stáhnout z[Stránka ke stažení Aspose.Cells for .NET](https://releases.aspose.com/cells/net/).
2. IDE – Jakékoli vývojové prostředí .NET, jako je Visual Studio.
3. Základní znalost C# – Měli byste znát programovací jazyk C# a pracovat s aplikacemi .NET.
Nezapomeňte také nainstalovat nejnovější verzi Aspose.Cells jejím stažením přímo nebo pomocí NuGet Package Manager v sadě Visual Studio.
## Importujte balíčky
Nejprve se ujistěte, že jste importovali potřebné balíčky. To je nezbytné pro přístup k funkcím potřebným pro práci se soubory aplikace Excel a programové použití stylů.
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Po dokončení nastavení jsme připraveni skočit do vzrušující části – formátování řádků!
této části rozebereme jednotlivé kroky procesu. Každý krok bude doprovázen úryvky kódu a podrobným vysvětlením, takže i když jste v Aspose.Cells noví, budete ho moci snadno sledovat.
## Krok 1: Nastavte sešit a pracovní list
Před použitím jakéhokoli formátování musíte vytvořit instanci sešitu a otevřít první list. Je to jako otevřít prázdné plátno, než začnete malovat.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Vytvoření instance objektu sešitu
Workbook workbook = new Workbook();
// Získání odkazu na první (výchozí) list předáním jeho indexu listu
Worksheet worksheet = workbook.Worksheets[0];
```
Zde vytvoříme nový objekt sešitu a načteme první list. Toto je list, kde použijeme naše formátování.
## Krok 2: Vytvořte a přizpůsobte styl
Nyní, když máte list připravený, je dalším krokem definovat styly, které chcete na řádek použít. Začneme vytvořením nového stylu a nastavením vlastností, jako je barva písma, zarovnání a okraje.
```csharp
// Přidání nového stylu ke stylům
Style style = workbook.CreateStyle();
// Nastavení vertikálního zarovnání textu v buňce "A1".
style.VerticalAlignment = TextAlignmentType.Center;
// Nastavení vodorovného zarovnání textu v buňce "A1".
style.HorizontalAlignment = TextAlignmentType.Center;
// Nastavení barvy písma textu v buňce "A1".
style.Font.Color = Color.Green;
```
této části nastavíme zarovnání textu v řádku (svislé i vodorovné) a určíme barvu písma. Zde začnete definovat, jak bude obsah vypadat vizuálně v listu aplikace Excel.
## Krok 3: Aplikujte Shrink to Fit
Někdy může být text v buňce příliš dlouhý a způsobit přetečení. Šikovným trikem je zmenšit text tak, aby se vešel do buňky, a přitom zachovat čitelnost.
```csharp
// Zmenšení textu, aby se vešel do buňky
style.ShrinkToFit = true;
```
 S`ShrinkToFit`, zajistíte, že velikost dlouhého textu bude upravena tak, aby se vešel do ohraničení buňky, takže váš excelový list bude vypadat lépe organizovaně.
## Krok 4: Nastavte okraje pro řádek
Chcete-li, aby vaše řádky vynikly, je použití ohraničení skvělou volbou. V tomto příkladu přizpůsobíme spodní okraj, nastavíme jeho barvu na červenou a styl na střední.
```csharp
// Nastavení barvy spodního okraje buňky na červenou
style.Borders[BorderType.BottomBorder].Color = Color.Red;
// Nastavení typu spodního ohraničení buňky na střední
style.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Medium;
```
Hranice mohou pomoci vizuálně oddělit obsah, díky čemuž budou vaše data snáze čitelná a esteticky příjemnější.
## Krok 5: Vytvořte objekt StyleFlag
 The`StyleFlag`objekt říká Aspose.Cells, které aspekty stylu se mají použít. To vám dává jemnou kontrolu nad tím, co se použije, a zajišťuje, že je nastaveno pouze zamýšlené formátování.
```csharp
// Vytváření StyleFlag
StyleFlag styleFlag = new StyleFlag();
styleFlag.HorizontalAlignment = true;
styleFlag.VerticalAlignment = true;
styleFlag.ShrinkToFit = true;
styleFlag.Borders = true;
styleFlag.FontColor = true;
```
V tomto případě určujeme, že se má použít vodorovné a svislé zarovnání, barva písma, zmenšení textu a ohraničení.
## Krok 6: Otevřete požadovaný řádek
Jakmile je styl vytvořen, dalším krokem je přístup k řádku, kde chceme použít formátování. V tomto příkladu naformátujeme první řádek (index řádku 0).
```csharp
// Přístup k řádku z kolekce Řádky
Row row = worksheet.Cells.Rows[0];
```
Zde načteme první řádek listu. Index můžete změnit na formátování libovolného jiného řádku.
## Krok 7: Použijte styl na řádek
 Konečně je čas aplikovat styl na řadu! Používáme`ApplyStyle` metoda pro použití definovaného stylu na vybraný řádek.
```csharp
// Přiřazení objektu Style vlastnosti Style řádku
row.ApplyStyle(style, styleFlag);
```
Styl je nyní aplikován na celý řádek, takže data vypadají přesně tak, jak jste si je představovali.
## Krok 8: Uložte sešit
Jakmile dokončíte použití formátování, musíte sešit uložit do souboru aplikace Excel. Je to jako stisknout "Uložit" v Excelu po provedení změn.
```csharp
// Uložení souboru Excel
workbook.Save(dataDir + "book1.out.xls");
```
Nyní máte plně formátovaný list aplikace Excel uložený do určeného adresáře!
## Závěr
To je vše! V několika jednoduchých krocích jste se naučili, jak programově použít formátování na řádek aplikace Excel pomocí Aspose.Cells for .NET. Od nastavení zarovnání textu až po přizpůsobení ohraničení, tento kurz pokryl základy, které vám pomohou vytvářet profesionální a vizuálně přitažlivé sestavy Excelu programově. 
Aspose.Cells nabízí širokou škálu možností a zde zobrazené metody lze snadno rozšířit tak, aby na vaše soubory Excelu aplikovaly složitější styly a formátování. Tak proč to nezkusit a neznechat svá data?
## FAQ
### Mohu použít různé styly na jednotlivé buňky v řadě?  
Ano, na jednotlivé buňky můžete použít různé styly tím, že k nim přistoupíte přímo přes`Cells` kolekce namísto použití stylu na celý řádek.
### Je možné použít podmíněné formátování s Aspose.Cells?  
Absolutně! Aspose.Cells podporuje podmíněné formátování, což vám umožňuje definovat pravidla na základě hodnot buněk.
### Jak mohu použít formátování na více řádků?  
 Pomocí a. můžete procházet více řádky`for` smyčku a aplikujte stejný styl na každý řádek jednotlivě.
### Podporuje Aspose.Cells použití stylů na celé sloupce?  
 Ano, podobně jako k řádkům můžete ke sloupcům přistupovat pomocí`Columns` sbírejte a aplikujte na ně styly.
### Mohu používat Aspose.Cells s aplikacemi .NET Core?  
Ano, Aspose.Cells je plně kompatibilní s .NET Core, což vám umožňuje používat jej na různých platformách.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
