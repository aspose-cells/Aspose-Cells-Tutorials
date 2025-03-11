---
title: Zapisywanie tabeli przestawnej w formacie ODS programowo w .NET
linktitle: Zapisywanie tabeli przestawnej w formacie ODS programowo w .NET
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak zapisywać tabele przestawne w formacie ODS przy użyciu Aspose.Cells dla .NET, korzystając z tego przewodnika krok po kroku.
weight: 25
url: /pl/net/creating-and-configuring-pivot-tables/saving-in-ods-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zapisywanie tabeli przestawnej w formacie ODS programowo w .NET

## Wstęp
Jeśli chodzi o zarządzanie danymi w arkuszach kalkulacyjnych, nic nie dorównuje mocy tabel przestawnych. Są one narzędziem do podsumowywania, analizowania i prezentowania złożonych zestawów danych. Dzisiaj zagłębimy się w używanie Aspose.Cells dla .NET do zapisywania tabeli przestawnej w formacie ODS. Niezależnie od tego, czy jesteś doświadczonym programistą, czy dopiero zaczynasz przygodę z .NET, ten przewodnik okaże się dla Ciebie przejrzysty. 
Zaczynajmy!
## Wymagania wstępne
Zanim przejdziemy do kodu, jest kilka niezbędnych rzeczy, których będziesz potrzebować:
### 1. Podstawowa wiedza o .NET
Podstawowa znajomość platformy .NET i jej koncepcji programowania ułatwi Ci naukę.
### 2. Aspose.Cells dla .NET
 Musisz mieć zainstalowany Aspose.Cells dla .NET. Możesz go pobrać ze strony[Strona wydań Aspose](https://releases.aspose.com/cells/net/) . Dostępna jest również wersja próbna[Tutaj](https://releases.aspose.com/).
### 3. Środowisko programistyczne
Upewnij się, że masz środowisko IDE, takie jak Visual Studio, w którym możesz pisać i testować kod .NET.
### 4. Trochę cierpliwości
Jak w przypadku każdego przedsięwzięcia związanego z kodowaniem, cierpliwość jest kluczowa. Nie martw się, jeśli coś nie działa idealnie za pierwszym razem; debugowanie jest częścią procesu.
## Importuj pakiety
Aby pracować z Aspose.Cells, musisz zaimportować niezbędne przestrzenie nazw. Dodaj następującą dyrektywę using na początku pliku kodu:
```csharp
using System;
using Aspose.Cells.Pivot;
```
Ten wiersz umożliwia dostęp do wszystkich funkcjonalności biblioteki Aspose.Cells, dzięki czemu proces kodowania staje się niezwykle prosty.
Teraz podzielimy ten proces na łatwiejsze do opanowania kroki.
## Krok 1: Skonfiguruj swój katalog wyjściowy
Najpierw musisz zdefiniować, gdzie chcesz zapisać plik ODS. Jest to proste przypisanie ścieżki katalogu.
```csharp
string outputDir = "Your Document Directory";
```
 W tym wierszu zamień`"Your Document Directory"` ze ścieżką, pod którą chcesz zapisać plik.
## Krok 2: Utwórz nowy skoroszyt
Następnie utworzysz nowy obiekt Skoroszyt, który będzie zawierał wszystkie dane i struktury, łącznie z tabelą przestawną.
```csharp
Workbook workbook = new Workbook();
```
Tutaj zaczynasz po prostu od nowa – pomyśl o tym jak o pustym płótnie, na którym stworzysz swoje arcydzieło.
## Krok 3: Uzyskaj dostęp do arkusza kalkulacyjnego
Teraz, gdy mamy nasz skoroszyt, musimy zacząć pracę nad naszym arkuszem. Aspose.Cells pozwala na łatwy dostęp do pierwszego dostępnego arkusza.
```csharp
Worksheet sheet = workbook.Worksheets[0];
```
Ten wiersz przenosi nas do pierwszego arkusza, gotowego do wprowadzania danych.
## Krok 4: Wypełnij komórki danymi
Czas wypełnić nasz arkusz danymi. Użyjemy prostego przykładu danych sprzedaży sportowej. 
Oto jak można ustawić wartości w różnych komórkach:
```csharp
Cells cells = sheet.Cells;
cells["A1"].PutValue("Sport");
cells["B1"].PutValue("Quarter");
cells["C1"].PutValue("Sales");
cells["A2"].PutValue("Golf");
cells["A3"].PutValue("Golf");
cells["A4"].PutValue("Tennis");
cells["A5"].PutValue("Tennis");
cells["A6"].PutValue("Tennis");
cells["A7"].PutValue("Tennis");
cells["A8"].PutValue("Golf");
cells["B2"].PutValue("Qtr3");
cells["B3"].PutValue("Qtr4");
cells["B4"].PutValue("Qtr3");
cells["B5"].PutValue("Qtr4");
cells["B6"].PutValue("Qtr3");
cells["B7"].PutValue("Qtr4");
cells["B8"].PutValue("Qtr3");
cells["C2"].PutValue(1500);
cells["C3"].PutValue(2000);
cells["C4"].PutValue(600);
cells["C5"].PutValue(1500);
cells["C6"].PutValue(4070);
cells["C7"].PutValue(5000);
cells["C8"].PutValue(6430);
```
W tych wierszach definiujemy nagłówki i wypełniamy dane sprzedażowe. Pomyśl o tym kroku jak o zapełnianiu spiżarni przed ugotowaniem posiłku; im lepsze składniki (dane), tym lepszy posiłek (analiza).
## Krok 5: Utwórz tabelę przestawną
Teraz nadchodzi zabawna część — tworzenie tabeli przestawnej! Oto jak dodać ją do arkusza kalkulacyjnego:
```csharp
PivotTableCollection pivotTables = sheet.PivotTables;
// Dodawanie tabeli przestawnej do arkusza kalkulacyjnego
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```
 W tym fragmencie kodu określamy zakres danych dla tabeli przestawnej i miejsce jej umieszczenia w arkuszu. Zakres danych`=A1:C8` obejmuje obszar, na którym znajdują się nasze dane.
## Krok 6: Dostosuj swoją tabelę przestawną
Następnie będziesz chciał dostosować swoją tabelę przestawną do swoich potrzeb. Wiąże się to z kontrolowaniem tego, co jest wyświetlane, jak jest kategoryzowane i jak oblicza dane.
```csharp
PivotTable pivotTable = pivotTables[index];
// Niewyświetlanie sum całkowitych dla wierszy.
pivotTable.RowGrand = false;
// Przeciąganie pierwszego pola do obszaru wiersza.
pivotTable.AddFieldToArea(PivotFieldType.Row, 0);
// Przeciągnij drugie pole do obszaru kolumny.
pivotTable.AddFieldToArea(PivotFieldType.Column, 1);
// Przeciąganie trzeciego pola do obszaru danych.
pivotTable.AddFieldToArea(PivotFieldType.Data, 2);
pivotTable.CalculateData();
```
Tutaj decydujesz, które pola danych podsumować i jak powinny być reprezentowane. To jak nakrywanie stołu na przyjęcie; decydujesz, co pasuje najlepiej i jak to przedstawić.
## Krok 7: Zapisz swój skoroszyt
Na koniec jesteś gotowy, aby zapisać swoją pracę w pożądanym formacie ODS. Oto, jak to zrobić:
```csharp
workbook.Save(outputDir + "PivotTableSaveInODS_out.ods");
```
Na tym etapie kończysz projekt i zabezpieczasz go w wybranym katalogu — to satysfakcjonujące zakończenie!
## Krok 8: Zweryfikuj swoje dane wyjściowe
Na koniec, zawsze dobrym pomysłem jest sprawdzenie, czy proces zakończył się pomyślnie. Możesz dodać prosty komunikat konsoli:
```csharp
Console.WriteLine("PivotTableSaveInODS executed successfully.");
```
Ta wiadomość pojawi się na Twojej konsoli, aby potwierdzić, że wszystko poszło bez problemów. Tak jak szef kuchni sprawdzający, czy wszystko jest ugotowane perfekcyjnie przed podaniem!
## Wniosek 
masz to! Nie tylko utworzyłeś tabelę przestawną za pomocą Aspose.Cells, ale także zapisałeś ją w formacie ODS. Ten przewodnik przeprowadzi Cię przez każdy krok, zapewniając, że jesteś uzbrojony w wiedzę i pewność siebie, aby zająć się podobnymi zadaniami w przyszłości.
## Najczęściej zadawane pytania
### Czym jest Aspose.Cells?
Aspose.Cells to zaawansowana biblioteka umożliwiająca tworzenie i manipulowanie plikami Excela w aplikacjach .NET.
### Czy mogę używać Aspose.Cells za darmo?
 Tak, możesz pobrać bezpłatną wersję próbną ze strony[Strona internetowa Aspose](https://releases.aspose.com/).
### Jakie formaty obsługuje Aspose.Cells?
Obsługuje wiele formatów, w tym XLSX, XLS, ODS, PDF i wiele innych.
### Jak uzyskać pomoc techniczną dotyczącą Aspose.Cells?
 Pomoc można znaleźć na[Forum wsparcia Aspose](https://forum.aspose.com/c/cells/9).
### Czy jest dostępna licencja tymczasowa?
 Tak, możesz ubiegać się o tymczasową licencję za pośrednictwem witryny Aspose[Tutaj](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
