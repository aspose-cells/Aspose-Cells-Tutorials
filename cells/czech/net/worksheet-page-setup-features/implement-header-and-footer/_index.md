---
title: Implementujte záhlaví a zápatí v listu
linktitle: Implementujte záhlaví a zápatí v listu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak nastavit záhlaví a zápatí v excelových listech pomocí Aspose.Cells for .NET, pomocí podrobného návodu, praktických příkladů a užitečných tipů.
weight: 22
url: /cs/net/worksheet-page-setup-features/implement-header-and-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Implementujte záhlaví a zápatí v listu

## Zavedení

Při práci s tabulkami aplikace Excel hrají záhlaví a zápatí klíčovou roli při poskytování důležitých kontextových informací, jako jsou názvy souborů, data nebo čísla stránek, vašemu publiku. Ať už automatizujete sestavy nebo generujete dynamické soubory, Aspose.Cells for .NET usnadňuje programové přizpůsobení záhlaví a zápatí v listech. Tato příručka se ponoří do komplexního přístupu krok za krokem k přidávání záhlaví a zápatí pomocí Aspose.Cells pro .NET, což dává vašim souborům Excel extra lesk a profesionalitu.

## Předpoklady

Než začnete, ujistěte se, že máte na svém místě následující:

1.  Aspose.Cells for .NET: Budete potřebovat nainstalovaný Aspose.Cells for .NET.[Stáhněte si jej zde](https://releases.aspose.com/cells/net/).
2. Nastavení IDE: Visual Studio (nebo vaše preferované IDE) s nainstalovaným rozhraním .NET.
3.  Licence: I když můžete začít s bezplatnou zkušební verzí, získání plné nebo dočasné licence odemkne plný potenciál Aspose.Cells.[Získejte dočasnou licenci](https://purchase.aspose.com/temporary-license/).

Dokumentace pro Aspose.Cells je užitečným zdrojem pro reference během tohoto procesu. Můžete to najít[zde](https://reference.aspose.com/cells/net/).

## Import balíčků

Do svého projektu importujte požadované jmenné prostory:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Importováním tohoto balíčku získáte přístup ke třídám a metodám potřebným pro práci se záhlavími, zápatími a dalšími funkcemi aplikace Excel v rámci Aspose.Cells.

V této příručce rozebereme každý krok, abyste je mohli snadno sledovat, i když jste v Aspose.Cells nebo .NET nováčkem.

## Krok 1: Nastavte svůj sešit a nastavení stránky

Nejprve: vytvořte nový sešit a otevřete nastavení stránky listu. Získáte tak nástroje, které potřebujete k úpravě záhlaví a zápatí listu.

```csharp
// Definujte cestu k uložení dokumentu
string dataDir = "Your Document Directory";

// Vytvořte instanci objektu sešitu
Workbook excel = new Workbook();
```

 Zde jsme vytvořili a`Workbook` objekt, který představuje náš soubor Excel. The`PageSetup` listu je místo, kde můžeme upravit možnosti záhlaví a zápatí.


## Krok 2: Otevřete vlastnosti listu a PageSetup

 V Aspose.Cells má každý list a`PageSetup`vlastnost, která řídí funkce rozvržení, včetně záhlaví a zápatí. Pojďme si`PageSetup` objekt pro náš pracovní list.

```csharp
// Získejte odkaz na PageSetup prvního listu
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

 s tímto`pageSetup` nyní obsahuje všechna nastavení potřebná k přizpůsobení záhlaví a zápatí.


## Krok 3: Nastavte levou část záhlaví

Záhlaví v Excelu jsou rozdělena do tří částí: levá, středová a pravá. Začněme nastavením levé části pro zobrazení názvu listu.

```csharp
// V levé části záhlaví nastavte název listu
pageSetup.SetHeader(0, "&A");
```

 Použití`&A` umožňuje dynamicky zobrazit název listu. To je zvláště užitečné, pokud máte v sešitu více listů a chcete, aby každé záhlaví odráželo jeho název listu.


## Krok 4: Přidejte datum a čas do středu záhlaví

Dále přidáme aktuální datum a čas do střední části záhlaví. Navíc pro styling použijeme vlastní písmo.

```csharp
// Nastavte datum a čas ve střední části záhlaví s tučným písmem
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

V tomto kódu:
- `&D`vloží aktuální datum.
- `&T` vloží aktuální čas.
- `"Times New Roman,Bold"` použije Times New Roman tučně na tyto prvky.


## Krok 5: Zobrazte název souboru v pravé části záhlaví

Pro dokončení záhlaví ukážeme název souboru na pravé straně spolu s úpravou písma.

```csharp
// Zobrazovat název souboru v pravé části záhlaví s vlastní velikostí písma
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

- `&F` představuje název souboru, takže je jasné, ke kterému souboru tištěné stránky patří.
- `&12` změní velikost písma pro tuto sekci na 12.


## Krok 6: Přidejte text s vlastním písmem do sekce levé zápatí

Přechod na zápatí! Začneme nastavením levé zápatí s vlastním textem a určeným stylem písma.

```csharp
// Přidejte vlastní text se stylem písma do levé části zápatí
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

 The`&\"Courier New\"&14` nastavení ve výše uvedeném kódu aplikuje na zadaný text písmo „Courier New“ o velikosti 14 (`123`). Zbytek textu zůstane ve výchozím písmu zápatí.


## Krok 7: Vložte číslo stránky do středu zápatí

Zahrnutí čísel stránek do zápatí je skvělý způsob, jak čtenářům pomoci udržet si přehled o vícestránkových dokumentech.

```csharp
// Vložte číslo stránky do střední části zápatí
pageSetup.SetFooter(1, "&P");
```

 Zde,`&P` přidá číslo aktuální stránky do středové části zápatí. Je to malý detail, ale zásadní pro profesionálně vypadající dokumenty.


## Krok 8: Zobrazit celkový počet stránek v pravé zápatí

Nakonec doplňte zápatí zobrazením celkového počtu stránek v pravé části.

```csharp
// Zobrazit celkový počet stránek v pravé části zápatí
pageSetup.SetFooter(2, "&N");
```

- `&N` poskytuje celkový počet stránek a dává čtenářům vědět, jak je dokument dlouhý.


## Krok 9: Uložte sešit

Jakmile nastavíte záhlaví a zápatí, je čas sešit uložit. Toto je poslední krok k vytvoření souboru aplikace Excel s plně přizpůsobenými záhlavími a zápatími.

```csharp
// Uložte sešit
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

Tento řádek uloží soubor do určeného adresáře s vlastním záhlavím a zápatím.


## Závěr

Přidávání záhlaví a zápatí do listů aplikace Excel je cennou dovedností pro vytváření organizovaných profesionálních dokumentů. S Aspose.Cells for .NET máte úplnou kontrolu nad záhlavím a zápatím souborů Excel, od zobrazení názvu listu po vkládání vlastního textu, data, času a dokonce i dynamických čísel stránek. Nyní, když jste viděli každý krok v akci, můžete posunout automatizaci Excelu na další úroveň.

## FAQ

### Mohu použít různá písma pro různé části záhlaví a zápatí?  
Ano, Aspose.Cells for .NET vám umožňuje určit písma pro každou část záhlaví a zápatí pomocí specifických značek písem.

### Jak odstraním záhlaví a zápatí?  
 Záhlaví a zápatí můžete vymazat nastavením textu záhlaví nebo zápatí na prázdný řetězec pomocí`SetHeader` nebo`SetFooter`.

### Mohu vkládat obrázky do záhlaví nebo zápatí pomocí Aspose.Cells pro .NET?  
V současné době Aspose.Cells podporuje především text v záhlaví a zápatí. Obrázky mohou vyžadovat řešení, jako je vkládání obrázků do samotného listu.

### Podporuje Aspose.Cells dynamická data v záhlaví a zápatí?  
 Ano, můžete použít různé dynamické kódy (např`&D` na datum popř`&P` pro číslo stránky) pro přidání dynamického obsahu.

### Jak mohu upravit výšku záhlaví nebo zápatí?  
 Aspose.Cells poskytuje možnosti v rámci`PageSetup` třídy pro úpravu okrajů záhlaví a zápatí, což vám dává kontrolu nad mezerami.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
