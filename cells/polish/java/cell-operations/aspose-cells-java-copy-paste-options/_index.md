---
date: '2026-02-22'
description: Dowiedz się, jak zautomatyzować raportowanie w Excelu przy użyciu Aspose.Cells
  w Javie, korzystając z CopyOptions i PasteOptions, aby zachować dokładność formuł
  i wklejać tylko widoczne wartości.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Automatyzacja raportowania w Excelu – opanowanie CopyOptions i PasteOptions
  w Javie z Aspose.Cells
url: /pl/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatyzuj raportowanie Excel przy użyciu Aspose.Cells: CopyOptions i PasteOptions w Javie

Czy chcesz **automatyzować raportowanie Excel** przy użyciu Javy? Dzięki Aspose.Cells możesz programowo kopiować, wklejać i modyfikować formuły, aby Twoje raporty były dokładne, a jedynie potrzebne dane były przenoszone. W tym samouczku przejdziemy przez dwie kluczowe funkcje — **CopyOptions.ReferToDestinationSheet** i **PasteOptions** — które pozwalają zachować odwołania do formuł oraz wklejać wartości tylko z widocznych komórek.

## Szybkie odpowiedzi
- **Co robi `CopyOptions.ReferToDestinationSheet`?** Dostosowuje formuły, aby wskazywały na docelowy arkusz podczas kopiowania danych.  
- **Jak wkleić tylko widoczne komórki?** Ustaw `PasteOptions.setOnlyVisibleCells(true)` wraz z `PasteType.VALUES`.  
- **Jakiej wersji biblioteki potrzebuję?** Aspose.Cells 25.3 lub nowsza.  
- **Czy potrzebna jest licencja do produkcji?** Tak, stała lub tymczasowa licencja usuwa ograniczenia wersji ewaluacyjnej.  
- **Czy mogę używać Maven lub Gradle?** Oba są wspierane; zobacz fragmenty zależności poniżej.

## Co to jest „automatyzacja raportowania Excel”?
Automatyzacja raportowania Excel oznacza programowe generowanie, konsolidowanie i formatowanie skoroszytów Excel, eliminując ręczne kroki kopiowania‑wklejania i zmniejszając liczbę błędów. Aspose.Cells udostępnia bogate API, które pozwala programistom Javy manipulować arkuszami kalkulacyjnymi na dużą skalę.

## Dlaczego używać CopyOptions i PasteOptions w raportowaniu?
- **Zachowanie integralności formuł** przy przenoszeniu danych między arkuszami.  
- **Wykluczanie ukrytych wierszy/kolumn**, aby raporty były czyste i skoncentrowane.  
- **Zwiększenie wydajności** poprzez kopiowanie tylko niezbędnych danych zamiast całych zakresów.

## Wymagania wstępne
- Java 8 lub wyższa.  
- Maven lub Gradle do zarządzania zależnościami.  
- Aspose.Cells 25.3+ (licencja próbna, tymczasowa lub stała).  

## Konfiguracja Aspose.Cells dla Javy

Dodaj bibliotekę do projektu, używając jednej z poniższych metod:

**Maven**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Uzyskanie licencji
- **Bezpłatna wersja próbna** – Pełny zestaw funkcji do oceny.  
- **Licencja tymczasowa** – Usuwa ograniczenia wersji próbnej podczas testów.  
- **Licencja stała** – Zalecana do środowisk produkcyjnych.

Zainicjalizuj Aspose.Cells w kodzie Javy:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Przewodnik krok po kroku

### 1. CopyOptions z ReferToDestinationSheet

#### Przegląd
Ustawienie `CopyOptions.ReferToDestinationSheet` na `true` przepisuje odwołania w formułach, aby wskazywały na nowy arkusz po operacji kopiowania.

#### Krok 1: Inicjalizacja Workbook i Worksheets
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Krok 2: Konfiguracja CopyOptions
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Krok 3: Wykonanie operacji kopiowania
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Dlaczego to ważne*: Formuły, które pierwotnie odwoływały się do `Sheet1`, będą teraz poprawnie wskazywać `DestSheet`, co zapewnia niezawodność automatycznych raportów.

**Wskazówka rozwiązywania problemów**: Jeśli formuły nadal odwołują się do starego arkusza, upewnij się, że `setReferToDestinationSheet(true)` jest wywoływane **przed** kopiowaniem.

### 2. PasteOptions dla wartości‑tylko z widocznych komórek

#### Przegląd
`PasteOptions` pozwala określić, co ma zostać wklejone. Użycie `PasteType.VALUES` razem z `onlyVisibleCells=true` kopiuje wyłącznie wyświetlane wartości, ignorując ukryte wiersze/kolumny oraz formatowanie.

#### Krok 1: Inicjalizacja Workbook i Worksheets
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Krok 2: Konfiguracja PasteOptions
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Krok 3: Wykonanie operacji wklejania
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Dlaczego to ważne*: Idealne do wyodrębniania przefiltrowanych danych lub generowania czystych raportów bez ukrytych wierszy i szumu formatowania.

**Wskazówka rozwiązywania problemów**: Upewnij się, że wiersze/kolumny są rzeczywiście ukryte w Excelu przed kopiowaniem; w przeciwnym razie zostaną uwzględnione.

## Praktyczne zastosowania
1. **Konsolidacja finansowa** – Łączenie miesięcznych arkuszy w głównym skoroszycie przy zachowaniu poprawnych formuł.  
2. **Eksport przefiltrowanych danych** – Pobieranie tylko widocznych wierszy z przefiltrowanej tabeli do arkusza podsumowania.  
3. **Planowane generowanie raportów** – Automatyzacja nocnego tworzenia raportów Excel z precyzyjnymi wartościami komórek i prawidłowymi odwołaniami.

## Rozważania dotyczące wydajności
- **Zwalnianie Workbooków** po zakończeniu (`wb.dispose();`) w celu zwolnienia zasobów natywnych.  
- **Operacje wsadowe** – Grupowanie wielu wywołań kopiuj/wklej w celu zmniejszenia narzutu.  
- **Monitorowanie pamięci** – Duże skoroszyty mogą wymagać zwiększenia przydziału pamięci (`-Xmx2g`).

## Najczęściej zadawane pytania

**P1: Do czego służy `CopyOptions.ReferToDestinationSheet`?**  
Odp: Przepisuje odwołania w formułach, aby wskazywały na docelowy arkusz po kopiowaniu, zapewniając prawidłowość formuł w raportach.

**P2: Jak wkleić tylko widoczne komórki?**  
Odp: Ustaw `PasteOptions.setOnlyVisibleCells(true)` i wybierz `PasteType.VALUES`.

**P3: Czy mogę używać Aspose.Cells bez zakupu licencji?**  
Odp: Tak, dostępna jest wersja próbna lub licencja tymczasowa do oceny, ale do produkcji wymagana jest licencja stała.

**P4: Dlaczego niektóre odwołania są nadal nieprawidłowe po kopiowaniu?**  
Odp: Sprawdź, czy `ReferToDestinationSheet` jest włączone **przed** operacją kopiowania oraz czy źródłowe formuły nie zawierają odwołań do zewnętrznych skoroszytów.

**P5: Jakie są najlepsze praktyki zarządzania pamięcią?**  
Odp: Zwalniaj obiekty `Workbook` po użyciu, przetwarzaj duże pliki w partiach i monitoruj zużycie pamięci JVM.

**P6: Czy można połączyć CopyOptions i PasteOptions w jednej operacji?**  
Odp: Tak, najpierw kopiujesz z użyciem `CopyOptions`, a następnie stosujesz `PasteOptions` na docelowym zakresie.

## Zasoby
- **Dokumentacja**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Pobieranie**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Zakup**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Bezpłatna wersja próbna**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Licencja tymczasowa**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Forum wsparcia**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Ostatnia aktualizacja:** 2026-02-22  
**Testowano z:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose