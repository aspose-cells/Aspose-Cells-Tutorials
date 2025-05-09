---
"description": "Dowiedz się, jak scalać komórki w nazwanym zakresie za pomocą Aspose.Cells dla .NET w tym samouczku krok po kroku. Odkryj, jak formatować, stylizować i automatyzować raporty programu Excel."
"linktitle": "Scalanie komórek w nazwanym zakresie w programie Excel"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Scalanie komórek w nazwanym zakresie w programie Excel"
"url": "/pl/net/excel-advanced-named-ranges/merge-cells-in-named-range/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Scalanie komórek w nazwanym zakresie w programie Excel

## Wstęp

Podczas pracy z plikami Excela programowo, jednym z typowych zadań, na jakie możesz się natknąć, jest scalanie komórek w obrębie nazwanego zakresu. Niezależnie od tego, czy automatyzujesz generowanie raportów, tworzysz pulpity nawigacyjne, czy po prostu zarządzasz dużymi zestawami danych, scalanie komórek jest niezbędną techniką. W tym samouczku zbadamy, jak scalać komórki w obrębie nazwanego zakresu przy użyciu Aspose.Cells dla .NET — potężnej biblioteki, która umożliwia programistom manipulowanie plikami Excela bez konieczności instalowania programu Microsoft Excel.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz przygotowane następujące rzeczy:

- Aspose.Cells dla .NET: Możesz pobrać go ze strony [Strona wydań Aspose.Cells](https://releases.aspose.com/cells/net/).
- .NET Framework zainstalowany na Twoim komputerze.
- Podstawowa znajomość języka C#: Pomocna będzie znajomość takich pojęć, jak klasy, metody i obiekty.

## Importuj pakiety

Zanim przejdziemy do kodowania, musisz zaimportować niezbędne przestrzenie nazw. Te przestrzenie nazw zapewnią Ci dostęp do funkcjonalności biblioteki Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

Mając już za sobą wymagania wstępne i pakiety, możemy przejść do przyjemniejszej części: kodowania!

Poniżej przedstawiono sposób scalania komórek w nazwanym zakresie w arkuszu programu Excel przy użyciu Aspose.Cells dla platformy .NET.

## Krok 1: Utwórz nowy skoroszyt

Pierwszą rzeczą, której potrzebujemy, jest skoroszyt. Skoroszyt w terminologii Excela jest odpowiednikiem pliku Excela. Utwórzmy jeden.

```csharp
// Utwórz nowy skoroszyt.
Workbook wb1 = new Workbook();
```

Dzięki zainicjowaniu nowego skoroszytu mamy teraz pusty plik Excela gotowy do manipulacji. To jak rozpoczęcie od pustego płótna!

## Krok 2: Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego

Każdy skoroszyt zawiera arkusze, a w tym przypadku chcemy pracować z pierwszym. Weźmy go!

```csharp
// Pobierz pierwszy arkusz ze skoroszytu.
Worksheet worksheet1 = wb1.Worksheets[0];
```

Pomyśl o arkuszu kalkulacyjnym jako o poszczególnych kartach w pliku Excel, gdzie znajdują się rzeczywiste dane. Domyślnie uzyskujemy dostęp do pierwszej karty.

## Krok 3: Utwórz zakres komórek

Teraz, gdy mamy nasz arkusz kalkulacyjny, czas utworzyć zakres. Zakres odnosi się do bloku komórek, który może obejmować wiele wierszy i kolumn.

```csharp
// Utwórz zakres.
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

Tutaj wybieramy komórki od D6 do I12 — blok obejmujący wiele wierszy i kolumn. Wkrótce połączymy ten zakres!

## Krok 4: Nazwij zakres

Nadanie nazwy zakresowi ułatwia późniejsze odwołanie się do niego, zwłaszcza w przypadku dużych zbiorów danych.

```csharp
// Podaj nazwę zakresu.
mrange.Name = "TestRange";
```

Nazywając ten zakres „TestRange”, możemy go szybko pobrać później w kodzie, bez konieczności ponownego określania współrzędnych komórki.

## Krok 5: Scalanie zakresu komórek

A teraz czas na magię — scalenie komórek z zakresu, który właśnie utworzyliśmy!

```csharp
// Połącz komórki zakresu.
mrange.Merge();
```

Ten krok łączy wszystkie komórki od D6 do I12 w jedną komórkę. Idealne do rzeczy takich jak tytuły lub podsumowania!

## Krok 6: Pobierz nazwany zakres

Gdy komórki zostaną połączone, możemy chcieć zastosować pewne formatowanie. Najpierw pobierzmy nasz nazwany zakres.

```csharp
// Uzyskaj zasięg.
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

Pobranie zakresu według nazwy pozwala na wykonanie dalszych operacji, takich jak dodawanie stylów lub wprowadzanie danych.

## Krok 7: Zdefiniuj styl dla połączonych komórek

Jaki pożytek ze scalonej komórki, jeśli nie wygląda na wypolerowaną? Utwórzmy obiekt stylu, aby wyrównać tekst i zastosować kolor tła.

```csharp
// Zdefiniuj obiekt stylu.
Style style = wb1.CreateStyle();

// Ustaw wyrównanie.
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

Tutaj wyrównujemy tekst poziomo i pionowo w środku i ustawiamy jasnoniebieski (aqua) kolor tła. Stylowo, prawda?

## Krok 8: Zastosuj styl do zakresu

Po zdefiniowaniu stylu czas zastosować go do scalonego zakresu.

```csharp
// Utwórz obiekt StyleFlag.
StyleFlag flag = new StyleFlag();

// Włącz atrybut stylu względnego.
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

// Zastosuj styl do zakresu.
range1.ApplyStyle(style, flag);
```

Ten `StyleFlag` informuje Aspose.Cells, jakie właściwości stylu zastosować — wyrównanie, cieniowanie itd. Dzięki temu masz szczegółową kontrolę nad sposobem stosowania stylu.

## Krok 9: Wprowadź dane do scalonego zakresu

Czym jest sformatowany zakres bez zawartości? Dodajmy trochę tekstu.

```csharp
// Wprowadź dane do zakresu.
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

Umieszcza tekst „Welcome to Aspose APIs” w pierwszej komórce naszego scalonego zakresu. Po scaleniu komórki tekst ten będzie obejmował wszystkie komórki od D6 do I12.

## Krok 10: Zapisz plik Excel

Na koniec zapiszmy skoroszyt jako plik programu Excel.

```csharp
// Zapisz plik Excela.
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

Tutaj skoroszyt zostanie zapisany pod nazwą „outputMergeCellsInNamedRange.xlsx” w określonym katalogu.

## Wniosek

masz to! Udało Ci się połączyć komórki w nazwanym zakresie, zastosować piękne formatowanie, a nawet wprowadzić dane — wszystko za pomocą Aspose.Cells dla .NET. Niezależnie od tego, czy pracujesz nad automatyzacją raportów, manipulujesz plikami Excela, czy po prostu uczysz się nowych technik, ten przewodnik krok po kroku powinien dać Ci potrzebne podstawy.

## Najczęściej zadawane pytania

### Czy mogę scalić wiele nieprzylegających do siebie zakresów w Aspose.Cells?  
Nie, w Aspose.Cells można scalać tylko sąsiadujące komórki.

### Czy mogę programowo cofnąć operację scalania?  
Po połączeniu komórek możesz je rozdzielić za pomocą `UnMerge()` metoda w Aspose.Cells.

### Czy scalanie komórek powoduje usunięcie zawartych w nich danych?  
Jeśli przed scaleniem w komórkach znajdowały się jakieś dane, zostaną zachowane dane z pierwszej komórki zakresu.

### Czy mogę zastosować różne style do poszczególnych komórek w ramach scalonego zakresu?  
Nie, scalony zakres działa jak pojedyncza komórka, więc nie można stosować różnych stylów do poszczególnych komórek w jego obrębie.

### Jak uzyskać dostęp do połączonej komórki po scaleniu?  
Po scaleniu nadal można uzyskać dostęp do scalonej komórki, korzystając ze współrzędnych jej lewego górnego rogu.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}