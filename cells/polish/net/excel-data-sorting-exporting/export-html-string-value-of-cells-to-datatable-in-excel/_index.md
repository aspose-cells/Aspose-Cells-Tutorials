---
"description": "Dowiedz się, jak eksportować wartości ciągu HTML z komórek programu Excel do tabeli DataTable przy użyciu Aspose.Cells dla .NET, korzystając z prostego samouczka krok po kroku."
"linktitle": "Eksportuj wartość ciągu HTML komórek do tabeli danych w programie Excel"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Eksportuj wartość ciągu HTML komórek do tabeli danych w programie Excel"
"url": "/pl/net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Eksportuj wartość ciągu HTML komórek do tabeli danych w programie Excel

## Wstęp

Podczas pracy z plikami Excela w środowisku .NET możesz potrzebować wyodrębnić informacje z komórek, nie tylko jako zwykły tekst, ale raczej jako ciągi HTML. Może to być bardzo przydatne, gdy masz do czynienia z danymi w formacie rich text lub gdy chcesz zachować formatowanie. W tym przewodniku przeprowadzę Cię przez eksportowanie wartości ciągu HTML komórek do DataTable przy użyciu Aspose.Cells dla .NET. 

## Wymagania wstępne

Zanim zagłębisz się w kod, upewnijmy się, że masz wszystko, czego potrzebujesz. Oto krótka lista kontrolna:

1. Podstawowa wiedza na temat języka C# i .NET: Zanim zaczniesz kodować, upewnij się, że znasz programowanie w języku C# i podstawy platformy .NET.
2. Aspose.Cells dla .NET: Jeśli jeszcze tego nie zrobiłeś, musisz zainstalować Aspose.Cells dla .NET. Możesz pobrać bezpłatną wersję próbną z [Tutaj](https://releases.aspose.com/).
3. Visual Studio lub IDE Twojego wyboru: Skonfiguruj swoje środowisko do pisania kodu C#. Visual Studio jest polecane ze względu na szeroki zakres funkcji i łatwość użytkowania.
4. Przykładowy plik Excela: Będziesz potrzebować przykładowego pliku Excela (`sampleExportTableAsHtmlString.xlsx`) do pracy. Upewnij się, że znajduje się w katalogu, do którego jest dostęp.
5. Menedżer pakietów NuGet: Upewnij się, że masz dostęp do Menedżera pakietów NuGet w swoim projekcie, aby móc łatwo dodać bibliotekę Aspose.Cells.

Mając te warunki wstępne za sobą, możemy zabrać się za kodowanie!

## Importuj pakiety

Zanim zaczniemy pracę z Aspose.Cells, musimy zaimportować niezbędne pakiety. Zazwyczaj wiąże się to z dodaniem pakietu NuGet Aspose.Cells do projektu. Oto jak to zrobić:

### Otwórz Menedżera pakietów NuGet

W programie Visual Studio kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz opcję Zarządzaj pakietami NuGet.

### Wyszukaj Aspose.Cells

W Menedżerze pakietów NuGet wpisz `Aspose.Cells` w pasku wyszukiwania.

### Zainstaluj pakiet

Po znalezieniu Aspose.Cells kliknij przycisk Install. Spowoduje to dodanie biblioteki do projektu i umożliwi zaimportowanie jej do kodu.

### Importuj przestrzeń nazw

Dodaj następującą dyrektywę using na górze pliku kodu:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

Teraz, gdy wszystko już skonfigurowaliśmy, możemy przejść do szczegółowego procesu eksportowania wartości ciągu HTML z pliku Excel do obiektu DataTable. 

## Krok 1: Zdefiniuj katalog źródłowy

Zacznij od zdefiniowania katalogu, w którym przechowywany jest przykładowy plik Excel. Jest to kluczowe, ponieważ informuje aplikację, gdzie ma znaleźć plik. Oto kod:

```csharp
string sourceDir = "Your Document Directory";
```

Pamiętaj o wymianie `"Your Document Directory"` z rzeczywistą ścieżką do pliku Excel.

## Krok 2: Załaduj przykładowy plik Excel

Następnym krokiem jest załadowanie skoroszytu programu Excel. Użyjesz `Workbook` klasa z Aspose.Cells, aby to zrobić. Oto jak możesz załadować plik:

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

Ta prosta linia kodu inicjuje skoroszyt i ładuje określony plik Excela.

## Krok 3: Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego

Po załadowaniu skoroszytu będziesz chciał uzyskać dostęp do konkretnego arkusza zawierającego interesujące Cię dane. Zazwyczaj zaczynasz od pierwszego arkusza:

```csharp
Worksheet ws = wb.Worksheets[0];
```

Tutaj pracujemy z pierwszym arkuszem kalkulacyjnym (indeks 0). Upewnij się, że Twoje dane są na właściwym arkuszu.

## Krok 4: Określ opcje eksportu tabeli

Aby kontrolować sposób eksportowania danych, należy skonfigurować `ExportTableOptions`tym przypadku należy upewnić się, że nazwy kolumn nie zostaną wyeksportowane, a dane komórek zostaną wyeksportowane jako ciągi HTML:

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

Taka konfiguracja umożliwia zachowanie bogatego formatowania danych komórki podczas eksportowania.

## Krok 5: Eksportuj komórki do tabeli danych

Teraz nadchodzi kluczowa część, w której faktycznie eksportujesz dane. Używając `ExportDataTable` metodą, możesz wyciągnąć dane z arkusza kalkulacyjnego do `DataTable`Oto jak to zrobić:

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

Ten kod eksportuje określony zakres komórek (od wiersza 0 i kolumny 0 do wiersza 3 i kolumny 3) do tabeli DataTable, korzystając z opcji określonych wcześniej.

## Krok 6: Wydrukuj wartość ciągu HTML

Na koniec wydrukujmy wartość ciągu HTML z określonej komórki w DataTable, aby zobaczyć, co udało nam się wyeksportować. Na przykład, jeśli chcesz wydrukować wartość z trzeciego wiersza i drugiej kolumny, wykonaj następujące czynności:

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

Ten wiersz drukuje żądany ciąg HTML z DataTable do konsoli. 

## Wniosek 

masz! Udało Ci się wyeksportować wartości ciągu HTML z komórek w pliku Excel do DataTable przy użyciu Aspose.Cells dla .NET. Ta możliwość nie tylko wzbogaca Twoje umiejętności manipulowania danymi, ale także rozszerza Twoje opcje w przypadku sformatowanej zawartości bezpośrednio z plików Excel. 

## Najczęściej zadawane pytania

### Czy mogę używać Aspose.Cells do innych formatów plików niż Excel?  
Tak, Aspose.Cells jest przeznaczony głównie dla programu Excel, ale Aspose oferuje również inne biblioteki dla innych formatów.

### Czy potrzebuję licencji na Aspose.Cells?  
Tak, do użytku produkcyjnego wymagana jest ważna licencja. Możesz uzyskać tymczasową licencję [Tutaj](https://purchase.aspose.com/temporary-license/).

### Co jeśli mój plik Excel zawiera formuły? Czy zostaną one poprawnie wyeksportowane?  
Tak, Aspose.Cells obsługuje formuły, a podczas eksportowania zostaną one obliczone na podstawie ich wartości wynikowych.

### Czy można zmienić opcje eksportu?  
Oczywiście! Możesz dostosować `ExportTableOptions` aby dopasować je do Twoich konkretnych potrzeb.

### Gdzie mogę znaleźć bardziej szczegółową dokumentację Aspose.Cells?  
Można znaleźć obszerną dokumentację [Tutaj](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}