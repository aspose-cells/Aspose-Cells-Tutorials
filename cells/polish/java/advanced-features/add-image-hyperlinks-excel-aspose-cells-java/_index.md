---
date: '2026-02-16'
description: Dowiedz się, jak tworzyć klikalne obrazy w Excelu przy użyciu Aspose.Cells
  for Java, dodając hiperłącza do zdjęć w interaktywnych arkuszach kalkulacyjnych.
keywords:
- image hyperlinks in Excel
- Aspose.Cells for Java
- interactive Excel spreadsheets
title: Utwórz klikalny obraz w Excelu przy użyciu Aspose.Cells dla Javy
url: /pl/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie klikalnego obrazu w Excelu przy użyciu Aspose.Cells dla Javy

## Wprowadzenie

Jeśli chcesz **tworzyć klikalne obrazy w skoroszytach Excel**, które pozwalają użytkownikom przejść do stron internetowych, dokumentów lub innych zasobów jednym kliknięciem, jesteś we właściwym miejscu. W tym samouczku pokażemy, jak Aspose.Cells dla Javy umożliwia **dodawanie obiektów obrazu z hiperłączem w Excelu**, konfigurowanie podpowiedzi ekranowych oraz utrzymanie arkuszy zarówno pięknych, jak i funkcjonalnych.

### Czego się nauczysz
- Inicjalizacji skoroszytu Aspose.Cells w Javie.  
- Wstawiania obrazu i przekształcania go w klikalny hiperlink.  
- Kluczowych metod, takich jak `addHyperlink`, `setPlacement` i `setScreenTip`.  
- Najlepszych praktyk dotyczących wydajności i licencjonowania.

## Szybkie odpowiedzi
- **Jakiej biblioteki potrzebuję?** Aspose.Cells dla Javy.  
- **Czy mogę używać plików .xlsx?** Tak – API działa zarówno z .xls, jak i .xlsx.  
- **Czy potrzebna jest licencja?** Wersja próbna działa w celach ewaluacyjnych; stała licencja jest wymagana w środowisku produkcyjnym.  
- **Ile linii kodu?** Około 20 linii, aby dodać klikalny obraz.  
- **Czy jest wątkowo‑bezpieczna?** Obiekty Workbook nie są wątkowo‑bezpieczne; twórz osobne instancje dla każdego wątku.  
- **Czy mogę dodać podpowiedź ekranową w Excelu?** Tak – użyj `Hyperlink.setScreenTip()`, aby wyświetlić pomocny tekst po najechaniu.

## Jak stworzyć klikalny obraz w Excelu przy użyciu Aspose.Cells dla Javy

### Wymagania wstępne
Zanim rozpoczniesz, upewnij się, że masz:

- **Aspose.Cells dla Javy** (v25.3 lub nowszy).  
- **JDK 8+** zainstalowane.  
- IDE (IntelliJ IDEA, Eclipse lub NetBeans) oraz Maven lub Gradle do zarządzania zależnościami.  

### Wymagane biblioteki
Dodaj Aspose.Cells do swojego projektu:

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
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Uzyskanie licencji
Aspose.Cells jest produktem komercyjnym, ale możesz rozpocząć od darmowej wersji próbnej lub poprosić o tymczasową licencję:

- Darmowa wersja próbna: Pobierz z [Aspose Downloads](https://releases.aspose.com/cells/java/).  
- Licencja tymczasowa: Zamów poprzez [Temporary License page](https://purchase.aspose.com/temporary-license/).  
- Zakup: Długoterminowe użycie dostępne jest pod adresem [Aspose Purchase](https://purchase.aspose.com/buy).

### Podstawowa inicjalizacja
Utwórz skoroszyt i pobierz pierwszy arkusz:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Implementacja krok po kroku

### Krok 1: Przygotuj swój skoroszyt
Zaczynamy od utworzenia nowego skoroszytu i wybrania pierwszego arkusza.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Krok 2: Wstaw etykietę i dostosuj rozmiar komórki
Dodaj opisową etykietę i zapewnij komórce wystarczająco miejsca na obraz.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```

### Krok 3: Dodaj obraz
Wczytaj plik obrazu i umieść go na arkuszu.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```
*Wskazówka*: Zastąp `"path/to/aspose-logo.jpg"` rzeczywistą ścieżką do pliku obrazu.

### Krok 4: Skonfiguruj położenie i dodaj hiperlink
Ustaw obraz jako wolno‑pływający i dołącz do niego hiperlink.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```

### Krok 5: Ustaw podpowiedź ekranową i zapisz skoroszyt
Dodaj pomocną etykietę podpowiedzi i zapisz skoroszyt na dysku.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```

## Dlaczego warto dodać hiperlink do obrazu w Excelu?
Osadzenie klikalnego obrazu pozwala przekształcić elementy brandingowe, ikony lub diagramy w bezpośrednie punkty nawigacyjne. Poprawia to doświadczenie użytkownika w raportach marketingowych, podręcznikach technicznych i arkuszach edukacyjnych, zmniejszając liczbę kliknięć potrzebnych do dotarcia do powiązanej treści.

## Jak dodać podpowiedź ekranową w Excelu
Metoda `setScreenTip` umożliwia określenie tekstu wyświetlanego po najechaniu kursorem na obraz. Jest to idealne rozwiązanie do podania kontekstu, np. „Zobacz szczegóły produktu” lub „Otwórz wideo instruktażowe”.

## Wskazówki rozwiązywania problemów
- **Błędy ścieżki obrazu** – sprawdź dokładnie lokalizację pliku i upewnij się, że aplikacja ma uprawnienia do odczytu.  
- **Licencja nie zastosowana** – po wygaśnięciu wersji próbnej hiperlinki mogą przestać działać; zastosuj ważną licencję za pomocą `License.setLicense`.  
- **Hiperlink nie klikalny** – zweryfikuj, czy `PlacementType` obrazu jest ustawiony na `FREE_FLOATING`.

## Praktyczne zastosowania
Osadzanie klikalnych obrazów jest przydatne w wielu scenariuszach:

1. **Raporty marketingowe** – łączenie logo marki ze stronami produktów.  
2. **Dokumentacja techniczna** – dołączanie diagramów otwierających szczegółowe schematy.  
3. **Arkusze edukacyjne** – przekształcanie ikon w skróty do dodatkowych filmów.  
4. **Dashboardy projektowe** – umożliwienie ikonom statusu otwierania powiązanych trackerów zadań.

## Uwagi dotyczące wydajności
- Utrzymuj rozmiary plików obrazów w rozsądnych granicach; duże obrazy zwiększają zużycie pamięci skoroszytu.  
- Usuwaj nieużywane obiekty (`workbook.dispose()`), gdy przetwarzasz wiele plików w pętli.  
- Aktualizuj do najnowszej wersji Aspose.Cells, aby korzystać z usprawnień wydajności i poprawek błędów.

## Podsumowanie
Teraz wiesz, **jak dodać hiperlink** do obrazów w Excelu przy użyciu Aspose.Cells dla Javy, co umożliwia **tworzenie klikalnych obrazów w Excelu** w bardziej bogatych i interaktywnych skoroszytach. Eksperymentuj z różnymi adresami URL, podpowiedziami ekranowymi i położeniem obrazów, aby dopasować je do swoich potrzeb raportowych. Następnie możesz rozważyć dodawanie hiperlinków do kształtów lub automatyzację masowego wstawiania obrazów w wielu arkuszach.

## Najczęściej zadawane pytania

**P:** Jaki jest maksymalny rozmiar obrazu obsługiwany przez Aspose.Cells dla Javy?  
**O:** Nie ma ścisłego limitu, ale bardzo duże obrazy mogą wpływać na wydajność i zwiększać rozmiar pliku.

**P:** Czy mogę używać tej funkcji z plikami .xlsx?  
**O:** Tak, API działa zarówno z formatami `.xls`, jak i `.xlsx`.

**P:** Jak powinienem obsługiwać wyjątki przy dodawaniu hiperlinków?  
**O:** Otocz kod blokiem try‑catch i loguj szczegóły `Exception`, aby diagnozować problemy ze ścieżkami lub licencją.

**P:** Czy można usunąć hiperlink z obrazu po jego dodaniu?  
**O:** Tak – pobierz obiekt `Picture` i wywołaj `pic.getHyperlink().remove()` lub usuń obraz z kolekcji.

**P:** Dlaczego mój hiperlink może nie działać zgodnie z oczekiwaniami?  
**O:** Typowe przyczyny to nieprawidłowy ciąg URL, brak prefiksu `http://`/`https://` lub nielicencjonowana wersja próbna, która wyłącza niektóre funkcje.

## Dodatkowe zasoby
- **Dokumentacja:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Pobranie:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Zakup i wersja próbna:** Odwiedź [Aspose Purchase](https://purchase.aspose.com/buy) lub [Temporary License Page](https://purchase.aspose.com/temporary-license/) w celu uzyskania opcji licencjonowania.  
- **Forum wsparcia:** Po pomoc zajrzyj na [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**Ostatnia aktualizacja:** 2026-02-16  
**Testowano z:** Aspose.Cells dla Javy 25.3  
**Autor:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}