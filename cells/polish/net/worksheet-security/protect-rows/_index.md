---
"description": "Dowiedz się, jak chronić wiersze w arkuszu kalkulacyjnym programu Excel za pomocą Aspose.Cells dla .NET. Zabezpiecz swoje dane za pomocą ochrony na poziomie wiersza i zapobiegaj przypadkowym zmianom."
"linktitle": "Chroń wiersze w arkuszu kalkulacyjnym za pomocą Aspose.Cells"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Chroń wiersze w arkuszu kalkulacyjnym za pomocą Aspose.Cells"
"url": "/pl/net/worksheet-security/protect-rows/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Chroń wiersze w arkuszu kalkulacyjnym za pomocą Aspose.Cells

## Wstęp
Praca z plikami Excela programowo jest często zadaniem, które wymaga nie tylko manipulacji danymi, ale także ich ochrony. Niezależnie od tego, czy chcesz chronić poufne dane, czy zapobiec przypadkowej edycji, ochrona wierszy w arkuszu kalkulacyjnym może być kluczowym krokiem. W tym samouczku zagłębimy się w to, jak chronić określone wiersze w arkuszu kalkulacyjnym Excela przy użyciu Aspose.Cells dla .NET. Przeprowadzimy przez wszystkie niezbędne kroki, od przygotowania środowiska po wdrożenie funkcji ochrony w prosty, łatwy do naśladowania sposób.
## Wymagania wstępne
Zanim zaczniesz chronić wiersze w arkuszu kalkulacyjnym, musisz zadbać o kilka rzeczy:
1. Aspose.Cells dla .NET: Upewnij się, że masz zainstalowany Aspose.Cells dla .NET na swoim komputerze deweloperskim. Jeśli jeszcze tego nie zrobiłeś, możesz łatwo pobrać go z [Strona pobierania Aspose Cells](https://releases.aspose.com/cells/net/).
2. Visual Studio lub dowolne IDE .NET: Aby wdrożyć rozwiązanie, musisz mieć skonfigurowane środowisko programistyczne. Visual Studio to świetna opcja, ale każde IDE zgodne z .NET będzie działać.
3. Podstawowa wiedza o języku C#: Zrozumienie podstaw programowania w języku C# pomoże Ci uczestniczyć w samouczku i modyfikować przykładowy kod zgodnie z własnymi potrzebami.
4. Dokumentacja API Aspose.Cells: Zapoznaj się z [Dokumentacja Aspose.Cells dla .NET](https://reference.aspose.com/cells/net/) aby uzyskać przegląd struktury klas i metod stosowanych w bibliotece.
Jeśli wszystkie wymagania wstępne zostały spełnione, możemy przejść bezpośrednio do wdrażania.
## Importuj pakiety
Na początek musisz zaimportować wymagane pakiety. Te biblioteki są kluczowe dla interakcji z plikami Excel w Twoim projekcie C#.
```csharp
using System.IO;
using Aspose.Cells;
```
Po zaimportowaniu niezbędnych pakietów możesz rozpocząć kodowanie. 
Teraz podzielmy proces na mniejsze kroki, aby było Ci bardzo łatwo go śledzić. Każdy krok będzie koncentrował się na konkretnej części implementacji, zapewniając, że będziesz w stanie ją szybko zrozumieć i zastosować. 
## Krok 1: Utwórz nowy skoroszyt i arkusz kalkulacyjny
Zanim zastosujesz jakiekolwiek ustawienia ochrony, musisz utworzyć nowy skoroszyt i wybrać arkusz, z którym chcesz pracować. Będzie to Twój dokument roboczy.
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
// Utwórz katalog, jeśli jeszcze go nie ma.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Utwórz nowy skoroszyt.
Workbook wb = new Workbook();
// Utwórz obiekt arkusza kalkulacyjnego i uzyskaj pierwszy arkusz.
Worksheet sheet = wb.Worksheets[0];
```
W tym przykładzie tworzymy nowy skoroszyt z pojedynczym arkuszem (co jest domyślnym ustawieniem podczas tworzenia nowego skoroszytu za pomocą Aspose.Cells). Następnie pobieramy pierwszy arkusz w skoroszycie, który będzie celem naszej ochrony wiersza.
## Krok 2: Zdefiniuj obiekty Style i StyleFlag
Następnym krokiem jest zdefiniowanie obiektów stylu i flagi stylu. Te obiekty pozwalają modyfikować właściwości komórki, takie jak to, czy jest zablokowana czy odblokowana.
```csharp
// Zdefiniuj obiekt stylu.
Style style;
// Zdefiniuj obiekt styleflag.
StyleFlag flag;
```
Będziesz używać tych obiektów w późniejszych krokach, aby dostosować właściwości komórek i zastosować je w arkuszu kalkulacyjnym.
## Krok 3: Odblokuj wszystkie kolumny w arkuszu kalkulacyjnym
Domyślnie wszystkie komórki w arkuszu kalkulacyjnym programu Excel są zablokowane. Jednak gdy chronisz arkusz kalkulacyjny, stan zablokowania jest wymuszany. Aby upewnić się, że chronione są tylko określone wiersze lub komórki, możesz najpierw odblokować wszystkie kolumny. Ten krok jest niezbędny, jeśli chcesz chronić tylko określone wiersze.
```csharp
// Przejdź przez wszystkie kolumny arkusza kalkulacyjnego i odblokuj je.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
W tym kodzie przechodzimy przez wszystkie 256 kolumn w arkuszu kalkulacyjnym (arkusze kalkulacyjne programu Excel mają maksymalnie 256 kolumn, indeksowanych od 0 do 255) i ustawiamy ich `IsLocked` nieruchomość do `false`Ta akcja zapewnia odblokowanie wszystkich kolumn, ale nadal zablokujemy określone wiersze później.
## Krok 4: Zablokuj pierwszy rząd
Po odblokowaniu kolumn następnym krokiem jest zablokowanie określonych wierszy, które chcesz chronić. W tym przykładzie zablokujemy pierwszy wiersz. Dzięki temu użytkownicy nie będą mogli go modyfikować, podczas gdy inne wiersze pozostaną odblokowane.
```csharp
// Pobierz styl pierwszego rzędu.
style = sheet.Cells.Rows[0].Style;
// Zamknij to.
style.IsLocked = true;
// Utwórz instancję flagi.
flag = new StyleFlag();
// Ustaw ustawienie blokady.
flag.Locked = true;
// Zastosuj styl do pierwszego wiersza.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Tutaj uzyskujemy dostęp do stylu pierwszego wiersza i ustawiamy jego `IsLocked` nieruchomość do `true`. Następnie używamy `ApplyRowStyle()` metoda zastosowania stylu blokady do całego wiersza. Możesz powtórzyć ten krok, aby zablokować dowolne inne wiersze, które chcesz chronić.
## Krok 5: Zabezpiecz arkusz
Teraz, gdy odblokowaliśmy i zablokowaliśmy niezbędne wiersze, czas zabezpieczyć arkusz kalkulacyjny. Ochrona zapewnia, że nikt nie może modyfikować zablokowanych wierszy lub komórek, chyba że usunie hasło zabezpieczające (jeśli jest podane).
```csharp
// Chroń arkusz.
sheet.Protect(ProtectionType.All);
```
tym kroku stosujemy ochronę całego arkusza za pomocą `ProtectionType.All`. Ten typ ochrony oznacza, że wszystkie aspekty arkusza, w tym zablokowane wiersze i komórki, są chronione. Możesz również dostosować tę ochronę, określając różne typy ochrony, jeśli to konieczne.
## Krok 6: Zapisz skoroszyt
Na koniec musimy zapisać skoroszyt po zastosowaniu niezbędnych stylów i ochrony. Skoroszyt można zapisać w różnych formatach, takich jak Excel 97-2003, Excel 2010 itp.
```csharp
// Zapisz plik Excela.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Ta linia kodu zapisuje skoroszyt w formacie Excel 97-2003 ze zmianami. Możesz zmienić format pliku według swoich potrzeb, wybierając z różnych `SaveFormat` opcje.
## Wniosek
I masz to! Udało Ci się nauczyć, jak chronić wiersze w arkuszu kalkulacyjnym za pomocą Aspose.Cells dla .NET. Postępując zgodnie z powyższymi krokami, możesz odblokować lub zablokować dowolne wiersze lub kolumny w razie potrzeby i zastosować ochronę, aby zapewnić integralność danych.
## Najczęściej zadawane pytania
### Jak mogę chronić wiele wierszy jednocześnie?  
Możesz przejść przez wiele wierszy i zastosować styl blokowania do każdego z nich z osobna. Po prostu zamień `0` z indeksem wiersza, który chcesz zablokować.
### Czy mogę ustawić hasło zabezpieczające arkusz?  
Tak! Możesz przekazać hasło do `sheet.Protect()` metoda wymuszania ochrony hasłem.
### Czy mogę odblokować komórki zamiast całych kolumn?  
Tak! Zamiast odblokowywać kolumny, możesz odblokować poszczególne komórki, modyfikując ich właściwości stylu.
### Co się stanie, jeśli spróbuję edytować chroniony wiersz?  
Gdy wiersz jest chroniony, program Excel uniemożliwia edycję zablokowanych komórek, chyba że wyłączysz ochronę arkusza.
### Czy mogę chronić konkretne zakresy z rzędu?  
Tak! Możesz zablokować poszczególne zakresy w rzędzie, ustawiając `IsLocked` właściwość dla określonych komórek w zakresie.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}