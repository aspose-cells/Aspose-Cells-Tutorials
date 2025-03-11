---
title: Nastavit záhlaví a zápatí aplikace Excel
linktitle: Nastavit záhlaví a zápatí aplikace Excel
second_title: Aspose.Cells for .NET API Reference
description: Naučte se, jak snadno nastavit Excel záhlaví a zápatí pomocí Aspose.Cells pro .NET s naším podrobným průvodcem. Ideální pro profesionální dokumenty.
weight: 100
url: /cs/net/excel-page-setup/set-excel-headers-and-footers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavit záhlaví a zápatí aplikace Excel

## Zavedení

Pokud jde o správu tabulkových dokumentů, záhlaví a zápatí hrají zásadní roli při poskytování kontextu. Představte si, že otevřete soubor aplikace Excel a hned nahoře uvidíte název listu, datum a možná i název souboru. Dodá vašemu dokumentu profesionální vzhled a pomůže sdělit důležité detaily na první pohled. Pokud chcete zvýšit profesionalitu svých excelových listů pomocí Aspose.Cells pro .NET, jste na správném místě! V této příručce vás provedeme kroky k snadnému nastavení záhlaví a zápatí v tabulkách Excel. 

## Předpoklady

Než se ponoříme do toho nejnutnějšího, ujistěte se, že máte vše, co potřebujete, abyste mohli začít. Nejprve budete potřebovat:

1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Zde budete psát a spouštět svůj kód C#.
2.  Aspose.Cells for .NET Library: Musíte mít knihovnu Aspose.Cells. Pokud jste tak ještě neučinili, můžete si jej stáhnout z[zde](https://releases.aspose.com/cells/net/).
3. Základní porozumění C#: Znalost programování v C# je zásadní, protože všechny ukázky kódu budou v tomto jazyce.
4. Nastavení projektu: Vytvořte nový projekt C# ve Visual Studiu, kde budeme implementovat naši logiku záhlaví/zápatí Excelu.

Jakmile potvrdíte, že máte výše uvedené předpoklady, je čas si ušpinit ruce!

## Importujte balíčky

Chcete-li začít pracovat s Aspose.Cells, musíte do kódu C# importovat příslušné jmenné prostory.

### Otevřete svůj projekt C#

Otevřete projekt v sadě Visual Studio, kde chcete implementovat nastavení záhlaví a zápatí. Ujistěte se, že máte jasnou strukturu, která pojme váš kód.

### Přidejte odkaz do Aspose.Cells

Po vytvoření nebo otevření projektu musíte přidat odkaz na knihovnu Aspose.Cells. Klikněte pravým tlačítkem na svůj projekt v Průzkumníku řešení, vyberte „Spravovat balíčky NuGet“ a vyhledejte „Aspose.Cells“. Nainstalujte jej do svého projektu.

### Importujte jmenný prostor

V horní části souboru C# přidejte následující řádek pro import jmenného prostoru Aspose.Cells:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Importováním tohoto jmenného prostoru můžete bez jakýchkoli překážek používat funkce poskytované knihovnou Aspose.Cells.

Velký! Nyní, když je vaše prostředí nastaveno a vaše balíčky jsou importovány, pojďme si krok za krokem rozebrat proces nastavení záhlaví a zápatí v Excelu.

## Krok 1: Inicializujte sešit

Nejprve musíme vytvořit instanci objektu Workbook, který představuje náš soubor Excel v paměti.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Workbook excel = new Workbook();
```

 Vysvětlení: Zde nahraďte`YOUR DOCUMENT DIRECTORY` se skutečnou cestou, kam chcete soubor Excel uložit. The`Workbook` objekt je vaším hlavním vstupním bodem pro vytváření a manipulaci se soubory Excel.

## Krok 2: Získejte referenční informace o nastavení PageSetup

 Dále musíme získat přístup k`PageSetup` vlastnost listu, kde chceme nastavit záhlaví a zápatí.

```csharp
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

 Vysvětlení: Přistupujeme k prvnímu listu (index`0` ) našeho sešitu. The`PageSetup` class poskytuje vlastnosti a metody pro přizpůsobení vzhledu stránky při tisku, včetně záhlaví a zápatí.

## Krok 3: Nastavte záhlaví

Nyní začneme s nastavením záhlaví. Začneme levou částí:

```csharp
pageSetup.SetHeader(0, "&A");
```

 Vysvětlení: The`SetHeader` nám umožňuje definovat obsah hlavičky. Zde,`&A` označuje název listu, který se objeví na levé straně záhlaví.

## Krok 4: Přizpůsobte centrální záhlaví

Dále přizpůsobíme centrální záhlaví tak, aby zobrazovalo aktuální datum a čas konkrétním písmem.

```csharp
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

 Vysvětlení: The`&D` a`&T` kódy se automaticky nahradí aktuálním datem a časem, resp. Také určujeme, že písmo pro toto záhlaví by mělo být „Times New Roman“ a tučné.

## Krok 5: Nastavte pravé záhlaví

Nyní nastavíme pravou část záhlaví tak, aby zobrazovala název souboru.

```csharp
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

 Vysvětlení: Zde,`&F` bude nahrazeno názvem souboru. Pro zachování konzistentního vzhledu používáme stejné písmo jako pro centrální záhlaví.

## Krok 6: Nakonfigurujte zápatí

Nyní, když naše záhlaví vypadají elegantně, zaměřme svou pozornost na zápatí. Začneme levým zápatím:

```csharp
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

Vysvětlení: Do levého zápatí vkládáme vlastní zprávu „Ahoj světe!“ spolu s textem`123` v jiném stylu písma — Courier New.

## Krok 7: Konfigurace středového zápatí

Dále nastavíme středové zápatí tak, aby zobrazovalo aktuální číslo stránky:

```csharp
pageSetup.SetFooter(1, "&P");
```

 Vysvětlení: The`&P` kód automaticky vloží číslo stránky do středu zápatí – praktický způsob, jak sledovat stránky.

## Krok 8: Konfigurace pravého zápatí

Chcete-li dokončit nastavení zápatí, nastavte pravé zápatí tak, aby zobrazovalo celkový počet stránek v dokumentu.

```csharp
pageSetup.SetFooter(2, "&N");
```

 Vysvětlení: Zde,`&N` bude nahrazeno celkovým počtem stran. Dodává profesionální nádech, zejména u delších dokumentů.

## Krok 9: Uložte sešit

Když je vše nyní nastaveno, stačí si sešit uložit, abyste viděli plody své práce.

```csharp
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

 Vysvětlení: Vyměnit`"SetHeadersAndFooters_out.xls"` s požadovaným názvem souboru. Uložte sešit a máte hotovo!

## Závěr

tady to máte! Nastavení záhlaví a zápatí v Excelu pomocí Aspose.Cells for .NET je jednoduché, pokud budete postupovat podle těchto kroků. Vylepšili jste nejen vzhled dokumentu, ale také zlepšili jeho funkčnost poskytnutím důležitého kontextu. Ať už připravujete zprávy, sdílíte šablony nebo jen organizujete svá data, záhlaví a zápatí dodají profesionální šmrnc, který je těžké překonat. Vyzkoušejte to a uvidíte, jak snadné je spravovat vaše dokumenty Excel pomocí této výkonné knihovny!

## FAQ

### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET používaná pro vytváření, manipulaci a vykreslování souborů aplikace Excel programově.

### Mohu vyzkoušet Aspose.Cells zdarma?
 Ano! Bezplatnou zkušební verzi si můžete stáhnout z[zde](https://releases.aspose.com/).

### Je Aspose.Cells kompatibilní se staršími formáty Excelu?
Absolutně! Aspose.Cells podporuje staré i nové formáty souborů Excel.

### Kde najdu další dokumentaci?
 Podrobnou dokumentaci si můžete prohlédnout na[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/).

### Jak získám podporu pro Aspose.Cells?
 Pro podporu navštivte[Aspose Support Forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
