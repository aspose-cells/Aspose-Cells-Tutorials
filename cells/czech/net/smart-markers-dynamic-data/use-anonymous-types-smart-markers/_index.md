---
"description": "Naučte se, jak používat anonymní typy s inteligentními značkami v Aspose.Cells pro dynamické generování sestav v Excelu v .NET. Postupujte podle našeho jednoduchého návodu."
"linktitle": "Použití anonymních typů s inteligentními značkami Aspose.Cells"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Použití anonymních typů s inteligentními značkami Aspose.Cells"
"url": "/cs/net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Použití anonymních typů s inteligentními značkami Aspose.Cells

## Zavedení
Pokud jde o generování dynamických excelových sestav v aplikacích .NET, Aspose.Cells vyniká jako výkonný nástroj. Jednou z jeho nejlepších funkcí je schopnost pracovat s inteligentními značkami a anonymními typy. Pokud s tímto konceptem teprve začínáte, nebojte se! Tato příručka vám rozebere vše, co potřebujete vědět, od předpokladů až po praktické příklady, a to vše při zachování poutavosti a snadného srozumitelnosti.
## Předpoklady
Než se pustíme do kódu, ujistěme se, že máte vše potřebné pro hladké spuštění příkladů v tomto tutoriálu.
### 1. Prostředí .NET
Ujistěte se, že máte na svém lokálním počítači nastavené funkční prostředí .NET. Můžete použít Visual Studio nebo jakékoli jiné IDE dle vlastního výběru.
### 2. Knihovna Aspose.Cells
Budete potřebovat knihovnu Aspose.Cells. Pokud jste si ji ještě nestáhli, snadno ji najdete. [zde](https://releases.aspose.com/cells/net/)Můžete si to také vyzkoušet s bezplatnou zkušební verzí dostupnou na [tento odkaz](https://releases.aspose.com/).
### 3. Základní znalost jazyka C#
Základní znalost programování v C# vám pomůže snáze se v tomto tutoriálu orientovat. Pokud jsou vám pojmy jako třídy, objekty a vlastnosti známé, můžete začít!
## Importovat balíčky
Chcete-li ve svém projektu použít knihovnu Aspose.Cells, musíte importovat související jmenné prostory. Na začátek souboru C# přidejte následující direktivy using:
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
Tyto jmenné prostory vám poskytnou přístup ke všem potřebným třídám a metodám, které budou probrány později.
A teď se pojďme pustit do jádra tutoriálu! Uvidíte, jak vytvořit soubor Excelu s inteligentními značkami pomocí vlastní třídy. Nebojte se, vše si rozdělíme na zvládnutelné kroky!
## Krok 1: Vytvořte vlastní třídu
Nejprve potřebujeme jednoduchou třídu pro reprezentaci dat, která chceme přidat do našeho excelového souboru. Tato třída bude obsahovat informace o osobě.
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
Zde definujeme třídu s názvem `Person` se dvěma nemovitostmi, `Name` a `Age`Konstruktor inicializuje tyto vlastnosti. 
## Krok 2: Nastavení návrháře sešitů
Dále si vytvořme instanci `WorkbookDesigner` třída, kterou použijeme k návrhu našeho souboru Excel s inteligentními značkami.
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
// Vytvořte instanci objektu návrháře sešitu.
WorkbookDesigner report = new WorkbookDesigner();
```
Nahradit `"Your Document Directory"` s vaší skutečnou cestou k souboru, kam chcete soubor Excel uložit. `WorkbookDesigner` Třída je srdcem této operace, kde definujete svou šablonu.
## Krok 3: Přidání značek do buněk
Nyní musíme do listu přidat inteligentní značky. Tyto značky budou zástupnými symboly pro data, která budeme později zadávat.
```csharp
// Získejte první list v sešitu.
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
// Vložte do buněk nějaké značky.
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
Označíme první list a nastavíme hodnoty pro buňky záhlaví. Inteligentní značky mají předponu `&=` což říká Aspose, že se jedná o zástupné symboly pro data, která mají být vložena později.
## Krok 4: Vytvořte seznam lidí
Nyní si vytvořme seznam lidí, kteří používají náš `Person` třída, kterou použijeme k naplnění inteligentních značek.
```csharp
// Vytvořte instanci kolekce seznamů na základě vlastní třídy.
IList<Person> list = new List<Person>();
// Zadejte hodnoty pro značky pomocí objektu vlastní třídy.
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
Vytvoříme seznam a přidáme instance `Person` k tomu. Tento seznam slouží jako zdroj dat při vyplňování šablony aplikace Excel.
## Krok 5: Nastavení zdroje dat a značek procesu
Jakmile máme seznam připravený, musíme ho nastavit jako zdroj dat pro naše `WorkbookDesigner` instanci a poté zpracovat značky.
```csharp
// Nastavte zdroj dat.
report.SetDataSource("MyProduct", list);
// Zpracujte značky.
report.Process(false);
```
Ten/Ta/To `SetDataSource` Metoda propojuje náš dříve definovaný seznam se značkami. `Process` Metoda nahrazuje inteligentní značky v sešitu skutečnými hodnotami z našich objektů.
## Krok 6: Uložte soubor Excel
Nakonec upravený sešit uložíme do námi určeného adresáře.
```csharp
// Uložte soubor Excelu.
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
Tento řádek uloží sešit do zadané cesty k souboru. Tento soubor můžete otevřít v Excelu a zobrazit vložená data.
## Závěr
tady to máte! Úspěšně jste vytvořili soubor Excelu pomocí inteligentních značek v Aspose.Cells s vlastní třídou. Tato metoda nejenže zdynamizuje správu dat, ale také udržuje váš kód čistý a organizovaný.
Ať už tedy generujete reporty pro analytické účely, sledujete informace nebo provádíte jakýkoli jiný úkol související s daty, inteligentní značky jsou vaším spojencem, který vám pomůže s přehlednějšími a flexibilnějšími reporty v Excelu!
## Často kladené otázky
### Co jsou chytré markery v Aspose.Cells?
Inteligentní značky jsou speciální zástupné symboly v dokumentu aplikace Excel, které umožňují dynamické vkládání dat za běhu.
### Mohu pro inteligentní značky použít anonymní typy?
Ano! Inteligentní značky lze použít s jakýmkoli typem objektu, včetně anonymních typů, pokud odpovídají očekávané datové struktuře.
### Je Aspose.Cells zdarma k použití?
Aspose.Cells je placený produkt, ale můžete začít s bezplatnou zkušební verzí a prozkoumat jeho funkce.
### Jaké formáty souborů podporuje Aspose.Cells?
Podporuje širokou škálu formátů souborů, včetně XLS, XLSX, CSV a dalších.
### Kde najdu více informací o Aspose.Cells?
Pro více informací se podívejte na [dokumentace](https://reference.aspose.com/cells/net/) nebo navštivte [fórum podpory](https://forum.aspose.com/c/cells/9).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}