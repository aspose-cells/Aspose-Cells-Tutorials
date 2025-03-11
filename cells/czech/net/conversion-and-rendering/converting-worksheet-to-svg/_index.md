---
title: Převod listu do SVG v .NET
linktitle: Převod listu do SVG v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak převést excelový list na SVG pomocí Aspose.Cells for .NET pomocí tohoto podrobného průvodce. Ideální pro vývojáře .NET, kteří chtějí vykreslit Excel do SVG.
weight: 11
url: /cs/net/conversion-and-rendering/converting-worksheet-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod listu do SVG v .NET

## Zavedení

Pokud chcete převést pracovní list aplikace Excel do formátu SVG, jste na správném místě! Aspose.Cells for .NET je výkonný nástroj, který umožňuje vývojářům manipulovat se soubory Excelu a převádět je do různých formátů, včetně široce podporovaného SVG (Scalable Vector Graphics). Tento tutoriál vás provede procesem převodu listu na SVG v .NET, rozdělí jej krok za krokem, takže i začátečníci mohou snadno postupovat.

## Předpoklady

Než se ponoříte do kódu, ujistěte se, že máte vše, co potřebujete:

1.  Aspose.Cells pro .NET: Stáhněte si a nainstalujte nejnovější verzi Aspose.Cells pro .NET z[Aspose.Cells for .NET](https://releases.aspose.com/cells/net/).
2. Vývojové prostředí .NET: Budete potřebovat nainstalované Visual Studio nebo jakékoli jiné .NET IDE.
3. Základní znalost C#: Je nutná znalost C#, ale nebojte, vše srozumitelně vysvětlíme.
4. Soubor Excel: Připravte si soubor Excel, který chcete převést do formátu SVG.

## Import nezbytných balíčků

Než přejdete do části kódování, ujistěte se, že jste v horní části souboru C# zahrnuli požadované jmenné prostory.

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

Tyto balíčky jsou nezbytné pro práci s Aspose.Cells a manipulaci s možnostmi vykreslování, jako je export SVG.

Nyní, když jsou pokryty základy, pojďme se pustit do skutečných kroků převodu listu aplikace Excel na obrázek SVG.

## Krok 1: Nastavte cestu k adresáři vašich dokumentů

První věc, kterou potřebujeme, je definovat cestu ke složce, kde se nachází váš soubor Excel. To je zásadní, protože váš kód bude odkazovat na adresář pro načítání a ukládání souborů.

```csharp
// Cesta k adresáři dokumentů
string dataDir = "Your Document Directory";
```

 Nezapomeňte vyměnit`"Your Document Directory"`se skutečnou cestou, kde se nachází váš soubor Excel.

##  Krok 2: Načtěte soubor aplikace Excel pomocí`Workbook`

 Dále musíme načíst soubor Excel do instance souboru`Workbook` třída. The`Workbook` class představuje celý soubor Excel, včetně všech listů v něm.

```csharp
string filePath = dataDir + "Template.xlsx";
Workbook book = new Workbook(filePath);
```

 Zde,`"Template.xlsx"` je název souboru aplikace Excel, se kterým pracujete. Ujistěte se, že tento soubor existuje v zadaném adresáři, jinak dojde k chybám.

## Krok 3: Nastavte možnosti obrázku nebo tisku pro převod SVG

 Než budeme moci převést list do formátu SVG, musíme určit možnosti obrázku. The`ImageOrPrintOptions` třída umožňuje řídit, jak bude list převeden. Konkrétně musíme nastavit`SaveFormat` na`SVG` a zajistit, aby byl každý list převeden na jednu stránku.

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.SaveFormat = SaveFormat.Svg;
imgOptions.OnePagePerSheet = true;
```

 The`SaveFormat.Svg` volba zajišťuje, že výstupní formát bude SVG, zatímco`OnePagePerSheet` zajišťuje, že každý list bude vykreslen na jedné stránce.

## Krok 4: Iterujte každý list v sešitu

Nyní musíme projít všechny listy v souboru aplikace Excel. Každý pracovní list bude převeden samostatně.

```csharp
foreach (Worksheet sheet in book.Worksheets)
{
    // Každý pracovní list zpracujeme jeden po druhém
}
```

Tato smyčka zajišťuje, že bez ohledu na to, kolik listů je ve vašem sešitu, bude zpracován každý.

##  Krok 5: Vytvořte a`SheetRender` Object for Rendering

 Pro každý pracovní list vytvoříme a`SheetRender` objekt. Tento objekt je zodpovědný za převod listu do požadovaného formátu obrázku, kterým je v tomto případě SVG.

```csharp
SheetRender sr = new SheetRender(sheet, imgOptions);
```

 The`SheetRender` objekt má dva argumenty: list, který převádíte, a možnosti obrázku, které jste definovali dříve.

## Krok 6: Převeďte pracovní list na SVG

 Nakonec v rámci cyklu převedeme každý list do formátu SVG. K iteraci stránek používáme vnořenou smyčku (i když v tomto případě existuje pouze jedna stránka na list, díky`OnePagePerSheet` volba).

```csharp
for (int i = 0; i < sr.PageCount; i++)
{
    // Výstup listu do formátu obrázku Svg
    sr.ToImage(i, filePath + sheet.Name + i + ".out.svg");
}
```

Tento kód uloží list jako soubor SVG do stejného adresáře jako soubor Excel. Každý soubor SVG bude pojmenován podle názvu listu a čísla indexu, aby se předešlo konfliktům v pojmenování.

## Závěr

A je to! Úspěšně jste převedli pracovní list aplikace Excel do formátu SVG pomocí Aspose.Cells for .NET. Tento proces vám umožňuje zachovat rozvržení a design vašeho listu a zároveň jej zpřístupnit v jakémkoli prohlížeči nebo zařízení, které podporuje SVG, což jsou téměř všechny. Ať už pracujete se složitými soubory Excelu nebo jen s jednoduchou tabulkou, tato metoda zajistí, že vaše data budou krásně vykreslena ve formátu vhodném pro web.

## FAQ

### Co je SVG a proč bych ho měl používat?
SVG (Scalable Vector Graphics) je webový formát, který dokáže nekonečně škálovat bez ztráty kvality. Je ideální pro grafy, diagramy a obrázky, které je třeba zobrazit v různých velikostech.

### Dokáže Aspose.Cells zpracovat velké soubory Excelu pro převod?
Ano, Aspose.Cells dokáže efektivně zpracovat velké soubory Excelu a převést je do SVG bez výrazných problémů s výkonem.

### Existuje nějaký limit na počet listů, které mohu převést do SVG?
Ne, v Aspose.Cells neexistuje žádný vlastní limit pro převod více listů. Jediným omezením by byla paměť a výkon vašeho systému.

### Potřebuji licenci k používání Aspose.Cells?
 Ano, Aspose.Cells vyžaduje licenci pro produkční použití. Můžete získat dočasnou licenci[zde](https://purchase.aspose.com/temporary-license/) nebo prozkoumat[zkušební verze zdarma](https://releases.aspose.com/).

### Mohu přizpůsobit výstup SVG?
 Ano, můžete to vyladit`ImageOrPrintOptions` k přizpůsobení různých aspektů výstupu SVG, jako je rozlišení a škálování.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
