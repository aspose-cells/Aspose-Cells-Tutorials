---
title: Manipulujte s ovládacími prvky textového pole v aplikaci Excel
linktitle: Manipulujte s ovládacími prvky textového pole v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak manipulovat s textovými poli v Excelu pomocí Aspose.Cells for .NET s tímto jednoduchým, podrobným návodem.
weight: 15
url: /cs/net/excel-shapes-controls/manipulate-textbox-controls-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Manipulujte s ovládacími prvky textového pole v aplikaci Excel

## Zavedení
Pokud jste někdy pracovali s Excelem, pravděpodobně jste narazili na malá textová pole, která vám umožňují přidat plovoucí text do tabulky. Ale co když potřebujete manipulovat s těmito textovými poli programově? To je místo, kde se Aspose.Cells for .NET hodí. S ním můžete snadno přistupovat a upravovat textová pole, takže je ideální pro automatizaci úloh nebo přizpůsobení sestav. V tomto tutoriálu vás provedeme procesem manipulace s textovými poli v Excelu pomocí Aspose.Cells for .NET.
## Předpoklady
Než se ponoříme do skutečného kódu, ujistěte se, že máte vše správně nastaveno:
1.  Aspose.Cells for .NET: Musíte si stáhnout knihovnu Aspose.Cells for .NET. Odkaz ke stažení najdete[zde](https://releases.aspose.com/cells/net/).
2. Vývojové prostředí .NET: Bude fungovat jakékoli IDE, které podporuje .NET, jako je Visual Studio.
3. Základní znalost C#: Tento tutoriál předpokládá, že jste obeznámeni se základní syntaxí C# a strukturou sešitů aplikace Excel.
4.  Soubor Excel: Stávající soubor Excel s textovými poli (použijeme`book1.xls` tomto příkladu).
5.  Aspose License: Pokud nepoužíváte bezplatnou zkušební verzi, budete muset[nakoupit](https://purchase.aspose.com/buy) licenci nebo získat a[dočasný](https://purchase.aspose.com/temporary-license/).
Nyní se pojďme ponořit do kroků!
## Importujte balíčky
Než budete moci manipulovat s excelovými sešity a textovými poli pomocí Aspose.Cells, musíte importovat potřebné jmenné prostory. Zde je fragment kódu, který použijete v horní části souboru C#:
```csharp
using System.IO;
using Aspose.Cells;
```
Tyto balíčky umožňují přístup k manipulaci se sešitem, přístup k listu a nakresleným objektům (jako jsou textová pole).
Nyní, když máme vše nastaveno, rozdělíme proces manipulace s textovými poli do snadno srozumitelných kroků.
## Krok 1: Nastavte adresář sešitů
 Prvním krokem je určit, kde jsou vaše soubory Excel umístěny ve vašem systému. Budete muset nahradit zástupný symbol`Your Document Directory` se skutečnou cestou k vašemu souboru. Tato cesta je uložena v`dataDir` proměnná pro snadný odkaz v celém kódu.
```csharp
string dataDir = "Your Document Directory";
```
To umožňuje vašemu programu vědět, kde najít vstupní soubor Excel (`book1.xls`) a kam uložit výstupní soubor.
## Krok 2: Otevřete soubor aplikace Excel
Dále budete muset načíst existující soubor Excel do objektu Aspose.Cells Workbook. Tento sešit funguje jako kontejner pro vaše data aplikace Excel a poskytuje vám přístup k jeho listům a jakýmkoli nakresleným objektům (jako jsou textová pole).
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 The`Workbook` třídy z Aspose.Cells načte zadaný soubor Excel z vašeho adresáře. Pokud soubor v zadaném adresáři neexistuje, vyvolá výjimku, takže se ujistěte, že je cesta správná.
## Krok 3: Otevřete první pracovní list
Nyní, když máte sešit načtený, máte přístup k jeho listům. V tomto příkladu přistupujeme k prvnímu listu v sešitu, který je uložen na indexu 0.
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
 The`Worksheets` vlastnost vám umožňuje přístup ke všem listům v sešitu. Zde nás zajímá pouze první list, ale můžete pracovat s libovolným listem zadáním správného indexu.
## Krok 4: Získejte první objekt TextBox
Textová pole v listu aplikace Excel jsou považována za nakreslené objekty. Třída Aspose.Cells.Drawing.TextBox poskytuje vlastnosti a metody pro manipulaci s nimi. Chcete-li získat přístup k prvnímu textovému poli na listu, jednoduše přejděte na`TextBoxes` kolekce podle indexu.
```csharp
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[0];
```
 Tím se načte první objekt textového pole z`TextBoxes` sbírka. Pokud váš list nemá u tohoto indexu textové pole, vyvolá výjimku, takže vždy zkontrolujte, zda je index platný.
## Krok 5: Načtení textu z prvního textového pole
 Po otevření textového pole můžete extrahovat text, který obsahuje, pomocí`.Text` vlastnictví.
```csharp
string text0 = textbox0.Text;
```
 Tím se zachytí text z prvního textového pole do`text0` řetězec. Nyní jej můžete zobrazit, manipulovat s ním nebo jej zpracovat ve své aplikaci.
## Krok 6: Přístup k druhému objektu TextBox
Chcete-li manipulovat s více textovými poli, můžeme z listu načíst další. Zde přistoupíme k druhému textovému poli podobným způsobem jako k prvnímu:
```csharp
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[1];
```
Opět přistupujeme k druhému textovému poli pomocí indexu 1 z`TextBoxes`sbírka.
## Krok 7: Načtení textu z druhého textového pole
Stejně jako u prvního textového pole můžete načíst text z druhého textového pole a uložit jej do řetězce:
```csharp
string text1 = textbox1.Text;
```
Tím se zachytí aktuální text z druhého textového pole.
## Krok 8: Upravte text ve druhém textovém poli
 Nyní řekněme, že chcete upravit text uvnitř druhého textového pole. Můžete to snadno provést přiřazením nového řetězce k`.Text` vlastnost objektu textového pole.
```csharp
textbox1.Text = "This is an alternative text";
```
Tím se text uvnitř druhého textového pole změní na nový obsah. Zde můžete vložit libovolný text na základě vašich požadavků.
## Krok 9: Uložte aktualizovaný soubor Excel
 Nakonec, po úpravě textových polí, je čas uložit změny. Aspose.Cells umožňuje uložit upravený sešit pomocí`.Save()` metoda. Můžete zadat nový název souboru nebo přepsat existující soubor.
```csharp
workbook.Save(dataDir + "output.out.xls");
```
Tím se upravený soubor Excel uloží do vámi určené výstupní cesty. Nyní, když otevřete soubor Excel, uvidíte změny, které jste provedli v textových polích.
## Závěr
A tady to máte! Právě jste se naučili, jak manipulovat s textovými poli v Excelu pomocí Aspose.Cells for .NET. Ať už automatizujete generování sestav, přizpůsobujete listy aplikace Excel nebo vytváříte dynamický obsah, Aspose.Cells usnadňuje programové ovládání všech aspektů vašich souborů aplikace Excel. Od extrahování a úprav textu až po ukládání aktualizovaných souborů je tato knihovna výkonným nástrojem pro vývojáře pracující s Excelem v prostředí .NET.
## FAQ
### Mohu s Aspose.Cells manipulovat s jinými objekty kreslení kromě textových polí?
Ano, Aspose.Cells vám umožňuje manipulovat s jinými objekty kreslení, jako jsou tvary, grafy a obrázky.
### Co se stane, když se pokusím otevřít textové pole, které neexistuje?
 Pokud je index textového pole mimo rozsah, an`IndexOutOfRangeException` bude vrženo.
### Mohu přidat nová textová pole do listu aplikace Excel pomocí Aspose.Cells?
 Ano, Aspose.Cells vám umožňuje přidávat nová textová pole pomocí`AddTextBox` metoda.
### Potřebuji licenci k používání Aspose.Cells?
 Ano, budete si muset zakoupit licenci, ale Aspose také nabízí a[zkušební verze zdarma](https://releases.aspose.com/).
### Mohu používat Aspose.Cells s jinými programovacími jazyky kromě C#?
Ano, Aspose.Cells lze použít s jakýmkoli jazykem podporovaným .NET, jako je VB.NET.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
