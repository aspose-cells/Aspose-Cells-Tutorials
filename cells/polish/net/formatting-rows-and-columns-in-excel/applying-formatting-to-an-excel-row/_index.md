---
"description": "Dowiedz się, jak programowo stosować formatowanie do wiersza programu Excel, używając Aspose.Cells dla .NET. Ten szczegółowy przewodnik krok po kroku obejmuje wszystko, od wyrównania po obramowania."
"linktitle": "Stosowanie formatowania do wiersza programu Excel programowo"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Stosowanie formatowania do wiersza programu Excel programowo"
"url": "/pl/net/formatting-rows-and-columns-in-excel/applying-formatting-to-an-excel-row/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Stosowanie formatowania do wiersza programu Excel programowo

## Wstęp
W tym samouczku pokażemy, jak programowo zastosować formatowanie do wiersza programu Excel, używając Aspose.Cells dla .NET. Omówimy wszystko, od konfiguracji środowiska po stosowanie różnych opcji formatowania, takich jak kolor czcionki, wyrównanie i obramowanie — wszystko to przy zachowaniu prostoty i zaangażowania. Zanurzmy się!
## Wymagania wstępne
Zanim zaczniemy, upewnijmy się, że masz wszystko, czego potrzebujesz, aby śledzić ten samouczek. Oto, czego będziesz potrzebować:
1. Biblioteka Aspose.Cells dla .NET – Można ją pobrać ze strony [Strona pobierania Aspose.Cells dla .NET](https://releases.aspose.com/cells/net/).
2. IDE – dowolne środowisko programistyczne .NET, np. Visual Studio.
3. Podstawowa znajomość języka C# – Powinieneś znać język programowania C# i pracować z aplikacjami .NET.
Pamiętaj również o zainstalowaniu najnowszej wersji pakietu Aspose.Cells, pobierając ją bezpośrednio lub korzystając z Menedżera pakietów NuGet w programie Visual Studio.
## Importuj pakiety
Na początek upewnij się, że importujesz niezbędne pakiety. Jest to niezbędne do uzyskania dostępu do funkcjonalności wymaganej do pracy z plikami Excel i stosowania stylów programowo.
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Po zakończeniu konfiguracji możemy przejść do ekscytującej części — formatowania wierszy!
W tej sekcji omówimy każdy krok procesu. Każdemu krokowi będą towarzyszyć fragmenty kodu i szczegółowe wyjaśnienie, więc nawet jeśli jesteś nowy w Aspose.Cells, będziesz w stanie łatwo śledzić.
## Krok 1: Skonfiguruj skoroszyt i arkusz kalkulacyjny
Przed zastosowaniem jakiegokolwiek formatowania musisz utworzyć wystąpienie skoroszytu i uzyskać dostęp do pierwszego arkusza. To jak otwarcie pustego płótna przed rozpoczęciem malowania.
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
// Utwórz katalog, jeśli jeszcze go nie ma.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Tworzenie instancji obiektu skoroszytu
Workbook workbook = new Workbook();
// Uzyskanie odniesienia do pierwszego (domyślnego) arkusza roboczego poprzez przekazanie jego indeksu arkusza
Worksheet worksheet = workbook.Worksheets[0];
```
Tutaj tworzymy nowy obiekt skoroszytu i pobieramy pierwszy arkusz. To jest arkusz, w którym zastosujemy nasze formatowanie.
## Krok 2: Utwórz i dostosuj styl
Teraz, gdy masz już gotowy arkusz kalkulacyjny, następnym krokiem jest zdefiniowanie stylów, które chcesz zastosować do wiersza. Zaczniemy od utworzenia nowego stylu i ustawienia właściwości, takich jak kolor czcionki, wyrównanie i obramowanie.
```csharp
// Dodawanie nowego stylu do stylów
Style style = workbook.CreateStyle();
// Ustawianie pionowego wyrównania tekstu w komórce „A1”
style.VerticalAlignment = TextAlignmentType.Center;
// Ustawianie poziomego wyrównania tekstu w komórce „A1”
style.HorizontalAlignment = TextAlignmentType.Center;
// Ustawianie koloru czcionki tekstu w komórce „A1”
style.Font.Color = Color.Green;
```
W tej części ustawiamy wyrównanie tekstu w wierszu (zarówno w pionie, jak i w poziomie) i określamy kolor czcionki. To tutaj zaczynasz definiować, jak treść będzie wyglądać wizualnie w arkuszu Excela.
## Krok 3: Zastosuj opcję „Skurcz, aby dopasować”
Czasami tekst w komórce może być za długi, powodując jej przepełnienie. Sprytnym trikiem jest zmniejszenie tekstu, aby zmieścił się w komórce, zachowując jednocześnie czytelność.
```csharp
// Zmniejszanie tekstu w celu dopasowania go do komórki
style.ShrinkToFit = true;
```
Z `ShrinkToFit`, masz pewność, że długi tekst zostanie dostosowany tak, aby mieścił się w granicach komórki, dzięki czemu arkusz programu Excel będzie wyglądał na bardziej uporządkowany.
## Krok 4: Ustaw obramowania dla wiersza
Aby wyróżnić wiersze, świetnym rozwiązaniem jest zastosowanie obramowań. W tym przykładzie dostosujemy dolną ramkę, ustawiając jej kolor na czerwony i styl na średni.
```csharp
// Ustawianie koloru dolnej krawędzi komórki na czerwony
style.Borders[BorderType.BottomBorder].Color = Color.Red;
// Ustawianie dolnej krawędzi komórki na średnią
style.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Medium;
```
Obramowania pomagają w wizualnym oddzieleniu treści, dzięki czemu dane są łatwiejsze do odczytania i bardziej estetyczne.
## Krok 5: Utwórz obiekt StyleFlag
Ten `StyleFlag` obiekt mówi Aspose.Cells, które aspekty stylu zastosować. Daje to precyzyjną kontrolę nad tym, co zostanie zastosowane i zapewnia, że ustawione zostanie tylko zamierzone formatowanie.
```csharp
// Tworzenie StyleFlag
StyleFlag styleFlag = new StyleFlag();
styleFlag.HorizontalAlignment = true;
styleFlag.VerticalAlignment = true;
styleFlag.ShrinkToFit = true;
styleFlag.Borders = true;
styleFlag.FontColor = true;
```
W tym przypadku określamy, że wyrównanie w poziomie i w pionie, kolor czcionki, zmniejszenie tekstu i obramowanie powinny zostać zastosowane.
## Krok 6: Uzyskaj dostęp do żądanego wiersza
Po utworzeniu stylu następnym krokiem jest dostęp do wiersza, w którym chcemy zastosować formatowanie. W tym przykładzie sformatujemy pierwszy wiersz (indeks wiersza 0).
```csharp
// Uzyskiwanie dostępu do wiersza z kolekcji Wiersze
Row row = worksheet.Cells.Rows[0];
```
Tutaj pobieramy pierwszy wiersz arkusza kalkulacyjnego. Możesz zmienić indeks, aby sformatować dowolny inny wiersz.
## Krok 7: Zastosuj styl do wiersza
Na koniec czas zastosować styl do wiersza! Używamy `ApplyStyle` metoda zastosowania zdefiniowanego stylu do wybranego wiersza.
```csharp
// Przypisywanie obiektu Style do właściwości Style wiersza
row.ApplyStyle(style, styleFlag);
```
Styl został zastosowany do całego wiersza, dzięki czemu dane wyglądają dokładnie tak, jak sobie wyobrażałeś.
## Krok 8: Zapisz skoroszyt
Po zakończeniu stosowania formatowania należy zapisać skoroszyt do pliku Excel. Jest to jak naciśnięcie „Zapisz” w programie Excel po wprowadzeniu zmian.
```csharp
// Zapisywanie pliku Excel
workbook.Save(dataDir + "book1.out.xls");
```
Masz teraz w pełni sformatowany arkusz programu Excel zapisany w określonym katalogu!
## Wniosek
To wszystko! W zaledwie kilku prostych krokach nauczyłeś się, jak programowo stosować formatowanie do wiersza programu Excel przy użyciu Aspose.Cells dla .NET. Od ustawiania wyrównania tekstu po dostosowywanie obramowań, ten samouczek obejmuje podstawowe elementy, które pomogą Ci programowo tworzyć profesjonalne i atrakcyjne wizualnie raporty programu Excel. 
Aspose.Cells oferuje szeroki zakres możliwości, a metody pokazane tutaj można łatwo rozszerzyć, aby zastosować bardziej złożone style i formatowanie do plików Excel. Więc dlaczego nie spróbować i nie sprawić, aby Twoje dane się wyróżniały?
## Najczęściej zadawane pytania
### Czy mogę zastosować różne style do poszczególnych komórek w wierszu?  
Tak, możesz stosować różne style do poszczególnych komórek, uzyskując do nich bezpośredni dostęp za pomocą `Cells` kolekcji zamiast stosowania stylu do całego wiersza.
### Czy można zastosować formatowanie warunkowe w Aspose.Cells?  
Oczywiście! Aspose.Cells obsługuje formatowanie warunkowe, co pozwala na definiowanie reguł na podstawie wartości komórek.
### Jak mogę zastosować formatowanie do wielu wierszy?  
Możesz przejść przez wiele wierszy za pomocą pętli `for` zapętlić i zastosować ten sam styl do każdego wiersza osobno.
### Czy Aspose.Cells obsługuje stosowanie stylów do całych kolumn?  
Tak, podobnie jak w przypadku wierszy, do kolumn można uzyskać dostęp za pomocą `Columns` kolekcję i stosować do nich style.
### Czy mogę używać Aspose.Cells z aplikacjami .NET Core?  
Tak, Aspose.Cells jest w pełni kompatybilny z platformą .NET Core, co pozwala na korzystanie z niego na różnych platformach.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}