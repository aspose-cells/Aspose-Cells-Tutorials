---
title: Odeslat tvar dopředu nebo dozadu v aplikaci Excel
linktitle: Odeslat tvar dopředu nebo dozadu v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Objevte, jak posílat tvary dopředu nebo dozadu v Excelu pomocí Aspose.Cells pro .NET. Tato příručka obsahuje návod krok za krokem s tipy.
weight: 16
url: /cs/net/excel-shape-text-modifications/send-shape-front-back-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Odeslat tvar dopředu nebo dozadu v aplikaci Excel

## Zavedení
Při práci se soubory aplikace Excel můžete zjistit, že potřebujete větší kontrolu nad vizuálními prvky v tabulce. Tvary, jako jsou obrázky a grafika, mohou zlepšit prezentaci vašich dat. Co se ale stane, když se tyto tvary překrývají nebo je třeba změnit jejich pořadí? To je místo, kde Aspose.Cells pro .NET září. V tomto kurzu vás provedeme kroky k manipulaci s tvary v listu aplikace Excel, konkrétně k odesílání tvarů na přední nebo zadní stranu jiných tvarů. Pokud jste připraveni vylepšit svou hru Excel, pojďme se do toho pustit!
## Předpoklady
Než začneme, musíte mít připraveno několik věcí:
1.  Instalace knihovny Aspose.Cells: Ujistěte se, že máte nainstalovanou knihovnu Aspose.Cells pro .NET. Můžete to najít[zde](https://releases.aspose.com/cells/net/).
2. Vývojové prostředí: Ujistěte se, že máte nastavené vývojové prostředí s podporou .NET, jako je Visual Studio.
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.
Dobře, zaškrtli jste všechna políčka v seznamu předpokladů? Velký! Přejděme k zábavnější části – psaní kódu!
## Importujte balíčky
Než se vrhneme na samotné kódování, naimportujeme potřebné balíčky. Stačí přidat následující direktivu pomocí příkazu v horní části souboru C#:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Tyto jmenné prostory jsou klíčové, protože obsahují třídy a metody, které budeme používat k manipulaci se soubory a tvary aplikace Excel.
## Krok 1: Definujte cesty k souborům
V tomto prvním kroku musíme vytvořit zdrojový a výstupní adresář. Zde se nachází váš soubor Excel a kam chcete uložit upravený soubor.
```csharp
//Zdrojový adresář
string sourceDir = "Your Document Directory";
//Výstupní adresář
string outputDir = "Your Document Directory";
```
 Nahradit`"Your Document Directory"` se skutečnou cestou, kde jsou uloženy vaše soubory Excel.
## Krok 2: Načtěte sešit
Nyní, když máme nastavené adresáře, načteme sešit (soubor Excel), který obsahuje tvary, se kterými chceme manipulovat.
```csharp
//Načtěte zdrojový soubor Excel
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
 Tento řádek kódu inicializuje nový`Workbook` objekt, načtení zadaného excelovského souboru do paměti, abychom s ním mohli pracovat.
## Krok 3: Otevřete sešit 
Dále musíme získat přístup ke konkrétnímu listu, kde jsou umístěny naše tvary. Pro tento příklad použijeme první pracovní list.
```csharp
//Přístup k prvnímu listu
Worksheet ws = wb.Worksheets[0];
```
 Odkazováním`Worksheets[0]`, zaměřujeme se na první list našeho sešitu. Pokud jsou vaše tvary na jiném listu, upravte podle toho index.
## Krok 4: Přístup k Shapes
Když máme připravený přístup k listu, uchopme tvary, které nás zajímají. V tomto příkladu přistoupíme k prvnímu a čtvrtému tvaru.
```csharp
//Přístup k prvnímu a čtvrtému tvaru
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Tyto řádky získají konkrétní tvary z listu na základě jejich indexu.
## Krok 5: Vytiskněte pozici Z-Order tvarů
Než nějaké tvary přesuneme, vytiskneme si jejich aktuální pozici Z-Order. To nám pomáhá sledovat jejich umístění, než provedeme změny.
```csharp
//Vytiskněte polohu Z-Order tvaru
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
 Zavoláním`ZOrderPosition`, můžeme vidět, kde každý tvar sedí v pořadí kreslení.
## Krok 6: Odešlete první tvar dopředu
Nyní je čas na akci! Pošleme první tvar do přední části Z-Řádu.
```csharp
//Pošlete tento tvar dopředu
sh1.ToFrontOrBack(2);
```
 Míjením`2` na`ToFrontOrBack`, dáváme Aspose.Cells pokyn, aby tento tvar přenesl dopředu. 
## Krok 7: Vytiskněte pozici Z-pořadí druhého tvaru
Než pošleme druhý tvar na zadní stranu, zkontrolujeme, kde je umístěn.
```csharp
//Vytiskněte polohu Z-Order tvaru
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
To nám umožňuje nahlédnout do pozice čtvrtého tvaru předtím, než provedeme jakékoli změny.
## Krok 8: Odešlete čtvrtý tvar dozadu
Nakonec odešleme čtvrtý tvar do zadní části zásobníku Z-Řádu.
```csharp
//Pošlete tento tvar dozadu
sh4.ToFrontOrBack(-2);
```
 Použití`-2` protože parametr posílá tvar směrem k zadní části zásobníku, což zajišťuje, že nebude překážet jiným tvarům nebo textu.
## Krok 9: Uložte sešit 
Posledním krokem je uložení sešitu s nově umístěnými tvary.
```csharp
//Uložte výstupní soubor aplikace Excel
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Tento příkaz uloží upravený sešit do zadaného výstupního adresáře.
## Krok 10: Potvrzující zpráva
Nakonec udělejme jednoduché potvrzení, abychom věděli, že náš úkol byl úspěšně dokončen.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
tím je kód pro náš tutoriál uzavřen!
## Závěr
Manipulace s tvary v Excelu pomocí Aspose.Cells pro .NET je nejen přímočará, ale také výkonná. Podle této příručky byste nyní měli být schopni snadno odesílat tvary dopředu nebo dozadu, což umožňuje lepší kontrolu nad prezentacemi aplikace Excel. S těmito nástroji, které máte k dispozici, jste připraveni zlepšit vizuální přitažlivost svých tabulek.
## FAQ
### Jaký programovací jazyk potřebuji pro Aspose.Cells?  
Pro práci s Aspose.Cells musíte použít C# nebo jakýkoli jiný jazyk podporovaný .NET.
### Mohu vyzkoušet Aspose.Cells zdarma?  
 Ano, můžete začít s bezplatnou zkušební verzí Aspose.Cells[zde](https://releases.aspose.com/).
### S jakými tvary mohu v Excelu manipulovat?  
Můžete manipulovat s různými tvary, jako jsou obdélníky, kruhy, čáry a obrázky.
### Jak mohu získat podporu pro Aspose.Cells?  
 Pro jakoukoli podporu nebo dotazy můžete navštívit jejich komunitní fórum[zde](https://forum.aspose.com/c/cells/9).
### Je k dispozici dočasná licence pro Aspose.Cells?  
 Ano, můžete požádat o dočasnou licenci[zde](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
