---
title: Dostosowywanie formatów wyświetlania za pomocą liczb zdefiniowanych przez użytkownika
linktitle: Dostosowywanie formatów wyświetlania za pomocą liczb zdefiniowanych przez użytkownika
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak dostosować formaty wyświetlania za pomocą Aspose.Cells dla .NET. Formatuj daty, procenty i waluty za pomocą tego przewodnika krok po kroku.
weight: 11
url: /pl/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dostosowywanie formatów wyświetlania za pomocą liczb zdefiniowanych przez użytkownika

## Wstęp
Praca z plikami Excela często wymaga niestandardowego formatowania komórek, aby przedstawić dane w bardziej znaczący i przyjazny dla użytkownika sposób. Wyobraź sobie, że tworzysz plik Excela na potrzeby raportu. Nie chcesz tylko surowych liczb. Chcesz, aby daty, procenty i waluty wyglądały elegancko i profesjonalnie, prawda? Właśnie tutaj wkraczają niestandardowe formaty wyświetlania. W tym samouczku zagłębiamy się w Aspose.Cells dla .NET, aby pokazać, jak dostosować format wyświetlania liczb przy użyciu ustawień zdefiniowanych przez użytkownika.
## Wymagania wstępne
Zanim zaczniesz, upewnij się, że masz wszystko gotowe, aby śledzić ten samouczek. Oto, czego będziesz potrzebować:
-  Aspose.Cells dla .NET zainstalowany.[Pobierz tutaj](https://releases.aspose.com/cells/net/).
- Podstawowa znajomość języka C# i .NET Framework.
-  Ważna licencja na Aspose.Cells. Jeśli jej nie masz, zdobądź[bezpłatny okres próbny](https://releases.aspose.com/) lub poproś o[licencja tymczasowa](https://purchase.aspose.com/temporary-license/).
- Środowisko IDE podobne do Visual Studio.
- .NET Framework 4.0 lub nowszy.
 Jeśli czegoś Ci brakuje, nie martw się. Zawsze możesz ponownie odwiedzić te linki, aby pobrać niezbędne pliki lub poprosić o pomoc[Forum wsparcia Aspose](https://forum.aspose.com/c/cells/9).
## Importuj przestrzenie nazw
Zanim przejdziesz do kodu, musisz zaimportować wymagane przestrzenie nazw, aby uzyskać dostęp do wszystkich niezbędnych funkcjonalności Aspose.Cells.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Te dwie przestrzenie nazw będą twoimi głównymi narzędziami w tym samouczku. Teraz przejdźmy do zabawnej części:
## Krok 1: Konfigurowanie katalogu projektu
Najpierw potrzebujesz miejsca do przechowywania plików, prawda? Utwórzmy katalog, aby zapisać plik wyjściowy Excela. W tym kroku upewnimy się również, że katalog istnieje, zanim cokolwiek zapiszemy.
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
// Utwórz katalog, jeśli jeszcze go nie ma.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
-  Definiujemy`dataDir` zmienna przechowująca ścieżkę dostępu do pliku wyjściowego programu Excel.
-  Następnie sprawdzamy, czy katalog istnieje, używając`System.IO.Directory.Exists()`.
-  Jeżeli katalog nie istnieje, zostanie utworzony za pomocą`System.IO.Directory.CreateDirectory()`.
## Krok 2: Utwórz nowy skoroszyt i dodaj arkusz kalkulacyjny
Teraz, gdy mamy już nasz katalog, utwórzmy nowy skoroszyt w programie Excel i dodajmy do niego arkusz.
```csharp
// Tworzenie instancji obiektu skoroszytu
Workbook workbook = new Workbook();
// Dodawanie nowego arkusza kalkulacyjnego do obiektu Excel
int i = workbook.Worksheets.Add();
// Uzyskanie odniesienia do nowo dodanego arkusza roboczego poprzez podanie indeksu arkusza
Worksheet worksheet = workbook.Worksheets[i];
```
-  Najpierw tworzymy nowy`Workbook` obiekt. Pomyśl o tym jak o swoim pliku Excel.
-  Dodajemy nowy arkusz do tego skoroszytu za pomocą`Add()`metoda i zapisz indeks w zmiennej`i`.
-  Do tego arkusza roboczego odwołujemy się za pomocą`workbook.Worksheets[i]`.
## Krok 3: Dodawanie daty do komórki i dostosowywanie jej formatu
 Teraz wstawmy bieżącą datę do komórki i sformatujmy ją tak, aby wyświetlała się w niestandardowy sposób. Zamiast domyślnego formatu daty ustawimy niestandardowy format, taki jak`d-mmm-yy`.
```csharp
// Dodawanie bieżącej daty systemowej do komórki „A1”
worksheet.Cells["A1"].PutValue(DateTime.Now);
// Uzyskiwanie stylu komórki A1
Style style = worksheet.Cells["A1"].GetStyle();
// Ustawianie niestandardowego formatu wyświetlania, aby data była wyświetlana jako „d-mmm-rr”
style.Custom = "d-mmm-yy";
// Stosowanie stylu do komórki A1
worksheet.Cells["A1"].SetStyle(style);
```
-  Dodajemy aktualną datę systemową do komórki`A1` używając`PutValue(DateTime.Now)`.
-  Pobieramy aktualny styl komórki`A1` używając`GetStyle()`.
-  Modyfikujemy styl komórki poprzez ustawienie`style.Custom = "d-mmm-yy"`, który formatuje datę tak, aby pokazywała dzień, skrócony miesiąc i rok.
-  Na koniec stosujemy nowy styl do komórki za pomocą`SetStyle()`.
## Krok 4: Formatowanie komórki jako wartości procentowej
 Następnie zajmiemy się liczbami. Dodamy wartość liczbową do innej komórki, powiedzmy`A2`i sformatuj go jako wartość procentową.
```csharp
//Dodawanie wartości liczbowej do komórki „A2”
worksheet.Cells["A2"].PutValue(20);
// Uzyskiwanie stylu komórki A2
style = worksheet.Cells["A2"].GetStyle();
// Ustawianie niestandardowego formatu wyświetlania w celu wyświetlania wartości jako procent
style.Custom = "0.0%";
// Stosowanie stylu do komórki A2
worksheet.Cells["A2"].SetStyle(style);
```
-  Dodajemy wartość`20` do komórki`A2`.
-  Pobieramy styl komórki`A2` i ustaw niestandardowy format na`0.0%` aby wyświetlić wartość jako procent (np. 20%).
-  Na koniec stosujemy styl do komórki za pomocą`SetStyle()`.
## Krok 5: Formatowanie komórki jako waluty
 Dodajmy kolejną wartość, powiedzmy do komórki`A3`i sformatuj go tak, aby wyświetlał się jako waluta. Aby było ciekawiej, użyjemy formatu, który wyświetla wartości dodatnie jako walutę w funtach, a wartości ujemne jako dolary.
```csharp
// Dodawanie wartości liczbowej do komórki „A3”
worksheet.Cells["A3"].PutValue(2546);
// Uzyskiwanie stylu komórki A3
style = worksheet.Cells["A3"].GetStyle();
// Ustawianie niestandardowego formatu wyświetlania w celu wyświetlania wartości jako waluty
style.Custom = "£#,##0;[Red]$-#,##0";
// Stosowanie stylu do komórki A3
worksheet.Cells["A3"].SetStyle(style);
```
-  Dodajemy wartość`2546` do komórki`A3`.
-  Ustawiliśmy niestandardowy format`£#,##0;[Red]$-#,##0`, który wyświetla wartości dodatnie za pomocą znaku funta, a wartości ujemne na czerwono ze znakiem dolara.
- Zastosowujemy styl do komórki za pomocą`SetStyle()`.
## Krok 6: Zapisywanie skoroszytu
Ostatnim krokiem jest zapisanie skoroszytu jako pliku Excel. W tym samouczku użyjemy formatu Excel 97-2003.
```csharp
// Zapisywanie pliku Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
-  Ten`Save()` Metoda zapisuje skoroszyt w określonym katalogu.
-  Wybieramy`SaveFormat.Excel97To2003` aby zapewnić zgodność ze starszymi wersjami programu Excel.
## Wniosek
Oto i masz! Właśnie utworzyliśmy plik Excel, dodaliśmy niestandardowe formaty daty, procentów i walut do określonych komórek za pomocą Aspose.Cells dla .NET i zapisaliśmy plik. Niestandardowe formatowanie sprawia, że pliki Excel są o wiele bardziej czytelne i profesjonalne. Nie zapomnij zapoznać się z innymi opcjami formatowania w Aspose.Cells, takimi jak formatowanie warunkowe, aby uzyskać jeszcze większą kontrolę nad wyglądem danych.
## Najczęściej zadawane pytania
### Jak mogę zastosować bardziej złożone opcje formatowania w Aspose.Cells?
Możesz łączyć różne style formatowania, takie jak kolor czcionki, obramowanie i kolory tła, z niestandardowymi formatami liczb.
### Czy mogę zastosować niestandardowy format liczb do zakresu komórek?
Tak, Aspose.Cells pozwala na zastosowanie stylu do zakresu komórek za pomocą`Range.SetStyle()` metoda.
### W jakich innych formatach plików mogę zapisać skoroszyt?
 Aspose.Cells obsługuje wiele formatów, w tym XLSX, CSV i PDF. Wystarczy zmienić`SaveFormat` w`Save()` metoda.
### Czy mogę inaczej sformatować liczby ujemne?
Oczywiście! Możesz użyć niestandardowych formatów liczbowych, aby wyświetlać liczby ujemne w różnych kolorach lub symbolach.
### Czy Aspose.Cells dla .NET jest darmowy?
 Aspose.Cells oferuje bezpłatną wersję próbną, ale do pełnej funkcjonalności potrzebna jest ważna licencja. Możesz uzyskać[tymczasowa licencja tutaj](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
