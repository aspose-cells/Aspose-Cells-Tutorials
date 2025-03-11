---
title: Uložit sešit do textového formátu CSV
linktitle: Uložit sešit do textového formátu CSV
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak bez námahy převést excelové sešity do formátu CSV pomocí Aspose.Cells v tomto komplexním, podrobném návodu určeném pro vývojáře .NET.
weight: 17
url: /cs/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uložit sešit do textového formátu CSV

## Zavedení
Při práci s daty může zvolený formát skutečně určit, jak snadno s nimi můžete pracovat. Mezi nejběžnější formáty pro práci s tabulkovými daty patří CSV (Comma-Separated Values). Pokud jste vývojář pracující se soubory aplikace Excel a potřebujete převést sešity do formátu CSV, Aspose.Cells for .NET je fantastická knihovna, která tento úkol zjednoduší. V tomto tutoriálu rozebereme kroky k bezproblémovému převodu sešitu aplikace Excel do textového formátu CSV.
## Předpoklady
Než se do toho pustíme, ujistěte se, že máte vše připraveno, abyste mohli začít:
1. Základní znalost C# a .NET: Protože budeme psát kód v C#, znalost jazyka a .NET frameworku je nezbytná.
2. Knihovna Aspose.Cells: Ujistěte se, že máte ve vývojovém prostředí nainstalovanou knihovnu Aspose.Cells for .NET. Můžete si jej stáhnout[zde](https://releases.aspose.com/cells/net/).
3. Visual Studio nebo libovolné C# IDE: K psaní a spouštění kódu budete potřebovat integrované vývojové prostředí (IDE). Visual Studio je oblíbenou volbou.
4. Sešit aplikace Excel: Připravte si vzorový sešit aplikace Excel (např. "sešit1.xls"), který obsahuje některá data pro testování převodu.
## Importujte balíčky
Nyní, když máme pokryty naše předpoklady, je prvním krokem v procesu import potřebných balíčků. Ve svém projektu C# musíte v horní části souboru kódu zahrnout následující jmenný prostor:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Tyto jmenné prostory vám umožní přístup ke třídám a metodám potřebným pro práci se soubory aplikace Excel a správu paměťových proudů.
## Krok 1: Definujte cestu k adresáři dokumentů
Prvním krokem v našem procesu je definovat, kde jsou naše dokumenty (sešity Excelu) uloženy. To je nezbytné, protože to našemu programu umožňuje vědět, kde najít soubory, které potřebuje zpracovat. 
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```
 Nezapomeňte vyměnit`"Your Document Directory"` se skutečnou cestou, kde se nachází váš soubor "book1.xls". Může to být adresář ve vašem počítači nebo cesta k serveru.
## Krok 2: Načtěte zdrojový sešit
Dále musíme načíst sešit Excel, který bude převeden do formátu CSV.
```csharp
// Načtěte zdrojový sešit
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 The`Workbook` třída z knihovny Aspose.Cells umožňuje manipulaci a přístup k sešitům aplikace Excel. Předáním cesty k souboru načítáme určený sešit ke zpracování.
## Krok 3: Inicializujte bajtové pole pro data sešitu
Než začneme převádět sešit do CSV, musíme inicializovat prázdné pole bajtů, které nakonec pojme všechna data listu.
```csharp
// Pole 0 bajtů
byte[] workbookData = new byte[0];
```
Toto bajtové pole spojí data z každého listu do jediné struktury, kterou můžeme později zapsat do souboru.
## Krok 4: Nastavte možnosti ukládání textu
Nyní nastavíme možnosti, jak chceme uložit formát textu. Můžete si vybrat vlastní oddělovače nebo držet s tabulátory.
```csharp
// Možnosti uložení textu. Můžete použít jakýkoli typ oddělovače
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // Karta nastavení jako oddělovač
```
 V tomto příkladu používáme jako oddělovač znak tabulátoru. Můžete vyměnit`'\t'` s jakoukoli postavou, kterou si přejete, jako je čárka (`,`), v závislosti na tom, jak chcete formát CSV.
## Krok 5: Iterujte každý list
 Dále projdeme všechny listy v sešitu a každý si uložíme do svého`workbookData` pole, ale nejprve musíte vybrat, se kterým listem chcete pracovat.
```csharp
// Zkopírujte data každého listu v textovém formátu do datového pole sešitu
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // Uložte aktivní list do textového formátu
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
 Smyčka prochází každým listem v sešitu.`ActiveSheetIndex` je nastaven tak, že pokaždé, když procházíme smyčkou, ukládáme aktuální list. Výsledky se uloží do paměti pomocí a`MemoryStream`.
## Krok 6: Načtěte data listu
 Po uložení listu do paměťového toku je dalším krokem načtení těchto dat a jejich připojení k našemu`workbookData` pole.
```csharp
    // Uložte data listu do pole dat listu
    ms.Position = 0; // Resetovat pozici toku paměti
    byte[] sheetData = ms.ToArray(); // Získejte bajtové pole
```
`ms.Position = 0;` resetuje pozici pro čtení po zápisu. Pak použijeme`ToArray()` převést paměťový proud na bajtové pole, které obsahuje data listu.
## Krok 7: Kombinujte data listu
 Nyní zkombinujeme data z každého listu do jednoho`workbookData` pole inicializováno dříve.
```csharp
    // Zkombinujte tato data listu do datového pole sešitu
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
Vytvoříme nové pole, které je dostatečně velké, aby se do něj vešla jak stávající data sešitu, tak data nového listu. Poté zkopírujeme stávající a nová data do tohoto kombinovaného pole pro pozdější použití.
## Krok 8: Uložte celá data sešitu do souboru
 Nakonec se všemi údaji spojenými v našem`workbookData` pole, můžeme toto pole uložit do zadané cesty k souboru.
```csharp
//Uložte celá data sešitu do souboru
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` vezme kombinované bajtové pole a zapíše je do textového souboru s názvem "out.txt" v určeném adresáři.
## Závěr
A tady to máte! Úspěšně jste převedli sešit aplikace Excel do formátu CSV pomocí Aspose.Cells for .NET. Nejen, že je tento proces efektivní, ale umožňuje snadnou manipulaci s excelovými daty pro další analýzu nebo reportování. Nyní můžete automatizovat své úlohy zpracování dat nebo dokonce integrovat tuto funkci do větších aplikací.
## FAQ
### Mohu pro soubor CSV použít různé oddělovače?
 Ano, můžete změnit`opts.Separator` na jakýkoli požadovaný znak, jako jsou čárky nebo čárky.
### Je Aspose.Cells zdarma k použití?
 Aspose.Cells není zdarma, ale můžete získat bezplatnou zkušební verzi[zde](https://releases.aspose.com/).
### Do jakých typů formátů mohu ukládat kromě CSV?
Aspose.Cells umožňuje ukládání do více formátů včetně XLSX, PDF a dalších.
### Mohu zpracovat velké soubory aplikace Excel pomocí Aspose.Cells?
Ano, Aspose.Cells je navržen tak, aby efektivně zpracovával velké soubory, ale výkon může záviset na systémových prostředcích.
### Kde najdu podrobnější dokumentaci?
Najdete na nich komplexní dokumentaci a příklady[referenční místo](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
