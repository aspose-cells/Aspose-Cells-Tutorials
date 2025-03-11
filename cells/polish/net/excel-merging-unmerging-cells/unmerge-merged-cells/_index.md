---
title: Rozdzielanie połączonych komórek w programie Excel
linktitle: Rozdzielanie połączonych komórek w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Łatwe rozdzielanie połączonych komórek w programie Excel za pomocą Aspose.Cells dla .NET. Postępuj zgodnie z naszym przewodnikiem krok po kroku, aby tworzyć lepsze arkusze kalkulacyjne.
weight: 10
url: /pl/net/excel-merging-unmerging-cells/unmerge-merged-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozdzielanie połączonych komórek w programie Excel

## Wstęp

Czy masz dość radzenia sobie ze scalonymi komórkami w arkuszach kalkulacyjnych programu Excel? Nie jesteś sam! Scalone komórki mogą być przydatną funkcją formatowania, ale często mogą prowadzić do bólu głowy, jeśli chodzi o manipulację danymi i analizę. Ale zgadnij co? Rozdzielenie tych irytujących komórek jest łatwiejsze, niż mogłoby się wydawać — szczególnie, gdy używasz Aspose.Cells dla .NET. W tym artykule przeprowadzę Cię przez proces rozdzielania scalonych komórek krok po kroku, zapewniając, że Twoje dane są schludne, uporządkowane i gotowe do działania! Więc chwyć swój kapelusz kodera i zanurzmy się w świecie Aspose.Cells.

## Wymagania wstępne

Zanim zabierzemy się do pracy, jest kilka niezbędnych rzeczy, które musisz mieć pod ręką:

### Podstawowa wiedza z zakresu języka C# i .NET Framework
Jeśli znasz programowanie w C# i masz podstawową wiedzę na temat .NET Framework, to masz już dobry start. Jeśli nie, nie martw się! Ten samouczek został zaprojektowany tak, aby był prosty, więc po drodze poznasz niezbędne koncepcje.

### Biblioteka Aspose.Cells
Upewnij się, że biblioteka Aspose.Cells jest zainstalowana w środowisku .NET. Możesz ją łatwo pobrać, odwiedzając[Strona pobierania Aspose.Cells](https://releases.aspose.com/cells/net/).

### Konfiguracja IDE
Powinieneś mieć przygotowane środowisko programistyczne, np. Visual Studio, w którym będziesz mógł pisać i wykonywać kod C#.

### Przykładowy plik Excela
Pobierz przykładowy plik programu Excel zawierający połączone komórki — będziesz go używać do ćwiczenia rozdzielania komórek.

Mając już za sobą wszystkie te wymagania wstępne, możemy przejść do ekscytującej części — kodowania naszego rozwiązania!

## Importuj pakiety

Najpierw zaimportujmy niezbędne pakiety. Dzięki Aspose.Cells będziesz wchodził w interakcję z różnymi klasami, aby skutecznie zarządzać plikami Excel. Oto, co musisz uwzględnić na początku pliku C#:

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

Dzięki temu pakietowi uzyskasz dostęp do wszystkich funkcji oferowanych przez Aspose.Cells.

Podzielmy proces rozłączania na łatwe do opanowania kroki. Każdy krok będzie jasno zdefiniowany, abyś mógł łatwo go śledzić.

## Krok 1: Zdefiniuj katalogi

Pierwszym krokiem jest zdefiniowanie katalogów, w których znajdują się plik wejściowy Excel (ten ze scalonymi komórkami) i plik wyjściowy (ten, w którym zostaną zapisane niepołączone dane). Oto, jak to skonfigurować:

```csharp
// Katalog źródłowy
string sourceDir = "Your Document Directory"; 

// Katalog wyjściowy
string outputDir = "Your Document Directory"; 
```

 Pamiętaj o wymianie`"Your Document Directory"` z rzeczywistą ścieżką do Twoich plików.

## Krok 2: Utwórz skoroszyt

Teraz, gdy ustawiłeś katalogi, czas utworzyć obiekt Workbook. Ten obiekt pozwoli ci manipulować plikiem Excel. Możesz to zrobić za pomocą następującego kodu:

```csharp
// Utwórz skoroszyt
Workbook wbk = new Aspose.Cells.Workbook(sourceDir + "sampleUnMergingtheMergedCells.xlsx");
```

Ta linijka kodu odczytuje przykładowy plik Excel i przygotowuje go do przetworzenia. 

## Krok 3: Uzyskaj dostęp do arkusza kalkulacyjnego

Każdy skoroszyt składa się z arkuszy. Musisz uzyskać dostęp do konkretnego arkusza, w którym chcesz rozdzielić komórki. Oto jak to zrobić:

```csharp
// Utwórz arkusz kalkulacyjny i pobierz pierwszy arkusz
Worksheet worksheet = wbk.Worksheets[0];
```

Ten kod pobiera pierwszy arkusz. Jeśli połączone komórki znajdują się na innym arkuszu, zaktualizuj odpowiednio indeks.

## Krok 4: Dostęp do komórek w arkuszu kalkulacyjnym

Następnie musisz uzyskać odwołanie do komórek w arkuszu kalkulacyjnym. Można to zrobić za pomocą:

```csharp
//Utwórz obiekt Cells, aby pobrać wszystkie komórki
Cells cells = worksheet.Cells;
```

Dzięki temu wierszowi masz teraz dostęp do wszystkich komórek w arkuszu kalkulacyjnym, co umożliwia Ci manipulowanie nimi według potrzeb.

## Krok 5: Rozdziel komórki

Oto kluczowy krok — rozłączenie komórek! Będziesz chciał określić zakres połączonych komórek, które chcesz rozłączyć. Użyj następującego kodu:

```csharp
// Rozdziel komórki
cells.UnMerge(5, 2, 2, 3);
```

 W tym przykładzie`UnMerge` Metoda przyjmuje cztery parametry: początkowy indeks wiersza (5), początkowy indeks kolumny (2), liczbę wierszy do rozłączenia (2) i liczbę kolumn do rozłączenia (3). Dostosuj te parametry, aby pasowały do konkretnych scalonych komórek w pliku Excel.

## Krok 6: Zapisz skoroszyt

Po rozłączeniu będziesz chciał zapisać zmiany w nowym pliku Excel. Oto jak to zrobić:

```csharp
// Zapisz plik
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

Ten wiersz zapisuje Twoje niepołączone dane w określonym katalogu wyjściowym. Proste!

## Krok 7: Potwierdź proces

Na koniec, dobrym pomysłem jest potwierdzenie, że wszystko poszło gładko. Możesz wydrukować wiadomość na konsoli, aby poinformować, że operacja została wykonana pomyślnie:

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

masz! Udało Ci się rozdzielić komórki w pliku Excel przy użyciu Aspose.Cells dla .NET.

## Wniosek

Rozdzielanie komórek może wydawać się żmudne, zwłaszcza jeśli masz do czynienia z dużymi arkuszami kalkulacyjnymi, ale dzięki Aspose.Cells dla .NET to pestka! Ten samouczek przeprowadził Cię przez wszystko, od konfiguracji środowiska po wykonanie kodu potrzebnego do efektywnego rozdzielania komórek. Elastyczność oferowana przez bibliotekę Aspose.Cells pozwala na wydajne przetwarzanie arkuszy kalkulacyjnych, co czyni ją idealnym wyborem dla programistów pracujących z plikami Excel. Więc zanurz się i zacznij cieszyć się czystszymi, bardziej zarządzalnymi arkuszami kalkulacyjnymi.

## Najczęściej zadawane pytania

### Czym jest Aspose.Cells?  
Aspose.Cells to potężna biblioteka służąca do tworzenia, modyfikowania i konwertowania dokumentów Excel w aplikacjach .NET.

### Czy potrzebuję licencji, aby korzystać z Aspose.Cells?  
 Chociaż Aspose.Cells oferuje bezpłatną wersję próbną, do pełnego wykorzystania wymagana jest licencja. Możesz uzyskać[tymczasowa licencja tutaj](https://purchase.aspose.com/temporary-license/).

### Czy mogę rozdzielić komórki w wielu arkuszach jednocześnie?  
Tak, możesz przechodzić przez wiele arkuszy w skoroszycie i w razie potrzeby rozdzielać komórki.

### Czy Aspose.Cells jest kompatybilny z .NET Core?  
Tak, Aspose.Cells jest kompatybilny z .NET Core, co czyni go wszechstronnym rozwiązaniem dla różnych aplikacji .NET.

### Gdzie mogę znaleźć więcej dokumentacji na temat Aspose.Cells?  
 Pełną dokumentację można znaleźć na stronie[Strona referencyjna Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
