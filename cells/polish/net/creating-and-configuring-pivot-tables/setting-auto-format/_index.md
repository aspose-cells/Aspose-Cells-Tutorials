---
"description": "W tym szczegółowym samouczku krok po kroku dowiesz się, jak programowo ustawić automatyczne formatowanie tabel przestawnych programu Excel za pomocą Aspose.Cells for .NET."
"linktitle": "Ustawianie automatycznego formatowania tabeli przestawnej programowo w .NET"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Ustawianie automatycznego formatowania tabeli przestawnej programowo w .NET"
"url": "/pl/net/creating-and-configuring-pivot-tables/setting-auto-format/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ustawianie automatycznego formatowania tabeli przestawnej programowo w .NET

## Wstęp
Jeśli chodzi o analizę danych, tabele przestawne w programie Excel mogą być przełomem. Umożliwiają dynamiczne podsumowywanie i analizowanie danych, pomagając w wyciąganiu wniosków, których wydobycie ręcznie byłoby niemal niemożliwe. Ale co, jeśli chcesz zautomatyzować proces formatowania tabel przestawnych w .NET? Tutaj pokażę Ci, jak programowo ustawić automatyczne formatowanie tabeli przestawnej przy użyciu potężnej biblioteki Aspose.Cells dla .NET.
W tym przewodniku omówimy podstawy, przejdziemy przez wymagania wstępne, zaimportujemy niezbędne pakiety, a następnie przejdziemy do samouczka krok po kroku, aby pomóc Ci formatować tabele przestawne jak profesjonalista. Brzmi dobrze? Zaczynajmy!
## Wymagania wstępne
Zanim zaczniemy, upewnijmy się, że masz wszystko, czego potrzebujesz:
1. Środowisko programistyczne .NET: upewnij się, że masz działającą instancję programu Visual Studio (lub dowolnego środowiska IDE obsługującego platformę .NET).
2. Biblioteka Aspose.Cells: Aby płynnie pracować z plikami Excel, musisz mieć zainstalowaną bibliotekę Aspose.Cells. Jeśli jeszcze tego nie zrobiłeś, możesz ją pobrać z [strona do pobrania](https://releases.aspose.com/cells/net/).
3. Podstawowa wiedza o języku C#: Znajomość programowania w języku C# pomoże Ci lepiej zrozumieć poszczególne kroki.
4. Plik Excel (szablon): Na początek będziesz potrzebować pliku szablonu Excel, który zostanie przetworzony w naszym przykładzie. Dla uproszczenia możesz utworzyć przykładowy plik o nazwie `Book1.xls`.
## Importuj pakiety
Aby rozpocząć pracę z Aspose.Cells w swoim projekcie, musisz zaimportować niezbędne pakiety. Oto, jak możesz to skonfigurować w swoim projekcie .NET:
### Utwórz nowy projekt
Zacznij od utworzenia nowego projektu .NET w preferowanym środowisku IDE. 
### Dodaj odniesienia
Upewnij się, że dodałeś odwołanie do biblioteki Aspose.Cells. Jeśli pobrałeś bibliotekę, dodaj biblioteki DLL z ekstrakcji. Jeśli używasz NuGet, możesz po prostu uruchomić:
```bash
Install-Package Aspose.Cells
```
### Importuj przestrzenie nazw
Teraz w pliku kodu musisz zaimportować przestrzeń nazw Aspose.Cells. Możesz to zrobić, dodając następujący wiersz na górze pliku C#:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Po wykonaniu tych kroków możesz przystąpić do pisania kodu!
Teraz rozłóżmy udostępniony przez Ciebie kod na szczegółowe kroki wraz z wyjaśnieniami, co robi każda część. 
## Krok 1: Zdefiniuj katalog dokumentów
Na początek musisz ustawić ścieżkę do katalogu dokumentów, w którym znajdują się pliki Excela. W naszym przykładzie zdefiniujemy ją w następujący sposób:
```csharp
string dataDir = "Your Document Directory";  // Modyfikuj według potrzeb
```
Ten wiersz tworzy zmienną łańcuchową `dataDir` który zawiera ścieżkę do Twoich dokumentów. Upewnij się, że zastąpisz `"Your Document Directory"` z rzeczywistą ścieżką w Twoim systemie.
## Krok 2: Załaduj plik szablonu
Następnie należy załadować istniejący skoroszyt zawierający tabelę przestawną:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Ta linia inicjuje nowy `Workbook` obiekt poprzez załadowanie określonego pliku Excel. Plik powinien zawierać co najmniej jedną tabelę przestawną, aby kolejne kroki były skuteczne.
## Krok 3: Uzyskaj dostęp do żądanego arkusza roboczego
Określ, nad którym arkuszem kalkulacyjnym musisz pracować, aby uzyskać dostęp do tabeli przestawnej. W tym przypadku po prostu pobierzemy pierwszy:
```csharp
int pivotIndex = 0;  // Indeks tabeli przestawnej
Worksheet worksheet = workbook.Worksheets[0];
```
Tutaj, `worksheet` pobiera pierwszy arkusz kalkulacyjny ze skoroszytu. Indeks tabeli przestawnej jest ustawiony na `0`, co oznacza, że uzyskujemy dostęp do pierwszej tabeli przestawnej w arkuszu.
## Krok 4: Znajdź tabelę przestawną
Mając gotowy arkusz kalkulacyjny, czas uzyskać dostęp do tabeli przestawnej:
```csharp
PivotTable pivotTable = worksheet.PivotTables[pivotIndex];
```
Inicjuje to nowy `PivotTable` obiekt, pobierając tabelę przestawną o określonym indeksie z arkusza kalkulacyjnego.
## Krok 5: Ustaw właściwość automatycznego formatowania
A teraz przejdźmy do ciekawszej części: ustawienia opcji automatycznego formatowania dla tabeli przestawnej.
```csharp
pivotTable.IsAutoFormat = true; // Włącz automatyczne formatowanie
```
Ten wiersz włącza funkcję automatycznego formatowania tabeli przestawnej. Gdy jest ustawiony na `true`tabela przestawna zostanie automatycznie sformatowana na podstawie zdefiniowanych stylów.
## Krok 6: Wybierz konkretny typ formatu automatycznego
Chcemy również określić, jaki styl auto formatu ma przyjąć tabela przestawna. Aspose.Cells ma różne formaty, spośród których możemy wybierać. Oto jak to ustawić:
```csharp
pivotTable.AutoFormatType = Aspose.Cells.Pivot.PivotTableAutoFormatType.Report5;
```
Za pomocą tego wiersza przypisujemy określony typ formatu automatycznego do tabeli przestawnej. `Report5` to tylko przykład jednego stylu; możesz wybierać spośród wielu opcji, zależnie od swoich potrzeb. 
## Krok 7: Zapisz skoroszyt
Na koniec nie zapomnij zapisać skoroszytu po wprowadzeniu wszystkich zmian:
```csharp
workbook.Save(dataDir + "output.xls");
```
Ta linia kodu zapisuje zmodyfikowany skoroszyt do nowego pliku o nazwie `output.xls` w określonym katalogu. Upewnij się, że sprawdziłeś ten plik, aby zobaczyć swoją pięknie sformatowaną tabelę przestawną!
## Wniosek
Gratulacje! Właśnie zaprogramowałeś tabelę przestawną programu Excel do automatycznego formatowania za pomocą Aspose.Cells w .NET. Ten proces nie tylko oszczędza czas podczas przygotowywania raportów, ale także zapewnia spójność wyglądu danych przy każdym uruchomieniu. Za pomocą zaledwie kilku linijek kodu możesz znacznie ulepszyć swoje pliki programu Excel — zupełnie jak cyfrowy magik.
## Najczęściej zadawane pytania
### Czym jest Aspose.Cells?
Aspose.Cells to zaawansowana biblioteka .NET umożliwiająca obsługę plików Excel bez konieczności instalowania programu Microsoft Excel.
### Czy mogę sformatować wiele tabel przestawnych w jednym skoroszycie?
Tak, możesz przechodzić przez wiele obiektów tabeli przestawnej w skoroszycie, aby sformatować je jeden po drugim.
### Czy jest dostępna bezpłatna wersja próbna Aspose.Cells?
Oczywiście! Możesz zacząć od bezpłatnej wersji próbnej dostępnej [Tutaj](https://releases.aspose.com/).
### Co zrobić, jeśli moja tabela przestawna nie jest prawidłowo sformatowana?
Sprawdź, czy tabela przestawna jest poprawnie odwołana i czy istnieje typ automatycznego formatowania — w przeciwnym razie mogą zostać przywrócone ustawienia domyślne.
### Czy mogę zautomatyzować ten proces za pomocą zaplanowanych zadań?
Tak! Włączając ten kod do zaplanowanego zadania, możesz regularnie automatyzować generowanie i formatowanie raportów.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}