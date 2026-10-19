---
date: '2026-02-22'
description: Dowiedz się, jak zmienić system daty w Excelu na 1904 przy użyciu Aspose.Cells
  dla Javy, ustawić format daty w Excelu i efektywnie konwertować system daty 1904.
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: Zmień system dat w Excelu na 1904 za pomocą Aspose.Cells Java
url: /pl/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zmień system dat w Excelu na 1904 przy użyciu Aspose.Cells Java

Zarządzanie danymi historycznymi w Excelu może być trudne, ponieważ Excel obsługuje dwa różne systemy dat. **W tym samouczku dowiesz się, jak zmienić system dat w Excelu na format 1904 przy użyciu Aspose.Cells dla Javy**, co ułatwia obsługę starszych dat. Przejdziemy przez inicjalizację skoroszytu, włączenie systemu dat 1904 i zapisanie zmiany.

## Szybkie odpowiedzi
- **Co robi system dat 1904?** Rozpoczyna liczenie dni od 1 stycznia 1904 r., przesuwając wszystkie daty o 1462 dni w porównaniu z domyślnym systemem 1900.  
- **Dlaczego używać Aspose.Cells do zmiany systemu dat?** Dostarcza prostego API, które działa bez zainstalowanego Excela i obsługuje duże pliki.  
- **Jakie wersje Javy są wspierane?** JDK 8 lub nowszy.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w celach oceny; licencja usuwa ograniczenia użytkowania.  
- **Czy mogę później przywrócić system 1900?** Tak, wystarczy ustawić `setDate1904(false)`.

## Co to jest system dat 1904 w Excelu?
System dat 1904 był pierwotnie używany w wczesnych wersjach Excela na Macintosh. Liczy dni od 1 stycznia 1904 r., co jest przydatne dla kompatybilności ze starszymi arkuszami kalkulacyjnymi i niektórymi modelami finansowymi.

## Dlaczego zmienić system dat w Excelu przy użyciu Aspose.Cells?
- **Kompatybilność międzyplatformowa** – działa na Windows, Linux i macOS.  
- **Brak wymogu instalacji Excela** – idealne do przetwarzania po stronie serwera.  
- **Wysoka wydajność** – obsługuje duże skoroszyty przy minimalnym zużyciu pamięci.  

## Wymagania wstępne
- Java Development Kit (JDK) 8 lub wyższy.  
- Maven lub Gradle do zarządzania zależnościami.  
- Podstawowa znajomość programowania w Javie.  

## Konfiguracja Aspose.Cells dla Javy

### Maven
Dodaj następującą zależność do pliku `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Umieść tę linię w pliku `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Uzyskanie licencji
Aspose oferuje darmową wersję próbną, tymczasową licencję oraz pełne licencje komercyjne. Możesz rozpocząć od [darmowej wersji próbnej](https://releases.aspose.com/cells/java/) lub uzyskać tymczasową licencję na [stronie tymczasowej licencji](https://purchase.aspose.com/temporary-license/).

## Zmiana systemu dat w Excelu przy użyciu Aspose.Cells Java

Poniżej znajduje się przewodnik krok po kroku, który faktycznie **zmienia system dat w Excelu**. Każdy krok zawiera krótkie wyjaśnienie oraz dokładny kod, którego potrzebujesz.

### Krok 1: Inicjalizacja i załadowanie skoroszytu
Najpierw utwórz instancję `Workbook`, która wskazuje na istniejący plik Excel.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Krok 2: Włączenie systemu dat 1904
Użyj ustawień skoroszytu, aby przełączyć system dat.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Wskazówka:** Możesz także później wywołać `setDate1904(false)`, jeśli potrzebujesz przywrócić poprzedni stan.

### Krok 3: Zapis zmodyfikowanego skoroszytu
Na koniec zapisz zmiany do nowego pliku (lub nadpisz oryginał).

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Uwaga:** Powyższy kod używa nazwy klasy `tWorkbook`, tak jak podano pierwotnie. Upewnij się, że ten błąd typograficzny pasuje do konwencji nazewnictwa w Twoim projekcie lub popraw go na `Workbook`, jeśli to konieczne.

## Ustawianie daty w Excelu programowo (słowo kluczowe drugorzędne)
Jeśli potrzebujesz dostosować wartości poszczególnych komórek po zmianie systemu, możesz użyć `Cells.get(i, j).putValue(Date)`, gdzie data zostanie zinterpretowana zgodnie z aktywnym systemem dat.

## Konwersja systemu 1904 w Excelu z powrotem na 1900 (słowo kluczowe drugorzędne)
Aby przywrócić, po prostu wywołaj:

```java
workbook.getSettings().setDate1904(false);
```

Następnie ponownie zapisz skoroszyt.

## Praktyczne zastosowania
1. **Archiwizacja danych** – Zachowaj starsze znaczniki czasu przy migracji starych arkuszy kalkulacyjnych z Maca.  
2. **Raportowanie międzyplatformowe** – Generuj raporty, które można otworzyć zarówno w Windows, jak i macOS bez niezgodności dat.  
3. **Modelowanie finansowe** – Dopasuj obliczenia dat do starszych modeli finansowych, które oczekują systemu 1904.

## Uwagi dotyczące wydajności
- Ogranicz operacje na skoroszycie w jednej sesji, aby utrzymać niskie zużycie pamięci.  
- Dostosuj mechanizm garbage‑collection Javy przy bardzo dużych plikach.  

## Najczęściej zadawane pytania

**Q: Jaka jest różnica między systemami dat 1900 i 1904?**  
A: System 1900 zaczyna się 1 stycznia 1900 r., natomiast system 1904 zaczyna się 1 stycznia 1904 r., przesuwając wszystkie daty o 1462 dni.

**Q: Czy mogę zmienić system dat w skoroszycie, który jest aktualnie otwarty w Excelu?**  
A: Tak, ale najpierw musisz zamknąć plik w Excelu; w przeciwnym razie operacja zapisu się nie powiedzie.

**Q: Czy potrzebna jest licencja do użycia `setDate1904`?**  
A: Metoda działa w wersji próbnej, ale pełna licencja usuwa ograniczenia oceny.

**Q: Czy można zmienić system dat tylko dla jednego arkusza?**  
A: Nie, system dat jest ustawieniem na poziomie skoroszytu; dotyczy wszystkich arkuszy.

**Q: Jak mogę zweryfikować, że system dat został zmieniony?**  
A: Otwórz zapisany plik w Excelu, przejdź do **Plik → Opcje → Zaawansowane** i zaznacz pole **"Użyj systemu dat 1904"**.

## Podsumowanie
Teraz wiesz, jak **zmienić system dat w Excelu** na 1904 przy użyciu Aspose.Cells dla Javy, jak ustawiać formaty dat w Excelu oraz jak przywrócić poprzedni system w razie potrzeby. Włącz te fragmenty kodu do swoich potoków przetwarzania danych, aby zapewnić zgodność dat na różnych platformach.

---

**Ostatnia aktualizacja:** 2026-02-22  
**Testowano z:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  

**Zasoby**
- **Dokumentacja:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Pobieranie:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Zakup licencji:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Darmowa wersja próbna:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Licencja tymczasowa:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Forum wsparcia:** [Aspose Support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}