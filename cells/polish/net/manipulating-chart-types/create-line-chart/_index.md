---
title: Utwórz wykres liniowy
linktitle: Utwórz wykres liniowy
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Twórz oszałamiające wykresy liniowe za pomocą Aspose.Cells dla .NET. Postępuj zgodnie z naszym przewodnikiem krok po kroku, aby skutecznie wizualizować swoje dane.
weight: 11
url: /pl/net/manipulating-chart-types/create-line-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz wykres liniowy

## Wstęp

Czy jesteś gotowy, aby wizualizować swoje dane w oszałamiającej przejrzystości? Wykresy liniowe to fantastyczny sposób na wyświetlanie trendów w czasie lub relacji między dwiema zmiennymi. Niezależnie od tego, czy zarządzasz danymi dla projektu biznesowego, czy analizujesz osobiste wskaźniki, możliwość tworzenia wykresów liniowych programowo może zaoszczędzić Ci czasu i zapewnić większą elastyczność. W tym przewodniku przeprowadzimy Cię przez każdy etap tworzenia wykresu liniowego przy użyciu Aspose.Cells dla .NET. Gotowy do działania? Zaczynajmy!

## Wymagania wstępne

Zanim przejdziemy do szczegółów tworzenia wykresu liniowego, upewnijmy się, że potrafisz to zrobić:

1. Visual Studio: Upewnij się, że na Twoim komputerze jest zainstalowany program Visual Studio, ponieważ jest to jedno z najpopularniejszych środowisk IDE do tworzenia aplikacji .NET.
2.  Biblioteka Aspose.Cells dla .NET: Będziesz potrzebować biblioteki Aspose.Cells, którą możesz pobrać ze strony[Tutaj](https://releases.aspose.com/cells/net/).
3. Podstawowa znajomość języka C#: Znajomość języka programowania C# pomoże Ci lepiej zrozumieć przykłady i fragmenty kodu.
4. .NET Framework lub .NET Core: podstawowa konfiguracja dowolnego z tych środowisk, ponieważ będzie ono stanowić podstawę naszych aplikacji.

Gdy już spełnisz te wymagania wstępne, będziesz gotowy, aby stworzyć wykresy!

## Importuj pakiety

Teraz, gdy skonfigurowaliśmy nasze środowisko, musimy zaimportować niezbędne pakiety do naszego kodu C#. Podobnie jak zbierasz swoje narzędzia przed rozpoczęciem projektu, importowanie pakietów jest niezbędne, aby mieć pewność, że masz wszystko, czego potrzebujesz.

Oto jak to zrobić:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

 Ta linia importuje`Aspose.Cells` przestrzeń nazw, która zawiera wszystkie klasy i metody, których użyjemy do utworzenia naszego wykresu liniowego.

Teraz rozbijmy cały proces na proste, przyswajalne kroki. Każdy krok poprowadzi Cię przez logiczny przepływ tworzenia wykresu liniowego przy użyciu Aspose.Cells dla .NET.

## Krok 1: Skonfiguruj katalog wyjściowy

Pierwszym krokiem jest określenie, gdzie chcesz zapisać plik wyjściowy. To jak skonfigurowanie przestrzeni roboczej przed rozpoczęciem pracy. 

```csharp
// Katalog wyjściowy
string outputDir = "Your Output Directory";
```
 Zastępować`"Your Output Directory"` rzeczywistą ścieżką, pod którą chcesz zapisać wygenerowany plik Excela.

## Krok 2: Utwórz obiekt skoroszytu

Następnie musimy utworzyć nową instancję skoroszytu. Pomyśl o skoroszycie jako o płótnie, na którym będzie płynąć Twoja kreatywność. 

```csharp
// Tworzenie instancji obiektu skoroszytu
Workbook workbook = new Workbook();
```
Ten wiersz inicjuje nowy skoroszyt, który będzie zawierał wszystkie dane i elementy wizualne.

## Krok 3: Uzyskaj dostęp do arkusza kalkulacyjnego

W naszym nowo utworzonym skoroszycie musimy uzyskać odniesienie do arkusza, w którym wprowadzimy nasze dane. Jeśli skoroszyt jest naszym płótnem, to arkusz jest naszą paletą.

```csharp
// Uzyskanie odniesienia do nowo dodanego arkusza roboczego poprzez podanie indeksu arkusza
Worksheet worksheet = workbook.Worksheets[0];
```
 Tutaj uzyskujemy dostęp do pierwszego arkusza kalkulacyjnego (indeks`0`).

## Krok 4: Dodaj wartości przykładowe do komórek

Teraz zaczyna się zabawa! Wprowadzimy kilka przykładowych wartości do naszego arkusza kalkulacyjnego. Te dane będą stanowić podstawę naszego wykresu liniowego. 

```csharp
// Dodawanie wartości próbek do komórek
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
W tym fragmencie kodu dodajemy wartości do komórek w kolumnach A i B. Kolumna A reprezentuje wartości osi X, natomiast kolumna B reprezentuje wartości osi Y.

## Krok 5: Dodaj wykres liniowy do arkusza kalkulacyjnego

Następnie wprowadzimy do arkusza wykres liniowy. To tutaj Twoje dane naprawdę ożyją!

```csharp
// Dodawanie wykresu do arkusza kalkulacyjnego
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Line, 5, 0, 25, 10);
```
Tutaj dodajemy wykres liniowy w określonym miejscu. Parametry (5, 0, 25, 10) definiują pozycję i rozmiar wykresu w arkuszu kalkulacyjnym.

## Krok 6: Uzyskaj dostęp do nowej instancji wykresu

Gdy dodamy już wykres, czas zająć się nowo utworzonym obiektem wykresu. 

```csharp
// Uzyskiwanie dostępu do wystąpienia nowo dodanego wykresu
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```
Kod ten łączy nas z wykresem, dzięki czemu możemy go dalej modyfikować.

## Krok 7: Dodaj SeriesCollection do wykresu

Teraz musimy powiedzieć naszemu wykresowi, jakie dane wyświetlić. Tutaj definiujemy źródło danych dla naszego wykresu liniowego, dodając SeriesCollection.

```csharp
// Dodawanie SeriesCollection (źródło danych wykresu) do wykresu w zakresie od komórki „A1” do „B3”
chart.NSeries.Add("A1:B3", true);
```
W tym przykładzie informujemy wykres, aby użył wartości w komórkach od A1 do B3.

## Krok 8: Zapisz plik Excel

Wielki finał! Po całej ciężkiej pracy czas zapisać plik Excela i zobaczyć wykres liniowy w akcji.

```csharp
// Zapisywanie pliku Excel
workbook.Save(outputDir + "outputHowToCreateLineChart.xlsx");
```
 Ten wiersz zapisuje skoroszyt w określonym katalogu wyjściowym pod nazwą`outputHowToCreateLineChart.xlsx`.

## Krok 9: Wykonaj i zweryfikuj

Na koniec możesz uruchomić swój kod i sprawdzić, czy wykres liniowy został pomyślnie utworzony w katalogu wyjściowym! 

```csharp
Console.WriteLine("HowToCreateLineChart executed successfully.");
```
Spowoduje to wyświetlenie komunikatu na konsoli informującego, że wszystko przebiegło prawidłowo.

## Wniosek

Tworzenie wykresu liniowego przy użyciu Aspose.Cells dla .NET to wydajny sposób na ożywienie danych. Postępując zgodnie z tym przewodnikiem krok po kroku, możesz łatwo wizualizować trendy i relacje w swoich zestawach danych. Niezależnie od tego, czy jesteś doświadczonym programistą, czy dopiero zaczynasz, Aspose.Cells zapewnia elastyczność i moc automatyzacji zadań wizualizacji danych. 

## Najczęściej zadawane pytania

### Czym jest Aspose.Cells dla .NET?  
Aspose.Cells for .NET to zaawansowana biblioteka przeznaczona do programowego zarządzania plikami Excela i manipulowania nimi. Umożliwia ona programistom tworzenie, edycję i konwersję arkuszy kalkulacyjnych.

### Czy Aspose.Cells obsługuje wykresy?  
Tak, Aspose.Cells zapewnia rozbudowaną obsługę różnych typów wykresów, w tym wykresów liniowych, kołowych, słupkowych i innych.

### Czy mogę używać Aspose.Cells za darmo?  
Tak, możesz pobrać bezpłatną wersję próbną, aby poznać jej funkcje. Do długoterminowego użytkowania rozważ zakup licencji.

### Czy istnieje forum wsparcia?  
 Oczywiście! Odpowiedzi i pytania znajdziesz na[Forum Aspose.Cells](https://forum.aspose.com/c/cells/9).

### Jak kupić licencję?  
 Licencje można łatwo nabyć za pośrednictwem[strona zakupu](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
