---
"description": "Dowiedz się, jak programowo zmieniać dane źródłowe tabeli przestawnej za pomocą Aspose.Cells dla platformy .NET, korzystając z naszego kompleksowego samouczka krok po kroku."
"linktitle": "Zmiana danych źródłowych tabeli przestawnej programowo w .NET"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Zmiana danych źródłowych tabeli przestawnej programowo w .NET"
"url": "/pl/net/creating-and-configuring-pivot-tables/changing-source-data/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zmiana danych źródłowych tabeli przestawnej programowo w .NET

## Wstęp
W świecie analizy danych niewiele narzędzi świeci tak jasno jak Microsoft Excel. Każdego dnia niezliczeni użytkownicy polegają na Excelu w zarządzaniu danymi i ich analizowaniu, ale w tle jest to o wiele bardziej skomplikowane niż po prostu klikanie i przeciąganie. Jeśli kiedykolwiek chciałeś programowo manipulować plikami Excela — konkretnie, aby zmienić dane źródłowe tabeli przestawnej — jesteś we właściwym miejscu! W tym przewodniku zbadamy, jak możesz to osiągnąć, używając Aspose.Cells dla .NET. Niezależnie od tego, czy jesteś doświadczonym programistą, czy dopiero zanurzasz palce u stóp w morzu programowania, znajdziesz ten samouczek wypełniony cennymi informacjami, które są łatwe do naśladowania.
## Wymagania wstępne
Zanim rozpoczniemy proces zmiany danych źródłowych tabeli przestawnej, upewnijmy się, że wszystko jest skonfigurowane i gotowe:
1. Visual Studio: Upewnij się, że masz zainstalowaną kopię programu Microsoft Visual Studio, ponieważ będziemy tutaj pisać kod.
2. Biblioteka Aspose.Cells: Musisz mieć pobraną bibliotekę Aspose.Cells i odwołać się do niej w swoim projekcie. Możesz ją pobrać [Tutaj](https://releases.aspose.com/cells/net/).
3. Podstawowa znajomość języka C#: Choć ten samouczek jest uproszczony, znajomość języka C# pomoże Ci lepiej zrozumieć kod.
4. Plik Excela: Powinieneś mieć przykładowy plik Excela (np. „Book1.xlsx”) zawierający tabelę przestawną, którą możemy manipulować.
Dobrze, mając te warunki wstępne spełnione, możemy przystąpić do importowania niezbędnych pakietów i rozpoczęcia kodowania!
## Importuj pakiety
Najpierw najważniejsze — zaimportujmy pakiety, których będziemy potrzebować. Otwórz projekt C# w Visual Studio i dodaj następujące dyrektywy using na górze pliku kodu:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Te przestrzenie nazw dadzą ci dostęp do podstawowych klas potrzebnych do pracy z plikami Excela i manipulowania ich zawartością za pomocą Aspose.Cells.

Teraz podzielmy proces na łatwe do opanowania kroki. Przejdziemy przez otwieranie pliku Excel, modyfikowanie arkusza kalkulacyjnego, zmianę źródła danych tabeli przestawnej i zapisywanie wyników.
## Krok 1: Zdefiniuj katalog dokumentów
Najpierw musisz określić, gdzie znajduje się plik Excel. Zmodyfikuj `dataDir` zmienna wskazująca na folder zawierający plik „Book1.xlsx”.
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
```
Ten wiersz określa katalog, w którym przechowywany jest plik Excela, dzięki czemu późniejszy dostęp do niego będzie łatwiejszy.
## Krok 2: Określ ścieżkę wejściową
Następnie utwórzmy ciąg określający pełną ścieżkę do pliku wejściowego programu Excel:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Pomaga to usprawnić dostęp do plików, ponieważ nie musisz wpisywać tej samej ścieżki wiele razy w całym kodzie.
## Krok 3: Utwórz strumień plików
Teraz czas otworzyć plik Excel. Utworzymy `FileStream` który umożliwia odczytanie zawartości pliku Excel:
```csharp
// Tworzenie strumienia plików zawierającego plik Excela do otwarcia
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Ten wiersz otwiera plik w trybie do odczytu, umożliwiając dostęp do jego danych.
## Krok 4: Załaduj skoroszyt
Mając już strumień plików, następnym krokiem jest załadowanie skoroszytu:
```csharp
// Otwieranie pliku Excel za pomocą strumienia plików
Workbook workbook = new Workbook(fstream);
```
To polecenie pobiera plik Excel i ładuje go do `Workbook` obiekt. Po załadowaniu pliku możesz nim manipulować według potrzeb.
## Krok 5: Uzyskaj dostęp do arkusza kalkulacyjnego
Czas zagłębić się w szczegóły. Uzyskamy dostęp do pierwszego arkusza w skoroszycie:
```csharp
// Dostęp do pierwszego arkusza kalkulacyjnego w pliku Excel
Worksheet worksheet = workbook.Worksheets[0];
```
Dzięki temu uzyskasz bezpośredni dostęp do danych w pierwszym arkuszu, co ułatwi ich modyfikację.
## Krok 6: Wprowadź nowe dane
Następnie chcemy wstawić nowe dane do komórek. W tym przykładzie dodamy kilka przykładowych danych:
```csharp
// Wprowadzanie nowych danych do komórek arkusza kalkulacyjnego
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
Tutaj wstawiamy wartości „Golf”, „Qtr4” i `7000` do określonych komórek. Możesz zmienić te wartości na takie, które odpowiadają Twoim potrzebom.
## Krok 7: Zmień zakres nazwany
Teraz zmienimy nazwany zakres, do którego odnosi się tabela przestawna. Wiąże się to z utworzeniem lub aktualizacją zakresu:
```csharp
// Zmiana zakresu nazwanego „DataSource”
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Definiując nowy zakres, mamy pewność, że tabela przestawna użyje nowych danych po odświeżeniu.
## Krok 8: Zapisz zmodyfikowany plik Excela
Po wszystkich zmianach, ważne jest, aby zapisać swoją pracę! Zapiszmy zmodyfikowany skoroszyt:
```csharp
// Zapisywanie zmodyfikowanego pliku Excel
workbook.Save(dataDir + "output.xls");
```
To polecenie zapisuje skoroszyt w nowym pliku, dzięki czemu nie musisz nadpisywać oryginalnego pliku, chyba że chcesz!
## Krok 9: Zamknij strumień plików
Na koniec należy koniecznie zamknąć strumień plików, aby zwolnić wszelkie używane zasoby:
```csharp
// Zamknięcie strumienia plików w celu zwolnienia wszystkich zasobów
fstream.Close();
```
Ten krok gwarantuje, że Twoja aplikacja nie będzie miała wycieków pamięci i pozostanie wydajna.
## Wniosek
Gratulacje! Właśnie udało Ci się zmienić dane źródłowe tabeli przestawnej programowo w .NET przy użyciu Aspose.Cells. Ta funkcjonalność otwiera wiele możliwości automatyzacji zadań programu Excel i usprawnienia przepływu pracy. Niezależnie od tego, czy aktualizujesz raporty finansowe, śledzisz dane sprzedaży, czy po prostu bawisz się zestawami danych, możliwość zrobienia tego programowo może zaoszczędzić mnóstwo czasu i zmniejszyć ryzyko błędów.

## Najczęściej zadawane pytania
### Czym jest Aspose.Cells?
Aspose.Cells to zaawansowana biblioteka .NET do pracy z plikami Excela, umożliwiająca użytkownikom programowe tworzenie, modyfikowanie i manipulowanie dokumentami Excela.
### Czy mogę zmienić dane źródłowe istniejących tabel przestawnych, korzystając z tej metody?
Oczywiście! Ta metoda pozwala na aktualizację źródła danych dla istniejących tabel przestawnych w skoroszycie programu Excel.
### Czy muszę mieć zainstalowany pakiet Office, aby używać Aspose.Cells?
Nie! Aspose.Cells to samodzielna biblioteka, co oznacza, że nie potrzebujesz zainstalowanego pakietu Microsoft Office, aby pracować z plikami Excel.
### Czy korzystanie z Aspose.Cells jest bezpłatne?
Aspose.Cells oferuje bezpłatną wersję próbną, ale aby uzyskać pełną funkcjonalność, musisz kupić licencję. Szczegóły znajdziesz [Tutaj](https://purchase.aspose.com/buy).
### Gdzie mogę znaleźć więcej przykładów i pomoc?
Aby uzyskać więcej przykładów i wsparcia, zapoznaj się z [Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/net/) i ich forum społecznościowe [Tutaj](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}