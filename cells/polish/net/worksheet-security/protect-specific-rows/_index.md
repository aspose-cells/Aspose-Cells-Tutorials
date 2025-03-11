---
title: Chroń określone wiersze w arkuszu kalkulacyjnym za pomocą Aspose.Cells
linktitle: Chroń określone wiersze w arkuszu kalkulacyjnym za pomocą Aspose.Cells
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak chronić określone wiersze w arkuszu kalkulacyjnym programu Excel za pomocą Aspose.Cells dla .NET dzięki temu przewodnikowi krok po kroku. Zabezpiecz swoje dane skutecznie.
weight: 16
url: /pl/net/worksheet-security/protect-specific-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chroń określone wiersze w arkuszu kalkulacyjnym za pomocą Aspose.Cells

## Wstęp
tym samouczku przeprowadzimy Cię przez proces ochrony określonych wierszy w arkuszu kalkulacyjnym programu Excel przy użyciu Aspose.Cells dla .NET. Przeprowadzimy Cię przez każdy krok szczegółowo, omawiając wymagania wstępne, importując wymagane pakiety i dzieląc kod na łatwe do naśladowania instrukcje. Na koniec będziesz wyposażony w wiedzę, aby stosować ochronę wierszy we własnych aplikacjach.
## Wymagania wstępne
Zanim przejdziesz do wdrażania, musisz spełnić kilka warunków wstępnych, aby móc korzystać z tego samouczka:
1. Aspose.Cells dla .NET: Musisz mieć zainstalowany Aspose.Cells dla .NET. Jeśli jeszcze go nie zainstalowałeś, możesz pobrać najnowszą wersję, odwiedzając witrynę Aspose.
2. Podstawowe zrozumienie C# i .NET: Ten samouczek zakłada, że znasz C# i posiadasz podstawową wiedzę na temat programowania .NET. Jeśli nie jesteś z nimi zaznajomiony, możesz najpierw sprawdzić niektóre wprowadzające zasoby.
3. Visual Studio lub dowolne IDE .NET: Będziesz potrzebować zintegrowanego środowiska programistycznego (IDE), takiego jak Visual Studio, aby uruchomić kod. Zapewnia ono wszystkie niezbędne narzędzia i możliwości debugowania.
4. Licencja Aspose.Cells: Jeśli chcesz uniknąć ograniczeń wersji ewaluacyjnej, upewnij się, że masz ważną licencję Aspose.Cells. Możesz również użyć licencji tymczasowej, jeśli dopiero zaczynasz.
 Aby uzyskać szczegółowe informacje na temat Aspose.Cells i instalacji, możesz sprawdzić ich stronę[dokumentacja](https://reference.aspose.com/cells/net/).
## Importuj pakiety
Aby rozpocząć korzystanie z Aspose.Cells, musisz zaimportować niezbędne przestrzenie nazw w swoim projekcie C#. Te przestrzenie nazw zapewniają dostęp do klas i metod wymaganych do manipulowania plikami Excel.
Oto jak zaimportować wymagane przestrzenie nazw:
```csharp
using System.IO;
using Aspose.Cells;
```
Tego typu importy są niezwykle istotne, gdyż zapewniają dostęp do funkcjonalności Aspose.Cells i pozwalają na interakcję z plikami programu Excel w projekcie .NET.
Teraz, gdy masz już skonfigurowane wymagania wstępne i niezbędne importy, czas zagłębić się w rzeczywisty kod. Podzielimy proces na kilka kroków, aby zapewnić przejrzystość.
## Krok 1: Skonfiguruj katalog swojego projektu
W każdym programie organizacja plików jest kluczowa. Najpierw utwórzmy katalog, w którym możemy przechowywać skoroszyt. Sprawdzamy, czy katalog istnieje i tworzymy go, jeśli to konieczne.
```csharp
// Zdefiniuj ścieżkę do katalogu dokumentów.
string dataDir = "Your Document Directory";
// Utwórz katalog, jeśli jeszcze go nie ma.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tutaj definiujesz ścieżkę, w której będą przechowywane Twoje pliki Excela. Jeśli folder nie istnieje, tworzymy go. Ten krok jest kluczowy dla zapewnienia, że Twój skoroszyt ma miejsce do zapisania.
## Krok 2: Utwórz nowy skoroszyt
 Następnie tworzymy nowy skoroszyt, używając`Workbook` klasa. Ta klasa zapewnia wszystkie funkcjonalności wymagane do pracy z plikami Excel.
```csharp
// Utwórz nowy skoroszyt.
Workbook wb = new Workbook();
```
W tym momencie mamy nowy skoroszyt, z którym możemy pracować.
## Krok 3: Uzyskaj dostęp do arkusza kalkulacyjnego
Teraz uzyskujemy dostęp do pierwszego arkusza nowo utworzonego skoroszytu. Skoroszyt może zawierać wiele arkuszy, ale w tym przypadku skupiamy się na pierwszym.
```csharp
// Utwórz obiekt arkusza kalkulacyjnego i uzyskaj pierwszy arkusz.
Worksheet sheet = wb.Worksheets[0];
```
 Tutaj,`Worksheets[0]` odnosi się do pierwszego arkusza w skoroszycie (którego indeksowanie zaczyna się od 0).
## Krok 4: Odblokuj wszystkie kolumny
programie Excel komórki są domyślnie blokowane, gdy arkusz jest chroniony. Jeśli chcesz chronić określone wiersze, musisz najpierw odblokować kolumny. W tym kroku przechodzimy przez wszystkie kolumny i odblokowujemy je.
```csharp
// Zdefiniuj obiekt stylu.
Style style;
// Zdefiniuj obiekt styleflag.
StyleFlag flag;
// Przejdź przez wszystkie kolumny arkusza i odblokuj je.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
Tutaj przechodzimy przez kolumny od 0 do 255 (całkowita liczba kolumn w arkuszu kalkulacyjnym programu Excel) i odblokowujemy je. Dzięki temu możemy nadal wchodzić w interakcje z wierszami, które chcemy chronić, podczas gdy inne pozostają zablokowane.
## Krok 5: Zablokuj pierwszy rząd
Teraz, gdy wszystkie kolumny są odblokowane, możemy przejść do ochrony wierszy. W tym kroku blokujemy pierwszy wiersz, co sprawi, że będzie on nieedytowalny po zabezpieczeniu arkusza.
```csharp
//Pobierz styl pierwszego rzędu.
style = sheet.Cells.Rows[0].Style;
// Zamknij to.
style.IsLocked = true;
//Utwórz instancję flagi.
flag = new StyleFlag();
// Ustaw ustawienie blokady.
flag.Locked = true;
// Zastosuj styl do pierwszego wiersza.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Ten kod blokuje pierwszy wiersz, zapewniając jego ochronę po zastosowaniu ochrony do arkusza.
## Krok 6: Chroń arkusz kalkulacyjny
W tym momencie jesteśmy gotowi, aby zabezpieczyć arkusz kalkulacyjny. Ten krok stosuje ustawienia ochrony do całego arkusza kalkulacyjnego, upewniając się, że żadne zablokowane komórki nie mogą być edytowane.
```csharp
// Chroń arkusz.
sheet.Protect(ProtectionType.All);
```
 Za pomocą`ProtectionType.All`upewniamy się, że wszystkie komórki, z wyjątkiem tych wyraźnie odblokowanych (jak nasze kolumny), są chronione. To jest krok, który stosuje ochronę do arkusza kalkulacyjnego.
## Krok 7: Zapisz plik Excel
Na koniec, po zastosowaniu ochrony, zapisujemy skoroszyt. Możesz określić format, w jakim chcesz zapisać plik. W tym przykładzie zapisujemy skoroszyt jako plik Excel 97-2003.
```csharp
// Zapisz plik Excela.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Ten krok zapisuje plik w określonej ścieżce, co kończy zadanie ochrony konkretnych wierszy w arkuszu kalkulacyjnym.
## Wniosek
Ochrona określonych wierszy w arkuszu kalkulacyjnym programu Excel za pomocą Aspose.Cells dla .NET to prosty proces, gdy rozłożysz go na części. Odblokowując kolumny, blokując określone wiersze i stosując ustawienia ochrony, zapewniasz, że Twoje dane pozostaną bezpieczne i edytowalne tylko wtedy, gdy będzie to konieczne. Ten samouczek obejmuje wszystkie kluczowe kroki, od skonfigurowania katalogu projektu po zapisanie ostatecznego skoroszytu.
Niezależnie od tego, czy tworzysz szablony, raporty czy interaktywne arkusze kalkulacyjne, korzystanie z ochrony wierszy jest prostym, ale skutecznym sposobem na zachowanie kontroli nad danymi. Wypróbuj ten proces we własnych projektach i odkryj pełny potencjał Aspose.Cells dla .NET.
## Najczęściej zadawane pytania
### Czy mogę chronić wiele wierszy w arkuszu kalkulacyjnym?  
Tak, możesz zastosować te same kroki ochrony do wielu wierszy, modyfikując pętlę lub stosując style do innych wierszy.
### Co się stanie, jeśli nie odblokuję żadnej kolumny przed włączeniem ochrony arkusza?  
Jeśli nie odblokujesz kolumn, po włączeniu ochrony arkusza zostaną one zablokowane, a użytkownicy nie będą mogli z nich korzystać.
### Jak mogę odblokować konkretne komórki zamiast całych kolumn?  
 Możesz odblokować określone komórki, uzyskując dostęp do ich stylu i ustawiając`IsLocked` nieruchomość do`false`.
### Czy mogę użyć tej metody do ochrony całych arkuszy kalkulacyjnych?  
Tak, możesz zabezpieczyć cały arkusz kalkulacyjny, stosując ochronę do wszystkich komórek i nie pozostawiając żadnej komórki odblokowanej.
### Jak mogę usunąć ochronę arkusza kalkulacyjnego?  
 Możesz usunąć ochronę dzwoniąc pod numer`Unprotect`metodę na arkuszu kalkulacyjnym i podając hasło zabezpieczające (jeśli zostało ustawione).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
