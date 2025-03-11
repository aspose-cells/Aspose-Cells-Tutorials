---
title: Implementujte zmrazená podokna v listu
linktitle: Implementujte zmrazená podokna v listu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak implementovat zmrazená podokna v Excelu pomocí Aspose.Cells for .NET, pomocí tohoto podrobného průvodce krok za krokem. Efektivně vylepšete použitelnost svého listu.
weight: 15
url: /cs/net/worksheet-display/implement-freeze-panes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Implementujte zmrazená podokna v listu

## Zavedení
Představte si, že máte excelový list s obrovskou datovou sadou a pokaždé, když se posunete dolů nebo napříč, ztratíte přehled o těchto důležitých záhlavích. Nebylo by vhodné, kdyby tato záhlaví mohla zůstat na místě, zatímco budete rolovat? To je místo, kde přichází na řadu zmrazená okna, díky čemuž je navigace plynulá a efektivní. Aspose.Cells for .NET tento proces zjednodušuje a dává vám možnost bezproblémově implementovat zmrazená okna. Tato příručka vás provede celým procesem a rozebere jej krok za krokem, abyste mohli tyto zmrazené hlavičky nastavit během okamžiku.
## Předpoklady
Před potápěním se ujistěte, že máte připraveno několik věcí:
-  Aspose.Cells for .NET Library: Tuto knihovnu si budete muset stáhnout z[Stránka vydání Aspose](https://releases.aspose.com/cells/net/).
- Nainstalované rozhraní .NET Framework: Ujistěte se, že máte ve svém vývojovém prostředí nastaveno rozhraní .NET.
- Základní znalost C#: Znalost C# bude užitečné pokračovat.
- Soubor Excel: Připravte si soubor Excel (např. „book1.xls“), na který použijete zmrazené panely.
Další podrobnosti o Aspose.Cells můžete prozkoumat na jejich stránkách[dokumentační stránku](https://reference.aspose.com/cells/net/).

## Importujte balíčky
Začněme importem potřebných balíčků. Otevřete svůj projekt C# a ujistěte se, že importujete tyto:
```csharp
using System.IO;
using Aspose.Cells;
```
Po nastavení balíčků se vrhneme na průvodce krok za krokem.
Projdeme každou fází nastavení panelů zmrazení pomocí Aspose.Cells pro .NET. Pečlivě dodržujte každý krok a budete mít zmrazené panely bez námahy aplikovány na váš list.
## Krok 1: Definujte cestu k adresáři vašich dokumentů
 Než budete moci otevřít soubor aplikace Excel, budete muset zadat cestu k dokumentu. Nastavit a`dataDir` proměnná, která obsahuje cestu k adresáři pro vaše soubory.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```
 Nahradit`"Your Document Directory"` se skutečnou cestou k umístění souborů aplikace Excel. To pomůže programu najít váš soubor.
## Krok 2: Otevřete soubor aplikace Excel pomocí FileStream
Dále musíme načíst soubor Excel, aby Aspose.Cells mohl fungovat. Chcete-li to provést, vytvoříme souborový proud a otevřeme soubor aplikace Excel pomocí tohoto proudu.
```csharp
// Vytvoření datového proudu souboru obsahujícího soubor Excel, který se má otevřít
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Pomocí datového proudu souborů otevíráte soubor pro přístup Aspose.Cells, aniž byste měnili původní soubor, dokud výslovně neuložíte jakékoli změny.
## Krok 3: Vytvořte instanci objektu sešitu
 Když je datový proud souborů na místě, je čas vytvořit soubor`Workbook` objekt. Tento objekt je nezbytný, protože představuje celý sešit aplikace Excel a umožňuje vám pracovat s jednotlivými listy, buňkami a nastaveními v souboru.
```csharp
// Vytvoření instance objektu sešitu
// Otevření souboru aplikace Excel prostřednictvím datového proudu souborů
Workbook workbook = new Workbook(fstream);
```
 Myslete na to`Workbook` jako pojivo, které drží všechny vaše listy pohromadě. Jakmile otevřete pořadač, můžete přistupovat k libovolné stránce (listu) v něm.
## Krok 4: Otevřete první pracovní list
Nyní, když je váš sešit načten, můžete si vybrat, na který list chcete použít zmrazená podokna. V tomto příkladu budeme pracovat s prvním listem. Aspose.Cells usnadňuje výběr listu indexováním.
```csharp
// Přístup k prvnímu listu v souboru aplikace Excel
Worksheet worksheet = workbook.Worksheets[0];
```
 Pokud potřebujete pracovat na jiném listu, jednoduše upravte index`workbook.Worksheets[0]`.
## Krok 5: Použijte nastavení Freeze Panes
 Tady se děje kouzlo! Chcete-li nastavit zmrazené panely, použijte`FreezePanes`určující řádek a sloupec, kde chcete, aby zmrazení začalo, a také počet řádků a sloupců, které chcete zmrazit.
```csharp
// Použití nastavení zmrazených panelů
worksheet.FreezePanes(3, 2, 3, 2);
```
Pojďme si rozebrat parametry:
- První řádek (3): Začněte zmrazení na řádku 3.
- První sloupec (2): Začněte zmrazení ve sloupci 2.
- Počet řádků (3): Zmrazit 3 řádky.
- Počet sloupců (2): Zmrazit 2 sloupce.
Upravte tyto hodnoty podle svých konkrétních potřeb. Bod zmrazení bude průsečíkem zadaného řádku a sloupce.
## Krok 6: Uložte upravený soubor Excel
 Po použití panelů zmrazení je čas uložit změny. Uložením upraveného souboru sešitu zajistíte zachování nastavení zmrazení. Aktualizovaný soubor můžete uložit pomocí`Save` metoda.
```csharp
// Uložení upraveného souboru Excel
workbook.Save(dataDir + "output.xls");
```
Pokud chcete zachovat i původní soubor, nezapomeňte jej uložit pod jiným názvem.
## Krok 7: Zavřete Stream souborů
Nakonec nezapomeňte zavřít datový proud souboru. Tím se uvolní systémové prostředky a dokončí se všechna otevřená připojení k souboru.
```csharp
// Zavřením datového proudu souborů uvolníte všechny zdroje
fstream.Close();
```
Uzavření streamu považujte za vrácení souboru zpět na polici, jakmile s ním skončíte. Je to dobrý zvyk v domácnosti.

## Závěr
Gratuluji! Úspěšně jste použili zmrazená podokna na list aplikace Excel pomocí Aspose.Cells for .NET. Tato technika je neuvěřitelně užitečná pro správu velkých datových sad a zajišťuje, že záhlaví nebo konkrétní řádky a sloupce zůstanou viditelné při procházení dat. Podle tohoto podrobného průvodce můžete s jistotou implementovat zmrazená podokna a zlepšit použitelnost svých tabulek.
## FAQ
### Mohu zmrazit více než jeden list v sešitu?
 Ano, jednoduše opakujte`FreezePanes` metoda na každém listu, na který ji chcete použít.
### Co se stane, když použiji hodnoty řádků a sloupců, které přesahují rozsah listu?
Aspose.Cells vyvolá výjimku, takže se ujistěte, že vaše hodnoty jsou v mezích listu.
### Mohu upravit nastavení zmrazených panelů po jejich použití?
 Absolutně! Stačí zavolat`FreezePanes`metodu znovu s novými parametry pro aktualizaci nastavení.
### Funguje podokno zmrazení ve všech verzích souborů aplikace Excel?
Ano, zmrazené panely budou zachovány ve většině formátů aplikace Excel (např. XLS, XLSX) podporovaných Aspose.Cells.
### Mohu rozmrazit tabule?
 Chcete-li odstranit zmrazené panely, jednoduše zavolejte`UnfreezePanes()` na pracovním listu.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
