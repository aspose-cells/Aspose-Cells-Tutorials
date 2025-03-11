---
title: Wstaw obraz w nagłówku i stopce
linktitle: Wstaw obraz w nagłówku i stopce
second_title: Aspose.Cells dla .NET API Reference
description: Dowiedz się, jak wstawiać obrazy do nagłówków i stopek za pomocą Aspose.Cells dla platformy .NET, korzystając z tego kompleksowego przewodnika krok po kroku.
weight: 60
url: /pl/net/excel-page-setup/insert-image-in-header-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wstaw obraz w nagłówku i stopce

## Wstęp

Podczas pracy z plikami Excela nagłówki i stopki odgrywają kluczową rolę w dostarczaniu kontekstu i cennych informacji. Wyobraź sobie, że tworzysz raport dla swojej firmy, a logo firmy musi być obecne w nagłówku, aby nadać mu profesjonalny charakter. W tym przewodniku pokażemy Ci, jak używać Aspose.Cells dla .NET, aby wstawić obraz w nagłówku lub stopce arkuszy Excela.

## Wymagania wstępne

Zanim zagłębisz się w kod, musisz przygotować kilka rzeczy:

1.  Biblioteka Aspose.Cells dla .NET: Upewnij się, że biblioteka Aspose.Cells jest zainstalowana w środowisku .NET. Jeśli jeszcze jej nie masz, możesz[pobierz tutaj](https://releases.aspose.com/cells/net/).
2. Visual Studio lub inne środowisko IDE: Będziesz potrzebować zintegrowanego środowiska programistycznego, aby pisać i wykonywać kod C#.
3.  Przykładowy obraz: Przygotuj obraz, który chcesz wstawić do nagłówka lub stopki. W naszym przykładzie użyjemy logo firmy o nazwie`aspose-logo.jpg`.
4. Podstawowa znajomość języka C#: Choć nie jest to obowiązkowe, zrozumienie języka C# ułatwi Ci korzystanie z tego samouczka.
5. Dostęp do systemu plików: Upewnij się, że masz dostęp do systemu plików, w którym będziesz mógł odczytać obraz i zapisać plik Excela.

## Importuj pakiety

Aby zacząć, musisz zaimportować niezbędne przestrzenie nazw do pliku C#. Oto krótkie podsumowanie:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Te importy zapewnią dostęp do wszystkich klas, których potrzebujemy do obsługi plików Excela i plików w systemie.

## Krok 1: Konfigurowanie ścieżki katalogu

Najpierw musisz określić katalog, w którym znajdują się pliki Excela i obrazy. Zaktualizuj ścieżkę, aby pasowała do Twojej lokalnej struktury.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Aktualizuj odpowiednio
```

 Ta linia ustawia`dataDir`zmienna, która jest ścieżką bazową do zlokalizowania obrazu, który chcesz wstawić do nagłówka.

## Krok 2: Tworzenie obiektu skoroszytu

Następnie musisz utworzyć nowy skoroszyt, do którego dodasz swój obraz.

```csharp
Workbook workbook = new Workbook();
```

 Ta linia kodu inicjuje nową instancję`Workbook` Klasa umożliwiająca pracę z arkuszami kalkulacyjnymi programu Excel.

## Krok 3: Definiowanie ścieżki obrazu

 Czas utworzyć zmienną typu string, która będzie zawierać ścieżkę do obrazu, którego chcesz użyć. W naszym przypadku używamy`aspose-logo.jpg`.

```csharp
string logo_url = dataDir + "aspose-logo.jpg";
```

Tutaj łączymy ścieżkę katalogu z nazwą pliku logo.

## Krok 4: Odczyt obrazu jako danych binarnych

Aby wstawić obraz do nagłówka, musimy odczytać plik obrazu jako dane binarne.

```csharp
FileStream inFile = new FileStream(logo_url, FileMode.Open, FileAccess.Read);
byte[] binaryData = new byte[inFile.Length];
long bytesRead = inFile.Read(binaryData, 0, (int)inFile.Length);
```

-  Ten`FileStream` służy do otwierania obrazu w trybie odczytu.
-  Następnie deklarujemy tablicę bajtów`binaryData` do przechowywania danych obrazu.
-  Na koniec odczytujemy dane obrazu z`FileStream`.

## Krok 5: Dostęp do obiektu ustawień strony

 Aby dokonać zmian w nagłówku, musimy uzyskać dostęp do`PageSetup` obiekt związany z pierwszym arkuszem kalkulacyjnym. 

```csharp
PageSetup pageSetup = workbook.Worksheets[0].PageSetup;
```

 Tutaj dostajemy`PageSetup` obiekt, który umożliwia manipulowanie ustawieniami drukowania arkusza kalkulacyjnego.

## Krok 6: Wstawianie obrazu do nagłówka

Mając już dane binarne obrazu, możemy wstawić je do nagłówka.

```csharp
pageSetup.SetHeaderPicture(1, binaryData);
```

 Ten wiersz umieszcza obraz w środkowej części nagłówka. Parametr`1` określa sekcję nagłówka.

## Krok 7: Ustawianie zawartości nagłówka

Teraz, gdy mamy już gotowy obraz, możemy dodać trochę tekstu do nagłówka, aby uwydatnić jego kontekst. 

```csharp
pageSetup.SetHeader(1, "&G"); // Wstawia obraz
pageSetup.SetHeader(2, "&A"); // Wstawia nazwę arkusza
```

- Pierwszy wiersz wstawia symbol zastępczy obrazu (`&G`).
- Drugi wiersz dodaje nazwę arkusza w prawej części nagłówka, używając symbolu zastępczego (`&A`).

## Krok 8: Zapisywanie skoroszytu

Po wprowadzeniu wszystkich niezbędnych zmian nadszedł czas na zapisanie skoroszytu.

```csharp
workbook.Save(dataDir + "InsertImageInHeaderFooter_out.xls");
```

Ten wiersz zapisuje skoroszyt pod określoną nazwą pliku w katalogu, który zdefiniowałeś wcześniej.

## Krok 9: Zamykanie strumienia plików

 Na koniec nie zapomnij zamknąć swojego`FileStream` aby uwolnić zasoby.

```csharp
inFile.Close();
```

Dzięki temu Twoja aplikacja będzie uporządkowana i zapobiegniesz wyciekom pamięci.

## Wniosek

Gratulacje! Udało Ci się dodać obraz do nagłówka pliku Excel przy użyciu Aspose.Cells dla .NET. Niezależnie od tego, czy jest to logo firmy, czy inspirujący cytat, nagłówki mogą znacznie zwiększyć profesjonalizm Twoich dokumentów. Teraz możesz zastosować tę wiedzę w różnych projektach — wyobraź sobie, jak dopracowane będą Twoje raporty z dostosowanymi nagłówkami i stopkami!

## Najczęściej zadawane pytania

### Jakie formaty plików graficznych obsługuje Aspose.Cells?
Aspose.Cells obsługuje wiele formatów, w tym JPEG, PNG, BMP, GIF i TIFF.

### Czy mogę wstawić wiele obrazów do nagłówka/stopki?
Tak, możesz wstawiać oddzielne obrazy w różnych sekcjach nagłówka lub stopki, używając różnych symboli zastępczych.

### Czy Aspose.Cells jest darmowy?
 Aspose.Cells oferuje bezpłatną wersję próbną, ale dostępna jest wersja licencjonowana, która zapewnia pełny dostęp i dodatkowe funkcje. Możesz uzyskać[tymczasowa licencja tutaj](https://purchase.aspose.com/temporary-license/).

### Jak mogę rozwiązać problem z wyświetlaniem obrazów?
Upewnij się, że ścieżka do obrazu jest poprawna i plik istnieje. Sprawdź również zgodność formatu obrazu.

### Gdzie mogę znaleźć dodatkową dokumentację dotyczącą Aspose.Cells?
 Szczegółową dokumentację można znaleźć[Tutaj](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
