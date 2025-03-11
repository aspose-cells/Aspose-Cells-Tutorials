---
title: Programowe używanie metody kopiowania w programie Excel
linktitle: Programowe używanie metody kopiowania w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak używać metody kopiowania w Aspose.Cells dla .NET, aby efektywnie manipulować plikami Excel. Zawiera przewodnik krok po kroku.
weight: 10
url: /pl/net/excel-formatting-methods-and-options/using-copy-method/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programowe używanie metody kopiowania w programie Excel

## Wstęp
Jeśli chodzi o programowe zarządzanie arkuszami kalkulacyjnymi i manipulowanie nimi, Aspose.Cells dla .NET to potęga, która może zaoszczędzić Ci czasu i usprawnić przepływ pracy. Jednym z typowych zadań, z jakimi mierzą się programiści, jest konieczność kopiowania zakresów z jednego arkusza kalkulacyjnego do drugiego w skoroszycie programu Excel. W tym samouczku przeprowadzimy Cię przez metodę Copy w Aspose.Cells, prowadząc Cię przez każdy krok za pomocą jasnych wyjaśnień i przykładów kodu.
## Wymagania wstępne
Zanim przejdziemy do szczegółów korzystania z metody Kopiuj, musisz upewnić się, że spełnione są następujące wymagania wstępne:
1. .NET Framework: Upewnij się, że na Twoim komputerze jest zainstalowany .NET Framework. Aspose.Cells jest kompatybilny z różnymi wersjami, więc sprawdź ich[dokumentacja](https://reference.aspose.com/cells/net/) po szczegóły.
2. Visual Studio: Posiadanie Visual Studio lub dowolnego kompatybilnego środowiska IDE skonfigurowanego do rozwoju .NET jest niezbędne. Pomoże Ci to wygodnie tworzyć i zarządzać projektami.
3.  Biblioteka Aspose.Cells: Pobierz bibliotekę Aspose.Cells z[strona wydań](https://releases.aspose.com/cells/net/) i dodaj do niego odniesienie w swoim projekcie.
4.  Przykładowy plik programu Excel: Utwórz lub przygotuj plik programu Excel (np.`Book1.xlsx`) z którymi będziesz pracować w tym samouczku.
5. Podstawowa wiedza o języku C#: Znajomość pojęć i składni języka C#.
Gdy spełnisz te wymagania wstępne, będziesz gotowy, aby rozpocząć kodowanie!
## Importuj pakiety
Aby skorzystać z funkcjonalności udostępnianych przez Aspose.Cells, musisz zaimportować niezbędne pakiety. W swoim projekcie C# upewnij się, że na początku pliku kodu dołączono następującą dyrektywę using:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Dzięki temu można uzyskać dostęp do klas i metod wymaganych do łatwego manipulowania plikami Excela.
Teraz, gdy wszystko jest już gotowe, podzielmy proces korzystania z metody Kopiuj na łatwe do opanowania kroki. Zaczniemy od załadowania pliku Excel, a następnie przejdziemy do skopiowania żądanego zakresu.
## Krok 1: Konfigurowanie strumienia plików
Pierwszym krokiem jest utworzenie strumienia plików, który pozwoli nam otworzyć i pracować z naszym plikiem Excel. Oto jak to zrobić:
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
// Tworzenie strumienia plików zawierającego plik Excela do otwarcia
FileStream fstream = new FileStream(dataDir + "Book1.xlsx", FileMode.Open);
```
 W tym kodzie musisz określić ścieżkę, w której znajduje się Twój`Book1.xlsx` plik jest zlokalizowany.`FileMode.Open` Parametr wskazuje, że chcemy otworzyć istniejący plik.
## Krok 2: Otwieranie skoroszytu
Następnie utworzymy obiekt Workbook, używając strumienia plików, który właśnie skonfigurowaliśmy. Daje nam to dostęp do zawartości pliku Excel.
```csharp
// Otwieranie pliku Excel za pomocą strumienia plików
Workbook workbook = new Workbook(fstream);
```
W tym momencie otworzyliśmy skoroszyt i możemy zacząć pracować z jego zawartością.
## Krok 3: Dostęp do arkusza kalkulacyjnego
Po załadowaniu skoroszytu musimy uzyskać dostęp do konkretnego arkusza, z którym chcemy pracować. Zazwyczaj będzie to pierwszy arkusz w skoroszycie.
```csharp
// Dostęp do pierwszego arkusza kalkulacyjnego w pliku Excel
Worksheet worksheet = workbook.Worksheets[0];
```
 Tutaj,`Worksheets[0]` chwyta pierwszy arkusz. Jeśli chcesz uzyskać dostęp do innego arkusza, po prostu zmień indeks.
## Krok 4: Kopiowanie zakresu
Teraz nadchodzi główna część — kopiowanie zakresu komórek. W tym samouczku pokażemy, jak kopiować ustawienia formatowania warunkowego z jednej komórki do drugiej, a także jak kopiować cały zakres arkusza Excela.
### Kopiowanie formatowania warunkowego (przykład)
```csharp
// Kopiowanie ustawień formatowania warunkowego z komórki „A1” do komórki „B1”
// arkusz kalkulacyjny.KopiujFormatowanieWarunkowe(0, 0, 0, 1);
```
Ten wiersz jest zakomentowany w oryginalnym kodzie, ale pokazuje, jak skopiować formatowanie warunkowe z komórki A1 do komórki B1 na tym samym arkuszu kalkulacyjnym. Parametry reprezentują indeksy wierszy i kolumn komórek źródłowych i docelowych. Możesz odkomentować, jeśli ta funkcjonalność jest potrzebna.
### Kopiowanie całego zakresu (przykład)
Możemy rozszerzyć funkcjonalność kopiowania, tak aby obejmowała kopiowanie całego zakresu. W tym celu użyjemy pętli, aby przejść przez wszystkie arkusze kalkulacyjne.
```csharp
int TotalRowCount = 0;
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    // Dostęp do każdego arkusza kalkulacyjnego
    Worksheet sourceSheet = workbook.Worksheets[i];
    // Uzyskiwanie zakresu wyświetlania w arkuszu kalkulacyjnym
    Range sourceRange = sourceSheet.Cells.MaxDisplayRange;
    // Tworzenie zakresu w arkuszu docelowym
    Range destRange = worksheet.Cells.CreateRange(
        sourceRange.FirstRow + TotalRowCount,
        sourceRange.FirstColumn,
        sourceRange.RowCount,
        sourceRange.ColumnCount);
    // Kopiowanie zakresu źródłowego do zakresu docelowego
    destRange.Copy(sourceRange);
    // Aktualizacja całkowitej liczby wierszy dla następnej iteracji pętli
    TotalRowCount += sourceRange.RowCount; 
}
```
## Krok 5: Zapisywanie zmodyfikowanego skoroszytu
Po skopiowaniu wymaganych zakresów, będziesz chciał zapisać zmodyfikowany skoroszyt, aby zachować zmiany. Oto jak to zrobić:
```csharp
// Zapisywanie zmodyfikowanego pliku Excel
workbook.Save(dataDir + "output.xls");
```
 Ten kod zapisze zmodyfikowany skoroszyt jako`output.xls` w podanym przez Ciebie katalogu. Upewnij się, że wybierzesz odpowiedni format, który odpowiada Twoim potrzebom. 
## Krok 6: Zamykanie strumienia plików
Na koniec, aby mieć pewność, że zasoby systemowe są wolne, musimy zamknąć początkowo otwarty strumień plików.
```csharp
// Zamknięcie strumienia plików w celu zwolnienia wszystkich zasobów
fstream.Close();
```
w ten sposób udało Ci się pomyślnie ukończyć proces kopiowania zakresów i zapisywania zaktualizowanego pliku Excel!
## Wniosek
Użycie metody Kopiuj w Aspose.Cells dla .NET daje Ci potężne możliwości łatwego manipulowania plikami Excel. Postępując zgodnie z tym przewodnikiem krok po kroku, możesz skutecznie kopiować zakresy komórek i formatowanie warunkowe z jednego arkusza kalkulacyjnego do drugiego, usprawniając zadania zarządzania danymi. 
## Najczęściej zadawane pytania
### Czym jest Aspose.Cells dla .NET?
Aspose.Cells for .NET to biblioteka umożliwiająca programistom tworzenie, modyfikowanie i zarządzanie plikami Excela programowo w aplikacjach .NET.
### Czy mogę kopiować formaty, formuły i wartości za pomocą Aspose.Cells?
Tak, Aspose.Cells pozwala na kopiowanie nie tylko wartości, ale także formatów i formuł pomiędzy zakresami.
### Czy korzystanie z Aspose.Cells jest bezpłatne?
 Aspose.Cells oferuje bezpłatną wersję próbną, ale do dalszego korzystania należy zakupić licencję. Więcej informacji można znaleźć[Tutaj](https://purchase.aspose.com/buy).
### Jak mogę uzyskać pomoc, jeśli napotkam problemy?
 Pomocy możesz szukać na forum pomocy technicznej Aspose, które znajdziesz[Tutaj](https://forum.aspose.com/c/cells/9).
### Gdzie mogę pobrać bibliotekę Aspose.Cells?
 Bibliotekę można pobrać ze strony z wydaniami[Tutaj](https://releases.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
