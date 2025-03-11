---
title: Otwieranie plików CSV za pomocą preferowanego parsera
linktitle: Otwieranie plików CSV za pomocą preferowanego parsera
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak otwierać i analizować pliki CSV za pomocą niestandardowych parserów w Aspose.Cells dla .NET. Bezproblemowo obsługuj tekst i daty. Idealne dla programistów.
weight: 11
url: /pl/net/csv-file-handling/csv-file-opening-csv-files-with-preferred-parser/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Otwieranie plików CSV za pomocą preferowanego parsera

## Wstęp
Podczas pracy z plikami CSV czasami chcesz obsługiwać różne typy danych za pomocą niestandardowych parserów. Ten samouczek pokaże Ci, jak otwierać pliki CSV za pomocą preferowanego parsera przy użyciu Aspose.Cells dla .NET. Niezależnie od tego, czy chcesz obsługiwać tekst, daty czy inne niestandardowe formaty, ten przewodnik przeprowadzi Cię przez każdy krok z jasnym wyjaśnieniem.
## Wymagania wstępne
Zanim zagłębimy się w kod, omówmy podstawowe elementy potrzebne do rozpoczęcia pracy.
1.  Aspose.Cells for .NET Library: Upewnij się, że masz zainstalowaną bibliotekę Aspose.Cells. Możesz ją pobrać[Tutaj](https://releases.aspose.com/cells/net/) . Możesz również skorzystać z bezpłatnej wersji próbnej[Tutaj](https://releases.aspose.com/).
2. Środowisko programistyczne .NET: zalecany jest program Visual Studio, ale sprawdzi się każde środowisko IDE zgodne z platformą .NET.
3. Podstawowa wiedza o języku C#: W tym samouczku zakładamy, że znasz język C# i programowanie obiektowe.
## Importuj pakiety
Aby użyć Aspose.Cells, musisz zaimportować niezbędne przestrzenie nazw na górze pliku C#:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Teraz, gdy już omówiliśmy podstawy, pokażemy, jak otworzyć plik CSV przy użyciu preferowanego parsera obsługującego różne formaty danych, takie jak tekst i daty.
## Krok 1: Zdefiniuj niestandardowe parsery
 Aby obsługiwać różne typy danych, takie jak tekst lub określone formaty dat, należy zdefiniować niestandardowe parsery. W Aspose.Cells niestandardowe parsery implementują`ICustomParser` interfejs.
### 1.1 Utwórz parser tekstu
Ten parser obsługuje zwykłe wartości tekstowe. Nie modyfikuje formatu, więc wartość jest zwracana taka, jaka jest.
```csharp
class TextParser : ICustomParser
{
    public object ParseObject(string value)
    {
        return value;
    }
    public string GetFormat()
    {
        return "";
    }
}
```
 Ten`ParseObject` Metoda po prostu zwraca wartość wejściową. To tak, jakby powiedzieć: „Nic nie zmieniaj, po prostu daj mi tekst!”
### 1.2 Utwórz parser dat
 W przypadku dat należy upewnić się, że dane w pliku CSV są poprawnie przetwarzane`DateTime` obiekty. Oto jak możesz utworzyć parser dat:
```csharp
class DateParser : ICustomParser
{
    public object ParseObject(string value)
    {
        DateTime myDate = DateTime.ParseExact(value, "dd/MM/yyyy", 
            System.Globalization.CultureInfo.InvariantCulture);
        return myDate;
    }
    public string GetFormat()
    {
        return "dd/MM/yyyy";
    }
}
```
 W tym parserze używamy`ParseExact` aby zapewnić prawidłową interpretację daty na podstawie wstępnie zdefiniowanego formatu (`"dd/MM/yyyy"`). W ten sposób każda data w pliku CSV zgodna z tym formatem zostanie przetworzona bez problemów.
## Krok 2: Skonfiguruj opcje ładowania
 Następnie należy skonfigurować sposób ładowania pliku CSV. Można to zrobić za pomocą`TxtLoadOptions` Klasa, która umożliwia określenie opcji parsowania, w tym kodowania i niestandardowych parserów.
### 2.1 Skonfiguruj opcje ładowania
 Zaczniemy od zainicjowania`TxtLoadOptions` i zdefiniowanie kluczowych parametrów, takich jak separator i kodowanie:
```csharp
TxtLoadOptions oTxtLoadOptions = new TxtLoadOptions(LoadFormat.Csv);
oTxtLoadOptions.Separator = Convert.ToChar(",");
oTxtLoadOptions.Encoding = Encoding.UTF8;
oTxtLoadOptions.ConvertDateTimeData = true;
```
- Separator: Określa znak używany do oddzielania wartości w pliku CSV (w tym przypadku przecinki).
- Kodowanie: Używamy kodowania UTF-8, aby obsługiwać szeroki zakres znaków.
-  ConvertDateTimeData: Ustawienie tej opcji na true zapewnia, że wartości daty zostaną automatycznie przekonwertowane na`DateTime` obiektów, o ile to możliwe.
### 2.2 Zastosuj niestandardowe parsery
Następnie przypiszemy parsery, które utworzyliśmy wcześniej, do obsługi wartości w pliku CSV:
```csharp
oTxtLoadOptions.PreferredParsers = new ICustomParser[] 
{ 
    new TextParser(), 
    new DateParser() 
};
```
 Informuje Aspose.Cells o użyciu`TextParser` dla ogólnych wartości tekstowych i`DateParser`dla wszystkich pól dat występujących w pliku CSV.
## Krok 3: Załaduj i odczytaj plik CSV
 Teraz, gdy opcje ładowania są skonfigurowane, możesz załadować plik CSV do`Aspose.Cells.Workbook` obiekt.
### 3.1 Załaduj plik CSV
 Ładujemy plik CSV, podając ścieżkę do pliku i skonfigurowany`TxtLoadOptions` do`Workbook` konstruktor:
```csharp
string sourceDir = "Your Document Directory";
Workbook oExcelWorkBook = new Aspose.Cells.Workbook(sourceDir + "samplePreferredParser.csv", oTxtLoadOptions);
```
Ten krok umożliwia konwersję danych CSV do w pełni funkcjonalnego skoroszytu programu Excel, a każda wartość jest analizowana według preferowanych przez Ciebie reguł.
## Krok 4: Dostęp i wyświetlanie danych komórkowych
Po załadowaniu pliku CSV do skoroszytu możesz zacząć pracować z danymi. Na przykład możesz chcieć wydrukować typ i wartość określonych komórek.
### 4.1 Pobierz i wyświetl komórkę A1
Pobierzmy pierwszą komórkę (A1) i wyświetlmy jej wartość oraz typ:
```csharp
Cell oCell = oExcelWorkBook.Worksheets[0].Cells["A1"];
Console.WriteLine("A1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
 Tutaj,`Type` Właściwość pokazuje typ danych (taki jak`String` Lub`DateTime` ), I`DisplayStringValue` podaje sformatowaną wartość.
### 4.2 Pobierz i wyświetl komórkę B1
Podobnie możemy pobrać i wyświetlić inną komórkę, np. B1:
```csharp
oCell = oExcelWorkBook.Worksheets[0].Cells["B1"];
Console.WriteLine("B1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
Proces ten można powtarzać dla dowolnej liczby komórek, które chcesz zbadać.
## Krok 5: Zapisz skoroszyt
 Po pracy z danymi możesz chcieć zapisać skoroszyt do nowego pliku. Aspose.Cells ułatwia to za pomocą prostego`Save` metoda:
```csharp
string outputDir = "Your Document Directory";
oExcelWorkBook.Save(outputDir + "outputsamplePreferredParser.xlsx");
```
Spowoduje to zapisanie skoroszytu w pliku programu Excel, z zachowaniem całego zastosowanego formatowania i analizy danych.
## Wniosek
Otwieranie plików CSV za pomocą preferowanego parsera w Aspose.Cells dla .NET to elastyczny i wydajny sposób obsługi różnych typów danych. Tworząc niestandardowe parsery i konfigurując opcje ładowania, możesz mieć pewność, że pliki CSV są analizowane dokładnie tak, jak tego potrzebujesz, niezależnie od tego, czy masz do czynienia z tekstem, datami czy innymi niestandardowymi formatami. Dzięki temu samouczkowi jesteś teraz wyposażony do obsługi bardziej złożonych scenariuszy analizy danych w swoich projektach.
## Najczęściej zadawane pytania
### Jaki jest cel niestandardowych parserów w Aspose.Cells dla .NET?
Niestandardowe parsery umożliwiają zdefiniowanie sposobu analizowania określonych typów danych, np. tekstu lub dat, podczas ładowania pliku CSV.
### Czy mogę użyć innego znaku separatora w pliku CSV?
 Tak, możesz określić dowolny znak jako separator w`TxtLoadOptions.Separator` nieruchomość.
### Jak poradzić sobie z kodowaniem w Aspose.Cells podczas ładowania pliku CSV?
 Możesz ustawić`Encoding` własność`TxtLoadOptions` do dowolnego schematu kodowania, np. UTF-8, ASCII itp.
### Co się stanie, jeśli format daty w pliku CSV będzie inny?
Możesz zdefiniować konkretny format daty za pomocą niestandardowego parsera, co zapewni poprawną analizę wartości dat.
### Czy mogę zapisać skoroszyt w innych formatach?
Tak, Aspose.Cells pozwala na zapisanie skoroszytu w różnych formatach, takich jak XLSX, CSV, PDF i inne.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
