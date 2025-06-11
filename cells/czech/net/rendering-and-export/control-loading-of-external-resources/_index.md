---
"description": "Zjistěte, jak ovládat externí zdroje při převodu z Excelu do PDF pomocí Aspose.Cells pro .NET s naším snadno srozumitelným průvodcem."
"linktitle": "Ovládání externích zdrojů v Excelu do PDF v Aspose.Cells"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Ovládání externích zdrojů v Excelu do PDF v Aspose.Cells"
"url": "/cs/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ovládání externích zdrojů v Excelu do PDF v Aspose.Cells

## Zavedení
V dnešní digitální době je převod excelových tabulek do PDF dokumentů běžným úkolem. Ať už se jedná o přípravu zpráv, finančních dat nebo prezentačních materiálů, chcete mít jistotu, že vaše PDF soubory budou vypadat přesně tak, jak si představujete. Aspose.Cells pro .NET je robustní knihovna, která vám umožňuje řídit tento proces převodu do posledního detailu, zejména při práci s externími zdroji, jako jsou obrázky, které doprovázejí vaše excelovské soubory. V této příručce se ponoříme do toho, jak ovládat externí zdroje během procesu převodu Excelu do PDF pomocí Aspose.Cells. Takže si vezměte svůj oblíbený nápoj a pojďme na to!
## Předpoklady
Než se pustíme do detailů, ujistěte se, že máte vše, co potřebujete k zahájení. Zde je stručný kontrolní seznam:
1. Visual Studio nebo jakékoli IDE kompatibilní s .NET: Budete potřebovat prostředí pro psaní a testování kódu.
2. Aspose.Cells pro .NET: Pokud jste si ho ještě nenainstalovali, přejděte na [Soubory ke stažení Aspose](https://releases.aspose.com/cells/net/) stránku a stáhněte si nejnovější verzi.
3. Základní znalost C#: Znalost programovacího jazyka C# bude užitečná. Pokud si nejste jisti nějakými koncepty, neváhejte si je vyhledat.
4. Ukázkový soubor Excel: Připravte si soubor Excel se všemi externími zdroji, které chcete převést. Můžete použít poskytnutý ukázkový soubor „samplePdfSaveOptions_StreamProvider.xlsx“.
5. Soubor obrázku pro testování: Tento soubor bude použit jako externí zdroj během převodu. Soubor obrázku „newPdfSaveOptions_StreamProvider.png“ je vhodným zástupným symbolem.
## Importovat balíčky
Pro zahájení budete muset importovat potřebné jmenné prostory z knihovny Aspose.Cells. To je klíčové pro přístup k jejím funkcím. Nezapomeňte na začátek souboru přidat následující direktivy using:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Tyto balíčky poskytnou všechny základní třídy a metody, které budete potřebovat k provádění svých úkolů.
## Krok 1: Vytvořte třídu poskytovatele streamu
Prvním úkolem je vytvořit třídu poskytovatele streamu, která implementuje `IStreamProvider` rozhraní. Tato třída vám umožní řídit, jak se načítají externí zdroje.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // Načíst nový obrázek v paměťovém proudu a přiřadit ho k vlastnosti Stream.
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
V této třídě:
- CloseStream: Tato metoda bude volána při uzavření streamu. Prozatím pouze píšeme ladicí zprávu pro sledování.
- InitStream: Tady začíná magie. Zde načtete svůj externí obraz jako bajtové pole, převedete ho do paměťového proudu a přiřadíte ho k `options.Stream` vlastnictví.
## Krok 2: Nastavení zdrojového a výstupního adresáře
Nyní, když je váš poskytovatel streamování připraven, je čas určit, kde se nachází váš soubor Excel a kam chcete uložit PDF.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Výstupní adresář
string outputDir = "Your Document Directory";
```
Jednoduše vyměňte `"Your Document Directory"` se skutečnou cestou v počítači, kde se vaše soubory nacházejí. Udržování pořádku v souborech je klíčové!
## Krok 3: Načtěte soubor aplikace Excel
Dále načtete soubor aplikace Excel, ze kterého chcete vytvořit PDF.
```csharp
// Načíst zdrojový soubor Excel obsahující externí obrázky
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
Používáme `Workbook` třída z Aspose.Cells, která představuje váš soubor Excel. Soubor může obsahovat různé externí zdroje, jako jsou obrázky, které chcete během převodu ovládat.
## Krok 4: Nastavení možností ukládání PDF
Než sešit uložíte jako PDF, určete si, jak ho chcete uložit. Tyto možnosti můžete upravit podle svých požadavků.
```csharp
// Zadejte možnosti ukládání PDF – poskytovatel streamu
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Uložit každý list na novou stránku
```
Zde vytváříme novou instanci `PdfSaveOptions`což vám umožňuje přizpůsobit formátování PDF. `OnePagePerSheet` Tato možnost je užitečná pro zajištění toho, aby každý list aplikace Excel měl ve výsledném PDF souborech svou vlastní stránku.
## Krok 5: Přiřaďte svého poskytovatele streamu
Po nastavení možností PDF musíte službě Aspose sdělit, aby pro externí zdroje používala vašeho vlastního poskytovatele streamování.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
Tato linka spojuje vaše `Workbook` instance s `MyStreamProvider` třídu, kterou jste vytvořili dříve. To znamená, že kdykoli se během převodu setkáte s externími zdroji, váš poskytovatel s nimi bude zacházet dle specifikace.
## Krok 6: Uložte sešit jako PDF
Jakmile je vše nastaveno, je konečně čas uložit sešit aplikace Excel jako PDF.
```csharp
// Uložit sešit do PDF
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
Zavoláním `Save` metodu na objektu sešitu a předáním výstupního adresáře spolu s možnostmi PDF převedete soubor Excel do krásně formátovaného PDF.
## Krok 7: Potvrzení úspěšného provedení
Na závěr je vždycky hezké potvrdit, že váš proces proběhl úspěšně!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Výpis zprávy o úspěšném provedení do konzole vám pomůže informovat se o stavu vaší operace. Je dobrým zvykem zahrnout tato malá potvrzení do kódu.
## Závěr
A máte to! Dodržováním těchto jednoduchých kroků můžete odborně ovládat, jak se s externími zdroji pracuje během převodů z Excelu do PDF pomocí Aspose.Cells. To znamená, že vaše dokumenty nyní mohou přesně obsahovat obrázky a další externí prvky, což pokaždé zajistí dokonale vybroušený konečný produkt.
## Často kladené otázky
### Co je Aspose.Cells?  
Aspose.Cells je výkonná knihovna pro vývojáře .NET, která umožňuje vytvářet, manipulovat, převádět a vykreslovat soubory Excelu v různých formátech.
### Jak si stáhnu Aspose.Cells?  
Nejnovější verzi Aspose.Cells si můžete stáhnout z [Odkaz ke stažení](https://releases.aspose.com/cells/net/).
### Mohu si Aspose.Cells vyzkoušet zdarma?  
Ano! Zkušební verzi zdarma můžete získat na [Stránka s bezplatnou zkušební verzí](https://releases.aspose.com/).
### Kde najdu podporu pro Aspose.Cells?  
jakýmikoli dotazy týkajícími se podpory můžete navštívit [Fórum podpory Aspose](https://forum.aspose.com/c/cells/9).
### Jak mohu získat dočasnou licenci pro Aspose.Cells?  
Můžete požádat o dočasnou licenci [zde](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}