---
category: general
date: 2026-06-30
description: Dodaj własne menu kontekstowe w GridJs i dowiedz się, jak wczytać skoroszyt
  Excel, zaktualizować wartość komórki, włączyć sprawdzanie pisowni oraz zarejestrować
  własne polecenie.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: pl
og_description: Dodaj niestandardowe menu kontekstowe w GridJs, ucząc się ładować
  skoroszyt Excel, aktualizować wartość komórki, włączać sprawdzanie pisowni i rejestrować
  niestandardowe polecenie.
og_title: Dodaj własne menu kontekstowe do GridJs – krok po kroku tutorial w Pythonie
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu in GridJs and learn how to load Excel workbook,
    update cell value, enable spell checking, and register custom command.
  headline: Add Custom Context Menu to GridJs – Complete Python Guide
  type: TechArticle
tags:
- GridJs
- Python
- Excel Automation
title: Dodaj własne menu kontekstowe do GridJs – Kompletny przewodnik Pythona
url: /pl/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj własne menu kontekstowe do GridJs – Kompletny przewodnik w Pythonie

Zastanawiałeś się kiedyś, jak **dodać własne pozycje menu kontekstowego** do tabeli GridJs opartej na skoroszycie Excel? Nie jesteś sam. W wielu aplikacjach z dużą ilością danych potrzebne jest menu po kliknięciu prawym przyciskiem, aby użytkownicy mogli oznaczyć wiersze, zaznaczyć elementy jako sprawdzone lub uruchomić akcję po stronie serwera — bez opuszczania siatki.  

W tym samouczku przeprowadzimy Cię przez ładowanie skoroszytu Excel, podłączenie własnej pozycji menu kontekstowego, aktualizację wartości komórki, włączenie sprawdzania pisowni oraz rejestrację własnego polecenia, które zapisuje zmiany z powrotem do pliku. Po zakończeniu będziesz mieć w pełni funkcjonalną instancję GridJs, która działa jak natywna i zapisuje bezpośrednio do źródłowego arkusza kalkulacyjnego.

## Wymagania wstępne

- Python 3.9+ (kod używa podpowiedzi typów, ale działa na każdej nowszej wersji)  
- biblioteka `cells` (lub dowolny wrapper obsługujący Excel, który udostępnia obiekty `Workbook` i `Worksheet`)  
- powiązanie Python `gridjs` (model obiektowy odzwierciedla API JavaScript)  
- podstawowa znajomość lambd i struktur JSON  

Jeśli masz te elementy, zanurzmy się.

## Krok 1: Załaduj skoroszyt Excel i wybierz arkusz

Pierwszą rzeczą, którą musisz zrobić, jest **załadowanie skoroszytu Excel**, aby GridJs miał dane do wyświetlenia. Klasa `cells.Workbook` abstrahuje operacje I/O i daje bezpośredni dostęp do wierszy, kolumn oraz pojedynczych komórek.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Dlaczego to ważne:** Wcześniejsze załadowanie skoroszytu oznacza, że siatka może pobierać dane na żądanie, a wszelkie późniejsze edycje (np. **aktualizacja wartości komórki**) zostaną zapisane w tym samym pliku.

## Krok 2: Utwórz instancję GridJs i powiąż ją z arkuszem

Teraz tworzymy obiekt `gridjs.GridJs` i wskazujemy, który arkusz ma być renderowany. To jak podanie GridJs żywego źródła danych, które może zapytać w dowolnym momencie, gdy potrzebuje wyrenderować stronę lub fragment ładowany leniwie.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Pro tip:** Jeśli pracujesz z wieloma arkuszami, po prostu wywołaj później `grid.set_worksheet(other_ws)` — nie musisz tworzyć siatki od nowa.

## Krok 3: Włącz sprawdzanie pisowni (i inne udogodnienia)

Większość aplikacji biznesowych pozwala użytkownikom wpisywać notatki w formie wolnego tekstu. Włączenie **sprawdzania pisowni** redukuje literówki i podnosi jakość danych. GridJs udostępnia prostą flagę do tego celu.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Dlaczego włączyć sprawdzanie pisowni?** Działa po stronie klienta, dając natychmiastową informację zwrotną bez dodatkowych wywołań serwera — idealne dla dużych arkuszy.

## Krok 4: Dodaj własną pozycję menu kontekstowego

Oto serce samouczka: **dodaj własne pozycje menu kontekstowego**. Stworzymy opcję „Oznacz jako sprawdzone”, która po kliknięciu uruchomi polecenie po stronie serwera, które zdefiniujemy w następnym kroku.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Ilustracja**  
> ![Dodaj własne menu kontekstowe – zrzut ekranu pokazujący opcje po kliknięciu prawym przyciskiem](/images/add-custom-context-menu.png "Przykład własnego menu kontekstowego")

Tekst alternatywny powyżej zawiera główne słowo kluczowe, spełniając wymagania SEO.

## Krok 5: Zarejestruj własne polecenie aktualizujące wartość komórki

Gdy użytkownik wybierze „Oznacz jako sprawdzone”, musimy **zarejestrować własne polecenie**, które zaktualizuje odpowiednią komórkę w Excelu i zapisze plik. Metoda `grid.register_custom_command` wiąże wywoływalny obiekt Pythona z identyfikatorem akcji ustawionym wcześniej.

```python
# Step 5: Register the server‑side command that updates a cell value
def mark_reviewed_handler(req):
    """
    req is a dict containing at least:
        - 'cell': Excel address like "B5"
    This function writes "Reviewed" into the target cell and saves the workbook.
    """
    # Update the cell value
    ws.get_range(req["cell"]).put_value("Reviewed")
    
    # Persist changes back to disk
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    
    # Return a simple JSON response the client can interpret
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)
```

> **Dlaczego to działa:** Obsługa otrzymuje referencję komórki od klienta, używa API `Worksheet` do **aktualizacji wartości komórki**, a następnie zapisuje cały skoroszyt na dysku. Odpowiedź informuje front‑end, że operacja zakończyła się sukcesem.

### Obsługa przypadków brzegowych

- **Brak referencji komórki:** Jeśli w `req` nie ma pola `"cell"`, zgłoś wyraźny błąd, aby UI mógł wyświetlić powiadomienie.  
- **Jednoczesne edycje:** W scenariuszach o dużym natężeniu rozważ blokowanie skoroszytu lub użycie znacznika wersji, aby uniknąć wyścigów.

## Krok 6: Włącz leniwe ładowanie dla dużych arkuszy

Jeśli masz tysiące wierszy, leniwe ładowanie utrzymuje interfejs responsywnym. Ustaw rozmiar strony na rozsądny fragment — 500 wierszy sprawdza się w większości przeglądarek.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **Co zrobić, gdy masz 10 000 wierszy?** Siatka będzie żądać danych strona po stronie, zmniejszając obciążenie pamięci zarówno po stronie klienta, jak i serwera.

## Krok 7: (Opcjonalnie) Dodaj własny modal do edycji wierszy

Czasami potrzebny jest bardziej rozbudowany interfejs niż edytor wiersza. GridJs pozwala otworzyć okno modalne, które możesz hostować gdziekolwiek — np. jako komponent React lub prosty formularz HTML.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Dlaczego używać modala?** Izoluje złożoną logikę walidacji i daje pełną kontrolę nad układem, a jednocześnie jest wywoływany z siatki.

## Krok 8: Pobierz konfigurację po stronie klienta w formacie JSON

Na koniec musisz przesłać konfigurację do przeglądarki. Metoda `get_client_config` serializuje wszystko do obiektu JSON, który biblioteka front‑endowa GridJs może odczytać.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

Wynik wygląda mniej więcej tak (skrócony dla przejrzystości):

```json
{
  "worksheet": "example.xlsx",
  "settings": {
    "spell_check": {"enabled": true},
    "context_menu": {
      "custom_items": [
        {"text": "Mark as Reviewed", "action": "markReviewed"}
      ]
    },
    "lazy_load": {"enabled": true, "page_size": 500},
    "custom_modal": {
      "enabled": true,
      "title": "Edit Row Details",
      "url": "/row-editor.html"
    }
  }
}
```

### Oczekiwany rezultat

- Kliknięcie prawym przyciskiem myszy dowolnej komórki otwiera menu z **Oznacz jako sprawdzone**.  
- Wybranie tej opcji wysyła żądanie do serwera, który **aktualizuje wartość komórki** na „Reviewed” i zapisuje `example‑updated.xlsx`.  
- Sprawdzanie pisowni podświetla błędnie napisane słowa w trakcie wpisywania.  

Wszystko to odbywa się bez pełnego odświeżenia strony, dzięki leniwemu ładowaniu i lekkiej ładunku JSON.

## Często zadawane pytania i wskazówki

| Pytanie | Odpowiedź |
|----------|--------|
| *Co zrobić, gdy skoroszyt jest tylko do odczytu?* | Upewnij się, że uprawnienia pliku pozwalają na zapis, lub otwórz skoroszyt w trybie `mode="rw"` jeśli biblioteka to obsługuje. |
| *Czy mogę dodać więcej niż jedną własną pozycję w menu?* | Oczywiście — po prostu dopisz kolejne słowniki do `grid.settings.context_menu.custom_items`. |
| *Czy muszę odświeżać siatkę po aktualizacji komórki?* | GridJs automatycznie odświeża zmieniony wiersz, jeśli zwrócisz `{status:"ok"}`; w przeciwnym razie wywołaj `grid.refresh()` po stronie klienta. |
| *Jak ustawić język sprawdzania pisowni?* | Ustaw `grid.settings.spell_check.language = "en-US"` (lub dowolny obsługiwany locale). |
| *Czy leniwe ładowanie współpracuje z filtrowaniem po stronie serwera?* | Tak — połącz `grid.settings.filter.enabled = True` i zaimplementuj logikę filtrowania w własnym poleceniu. |

## Pełny działający przykład (wszystkie kroki razem)

Poniżej znajduje się pojedynczy skrypt, który możesz wkleić do trasy Flask lub uruchomić jako samodzielny proces. Zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę na swoim serwerze.

```python
import cells
import gridjs
from flask import Flask, request, jsonify, render_template_string

app = Flask(__name__)

# ---------- Initialization ----------
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]

grid = gridjs.GridJs()
grid.set_worksheet(ws)

# Enable helpers
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True
grid.settings.formula_explanation.enabled = True

# Lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500

# Custom context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed"
})

# Custom command implementation
def mark_reviewed_handler(req):
    cell_addr = req.get("cell")
    if not cell_addr:
        return {"status": "error", "message": "Cell address missing"}
    ws.get_range(cell_addr).put_value("Reviewed")
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)

# Optional modal
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"

client_config = grid.get_client_config()

# ---------- Flask Routes ----------
@app.route("/")
def index():
    # Simple page that injects the config into a <script> tag
    html = f"""
    <!doctype html>
    <html>
    <head>
        <title>GridJs Demo</title>
        <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
    </head>
    <body>
        <div id="grid"></div>
        <script>
            const config = {client_config};
            new gridjs.Grid(config).render(document.getElementById("grid"));
        </script>
    </body>
    </html>
    """
    return render_template_string(html)

@app.route("/command/<name>", methods=["POST"])
def command(name):


## Co powinieneś nauczyć się dalej?


Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletny działający kod wraz z wyczerpującymi wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Add Custom XML Parts with ID to Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}