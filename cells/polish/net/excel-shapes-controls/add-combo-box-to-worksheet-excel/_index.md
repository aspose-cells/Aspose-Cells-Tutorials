---
title: Dodaj pole kombi do arkusza kalkulacyjnego w programie Excel
linktitle: Dodaj pole kombi do arkusza kalkulacyjnego w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak programowo dodać pole kombi do arkusza kalkulacyjnego programu Excel, używając Aspose.Cells dla .NET. Ten przewodnik krok po kroku przeprowadzi Cię przez każdy szczegół.
weight: 21
url: /pl/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj pole kombi do arkusza kalkulacyjnego w programie Excel

## Wstęp
Tworzenie interaktywnych arkuszy kalkulacyjnych programu Excel może znacznie poprawić doświadczenia użytkownika, zwłaszcza gdy dodajesz elementy formularza, takie jak pola kombi. Pola kombi pozwalają użytkownikom wybierać opcje z predefiniowanej listy, co ułatwia i usprawnia wprowadzanie danych. Dzięki Aspose.Cells dla .NET możesz programowo tworzyć pola kombi w arkuszach programu Excel bez bezpośredniego korzystania z programu Excel. Ta potężna biblioteka umożliwia programistom manipulowanie plikami programu Excel na różne sposoby, w tym automatyzację kontrolek formularza.
W tym samouczku przeprowadzimy Cię przez proces dodawania pola kombi do arkusza kalkulacyjnego w programie Excel przy użyciu Aspose.Cells dla .NET. Jeśli chcesz tworzyć dynamiczne, przyjazne dla użytkownika arkusze kalkulacyjne, ten przewodnik pomoże Ci zacząć.
## Wymagania wstępne
Zanim zagłębimy się w kod, upewnijmy się, że masz wszystko, czego potrzebujesz:
- Aspose.Cells dla .NET: Pobierz i zainstaluj bibliotekę Aspose.Cells dla .NET z[strona do pobrania](https://releases.aspose.com/cells/net/).
- .NET Framework: Upewnij się, że masz zainstalowany .NET Framework na swoim komputerze. Każda wersja obsługiwana przez Aspose.Cells będzie działać.
- Środowisko programistyczne: Użyj środowiska IDE, takiego jak Visual Studio, do zarządzania projektem i pisania kodu.
-  Licencja Aspose: Możesz pracować bez licencji w trybie ewaluacyjnym, ale w przypadku pełnej wersji musisz zastosować licencję. Uzyskaj[licencja tymczasowa](https://purchase.aspose.com/temporary-license/) jeśli to konieczne.
## Importuj pakiety
Aby rozpocząć, musisz zaimportować wymagane przestrzenie nazw do swojego projektu. Oto, czego potrzebujesz:
```csharp
using System.IO;
using Aspose.Cells;
```
Są one niezbędne do interakcji z plikami programu Excel i manipulowania elementami formularzy, takimi jak pola kombi w skoroszycie.
Aby ułatwić zrozumienie, podzielimy proces dodawania pola kombi na kilka prostych kroków.
## Krok 1: Skonfiguruj katalog dokumentów
Pierwszym krokiem jest utworzenie katalogu, w którym zostaną zapisane pliki Excela. Możesz utworzyć nowy folder, jeśli jeszcze nie istnieje.
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
// Utwórz katalog, jeśli jeszcze go nie ma.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Określa lokalizację, w której zostanie zapisany plik wyjściowy.
- System.IO.Directory.Exists: sprawdza, czy katalog już istnieje.
- System.IO.Directory.CreateDirectory: Tworzy katalog, jeśli go brakuje.
## Krok 2: Utwórz nowy skoroszyt
Teraz utwórz nowy skoroszyt w programie Excel, do którego chcesz dodać pole kombi.

```csharp
// Utwórz nowy skoroszyt.
Workbook workbook = new Workbook();
```

- Skoroszyt skoroszyt: Inicjuje nowe wystąpienie klasy Skoroszyt, reprezentujące plik programu Excel.
## Krok 3: Pobierz arkusz kalkulacyjny i komórki
Następnie przejdź do pierwszego arkusza kalkulacyjnego w skoroszycie i pobierz zbiór komórek, do którego chcesz wprowadzić dane.

```csharp
// Pobierz pierwszy arkusz.
Worksheet sheet = workbook.Worksheets[0];
// Pobierz kolekcję komórek arkusza kalkulacyjnego.
Cells cells = sheet.Cells;
```

- Arkusz kalkulacyjny: Pobiera pierwszy arkusz kalkulacyjny ze skoroszytu.
- Komórki komórki: Pobiera zbiór komórek z arkusza kalkulacyjnego.
## Krok 4: Wprowadź wartości dla pola kombi
Teraz musimy wprowadzić pewne wartości do komórek. Te wartości będą służyć jako opcje dla pola kombi.

```csharp
// Wprowadź wartość.
cells["B3"].PutValue("Employee:");
// Pogrub to.
cells["B3"].GetStyle().Font.IsBold = true;
// Wprowadź wartości określające zakres wejściowy dla pola kombi.
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- komórki[„B3”].PutValue: Umieszcza etykietę „Pracownik” w komórce B3.
- Font.IsBold = true: Ustawia tekst na pogrubiony, aby się wyróżniał.
- Zakres wejściowy: Wprowadź kilka identyfikatorów pracowników w komórkach A2 do A7. Zostaną one wyświetlone na liście rozwijanej pola kombi.
## Krok 5: Dodaj pole kombi do arkusza kalkulacyjnego
Następnym krokiem jest dodanie kontrolki pola kombi do arkusza kalkulacyjnego. To pole kombi pozwoli użytkownikom wybrać jeden z identyfikatorów pracowników, które wprowadziłeś wcześniej.

```csharp
// Dodaj nowe pole kombi.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: Dodaje nowe pole kombi do arkusza kalkulacyjnego. Liczby (2, 0, 2, 0, 22, 100) oznaczają pozycję i wymiary pola kombi.
## Krok 6: Połącz pole kombi z komórką i ustaw zakres wejściowy
Aby pole kombi działało, musimy powiązać je z konkretną komórką i zdefiniować zakres komórek, z których będzie pobierać opcje.

```csharp
// Ustaw połączoną komórkę.
comboBox.LinkedCell = "A1";
// Ustaw zakres wejściowy.
comboBox.InputRange = "A2:A7";
```

- LinkedCell: Łączy wybór pola kombi z komórką A1. Wybrana wartość z pola kombi pojawi się w tej komórce.
- InputRange: Definiuje zakres komórek (A2:A7) zawierający wartości, które zostaną umieszczone w opcjach pola kombi.
## Krok 7: Dostosuj wygląd pola kombi
Możesz dodatkowo dostosować pole kombi, określając liczbę linii rozwijanych i włączając cieniowanie 3D w celu uzyskania lepszego efektu estetycznego.

```csharp
// Ustaw liczbę wierszy listy wyświetlanych w części listy pola kombi.
comboBox.DropDownLines = 5;
// Ustaw pole kombi z cieniowaniem 3-D.
comboBox.Shadow = true;
```

- DropDownLines: Określa, ile opcji będzie jednocześnie widocznych na liście rozwijanej pola kombi.
- Cień: Dodaje efekt cieniowania 3D do pola kombi.
## Krok 8: Automatyczne dopasowanie kolumn i zapisywanie skoroszytu
Na koniec dopasujmy automatycznie kolumny, aby uzyskać przejrzysty układ, i zapiszmy skoroszyt.

```csharp
// Automatyczne dopasowanie kolumn
sheet.AutoFitColumns();
// Zapisuje plik.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: automatycznie dostosowuje szerokość kolumn do zawartości.
- Zapisz: Zapisuje skoroszyt jako plik programu Excel w określonym katalogu.

## Wniosek
Dodawanie pola kombi do arkuszy kalkulacyjnych programu Excel przy użyciu Aspose.Cells dla .NET to prosty proces, który znacznie zwiększa elastyczność wprowadzania danych. Programowe tworzenie kontrolek formularzy umożliwia łatwe tworzenie interaktywnych arkuszy kalkulacyjnych. Ten samouczek pokazał, jak dodać pole kombi, połączyć je z komórką i skonfigurować zakres wprowadzania danych, a wszystko to przy użyciu Aspose.Cells.
 Aspose.Cells oferuje szeroki zakres funkcji do manipulacji plikami Excel, co czyni go idealnym wyborem dla programistów, którzy chcą zautomatyzować zadania arkusza kalkulacyjnego. Wypróbuj go z[bezpłatny okres próbny](https://releases.aspose.com/).
## Najczęściej zadawane pytania
### Czy mogę używać Aspose.Cells bez zainstalowanego programu Excel?
Tak, Aspose.Cells działa niezależnie od programu Excel i nie wymaga instalacji programu Excel.
### Jak zastosować licencję w Aspose.Cells?
 Możesz ubiegać się o licencję, uzyskując ją od[Tutaj](https://purchase.aspose.com/buy) i dzwonię`License.SetLicense()` w twoim kodzie.
### Jakie formaty zapisywania plików obsługuje Aspose.Cells?
Aspose.Cells obsługuje zapisywanie plików w wielu formatach, takich jak XLSX, XLS, CSV, PDF i inne.
### Czy liczba pól kombi, które mogę dodać, jest ograniczona?
Nie, nie ma ścisłego limitu. Możesz dodać tyle pól kombi, ile wymaga Twój projekt.
### Jak uzyskać pomoc techniczną dotyczącą Aspose.Cells?
 Możesz uzyskać wsparcie od[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
