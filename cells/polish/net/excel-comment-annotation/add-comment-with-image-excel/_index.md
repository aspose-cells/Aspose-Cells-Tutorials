---
title: Dodaj komentarz z obrazem w programie Excel
linktitle: Dodaj komentarz z obrazem w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak dodawać komentarze do obrazów w programie Excel za pomocą Aspose.Cells dla platformy .NET. Ulepsz swoje arkusze kalkulacyjne dzięki spersonalizowanym adnotacjom.
weight: 10
url: /pl/net/excel-comment-annotation/add-comment-with-image-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj komentarz z obrazem w programie Excel

## Wstęp
Excel to potężne narzędzie do zarządzania danymi i analizowania ich, ale czasami trzeba dodać osobisty akcent do arkuszy kalkulacyjnych, prawda? Może chcesz opatrzyć dane adnotacjami, przekazać informacje zwrotne, a nawet dodać odrobinę elegancji za pomocą obrazów. W tym miejscu przydają się komentarze! W tym samouczku pokażemy, jak dodać komentarz z obrazem w programie Excel, korzystając z biblioteki Aspose.Cells dla platformy .NET. To podejście może być szczególnie przydatne do tworzenia bardziej interaktywnych i atrakcyjnych wizualnie arkuszy kalkulacyjnych.
## Wymagania wstępne
Zanim zagłębimy się w szczegóły dodawania komentarzy do obrazów w programie Excel, upewnijmy się, że masz wszystko, czego potrzebujesz, aby zacząć:
1. Visual Studio: Upewnij się, że masz zainstalowany Visual Studio na swoim komputerze. Tutaj będziesz pisać i wykonywać swój kod.
2.  Aspose.Cells dla .NET: Musisz mieć bibliotekę Aspose.Cells. Jeśli jeszcze jej nie zainstalowałeś, możesz ją pobrać z[Tutaj](https://releases.aspose.com/cells/net/).
3. Podstawowa wiedza o języku C#: Znajomość programowania w języku C# pomoże Ci lepiej zrozumieć fragmenty kodu.
4. Plik obrazu: Przygotuj plik obrazu (np. logo), który chcesz osadzić w komentarzu programu Excel. W tym samouczku założymy, że masz plik o nazwie`logo.jpg`.
5. .NET Framework: Upewnij się, że masz zainstalowany .NET Framework, ponieważ Aspose.Cells wymaga go do prawidłowego działania.
Teraz, gdy omówiliśmy już nasze wymagania wstępne, możemy zająć się kodowaniem!
## Importuj pakiety
Po pierwsze, musimy zaimportować niezbędne pakiety. W swoim projekcie C# upewnij się, że dodałeś odwołanie do biblioteki Aspose.Cells. Możesz to zrobić, używając NuGet Package Manager w Visual Studio. Oto jak to zrobić:
1. Otwórz program Visual Studio.
2. Utwórz nowy projekt lub otwórz istniejący.
3. Kliknij prawym przyciskiem myszy swój projekt w Eksploratorze rozwiązań.
4. Wybierz opcję Zarządzaj pakietami NuGet.
5. Wyszukaj Aspose.Cells i zainstaluj.

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Po zainstalowaniu biblioteki możesz zacząć pisać swój kod. Oto jak to zrobić krok po kroku.
## Krok 1: Skonfiguruj katalog dokumentów
Na początek musimy utworzyć katalog, w którym będziemy mogli zapisywać nasze pliki Excel. Jest to kluczowy krok, ponieważ chcemy zachować porządek w naszej pracy.
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
// Utwórz katalog, jeśli jeszcze go nie ma.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Ta zmienna przechowuje ścieżkę do katalogu dokumentów. Zastąp`"Your Document Directory"` z rzeczywistą ścieżką, pod którą chcesz zapisać plik Excela.
- Directory.Exists: sprawdza, czy katalog już istnieje.
- Directory.CreateDirectory: Jeżeli katalog nie istnieje, to polecenie go utworzy.
## Krok 2: Utwórz skoroszyt
 Następnie musimy utworzyć instancję`Workbook` klasa. Ta klasa reprezentuje skoroszyt programu Excel w pamięci.
```csharp
//Utwórz instancję skoroszytu
Workbook workbook = new Workbook();
```
- Workbook: To główna klasa w Aspose.Cells, która umożliwia tworzenie i manipulowanie plikami Excel. Tworząc ją, zasadniczo tworzysz nowy skoroszyt Excel.
## Krok 3: Pobierz kolekcję komentarzy
Teraz, gdy mamy już skoroszyt, możemy uzyskać dostęp do zbioru komentarzy pierwszego arkusza.
```csharp
// Uzyskaj odniesienie do zbioru komentarzy z pierwszym arkuszem
CommentCollection comments = workbook.Worksheets[0].Comments;
```
- Arkusze robocze[ 0]: Uzyskuje dostęp do pierwszego arkusza w skoroszycie. Pamiętaj, że indeks jest zerowy, więc`[0]` odnosi się do pierwszego arkusza.
- Komentarze: Ta właściwość daje nam dostęp do zbioru komentarzy w danym arkuszu kalkulacyjnym.
## Krok 4: Dodaj komentarz do komórki
Dodajmy komentarz do konkretnej komórki. W tym przypadku dodamy komentarz do komórki A1.
```csharp
// Dodaj komentarz do komórki A1
int commentIndex = comments.Add(0, 0);
Comment comment = comments[commentIndex];
comment.Note = "First note.";
comment.Font.Name = "Times New Roman";
```
- comments.Add(0, 0): Ta metoda dodaje komentarz do komórki A1 (wiersz 0, kolumna 0).
- komentarz.Uwaga: Tutaj ustawiamy tekst komentarza.
- comment.Font.Name: Ustawia czcionkę tekstu komentarza.
## Krok 5: Załaduj obraz do strumienia
 Teraz czas załadować obraz, który chcemy osadzić w naszym komentarzu. Użyjemy`MemoryStream` do przechowywania danych obrazu.
```csharp
// Załaduj obraz do strumienia
Bitmap bmp = new Bitmap(dataDir + "logo.jpg");
MemoryStream ms = new MemoryStream();
bmp.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
```
- Bitmap: Ta klasa jest używana do ładowania pliku obrazu. Upewnij się, że ścieżka jest poprawna.
- MemoryStream: To strumień, którego użyjemy do zapisania obrazu w pamięci.
- bmp.Save: Zapisuje obraz bitmapowy w strumieniu pamięci w formacie PNG.
## Krok 6: Ustaw dane obrazu na kształt komentarza
Teraz musimy ustawić dane obrazu na kształt skojarzony z komentarzem, który utworzyliśmy wcześniej.
```csharp
// Ustaw dane obrazu na kształt skojarzony z komentarzem
comment.CommentShape.Fill.ImageData = ms.ToArray();
```
- comment.CommentShape.Fill.ImageData: Ta właściwość pozwala ustawić obraz dla kształtu komentarza. Konwertujemy`MemoryStream` do tablicy bajtów za pomocą`ms.ToArray()`.
## Krok 7: Zapisz skoroszyt
Na koniec zapiszmy nasz skoroszyt z dołączonym komentarzem i obrazkiem.
```csharp
// Zapisz skoroszyt
workbook.Save(dataDir + "book1.out.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
- workbook.Save: Ta metoda zapisuje skoroszyt do określonej ścieżki. Zapisujemy go jako plik XLSX.
## Wniosek
I masz! Udało Ci się dodać komentarz z obrazem do pliku Excel przy użyciu Aspose.Cells dla .NET. Ta funkcja może sprawić, że Twoje arkusze kalkulacyjne będą bardziej informacyjne i atrakcyjne wizualnie. Niezależnie od tego, czy dodajesz adnotacje do danych, przekazujesz informacje zwrotne, czy po prostu dodajesz osobisty akcent, komentarze z obrazami mogą znacznie poprawić wrażenia użytkownika.
## Najczęściej zadawane pytania
### Czy mogę dodać wiele komentarzy do tej samej komórki?
Nie, Excel nie pozwala na wiele komentarzy w tej samej komórce. Można mieć tylko jeden komentarz na komórkę.
### Jakie formaty obrazów są obsługiwane?
Aspose.Cells obsługuje różne formaty obrazów, w tym PNG, JPEG i BMP.
### Czy potrzebuję licencji, aby korzystać z Aspose.Cells?
Aspose.Cells oferuje bezpłatną wersję próbną, jednak aby korzystać z pełnej funkcjonalności, należy zakupić licencję.
### Czy mogę dostosować wygląd komentarza?
Tak, możesz dostosować czcionkę, rozmiar i kolor tekstu komentarza, a także możesz zmienić kształt i rozmiar samego komentarza.
### Gdzie mogę znaleźć więcej dokumentacji na temat Aspose.Cells?
 Pełną dokumentację Aspose.Cells można znaleźć[Tutaj](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
