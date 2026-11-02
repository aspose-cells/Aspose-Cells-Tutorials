---
date: '2026-09-02'
description: Dowiedz się, jak tworzyć klikalne obrazy w skoroszytach Excel przy użyciu
  Aspose.Cells for Java, dodając hyperlinks do obrazów, aby uzyskać interaktywne arkusze
  kalkulacyjne.
keywords:
- create clickable image
- add image hyperlink
- add hyperlink to picture
- interactive excel spreadsheet
- how to add hyperlink
lastmod: '2026-09-02'
og_description: Dowiedz się, jak tworzyć klikalne obrazy w skoroszytach Excel przy
  użyciu Aspose.Cells for Java, dodając hyperlinks, screen tips oraz optymalizując
  performance w zaledwie kilku linijkach kodu.
og_image_alt: 'Developer guide: create clickable image Excel using Aspose.Cells for
  Java'
og_title: Tworzenie klikalnego obrazu w Excelu przy użyciu Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  headline: Create clickable image Excel using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  name: Create clickable image Excel using Aspose.Cells for Java
  steps:
  - name: prepare your workbook
    text: We start by creating a new workbook and selecting the first sheet.
  - name: insert a label and adjust cell size
    text: Add a descriptive label and give the cell enough space for the picture.
  - name: add the image
    text: '`Picture` represents an image object placed on a worksheet. *Tip*: Replace
      `"path/to/aspose-logo.jpg"` with the actual path to your image file.'
  - name: configure placement and add the hyperlink
    text: '`Hyperlink` defines a link associated with a cell, shape, or picture, enabling
      navigation when clicked.'
  - name: set a screen tip and save the workbook
    text: Provide a helpful tooltip and write the workbook to disk.
  type: HowTo
- questions:
  - answer: Aspose.Cells for Java.
    question: What library is required?
  - answer: Yes – the API works with both .xls and .xlsx.
    question: Can I use .xlsx files?
  - answer: A trial works for evaluation; a permanent license is required for production.
    question: Do I need a license?
  - answer: About 20 lines to add a clickable image.
    question: How many lines of code?
  - answer: Workbook objects are not thread‑safe; create separate instances per thread.
    question: Is it thread‑safe?
  type: FAQPage
tags:
- create clickable image
- Aspose.Cells
- Java Excel automation
title: Tworzenie klikalnego obrazu w Excelu przy użyciu Aspose.Cells for Java
url: /pl/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz klikalny obraz w Excelu przy użyciu Aspose.Cells dla Javy

## Wprowadzenie

Jeśli chcesz **utworzyć klikalny obraz w Excelu** skoroszyty, które pozwalają użytkownikom przejść do stron internetowych, dokumentów lub innych zasobów jednym kliknięciem, jesteś we właściwym miejscu. W tym samouczku pokażemy, jak Aspose.Cells dla Javy umożliwia **dodawanie obiektów obrazu z hiperłączem w Excelu**, konfigurowanie podpowiedzi ekranowych i utrzymanie arkuszy kalkulacyjnych zarówno pięknych, jak i funkcjonalnych.

### Co się nauczysz
- Inicjalizacja skoroszytu Aspose.Cells w Javie.  
- Wstawianie obrazu i przekształcanie go w klikalny hiperłącze.  
- Kluczowe metody, takie jak `addHyperlink`, `setPlacement` i `setScreenTip`.  
- Najlepsze praktyki dotyczące wydajności i licencjonowania.

## Szybkie odpowiedzi
- **Jaka biblioteka jest wymagana?** Aspose.Cells for Java.  
- **Czy mogę używać plików .xlsx?** Tak – API działa zarówno z .xls, jak i .xlsx.  
- **Czy potrzebna jest licencja?** Wersja próbna działa w celach oceny; stała licencja jest wymagana w produkcji.  
- **Ile linii kodu?** Około 20 linii, aby dodać klikalny obraz.  
- **Czy jest bezpieczna wątkowo?** Obiekty Workbook nie są bezpieczne wątkowo; twórz oddzielne instancje dla każdego wątku.  
- **Czy mogę dodać podpowiedź ekranową w Excelu?** Tak – użyj `Hyperlink.setScreenTip()`, aby wyświetlić pomocny tekst po najechaniu.

## Jak utworzyć klikalny obraz w Excelu przy użyciu Aspose.Cells dla Javy

Tworzysz klikalny obraz w Excelu, tworząc skoroszyt, poprzez załadowanie lub utworzenie `Workbook`, wstawienie obiektu `Picture`, dołączenie `Hyperlink` do tego obrazu, opcjonalne ustawienie podpowiedzi ekranowej i ostateczne zapisanie pliku. API obsługuje cały niskopoziomowy XML Excela, więc piszesz tylko kilka prostych linii kodu w Javie.

### Wymagania wstępne
Zanim rozpoczniesz, upewnij się, że masz:

- **Aspose.Cells for Java** (v25.3 lub nowszy).  
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
Aspose.Cells jest komercyjny, ale możesz rozpocząć od darmowej wersji próbnej lub poprosić o tymczasową licencję:

- Darmowa wersja próbna: Pobierz z [Aspose Downloads](https://releases.aspose.com/cells/java/).  
- Licencja tymczasowa: Zamów poprzez [Temporary License page](https://purchase.aspose.com/temporary-license/).  
- Zakup: Aby korzystać długoterminowo, odwiedź [Aspose Purchase](https://purchase.aspose.com/buy).

### Podstawowa inicjalizacja
Klasa `Workbook` reprezentuje cały plik Excel w pamięci. Tworzysz jej instancję, a następnie uzyskujesz odwołanie do pierwszego arkusza. `Worksheet` reprezentuje pojedynczy arkusz w skoroszycie.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

## Implementacja krok po kroku

### Krok 1: przygotuj swój skoroszyt
Zaczynamy od utworzenia nowego skoroszytu i wybrania pierwszego arkusza.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

### Krok 2: wstaw etykietę i dostosuj rozmiar komórki
Dodaj opisową etykietę i zapewnij komórce wystarczająco miejsca na obraz.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```  

### Krok 3: dodaj obraz
`Picture` reprezentuje obiekt obrazu umieszczony w arkuszu.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```  
*Wskazówka*: Zastąp `"path/to/aspose-logo.jpg"` rzeczywistą ścieżką do pliku obrazu.

### Krok 4: skonfiguruj położenie i dodaj hiperłącze
`Hyperlink` definiuje link powiązany z komórką, kształtem lub obrazem, umożliwiając nawigację po kliknięciu.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```  

### Krok 5: ustaw podpowiedź ekranową i zapisz skoroszyt
Podaj przydatną podpowiedź i zapisz skoroszyt na dysku.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```  

## Dlaczego dodawać obraz z hiperłączem w Excelu?

Osadzenie klikalnego obrazu pozwala przekształcić elementy brandingowe, ikony lub diagramy w bezpośrednie punkty nawigacyjne, zmniejszając liczbę kliknięć potrzebnych do dotarcia do powiązanej treści. Takie podejście zwiększa wydajność użytkowników w dashboardach marketingowych, podręcznikach technicznych i arkuszach edukacyjnych.

## Jak dodać podpowiedź ekranową w Excelu

Dodajesz podpowiedź ekranową, wywołując `hyperlink.setScreenTip("Your tip here")` na obiekcie `Hyperlink` dołączonym do obrazu. Podpowiedź pojawia się, gdy kursor najedzie na obraz, zapewniając użytkownikom kontekstową pomoc bez zagracania arkusza.

## Porady dotyczące rozwiązywania problemów
- **Błędy ścieżki obrazu** – sprawdź ponownie lokalizację pliku i upewnij się, że aplikacja ma uprawnienia do odczytu.  
- **Licencja nie zastosowana** – jeśli wersja próbna wygaśnie, hiperłącza mogą przestać działać; zastosuj ważną licencję za pomocą `License.setLicense`.  
- **Hiperłącze nieklikalne** – zweryfikuj, czy `PlacementType` obrazu jest ustawiony na `FREE_FLOATING`.

## Praktyczne zastosowania
Embedding clickable images is useful in many scenarios:

1. **Raporty marketingowe** – połącz logotypy marek z stronami produktów.  
2. **Dokumentacja techniczna** – dołącz diagramy otwierające szczegółowe schematy.  
3. **Arkusze edukacyjne** – przekształć ikony w skróty do dodatkowych filmów.  
4. **Dashboardy projektowe** – spraw, aby ikony statusu otwierały powiązane śledzenie zadań.

## Uwagi dotyczące wydajności
- Utrzymuj rozmiary plików obrazów w rozsądnych granicach; duże obrazy zwiększają zużycie pamięci skoroszytu.  
- Uwalniaj nieużywane obiekty (`workbook.dispose()`), przetwarzając wiele plików w pętli.  
- Uaktualnij do najnowszej wersji Aspose.Cells, aby uzyskać poprawę wydajności i naprawy błędów.

## Podsumowanie
Teraz wiesz, jak dodać hiperłącze do obrazów w Excelu przy użyciu Aspose.Cells dla Javy, co umożliwia **utworzyć klikalny obraz w Excelu** skoroszyty, które są bogatsze i bardziej interaktywne. Eksperymentuj z różnymi adresami URL, podpowiedziami ekranowymi i położeniem obrazów, aby dopasować je do potrzeb raportowania. Następnie możesz zbadać dodawanie hiperłączy do kształtów lub automatyzację masowego wstawiania obrazów w wielu arkuszach.

## Najczęściej zadawane pytania

**Q:** Jaki jest maksymalny rozmiar obrazu obsługiwany przez Aspose.Cells dla Javy?  
**A:** Nie ma ścisłego limitu, ale bardzo duże obrazy mogą wpływać na wydajność i zwiększać rozmiar pliku.

**Q:** Czy mogę używać tej funkcji z plikami .xlsx?  
**A:** Tak, API działa zarówno z formatami `.xls`, jak i `.xlsx`.

**Q:** Jak powinienem obsługiwać wyjątki przy dodawaniu hiperłączy?  
**A:** Otocz kod blokiem try‑catch i zaloguj szczegóły `Exception`, aby zdiagnozować problemy ze ścieżką lub licencją.

**Q:** Czy można usunąć hiperłącze z obrazu po jego dodaniu?  
**A:** Tak – pobierz obiekt `Picture` i wywołaj `pic.getHyperlink().remove()` lub usuń obraz z kolekcji.

**Q:** Dlaczego moje hiperłącze może nie działać zgodnie z oczekiwaniami?  
**A:** Typowe przyczyny to nieprawidłowy ciąg URL, brak prefiksu `http://`/`https://` lub nielicencjonowana wersja próbna, która wyłącza niektóre funkcje.

## Dodatkowe zasoby
- **Dokumentacja:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Pobranie:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Zakup i wersja próbna:** Odwiedź [Aspose Purchase](https://purchase.aspose.com/buy) lub [Temporary License Page](https://purchase.aspose.com/temporary-license/) w celu uzyskania opcji licencjonowania.  
- **Forum wsparcia:** W razie potrzeby sprawdź [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**Ostatnia aktualizacja:** 2026-09-02  
**Testowano z:** Aspose.Cells for Java 25.3  
**Autor:** Aspose

## Powiązane samouczki

- [Jak tworzyć hiperłącza w Excelu przy użyciu Aspose.Cells dla Javy – przewodnik krok po kroku](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [Jak stylizować komórki Excela i dodawać hiperłącza przy użyciu Aspose.Cells dla Javy](/cells/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Dodaj obraz do komentarza w Excelu przy użyciu Aspose.Cells dla Javy: kompletny przewodnik](/cells/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}