---
"description": "Naučte se používat ICellsDataTableDataSource s Aspose.Cells pro .NET k dynamickému naplňování excelových listů. Ideální pro automatizaci zákaznických dat v sešitech."
"linktitle": "Použití ICellsDataTableDataSource pro návrhář sešitů"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Použití ICellsDataTableDataSource pro návrhář sešitů"
"url": "/cs/net/workbook-operations/use-icells-datatable-data-source/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Použití ICellsDataTableDataSource pro návrhář sešitů

## Zavedení
Vytváření pokročilých tabulek s automatizovanou integrací dat může být převratné, zejména v obchodních aplikacích. V tomto tutoriálu se ponoříme do toho, jak je používat. `ICellsDataTableDataSource` pro návrháře sešitů v Aspose.Cells pro .NET. Provedeme vás vytvořením jednoduchého, lidsky čitelného řešení pro dynamické načítání vlastních dat do souboru aplikace Excel. Pokud tedy pracujete se seznamy zákazníků, prodejními daty nebo něčím podobným, je tento průvodce určen právě vám!
## Předpoklady
Chcete-li začít, ujistěte se, že máte následující:
- Knihovna Aspose.Cells pro .NET – Můžete si ji stáhnout z [zde](https://releases.aspose.com/cells/net/) nebo si stáhněte bezplatnou zkušební verzi.
- Vývojové prostředí .NET – Visual Studio je skvělou volbou.
- Základní znalost jazyka C# – Znalost tříd a práce s daty vám pomůže s nácvikem.
Než budeme pokračovat, ujistěte se, že vaše vývojové prostředí je nastaveno s potřebnými balíčky.
## Importovat balíčky
Pro efektivní používání Aspose.Cells je nutné importovat základní balíčky. Níže je uveden stručný přehled požadovaných jmenných prostorů:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Krok 1: Definování třídy dat zákazníka
Pro začátek si vytvořte jednoduchý `Customer` třída. Tato třída bude obsahovat základní údaje o zákaznících, jako například `FullName` a `Address`Představte si to jako způsob, jak definovat „tvar“ vašich dat.
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
## Krok 2: Nastavení třídy Seznam zákazníků
Dále definujte `CustomerList` třída, která rozšiřuje `ArrayList`Tento přizpůsobený seznam bude obsahovat instance `Customer` a povolit indexovaný přístup ke každé položce.
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
V tomto kroku zabalíme naše data do formátu, který Aspose.Cells dokáže rozpoznat a zpracovat.
## Krok 3: Vytvořte třídu zdroje dat zákazníka
A tady to začíná být zajímavé. Vytvoříme `CustomerDataSource` implementace třídy `ICellsDataTable` aby naše data byla kompatibilní s návrhářem sešitů Aspose.Cells.
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
Tento zvyk `CustomerDataSource` třída umožňuje Aspose.Cells interpretovat každý `Customer` objekt jako řádek v souboru aplikace Excel.
## Krok 4: Inicializace zákaznických dat
Nyní přidejme do našeho seznamu několik zákazníků. Zde načteme data, která se mají zapsat do sešitu. V případě potřeby můžete přidat další položky.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
tomto příkladu pracujeme s malou datovou sadou. Tento seznam však můžete snadno rozšířit načtením dat z databáze nebo jiných zdrojů.
## Krok 5: Načtení sešitu
Nyní otevřeme existující sešit aplikace Excel, který obsahuje potřebné inteligentní značky. Tento sešit bude sloužit jako naše šablona a Aspose.Cells bude dynamicky nahrazovat inteligentní značky daty o zákaznících.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
Zajistěte, aby `"SmartMarker1.xlsx"` obsahuje zástupné symboly jako `&=Customer.FullName` a `&=Customer.Address` kam se mají údaje vyplnit.
## Krok 6: Nastavení návrháře sešitů
Nyní nakonfigurujme návrháře sešitů tak, aby propojil zdroj dat o zákaznících s inteligentními značkami sešitu.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
Ten/Ta/To `SetDataSource` metoda spojuje naše `CustomerDataSource` k chytrým značkám v sešitu. Každá značka označená `&=Customer` v Excelu budou nyní nahrazeny odpovídajícími zákaznickými daty.
## Krok 7: Zpracování a uložení sešitu
Nakonec zpracujme sešit, doplníme data a uložíme výsledky.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Tento kód spustí zpracování funkce Smart Marker, nahradí všechny zástupné symboly daty a uloží výsledek jako `dest.xlsx`.
## Závěr
Gratulujeme! Úspěšně jste implementovali `ICellsDataTableDataSource` pro návrháře sešitů používající Aspose.Cells pro .NET. Tento přístup je ideální pro automatizaci vkládání dat do tabulek, zejména při práci s dynamickými daty, jako jsou seznamy zákazníků nebo skladové zásoby produktů. S těmito dovednostmi jste na dobré cestě k vytváření datově řízených aplikací, které vám usnadní tvorbu reportů v Excelu!
## Často kladené otázky
### Co je `ICellsDataTable` v Aspose.Cells?  
Jedná se o rozhraní, které umožňuje propojení vlastních zdrojů dat s inteligentními markery Aspose.Cells pro dynamické naplňování dat.
### Jak mohu přizpůsobit data v šabloně sešitu?  
Zástupné symboly nazývané inteligentní značky, jako například `&=Customer.FullName`, se používají. Tyto značky jsou během zpracování nahrazeny skutečnými daty.
### Je Aspose.Cells pro .NET zdarma?  
Aspose.Cells nabízí bezplatnou zkušební verzi, ale plný přístup vyžaduje placenou licenci. Podívejte se na jejich [bezplatná zkušební verze](https://releases.aspose.com/) nebo [nakoupit](https://purchase.aspose.com/buy) možnosti.
### Mohu dynamicky přidávat další zákaznická data?  
Rozhodně! Jednoduše vyplňte `CustomerList` s dalšími položkami před spuštěním programu.
### Kde můžu získat pomoc, když se ocitnu v pasti?  
Aspose má [fórum podpory](https://forum.aspose.com/c/cells/9) kde se uživatelé mohou ptát a získat pomoc od komunity a týmu Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}