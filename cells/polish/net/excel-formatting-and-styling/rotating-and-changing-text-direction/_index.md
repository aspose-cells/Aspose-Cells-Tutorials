---
title: Obracanie i zmiana kierunku tekstu w programie Excel
linktitle: Obracanie i zmiana kierunku tekstu w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Zmień kierunek tekstu w programie Excel za pomocą Aspose.Cells dla .NET. Postępuj zgodnie z naszym przewodnikiem krok po kroku, aby łatwo obracać i dostosowywać tekst.
weight: 22
url: /pl/net/excel-formatting-and-styling/rotating-and-changing-text-direction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obracanie i zmiana kierunku tekstu w programie Excel

## Wstęp
Jeśli chodzi o programową pracę z plikami Excela, często stajemy przed wyzwaniem wyświetlania danych w pożądanym formacie. Czy kiedykolwiek chciałeś zmienić kierunek tekstu w komórce Excela? Może potrzebujesz tekstu czytanego od prawej do lewej, szczególnie jeśli pracujesz z językami takimi jak arabski lub hebrajski. Albo może po prostu szukasz sposobu na poprawę wizualnej atrakcyjności swoich arkuszy kalkulacyjnych. Bez względu na powód, Aspose.Cells dla .NET zapewnia proste rozwiązanie do manipulowania kierunkiem tekstu w plikach Excela. W tym samouczku omówimy kroki potrzebne do obracania i zmiany kierunku tekstu w Excelu za pomocą Aspose.Cells.
## Wymagania wstępne
Zanim przejdziemy do kodowania, upewnij się, że masz przygotowane kilka rzeczy:
1. Visual Studio: Upewnij się, że masz zainstalowane na swoim komputerze Visual Studio. Biblioteka Aspose.Cells dobrze z nim współpracuje.
2.  Biblioteka Aspose.Cells: Będziesz potrzebować biblioteki Aspose.Cells dla .NET. Możesz ją pobrać ze strony[strona](https://releases.aspose.com/cells/net/).
3. Podstawowa wiedza o języku C#: Znajomość programowania w języku C# ułatwi Ci śledzenie kursu.
4. .NET Framework: Upewnij się, że Twój projekt jest przeznaczony dla platformy .NET Framework, ponieważ Aspose.Cells jest przeznaczony do pracy w tym środowisku.
Gdy już wszystko będzie gotowe, możesz zacząć!
## Importuj pakiety
Teraz przygotujmy nasz projekt, importując wymagane pakiety. Oto jak możesz to zrobić:
### Utwórz nowy projekt
- Otwórz program Visual Studio i utwórz nowy projekt.
- Wybierz Aplikację konsolową ze szablonów i nadaj jej odpowiednią nazwę, np. „ExcelTextDirectionDemo”.
### Dodaj bibliotekę Aspose.Cells
- Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz opcję Zarządzaj pakietami NuGet.
- Wyszukaj Aspose.Cells i zainstaluj.
### Importuj niezbędne przestrzenie nazw
 Teraz czas na wprowadzenie niezbędnych przestrzeni nazw. Na górze`Program.cs` plik zawiera następujące elementy:
```csharp
using System.IO;
using Aspose.Cells;
```
Dzięki temu możesz zacząć modyfikować pliki Excela! Teraz przejdźmy do faktycznego kodowania.
## Krok 1: Skonfiguruj katalog dokumentów
Aby mieć pewność, że zapiszemy nasz plik Excel w odpowiednim miejscu, musimy zdefiniować katalog. Oto jak to zrobić:
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory"; // Dostosuj ścieżkę katalogu
// Utwórz katalog, jeśli jeszcze go nie ma.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Ten kod ustawia katalog do zapisywania pliku Excel. Sprawdza, czy katalog istnieje i tworzy go, jeśli nie. Upewnij się, że zastąpiłeś`"Your Document Directory"` z prawidłową ścieżką.
## Krok 2: Tworzenie instancji obiektu skoroszytu
Następnie utwórzmy nowy skoroszyt programu Excel. Tutaj będziemy manipulować naszymi komórkami.
```csharp
// Tworzenie instancji obiektu skoroszytu
Workbook workbook = new Workbook();
```

 Tworząc`Workbook` obiekt, w zasadzie zaczynasz od nowego, pustego pliku Excel, który możesz modyfikować.
## Krok 3: Uzyskanie odniesienia do arkusza roboczego
Teraz przejdź do arkusza, w którym chcesz wprowadzić zmiany.
```csharp
// Uzyskanie odniesienia do arkusza roboczego
Worksheet worksheet = workbook.Worksheets[0];
```

 Ten`Worksheet` obiekt odnosi się do pierwszego arkusza w skoroszycie. Możesz uzyskać dostęp do innych arkuszy, zmieniając indeks.
## Krok 4: Dostęp do konkretnej komórki
Skupmy się na konkretnej komórce, w tym przypadku „A1”. 
```csharp
// Dostęp do komórki „A1” z arkusza kalkulacyjnego
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```

Ta linijka kodu uzyskuje dostęp do komórki „A1”, którą wkrótce zmodyfikujemy.
## Krok 5: Dodawanie wartości do komórki
Czas wprowadzić trochę danych do naszej komórki.
```csharp
// Dodawanie wartości do komórki „A1”
cell.PutValue("Visit Aspose!");
```

Tutaj po prostu dodajemy tekst „Visit Aspose!” do komórki „A1”. Możesz to zmienić na cokolwiek chcesz.
## Krok 6: Konfigurowanie stylu tekstu
Teraz nadchodzi moment, w którym zmieniamy kierunek tekstu. 
```csharp
// Ustawianie poziomego wyrównania tekstu w komórce „A1”
Style style = cell.GetStyle();
```

Przywraca to istniejący styl komórki, co otwiera drogę do modyfikacji.
## Krok 7: Zmiana kierunku tekstu 
Tutaj dzieje się magia! Możesz zmienić kierunek tekstu w ten sposób:
```csharp
// Ustawianie kierunku tekstu od prawej do lewej
style.TextDirection = TextDirectionType.RightToLeft;
```

Ten wiersz ustawia kierunek tekstu od prawej do lewej, co jest istotne w przypadku języków takich jak arabski czy hebrajski. 
## Krok 8: Stosowanie stylu do komórki
Po zmianie stylu kierunku tekstu zastosuj te zmiany ponownie do komórki:
```csharp
cell.SetStyle(style);
```

Stosujesz zmodyfikowany styl z powrotem do komórki, upewniając się, że odzwierciedla on nowy kierunek tekstu.
## Krok 9: Zapisywanie pliku Excel
Na koniec zapiszemy zmiany w nowym pliku Excela.
```csharp
// Zapisywanie pliku Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```

Ten kod zapisuje skoroszyt z określoną nazwą pliku w zdefiniowanym katalogu. Określony format to Excel 97-2003.
## Wniosek
gotowe! Udało Ci się nauczyć, jak obracać i zmieniać kierunek tekstu w komórce Excela za pomocą Aspose.Cells dla .NET. Czyż nie jest niesamowite, jak kilka linijek kodu może całkowicie zmienić układ i dostępność językową arkusza kalkulacyjnego? Możliwość programowego manipulowania plikami Excela otwiera świat możliwości, od automatyzacji raportów po ulepszanie prezentacji danych.
## Najczęściej zadawane pytania
### Czy mogę zmienić kierunek tekstu w wielu komórkach?  
Tak, można przejść przez zakres komórek i zastosować te same zmiany.
### Czy korzystanie z Aspose.Cells jest bezpłatne?  
Aspose.Cells oferuje bezpłatny okres próbny, jednak do dalszego korzystania wymagana jest licencja.
### W jakich innych formatach mogę zapisywać?  
Aspose.Cells obsługuje różne formaty, takie jak XLSX, CSV i PDF.
### Czy muszę zainstalować coś jeszcze oprócz programu Visual Studio?  
Do projektu należy dodać tylko bibliotekę Aspose.Cells.
### Gdzie mogę znaleźć więcej informacji na temat Aspose.Cells?  
 Możesz sprawdzić[dokumentacja](https://reference.aspose.com/cells/net/) aby uzyskać kompleksowe przewodniki i odniesienia do API.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
