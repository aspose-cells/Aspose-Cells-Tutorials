---
"description": "Naučte se, jak nastavit záhlaví a zápatí v listech aplikace Excel pomocí Aspose.Cells pro .NET s podrobným návodem, praktickými příklady a užitečnými tipy."
"linktitle": "Implementace záhlaví a zápatí v pracovním listu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Implementace záhlaví a zápatí v pracovním listu"
"url": "/cs/net/worksheet-page-setup-features/implement-header-and-footer/"
"weight": 22
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Implementace záhlaví a zápatí v pracovním listu

## Zavedení

Při práci s tabulkami aplikace Excel hrají záhlaví a zápatí klíčovou roli v poskytování důležitých kontextových informací, jako jsou názvy souborů, data nebo čísla stránek, vašemu publiku. Ať už automatizujete sestavy nebo generujete dynamické soubory, Aspose.Cells pro .NET usnadňuje programově upravovat záhlaví a zápatí v listech. Tato příručka se ponořuje do komplexního, podrobného postupu přidávání záhlaví a zápatí pomocí Aspose.Cells pro .NET, což dodá vašim souborům aplikace Excel extra eleganci a profesionalitu.

## Předpoklady

Než začnete, ujistěte se, že máte připraveno následující:

1. Aspose.Cells pro .NET: Budete potřebovat nainstalovaný Aspose.Cells pro .NET. [Stáhněte si to zde](https://releases.aspose.com/cells/net/).
2. Nastavení IDE: Visual Studio (nebo vámi preferované IDE) s nainstalovaným .NET frameworkem.
3. Licence: I když můžete začít s bezplatnou zkušební verzí, získání plné nebo dočasné licence odemkne plný potenciál Aspose.Cells. [Získejte dočasnou licenci](https://purchase.aspose.com/temporary-license/).

Dokumentace k Aspose.Cells je užitečným zdrojem informací v průběhu celého procesu. Najdete ji [zde](https://reference.aspose.com/cells/net/).

## Import balíčků

Do projektu importujte požadované jmenné prostory:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Importem tohoto balíčku získáte přístup ke třídám a metodám potřebným pro práci se záhlavími, zápatími a dalšími funkcemi Excelu v rámci Aspose.Cells.

V této příručce si jednotlivé kroky rozebereme, abyste je mohli snadno sledovat, i když s Aspose.Cells nebo .NET teprve začínáte.

## Krok 1: Nastavení sešitu a stránky

Nejdříve to nejdůležitější: vytvořte nový sešit a přejděte k nastavení stránky listu. Tím získáte nástroje potřebné k úpravě záhlaví a zápatí listu.

```csharp
// Definujte cestu k uložení dokumentu
string dataDir = "Your Document Directory";

// Vytvoření instance objektu Workbook
Workbook excel = new Workbook();
```

Zde jsme vytvořili `Workbook` objekt, který představuje náš soubor Excel. `PageSetup` na listu můžeme upravit možnosti záhlaví a zápatí.


## Krok 2: Přístup k vlastnostem listu a nastavení stránky

V Aspose.Cells má každý pracovní list `PageSetup` vlastnost, která řídí funkce rozvržení, včetně záhlaví a zápatí. Pojďme se podívat na `PageSetup` objekt pro náš pracovní list.

```csharp
// Získání odkazu na PageSetup prvního listu
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

S tímto, `pageSetup` nyní obsahuje všechna nastavení potřebná k přizpůsobení záhlaví a zápatí.


## Krok 3: Nastavení levé části záhlaví

Záhlaví v Excelu jsou rozdělena do tří částí: levá, středová a pravá. Začněme nastavením levé části pro zobrazení názvu listu.

```csharp
// Nastavení názvu listu v levé části záhlaví
pageSetup.SetHeader(0, "&A");
```

Používání `&A` umožňuje dynamicky zobrazit název listu. To je obzvláště užitečné, pokud máte v sešitu více listů a chcete, aby každé záhlaví odráželo název daného listu.


## Krok 4: Přidejte datum a čas do středu záhlaví

Dále přidáme aktuální datum a čas do střední části záhlaví. Navíc použijeme vlastní písmo pro styling.

```csharp
// Nastavit datum a čas do střední části záhlaví tučným písmem
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

V tomto kódu:
- `&D` vloží aktuální datum.
- `&T` vloží aktuální čas.
- `"Times New Roman,Bold"` Na tyto prvky se použije tučné písmo Times New Roman.


## Krok 5: Zobrazení názvu souboru v pravé části záhlaví

Pro dokončení záhlaví zobrazme na pravé straně název souboru spolu s úpravou písma.

```csharp
// Zobrazit název souboru v pravé části záhlaví s vlastní velikostí písma
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

- `&F` představuje název souboru, který jasně ukazuje, do kterého souboru patří vytištěné stránky.
- `&12` změní velikost písma pro tuto sekci na 12.


## Krok 6: Přidání textu s vlastním písmem do sekce levé patičky

Přejdeme k zápatím! Začneme nastavením levé části zápatí s vlastním textem a zadaným stylem písma.

```csharp
// Přidat vlastní text se stylem písma do levé části zápatí
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

Ten/Ta/To `&\"Courier New\"&14` nastavení ve výše uvedeném kódu použije na zadaný text písmo „Courier New“ o velikosti 14 (`123`). Zbytek textu zůstává ve výchozím písmu zápatí.


## Krok 7: Vložte číslo stránky do středu zápatí

Zahrnutí čísel stránek do zápatí je skvělý způsob, jak čtenářům pomoci sledovat vícestránkové dokumenty.

```csharp
// Vložit číslo stránky do střední části zápatí
pageSetup.SetFooter(1, "&P");
```

Zde, `&P` přidá aktuální číslo stránky do střední části zápatí. Je to malý detail, ale zásadní pro profesionálně vypadající dokumenty.


## Krok 8: Zobrazení celkového počtu stránek v pravé části zápatí

Nakonec doplňme zápatí zobrazením celkového počtu stránek v pravé části.

```csharp
// Zobrazit celkový počet stránek v pravé části zápatí
pageSetup.SetFooter(2, "&N");
```

- `&N` poskytuje celkový počet stránek a informuje čtenáře o délce dokumentu.


## Krok 9: Uložení sešitu

Jakmile nastavíte záhlaví a zápatí, je čas sešit uložit. Toto je poslední krok k vygenerování souboru aplikace Excel s plně přizpůsobenými záhlavími a zápatími.

```csharp
// Uložit sešit
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

Tento řádek uloží soubor do vámi určeného adresáře s vlastními záhlavími a zápatími.


## Závěr

Přidávání záhlaví a zápatí do listů aplikace Excel je cenná dovednost pro vytváření organizovaných a profesionálních dokumentů. S Aspose.Cells pro .NET máte úplnou kontrolu nad záhlavími a zápatími souborů aplikace Excel, od zobrazení názvu listu až po vkládání vlastního textu, data, času a dokonce i dynamických čísel stránek. Nyní, když jste viděli každý krok v akci, můžete posunout automatizaci Excelu na další úroveň.

## Často kladené otázky

### Mohu použít různá písma pro různé části záhlaví a zápatí?  
Ano, Aspose.Cells pro .NET umožňuje specifikovat písma pro každou sekci záhlaví a zápatí pomocí specifických značek písma.

### Jak odstraním záhlaví a zápatí?  
Záhlaví a zápatí můžete vymazat nastavením textu záhlaví nebo zápatí na prázdný řetězec pomocí `SetHeader` nebo `SetFooter`.

### Mohu vkládat obrázky do záhlaví nebo zápatí pomocí Aspose.Cells pro .NET?  
Aspose.Cells v současné době primárně podporuje text v záhlavích a zápatích. Obrázky mohou vyžadovat alternativní řešení, například vložení obrázků do samotného listu.

### Podporuje Aspose.Cells dynamická data v záhlavích a zápatích?  
Ano, můžete použít různé dynamické kódy (například `&D` pro datum nebo `&P` pro číslo stránky) pro přidání dynamického obsahu.

### Jak mohu upravit výšku záhlaví nebo zápatí?  
Aspose.Cells nabízí možnosti v rámci `PageSetup` třída pro úpravu okrajů záhlaví a zápatí, což vám dává kontrolu nad rozestupy.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}