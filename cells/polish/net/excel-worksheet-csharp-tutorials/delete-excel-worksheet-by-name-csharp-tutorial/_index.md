---
title: Usuń arkusz kalkulacyjny Excel według nazwy Samouczek C#
linktitle: Usuń arkusz kalkulacyjny programu Excel według nazwy
second_title: Aspose.Cells dla .NET API Reference
description: Dowiedz się, jak usuwać arkusze kalkulacyjne programu Excel według nazwy za pomocą języka C#. Ten przyjazny dla początkujących samouczek krok po kroku przeprowadzi Cię przez Aspose.Cells dla .NET.
weight: 40
url: /pl/net/excel-worksheet-csharp-tutorials/delete-excel-worksheet-by-name-csharp-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Usuń arkusz kalkulacyjny Excel według nazwy Samouczek C#

## Wstęp

Podczas pracy z plikami Excel programowo, czy to w celu raportowania, analizy danych, czy po prostu zarządzania rekordami, możesz potrzebować usunąć określone arkusze kalkulacyjne. W tym przewodniku przeprowadzę Cię przez prosty, ale skuteczny sposób usuwania arkusza kalkulacyjnego Excel według jego nazwy przy użyciu Aspose.Cells dla .NET. Zanurzmy się!

## Wymagania wstępne

Zanim zaczniemy, musisz mieć pewność, że masz przygotowane kilka rzeczy:

1.  Aspose.Cells for .NET Library: To jest główny komponent, który umożliwia manipulowanie plikami Excel. Jeśli jeszcze go nie zainstalowałeś, możesz[pobierz stąd](https://releases.aspose.com/cells/net/).
2. Środowisko programistyczne: Powinieneś mieć przygotowane środowisko programistyczne, najlepiej Visual Studio, w którym będziesz mógł pisać i uruchamiać kod w języku C#.
3. Podstawowa znajomość języka C#: Choć dokładnie wyjaśnię każdy krok, podstawowa znajomość języka C# pomoże Ci lepiej nadążać.
4. Plik Excel: Powinieneś mieć utworzony plik Excel (w tym samouczku będziemy się odwoływać do „book1.xls”). W tym celu możesz utworzyć prosty plik z kilkoma arkuszami kalkulacyjnymi.

Gdy już spełnisz te wymagania wstępne, będziesz gotowy, aby zająć się kodowaniem!

## Importuj pakiety

Teraz zaimportujmy niezbędne pakiety. Jest to niezbędne, ponieważ bez tych pakietów Twój program nie będzie wiedział, jak obsługiwać pliki Excel.

```csharp
using System.IO;
using Aspose.Cells;
```

## Krok 1: Konfigurowanie środowiska

Na początek musisz skonfigurować strumień plików, który umożliwi programowi odczytanie pliku Excel.

```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Upewnij się, że zastąpiłeś „YOUR DOCUMENT DIRECTORY” ścieżką do miejsca, w którym przechowywany jest plik Excel. Ta konfiguracja zapewnia, że program wie, gdzie znaleźć pliki, z którymi będzie pracować.

## Krok 2: Otwieranie pliku Excel

Po ustawieniu ścieżki pliku należy utworzyć strumień plików dla pliku Excel, którym chcesz manipulować.

```csharp
// Tworzenie strumienia plików zawierającego plik Excela do otwarcia
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```

Tutaj otwieramy „book1.xls”. Ważne jest, aby ten plik znajdował się w podanym przez Ciebie katalogu; w przeciwnym razie wystąpią błędy.

## Krok 3: Tworzenie instancji obiektu skoroszytu

 Następnie musisz utworzyć`Workbook` obiekt. Ten obiekt reprezentuje plik Excel i pozwala manipulować jego zawartością.

```csharp
// Tworzenie instancji obiektu skoroszytu
// Otwieranie pliku Excel za pomocą strumienia plików
Workbook workbook = new Workbook(fstream);
```

 W tym momencie Twój`workbook` zawiera teraz wszystkie dane z pliku Excel i można na nim wykonywać różne operacje.

## Krok 4: Usuwanie arkusza kalkulacyjnego według nazwy

Przejdźmy teraz do sedna sprawy — usuwania arkusza kalkulacyjnego po nazwie. 

```csharp
// Usuwanie arkusza kalkulacyjnego za pomocą nazwy arkusza
workbook.Worksheets.RemoveAt("Sheet1");
```

W tym przykładzie próbujemy usunąć arkusz o nazwie „Arkusz1”. Jeśli ten arkusz istnieje, zostanie pomyślnie usunięty. Jeśli nie istnieje, napotkasz wyjątek, więc upewnij się, że nazwa dokładnie pasuje.

## Krok 5: Zapisywanie skoroszytu

Po usunięciu żądanego arkusza kalkulacyjnego należy zapisać zmiany w pliku.

```csharp
// Zapisz skoroszyt
workbook.Save(dataDir + "output.out.xls");
```

Możesz zmienić nazwę pliku wyjściowego lub nadpisać oryginalny plik, jeśli to konieczne. Ważne jest, aby Twoje zmiany zostały zachowane w tym kroku!

## Wniosek

I masz to! Udało Ci się nauczyć, jak usunąć arkusz kalkulacyjny Excela według nazwy, używając Aspose.Cells dla .NET. Ta potężna biblioteka pozwala Ci bez wysiłku manipulować plikami Excela, a dzięki tej wiedzy możesz dalej odkrywać edycję i zarządzanie dokumentami Excela dla różnych aplikacji.

Zachęcamy do eksperymentowania z innymi funkcjami biblioteki Aspose.Cells i nie wahaj się eksperymentować z bardziej złożonymi manipulacjami, gdy już nabierzesz wprawy.

## Najczęściej zadawane pytania

### Czy korzystanie z Aspose.Cells jest bezpłatne?
 Aspose.Cells oferuje bezpłatną wersję próbną, ale musisz kupić licencję, aby móc dalej korzystać z usługi. Możesz otrzymać bezpłatną wersję próbną[Tutaj](https://releases.aspose.com/).

### Czy mogę usunąć wiele arkuszy kalkulacyjnych jednocześnie?
Możesz iterować kolekcję arkuszy i usuwać wiele arkuszy za pomocą pętli. Upewnij się tylko, że prawidłowo zarządzasz indeksami.

### Co zrobić, jeśli nazwa arkusza kalkulacyjnego nie istnieje?
Jeśli spróbujesz usunąć arkusz o nazwie, która nie istnieje, zostanie zgłoszony wyjątek. Warto dodać obsługę błędów, aby najpierw sprawdzić istnienie arkusza.

### Czy mogę przywrócić usunięty arkusz kalkulacyjny?
Po usunięciu arkusza kalkulacyjnego i zapisaniu zmian nie można go przywrócić, jeśli nie posiadasz kopii zapasowej oryginalnego pliku.

### Gdzie mogę znaleźć więcej materiałów na temat Aspose.Cells?
 Możesz sprawdzić kompleksowe[dokumentacja](https://reference.aspose.com/cells/net/) możesz odkryć więcej funkcji i możliwości.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
