---
title: Chroń określone komórki w arkuszu kalkulacyjnym za pomocą Aspose.Cells
linktitle: Chroń określone komórki w arkuszu kalkulacyjnym za pomocą Aspose.Cells
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak chronić określone komórki w arkuszu kalkulacyjnym programu Excel za pomocą Aspose.Cells dla .NET. Zabezpiecz poufne dane i zapobiegaj przypadkowym zmianom w zaledwie kilku krokach.
weight: 14
url: /pl/net/worksheet-security/protect-specific-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chroń określone komórki w arkuszu kalkulacyjnym za pomocą Aspose.Cells

## Wstęp
W tym samouczku przeprowadzimy Cię przez proces ochrony określonych komórek w arkuszu kalkulacyjnym programu Excel. Pod koniec będziesz w stanie pewnie blokować komórki jak profesjonalista, zapobiegając nieautoryzowanym zmianom, a jednocześnie zachowując elastyczność arkusza kalkulacyjnego tam, gdzie jest to potrzebne.
## Wymagania wstępne
Zanim przejdziemy do szczegółów, upewnijmy się, że masz wszystko, czego potrzebujesz, aby płynnie przejść przez ten samouczek:
1. Visual Studio – Jeśli jeszcze tego nie zrobiłeś, pobierz i zainstaluj Visual Studio. Będzie to główne środowisko, w którym uruchamiasz aplikacje .NET.
2.  Aspose.Cells dla .NET – Będziesz potrzebować biblioteki Aspose.Cells, aby pracować z plikami Excel w aplikacjach .NET. Jeśli jeszcze jej nie zainstalowałeś, możesz pobrać najnowszą wersję z[Strona internetowa Aspose](https://releases.aspose.com/cells/net/).
3. .NET Framework lub .NET Core – Ten samouczek działa zarówno z .NET Framework, jak i .NET Core. Upewnij się tylko, że Twój projekt jest zgodny z Aspose.Cells.
Gdy już to wszystko zrobisz, będziesz gotowy do rozpoczęcia pracy.
## Importuj pakiety
Zanim przejdziesz do przewodnika krok po kroku, musisz upewnić się, że importujesz niezbędne przestrzenie nazw do pracy z Aspose.Cells. W swoim projekcie umieść następujące polecenia importu na górze pliku:
```csharp
using System.IO;
using Aspose.Cells;
```
Te przestrzenie nazw umożliwią Ci interakcję z plikami Excela i klasami wymaganymi do stylizowania i ochrony komórek arkusza kalkulacyjnego.
Teraz podzielmy to na proste kroki, aby chronić określone komórki w arkuszu kalkulacyjnym za pomocą Aspose.Cells dla .NET. Zabezpieczymy komórki A1, B1 i C1, pozostawiając resztę arkusza kalkulacyjnego otwartą do edycji.
## Krok 1: Utwórz nowy skoroszyt i arkusz kalkulacyjny
Po pierwsze, musisz utworzyć nowy skoroszyt (plik Excel) i arkusz w nim. Tutaj zastosujesz ochronę komórki.
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
// Utwórz katalog, jeśli jeszcze go nie ma.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
// Utwórz nowy skoroszyt.
Workbook wb = new Workbook();
// Utwórz obiekt arkusza kalkulacyjnego i uzyskaj pierwszy arkusz.
Worksheet sheet = wb.Worksheets[0];
```
 W tym kroku tworzysz również katalog do przechowywania wynikowego pliku Excel, jeśli jeszcze nie istnieje.`Workbook` Klasa inicjuje nowy plik Excela i`Worksheets[0]` pozwala nam pracować na pierwszym arkuszu skoroszytu.
## Krok 2: Odblokuj wszystkie kolumny
Następnie odblokujesz wszystkie kolumny w arkuszu. Dzięki temu domyślnie wszystkie komórki w arkuszu będą edytowalne. Później zablokujemy tylko te komórki, które chcemy chronić.
```csharp
// Zdefiniuj obiekt stylu.
Style style;
// Zdefiniuj obiekt styleflag
StyleFlag styleflag;
// Przejdź przez wszystkie kolumny arkusza i odblokuj je.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    styleflag = new StyleFlag();
    styleflag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, styleflag);
}
```
 W tym bloku kodu przechodzimy przez wszystkie kolumny (do 255) i ustawiamy`IsLocked` nieruchomość do`false` To zasadniczo odblokowuje wszystkie komórki w tych kolumnach, dzięki czemu są one domyślnie edytowalne. Następnie stosujemy styl do kolumny za pomocą`ApplyStyle()` metoda.
## Krok 3: Zablokuj określone komórki (A1, B1, C1)
 Teraz, gdy wszystkie kolumny są odblokowane, skupimy się na zablokowaniu konkretnych komórek, mianowicie A1, B1 i C1. Zmodyfikujemy style komórek i ustawimy ich`IsLocked` nieruchomość do`true`.
```csharp
// Zablokuj trzy komórki...tj. A1, B1, C1.
style = sheet.Cells["A1"].GetStyle();
style.IsLocked = true;
sheet.Cells["A1"].SetStyle(style);
style = sheet.Cells["B1"].GetStyle();
style.IsLocked = true;
sheet.Cells["B1"].SetStyle(style);
style = sheet.Cells["C1"].GetStyle();
style.IsLocked = true;
sheet.Cells["C1"].SetStyle(style);
```
Ten krok zapewnia, że komórki A1, B1 i C1 są zablokowane. Są to komórki, które będą chronione i nie będą edytowalne po zastosowaniu ochrony arkusza kalkulacyjnego.
## Krok 4: Chroń arkusz kalkulacyjny
Po zablokowaniu niezbędnych komórek następnym krokiem jest ochrona całego arkusza kalkulacyjnego. Ten krok sprawia, że zablokowane komórki (A1, B1, C1) stają się nieedytowalne, podczas gdy inne komórki pozostają otwarte do edycji.
```csharp
// Na koniec zabezpiecz arkusz.
sheet.Protect(ProtectionType.All);
```
 Ten`Protect` Metoda jest wywoływana na arkuszu, określając, że wszystkie aspekty arkusza powinny być chronione. Blokuje to określone komórki, które zostały oznaczone`IsLocked = true` i zapewnia, że użytkownicy nie mogą ich zmienić.
## Krok 5: Zapisz skoroszyt
Po zablokowaniu komórek i zabezpieczeniu arkusza możesz zapisać skoroszyt w wybranej lokalizacji.
```csharp
// Zapisz plik Excela.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Ten krok zapisuje skoroszyt do`dataDir` folder z nazwą pliku`output.out.xls`. Możesz zmienić nazwę pliku i katalog zgodnie ze swoimi potrzebami. Plik jest zapisany w formacie Excel 97-2003, ale możesz dostosować go do swoich wymagań.
## Wniosek
Ochrona określonych komórek w arkuszu kalkulacyjnym programu Excel za pomocą Aspose.Cells dla .NET to prosty proces. Wykonując powyższe kroki, możesz zablokować określone komórki, a jednocześnie pozwolić innym pozostać edytowalnymi. Ta funkcja jest niezwykle przydatna podczas udostępniania skoroszytów innym osobom, ponieważ pomaga kontrolować, które dane można modyfikować, a które powinny pozostać chronione. Niezależnie od tego, czy pracujesz nad poufnymi danymi, czy po prostu zapobiegasz przypadkowym zmianom, Aspose.Cells zapewnia elastyczne i wydajne rozwiązanie.
## Najczęściej zadawane pytania
### Jak mogę chronić konkretny zakres komórek, a nie tylko kilka?
Możesz zmodyfikować kod, aby przechodził przez określony zakres komórek lub kolumn i blokował je, zamiast ręcznie blokować poszczególne komórki.
### Czy mogę dodać hasła, aby chronić arkusz kalkulacyjny?
Tak, możesz podać hasło podczas dzwonienia`Protect()` metoda uniemożliwiająca użytkownikom odblokowanie arkusza bez podania prawidłowego hasła.
### Czy mogę chronić konkretne wiersze lub kolumny zamiast komórek?
 Tak, Aspose.Cells pozwala na blokowanie całych wierszy lub kolumn poprzez modyfikację`IsLocked` właściwość dla wierszy lub kolumn, podobnie jak blokujemy komórki.
### Jak mogę usunąć ochronę arkusza kalkulacyjnego?
 Aby usunąć ochronę arkusza kalkulacyjnego, użyj`Unprotect()` metoda opcjonalnie podająca hasło, jeśli zostało ustawione podczas ochrony.
### Czy mogę używać Aspose.Cells do innych operacji w programie Excel, na przykład dodawania formuł lub wykresów?
Oczywiście! Aspose.Cells to solidna biblioteka, która umożliwia wykonywanie szerokiego zakresu operacji w programie Excel, w tym dodawanie formuł, tworzenie wykresów i wiele więcej.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
