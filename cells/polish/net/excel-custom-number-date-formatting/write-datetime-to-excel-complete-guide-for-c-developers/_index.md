---
category: general
date: 2026-04-07
description: Zapisz datę i czas do Excela przy użyciu C#. Dowiedz się, jak wstawić
  datę do arkusza, obsłużyć wartość daty w komórce Excela oraz przekształcić datę
  w japońskim kalendarzu w kilku prostych krokach.
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: pl
og_description: Szybko zapisz datę i czas w Excelu. Ten przewodnik pokazuje, jak wstawić
  datę do arkusza, zarządzać wartością daty w komórce Excela oraz konwertować datę
  z japońskiego kalendarza przy użyciu C#.
og_title: Zapisz datę i godzinę do Excela – krok po kroku tutorial C#
tags:
- C#
- Excel automation
- Aspose.Cells
title: Zapis daty i godziny do Excela – Kompletny przewodnik dla programistów C#
url: /pl/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zapis daty i czasu do Excela – Kompletny przewodnik dla programistów C#

Czy kiedykolwiek potrzebowałeś **zapis daty i czasu do Excela**, ale nie byłeś pewien, które wywołanie API faktycznie zapisuje prawidłową datę Excela? Nie jesteś jedyny. W wielu narzędziach korporacyjnych musimy wstawić obiekt C# `DateTime` do arkusza kalkulacyjnego, a wynik powinien zachowywać się jak prawdziwa data Excela — dająca się sortować, filtrować i gotowa do tabel przestawnych.  

W tym samouczku przeprowadzimy Cię przez dokładne kroki, aby *wstawić datę do arkusza* przy użyciu Aspose.Cells, wyjaśnimy, dlaczego ustawienie kultury ma znaczenie, i pokażemy, jak **przekształcić datę z japońskiego kalendarza** na zwykły `DateTime` przed jej zapisem. Po zakończeniu będziesz mieć samodzielny fragment kodu, który możesz skopiować i wkleić do dowolnego projektu .NET.

## Czego będziesz potrzebować

- **.NET 6+** (lub dowolna nowsza wersja .NET; kod działa również na .NET Framework)  
- **Aspose.Cells for .NET** – pakiet NuGet umożliwiający manipulację plikami Excel bez zainstalowanego Office.  
- Podstawowa znajomość C# `DateTime` oraz kultur.  

Bez dodatkowych bibliotek, bez interfejsu COM i bez wymaganego zainstalowanego Excela. Jeśli już masz instancję arkusza (`ws`), możesz od razu przystąpić.

## Krok 1: Ustawienie japońskiej kultury (Konwersja daty z japońskiego kalendarza)

Gdy otrzymujesz datę w formacie `"R02/05/01"` (Reiwa 2, 1 maja), musisz poinformować .NET, jak interpretować symbole epok. Japoński kalendarz nie jest domyślnym kalendarzem gregoriańskim, więc tworzymy obiekt `CultureInfo`, który zamienia jego kalendarz na `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**Dlaczego to ważne:**  
Jeśli spróbujesz sparsować ciąg znaków przy użyciu domyślnej kultury, .NET zgłosi wyjątek formatu, ponieważ nie potrafi dopasować `R` (epoki Reiwa) do roku. Dzięki zamianie na `JapaneseCalendar` parser rozumie symbole epok i przekształca je na właściwy rok gregoriański.

## Krok 2: Parsowanie ciągu opartego na erze do `DateTime`

Teraz, gdy kultura jest gotowa, możemy bezpiecznie wywołać `DateTime.ParseExact`. Format ciągu `"ggyy/MM/dd"` informuje parser:

- `gg` – oznaczenie ery (np. `R` dla Reiwa)  
- `yy` – dwucyfrowy rok w ramach ery  
- `MM/dd` – miesiąc i dzień.

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**Wskazówka:**  
Jeśli możesz otrzymywać daty w innych formatach (np. `"Heisei 30/12/31"`), otocz parsowanie w `try/catch` i użyj `DateTime.TryParseExact` jako awaryjnego rozwiązania. Zapobiegnie to awarii całego procesu importu z powodu jednej niepoprawnej linii.

## Krok 3: Zapis `DateTime` do komórki Excela (Wartość daty w komórce Excela)

Aspose.Cells traktuje obiekt .NET `DateTime` jako natywną datę Excela, gdy używasz `PutValue`. Biblioteka automatycznie konwertuje ticki na numer seryjny Excela (liczbę dni od 1900‑01‑00). Oznacza to, że komórka wyświetli prawidłową **wartość daty w komórce Excela** i możesz ją później sformatować przy użyciu wbudowanych stylów dat w Excelu.

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**Co zobaczysz w Excelu:**  
Komórka C1 zawiera teraz numer seryjny `44796`, który Excel wyświetla jako `2020‑05‑01` (lub w innym zastosowanym formacie). Wartość podstawowa jest prawdziwą datą, a nie ciągiem znaków, więc sortowanie działa zgodnie z oczekiwaniami.

## Krok 4: Zapisanie skoroszytu (Podsumowanie)

Jeśli jeszcze nie zapisałeś skoroszytu, zrób to teraz. Ten krok nie dotyczy bezpośrednio zapisu daty i czasu, ale kończy cały proces.

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

To wszystko — cztery zwięzłe kroki i udało Ci się **zapis daty i czasu do Excela**, obsługując przy tym datę z japońskiej ery.

---

![write datetime to excel example](/images/write-datetime-to-excel.png "Screenshot showing a C# project writing a DateTime into Excel cell C1")

*Powyższy obrazek ilustruje końcowy plik Excel z datą poprawnie wyświetlaną w komórce C1.*

## Często zadawane pytania i przypadki brzegowe

### Co zrobić, jeśli zmienna worksheet nie jest jeszcze gotowa?

Możesz utworzyć nowy skoroszyt w locie:

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### Jak zachować oryginalny ciąg daty z japońską erą w arkuszu?

Jeśli potrzebujesz zarówno oryginalnego ciągu, jak i sparsowanej daty, zapisz je w sąsiednich komórkach:

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### Czy to działa ze starszymi wersjami .NET?

Tak. `JapaneseCalendar` istnieje od .NET 2.0, a Aspose.Cells obsługuje .NET Framework 4.5+. Upewnij się tylko, że odwołujesz się do właściwego zestawu.

### A co z strefami czasowymi?

`DateTime.ParseExact` zwraca **Kind** jako `Unspecified`. Jeśli Twoje źródłowe daty są w UTC, najpierw je skonwertuj:

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### Czy mogę ustawić własny format daty (np. „yyyy年MM月dd日”)?

Oczywiście. Użyj właściwości `Style.Custom`:

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

Teraz Excel wyświetli `2020年05月01日`, jednocześnie przechowując prawdziwą wartość daty.

## Podsumowanie

Omówiliśmy wszystko, co potrzebujesz, aby **zapis daty i czasu do Excela** z C#:

1. **Skonfiguruj** japońską kulturę z `JapaneseCalendar`, aby **przekształcić ciągi dat z japońskiego kalendarza**.  
2. **Parsuj** ciąg oparty na erze przy użyciu `DateTime.ParseExact`.  
3. **Wstaw** otrzymany `DateTime` do komórki, zapewniając prawidłową **wartość daty w komórce Excela**.  
4. **Zapisz** skoroszyt, aby dane pozostały.  

Dzięki tym czterem krokom możesz bezpiecznie **wstawiać datę do arkusza** niezależnie od formatu źródłowego. Kod jest w pełni gotowy do uruchomienia, wymaga jedynie Aspose.Cells i działa na każdym nowoczesnym środowisku .NET.

## Co dalej?

- **Import zbiorczy:** Przejdź pętlą po wierszach w CSV, parsuj każdą japońską datę i zapisuj je w kolejnych komórkach.  
- **Stylowanie:** Zastosuj formatowanie warunkowe, aby podświetlić przeterminowane terminy.  
- **Wydajność:** Użyj `WorkbookDesigner` lub buforowania `CellStyle` przy obsłudze tysięcy wierszy.  

Śmiało eksperymentuj — zamień japońską erę na kalendarz gregoriański, zmień docelową komórkę lub wyeksportuj do innego formatu pliku (CSV, ODS). Główna idea pozostaje ta sama: parsuj, konwertuj i **zapisuj datę i czas do Excela** z pewnością.

Miłego kodowania i niech Twoje arkusze kalkulacyjne zawsze sortują się poprawnie!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}