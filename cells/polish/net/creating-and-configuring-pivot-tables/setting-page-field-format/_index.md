---
title: Ustawianie formatu pola strony programowo w .NET
linktitle: Ustawianie formatu pola strony programowo w .NET
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak programowo ustawić formaty pól stron w tabelach przestawnych przy użyciu Aspose.Cells dla .NET. Postępuj zgodnie z naszym samouczkiem krok po kroku, aby płynnie zarządzać danymi.
weight: 21
url: /pl/net/creating-and-configuring-pivot-tables/setting-page-field-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ustawianie formatu pola strony programowo w .NET

## Wstęp
Tworzenie i manipulowanie plikami Excela za pomocą kodu może być bardzo pomocne, zwłaszcza gdy trzeba analizować duże zbiory danych. Jednym z fantastycznych narzędzi w Twoim arsenale jest Aspose.Cells dla .NET, który umożliwia programową interakcję z plikami Excela i tworzenie złożonych struktur raportowania. W tym samouczku zagłębimy się w to, jak możesz skonfigurować formaty pól stron w tabeli przestawnej za pomocą tej potężnej biblioteki. Niezależnie od tego, czy jesteś doświadczonym programistą, czy początkującym, pod koniec tego przewodnika będziesz mieć solidne pojęcie o tym, jak obsługiwać tabele przestawne i ich różne ustawienia w .NET.
## Wymagania wstępne
Zanim zaczniemy kodować, upewnijmy się, że wszystko jest poprawnie skonfigurowane. Będziesz potrzebować następujących rzeczy:
- Visual Studio: środowisko robocze, w którym można pisać i wykonywać kod .NET.
-  Aspose.Cells: Możesz pobrać bibliotekę[Tutaj](https://releases.aspose.com/cells/net/).
- Podstawowa wiedza o języku C#: Znajomość programowania w języku C# pomoże Ci lepiej zrozumieć fragmenty kodu.
-  Plik Excela: Przygotuj plik Excela (np.`Book1.xls`) zawierający dane nadające się do utworzenia tabeli przestawnej. 
 Jeśli jeszcze tego nie zrobiłeś, pobierz bezpłatną wersję próbną Aspose.Cells[Tutaj](https://releases.aspose.com/).
## Importuj pakiety
Aby zacząć, musisz zaimportować odpowiednie pakiety do swojego projektu. Zacznij od dodania odniesień do biblioteki Aspose.Cells w swoim projekcie C#. Oto, jak to zrobić:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Spowoduje to pobranie wszystkich niezbędnych klas i metod potrzebnych do manipulowania plikami Excela za pomocą Aspose.Cells.
## Krok 1: Skonfiguruj swoje miejsce pracy
Zacznij od zdefiniowania katalogu roboczego, w którym będą przechowywane pliki Excela. Na przykład możesz zadeklarować zmienną w następujący sposób:
```csharp
string dataDir = "Your Document Directory";
```
## Ładowanie skoroszytu
Następnie musimy załadować nasz szablon Excela. Jest to niezbędny krok, ponieważ ustala kontekst dla naszych operacji:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Ten wiersz ładuje istniejący skoroszyt ze wskazanego katalogu.
## Krok 2: Uzyskaj dostęp do arkusza kalkulacyjnego
Gdy skoroszyt zostanie załadowany, czas uzyskać dostęp do arkusza zawierającego tabelę przestawną lub dane, które chcesz przeanalizować. Oto, jak to zrobić:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
To pobiera pierwszy arkusz załadowanego skoroszytu. Możesz łatwo zmodyfikować indeks, jeśli pracujesz z wieloma arkuszami.
## Krok 3: Dostęp do tabeli przestawnej
 Kontynuując, uzyskajmy dostęp do tabeli przestawnej w wybranym arkuszu. Jeśli używasz pojedynczej tabeli przestawnej, możesz ustawić jej indeks na`0`:
```csharp
int pivotindex = 0;
// Dostęp do tabeli przestawnej
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
Ten fragment kodu wybiera pierwszą tabelę przestawną w arkuszu kalkulacyjnym. 
## Krok 4: Konfigurowanie tabeli przestawnej
Teraz nadchodzi ekscytująca część! Ustawmy tabelę przestawną tak, aby pokazywała sumy całkowite dla wierszy:
```csharp
pivotTable.RowGrand = true;
```
Ten wiersz zapewnia, że w raporcie będą wyświetlane sumy całkowite, co może być przydatnym podsumowaniem przy analizie danych.
## Krok 5: Dostęp i konfiguracja pól wierszy
Następnie musimy uzyskać dostęp do pól wierszy tabeli przestawnej:
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
Kolekcja ta umożliwia nam manipulowanie polami według potrzeb.
## Skonfiguruj pole pierwszego wiersza
Chcesz ustawić konkretne typy sum częściowych? Uzyskajmy dostęp do pierwszego pola w naszej kolekcji i skonfigurujmy je:
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// Ustawianie sum częściowych.
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
 Włączając`Sum` I`Count` sumy częściowe pozwalają nam szybko podsumować dane w naszym raporcie.
## Krok 6: Ustawianie opcji automatycznego sortowania
Następnie wprowadźmy trochę inteligentnego sortowania. W ten sposób Twoja tabela przestawna uporządkuje dane w sensownym porządku:
```csharp
// Ustawianie opcji automatycznego sortowania.
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // Korzystanie z predefiniowanego pola sortowania.
```
Ten fragment kodu włącza automatyczne sortowanie i określa kolejność rosnącą. 
## Krok 7: Ustawianie opcji automatycznego wyświetlania
Czy chcesz dalej filtrować swoje dane? Opcja AutoShow jest pomocna w pokazywaniu konkretnych punktów danych w określonych warunkach:
```csharp
// Ustawianie opcji automatycznego wyświetlania.
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // Określ pole, które ma być wyświetlane automatycznie.
```
Dzięki temu masz pewność, że tabela przestawna wyświetla wyłącznie istotne dane, co zwiększa jej przejrzystość i skuteczność.
## Krok 8: Zapisywanie swojej pracy
Po wszystkich tych konfiguracjach nie chciałbyś stracić swojej pracy! Zapisz zmodyfikowany skoroszyt w ten sposób:
```csharp
workbook.Save(dataDir + "output.xls");
```
Teraz możesz znaleźć nowo utworzony plik Excela w katalogu dokumentów.
## Wniosek
I masz to! Przeszliśmy przez kompleksowe i praktyczne podejście do ustawiania formatów pól stron programowo w tabeli przestawnej przy użyciu Aspose.Cells dla .NET. Dzięki prostym krokom powinieneś czuć się pewnie, modyfikując dane w programie Excel, aby odpowiadały Twoim potrzebom w zakresie raportowania. To niesamowite, co możesz osiągnąć, łącząc moc języka C# z Aspose.Cells.
## Najczęściej zadawane pytania
### Czym jest Aspose.Cells?
Aspose.Cells to biblioteka .NET umożliwiająca programistom programowe tworzenie, edytowanie i konwertowanie plików Excel.
### Jak zainstalować Aspose.Cells?
 Można go pobrać bezpośrednio ze strony[Strona internetowa Aspose](https://releases.aspose.com/cells/net/).
### Czy mogę używać Aspose.Cells bez instalacji programu Excel?
Tak, Aspose.Cells jest samodzielną biblioteką, która nie wymaga instalacji programu Microsoft Excel.
### Gdzie mogę znaleźć szczegółową pomoc?
 Szczegółową pomoc techniczną i fora można uzyskać pod adresem[Wsparcie Aspose](https://forum.aspose.com/c/cells/9).
### Jak mogę uzyskać tymczasową licencję?
 Możesz nabyć tymczasową licencję od[Tutaj](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
