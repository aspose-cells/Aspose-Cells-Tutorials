---
"description": "Naučte se, jak vypočítat barvu vybranou aplikací MS Excel pomocí Aspose.Cells pro .NET. Postupujte podle tohoto podrobného návodu, jak programově přistupovat k barvám podmíněného formátování v Excelu."
"linktitle": "Výpočet barvy vybrané programem v MS Excel"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Výpočet barvy vybrané programem v MS Excel"
"url": "/cs/net/color-settings-and-customization-in-excel/compute-color-chosen-by-ms-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Výpočet barvy vybrané programem v MS Excel

## Zavedení
Pracovali jste někdy s excelovými soubory a přemýšleli jste, jak se určité barvy automaticky vybírají pro formátování? Nejste sami. Podmíněné formátování v Excelu může být trochu záhadou, zvláště když se snažíte extrahovat přesnou barvu, kterou Excel přiřadí. Ale nebojte se, postaráme se o vás! V tomto tutoriálu se podrobně ponoříme do toho, jak programově vypočítat barvu vybranou MS Excelem pomocí Aspose.Cells pro .NET. Rozebereme si to krok za krokem, abyste mohli snadno sledovat a aplikovat to na své vlastní projekty. Pojďme na to!
## Předpoklady
Než se ponoříme do kódu, pojďme si ujasnit, co budete potřebovat k provedení tohoto tutoriálu:
- Aspose.Cells pro .NET je nainstalován. Pokud ho ještě nemáte, můžete [stáhněte si to zde](https://releases.aspose.com/cells/net/).
- Pracovní znalost C# a .NET frameworku.
- Ukázkový soubor aplikace Excel (Book1.xlsx) s použitým podmíněným formátováním.
Pokud ještě nemáte licenci, můžete si také vyzkoušet bezplatnou zkušební verzi Aspose.Cells pro .NET. Stáhněte si zkušební verzi. [zde](https://releases.aspose.com/).
## Importovat balíčky
Než začneme s kódováním, musíme importovat potřebné balíčky, aby vše běželo hladce. Ujistěte se, že ve svém projektu zahrnete následující jmenné prostory:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using System;
```
Tyto importy poskytují přístup k hlavním třídám Aspose.Cells a nativní knihovně pro kreslení systému .NET pro práci s barvami.

Nyní, když máme vše připravené, rozdělme si tento úkol na srozumitelné kroky:
## Krok 1: Nastavení objektu sešitu
První věc, kterou musíme udělat, je vytvořit instanci `Workbook` objekt a načtěte soubor Excel, se kterým chceme pracovat. A tady začíná naše cesta!
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
// Vytvoření instance objektu sešitu a otevření souboru šablony
Workbook workbook = new Workbook(dataDir + "Book1.xlsx");
```
V tomto kroku vytváříme novou instanci `Workbook` třída z Aspose.Cells. `Workbook` Třída představuje soubor aplikace Excel a poskytnutím cesty k našemu souboru jej můžeme snadno načíst pro další manipulaci.
## Krok 2: Přístup k prvnímu pracovnímu listu
Jakmile je sešit načten, musíme přistupovat ke konkrétnímu listu, ze kterého chceme extrahovat barvu. V tomto příkladu budeme pracovat s prvním listem.
```csharp
// Získejte první pracovní list
Worksheet worksheet = workbook.Worksheets[0];
```
Zde načítáme první list v sešitu pomocí `Worksheets[0]` index. Aspose.Cells umožňuje přístup k libovolnému listu v souboru aplikace Excel podle jeho indexu nebo názvu.
## Krok 3: Vyberte buňku, která vás zajímá
Dále vybereme konkrétní buňku v listu. V tomto tutoriálu se zaměříme na buňku „A1“, ale můžete vybrat libovolnou buňku s podmíněným formátováním.
```csharp
// Získejte buňku A1
Cell a1 = worksheet.Cells["A1"];
```
Používáme `Cells` vlastnost odkazovat na konkrétní buňku podle její adresy. V tomto případě vybíráme buňku „A1“, protože chceme extrahovat výsledky podmíněného formátování použité na tuto buňku.
## Krok 4: Načtení výsledku podmíněného formátování
A teď se začne dít ta pravá magie! Použijeme Aspose.Cells k načtení výsledku podmíněného formátování pro vybranou buňku. Takto Excel dynamicky vypočítává formátování, včetně barev.
```csharp
// Získání výsledného objektu podmíněného formátování
ConditionalFormattingResult cfr1 = a1.GetConditionalFormattingResult();
```
Ten/Ta/To `GetConditionalFormattingResult()` Metoda je v tomto kroku klíčová. Vrací objekt, který obsahuje výsledky jakéhokoli podmíněného formátování použitého na buňku. Zde začínáme využívat informace o barvách, které Excel používá.
## Krok 5: Přístup k ColorScaleResult
Jakmile máme výsledek podmíněného formátování, můžeme se hlouběji ponořit a získat přístup k barevné škále, kterou Excel použil pro tuto konkrétní buňku.
```csharp
// Získání výsledného barevného objektu ColorScale
Color c = cfr1.ColorScaleResult;
```
Podmíněné formátování v Excelu se často spoléhá na barevné stupnice. Tento řádek nám umožňuje extrahovat výslednou barvu, která byla použita na základě pravidel podmíněného formátování.
## Krok 6: Výstup informací o barvě
Nakonec chceme vidět použitou barvu z Excelu. Vytiskněme si podrobnosti o barvě ve snadno srozumitelném formátu, včetně její ARGB hodnoty a názvu.
```csharp
// Přečtěte si barvu
Console.WriteLine(c.ToArgb().ToString());
Console.WriteLine(c.Name);
```
Ten/Ta/To `ToArgb()` metoda nám dává barvu ve formátu ARGB (alfa, červená, zelená, modrá), zatímco `Name` Vlastnost poskytuje název barvy ve formátu čitelnějším pro člověka. Tyto podrobnosti o barvě můžete použít k jejich porovnání v jiných aplikacích nebo programově upravit soubory aplikace Excel.

## Závěr
tady to máte! Dodržováním těchto kroků jste se právě naučili, jak programově vypočítat barvu vybranou MS Excelem pomocí Aspose.Cells pro .NET. Tento přístup může být neuvěřitelně užitečný pro automatizaci úloh v Excelu, zejména při práci se složitým podmíněným formátováním. Nyní, až příště narazíte v Excelu na záhadnou barvu, budete přesně vědět, jak odhalit její tajemství.
## Často kladené otázky
### Mohu programově použít podmíněné formátování pomocí Aspose.Cells?
Ano, Aspose.Cells umožňuje programově aplikovat, upravovat a dokonce i odstraňovat podmíněné formátování v souborech aplikace Excel.
### Podporuje Aspose.Cells všechny verze Excelu?
Rozhodně! Aspose.Cells podporuje Excel 97-2003 (XLS), Excel 2007-2019/365 (XLSX) a další formáty, včetně PDF, HTML a CSV.
### Je Aspose.Cells dostupný pro jiné platformy než .NET?
Ano, Aspose.Cells je k dispozici pro různé platformy, včetně Javy, C++ a Androidu přes Javu.
### Jak mohu získat bezplatnou zkušební verzi Aspose.Cells?
Zkušební verzi Aspose.Cells pro .NET si můžete stáhnout zdarma z [zde](https://releases.aspose.com/).
### Jak mohu zpracovat velké soubory aplikace Excel pomocí Aspose.Cells?
Aspose.Cells je optimalizován pro výkon, a to i při práci s velkými soubory. Pro efektivní zpracování velkých dat můžete využít streamovací API.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}