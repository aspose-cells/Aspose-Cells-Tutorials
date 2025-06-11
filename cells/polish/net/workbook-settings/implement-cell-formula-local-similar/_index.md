---
"description": "Dowiedz się, jak zaimplementować formułę komórki, która jest podobna do lokalnej funkcjonalności formuły zakresu w Aspose.Cells dla .NET. Dowiedz się, jak dostosować wbudowane nazwy funkcji programu Excel i nie tylko."
"linktitle": "Implementacja formuły komórki lokalnej podobnej do formuły zakresu lokalnej"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Implementacja formuły komórki lokalnej podobnej do formuły zakresu lokalnej"
"url": "/pl/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Implementacja formuły komórki lokalnej podobnej do formuły zakresu lokalnej

## Wstęp
Aspose.Cells dla .NET to potężny i elastyczny interfejs API do manipulacji arkuszami kalkulacyjnymi, który umożliwia programowe tworzenie, manipulowanie i konwertowanie plików Excel. Jedną z wielu funkcji oferowanych przez Aspose.Cells jest możliwość dostosowania zachowania wbudowanych funkcji Excel, w tym możliwość tworzenia własnych lokalnych nazw funkcji. W tym samouczku przeprowadzimy Cię przez kroki implementacji formuły komórki, która jest podobna do lokalnej funkcjonalności formuły zakresu w Aspose.Cells dla .NET.
## Wymagania wstępne
Zanim zaczniesz, upewnij się, że masz następujące rzeczy:
1. Na Twoim komputerze zainstalowany jest program Microsoft Visual Studio 2010 lub nowszy.
2. Najnowsza wersja biblioteki Aspose.Cells for .NET zainstalowana w Twoim projekcie. Możesz pobrać bibliotekę ze strony [Strona pobierania Aspose.Cells dla .NET](https://releases.aspose.com/cells/net/).
## Importuj pakiety
Aby rozpocząć, musisz zaimportować niezbędne pakiety do swojego projektu C#. Dodaj następujące instrukcje using na górze pliku kodu:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Krok 1: Utwórz klasę niestandardowych ustawień globalizacji
Pierwszym krokiem jest utworzenie niestandardowego `GlobalizationSettings` klasa, która pozwoli Ci zastąpić domyślne zachowanie funkcji Excela. W tym przykładzie zmienimy nazwy `SUM` I `AVERAGE` funkcje do `UserFormulaLocal_SUM` I `UserFormulaLocal_AVERAGE`, odpowiednio.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Zmień nazwę funkcji SUMA według swoich potrzeb.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Zmień nazwę funkcji ŚREDNIA zgodnie ze swoimi potrzebami.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Krok 2: Utwórz nowy skoroszyt i przypisz niestandardowe ustawienia globalizacji
Następnie utwórz nową instancję skoroszytu i przypisz ją niestandardowo `GlobalizationSettings` klasa implementacyjna do skoroszytu `Settings.GlobalizationSettings` nieruchomość.
```csharp
//Utwórz skoroszyt
Workbook wb = new Workbook();
//Przypisz klasę implementacji GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## Krok 3: Dostęp do pierwszego arkusza kalkulacyjnego i komórki
Teraz uzyskajmy dostęp do pierwszego arkusza kalkulacyjnego w skoroszycie i konkretnej komórki w tym arkuszu.
```csharp
//Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
Worksheet ws = wb.Worksheets[0];
//Uzyskaj dostęp do pewnej komórki
Cell cell = ws.Cells["C4"];
```
## Krok 4: Przypisz formuły i wydrukuj formułęLocal
Na koniec przypiszmy `SUM` I `AVERAGE` formuły do komórki i wydrukuj wynik `FormulaLocal` wartości.
```csharp
//Przypisz formułę SUMA i wydrukuj jej FormulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Przypisz formułę AVERAGE i wydrukuj jej FormulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Wniosek
W tym samouczku dowiedziałeś się, jak zaimplementować formułę komórki, która jest podobna do lokalnej funkcjonalności formuły zakresu w Aspose.Cells dla .NET. Tworząc niestandardową `GlobalizationSettings` class, możesz zastąpić domyślne zachowanie funkcji Excela i dostosować lokalne nazwy funkcji do swoich potrzeb. Może to być szczególnie przydatne podczas pracy z zlokalizowanymi lub zinternacjonalizowanymi dokumentami Excela.
## Najczęściej zadawane pytania
### Jaki jest cel `GlobalizationSettings` klasa w Aspose.Cells?
Ten `GlobalizationSettings` Klasa w Aspose.Cells umożliwia dostosowanie zachowania wbudowanych funkcji programu Excel, łącznie z możliwością zmiany lokalnych nazw funkcji.
### Czy mogę zastąpić zachowanie funkcji innych niż `SUM` I `AVERAGE`?
Tak, możesz zmienić zachowanie dowolnej wbudowanej funkcji programu Excel, modyfikując `GetLocalFunctionName` metoda w Twoim niestandardowym `GlobalizationSettings` klasa.
### Czy istnieje sposób na przywrócenie domyślnych wartości nazw funkcji?
Tak, możesz zresetować nazwy funkcji, usuwając niestandardowe `GlobalizationSettings` klasy lub zwracając pusty ciąg znaków z `GetLocalFunctionName` metoda.
### Czy mogę użyć tej funkcji do tworzenia niestandardowych funkcji w Aspose.Cells?
Nie, `GlobalizationSettings` Klasa jest zaprojektowana do nadpisywania zachowania wbudowanych funkcji programu Excel, a nie do tworzenia funkcji niestandardowych. Jeśli musisz utworzyć funkcje niestandardowe, możesz użyć `UserDefinedFunction` Klasa w Aspose.Cells.
### Czy ta funkcja jest dostępna we wszystkich wersjach Aspose.Cells dla .NET?
Tak, `GlobalizationSettings` Klasa i możliwość dostosowywania nazw funkcji są dostępne we wszystkich wersjach Aspose.Cells dla platformy .NET.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}