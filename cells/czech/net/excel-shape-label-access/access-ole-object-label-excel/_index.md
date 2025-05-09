---
"description": "Naučte se, jak přistupovat k popiskům objektů OLE a jak je upravovat v Excelu pomocí Aspose.Cells pro .NET. Jednoduchý návod s příklady kódu."
"linktitle": "Přístup k popisku objektu OLE v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Přístup k popisku objektu OLE v Excelu"
"url": "/cs/net/excel-shape-label-access/access-ole-object-label-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přístup k popisku objektu OLE v Excelu

## Zavedení
Pokud jste se někdy pustili do práce s Excelem, víte, jak mocný a složitý může být. Někdy můžete narazit na data vložená v objektech OLE (Object Linking and Embedding) – představte si to jako „mini-okno“ do jiného softwarového nástroje, jako je dokument Wordu nebo snímek PowerPointu, to vše pohodlně zasazené do vaší tabulky. Ale jak k těmto popiskům v našich objektech OLE přistupujeme a manipulujeme s nimi pomocí Aspose.Cells pro .NET? Připoutejte se, protože v tomto tutoriálu si to krok za krokem rozebereme!
## Předpoklady
 
Než se vrhneme do akcí nabitého světa Aspose.Cells pro .NET, zde je to, co potřebujete mít ve své sadě nástrojů:
1. Nainstalované Visual Studio: Toto bude vaše hřiště, kde budete kódovat a testovat svou aplikaci v C#.
2. .NET Framework: Ujistěte se, že používáte alespoň .NET Framework 4.0 nebo vyšší. To poskytne našemu programu potřebný základ pro bezproblémové fungování.
3. Knihovna Aspose.Cells: Budete potřebovat kopii knihovny Aspose.Cells. Můžete si ji stáhnout z [zde](https://releases.aspose.com/cells/net/)Pokud si to chcete před nákupem vyzkoušet, podívejte se na [bezplatná zkušební verze](https://releases.aspose.com/).
4. Základní znalost C#: Znalost C# vám pomůže snadno se s kódem vypořádat.
Když jsme si to ujasnili, pojďme se ponořit do detailů přístupu k popiskům objektů OLE a jejich úprav!
## Importovat balíčky 
Pro začátek musíme do našeho projektu importovat potřebné balíčky. To nám usnadní život tím, že nám poskytne přístup ke všem funkcím a třídám, které potřebujeme. Zde je návod:
### Vytvoření nového projektu v C# 
- Otevřete Visual Studio a vytvořte nový projekt konzolové aplikace v C#.
- Pojmenujte to například „Příklad popisku objektu OLE“.
### Přidejte referenci Aspose.Cells 
- Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
- Vyberte možnost „Spravovat balíčky NuGet“.
- Vyhledejte „Aspose.Cells“ a nainstalujte knihovnu.
### Importovat jmenné prostory
V horní části souboru programu (např. `Program.cs`), je třeba importovat potřebné jmenné prostory:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Tyto jmenné prostory nám pomohou přistupovat ke třídám a metodám potřebným pro manipulace s Excelem.
Nyní, když je vše na svém místě, pojďme přistupovat k popisku objektu OLE vloženého do souboru aplikace Excel a upravovat ho. Postupujte podle níže uvedeného podrobného návodu:
## Krok 1: Nastavení zdrojového adresáře
Nejprve definujeme adresář, kde se nachází váš dokument aplikace Excel. Nahraďte `"Your Document Directory"` se skutečnou cestou k dokumentu.
```csharp
string sourceDir = "Your Document Directory";
```
## Krok 2: Načtěte ukázkový soubor Excel 
Dále načteme soubor Excelu .xlsx, který obsahuje náš objekt OLE:
```csharp
Workbook wb = new Workbook(sourceDir + "sampleAccessAndModifyLabelOfOleObject.xlsx");
```
Tento řádek inicializuje `Workbook` objekt, který nám umožňuje přístup ke všem listům a komponentám souboru aplikace Excel.
## Krok 3: Přístup k prvnímu pracovnímu listu
Nyní se podívejme na první list v našem sešitu:
```csharp
Worksheet ws = wb.Worksheets[0];
```
Zde, `Worksheets[0]` je první pracovní list ve sbírce.
## Krok 4: Přístup k prvnímu objektu OLE 
Dále načteme první OLE objekt:
```csharp
Aspose.Cells.Drawing.OleObject oleObject = ws.OleObjects[0];
```
To nám umožní interagovat s objektem OLE, se kterým chceme pracovat.
## Krok 5: Zobrazení popisku objektu OLE
Než upravíme popisek, vytiskněme si jeho aktuální hodnotu:
```csharp
Console.WriteLine("Ole Object Label - Before: " + oleObject.Label);
```
Díky tomu máme jasný přehled o štítku před provedením jakýchkoli změn.
## Krok 6: Úprava popisku 
A teď ta zábavná část – změníme popisek objektu OLE:
```csharp
oleObject.Label = "Aspose APIs";
```
Můžete si to nastavit na cokoli chcete. „Aspose API“ je jen elegantní způsob, jak ukázat, co děláme.
## Krok 7: Uložení sešitu do paměťového streamu 
Pak uložíme změny do paměťového proudu a poté znovu načteme sešit:
```csharp
MemoryStream ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
```
Tím se upravený sešit uloží do paměti, což usnadní jeho pozdější přístup.
## Krok 8: Nastavení odkazu na sešit na hodnotu Null 
Pro vyčištění paměti bychom měli nastavit odkaz na sešit na hodnotu null:
```csharp
wb = null;
```
## Krok 9: Načtení sešitu z paměťového proudu 
Dále znovu načteme náš sešit z paměťového proudu, který jsme právě uložili:
```csharp
wb = new Workbook(ms);
```
## Krok 10: Znovu zpřístupněte první pracovní list 
Stejně jako předtím musíme znovu přistupovat k prvnímu listu:
```csharp
ws = wb.Worksheets[0];
```
## Krok 11: Znovu zpřístupněte první objekt OLE
Nyní znovu načtěte objekt OLE pro závěrečnou kontrolu:
```csharp
oleObject = ws.OleObjects[0];
```
## Krok 12: Zobrazení upraveného popisku 
Abychom zjistili, zda se naše změny projevily, vytiskněme si nový popisek:
```csharp
Console.WriteLine("Ole Object Label - After: " + oleObject.Label);
```
## Krok 13: Potvrzení provedení 
Nakonec zašlete zprávu o úspěchu, abychom věděli, že vše proběhlo podle plánu:
```csharp
Console.WriteLine("AccessAndModifyLabelOfOleObject executed successfully.");
```
## Závěr 
tady to máte! Úspěšně jste přistupovali k popisku objektu OLE v Excelu a upravovali ho pomocí Aspose.Cells pro .NET. Je to skvělý způsob, jak dodat vloženým dokumentům osobní nádech, zlepšit přehlednost a komunikaci v rámci tabulek. 
Ať už vyvíjíte skvělou aplikaci, nebo jen vylepšujete své reporty, manipulace s objekty OLE může být převratná. Pokračujte v prozkoumávání toho, co Aspose.Cells nabízí, a objevíte celý svět možností.
## Často kladené otázky
### Co je objekt OLE v Excelu?  
Objekty OLE jsou vložené soubory, které umožňují integrovat dokumenty z jiných aplikací sady Microsoft Office do tabulky aplikace Excel.
### Může Aspose.Cells pracovat s jinými formáty souborů?  
Ano! Aspose.Cells podporuje různé formáty, včetně XLS, XLSX, CSV a dalších.
### Je k dispozici bezplatná zkušební verze pro Aspose.Cells?  
Ano! Můžeš to vyzkoušet. [zde](https://releases.aspose.com/).
### Mohu v listu přistupovat k více objektům OLE?  
Rozhodně! Můžete to procházet `ws.OleObjects` pro přístup ke všem vloženým objektům OLE v listu.
### Jak si mohu zakoupit licenci pro Aspose.Cells?  
Licenci si můžete zakoupit přímo od [zde](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}