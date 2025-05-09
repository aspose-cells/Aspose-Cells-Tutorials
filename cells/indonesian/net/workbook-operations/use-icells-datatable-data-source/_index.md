---
"description": "Tanuld meg az ICellsDataTableDataSource és az Aspose.Cells for .NET használatát Excel-táblázatok dinamikus feltöltéséhez. Tökéletes az ügyféladatok munkafüzetekben történő automatizálásához."
"linktitle": "Az ICellsDataTableDataSource használata a Workbook Designerhez"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Az ICellsDataTableDataSource használata a Workbook Designerhez"
"url": "/id/net/workbook-operations/use-icells-datatable-data-source/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Az ICellsDataTableDataSource használata a Workbook Designerhez

## Bevezetés
A fejlett táblázatok létrehozása automatizált adatintegrációval gyökeresen megváltoztathatja a játékszabályokat, különösen az üzleti alkalmazásokban. Ebben az oktatóanyagban részletesebben is bemutatjuk, hogyan használhatók. `ICellsDataTableDataSource` egy Aspose.Cells for .NET munkafüzet-tervező számára. Végigvezetünk egy egyszerű, ember által olvasható megoldás létrehozásán, amellyel dinamikusan betöltheti az egyéni adatokat egy Excel-fájlba. Tehát, ha ügyféllistákkal, értékesítési adatokkal vagy bármi hasonlóval dolgozik, ez az útmutató Önnek szól!
## Előfeltételek
Kezdésként győződjön meg arról, hogy rendelkezik a következőkkel:
- Aspose.Cells .NET könyvtárhoz – Letöltheti innen: [itt](https://releases.aspose.com/cells/net/) vagy szerezz be egy ingyenes próbaverziót.
- .NET fejlesztői környezet – A Visual Studio nagyszerű választás.
- C# alapismeretek – Az osztályok és az adatkezelés ismerete segít majd a haladásban.
Mielőtt továbblépnénk, győződjünk meg arról, hogy a fejlesztői környezetünk telepítve van a szükséges csomagokkal.
## Csomagok importálása
Az Aspose.Cells hatékony használatához importálnia kell a nélkülözhetetlen csomagokat. Az alábbiakban egy gyors áttekintést talál a szükséges névterekről:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## 1. lépés: Ügyféladat-osztály definiálása
Kezdésként hozzon létre egy egyszerű `Customer` osztály. Ez az osztály az alapvető ügyféladatokat fogja tartalmazni, mint például `FullName` és `Address`Gondolj rá úgy, mint egy módra az adataid „alakjának” meghatározására.
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
## 2. lépés: Az Ügyféllista osztály beállítása
Ezután definiáljon egy `CustomerList` osztály, amely kiterjed `ArrayList`Ez a testreszabott lista a következő példányokat fogja tartalmazni: `Customer` és engedélyezze az indexelt hozzáférést minden bejegyzéshez.
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
Ebben a lépésben az adatainkat egy olyan formátumba csomagoljuk, amelyet az Aspose.Cells felismer és feldolgoz.
## 3. lépés: Hozza létre az Ügyfél adatforrás osztályt
Itt kezd érdekessé válni a dolog. Létrehozunk egy `CustomerDataSource` osztály megvalósítása `ICellsDataTable` hogy adataink kompatibilisek legyenek az Aspose.Cells munkafüzet-tervezőjével.
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
Ez a szokás `CustomerDataSource` osztály lehetővé teszi az Aspose.Cells számára, hogy mindegyiket értelmezze `Customer` objektum sorként az Excel fájlban.
## 4. lépés: Az ügyféladatok inicializálása
Most adjunk hozzá néhány ügyfelet a listánkhoz. Itt töltjük be a munkafüzetbe írandó adatokat. Szükség szerint további bejegyzéseket is hozzáadhatunk.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
Ebben a példában egy kis adathalmazzal dolgozunk. Ez a lista azonban könnyen bővíthető adatbázisból vagy más forrásokból származó adatok betöltésével.
## 5. lépés: A munkafüzet betöltése
Most nyissunk meg egy meglévő Excel-munkafüzetet, amely tartalmazza a szükséges intelligens jelölőket. Ez a munkafüzet fog szolgálni sablonként, és az Aspose.Cells dinamikusan lecseréli az intelligens jelölőket az ügyféladatokra.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
Győződjön meg róla, hogy `"SmartMarker1.xlsx"` helyőrzőket tartalmaz, mint például `&=Customer.FullName` és `&=Customer.Address` hova kell kitölteni az adatokat.
## 6. lépés: A Munkafüzet-tervező beállítása
Most konfiguráljuk a munkafüzet-tervezőt úgy, hogy az ügyféladatforrásunkat a munkafüzet intelligens jelölőivel összekapcsolja.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
A `SetDataSource` a módszer megköti a mi `CustomerDataSource` a munkafüzet intelligens jelölőihez. Minden jelölő fel van tüntetve `&=Customer` az Excelben mostantól a megfelelő ügyféladatokkal lesznek helyettesítve.
## 7. lépés: A munkafüzet feldolgozása és mentése
Végül dolgozzuk fel a munkafüzetet az adatok kitöltéséhez és az eredmények mentéséhez.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Ez a kód elindítja az intelligens jelölő feldolgozását, az összes helyőrzőt adatokkal helyettesíti, és az eredményt más néven menti. `dest.xlsx`.
## Következtetés
Gratulálunk! Sikeresen megvalósítottad `ICellsDataTableDataSource` egy Aspose.Cells for .NET-et használó munkafüzet-tervező számára. Ez a megközelítés ideális a táblázatok adatfeltöltésének automatizálására, különösen dinamikus adatok, például ügyféllisták vagy termékkészletek kezelésekor. Ezekkel a készségekkel jó úton haladsz afelé, hogy adatvezérelt alkalmazásokat építs, amelyek megkönnyítik az Excel-alapú jelentéskészítést!
## GYIK
### Mi az `ICellsDataTable` az Aspose.Cells-ben?  
Ez egy olyan felület, amely lehetővé teszi az egyéni adatforrások összekapcsolását az Aspose.Cells intelligens jelölőivel a dinamikus adatfeltöltés érdekében.
### Hogyan szabhatom testre az adatokat a munkafüzet sablonjában?  
Intelligens jelölőknek nevezett helyőrzők, például `&=Customer.FullName`, használatosak. Ezeket a jelölőket a feldolgozás során valós adatokkal helyettesítjük.
### Ingyenes az Aspose.Cells .NET-hez?  
Az Aspose.Cells ingyenes próbaverziót kínál, de a teljes hozzáféréshez fizetős licenc szükséges. Ellenőrizze a következőt: [ingyenes próba](https://releases.aspose.com/) vagy [vétel](https://purchase.aspose.com/buy) opciók.
### Dinamikusan hozzáadhatok több ügyféladatot?  
Teljesen! Egyszerűen töltse ki a `CustomerList` további bejegyzésekkel a program futtatása előtt.
### Hol kaphatok segítséget, ha elakadtam?  
Aspose-nak van egy [támogató fórum](https://forum.aspose.com/c/cells/9) ahol a felhasználók kérdéseket tehetnek fel és segítséget kaphatnak a közösségtől és az Aspose csapatától.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}