---
title: Používejte anonymní typy s inteligentními značkami Aspose.Cells
linktitle: Používejte anonymní typy s inteligentními značkami Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se používat anonymní typy s inteligentními značkami v Aspose.Cells pro dynamické generování sestav Excel v .NET. Postupujte podle našeho snadného průvodce.
weight: 17
url: /cs/net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Používejte anonymní typy s inteligentními značkami Aspose.Cells

## Zavedení
Pokud jde o generování dynamických sestav aplikace Excel v aplikacích .NET, Aspose.Cells vyniká jako výkonný nástroj. Jednou z jeho nejlepších vlastností je schopnost pracovat s inteligentními značkami a anonymními typy. Pokud s tímto konceptem začínáte, nebojte se! Tato příručka rozebere vše, co potřebujete vědět, od nezbytných předpokladů až po praktické příklady, a to vše při zachování poutavé a snadné kontroly.
## Předpoklady
Než se ponoříme do kódu, ujistěte se, že máte vše, co potřebujete k hladkému spuštění příkladů v tomto tutoriálu.
### 1. Prostředí .NET
Ujistěte se, že máte na svém lokálním počítači nastaveno fungující prostředí .NET. Můžete použít Visual Studio nebo jakékoli jiné IDE dle vašeho výběru.
### 2. Aspose.Cells Library
 Budete potřebovat knihovnu Aspose.Cells. Pokud jste si ji ještě nestáhli, můžete ji snadno najít[zde](https://releases.aspose.com/cells/net/) . Můžete to také vyzkoušet pomocí bezplatné zkušební verze, která je k dispozici na adrese[tento odkaz](https://releases.aspose.com/).
### 3. Základní znalost C#
Základní znalost programování v C# vám pomůže snadněji procházet výukovým programem. Pokud jsou vám pojmy jako třídy, objekty a vlastnosti známé, můžete začít!
## Importujte balíčky
Chcete-li ve svém projektu použít knihovnu Aspose.Cells, musíte importovat související jmenné prostory. Přidejte následující pomocí direktiv v horní části souboru C#:
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
Tyto jmenné prostory vám umožní přístup ke všem nezbytným třídám a metodám, o kterých bude řeč později.
Nyní se pustíme do jádra tutoriálu! Uvidíte, jak vytvořit soubor aplikace Excel s inteligentními značkami pomocí vlastní třídy. Nebojte se; vše rozdělíme do zvládnutelných kroků!
## Krok 1: Vytvořte vlastní třídu
Nejprve potřebujeme jednoduchou třídu, která bude reprezentovat data, která chceme přidat do našeho souboru Excel. Tato třída bude obsahovat informace o osobě.
```csharp
public class Person
{
    private string m_Name;
    private int m_Age;
    public string Name
    {
        get { return m_Name; }
        set { m_Name = value; }
    }
    public int Age
    {
        get { return m_Age; }
        set { m_Age = value; }
    }
    internal Person(string name, int age)
    {
        this.m_Name = name;
        this.m_Age = age;
    }
}
```
 Zde definujeme třídu s názvem`Person` se dvěma vlastnostmi,`Name` a`Age`. Konstruktor tyto vlastnosti inicializuje. 
## Krok 2: Nastavte Návrhář sešitu
 Dále vytvoříme instanci`WorkbookDesigner`třídy, kterou použijeme k návrhu našeho souboru Excel s chytrými značkami.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvořte instanci objektu návrháře sešitu.
WorkbookDesigner report = new WorkbookDesigner();
```
 Nahradit`"Your Document Directory"` s vaší skutečnou cestou k souboru, kam chcete soubor Excel uložit. The`WorkbookDesigner` class je srdcem této operace, kde definujete svou šablonu.
## Krok 3: Přidejte značky do buněk
Nyní musíme do listu přidat chytré značky. Tyto značky budou zástupnými symboly pro data, která zadáme později.
```csharp
// Získejte první pracovní list v sešitu.
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
// Vložte do buněk nějaké značky.
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
 Označíme první list a nastavíme hodnoty pro buňky záhlaví. Inteligentní značky mají předponu`&=` což Aspose říká, že se jedná o zástupné symboly pro data, která mají být vložena později.
## Krok 4: Vytvořte seznam lidí
 Nyní vytvoříme seznam lidí, kteří používají naše`Person` třídy, kterou použijeme k naplnění inteligentních značek.
```csharp
// Vytvořte instanci kolekce seznamů na základě vlastní třídy.
IList<Person> list = new List<Person>();
// Zadejte hodnoty pro značky pomocí objektu vlastní třídy.
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
 Vytvoříme seznam a přidáme instance`Person` tomu. Tento seznam slouží jako zdroj dat při naplňování šablony Excel.
## Krok 5: Nastavte zdroje dat a značky procesů
 Poté, co máme náš seznam hotový, musíme jej nastavit jako zdroj dat pro náš`WorkbookDesigner` instance a poté zpracujte značky.
```csharp
// Nastavte zdroj dat.
report.SetDataSource("MyProduct", list);
// Zpracujte značky.
report.Process(false);
```
 The`SetDataSource` metoda spojuje náš dříve definovaný seznam se značkami. The`Process` metoda nahradí inteligentní značky v sešitu skutečnými hodnotami z našich objektů.
## Krok 6: Uložte soubor Excel
Nakonec upravený sešit uložíme do námi určeného adresáře.
```csharp
// Uložte soubor aplikace Excel.
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
Tento řádek uloží sešit do zadané cesty k souboru. Tento soubor můžete otevřít pomocí Excelu a zobrazit vložená data.
## Závěr
A tady to máte! Úspěšně jste vytvořili soubor aplikace Excel pomocí inteligentních značek v Aspose.Cells s vaší vlastní třídou. Tato metoda nejen činí vaši správu dat dynamičtější, ale také udržuje váš kód čistý a organizovaný.
Ať už tedy generujete sestavy pro analýzu, sledování informací nebo jakýkoli jiný úkol související s daty, chytré značky jsou vaším spojencem při vytváření přehledů Excelu, které jsou lépe spravovatelné a flexibilní!
## FAQ
### Co jsou chytré značky v Aspose.Cells?
Inteligentní značky jsou speciální zástupné symboly v dokumentu aplikace Excel, které vám umožňují dynamicky vkládat data za běhu.
### Mohu pro chytré značky používat anonymní typy?
Ano! Inteligentní značky lze použít s jakýmkoli typem objektu, včetně anonymních typů, pokud odpovídají očekávané datové struktuře.
### Je Aspose.Cells zdarma k použití?
Aspose.Cells je placený produkt, ale můžete začít s bezplatnou zkušební verzí a prozkoumat jeho funkce.
### Jaké formáty souborů Aspose.Cells podporuje?
Podporuje širokou škálu formátů souborů, včetně XLS, XLSX, CSV a dalších.
### Kde najdu více informací o Aspose.Cells?
 Pro více podrobností se podívejte na[dokumentace](https://reference.aspose.com/cells/net/) nebo navštivte[fórum podpory](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
