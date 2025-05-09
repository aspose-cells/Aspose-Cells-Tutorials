---
"description": "Naučte se, jak snadno převést sešity aplikace Excel do formátu CSV pomocí Aspose.Cells v tomto komplexním, podrobném tutoriálu určeném pro vývojáře .NET."
"linktitle": "Uložit sešit do textového formátu CSV"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Uložit sešit do textového formátu CSV"
"url": "/cs/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Uložit sešit do textového formátu CSV

## Zavedení
Při práci s daty může zvolený formát skutečně ovlivnit, jak snadno s nimi budete pracovat. Mezi nejběžnější formáty pro práci s tabulkovými daty patří CSV (hodnoty oddělené čárkami). Pokud jste vývojář pracující s excelovými soubory a potřebujete převést sešity do formátu CSV, Aspose.Cells for .NET je fantastická knihovna, která tento úkol zjednodušuje. V tomto tutoriálu si rozebereme kroky pro bezproblémový převod excelového sešitu do textového formátu CSV.
## Předpoklady
Než se do toho pustíme, ujistěte se, že máte vše připravené k zahájení:
1. Základní znalost C# a .NET: Protože budeme psát kód v C#, je znalost jazyka a frameworku .NET nezbytná.
2. Knihovna Aspose.Cells: Ujistěte se, že máte ve svém vývojovém prostředí nainstalovanou knihovnu Aspose.Cells pro .NET. Můžete si ji stáhnout [zde](https://releases.aspose.com/cells/net/).
3. Visual Studio nebo jakékoli vývojové prostředí C#: Pro psaní a spouštění kódu budete potřebovat integrované vývojové prostředí (IDE). Visual Studio je oblíbenou volbou.
4. Sešit aplikace Excel: Připravte si ukázkový sešit aplikace Excel (např. „book1.xls“), který obsahuje nějaká data pro otestování převodu.
## Importovat balíčky
Nyní, když máme pokryty všechny předpoklady, je prvním krokem import potřebných balíčků. Ve vašem projektu C# je třeba na začátek souboru s kódem zahrnout následující jmenný prostor:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Tyto jmenné prostory vám poskytnou přístup ke třídám a metodám potřebným pro práci s excelovými soubory a správu paměťových streamů.
## Krok 1: Definujte cestu k adresáři dokumentů
Prvním krokem v našem procesu je definování místa, kde jsou uloženy naše dokumenty (sešity aplikace Excel). To je nezbytné, protože to našemu programu umožňuje vědět, kde najít soubory, které potřebuje zpracovat. 
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
```
Nezapomeňte vyměnit `"Your Document Directory"` se skutečnou cestou, kde se nachází váš soubor „book1.xls“. Může se jednat o adresář ve vašem počítači nebo cestu k serveru.
## Krok 2: Načtěte zdrojový sešit
Dále musíme načíst sešit aplikace Excel, který bude převeden do formátu CSV.
```csharp
// Načtěte zdrojový sešit
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
Ten/Ta/To `Workbook` Třída z knihovny Aspose.Cells umožňuje manipulaci a přístup k sešitům aplikace Excel. Předáním cesty k souboru načítáme zadaný sešit ke zpracování.
## Krok 3: Inicializace bajtového pole pro data sešitu
Než začneme s převodem sešitu do formátu CSV, musíme inicializovat prázdné bajtové pole, které bude nakonec obsahovat všechna data listu.
```csharp
// 0bajtové pole
byte[] workbookData = new byte[0];
```
Toto bajtové pole zkombinuje data z každého listu do jedné struktury, kterou můžeme později zapsat do souboru.
## Krok 4: Nastavení možností ukládání textu
Nyní nastavme možnosti, jak chceme ukládat formát textu. Můžete si vybrat vlastní oddělovače nebo se držet tabulátorů.
```csharp
// Možnosti ukládání textu. Můžete použít libovolný typ oddělovače.
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // Nastavení tabulátoru jako oddělovače
```
V tomto příkladu používáme jako oddělovač znak tabulátoru. Můžete jej nahradit `'\t'` s libovolným znakem, například čárkou (`,`), v závislosti na tom, jak chcete formátovat soubor CSV.
## Krok 5: Iterujte každým pracovním listem
Dále projdeme všechny listy v sešitu a každý z nich uložíme do našeho `workbookData` pole, ale nejprve musíte vybrat, na kterém listu chcete pracovat.
```csharp
// Zkopírujte data každého listu v textovém formátu do datového pole sešitu
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // Uložit aktivní list do textového formátu
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
Smyčka prochází každým listem v sešitu. `ActiveSheetIndex` je nastaveno tak, že pokaždé, když projdeme smyčkou, ukládáme aktuální pracovní list. Výsledky se uloží do paměti pomocí `MemoryStream`.
## Krok 6: Načtení dat z pracovního listu
Po uložení listu do paměťového proudu je dalším krokem načtení těchto dat a jejich připojení k našemu `workbookData` pole.
```csharp
    // Uložení dat listu do datového pole listu
    ms.Position = 0; // Obnovit pozici paměťového proudu
    byte[] sheetData = ms.ToArray(); // Získejte bajtové pole
```
`ms.Position = 0;` resetuje pozici pro čtení po zápisu. Pak použijeme `ToArray()` převést paměťový proud do bajtového pole, které obsahuje data listu.
## Krok 7: Sloučení dat z pracovního listu
Nyní sloučíme data z každého listu do jednoho `workbookData` pole inicializované dříve.
```csharp
    // Sloučit data z tohoto listu do datového pole sešitu
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
Vytvoříme nové pole, které je dostatečně velké pro uložení dat ze stávajícího sešitu i dat z nového listu. Poté zkopírujeme stávající a nová data do tohoto kombinovaného pole pro pozdější použití.
## Krok 8: Uložení všech dat sešitu do souboru
Nakonec, se všemi daty zkombinovanými v našich `workbookData` pole, můžeme toto pole uložit do zadané cesty k souboru.
```csharp
// Uložit celá data sešitu do souboru
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` vezme kombinované bajtové pole a zapíše ho do textového souboru s názvem „out.txt“ v zadaném adresáři.
## Závěr
A tady to máte! Úspěšně jste převedli sešit aplikace Excel do formátu CSV pomocí nástroje Aspose.Cells pro .NET. Tento proces je nejen efektivní, ale také umožňuje snadnou manipulaci s daty aplikace Excel pro další analýzu nebo vytváření sestav. Nyní můžete automatizovat úlohy zpracování dat nebo tuto funkci integrovat i do větších aplikací.
## Často kladené otázky
### Mohu pro soubor CSV použít různé oddělovače?
Ano, můžete změnit `opts.Separator` na libovolný znak, například čárky nebo svislé čárky.
### Je Aspose.Cells zdarma k použití?
Aspose.Cells není zdarma, ale můžete si ho vyzkoušet zdarma. [zde](https://releases.aspose.com/).
### Do jakých formátů kromě CSV mohu ukládat?
Aspose.Cells umožňuje ukládání do různých formátů včetně XLSX, PDF a dalších.
### Mohu zpracovat velké soubory aplikace Excel pomocí Aspose.Cells?
Ano, Aspose.Cells je navržen pro efektivní zpracování velkých souborů, ale výkon může záviset na systémových zdrojích.
### Kde najdu podrobnější dokumentaci?
Na jejich stránkách najdete komplexní dokumentaci a příklady [referenční místo](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}