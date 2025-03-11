---
title: Wstaw obraz w nagłówku i stopce arkusza kalkulacyjnego
linktitle: Wstaw obraz w nagłówku i stopce arkusza kalkulacyjnego
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: W tym kompleksowym przewodniku dowiesz się, jak w prosty sposób wstawić obraz do nagłówka/stopki za pomocą Aspose.Cells for .NET.
weight: 15
url: /pl/net/worksheet-page-setup-features/insert-image-in-header-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wstaw obraz w nagłówku i stopce arkusza kalkulacyjnego

## Wstęp
Jeśli chodzi o tworzenie profesjonalnie wyglądających arkuszy kalkulacyjnych programu Excel, drobne szczegóły mogą mieć ogromne znaczenie. Jednym z takich szczegółów jest dodawanie obrazów do nagłówka lub stopki arkuszy kalkulacyjnych. To pewny sposób na oznakowanie dokumentów i nadanie im odrobiny profesjonalizmu. Chociaż może to brzmieć skomplikowanie, zwłaszcza jeśli nie jesteś ekspertem od technologii, użycie Aspose.Cells dla .NET znacznie upraszcza ten proces. Więc zanurzmy się i dowiedzmy się, jak to zrobić krok po kroku!
## Wymagania wstępne
Zanim rozpoczniesz wstawianie obrazów do sekcji nagłówka i stopki, upewnij się, że masz kilka rzeczy na swoim miejscu:
1. Visual Studio: Upewnij się, że masz zainstalowane na swoim komputerze Visual Studio. To IDE jest potęgą dla rozwoju .NET.
2.  Aspose.Cells dla .NET: Możesz otrzymać bezpłatną wersję próbną lub kupić ją, jeśli poważnie myślisz o maksymalizacji swoich możliwości w programie Excel. Pobierz ją[Tutaj](https://releases.aspose.com/cells/net/).
3. Podstawowa znajomość języka C#: Przydatna będzie podstawowa znajomość języka C# i umiejętność uruchamiania aplikacji .NET.
4. Plik obrazu: Przygotuj plik obrazu, np. logo firmy. W tym przykładzie będziemy się do niego odwoływać jako`aspose-logo.jpg`.
## Importuj pakiety
Aby rozpocząć naszą podróż kodowania, upewnij się, że masz niezbędne pakiety zaimportowane do swojego projektu C#. Potrzebujesz przestrzeni nazw Aspose.Cells, która zawiera wszystkie klasy i metody, z którymi będziesz pracować.
Oto jak uwzględnić to w kodzie:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Teraz, gdy wszystko już skonfigurowaliśmy, możemy przejść przez cały proces, podając proste do wykonania kroki.
## Krok 1: Skonfiguruj swój katalog
Zdefiniuj miejsce przechowywania plików.
 Najpierw musimy określić ścieżkę do naszego katalogu dokumentów, w którym znajdują się plik Excel i obraz. Możesz ustawić dowolną ścieżkę; wystarczy podstawić`"Your Document Directory"` z rzeczywistą ścieżką katalogu.
```csharp
string dataDir = "Your Document Directory";
```
## Krok 2: Utwórz obiekt skoroszytu
Utwórz wystąpienie skoroszytu programu Excel.
Po ustaleniu ścieżki musimy utworzyć nową instancję arkusza kalkulacyjnego, do którego wstawimy obraz. 
```csharp
Workbook workbook = new Workbook();
```
## Krok 3: Załaduj swój obraz
Otwórz i odczytaj plik obrazu, konwertując go na tablicę bajtów w celu przetworzenia.
Następnie ustawimy ścieżkę do naszego obrazu (w tym przypadku logo) i zainicjujemy`FileStream` obiekt do odczytu obrazu. Oto jak to zrobić:
```csharp
string logo_url = dataDir + "aspose-logo.jpg";
// Deklarowanie obiektu FileStream
FileStream inFile;
byte[] binaryData;
// Tworzenie instancji obiektu FileStream
inFile = new FileStream(logo_url, FileMode.Open, FileAccess.Read);
```
## Krok 4: Odczytaj obraz do tablicy bajtów
Konwertuj dane pliku obrazu na tablicę bajtów.
Aby pracować z obrazem, musimy go odczytać do tablicy bajtów. Jest to niezbędne, ponieważ pozwala nam manipulować obrazem w aplikacji.
```csharp
// Tworzenie instancji tablicy bajtów o rozmiarze obiektu FileStream
binaryData = new byte[inFile.Length];
// Odczytuje blok bajtów ze strumienia i zapisuje dane w podanym buforze tablicy bajtów.
long bytesRead = inFile.Read(binaryData, 0, (int)inFile.Length);
```
## Krok 5: Skonfiguruj ustawienia strony dla nagłówka/stopki
Uzyskaj dostęp do obiektu PageSetup, aby manipulować sekcjami nagłówka i stopki.
Aby wstawić nasz obraz, musimy skonfigurować obiekt ustawień strony. Pozwala nam to dostosować nagłówek naszego arkusza kalkulacyjnego:
```csharp
PageSetup pageSetup = workbook.Worksheets[0].PageSetup;
```
## Krok 6: Wstaw logo do nagłówka
Osadź obraz w sekcji nagłówka arkusza kalkulacyjnego.
To jest magiczny moment! Wstawimy nasze logo do środkowej sekcji nagłówka:
```csharp
// Umieść logo/obraz w środkowej części nagłówka strony.
pageSetup.SetHeaderPicture(1, binaryData);
// Ustaw skrypt dla logo/obrazu
pageSetup.SetHeader(1, "&G");
// Ustaw nazwę Arkusza w prawej sekcji nagłówka strony za pomocą skryptu
pageSetup.SetHeader(2, "&A");
```
## Krok 7: Zapisz swój skoroszyt
Zapisz zmiany w nowym pliku Excel.
Po skonfigurowaniu wszystkiego, czas zapisać nasz skoroszyt. Upewnij się, że podałeś nową nazwę dla swojego pliku wyjściowego:
```csharp
workbook.Save(dataDir + "InsertImageInHeaderFooter_out.xls");
```
## Krok 8: Oczyść zasoby
Zamknij FileStream, aby zwolnić zasoby.
 Na koniec, po wszystkich manipulacjach, nie zapomnij o uporządkowaniu i zamknięciu`FileStream`!
```csharp
inFile.Close();
```
## Wniosek
I masz! Udało Ci się wstawić obraz do nagłówka/stopki arkusza kalkulacyjnego programu Excel przy użyciu Aspose.Cells dla .NET. To proste, prawda? Po zrozumieniu kroków możesz dostosować je dalej, aby dopasować do swoich konkretnych potrzeb. Niezależnie od tego, czy chcesz oznaczyć raporty dla swojej firmy, czy po prostu dodać osobisty akcent, ta technika jest niezwykle przydatna. 
## Najczęściej zadawane pytania
### Czy mogę użyć dowolnego formatu obrazu?
Tak, Aspose.Cells obsługuje różne formaty obrazów, w tym JPEG, PNG i BMP dla obrazów nagłówka i stopki.
### Czy korzystanie z Aspose.Cells jest bezpłatne?
 Aspose.Cells oferuje bezpłatną wersję próbną, ale aby kontynuować korzystanie, musisz kupić licencję. Dowiedz się więcej o cenach[Tutaj](https://purchase.aspose.com/buy).
### Jak uzyskać dostęp do dokumentacji Aspose.Cells?
 Możesz zagłębić się w funkcje i funkcje Aspose.Cells odwiedzając stronę[dokumentacja](https://reference.aspose.com/cells/net/).
### Czy mogę używać Aspose.Cells bez programu Visual Studio?
Tak, o ile dysponujesz środowiskiem uruchomieniowym .NET, możesz używać Aspose.Cells w dowolnym środowisku programistycznym zgodnym z .NET.
### Co powinienem zrobić, jeśli napotkam problemy?
 Jeśli napotkasz jakiekolwiek problemy lub potrzebujesz wsparcia, sprawdź[Forum wsparcia Aspose](https://forum.aspose.com/c/cells/9) aby uzyskać pomoc od społeczności i deweloperów.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
