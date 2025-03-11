---
title: Kopiowanie danych w skoroszycie za pomocą Aspose.Cells
linktitle: Kopiowanie danych w skoroszycie za pomocą Aspose.Cells
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Naucz się efektywnie kopiować dane w skoroszycie programu Excel za pomocą Aspose.Cells dla platformy .NET, korzystając z przewodnika krok po kroku, przykładów kodu i przydatnych wskazówek.
weight: 12
url: /pl/net/worksheet-value-operations/copy-data-within-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiowanie danych w skoroszycie za pomocą Aspose.Cells

## Wstęp
Zarządzanie danymi w skoroszytach programu Excel jest podstawową częścią wielu aplikacji. Wyobraź sobie, że masz szablon lub arkusz wypełniony niezbędnymi danymi i chcesz go zduplikować w tym samym skoroszycie, aby móc go dalej używać. To właśnie tutaj Aspose.Cells dla .NET błyszczy! W tym przewodniku przeprowadzimy Cię przez kopiowanie danych w tym samym skoroszycie, używając Aspose.Cells, z przyjaznym i przejrzystym samouczkiem krok po kroku.
## Wymagania wstępne
Zanim przejdziemy do kodowania, upewnijmy się, że mamy wszystko, czego potrzebujemy do wykonania tego zadania:
1.  Biblioteka Aspose.Cells dla .NET — pobierz najnowszą wersję ze strony[Strona pobierania Aspose.Cells dla .NET](https://releases.aspose.com/cells/net/).
2. Środowisko programistyczne – Będziesz potrzebować środowiska IDE zgodnego z platformą .NET, np. Visual Studio.
3.  Licencja – Korzystanie z bezpłatnej wersji próbnej lub zakupionej licencji dla Aspose.Cells. Możesz uzyskać tymczasową licencję[Tutaj](https://purchase.aspose.com/temporary-license/) lub sprawdź opcje zakupu[Tutaj](https://purchase.aspose.com/buy).
## Importuj pakiety
W swoim kodzie musisz zaimportować Aspose.Cells, aby wykorzystać jego klasy i metody:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Zanurzmy się w kodzie! Podzielimy zadanie kopiowania danych w skoroszycie przy użyciu Aspose.Cells dla .NET na łatwe do wykonania kroki.
## Krok 1: Skonfiguruj ścieżki katalogów
Zanim zaczniemy obsługiwać skoroszyt, określmy, gdzie znajdują się nasze pliki i gdzie chcemy zapisać dane wyjściowe. Ustawienie ścieżki katalogu pozwala zachować porządek.
```csharp
// Ustaw ścieżkę katalogu dla dokumentów.
string dataDir = "Your Document Directory";
string inputPath = dataDir + "book1.xls";
```
 Tutaj zamień`"Your Document Directory"` z rzeczywistą ścieżką, w której przechowywany jest Twój skoroszyt. Ta zmienna ścieżki ułatwi odwoływanie się do plików wejściowych i wyjściowych.
## Krok 2: Otwórz istniejący plik Excel
Aby pracować z plikiem Excel, musimy załadować go do obiektu skoroszytu w Aspose.Cells. Ten krok otwiera plik, z którego chcesz skopiować dane.
```csharp
// Otwórz istniejący plik Excela.
Workbook wb = new Workbook(inputPath);
```
 Dzięki temu nasz`Workbook` obiekt`wb` jest teraz gotowy do interakcji z zawartością`book1.xls`.
## Krok 3: Uzyskaj dostęp do kolekcji arkuszy roboczych
 Teraz, gdy skoroszyt jest otwarty, uzyskamy dostęp do jego zbioru arkuszy.`WorksheetCollection` Klasa ta pomaga nam pracować z wieloma arkuszami w skoroszycie.
```csharp
// Utwórz obiekt Arkusze, który odwołuje się do wszystkich arkuszy w skoroszycie.
WorksheetCollection sheets = wb.Worksheets;
```
 Tutaj,`sheets` umożliwi nam manipulowanie każdym arkuszem w skoroszycie, w tym dodawanie kopii istniejącego arkusza.
## Krok 4: Kopiowanie danych do nowego arkusza
Główną częścią naszego zadania jest skopiowanie zawartości jednego arkusza do nowego arkusza w tym samym skoroszycie. W tym przykładzie skopiujemy dane z „Arkusza1” do nowego arkusza.
```csharp
// Kopiuj dane z „Arkusza1” do nowego arkusza w skoroszycie.
sheets.AddCopy("Sheet1");
```
 Ten`AddCopy`Metoda tworzy dokładną kopię określonego arkusza, dołączając go do skoroszytu. Tutaj duplikujemy „Arkusz1”. Możesz określić nazwę dowolnego arkusza, który chcesz skopiować.
## Krok 5: Zapisz skoroszyt z nowym arkuszem
Po skopiowaniu arkusza zapisz skoroszyt pod nową nazwą lub w nowej lokalizacji, aby zachować zmiany.
```csharp
// Zapisz skoroszyt ze skopiowanymi danymi.
wb.Save(dataDir + "CopyWithinWorkbook_out.xls");
```
 Ten wiersz zapisuje zmodyfikowany skoroszyt jako`CopyWithinWorkbook_out.xls` w określonym katalogu.
## Wniosek
I masz to! Kopiowanie danych w skoroszycie za pomocą Aspose.Cells dla .NET jest dziecinnie proste. Aspose.Cells sprawia, że obsługa plików Excel jest prosta i pozwala na łatwe wykonywanie złożonych zadań zarządzania danymi. Niezależnie od tego, czy potrzebujesz duplikować arkusze do użycia szablonu, tworzenia kopii zapasowych czy tworzenia nowych wersji, omówione przez nas kroki pomogą Ci osiągnąć Twoje cele.
 Jeśli chcesz dowiedzieć się więcej, sprawdź[Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/net/) aby uzyskać dostęp do zaawansowanych funkcji i możliwości.
## Najczęściej zadawane pytania
### Czy mogę kopiować wiele arkuszy jednocześnie?
Aspose.Cells nie obsługuje kopiowania wielu arkuszy w jednym wywołaniu, ale możesz przechodzić przez arkusze, które chcesz zduplikować, i kopiować je pojedynczo.
### Czy mogę zmienić nazwę skopiowanego arkusza?
 Tak, po skopiowaniu arkusza możesz zmienić jego nazwę za pomocą`sheets[sheets.Count - 1].Name = "NewSheetName";`.
### Czy Aspose.Cells jest kompatybilny z .NET Core?
Oczywiście! Aspose.Cells obsługuje zarówno środowiska .NET Framework, jak i .NET Core.
### Jak radzić sobie z formatowaniem podczas kopiowania arkuszy?
 Ten`AddCopy` Metoda ta zachowuje całą zawartość i formatowanie, dzięki czemu skopiowany arkusz będzie wyglądał dokładnie tak samo jak oryginał.
### Co zrobić, jeśli chcę skopiować arkusz do innego skoroszytu?
Możesz użyć`Copy` metoda z odwołaniem do innego skoroszytu, np.`sheets.Add().Copy(wb.Worksheets["Sheet1"]);`.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
