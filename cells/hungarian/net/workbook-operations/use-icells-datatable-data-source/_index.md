---
title: Használja az ICellsDataTableDataSource for Workbook Designer alkalmazást
linktitle: Használja az ICellsDataTableDataSource for Workbook Designer alkalmazást
second_title: Aspose.Cells .NET Excel Processing API
description: Tanulja meg az ICellsDataTableDataSource használatát az Aspose.Cells for .NET-ben az Excel-lapok dinamikus feltöltéséhez. Tökéletes az ügyféladatok munkafüzetekben való automatizálására.
weight: 21
url: /hu/net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Használja az ICellsDataTableDataSource for Workbook Designer alkalmazást

## Bevezetés
 A fejlett táblázatok automatizált adatintegrációval történő készítése nagy változást hozhat, különösen az üzleti alkalmazásokban. Ebben az oktatóanyagban a használat módját mutatjuk be`ICellsDataTableDataSource`munkafüzet-tervezőnek az Aspose.Cells for .NET-ben. Végigvezetjük egy egyszerű, ember által olvasható megoldás létrehozásán, amellyel dinamikusan tölthet be egyéni adatokat egy Excel-fájlba. Tehát, ha vásárlói listákkal, értékesítési adatokkal vagy bármi hasonlóval dolgozik, ez az útmutató az Ön számára készült!
## Előfeltételek
A kezdéshez győződjön meg arról, hogy rendelkezik a következőkkel:
-  Aspose.Cells for .NET Library – Letöltheti innen[itt](https://releases.aspose.com/cells/net/) vagy szerezzen be egy ingyenes próbaverziót.
- .NET fejlesztői környezet – A Visual Studio nagyszerű választás.
- A C# alapvető ismerete – Az osztályok és az adatkezelés ismerete segít a követésben.
Mielőtt folytatnánk, győződjön meg arról, hogy fejlesztői környezete be van állítva a szükséges csomagokkal.
## Csomagok importálása
Az Aspose.Cells hatékony használatához fontos csomagokat kell importálnia. Az alábbiakban egy gyors hivatkozás található a szükséges névterekhez:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## 1. lépés: Határozzon meg egy ügyféladatosztályt
 Kezdésként hozzon létre egy egyszerű`Customer` osztály. Ez az osztály olyan alapvető ügyféladatokat tartalmaz, mint pl`FullName` és`Address`Tekints rá úgy, mint az adatok "alakjának" meghatározására.
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
## 2. lépés: Állítsa be az Ügyféllista osztályt
 Ezután határozza meg a`CustomerList` osztály, amely kiterjed`ArrayList` . Ez a testreszabott lista tartalmazza a példányokat`Customer` és indexelt hozzáférést tesz lehetővé minden bejegyzéshez.
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
Ebben a lépésben adatainkat olyan formátumba csomagoljuk, amelyet az Aspose.Cells képes felismerni és feldolgozni.
## 3. lépés: Hozza létre az Ügyfél adatforrás osztályát
 Itt válnak érdekessé a dolgok. Létrehozunk a`CustomerDataSource` osztály megvalósítása`ICellsDataTable` hogy adataink kompatibilisek legyenek az Aspose.Cells munkafüzet-tervezőjével.
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
 Ez a szokás`CustomerDataSource` osztály lehetővé teszi az Aspose.Cells számára, hogy mindegyiket értelmezze`Customer` objektumot sorként az Excel fájlban.
## 4. lépés: Inicializálja az Ügyféladatokat
Most adjunk hozzá néhány ügyfelet a listánkhoz. Itt töltjük be a munkafüzetbe írandó adatokat. Ha szükséges, adjon hozzá további bejegyzéseket.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
Ebben a példában egy kis adatkészlettel dolgozunk. Ezt a listát azonban könnyen bővítheti adatbázisból vagy más forrásból származó adatok betöltésével.
## 5. lépés: Töltse be a munkafüzetet
Most nyissunk meg egy meglévő Excel-munkafüzetet, amely tartalmazza a szükséges intelligens jelölőket. Ez a munkafüzet lesz a sablonunk, és az Aspose.Cells dinamikusan lecseréli az intelligens jelölőket az ügyféladatokra.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
 Biztosítsd ezt`"SmartMarker1.xlsx"` helyőrzőket tartalmaz, mint például`&=Customer.FullName` és`&=Customer.Address` ahol adatokat kell kitölteni.
## 6. lépés: Állítsa be a munkafüzet-tervezőt
Most állítsuk be a munkafüzet-tervezőt úgy, hogy az ügyféladatforrásunkat összekapcsolja a munkafüzet intelligens jelölőivel.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
 A`SetDataSource` módszer megköti a mi`CustomerDataSource` a munkafüzet intelligens jelölőihez. Minden marker fel van címkézve`&=Customer` Az Excelben most a megfelelő ügyféladatok váltják fel.
## 7. lépés: A munkafüzet feldolgozása és mentése
Végül dolgozzuk fel a munkafüzetet az adatok kitöltéséhez és az eredmények mentéséhez.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Ez a kód elindítja az intelligens jelölő feldolgozást, lecseréli az összes helyőrzőt adatra, és az eredményt más néven menti`dest.xlsx`.
## Következtetés
 Gratulálok! Sikeresen végrehajtottad`ICellsDataTableDataSource` Aspose.Cells for .NET használatával munkafüzet-tervező számára. Ez a megközelítés ideális a táblázatok adatpopulációjának automatizálására, különösen dinamikus adatok, például ügyféllisták vagy termékkészletek kezelésekor. Ezekkel a készségekkel már jó úton halad az adatvezérelt alkalmazások létrehozása felé, amelyek az Excel-alapú jelentéskészítést gyerekjátékká teszik!
## GYIK
###  Mi az`ICellsDataTable` in Aspose.Cells?  
Ez egy olyan felület, amely lehetővé teszi az egyéni adatforrások összekapcsolását az Aspose.Cells intelligens jelölőkkel a dinamikus adatpopuláció érdekében.
### Hogyan testreszabhatom az adatokat a munkafüzet-sablonban?  
 Az intelligens jelölőknek nevezett helyőrzők, mint pl`&=Customer.FullName`, használatosak. Ezeket a markereket a feldolgozás során valós adatokkal helyettesítjük.
### Az Aspose.Cells for .NET ingyenes?  
 Az Aspose.Cells ingyenes próbaverziót kínál, de a teljes hozzáféréshez fizetős licenc szükséges. Ellenőrizze az övéket[ingyenes próbaverzió](https://releases.aspose.com/) vagy[vétel](https://purchase.aspose.com/buy) opciók.
### Hozzáadhatok több ügyféladatot dinamikusan?  
 Teljesen! Egyszerűen töltse fel a`CustomerList`további bejegyzésekkel a program futtatása előtt.
### Hol kaphatok segítséget, ha elakadok?  
 Aspose rendelkezik a[támogatási fórum](https://forum.aspose.com/c/cells/9) ahol a felhasználók kérdéseket tehetnek fel, és segítséget kaphatnak a közösségtől és az Aspose csapatától.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
