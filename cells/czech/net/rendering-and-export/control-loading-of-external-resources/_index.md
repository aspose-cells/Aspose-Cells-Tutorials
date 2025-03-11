---
title: Ovládání externích zdrojů v Excelu do PDF v Aspose.Cells
linktitle: Ovládání externích zdrojů v Excelu do PDF v Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Objevte, jak ovládat externí zdroje v Excelu do PDF převodu pomocí Aspose.Cells for .NET s naším snadno pochopitelným průvodcem.
weight: 12
url: /cs/net/rendering-and-export/control-loading-of-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ovládání externích zdrojů v Excelu do PDF v Aspose.Cells

## Zavedení
V dnešní digitální době je převod tabulek Excelu na dokumenty PDF běžným úkolem. Ať už se jedná o přípravu zpráv, finančních dat nebo prezentačních materiálů, chcete zajistit, aby vaše soubory PDF vypadaly přesně tak, jak je zamýšlíte. Aspose.Cells for .NET je robustní knihovna, která vám umožňuje řídit tento proces převodu do posledního detailu, zejména při manipulaci s externími zdroji, jako jsou obrázky, které doprovázejí vaše soubory Excel. V této příručce se ponoříme do toho, jak ovládat externí zdroje během procesu převodu Excel do PDF pomocí Aspose.Cells. Takže si vezměte svůj oblíbený nápoj a můžeme začít!
## Předpoklady
Než se vrhneme na to, co se dá, ujistíme se, že máte vše, co potřebujete, abyste se mohli rozjet. Zde je rychlý kontrolní seznam:
1. Visual Studio nebo jakékoli IDE kompatibilní s .NET: Budete chtít prostředí pro psaní a testování kódu.
2.  Aspose.Cells for .NET: Pokud jste jej ještě nenainstalovali, přejděte na[Aspose ke stažení](https://releases.aspose.com/cells/net/) stránku a stáhněte si nejnovější verzi.
3. Základní znalost C#: Užitečná bude znalost programovacího jazyka C#. Pokud si nejste jisti nějakými pojmy, neváhejte si je vyhledat.
4. Ukázkový soubor Excel: Připravte soubor Excel s jakýmikoli externími zdroji, které chcete převést. Můžete použít poskytnutý ukázkový soubor "samplePdfSaveOptions_StreamProvider.xlsx".
5. Soubor obrázku pro testování: Tento soubor bude použit jako externí zdroj během převodu. Soubor obrázku „newPdfSaveOptions_StreamProvider.png“ je dobrým zástupným symbolem.
## Importujte balíčky
Chcete-li to nastartovat, budete muset importovat potřebné jmenné prostory z knihovny Aspose.Cells. To je klíčové pro přístup k jeho funkcím. Ujistěte se, že jste pomocí direktiv v horní části souboru přidali následující:
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
 Prvním úkolem je vytvořit třídu poskytovatele streamu, která implementuje`IStreamProvider` rozhraní. Tato třída vám umožní řídit, jak se načítají externí zdroje.
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
        // Přečtěte si nový obrázek v paměťovém streamu a přiřaďte jej vlastnosti Stream
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
V této třídě:
- CloseStream: Tato metoda bude volána, když je stream uzavřen. Zatím jen píšeme ladicí zprávu pro sledování.
-  InitStream: Tady začíná kouzlo. Zde načtete svůj externí obrázek jako bajtové pole, převedete jej na paměťový proud a přiřadíte jej`options.Stream` vlastnictví.
## Krok 2: Nastavte zdrojové a výstupní adresáře
Nyní, když je váš poskytovatel streamu připraven, je čas určit, kde se váš soubor Excel nachází a kam chcete uložit PDF.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Výstupní adresář
string outputDir = "Your Document Directory";
```
 Jednoduše vyměnit`"Your Document Directory"` se skutečnou cestou ve vašem počítači, kde jsou uloženy vaše soubory. Udržování pořádku v souborech je klíčové!
## Krok 3: Načtěte soubor Excel
Dále načtete soubor Excel, ze kterého chcete vytvořit PDF.
```csharp
// Načtěte zdrojový soubor Excel obsahující externí obrázky
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
 Používáme`Workbook` třídy z Aspose.Cells, která představuje váš soubor Excel. Soubor může obsahovat různé externí zdroje, jako jsou obrázky, které chcete během převodu ovládat.
## Krok 4: Nastavte možnosti uložení PDF
Než sešit uložíte jako PDF, určete, jak jej chcete uložit. Tyto možnosti můžete upravit podle svých požadavků.
```csharp
// Zadejte možnosti uložení PDF - Poskytovatel streamu
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Uložte každý list na novou stránku
```
 Zde vytváříme novou instanci`PdfSaveOptions` , která vám umožní přizpůsobit, jak bude váš PDF formátován. The`OnePagePerSheet`Tato možnost je užitečná pro zajištění toho, že každý list aplikace Excel dostane svou vlastní stránku ve výsledném PDF.
## Krok 5: Přiřaďte svého poskytovatele streamování
Když máte nastavené možnosti PDF, musíte Aspose říct, aby používal vašeho vlastního poskytovatele streamu pro externí zdroje.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
 Tato linka spojuje vaše`Workbook` příklad s`MyStreamProvider` třídu, kterou jste dříve vytvořili. To znamená, že kdykoli během převodu narazíte na externí zdroje, váš poskytovatel s nimi naloží tak, jak je uvedeno.
## Krok 6: Uložte sešit jako PDF
Když je vše nastaveno, je konečně čas uložit sešit aplikace Excel jako PDF.
```csharp
// Uložte sešit do Pdf
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
 Zavoláním na`Save` metodou na objekt sešitu a předáním výstupního adresáře spolu s možnostmi PDF převedete soubor Excel do krásně formátovaného PDF.
## Krok 7: Potvrďte úspěšné provedení
Abychom vše uzavřeli, je vždy příjemné potvrdit, že váš proces byl úspěšný!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Vytištění zprávy o úspěchu na konzoli vám pomůže získat informace o stavu vaší operace. Je dobrým zvykem zahrnout tato malá potvrzení do vašeho kódu.
## Závěr
Tady to máš! Dodržováním těchto jednoduchých kroků můžete odborně ovládat, jak se zachází s externími zdroji během převodu Excelu do PDF pomocí Aspose.Cells. To znamená, že vaše dokumenty mohou nyní přesně obsahovat obrázky a další externí prvky, což pokaždé zajistí vyleštěný konečný produkt.
## FAQ
### Co je Aspose.Cells?  
Aspose.Cells je výkonná knihovna pro vývojáře .NET, která vám umožňuje vytvářet, manipulovat, převádět a vykreslovat soubory aplikace Excel v různých formátech.
### Jak stáhnu Aspose.Cells?  
 Nejnovější verzi Aspose.Cells si můžete stáhnout z[Odkaz ke stažení](https://releases.aspose.com/cells/net/).
### Mohu vyzkoušet Aspose.Cells zdarma?  
 Ano! Můžete získat bezplatnou zkušební verzi návštěvou[Bezplatná zkušební stránka](https://releases.aspose.com/).
### Kde najdu podporu pro Aspose.Cells?  
 V případě jakýchkoli dotazů souvisejících s podporou můžete navštívit stránku[Fórum podpory Aspose](https://forum.aspose.com/c/cells/9).
### Jak mohu získat dočasnou licenci pro Aspose.Cells?  
 Můžete požádat o dočasnou licenci[zde](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
