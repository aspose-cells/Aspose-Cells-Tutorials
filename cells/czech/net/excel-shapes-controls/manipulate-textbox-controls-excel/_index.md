---
"description": "Naučte se, jak manipulovat s textovými poli v Excelu pomocí Aspose.Cells pro .NET, v tomto snadno srozumitelném a podrobném tutoriálu."
"linktitle": "Manipulace s ovládacími prvky TextBox v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Manipulace s ovládacími prvky TextBox v Excelu"
"url": "/cs/net/excel-shapes-controls/manipulate-textbox-controls-excel/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Manipulace s ovládacími prvky TextBox v Excelu

## Zavedení
Pokud jste někdy pracovali s Excelem, pravděpodobně jste narazili na malá textová pole, která umožňují přidávat plovoucí text do tabulky. Co když ale potřebujete s těmito textovými poli manipulovat programově? A právě v tom případě se vám hodí Aspose.Cells for .NET. S ním můžete snadno přistupovat k textovým polím a upravovat je, což je ideální pro automatizaci úkolů nebo úpravu sestav. V tomto tutoriálu vás provedeme procesem manipulace s textovými poli v Excelu pomocí Aspose.Cells for .NET.
## Předpoklady
Než se ponoříme do samotného kódu, ujistěme se, že máte vše správně nastavené:
1. Aspose.Cells pro .NET: Je třeba si stáhnout knihovnu Aspose.Cells pro .NET. Odkaz ke stažení naleznete [zde](https://releases.aspose.com/cells/net/).
2. Vývojové prostředí .NET: Fungovat bude jakékoli vývojové prostředí (IDE), které podporuje .NET, například Visual Studio.
3. Základní znalost jazyka C#: Tento tutoriál předpokládá, že jste obeznámeni se základní syntaxí jazyka C# a strukturou sešitů aplikace Excel.
4. Soubor aplikace Excel: Existující soubor aplikace Excel s textovými poli (použijeme `book1.xls` v tomto příkladu).
5. Licence Aspose: Pokud nepoužíváte bezplatnou zkušební verzi, budete muset [nakoupit](https://purchase.aspose.com/buy) licenci nebo získat [dočasný](https://purchase.aspose.com/temporary-license/).
A teď se pojďme ponořit do kroků!
## Importovat balíčky
Než budete moci manipulovat se sešity a textovými poli aplikace Excel pomocí Aspose.Cells, musíte importovat potřebné jmenné prostory. Zde je úryvek kódu, který použijete na začátku souboru C#:
```csharp
using System.IO;
using Aspose.Cells;
```
Tyto balíčky vám poskytují přístup k manipulaci se sešity, přístupu k pracovním listům a objektům kreslení (například textovým polím).
Nyní, když máme vše nastavené, pojďme si rozebrat proces manipulace s textovými poli do snadno sledovatelných kroků.
## Krok 1: Nastavení adresáře sešitu
Prvním krokem je určit, kde se soubory Excelu nacházejí ve vašem systému. Budete muset nahradit zástupný symbol `Your Document Directory` se skutečnou cestou k vašemu souboru. Tato cesta je uložena v `dataDir` proměnná pro snadné použití v celém kódu.
```csharp
string dataDir = "Your Document Directory";
```
Díky tomu bude váš program vědět, kde má najít vstupní soubor Excelu (`book1.xls`) a kam uložit výstupní soubor.
## Krok 2: Otevřete soubor Excel
Dále budete muset načíst existující soubor aplikace Excel do objektu Aspose.Cells Workbook. Tento sešit slouží jako kontejner pro vaše data aplikace Excel a poskytuje vám přístup k jeho listům a všem objektům kreslení (například textovým polím).
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
Ten/Ta/To `Workbook` Třída z Aspose.Cells načte zadaný soubor aplikace Excel z vašeho adresáře. Pokud soubor v zadaném adresáři neexistuje, vyvolá se výjimka, proto se ujistěte, že je cesta správná.
## Krok 3: Přístup k prvnímu pracovnímu listu
Nyní, když máte načten sešit, můžete přistupovat k jeho listům. V tomto příkladu přistupujeme k prvnímu listu v sešitu, který je uložen na indexu 0.
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Ten/Ta/To `Worksheets` Vlastnost vám poskytuje přístup ke všem listům v sešitu. Zde nás zajímá pouze první list, ale můžete pracovat s libovolným listem zadáním správného indexu.
## Krok 4: Získání prvního objektu TextBox
Textová pole v listu aplikace Excel jsou považována za kreslené objekty. Třída Aspose.Cells.Drawing.TextBox poskytuje vlastnosti a metody pro jejich manipulaci. Chcete-li získat přístup k prvnímu textovému poli na listu, jednoduše se odkážete na `TextBoxes` sbírka podle indexu.
```csharp
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[0];
```
Tím se načte první objekt textového pole z `TextBoxes` kolekce. Pokud váš list neobsahuje textové pole na daném indexu, vyvolá se výjimka, proto se vždy ujistěte, že je index platný.
## Krok 5: Načtení textu z prvního textového pole
Po přístupu k textovému poli můžete extrahovat text, který obsahuje, pomocí `.Text` vlastnictví.
```csharp
string text0 = textbox0.Text;
```
Tím se text z prvního textového pole zachytí do `text0` řetězec. Nyní jej můžete zobrazit, manipulovat s ním nebo jej zpracovat ve své aplikaci.
## Krok 6: Přístup k druhému objektu TextBox
Pro manipulaci s více textovými poli můžeme z listu načíst další. Zde budeme k druhému textovému poli přistupovat podobným způsobem jako k prvnímu:
```csharp
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[1];
```
Opět přistupujeme k druhému textovému poli pomocí indexu 1 z `TextBoxes` sbírka.
## Krok 7: Načtení textu z druhého textového pole
Stejně jako u prvního textového pole můžete načíst text z druhého textového pole a uložit ho do řetězce:
```csharp
string text1 = textbox1.Text;
```
Tím se zachytí aktuální text z druhého textového pole.
## Krok 8: Úprava textu ve druhém textovém poli
Řekněme, že chcete upravit text uvnitř druhého textového pole. Můžete to snadno provést přiřazením nového řetězce k `.Text` vlastnost objektu textového pole.
```csharp
textbox1.Text = "This is an alternative text";
```
Tím se text uvnitř druhého textového pole změní na nový obsah. Zde můžete vložit libovolný text dle vašich požadavků.
## Krok 9: Uložte aktualizovaný soubor aplikace Excel
Nakonec, po úpravě textových polí, je čas uložit změny. Aspose.Cells umožňuje uložit upravený sešit pomocí `.Save()` metoda. Můžete zadat nový název souboru nebo přepsat existující soubor.
```csharp
workbook.Save(dataDir + "output.out.xls");
```
Tímto se upravený soubor Excel uloží do vámi určené výstupní cesty. Nyní, když soubor Excel otevřete, uvidíte změny, které jste provedli v textových polích.
## Závěr
A tady to máte! Právě jste se naučili, jak manipulovat s textovými poli v Excelu pomocí knihovny Aspose.Cells pro .NET. Ať už automatizujete generování sestav, upravujete excelové listy nebo vytváříte dynamický obsah, Aspose.Cells vám usnadňuje programově ovládat všechny aspekty vašich excelových souborů. Od extrakce a úpravy textu až po ukládání aktualizovaných souborů je tato knihovna výkonným nástrojem pro vývojáře pracující s Excelem v prostředí .NET.
## Často kladené otázky
### Mohu pomocí Aspose.Cells manipulovat s jinými objekty kresby kromě textových polí?
Ano, Aspose.Cells umožňuje manipulovat s dalšími nakreslenými objekty, jako jsou tvary, grafy a obrázky.
### Co se stane, když se pokusím o přístup k textovému poli, které neexistuje?
Pokud je index textového pole mimo rozsah, zobrazí se `IndexOutOfRangeException` bude hozen.
### Mohu přidat nová textová pole do listu aplikace Excel pomocí Aspose.Cells?
Ano, Aspose.Cells umožňuje přidávat nová textová pole pomocí `AddTextBox` metoda.
### Potřebuji licenci k používání Aspose.Cells?
Ano, budete si muset zakoupit licenci, ale Aspose také nabízí [bezplatná zkušební verze](https://releases.aspose.com/).
### Mohu používat Aspose.Cells s jinými programovacími jazyky než C#?
Ano, Aspose.Cells lze použít s jakýmkoli jazykem podporovaným .NET, například VB.NET.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}