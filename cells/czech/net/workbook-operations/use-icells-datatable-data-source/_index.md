---
title: Použijte ICellsDataTableDataSource pro Workbook Designer
linktitle: Použijte ICellsDataTableDataSource pro Workbook Designer
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se používat ICellsDataTableDataSource s Aspose.Cells for .NET k dynamickému vyplňování tabulek aplikace Excel. Ideální pro automatizaci zákaznických dat v sešitech.
weight: 21
url: /cs/net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Použijte ICellsDataTableDataSource pro Workbook Designer

## Zavedení
 Vytváření pokročilých tabulek s automatizovanou integrací dat může změnit hru, zejména v podnikových aplikacích. V tomto tutoriálu se ponoříme do toho, jak používat`ICellsDataTableDataSource`pro návrháře sešitu v Aspose.Cells pro .NET. Provedeme vás vytvořením jednoduchého, člověku čitelného řešení pro dynamické načítání vlastních dat do souboru aplikace Excel. Pokud tedy pracujete se seznamy zákazníků, prodejními daty nebo čímkoli podobným, tento průvodce je pro vás!
## Předpoklady
Chcete-li začít, ujistěte se, že máte následující:
-  Aspose.Cells for .NET Library – můžete si ji stáhnout z[zde](https://releases.aspose.com/cells/net/) nebo získat bezplatnou zkušební verzi.
- .NET Development Environment – Visual Studio je skvělá volba.
- Základní porozumění C# – Znalost tříd a zpracování dat vám pomůže pokračovat.
Než budeme pokračovat, ujistěte se, že vaše vývojové prostředí obsahuje potřebné balíčky.
## Importujte balíčky
Chcete-li efektivně používat Aspose.Cells, musíte importovat základní balíčky. Níže je rychlý odkaz na požadované jmenné prostory:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Krok 1: Definujte třídu zákaznických dat
 Chcete-li začít, vytvořte jednoduchý`Customer` třída. Tato třída bude obsahovat základní podrobnosti o zákaznících, jako je`FullName` a`Address`Berte to jako způsob, jak definovat „tvar“ vašich dat.
```csharp
public class Customer
{
    public Customer(string aFullName, string anAddress)
    {
        FullName = aFullName;
        Address = anAddress;
    }
    public string FullName { get; set; }
    public string Address { get; set; }
}
```
## Krok 2: Nastavte třídu seznamu zákazníků
 Dále definujte a`CustomerList` třída, která se rozšiřuje`ArrayList` . Tento přizpůsobený seznam bude obsahovat instance`Customer` a umožnit indexovaný přístup ke každému záznamu.
```csharp
public class CustomerList : ArrayList
{
    public new Customer this[int index]
    {
        get { return (Customer)base[index]; }
        set { base[index] = value; }
    }
}
```
V tomto kroku zabalujeme naše data do formátu, který Aspose.Cells dokáže rozpoznat a zpracovat.
## Krok 3: Vytvořte třídu zdroje dat zákazníka
 Tady jsou věci zajímavé. Vytvoříme a`CustomerDataSource` třída provádění`ICellsDataTable` aby byla naše data kompatibilní s návrhářem sešitů Aspose.Cells.
```csharp
public class CustomerDataSource : ICellsDataTable
{
    internal string[] m_Columns;
    internal ICollection m_DataSource;
    private Hashtable m_PropHash;
    private IEnumerator m_IEnumerator;
    private PropertyInfo[] m_Properties;
    public CustomerDataSource(CustomerList customers)
    {
        this.m_DataSource = customers;
        this.m_Properties = customers[0].GetType().GetProperties();
        this.m_Columns = new string[this.m_Properties.Length];
        this.m_PropHash = new Hashtable(this.m_Properties.Length);
        for (int i = 0; i < m_Properties.Length; i++)
        {
            this.m_Columns[i] = m_Properties[i].Name;
            this.m_PropHash.Add(m_Properties[i].Name, m_Properties[i]);
        }
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public string[] Columns => this.m_Columns;
    public int Count => this.m_DataSource.Count;
    public void BeforeFirst()
    {
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public object this[int index] => this.m_Properties[index].GetValue(this.m_IEnumerator.Current, null);
    public object this[string columnName] => ((PropertyInfo)this.m_PropHash[columnName]).GetValue(this.m_IEnumerator.Current, null);
    public bool Next()
    {
        if (this.m_IEnumerator == null)
            return false;
        return this.m_IEnumerator.MoveNext();
    }
}
```
 Tento zvyk`CustomerDataSource` třída umožňuje Aspose.Cells interpretovat každý z nich`Customer` objekt jako řádek v souboru aplikace Excel.
## Krok 4: Inicializujte zákaznická data
Nyní do našeho seznamu přidejte několik zákazníků. Zde načteme data, která mají být zapsána do sešitu. Podle potřeby můžete přidat další položky.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
tomto příkladu pracujeme s malou datovou sadou. Tento seznam však můžete snadno rozšířit načtením dat z databáze nebo jiných zdrojů.
## Krok 5: Načtěte sešit
Nyní otevřeme existující excelový sešit, který obsahuje potřebné inteligentní značky. Tento sešit bude sloužit jako naše šablona a Aspose.Cells dynamicky nahradí inteligentní značky daty zákazníků.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
 Zajistěte to`"SmartMarker1.xlsx"` obsahuje zástupné symboly jako`&=Customer.FullName` a`&=Customer.Address` kde se mají údaje vyplnit.
## Krok 6: Nastavte Návrhář sešitu
Nyní nakonfigurujeme návrháře sešitu tak, aby propojil náš zdroj dat zákazníků s inteligentními značkami sešitu.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
 The`SetDataSource` metoda váže naše`CustomerDataSource` k inteligentním značkám v sešitu. Každá značka označena`&=Customer` v Excelu budou nyní nahrazeny odpovídajícími zákaznickými údaji.
## Krok 7: Zpracujte a uložte sešit
Nakonec zpracujeme sešit k vyplnění údajů a uložení výsledků.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Tento kód spustí zpracování Smart Marker, nahradí všechny zástupné symboly daty a uloží výsledek jako`dest.xlsx`.
## Závěr
 Gratuluji! Úspěšně jste implementovali`ICellsDataTableDataSource` pro návrháře sešitů pomocí Aspose.Cells pro .NET. Tento přístup je ideální pro automatizaci populace dat v tabulkových procesorech, zejména při práci s dynamickými daty, jako jsou seznamy zákazníků nebo inventáře produktů. S těmito dovednostmi jste na dobré cestě k vytváření aplikací založených na datech, díky nimž bude reporting v Excelu hračkou!
## FAQ
###  co je`ICellsDataTable` in Aspose.Cells?  
Je to rozhraní umožňující propojení vlastních zdrojů dat s Aspose.Cells Smart Markers pro dynamickou populaci dat.
### Jak mohu přizpůsobit data v šabloně sešitu?  
 Zástupné symboly zvané Smart Markers, jako např`&=Customer.FullName`, se používají. Tyto značky jsou během zpracování nahrazeny skutečnými daty.
### Je Aspose.Cells for .NET zdarma?  
 Aspose.Cells nabízí bezplatnou zkušební verzi, ale úplný přístup vyžaduje placenou licenci. Zkontrolujte jejich[zkušební verze zdarma](https://releases.aspose.com/) nebo[nakoupit](https://purchase.aspose.com/buy) možnosti.
### Mohu dynamicky přidávat další zákaznická data?  
 Absolutně! Jednoduše naplňte`CustomerList` dalšími položkami před spuštěním programu.
### Kde mohu získat pomoc, když uvíznu?  
 Aspose má a[fórum podpory](https://forum.aspose.com/c/cells/9) kde mohou uživatelé klást otázky a získat pomoc od komunity a týmu Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
