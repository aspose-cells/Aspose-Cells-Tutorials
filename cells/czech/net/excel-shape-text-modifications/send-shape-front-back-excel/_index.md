---
"description": "Zjistěte, jak v Excelu pomocí Aspose.Cells pro .NET odeslat tvary dopředu nebo dozadu. Tato příručka poskytuje podrobný návod s tipy."
"linktitle": "Odeslat tvar dopředu nebo dozadu v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Odeslat tvar dopředu nebo dozadu v Excelu"
"url": "/cs/net/excel-shape-text-modifications/send-shape-front-back-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Odeslat tvar dopředu nebo dozadu v Excelu

## Zavedení
Při práci se soubory aplikace Excel se můžete setkat s potřebou větší kontroly nad vizuálními prvky v tabulce. Tvary, jako jsou obrázky a grafika, mohou vylepšit prezentaci vašich dat. Co se ale stane, když se tyto tvary překrývají nebo je třeba je změnit? A právě zde vynikne Aspose.Cells pro .NET. V tomto tutoriálu vás provedeme kroky pro manipulaci s tvary v listu aplikace Excel, konkrétně odesíláním tvarů na začátek nebo konec jiných tvarů. Pokud jste připraveni vylepšit si práci s Excelem, pojďme se do toho pustit!
## Předpoklady
Než začneme, budete potřebovat mít připraveno několik věcí:
1. Instalace knihovny Aspose.Cells: Ujistěte se, že máte nainstalovanou knihovnu Aspose.Cells pro .NET. Najdete ji [zde](https://releases.aspose.com/cells/net/).
2. Vývojové prostředí: Ujistěte se, že máte nastavené vývojové prostředí s podporou .NET, například Visual Studio.
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.
Dobře, splnili jste všechna políčka v seznamu předpokladů? Skvělé! Pojďme se přesunout k té zábavné části – psaní kódu!
## Importovat balíčky
Než se pustíme do samotného kódování, importujme potřebné balíčky. Stačí přidat následující direktivu using na začátek vašeho C# souboru:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Tyto jmenné prostory jsou klíčové, protože obsahují třídy a metody, které budeme používat k manipulaci s excelovými soubory a tvary.
## Krok 1: Definování cest k souborům
tomto prvním kroku musíme nastavit zdrojový a výstupní adresář. Zde se nachází váš soubor Excel a kam chcete uložit upravený soubor.
```csharp
//Zdrojový adresář
string sourceDir = "Your Document Directory";
//Výstupní adresář
string outputDir = "Your Document Directory";
```
Nahradit `"Your Document Directory"` se skutečnou cestou, kde jsou uloženy vaše soubory aplikace Excel.
## Krok 2: Načtení sešitu
Nyní, když máme nastavené adresáře, načtěme sešit (soubor aplikace Excel), který obsahuje tvary, se kterými chceme manipulovat.
```csharp
//Načíst zdrojový soubor Excel
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
Tento řádek kódu inicializuje nový `Workbook` objekt, načtení zadaného souboru aplikace Excel do paměti, abychom s ním mohli pracovat.
## Krok 3: Přístup k pracovnímu listu 
Dále potřebujeme přístup ke konkrétnímu listu, kde se nacházejí naše tvary. V tomto příkladu použijeme první list.
```csharp
//Přístup k prvnímu listu
Worksheet ws = wb.Worksheets[0];
```
Odkazováním `Worksheets[0]`, zaměřujeme se na první list našeho sešitu. Pokud jsou vaše tvary na jiném listu, upravte index odpovídajícím způsobem.
## Krok 4: Přístup k tvarům
přístupem k pracovnímu listu připraveným si vezměme tvary, které nás zajímají. V tomto příkladu si vezmeme první a čtvrtý tvar.
```csharp
//Přístup k prvnímu a čtvrtému tvaru
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Tyto čáry získávají specifické tvary z pracovního listu na základě svého indexu.
## Krok 5: Vytiskněte polohu tvarů v ose Z
Než přesuneme jakékoli tvary, vytiskněme si jejich aktuální pozici v ose Z. To nám pomůže sledovat jejich umístění před provedením změn.
```csharp
//Vytiskněte pozici tvaru v ose Z
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
Zavoláním `ZOrderPosition`, můžeme vidět, kde se každý tvar nachází v pořadí kreslení.
## Krok 6: Odešlete první tvar dopředu
A teď je čas na akci! Pošleme první tvar na začátek Z-pořadí.
```csharp
//Poslat tento tvar dopředu
sh1.ToFrontOrBack(2);
```
Procházením `2` na `ToFrontOrBack`, dáváme instrukci Aspose.Cells, aby tento tvar přesunul do popředí. 
## Krok 7: Vytiskněte pozici druhého tvaru v ose Z
Než odešleme druhý tvar dozadu, zkontrolujme, kde je umístěn.
```csharp
//Vytiskněte pozici tvaru v ose Z
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
To nám dává vhled do polohy čtvrtého tvaru, než provedeme jakékoli změny.
## Krok 8: Pošlete čtvrtý tvar dozadu
Nakonec pošleme čtvrtý tvar na konec zásobníku v pořadí Z.
```csharp
//Poslat tento tvar dozadu
sh4.ToFrontOrBack(-2);
```
Používání `-2` protože parametr posílá tvar směrem do zadní části zásobníku, čímž zajišťuje, že nebude překážet jiným tvarům ani textu.
## Krok 9: Uložení sešitu 
Posledním krokem je uložení sešitu s nově umístěnými tvary.
```csharp
//Uložte výstupní soubor Excel
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Tento příkaz uloží upravený sešit do zadaného výstupního adresáře.
## Krok 10: Potvrzovací zpráva
Nakonec nám poskytněte jednoduché potvrzení, které nám dá vědět, že náš úkol byl úspěšně dokončen.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
A tím je kód pro náš tutoriál hotový!
## Závěr
Manipulace s tvary v Excelu pomocí Aspose.Cells pro .NET je nejen jednoduchá, ale i výkonná. Dodržováním tohoto návodu byste nyní měli být schopni snadno odesílat tvary dopředu nebo dozadu, což vám umožní lepší kontrolu nad vašimi prezentacemi v Excelu. S těmito nástroji k dispozici jste připraveni vylepšit vizuální atraktivitu vašich tabulek.
## Často kladené otázky
### Jaký programovací jazyk potřebuji pro Aspose.Cells?  
Pro práci s Aspose.Cells musíte použít C# nebo jakýkoli jazyk podporovaný rozhraním .NET.
### Mohu si Aspose.Cells vyzkoušet zdarma?  
Ano, můžete začít s bezplatnou zkušební verzí Aspose.Cells [zde](https://releases.aspose.com/).
### S jakými tvary mohu v Excelu manipulovat?  
Můžete manipulovat s různými tvary, jako jsou obdélníky, kruhy, čáry a obrázky.
### Jak mohu získat podporu pro Aspose.Cells?  
Pro jakoukoli podporu nebo dotazy můžete navštívit jejich komunitní fórum [zde](https://forum.aspose.com/c/cells/9).
### Je k dispozici dočasná licence pro Aspose.Cells?  
Ano, můžete požádat o dočasnou licenci [zde](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}