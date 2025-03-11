---
title: Programowe używanie wbudowanych formatów liczbowych w programie Excel
linktitle: Programowe używanie wbudowanych formatów liczbowych w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Zautomatyzuj formatowanie liczb w programie Excel za pomocą Aspose.Cells dla .NET. Dowiedz się, jak programowo stosować formaty daty, procentów i walut.
weight: 10
url: /pl/net/number-and-display-formats-in-excel/using-built-in-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programowe używanie wbudowanych formatów liczbowych w programie Excel

## Wstęp
tym samouczku pokażemy Ci, jak używać wbudowanych formatów liczbowych w programie Excel przy użyciu Aspose.Cells dla .NET. Omówimy wszystko, od konfiguracji środowiska po stosowanie różnych formatów, takich jak daty, procenty i waluty. Niezależnie od tego, czy jesteś doświadczonym profesjonalistą, czy dopiero zaczynasz przygodę z ekosystemem .NET, ten przewodnik sprawi, że formatowanie komórek w programie Excel będzie dla Ciebie pestką.
## Wymagania wstępne
Zanim zaczniesz, upewnij się, że masz następujące rzeczy:
-  Zainstalowano bibliotekę Aspose.Cells dla .NET. Możesz[pobierz tutaj](https://releases.aspose.com/cells/net/).
- Znajomość języka C# i podstaw programowania .NET.
- Visual Studio lub dowolne środowisko IDE .NET zainstalowane na Twoim komputerze.
-  Ważna licencja Aspose lub[licencja tymczasowa](https://purchase.aspose.com/temporary-license/).
- Zainstalowana platforma .NET Framework (wersja 4.0 lub nowsza).
  
Jeśli brakuje Ci czegoś z powyższych, skorzystaj z podanych linków, aby wszystko skonfigurować. Gotowy? Przejdźmy do zabawy!
## Importuj pakiety
Zanim rozpoczniesz pracę z samouczkiem, pamiętaj o zaimportowaniu niezbędnych przestrzeni nazw do pracy z Aspose.Cells dla .NET:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Po zaimportowaniu ich możesz już programowo manipulować plikami Excela. Teraz przejdźmy do przewodnika krok po kroku!
## Krok 1: Utwórz lub uzyskaj dostęp do skoroszytu programu Excel
W tym kroku utworzysz nowy skoroszyt. Pomyśl o tym jak o otwarciu nowego pliku Excel, z tą różnicą, że robisz to za pomocą kodu!
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
// Utwórz katalog, jeśli jeszcze go nie ma.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Tworzenie instancji obiektu skoroszytu
Workbook workbook = new Workbook();
```
 Tutaj po prostu tworzymy nową instancję`Workbook` obiekt. Działa jak plik Excel, gotowy do manipulacji danymi. Możesz również załadować istniejący plik, podając jego ścieżkę.
## Krok 2: Uzyskaj dostęp do arkusza kalkulacyjnego
Skoroszyty programu Excel mogą zawierać wiele arkuszy. W tym kroku uzyskamy dostęp do pierwszego arkusza w skoroszycie:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Teraz uzyskujemy dostęp do pierwszego arkusza w skoroszycie. Jeśli potrzebujesz manipulować dodatkowymi arkuszami, możesz odwołać się do nich, używając ich indeksu lub nazwy.
## Krok 3: Dodaj dane do komórek
Zacznijmy dodawać dane do konkretnych komórek. Najpierw wstawimy bieżącą datę systemową do komórki „A1”:
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Ten wiersz wstawia bieżącą datę do komórki A1. Całkiem fajne, prawda? Wyobraź sobie, że robisz to ręcznie dla setek komórek — to byłby koszmar. Teraz przejdziemy do formatowania!
## Krok 4: Formatowanie daty w komórce „A1”
Następnie sformatujmy tę datę w bardziej czytelnym formacie, np. „15-Oct-24”. To tutaj Aspose.Cells naprawdę się wyróżnia:
1. Pobierz styl komórki:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Tutaj chwytamy styl komórki A1. Pomyśl o tym jak o chwytaniu „mody” komórki przed wprowadzeniem jakichkolwiek poprawek.
2. Ustaw format daty:
```csharp
style.Number = 15;
```
 Ustawianie`Number` właściwość do 15 stosuje pożądany format daty. Jest to wbudowany kod formatu liczbowego do wyświetlania dat w formacie „d-mmm-yy”.
3. Zastosuj styl do komórki:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Ten wiersz stosuje zmiany stylu do komórki. Teraz zamiast domyślnego formatu daty zobaczysz coś o wiele bardziej przyjaznego dla użytkownika, np. „15-Oct-24”.
## Krok 5: Dodaj i sformatuj procent w komórce „A2”
Przejdźmy do formatowania procentów. Wyobraź sobie, że chcesz wstawić wartość i wyświetlić ją jako procent. W tym kroku dodamy wartość liczbową do komórki „A2” i sformatujemy ją jako procent:
1. Wprowadź wartość liczbową:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Wstawia liczbę 20 do komórki A2. Możesz pomyśleć: „To po prostu zwykła liczba — jak zamienić ją na procent?” No cóż, zaraz do tego dojdziemy.
2. Pobierz styl i ustaw format procentowy:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Formatuj jako procent
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Tutaj dodajemy 2546 do komórki A3. Następnie sformatujemy tę liczbę tak, aby wyświetlała się jako waluta.
2. Pobierz styl i ustaw format waluty:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Formatuj jako walutę
worksheet.Cells["A3"].SetStyle(style);
```
 Ustawianie`Number` property to 6 stosuje format waluty. Teraz wartość w komórce A3 będzie wyświetlana jako „2,546.00”, z przecinkami i dwoma miejscami dziesiętnymi.
## Krok 7: Zapisz plik Excel
Teraz, gdy zastosowaliśmy całą magię formatowania, czas zapisać plik:
```csharp
// Zapisywanie pliku Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 Ten wiersz zapisuje plik Excel w formacie Excel 97-2003. Możesz zmienić`SaveFormat`aby dopasować do Twoich potrzeb. I tak po prostu, utworzyłeś i sformatowałeś plik Excel programowo!
## Wniosek
Gratulacje! Udało Ci się nauczyć, jak używać Aspose.Cells dla .NET, aby stosować wbudowane formaty liczbowe do komórek w pliku Excel. Od dat po procenty i waluty, omówiliśmy niektóre z najczęstszych potrzeb formatowania dla przetwarzania danych w programie Excel. Teraz zamiast ręcznie formatować komórki, możesz zautomatyzować cały proces — oszczędzając czas i zmniejszając liczbę błędów.
## Najczęściej zadawane pytania
### Czy mogę stosować niestandardowe formaty liczb przy użyciu Aspose.Cells dla .NET?
 Tak! Oprócz wbudowanych formatów, Aspose.Cells obsługuje również niestandardowe formaty liczbowe. Możesz tworzyć bardzo specyficzne formaty za pomocą`Custom` nieruchomość w`Style` klasa.
### Jak mogę sformatować komórkę jako walutę z określonym symbolem?
 Aby zastosować konkretny symbol waluty, możesz użyć formatowania niestandardowego, ustawiając`Style.Custom` nieruchomość.
### Czy mogę formatować całe wiersze lub kolumny?
 Oczywiście! Możesz stosować style do całych wierszy lub kolumn za pomocą`Rows` Lub`Columns`kolekcje w`Worksheet` obiekt.
### Jak mogę sformatować wiele komórek jednocześnie?
Możesz użyć`Range` obiekt umożliwiający zaznaczenie wielu komórek i zastosowanie do nich wszystkich stylów jednocześnie.
### Czy muszę mieć zainstalowany program Microsoft Excel, aby korzystać z Aspose.Cells?
Nie, Aspose.Cells działa niezależnie od programu Microsoft Excel, więc nie musisz instalować programu Excel na swoim komputerze.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
