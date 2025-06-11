---
"description": "Naucz się używać ICellsDataTableDataSource z Aspose.Cells dla .NET, aby dynamicznie wypełniać arkusze Excela. Idealne do automatyzacji danych klientów w skoroszytach."
"linktitle": "Użyj ICellsDataTableDataSource dla projektanta skoroszytów"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Użyj ICellsDataTableDataSource dla projektanta skoroszytów"
"url": "/pl/net/workbook-operations/use-icells-datatable-data-source/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Użyj ICellsDataTableDataSource dla projektanta skoroszytów

## Wstęp
Tworzenie zaawansowanych arkuszy kalkulacyjnych z automatyczną integracją danych może być przełomem, szczególnie w aplikacjach biznesowych. W tym samouczku zagłębimy się w to, jak używać `ICellsDataTableDataSource` dla projektanta skoroszytów w Aspose.Cells dla .NET. Przeprowadzimy Cię przez proces tworzenia prostego, czytelnego dla człowieka rozwiązania do dynamicznego ładowania niestandardowych danych do pliku Excel. Więc jeśli pracujesz z listami klientów, danymi sprzedaży lub czymś podobnym, ten przewodnik jest dla Ciebie!
## Wymagania wstępne
Aby rozpocząć, upewnij się, że masz następujące elementy:
- Biblioteka Aspose.Cells dla .NET – Można ją pobrać ze strony [Tutaj](https://releases.aspose.com/cells/net/) lub pobierz bezpłatną wersję próbną.
- Środowisko programistyczne .NET – Visual Studio to świetny wybór.
- Podstawowa znajomość języka C# – znajomość klas i obsługi danych ułatwi Ci zrozumienie tekstu.
Zanim przejdziemy dalej, upewnij się, że Twoje środowisko programistyczne zawiera niezbędne pakiety.
## Importuj pakiety
Aby skutecznie używać Aspose.Cells, musisz zaimportować niezbędne pakiety. Poniżej znajduje się krótki odnośnik do wymaganych przestrzeni nazw:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Krok 1: Zdefiniuj klasę danych klienta
Na początek utwórz prosty `Customer` klasa. Ta klasa będzie zawierać podstawowe dane klienta, takie jak `FullName` I `Address`. Pomyśl o tym jako o sposobie zdefiniowania „kształtu” swoich danych.
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
## Krok 2: Skonfiguruj klasę listy klientów
Następnie zdefiniuj `CustomerList` klasa, która się rozszerza `ArrayList`. Ta dostosowana lista będzie zawierać wystąpienia `Customer` i zezwól na indeksowany dostęp do każdego wpisu.
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
Na tym etapie pakujemy nasze dane do formatu, który Aspose.Cells może rozpoznać i przetworzyć.
## Krok 3: Utwórz klasę źródła danych klienta
Tutaj zaczyna się robić ciekawie. Stworzymy `CustomerDataSource` klasa wdrażająca `ICellsDataTable` aby nasze dane były kompatybilne z projektantem skoroszytów Aspose.Cells.
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
Ten zwyczaj `CustomerDataSource` Klasa umożliwia Aspose.Cells interpretowanie każdego `Customer` obiekt jako wiersz w pliku Excel.
## Krok 4: Zainicjuj dane klienta
Teraz dodajmy kilku klientów do naszej listy. Tutaj ładujemy dane, które mają zostać zapisane w skoroszycie. Możesz swobodnie dodawać więcej wpisów, jeśli to konieczne.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
tym przykładzie pracujemy z małym zestawem danych. Jednak możesz łatwo rozszerzyć tę listę, ładując dane z bazy danych lub innych źródeł.
## Krok 5: Załaduj skoroszyt
Teraz otwórzmy istniejący skoroszyt programu Excel, który zawiera niezbędne znaczniki inteligentne. Ten skoroszyt będzie służył jako nasz szablon, a Aspose.Cells dynamicznie zastąpi znaczniki inteligentne danymi klienta.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
Upewnij się, że `"SmartMarker1.xlsx"` zawiera symbole zastępcze, takie jak `&=Customer.FullName` I `&=Customer.Address` gdzie należy wpisać dane.
## Krok 6: Skonfiguruj projektanta skoroszytów
Teraz skonfigurujmy projektanta skoroszytów tak, aby powiązał źródło danych o klientach z inteligentnymi znacznikami skoroszytu.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
Ten `SetDataSource` metoda wiąże nasze `CustomerDataSource` do inteligentnych znaczników w skoroszycie. Każdy znacznik oznaczony `&=Customer` w programie Excel zostaną teraz zastąpione odpowiednimi danymi klienta.
## Krok 7: Przetwarzanie i zapisywanie skoroszytu
Na koniec przetworzymy skoroszyt, uzupełniając dane i zapisując wyniki.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Ten kod uruchamia przetwarzanie Smart Marker, zastępuje wszystkie symbole zastępcze danymi i zapisuje wynik jako `dest.xlsx`.
## Wniosek
Gratulacje! Udało Ci się wdrożyć `ICellsDataTableDataSource` dla projektanta skoroszytów korzystającego z Aspose.Cells dla .NET. To podejście jest idealne do automatyzacji wypełniania danych w arkuszach kalkulacyjnych, zwłaszcza w przypadku danych dynamicznych, takich jak listy klientów lub inwentaryzacje produktów. Dzięki tym umiejętnościom jesteś na dobrej drodze do tworzenia aplikacji opartych na danych, które sprawiają, że raportowanie oparte na programie Excel jest dziecinnie proste!
## Najczęściej zadawane pytania
### Co to jest `ICellsDataTable` w Aspose.Cells?  
Jest to interfejs umożliwiający łączenie niestandardowych źródeł danych z inteligentnymi znacznikami Aspose.Cells w celu dynamicznego wypełniania danych.
### Jak mogę dostosować dane w szablonie skoroszytu?  
Symbole zastępcze nazywane inteligentnymi znacznikami, takie jak `&=Customer.FullName`, są używane. Te znaczniki są zastępowane rzeczywistymi danymi podczas przetwarzania.
### Czy Aspose.Cells dla .NET jest darmowy?  
Aspose.Cells oferuje bezpłatny okres próbny, ale pełny dostęp wymaga płatnej licencji. Sprawdź ich [bezpłatny okres próbny](https://releases.aspose.com/) Lub [kupić](https://purchase.aspose.com/buy) opcje.
### Czy mogę dynamicznie dodawać więcej danych klientów?  
Oczywiście! Po prostu wypełnij `CustomerList` z dodatkowymi wpisami przed uruchomieniem programu.
### Gdzie mogę uzyskać pomoc, jeśli utknę?  
Aspose ma [forum wsparcia](https://forum.aspose.com/c/cells/9) gdzie użytkownicy mogą zadawać pytania i otrzymywać pomoc od społeczności i zespołu Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}