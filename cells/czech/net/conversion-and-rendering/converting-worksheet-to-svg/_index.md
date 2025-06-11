---
"description": "Naučte se, jak převést list aplikace Excel do formátu SVG pomocí Aspose.Cells pro .NET v tomto podrobném návodu. Ideální pro vývojáře .NET, kteří chtějí vykreslit Excel do formátu SVG."
"linktitle": "Převod pracovního listu do SVG v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Převod pracovního listu do SVG v .NET"
"url": "/cs/net/conversion-and-rendering/converting-worksheet-to-svg/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Převod pracovního listu do SVG v .NET

## Zavedení

Pokud chcete převést list aplikace Excel do formátu SVG, jste na správném místě! Aspose.Cells pro .NET je výkonný nástroj, který umožňuje vývojářům manipulovat s excelovými soubory a převádět je do různých formátů, včetně široce podporovaného SVG (Scalable Vector Graphics). Tento tutoriál vás provede procesem převodu listu do formátu SVG v .NET a rozebere ho krok za krokem, takže i začátečníci ho snadno zvládnou.

## Předpoklady

Než se ponoříme do kódu, ujistěte se, že máte vše potřebné:

1. Aspose.Cells pro .NET: Stáhněte a nainstalujte nejnovější verzi Aspose.Cells pro .NET z [Aspose.Cells pro .NET](https://releases.aspose.com/cells/net/).
2. Vývojové prostředí .NET: Budete potřebovat nainstalované Visual Studio nebo jakékoli jiné vývojové prostředí .NET.
3. Základní znalost C#: Znalost C# je vyžadována, ale nebojte se, vše vám srozumitelně vysvětlíme.
4. Soubor Excel: Mějte připravený soubor Excel, který chcete převést do formátu SVG.

## Import potřebných balíčků

Než se pustíte do kódování, nezapomeňte na začátek souboru C# uvést požadované jmenné prostory.

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

Tyto balíčky jsou nezbytné pro práci s Aspose.Cells a pro zpracování možností vykreslování, jako je export SVG.

Nyní, když jsme si probrali základy, pojďme se pustit do samotných kroků převodu listu aplikace Excel do obrázku SVG.

## Krok 1: Nastavení cesty k adresáři dokumentů

První věc, kterou potřebujeme, je definovat cestu ke složce, kde se nachází váš soubor Excel. To je klíčové, protože váš kód bude odkazovat na tento adresář pro načítání a ukládání souborů.

```csharp
// Cesta k adresáři s dokumenty
string dataDir = "Your Document Directory";
```

Nezapomeňte vyměnit `"Your Document Directory"` se skutečnou cestou, kde se nachází váš soubor Excel.

## Krok 2: Načtěte soubor Excel pomocí `Workbook`

Dále musíme načíst soubor Excel do instance `Workbook` třída. Ta `Workbook` Třída představuje celý soubor aplikace Excel, včetně všech listů v něm obsažených.

```csharp
string filePath = dataDir + "Template.xlsx";
Workbook book = new Workbook(filePath);
```

Zde, `"Template.xlsx"` je název souboru aplikace Excel, se kterým pracujete. Ujistěte se, že tento soubor existuje v zadaném adresáři, jinak se setkáte s chybami.

## Krok 3: Nastavení možností obrázku nebo tisku pro převod SVG

Než budeme moci převést pracovní list do formátu SVG, musíme zadat možnosti obrázku. `ImageOrPrintOptions` třída umožňuje ovládat, jak bude pracovní list převeden. Konkrétně musíme nastavit `SaveFormat` na `SVG` a ujistěte se, že každý pracovní list je převeden na jednu stránku.

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.SaveFormat = SaveFormat.Svg;
imgOptions.OnePagePerSheet = true;
```

Ten/Ta/To `SaveFormat.Svg` Možnost zajišťuje, že výstupní formát bude SVG, zatímco `OnePagePerSheet` zajišťuje, že každý pracovní list bude vykreslen na jedné stránce.

## Krok 4: Iterujte každým listem v sešitu

Nyní musíme projít všechny listy v souboru aplikace Excel. Každý list bude převeden jednotlivě.

```csharp
foreach (Worksheet sheet in book.Worksheets)
{
    // Každý pracovní list budeme zpracovávat jeden po druhém.
}
```

Tato smyčka zajišťuje, že bez ohledu na to, kolik listů je v sešitu přítomno, bude zpracován každý z nich.

## Krok 5: Vytvořte `SheetRender` Objekt pro vykreslování

Pro každý pracovní list vytvoříme `SheetRender` objekt. Tento objekt je zodpovědný za převod listu do požadovaného obrazového formátu, kterým je v tomto případě SVG.

```csharp
SheetRender sr = new SheetRender(sheet, imgOptions);
```

Ten/Ta/To `SheetRender` Objekt přijímá dva argumenty: list, který převádíte, a možnosti obrázku, které jste definovali dříve.

## Krok 6: Převod pracovního listu do formátu SVG

Nakonec v rámci smyčky převedeme každý list do formátu SVG. Pro iteraci mezi stránkami použijeme vnořenou smyčku (i když v tomto případě je na listu pouze jedna stránka, díky `OnePagePerSheet` volba).

```csharp
for (int i = 0; i < sr.PageCount; i++)
{
    // Výstup pracovního listu do formátu obrázku Svg
    sr.ToImage(i, filePath + sheet.Name + i + ".out.svg");
}
```

Tento kód uloží list jako soubor SVG do stejného adresáře jako soubor Excelu. Každý soubor SVG bude pojmenován podle názvu listu a indexového čísla, aby se předešlo konfliktům názvů.

## Závěr

to je vše! Úspěšně jste převedli list aplikace Excel do formátu SVG pomocí nástroje Aspose.Cells pro .NET. Tento proces vám umožňuje zachovat rozvržení a design listu a zároveň jej zobrazit v jakémkoli prohlížeči nebo zařízení, které podporuje SVG, což je v podstatě všechno. Ať už pracujete se složitými soubory aplikace Excel nebo jen s jednoduchou tabulkou, tato metoda zajistí, že vaše data budou krásně vykreslena ve webově přívětivém formátu.

## Často kladené otázky

### Co je SVG a proč bych ho měl používat?
SVG (Scalable Vector Graphics) je webový formát, který lze nekonečně škálovat bez ztráty kvality. Je ideální pro grafy, diagramy a obrázky, které je třeba zobrazit v různých velikostech.

### Dokáže Aspose.Cells zpracovat velké soubory Excelu pro konverzi?
Ano, Aspose.Cells dokáže efektivně zpracovávat velké soubory Excelu a převádět je do formátu SVG bez významných problémů s výkonem.

### Existuje omezení počtu pracovních listů, které mohu převést do formátu SVG?
Ne, v Aspose.Cells neexistuje žádné inherentní omezení pro převod více pracovních listů. Jediným omezením by byla paměť a výkon vašeho systému.

### Potřebuji licenci k používání Aspose.Cells?
Ano, Aspose.Cells vyžaduje licenci pro produkční použití. Můžete získat dočasnou licenci. [zde](https://purchase.aspose.com/temporary-license/) nebo prozkoumejte [bezplatná zkušební verze](https://releases.aspose.com/).

### Mohu si přizpůsobit SVG výstup?
Ano, můžete to upravit `ImageOrPrintOptions` pro přizpůsobení různých aspektů SVG výstupu, jako je rozlišení a škálování.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}