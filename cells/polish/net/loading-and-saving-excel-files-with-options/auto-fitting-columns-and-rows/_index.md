---
title: Automatyczne dopasowywanie kolumn i wierszy podczas ładowania kodu HTML w skoroszycie
linktitle: Automatyczne dopasowywanie kolumn i wierszy podczas ładowania kodu HTML w skoroszycie
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak automatycznie dopasowywać kolumny i wiersze podczas ładowania HTML do programu Excel za pomocą Aspose.Cells dla .NET. Zawiera przewodnik krok po kroku.
weight: 10
url: /pl/net/loading-and-saving-excel-files-with-options/auto-fitting-columns-and-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatyczne dopasowywanie kolumn i wierszy podczas ładowania kodu HTML w skoroszycie

## Wstęp
Czy zastanawiałeś się kiedyś, jak automatycznie dostosować rozmiary kolumn i wierszy podczas ładowania zawartości HTML do skoroszytu programu Excel przy użyciu Aspose.Cells dla .NET? Cóż, jesteś we właściwym miejscu! W tym samouczku zagłębimy się w to, jak możesz załadować tabelę HTML do skoroszytu i upewnić się, że kolumny i wiersze są automatycznie dopasowywane do zawartości. Jeśli pracujesz z dynamicznymi danymi, które często się zmieniają, ten przewodnik będzie dla Ciebie pomocny w tworzeniu dobrze sformatowanych arkuszy programu Excel z HTML.
### Wymagania wstępne
Zanim przejdziesz do kodu, musisz skonfigurować kilka rzeczy w swoim systemie. Nie martw się, to proste i przejrzyste!
1. Zainstalowany program Visual Studio: Będziesz potrzebować programu Visual Studio lub innego środowiska programistycznego .NET.
2.  Aspose.Cells dla .NET: Możesz[pobierz najnowszą wersję](https://releases.aspose.com/cells/net/) lub zainstaluj go przy użyciu menedżera pakietów NuGet.
3. .NET Framework: Upewnij się, że masz zainstalowany .NET Framework 4.0 lub nowszy.
4. Podstawowa znajomość języka C#: Posiadanie pewnej wiedzy na temat języka C# sprawi, że ten samouczek będzie dla Ciebie łatwiejszy.
5. Dane tabeli HTML: Przygotuj zawartość HTML (nawet prostą tabelę), którą chcesz załadować do programu Excel.
## Importuj pakiety
Po pierwsze — zaimportujmy niezbędne przestrzenie nazw, aby zacząć. Oto prosta lista tego, co musisz zaimportować:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Pakiety te umożliwiają obsługę skoroszytu, manipulowanie danymi HTML i bezproblemowe ładowanie ich do programu Excel.
Podzielmy ten proces na łatwe do opanowania części, abyś mógł łatwo śledzić. Pod koniec tego będziesz mieć działający przykład, jak automatycznie dopasowywać kolumny i wiersze podczas ładowania HTML do skoroszytu za pomocą Aspose.Cells dla .NET.
## Krok 1: Skonfiguruj katalog dokumentów
Aby łatwo zapisywać i odzyskiwać pliki, określimy ścieżkę, w której będą przechowywane Twoje dokumenty. Możesz zastąpić ścieżkę katalogu własną lokalizacją folderu.
```csharp
string dataDir = "Your Document Directory";
```
Ten wiersz ustawia katalog, w którym zostaną zapisane pliki Excela. Ważne jest, aby prawidłowo organizować pliki podczas pracy nad wieloma projektami. Wyobraź sobie to jako szafkę na dokumenty swojego projektu!
## Krok 2: Utwórz dane HTML jako ciąg
Następnie zdefiniujemy podstawową zawartość HTML. Na potrzeby tego przykładu użyjemy prostej tabeli HTML. Możesz ją dostosować do potrzeb swojego projektu.
```csharp
string sampleHtml = "<html><body><table><tr><td>This is sample text.</td><td>Some text.</td></tr><tr><td>This is another sample text.</td><td>Some text.</td></tr></table></body></html>";
```
Definiujemy tutaj bardzo podstawowy ciąg HTML. Zawiera on tabelę z kilkoma wierszami i kolumnami. Możesz dodać więcej wierszy lub kolumn zgodnie ze swoimi wymaganiami. Pomyśl o tym jak o przygotowywaniu składników przed ugotowaniem posiłku!
## Krok 3: Załaduj ciąg HTML do MemoryStream
 Teraz, gdy mamy już gotową zawartość HTML, następnym krokiem jest załadowanie jej do pamięci za pomocą`MemoryStream`Dzięki temu możemy manipulować zawartością HTML w pamięci, bez konieczności jej wcześniejszego zapisywania na dysku.
```csharp
MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(sampleHtml));
```
 Konwertując ciąg HTML na tablicę bajtów i wprowadzając ją do`MemoryStream`, możemy pracować z danymi HTML w pamięci. Wyobraź sobie ten krok jako przygotowanie dania w garnku przed włożeniem go do piekarnika!
## Krok 4: Załaduj MemoryStream do skoroszytu (bez automatycznego dopasowywania)
 Gdy już mamy zawartość HTML w pamięci, ładujemy ją do Aspose`Workbook`W tym momencie nie dopasowujemy jeszcze automatycznie kolumn i wierszy. To nasz scenariusz „przed”, który później porównamy z wersją dopasowywaną automatycznie.
```csharp
Workbook wb = new Workbook(ms);
wb.Save(dataDir + "outputWithout_AutoFitColsAndRows.xlsx");
```
Skoroszyt jest załadowany treścią HTML, ale kolumny i wiersze nie są jeszcze automatycznie dopasowane do tekstu. Wyobraź sobie pieczenie ciasta, ale zapominanie o sprawdzeniu temperatury — działa, ale może nie być idealne!
## Krok 5: Określ opcje ładowania HTML z włączonym automatycznym dopasowaniem
 A oto magia! Tworzymy instancję`HtmlLoadOptions` i włącz`AutoFitColsAndRows` Właściwość. Zapewnia to, że po załadowaniu zawartości HTML kolumny i wiersze dostosowują się do zawartości w nich zawartej.
```csharp
HtmlLoadOptions opts = new HtmlLoadOptions();
opts.AutoFitColsAndRows = true;
```
Ustawiając tę opcję, mówimy Aspose.Cells, aby automatycznie zmieniał rozmiar wierszy i kolumn. Wyobraź sobie to jako ustawienie piekarnika na idealną temperaturę, aby ciasto wyrosło idealnie!
## Krok 6: Wczytaj kod HTML do skoroszytu z włączonym automatycznym dopasowaniem
 Teraz ponownie ładujemy zawartość HTML, ale tym razem z`AutoFitColsAndRows`opcja włączona. Spowoduje to dostosowanie szerokości kolumn i wysokości wierszy na podstawie zawartości wewnątrz nich.
```csharp
wb = new Workbook(ms, opts);
wb.Save(dataDir + "outputWith_AutoFitColsAndRows.xlsx");
```
Ten krok ładuje zawartość HTML do nowego skoroszytu i zapisuje ją jako plik Excela, ale teraz kolumny i wiersze są automatycznie dopasowywane! Wyobraź to sobie jako idealnie upieczone ciasto, w którym wszystko ma odpowiedni rozmiar.
## Wniosek
Postępując zgodnie z tymi prostymi krokami, nauczyłeś się, jak ładować zawartość HTML do skoroszytu za pomocą Aspose.Cells dla .NET i automatycznie dopasowywać kolumny i wiersze. Dzięki temu Twoje arkusze Excela zawsze będą wyglądać schludnie, niezależnie od tego, jak dynamiczna jest zawartość. To prosta, ale potężna funkcja, która może zaoszczędzić Ci mnóstwo czasu na formatowaniu i organizowaniu danych Excela.
Teraz, gdy posiadasz tę wiedzę, możesz eksperymentować z bardziej złożoną zawartością HTML, dodawać style, a nawet tworzyć całe skoroszyty programu Excel ze stron internetowych!
## Najczęściej zadawane pytania
### Czy mogę użyć tej metody do ładowania dużych tabel HTML?
Tak, Aspose.Cells sprawnie obsługuje duże tabele HTML, ale w celu uzyskania optymalnej wydajności zaleca się przeprowadzenie testów z wykorzystaniem rozmiarów danych.
### Czy mogę ręcznie zastosować określone szerokości kolumn i wysokości wierszy po automatycznym dopasowaniu?
Oczywiście! Nadal możesz dostosowywać poszczególne kolumny i wiersze nawet po użyciu funkcji autodopasowania.
### Jak mogę nadać styl tabeli po załadowaniu kodu HTML?
Możesz stosować style, korzystając z rozbudowanych opcji stylów Aspose.Cells po załadowaniu kodu HTML.
### Czy Aspose.Cells dla .NET jest zgodny ze starszymi wersjami .NET Framework?
Tak, Aspose.Cells for .NET obsługuje .NET Framework 4.0 i nowsze wersje.
### Czy mogę załadować do programu Excel inne typy treści niż HTML za pomocą Aspose.Cells?
Tak, Aspose.Cells obsługuje ładowanie różnych formatów, takich jak CSV, JSON i XML do programu Excel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
