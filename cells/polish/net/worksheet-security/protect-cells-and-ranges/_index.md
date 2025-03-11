---
title: Chroń komórki i zakresy w arkuszu kalkulacyjnym za pomocą Aspose.Cells
linktitle: Chroń komórki i zakresy w arkuszu kalkulacyjnym za pomocą Aspose.Cells
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak chronić komórki i zakresy w arkuszu kalkulacyjnym programu Excel za pomocą Aspose.Cells dla .NET. Postępuj zgodnie z tym przewodnikiem krok po kroku, aby zabezpieczyć arkusze kalkulacyjne.
weight: 11
url: /pl/net/worksheet-security/protect-cells-and-ranges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chroń komórki i zakresy w arkuszu kalkulacyjnym za pomocą Aspose.Cells

## Wstęp
Praca z arkuszami kalkulacyjnymi często wiąże się z ochroną niektórych części arkusza przed niechcianymi modyfikacjami, szczególnie w środowiskach współpracy. W tym samouczku zbadamy, jak chronić określone komórki i zakresy w arkuszu kalkulacyjnym za pomocą Aspose.Cells dla .NET. Przeprowadzimy Cię przez proces konfigurowania chronionego arkusza, określania, które zakresy są edytowalne, i zapisywania pliku. Może to być niezwykle przydatna funkcja, gdy chcesz ograniczyć dostęp do poufnych danych, jednocześnie umożliwiając innym osobom modyfikowanie niektórych sekcji.
## Wymagania wstępne
Zanim przejdziesz do samouczka, upewnij się, że spełnione są następujące wymagania wstępne:
1. Aspose.Cells dla .NET: Musisz mieć zainstalowaną bibliotekę Aspose.Cells w swoim projekcie. Jeśli jeszcze jej nie masz, możesz ją pobrać ze strony[Strona internetowa Aspose](https://releases.aspose.com/cells/net/).
2. Visual Studio: W tym przewodniku założono, że używasz programu Visual Studio lub podobnego środowiska IDE obsługującego programowanie w języku C#.
3. Podstawowa znajomość języka C#: Powinieneś znać podstawy programowania w języku C# i wiedzieć, jak skonfigurować projekt w programie Visual Studio.
4.  Licencja Aspose.Cells: Aspose oferuje bezpłatną wersję próbną, ale ważna licencja pozwoli Ci korzystać z pełnego zestawu funkcji biblioteki. Jeśli jej nie masz, możesz uzyskać[tymczasowa licencja tutaj](https://purchase.aspose.com/temporary-license/).
Gdy już będziesz mieć pewność, że wszystko powyżej jest gotowe, możemy przejść do części kodowania.
## Importuj pakiety
Aby pracować z Aspose.Cells, musisz najpierw zaimportować niezbędne przestrzenie nazw do pliku C#. Oto jak możesz je zaimportować:
```csharp
using System.IO;
using Aspose.Cells;
```
 Ten`Aspose.Cells` przestrzeń nazw zapewnia dostęp do podstawowych funkcji umożliwiających manipulowanie plikami programu Excel i`System.IO` służy do operacji na plikach, np. zapisywania skoroszytu.
Teraz przeanalizujemy szczegółowo kroki, które należy wykonać, aby chronić komórki i zakresy w arkuszu kalkulacyjnym przy użyciu Aspose.Cells.
## Krok 1: Skonfiguruj swoje środowisko
Najpierw utwórz katalog, w którym chcesz zapisać pliki Excela. Jeśli katalog jeszcze nie istnieje, utworzymy go. Pomaga to upewnić się, że masz miejsce do przechowywania pliku wyjściowego.
```csharp
// Zdefiniuj ścieżkę do katalogu dokumentów
string dataDir = "Your Document Directory";
// Sprawdź czy katalog istnieje, jeśli nie, utwórz go
bool IsExists = Directory.Exists(dataDir);
if (!IsExists)
    Directory.CreateDirectory(dataDir);
```
 Tutaj używamy`System.IO.Directory.Exists()` aby sprawdzić, czy folder istnieje, a jeśli nie, tworzymy go za pomocą`Directory.CreateDirectory()`.
## Krok 2: Utwórz nowy skoroszyt
Teraz utwórzmy nowy obiekt Workbook. Będzie on służył jako nasz plik Excel, w którym zdefiniujemy nasze komórki i zakresy.
```csharp
// Utwórz nowy obiekt skoroszytu
Workbook book = new Workbook();
```
 Ten`Workbook` Klasa jest punktem wejścia do pracy z plikami Excel w Aspose.Cells. Reprezentuje dokument Excel.
## Krok 3: Uzyskaj dostęp do domyślnego arkusza kalkulacyjnego
Każdy nowo utworzony skoroszyt ma domyślny arkusz. Pobierzemy go, aby pracować z jego zawartością.
```csharp
// Pobierz pierwszy (domyślny) arkusz w skoroszycie
Worksheet sheet = book.Worksheets[0];
```
 Tutaj,`Worksheets[0]` podaje nam pierwszy arkusz w skoroszycie (indeksowanie zaczyna się od 0).
## Krok 4: Zdefiniuj zakresy edytowalne
Aby chronić określone części arkusza kalkulacyjnego, a jednocześnie umożliwić użytkownikom edycję określonych komórek, musimy zdefiniować edytowalne zakresy. Utworzymy zakres, który można edytować, i dodamy go do kolekcji AllowEditRanges arkusza kalkulacyjnego.
```csharp
// Pobierz kolekcję AllowEditRanges
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
// Zdefiniuj ProtectedRange i dodaj go do kolekcji
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
ProtectedRange protectedRange = allowRanges[idx];
```
W powyższym kodzie:
- `"r2"` jest nazwą zakresu edytowalnego.
-  Księga Liczb`1, 1, 3, 3` reprezentują początkowe i końcowe indeksy wiersza i kolumny dla zakresu (tj. od komórki B2 do D4).
## Krok 5: Ustaw hasło dla zakresu chronionego
Teraz, gdy zdefiniowaliśmy zakres edytowalny, dodajmy hasło, aby go zabezpieczyć. Oznacza to, że użytkownicy będą potrzebować hasła, aby edytować ten konkretny zakres.
```csharp
// Podaj hasło dla zakresu edytowalnego
protectedRange.Password = "123";
```
 Tutaj ustawiliśmy hasło jako`"123"`, ale możesz wybrać dowolne bezpieczne hasło. Ten krok jest niezbędny do kontrolowania dostępu do obszarów edytowalnych.
## Krok 6: Zabezpiecz cały arkusz
Na tym etapie zabezpieczymy cały arkusz. Zabezpieczenie arkusza zapewnia, że inne części arkusza, z wyjątkiem dozwolonych zakresów, nie będą edytowalne.
```csharp
// Zabezpiecz arkusz określonym typem ochrony (Wszystkie)
sheet.Protect(ProtectionType.All);
```
Dzięki temu wszystkie komórki w arkuszu zostaną zablokowane, za wyjątkiem tych, które znajdują się w zakresach edytowalnych.
## Krok 7: Zapisz skoroszyt
Na koniec zapisujemy skoroszyt do pliku. Zabezpieczony arkusz zostanie zapisany pod nazwą, którą podasz.
```csharp
// Zapisz plik Excela w określonym katalogu
book.Save(dataDir + "protectedrange.out.xls");
```
 Tutaj plik Excel zostanie zapisany jako`protectedrange.out.xls` w katalogu, który zdefiniowaliśmy wcześniej. Jeśli chcesz zapisać go pod inną nazwą lub w innym formacie, możesz zmienić nazwę pliku i rozszerzenie.
## Wniosek
Dzięki temu samouczkowi nauczyłeś się, jak chronić komórki i zakresy w arkuszu kalkulacyjnym programu Excel za pomocą Aspose.Cells dla .NET. To podejście daje Ci elastyczność w kontrolowaniu, które obszary arkusza kalkulacyjnego można edytować, a których nie. Teraz możesz zastosować te umiejętności we własnych projektach, zapewniając bezpieczeństwo poufnych danych, a jednocześnie udostępniając użytkownikom obszary edytowalne.
Pamiętaj, że Aspose.Cells oferuje rozbudowany zestaw narzędzi do pracy z plikami Excela, a to tylko jedna z wielu rzeczy, które możesz dzięki niemu zrobić. 
## Najczęściej zadawane pytania
### Czy mogę chronić tylko wybrane komórki w arkuszu kalkulacyjnym?
 Tak, korzystając z`AllowEditRanges` Właściwość umożliwia określenie, które komórki lub zakresy można edytować, podczas gdy reszta arkusza kalkulacyjnego pozostanie chroniona.
### Czy mogę później usunąć zabezpieczenie?
 Tak, możesz usunąć ochronę arkusza kalkulacyjnego za pomocą`Unprotect()` metodę, a jeśli hasło zostało ustawione, będziesz musiał je podać.
### Jak zabezpieczyć cały arkusz hasłem?
 Aby zabezpieczyć cały arkusz, wystarczy użyć`Protect()` metoda z hasłem lub bez. Na przykład,`sheet.Protect("password")`.
### Czy mogę dodać wiele zakresów edytowalnych?
 Oczywiście! Możesz dodać tyle edytowalnych zakresów, ile potrzebujesz, dzwoniąc`allowRanges.Add()` wiele razy.
### Jakie inne funkcje bezpieczeństwa oferuje Aspose.Cells?
Aspose.Cells obsługuje różne funkcje bezpieczeństwa, takie jak szyfrowanie skoroszytów, ustawianie haseł do plików oraz ochrona komórek i arkuszy.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
