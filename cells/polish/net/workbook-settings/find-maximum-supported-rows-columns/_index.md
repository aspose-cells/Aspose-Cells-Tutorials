---
title: Znajdź maksymalną liczbę wierszy i kolumn obsługiwanych przez formaty XLS i XLSX
linktitle: Znajdź maksymalną liczbę wierszy i kolumn obsługiwanych przez formaty XLS i XLSX
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Odkryj maksymalną liczbę wierszy i kolumn obsługiwanych przez formaty XLS i XLSX przy użyciu Aspose.Cells dla .NET. Zmaksymalizuj zarządzanie danymi w programie Excel dzięki temu kompleksowemu samouczkowi.
weight: 11
url: /pl/net/workbook-settings/find-maximum-supported-rows-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Znajdź maksymalną liczbę wierszy i kolumn obsługiwanych przez formaty XLS i XLSX

## Wstęp
W świecie Excela zarządzanie dużymi zestawami danych może być trudnym zadaniem, zwłaszcza jeśli chodzi o obsługę maksymalnej liczby wierszy i kolumn obsługiwanych przez różne formaty plików. Ten samouczek przeprowadzi Cię przez proces znajdowania maksymalnej liczby wierszy i kolumn obsługiwanych przez formaty XLS i XLSX przy użyciu biblioteki Aspose.Cells for .NET. Pod koniec tego artykułu będziesz mieć kompleksowe zrozumienie, jak korzystać z tego potężnego narzędzia, aby wydajnie obsługiwać zadania związane z Excelem.
## Wymagania wstępne
Zanim przejdziemy do samouczka, upewnij się, że spełnione są następujące wymagania wstępne:
1. [.NET Framework](https://dotnet.microsoft.com/en-us/download) Lub[.NET Core](https://dotnet.microsoft.com/en-us/download) zainstalowany w Twoim systemie.
2. [Aspose.Cells dla .NET](https://releases.aspose.com/cells/net/) biblioteka pobrana i przywoływana w Twoim projekcie.
 Jeśli jeszcze tego nie zrobiłeś, możesz pobrać bibliotekę Aspose.Cells dla .NET ze strony[strona internetowa](https://releases.aspose.com/cells/net/) lub zainstaluj go poprzez[Pobierz](https://www.nuget.org/packages/Aspose.Cells/).
## Importuj pakiety
Aby rozpocząć, musisz zaimportować niezbędne pakiety z biblioteki Aspose.Cells for .NET. Dodaj następujące polecenia using na górze pliku C#:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Krok 1: Znajdź maksymalną liczbę wierszy i kolumn obsługiwanych przez format XLS
Zacznijmy od sprawdzenia maksymalnej liczby wierszy i kolumn obsługiwanych przez format XLS (Excel 97-2003).
```csharp
// Wydrukuj wiadomość o formacie XLS.
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// Utwórz skoroszyt w formacie XLS.
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// Wydrukuj maksymalną liczbę wierszy i kolumn obsługiwanych przez format XLS.
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
Na tym etapie:
1. Wyświetl komunikat informujący, że pracujemy w formacie XLS.
2.  Utwórz nowy`Workbook` wystąpienie przy użyciu`FileFormatType.Excel97To2003` enum, które reprezentuje format XLS.
3.  Pobierz maksymalną liczbę wierszy i kolumn obsługiwanych przez format XLS, korzystając z`Workbook.Settings.MaxRow` I`Workbook.Settings.MaxColumn`właściwości, odpowiednio. Dodajemy 1 do tych wartości, aby uzyskać rzeczywiste maksymalne numery wierszy i kolumn (ponieważ są one zerowe).
4. Wydrukuj maksymalną liczbę wierszy i kolumn na konsoli.
## Krok 2: Znajdź maksymalną liczbę wierszy i kolumn obsługiwanych przez format XLSX
Następnie przyjrzyjmy się maksymalnej liczbie wierszy i kolumn obsługiwanych przez format XLSX (Excel 2007 i nowsze).
```csharp
// Wydrukuj wiadomość o formacie XLSX.
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// Utwórz skoroszyt w formacie XLSX.
wb = new Workbook(FileFormatType.Xlsx);
// Wydrukuj maksymalną liczbę wierszy i kolumn obsługiwanych przez format XLSX.
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
Na tym etapie:
1. Wyświetl komunikat informujący, że pracujemy z formatem XLSX.
2.  Utwórz nowy`Workbook` wystąpienie przy użyciu`FileFormatType.Xlsx` enum, które reprezentuje format XLSX.
3.  Pobierz maksymalną liczbę wierszy i kolumn obsługiwanych przez format XLSX, korzystając z`Workbook.Settings.MaxRow` I`Workbook.Settings.MaxColumn`właściwości, odpowiednio. Dodajemy 1 do tych wartości, aby uzyskać rzeczywiste maksymalne numery wierszy i kolumn (ponieważ są one zerowe).
4. Wydrukuj maksymalną liczbę wierszy i kolumn na konsoli.
## Krok 3: Wyświetl komunikat o powodzeniu
Na koniec wyświetlmy komunikat o powodzeniu, aby poinformować, że przykład „FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats” został wykonany pomyślnie.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
Ten krok po prostu wyświetla na konsoli komunikat o powodzeniu.
## Wniosek
tym samouczku nauczyłeś się, jak używać biblioteki Aspose.Cells for .NET, aby znaleźć maksymalną liczbę wierszy i kolumn obsługiwanych przez formaty plików XLS i XLSX. Dzięki zrozumieniu ograniczeń tych formatów możesz lepiej planować i zarządzać projektami opartymi na programie Excel, zapewniając, że Twoje dane mieszczą się w obsługiwanych zakresach.
## Najczęściej zadawane pytania
### Jaka jest maksymalna liczba wierszy obsługiwana przez format XLS?
Maksymalna liczba wierszy obsługiwanych przez format XLS (Excel 97-2003) wynosi 65 536.
### Jaka jest maksymalna liczba kolumn obsługiwana przez format XLS?
Maksymalna liczba kolumn obsługiwana przez format XLS (Excel 97-2003) wynosi 256.
### Jaka jest maksymalna liczba wierszy obsługiwana przez format XLSX?
Maksymalna liczba wierszy obsługiwana przez format XLSX (Excel 2007 i nowsze) wynosi 1 048 576.
### Jaka jest maksymalna liczba kolumn obsługiwana przez format XLSX?
Maksymalna liczba kolumn obsługiwana przez format XLSX (Excel 2007 i nowsze) wynosi 16 384.
### Czy mogę używać biblioteki Aspose.Cells for .NET do pracy z innymi formatami plików Excel?
 Tak, biblioteka Aspose.Cells for .NET obsługuje szeroki zakres formatów plików Excel, w tym XLS, XLSX, ODS i inne. Możesz eksplorować[dokumentacja](https://reference.aspose.com/cells/net/) aby dowiedzieć się więcej o dostępnych funkcjach i możliwościach.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
