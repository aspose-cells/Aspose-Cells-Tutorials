---
title: Zezwalaj użytkownikom na edycję zakresów w arkuszu kalkulacyjnym za pomocą Aspose.Cells
linktitle: Zezwalaj użytkownikom na edycję zakresów w arkuszu kalkulacyjnym za pomocą Aspose.Cells
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Naucz się tworzyć edytowalne zakresy w arkuszach kalkulacyjnych programu Excel za pomocą pakietu Aspose.Cells for .NET, umożliwiając edycję wybranych komórek i zabezpieczając resztę za pomocą ochrony arkusza kalkulacyjnego.
weight: 10
url: /pl/net/worksheet-security/allow-edit-ranges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zezwalaj użytkownikom na edycję zakresów w arkuszu kalkulacyjnym za pomocą Aspose.Cells

## Wstęp
Dokumenty programu Excel często zawierają poufne dane lub ustrukturyzowaną zawartość, którą chcesz chronić przed niechcianą edycją. Mogą jednak istnieć określone komórki lub zakresy, które chcesz udostępnić do edycji określonym użytkownikom. W tym miejscu Aspose.Cells for .NET wkracza jako potężne narzędzie, które pozwala chronić cały arkusz kalkulacyjny, jednocześnie udzielając uprawnień do edycji wyznaczonym zakresom. Wyobraź sobie udostępnianie arkusza kalkulacyjnego budżetu, w którym tylko niektóre komórki są edytowalne, a inne pozostają bezpieczne — Aspose.Cells ułatwia to i usprawnia.
## Wymagania wstępne
Zanim przejdziemy do kodowania, upewnijmy się, że masz wszystko, czego potrzebujesz:
-  Aspose.Cells dla .NET: Upewnij się, że zainstalowałeś bibliotekę Aspose.Cells dla .NET. Możesz ją pobrać[Tutaj](https://releases.aspose.com/cells/net/).
- Środowisko programistyczne: Visual Studio lub dowolne środowisko IDE zgodne z C#.
- .NET Framework: wersja 4.0 lub nowsza.
- Licencja: Rozważ uzyskanie licencji, aby uniknąć ograniczeń dotyczących okresu próbnego. Możesz uzyskać[tymczasowa licencja tutaj](https://purchase.aspose.com/temporary-license/).
## Importuj pakiety
Pamiętaj o uwzględnieniu niezbędnej przestrzeni nazw Aspose.Cells na początku kodu:
```csharp
using System.IO;
using Aspose.Cells;
```
Dzięki temu będziesz mieć dostęp do wszystkich klas i metod wymaganych do skonfigurowania chronionych zakresów w plikach Excela.
Teraz, gdy już mamy podstawy, możemy omówić kod szczegółowo, krok po kroku.
## Krok 1: Skonfiguruj katalog
Przed rozpoczęciem pracy z plikami musisz skonfigurować katalog, w którym zapiszesz plik Excela. Dzięki temu pliki będą dobrze zorganizowane i bezpiecznie przechowywane.
```csharp
// Zdefiniuj ścieżkę do katalogu dokumentów
string dataDir = "Your Document Directory";
// Sprawdź czy katalog istnieje, jeśli nie, utwórz go
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
Ta część kodu zapewnia, że katalog jest gotowy do operacji na plikach. Pomyśl o tym jako o położeniu fundamentu pod wszystko, co następuje.
## Krok 2: Zainicjuj skoroszyt i arkusz kalkulacyjny
Teraz utworzymy nowy skoroszyt i uzyskamy dostęp do jego domyślnego arkusza.
```csharp
// Zainicjuj nowy skoroszyt
Workbook book = new Workbook();
// Uzyskaj dostęp do pierwszego arkusza w skoroszycie
Worksheet sheet = book.Worksheets[0];
```
Tutaj inicjujemy skoroszyt programu Excel i wybieramy pierwszy arkusz w nim zawarty. Ten arkusz będzie płótnem, w którym zastosujemy nasze ustawienia ochrony i zdefiniujemy edytowalne zakresy.
## Krok 3: Uzyskaj dostęp do kolekcji Zezwalaj na edycję zakresów
 Aspose.Cells ma funkcję o nazwie`AllowEditRanges`, który jest zbiorem zakresów, które można edytować, nawet gdy arkusz kalkulacyjny jest chroniony.
```csharp
// Uzyskaj dostęp do kolekcji Zezwalaj na edycję zakresów
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
Ten wiersz ustawia dostęp do specjalnej kolekcji zakresów, które będą edytowalne. Pomyśl o tym jak o obszarze „VIP” w arkuszu kalkulacyjnym, gdzie tylko określone zakresy mogą ominąć ochronę.
## Krok 4: Zdefiniuj i utwórz zakres chroniony
Teraz zdefiniujmy i utwórzmy chroniony zakres w naszym arkuszu kalkulacyjnym. Określimy komórki początkowe i końcowe dla tego zakresu.
```csharp
// Zdefiniuj zmienną ProtectedRange
ProtectedRange protectedRange;
// Dodaj nowy zakres do kolekcji z określoną nazwą i pozycjami komórek
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
W tym bloku kodu:
- `EditableRange` jest nazwą przypisaną zakresowi.
- Liczby (1, 1, 3, 3) określają współrzędne zakresu, co oznacza, że zaczyna się on od komórki B2 (wiersz 1, kolumna 1) i kończy się na komórce D4 (wiersz 3, kolumna 3).
## Krok 5: Ustaw hasło dla zakresu chronionego
Aby zwiększyć bezpieczeństwo, możesz ustawić hasło dla chronionego zakresu. Ten krok dodaje dodatkową warstwę ochrony, aby zapewnić, że tylko autoryzowani użytkownicy mogą edytować zakres.
```csharp
// Ustaw hasło dla zakresu edytowalnego
protectedRange.Password = "123";
```
Tutaj dodaliśmy hasło (`"123"`) do chronionego zakresu. Ten wymóg hasła zapewnia dodatkowy poziom kontroli nad tym, kto może wprowadzać zmiany.
## Krok 6: Chroń arkusz kalkulacyjny
Mając już ustalony zakres edytowalny, następnym krokiem jest ochrona całego arkusza kalkulacyjnego. To ustawienie ochrony zapewni, że wszystkie komórki poza zdefiniowanym zakresem zostaną zablokowane i nie będą edytowalne.
```csharp
// Zastosuj ochronę arkusza kalkulacyjnego, uniemożliwiając edycję wszystkich pozostałych komórek
sheet.Protect(ProtectionType.All);
```
 Ten`Protect`Metoda blokuje cały arkusz roboczy, z wyjątkiem zakresów, które zdefiniowaliśmy jako edytowalne. Ten krok zasadniczo tworzy bezpieczne środowisko „tylko do odczytu”, z dostępem do określonych komórek w razie potrzeby.
## Krok 7: Zapisz skoroszyt
Ostatnim krokiem jest zapisanie skoroszytu, aby ustawienia zostały zastosowane i zapisane.
```csharp
// Zapisz plik Excela w określonym katalogu
book.Save(dataDir + "protectedrange.out.xls");
```
W tym kroku zapisujemy nasz skoroszyt pod nazwą „protectedrange.out.xls” w katalogu, który skonfigurowaliśmy w kroku 1. Teraz masz w pełni funkcjonalny, bezpieczny plik Excela, w którym można edytować tylko określone zakresy!
## Wniosek
Aspose.Cells for .NET zapewnia doskonały sposób zarządzania ochroną i uprawnieniami w plikach Excel. Tworząc edytowalne zakresy, możesz zabezpieczyć arkusze kalkulacyjne, jednocześnie umożliwiając dostęp do określonych obszarów. Ta funkcjonalność jest szczególnie przydatna w przypadku dokumentów grupowych, w których tylko kilka komórek powinno być otwartych do edycji, a inne powinny pozostać zablokowane.
## Najczęściej zadawane pytania
### Czy mogę dodać do arkusza kalkulacyjnego wiele zakresów edytowalnych?
Tak, możesz dodać wiele zakresów, po prostu powtarzając`allowRanges.Add()` metodę dla każdego nowego zakresu.
### Co się stanie, jeśli później będę chciał usunąć chroniony zakres?
 Użyj`allowRanges.RemoveAt()` metodę z indeksem zakresu, który chcesz usunąć.
### Czy mogę ustawić różne hasła dla każdego zakresu?
 Absolutnie. Każdy`ProtectedRange` może mieć własne, unikalne hasło, co zapewni Ci szczegółową kontrolę.
### Co się stanie, jeśli zabezpieczę arkusz kalkulacyjny bez żadnych zakresów edytowalnych?
Jeśli nie zdefiniujesz zakresów edytowalnych, cały arkusz kalkulacyjny stanie się nieedytowalny po włączeniu ochrony.
### Czy zakres chroniony jest widoczny dla innych użytkowników?
Nie, ochrona jest wewnętrzna. Użytkownicy będą proszeni o podanie hasła tylko wtedy, gdy spróbują edytować chroniony obszar.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
