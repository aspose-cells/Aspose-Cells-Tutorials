---
"description": "Dowiedz się, jak bez wysiłku konwertować skoroszyty programu Excel do formatu CSV za pomocą Aspose.Cells, korzystając z tego kompleksowego samouczka krok po kroku przeznaczonego dla programistów .NET."
"linktitle": "Zapisz skoroszyt w formacie tekstowym CSV"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Zapisz skoroszyt w formacie tekstowym CSV"
"url": "/pl/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zapisz skoroszyt w formacie tekstowym CSV

## Wstęp
Podczas pracy z danymi, wybrany format może naprawdę określić, jak łatwo możesz z nimi pracować. Jednym z najpopularniejszych formatów obsługi danych tabelarycznych jest CSV (Comma-Separated Values). Jeśli jesteś programistą pracującym z plikami Excela i musisz przekonwertować skoroszyty do formatu CSV, Aspose.Cells dla .NET to fantastyczna biblioteka, która upraszcza to zadanie. W tym samouczku przedstawimy kroki, aby płynnie przekonwertować skoroszyt Excela do formatu tekstowego CSV.
## Wymagania wstępne
Zanim przejdziemy do konkretów, upewnijmy się, że masz wszystko, czego potrzebujesz, aby zacząć:
1. Podstawowa znajomość języka C# i .NET: Ponieważ będziemy pisać kod w języku C#, niezbędna jest znajomość tego języka i platformy .NET.
2. Biblioteka Aspose.Cells: Upewnij się, że masz zainstalowaną bibliotekę Aspose.Cells dla .NET w swoim środowisku programistycznym. Możesz ją pobrać [Tutaj](https://releases.aspose.com/cells/net/).
3. Visual Studio lub dowolne środowisko IDE C#: Będziesz potrzebować zintegrowanego środowiska programistycznego (IDE), aby pisać i wykonywać swój kod. Visual Studio jest popularnym wyborem.
4. Skoroszyt programu Excel: Przygotuj przykładowy skoroszyt programu Excel (np. „książka1.xls”) zawierający dane umożliwiające przetestowanie konwersji.
## Importuj pakiety
Teraz, gdy mamy już spełnione nasze wymagania wstępne, pierwszym krokiem w procesie jest zaimportowanie niezbędnych pakietów. W swoim projekcie C# musisz uwzględnić następującą przestrzeń nazw na górze pliku kodu:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Te przestrzenie nazw dadzą ci dostęp do klas i metod potrzebnych do pracy z plikami Excela i zarządzania strumieniami pamięci.
## Krok 1: Określ ścieżkę do katalogu dokumentów
Pierwszym krokiem w naszym procesie jest zdefiniowanie, gdzie przechowywane są nasze dokumenty (skoroszyty programu Excel). Jest to niezbędne, ponieważ pozwala naszemu programowi wiedzieć, gdzie znaleźć pliki, które musi przetworzyć. 
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
```
Pamiętaj o wymianie `"Your Document Directory"` z rzeczywistą ścieżką, gdzie znajduje się Twój plik „book1.xls”. Może to być katalog na Twoim komputerze lub ścieżka do serwera.
## Krok 2: Załaduj swój skoroszyt źródłowy
Następnie musimy załadować skoroszyt programu Excel, który zostanie przekonwertowany do formatu CSV.
```csharp
// Załaduj swój skoroszyt źródłowy
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
Ten `Workbook` Klasa z biblioteki Aspose.Cells umożliwia manipulację i dostęp do skoroszytów programu Excel. Przekazując ścieżkę do pliku, ładujemy określony skoroszyt do przetworzenia.
## Krok 3: Zainicjuj tablicę bajtów dla danych skoroszytu
Zanim rozpoczniemy konwersję skoroszytu do formatu CSV, musimy zainicjować pustą tablicę bajtów, która będzie ostatecznie przechowywać wszystkie dane arkusza kalkulacyjnego.
```csharp
// Tablica 0-bajtowa
byte[] workbookData = new byte[0];
```
Ta tablica bajtów połączy dane z każdego arkusza kalkulacyjnego w pojedynczą strukturę, którą później możemy zapisać w pliku.
## Krok 4: Skonfiguruj opcje zapisywania tekstu
Teraz ustawmy opcje, jak chcemy zapisać format tekstu. Możesz wybrać niestandardowe ograniczniki lub pozostać przy tabulatorach.
```csharp
// Opcje zapisywania tekstu. Możesz użyć dowolnego typu separatora
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // Ustawianie tabulatora jako separatora
```
W tym przykładzie używamy znaku tabulacji jako separatora. Możesz zastąpić `'\t'` z dowolnym znakiem, np. przecinkiem (`,`), w zależności od tego jak chcesz sformatować plik CSV.
## Krok 5: Przejrzyj każdy arkusz kalkulacyjny
Następnie przejdziemy przez wszystkie arkusze kalkulacyjne w skoroszycie, zapisując każdy z nich w naszym `workbookData` tablicy, ale najpierw musisz wybrać arkusz, na którym chcesz pracować.
```csharp
// Skopiuj dane każdego arkusza kalkulacyjnego w formacie tekstowym do tablicy danych skoroszytu
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // Zapisz aktywny arkusz kalkulacyjny w formacie tekstowym
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
Pętla przechodzi przez każdy arkusz w skoroszycie. `ActiveSheetIndex` jest ustawiony tak, że za każdym razem, gdy przechodzimy przez pętlę, zapisujemy bieżący arkusz roboczy. Wyniki zostaną zapisane w pamięci za pomocą `MemoryStream`.
## Krok 6: Pobierz dane z arkusza kalkulacyjnego
Po zapisaniu arkusza kalkulacyjnego w strumieniu pamięci kolejnym krokiem jest pobranie tych danych i dołączenie ich do naszego `workbookData` szyk.
```csharp
    // Zapisz dane arkusza kalkulacyjnego w tablicy danych arkusza
    ms.Position = 0; // Zresetuj pozycję strumienia pamięci
    byte[] sheetData = ms.ToArray(); // Pobierz tablicę bajtów
```
`ms.Position = 0;` resetuje pozycję do odczytu po zapisie. Następnie używamy `ToArray()` aby przekonwertować strumień pamięci na tablicę bajtów przechowującą dane arkusza kalkulacyjnego.
## Krok 7: Połącz dane z arkusza kalkulacyjnego
Teraz połączymy dane z każdego arkusza w jeden `workbookData` tablica zainicjowana wcześniej.
```csharp
    // Połącz dane z tego arkusza kalkulacyjnego w tablicę danych skoroszytu
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
Tworzymy nową tablicę, która jest wystarczająco duża, aby pomieścić zarówno istniejące dane skoroszytu, jak i nowe dane arkusza. Następnie kopiujemy istniejące i nowe dane do tej połączonej tablicy w celu późniejszego wykorzystania.
## Krok 8: Zapisz wszystkie dane skoroszytu do pliku
Na koniec, po połączeniu wszystkich danych w naszym `workbookData` tablicę, możemy zapisać tę tablicę w określonej ścieżce pliku.
```csharp
// Zapisz całe dane skoroszytu do pliku
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` pobiera połączoną tablicę bajtów i zapisuje ją do pliku tekstowego o nazwie „out.txt” w określonym katalogu.
## Wniosek
I masz! Udało Ci się przekonwertować skoroszyt programu Excel do formatu CSV przy użyciu Aspose.Cells dla .NET. Ten proces jest nie tylko wydajny, ale umożliwia łatwą manipulację danymi programu Excel w celu dalszej analizy lub raportowania. Teraz możesz zautomatyzować zadania przetwarzania danych lub nawet zintegrować tę funkcjonalność z większymi aplikacjami.
## Najczęściej zadawane pytania
### Czy mogę użyć różnych ograniczników w pliku CSV?
Tak, możesz zmienić `opts.Separator` do dowolnego znaku, np. przecinka lub pionowej kreski.
### Czy korzystanie z Aspose.Cells jest bezpłatne?
Aspose.Cells nie jest darmowy, ale możesz skorzystać z bezpłatnej wersji próbnej [Tutaj](https://releases.aspose.com/).
### W jakich formatach oprócz CSV mogę zapisywać pliki?
Aspose.Cells pozwala na zapisywanie w wielu formatach, w tym XLSX, PDF i innych.
### Czy mogę przetwarzać duże pliki Excela za pomocą Aspose.Cells?
Tak, Aspose.Cells został zaprojektowany do wydajnej obsługi dużych plików, ale wydajność może zależeć od zasobów systemowych.
### Gdzie mogę znaleźć bardziej szczegółową dokumentację?
Pełną dokumentację i przykłady można znaleźć na ich stronie [miejsce odniesienia](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}