---
title: Zamień tag na tekst w polu tekstowym w programie Excel
linktitle: Zamień tag na tekst w polu tekstowym w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Bezproblemowo zastępuj tekst w polach tekstowych w arkuszach Excela za pomocą Aspose.Cells dla .NET. Przewodnik krok po kroku po automatyzacji programu Excel.
weight: 11
url: /pl/net/excel-shape-text-modifications/replace-tag-text-textbox-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zamień tag na tekst w polu tekstowym w programie Excel

## Wstęp
W tym artykule zajmiemy się konkretnym zadaniem: zastępowaniem tagów tekstem wewnątrz pól tekstowych w arkuszu Excela za pomocą Aspose.Cells. Przeprowadzimy Cię przez cały proces krok po kroku, zapewniając, że zrozumiesz każdy szczegół. Do końca tego samouczka nie tylko poszerzysz swoją wiedzę na temat Aspose.Cells, ale także usprawnisz zadania związane z Excelem!
## Wymagania wstępne
Zanim zaczniesz, musisz przygotować kilka rzeczy:
1. Visual Studio: Upewnij się, że masz zainstalowane Visual Studio. To elastyczne IDE, które sprawia, że kodowanie w C# jest dziecinnie proste.
2.  Biblioteka Aspose.Cells: Jeśli jeszcze tego nie zrobiłeś, pobierz bibliotekę Aspose.Cells dla platformy .NET ze strony[strona](https://releases.aspose.com/cells/net/)Możesz również pobrać bezpłatną wersję próbną, aby sprawdzić jej funkcje.
3. Podstawowa znajomość języka C#: Podstawowa znajomość programowania w języku C# znacznie ułatwi Ci korzystanie z tego przewodnika.
Teraz, gdy już wszystko jest gotowe, możemy przejść do przyjemniejszej części — pisania kodu!
## Importuj pakiety
Po pierwsze — zaimportujmy niezbędne pakiety. Jest to kluczowe, ponieważ bez odpowiednich importów kod nie rozpozna klas i metod, których będziemy używać.
## Rozpocznij swój projekt C#
Otwórz program Visual Studio i utwórz nowy projekt w języku C#, najlepiej aplikację konsolową, dzięki czemu będziesz mógł łatwo przeglądać dane wyjściowe.
## Dodaj odniesienie Aspose.Cells
- Kliknij prawym przyciskiem myszy swój projekt w Eksploratorze rozwiązań.
- Wybierz „Dodaj” > „Odniesienie”.
- Przejdź do lokalizacji, w której pobrałeś bibliotekę Aspose.Cells i uwzględnij ją w swoim projekcie.
## Importuj niezbędne przestrzenie nazw
 Po dodaniu odniesienia dodaj następujący kod`using` dyrektywa na górze pliku głównego:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Dzięki temu uzyskasz dostęp do klas w przestrzeni nazw Aspose.Cells.
Teraz, gdy skonfigurowaliśmy nasze środowisko, przejdźmy do soczystej części — kodowania! Naszym celem jest znalezienie określonych tagów w polach tekstowych w pliku Excel i zastąpienie ich dostarczonym tekstem.
## Krok 1: Zdefiniuj katalog źródłowy i wyjściowy
Najpierw musimy określić, gdzie znajduje się nasz plik źródłowy Excel i gdzie chcemy zapisać zmodyfikowaną wersję.
```csharp
// Katalog źródłowy i wyjściowy
string sourceDir = "Your Document Directory"; // Zmień na swój katalog
string outputDir = "Your Document Directory"; // Zmień na swój katalog
```
## Krok 2: Załaduj skoroszyt
Tutaj załadujemy nasz skoroszyt programu Excel. Jeśli plik nie istnieje, pojawi się błąd. Upewnij się więc, że ścieżka do pliku jest poprawna!
```csharp
Workbook wb = new Workbook(sourceDir + "sampleReplaceTagWithText.xlsx");
```
 Tutaj ładujemy istniejący plik Excela o nazwie`sampleReplaceTagWithText.xlsx`.
## Krok 3: Zdefiniuj znaczniki i tekst zastępczy
Następnie musimy zdefiniować tagi, których szukamy i to, czym chcemy je zastąpić.
```csharp
string tag = "TAG_2$TAG_1";
string replace = "1$ys";
```
 W tym przykładzie tagi są dzielone za pomocą`$`Możesz zastąpić go dowolnym innym ogranicznikiem.
## Krok 4: Przeprowadź pętlę po tagach i zamień je
Stworzymy pętlę, aby przejść przez każdy tag, który chcemy zastąpić. Tutaj dzieje się magia!
```csharp
for (int i = 0; i < tag.Split('$').Length; i++)
{
    sheetReplace(wb, "<" + tag.Split('$')[i] + ">", replace.Split('$')[i]);
}
```
## Krok 5: Zapisz skoroszyt
Teraz, gdy dokonaliśmy naszych zamian, nadszedł czas, aby zapisać zmodyfikowany skoroszyt w pożądanym formacie. Oto jak konwertujemy go do pliku PDF.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
wb.Save(outputDir + "outputReplaceTagWithText.pdf", opts);
```
Można go również zapisać w innych formatach, w tym XLSX.
## Krok 6: Wdrażanie logiki zastępczej
 To właśnie tutaj znajduje się serce naszej funkcjonalności.`sheetReplace` Metoda ta zajmie się faktyczną zamianą w arkuszach kalkulacyjnych Excela.
```csharp
public static void sheetReplace(Workbook workbook, string sFind, string sReplace)
{
    string finding = sFind;
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sheet.Replace(finding, sReplace);
        for (int j = 0; j < 3; j++)
        {
            if (sheet.PageSetup.GetHeader(j) != null)
                sheet.PageSetup.SetHeader(j, sheet.PageSetup.GetHeader(j).Replace(finding, sReplace));
                
            if (sheet.PageSetup.GetFooter(j) != null)
                sheet.PageSetup.SetFooter(j, sheet.PageSetup.GetFooter(j).Replace(finding, sReplace));
        }
    }
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sFind = sFind.Replace("<", "&lt;");
        sFind = sFind.Replace(">", "&gt;");
        foreach (Aspose.Cells.Drawing.TextBox mytextbox in sheet.TextBoxes)
        {
            if (mytextbox.HtmlText != null)
            {
                if (mytextbox.HtmlText.IndexOf(sFind) >= 0)
                {
                    mytextbox.HtmlText = mytextbox.HtmlText.Replace(sFind, sReplace);
                }
            }
        }
    }
}
```
- Najpierw przechodzimy przez każdy arkusz w skoroszycie.
- Zastępujemy znacznik główny nie tylko w zawartości komórki, ale także w nagłówkach i stopkach (jeśli istnieją).
- Na koniec sprawdzamy każde pole tekstowe w arkuszu i zastępujemy znajdujący się w nim tekst na podstawie poszukiwanego przez nas znacznika.
## Wniosek
voila! Teraz nauczyłeś się, jak zastępować tagi tekstem w polach tekstowych w dokumentach Excela za pomocą Aspose.Cells dla .NET. Może to być prawdziwa oszczędność czasu, zwłaszcza w przypadku powtarzających się zadań w arkuszach kalkulacyjnych.
## Najczęściej zadawane pytania
### Czy mogę zamieniać tagi w wielu plikach Excela jednocześnie?
Tak, przeglądając listę plików, możesz zastosować tę samą logikę do wielu plików Excela.
### Czy potrzebuję płatnej licencji, aby korzystać z Aspose.Cells?
 Możesz zacząć od bezpłatnego okresu próbnego, ale aby uzyskać pełną funkcjonalność, musisz kupić licencję. Sprawdź[Opcje zakupu Aspose](https://purchase.aspose.com/buy).
### Czy mogę zastąpić obrazy w polach tekstowych za pomocą Aspose.Cells?
Aspose.Cells zajmuje się głównie tekstem. Jednak możesz manipulować obrazami osobno, jeśli to konieczne.
### W jakich formatach mogę zapisać zmodyfikowany plik Excela?
Można zapisać go w różnych formatach, w tym XLSX, PDF, CSV itp.
### Gdzie mogę znaleźć pomoc dotyczącą Aspose.Cells?
 Wsparcie i zadawanie pytań można znaleźć na stronie[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
