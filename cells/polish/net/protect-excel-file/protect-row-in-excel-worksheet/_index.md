---
title: Chroń wiersz w arkuszu kalkulacyjnym programu Excel
linktitle: Chroń wiersz w arkuszu kalkulacyjnym programu Excel
second_title: Aspose.Cells dla .NET API Reference
description: Odkryj w tym samouczku, jak chronić wiersze arkusza kalkulacyjnego Excela za pomocą Aspose.Cells dla .NET. Samouczek krok po kroku w C#.
weight: 60
url: /pl/net/protect-excel-file/protect-row-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chroń wiersz w arkuszu kalkulacyjnym programu Excel

## Wstęp

Podczas pracy z arkuszami Excela często konieczne jest zabezpieczenie określonych wierszy w celu zachowania integralności danych. Niezależnie od tego, czy zarządzasz projektem zespołowym, nadzorujesz raport finansowy, czy udostępniasz dokumentację, ograniczenie dostępu do określonych wierszy może zapobiec niechcianym zmianom. W tym samouczku przyjrzymy się, jak wykorzystać Aspose.Cells dla .NET do zabezpieczenia określonych wierszy w arkuszu kalkulacyjnym Excela. Więc chwyć swój kapelusz kodera i zanurzmy się w ekscytującym świecie manipulacji Excelem za pomocą C#!

## Wymagania wstępne

Zanim przejdziemy do części praktycznej, upewnijmy się, że wszystko jest skonfigurowane. Oto kilka wymagań wstępnych:

1.  Aspose.Cells dla .NET: Pobierz bibliotekę ze strony[Strona internetowa Aspose](https://releases.aspose.com/cells/net/). Upewnij się, że masz najnowszą wersję, aby korzystać ze wszystkich nowych funkcji i poprawek błędów.
2. Visual Studio: Zintegrowane środowisko programistyczne (IDE), takie jak Visual Studio (Community, Professional lub Enterprise), pomoże Ci efektywnie kompilować i uruchamiać kod w języku C#.
3. .NET Framework: Będziesz potrzebować zgodnej wersji .NET Framework. Aspose.Cells obsługuje wiele wersji, więc upewnij się, że Twoja jest aktualna. 
4. Podstawowa znajomość języka C#: Podstawowa znajomość języka C# będzie pomocna podczas pisania kodu w tym przewodniku.
5.  Dokumentacja referencyjna: Zapoznaj się z[Dokumentacja Aspose.Cells dla .NET](https://reference.aspose.com/cells/net/) aby uzyskać dodatkowe informacje na temat zastosowanych metod i klas.

## Importuj pakiety

Pierwszym krokiem w naszej podróży jest zaimportowanie niezbędnych pakietów do naszego projektu C#. Aspose.Cells działa poprzez zestaw klas, które musimy uwzględnić:

```csharp
using System.IO;
using Aspose.Cells;
```

Teraz, gdy zaimportowaliśmy wymagane pakiety, przeanalizujmy kroki tworzenia skoroszytu programu Excel i ochrony konkretnego wiersza. 

## Krok 1: Zdefiniuj katalog

tym kroku określimy lokalizację, w której zostanie zapisany nasz plik Excel. Ważne jest, aby upewnić się, że ten katalog istnieje, w przeciwnym razie utworzymy go programowo, jeśli będzie to konieczne.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Zastąp ścieżką swojego dokumentu
bool IsExists = Directory.Exists(dataDir);
if (!IsExists)
{
    Directory.CreateDirectory(dataDir);
}
```
 W tym kodzie zamień`YOUR DOCUMENT DIRECTORY` z rzeczywistą ścieżką, pod którą chcesz zapisać plik Excela.

## Krok 2: Utwórz nowy skoroszyt

Następnie utworzymy nowy skoroszyt, w którym będą wykonywane wszelkie manipulacje. To fundamentalny krok, taki jak położenie fundamentu przed zbudowaniem wymarzonego domu.

```csharp
Workbook wb = new Workbook();
```
 Ta linia inicjuje nową instancję`Workbook` klasie, tworząc dla nas nowy arkusz ćwiczeń.

## Krok 3: Uzyskaj dostęp do arkusza kalkulacyjnego

Mając już utworzony skoroszyt, możemy zająć się pierwszym arkuszem. Pamiętaj, że plik Excela może zawierać wiele arkuszy, więc wybór właściwego jest kluczowy.

```csharp
Worksheet sheet = wb.Worksheets[0]; // Dostęp do pierwszego arkusza
```

## Krok 4: Odblokuj wszystkie kolumny

Przed zablokowaniem konkretnego wiersza, dobrą praktyką jest odblokowanie wszystkich kolumn na początku. Pozwala nam to kontrolować, które dane pozostają edytowalne później.

```csharp
Style style;
StyleFlag flag;

// Przejdź przez wszystkie kolumny i odblokuj je
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
Pętla ta przechodzi przez pierwsze 256 kolumn, odblokowując każdą z nich, aby zapewnić domyślne uprawnienia do edycji.

## Krok 5: Zablokowanie określonego wiersza

Teraz będziemy blokować pierwszy wiersz naszego arkusza kalkulacyjnego. Ten krok zapewnia, że użytkownicy nie będą mogli wprowadzać nieautoryzowanych zmian w krytycznych danych zawartych w tym wierszu.

```csharp
style = sheet.Cells.Rows[0].Style; // Uzyskaj styl pierwszego rzędu
style.IsLocked = true; // Zablokuj rząd
flag = new StyleFlag();
flag.Locked = true; // Ustaw flagę blokady
sheet.Cells.ApplyRowStyle(0, style, flag); // Zastosuj styl do pierwszego wiersza
```
Tutaj pobieramy styl dla pierwszego wiersza, oznaczamy go jako zablokowany i stosujemy styl blokowania. Jest to analogiczne do zakładania zamka na ważną szufladę — niezbędne do zabezpieczenia poufnych informacji!

## Krok 6: Ochrona arkusza

 Mając nasz wiersz zablokowany, zróbmy ten dodatkowy krok i w pełni zabezpieczmy arkusz kalkulacyjny. Wymusi to blokadę we wszystkich funkcjonalnościach zdefiniowanych w`ProtectionType`.

```csharp
sheet.Protect(ProtectionType.All); // Chroń arkusz za pomocą wszystkich funkcji
```
Po zastosowaniu tej ochrony użytkownicy nie mogą edytować zablokowanego wiersza ani wprowadzać żadnych zmian, które mogłyby wpłynąć na zablokowane obszary.

## Krok 7: Zapisywanie skoroszytu

Ostatni krok obejmuje zapisanie skoroszytu. To tutaj cała nasza ciężka praca się opłaca i możemy zobaczyć, jak nasz piękny, chroniony arkusz kalkulacyjny ożywa!

```csharp
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Upewnij się, że nazwa i format zapisanego pliku odpowiadają Twoim wymaganiom. W tym przypadku zapisujemy go w starszym formacie Excel (Excel 97-2003).

## Wniosek

I masz to! Udało Ci się skutecznie nauczyć, jak chronić konkretny wiersz w arkuszu kalkulacyjnym programu Excel za pomocą Aspose.Cells dla .NET. Za pomocą zaledwie kilku linijek kodu nie tylko utworzyłeś skoroszyt, ale także zabezpieczyłeś poufne informacje, zapewniając, że Twoje pliki programu Excel pozostaną nienaruszone i wiarygodne. Niezależnie od tego, czy jest to raport finansowy, arkusz obecności czy plan projektu współpracy, ochrona kluczowych danych jest niezbędna. 

## Najczęściej zadawane pytania

### Czym jest Aspose.Cells?
Aspose.Cells to zaawansowana biblioteka dla platformy .NET umożliwiająca użytkownikom programowe tworzenie, edytowanie i konwertowanie plików Excel.

### Czy mogę chronić wiele wierszy jednocześnie za pomocą Aspose.Cells?
Tak, możesz rozszerzyć technikę blokowania, powtarzając wiele wierszy i stosując podobne zmiany stylu w każdym z nich.

### Czy istnieje sposób na odblokowanie rzędów po zabezpieczeniu?
 Tak, możesz najpierw usunąć ochronę arkusza, a następnie dostosować`IsLocked` właściwość żądanych wierszy, a następnie ponowne zastosowanie ochrony.

### Czy Aspose.Cells obsługuje inne formaty oprócz Excela?
Oczywiście! Aspose.Cells może konwertować i zapisywać skoroszyty do różnych formatów, w tym CSV, PDF i HTML.

### Gdzie mogę uzyskać pomoc dotyczącą Aspose.Cells?
 Możesz odwiedzić[Forum wsparcia Aspose](https://forum.aspose.com/c/cells/9) w celu uzyskania pomocy i wskazówek od społeczności.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
