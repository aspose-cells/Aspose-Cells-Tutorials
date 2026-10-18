---
category: general
date: 2026-06-30
description: Dodaj własne menu kontekstowe do siatki Excel w Pythonie i zapisz wartość
  w komórce Excela przy zapisywaniu zaktualizowanego pliku. Naucz się tworzyć menu
  po kliknięciu prawym przyciskiem i aktualizować wartość komórki w stylu Pythona.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: pl
og_description: Dodaj własne menu kontekstowe w Pythonie, aby zapisać wartość w komórce
  Excela i zapisać zaktualizowany plik Excel. Ten przewodnik krok po kroku pokazuje,
  jak stworzyć menu po kliknięciu prawym przyciskiem myszy przy użyciu GridJs.
og_title: Dodaj własne menu kontekstowe w Pythonie – samouczek krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: Dodaj własne menu kontekstowe w Pythonie – kompletny przewodnik
url: /pl/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj własne menu kontekstowe w Pythonie – Kompletny przewodnik

Zastanawiałeś się kiedyś, jak **add custom context menu** items to a spreadsheet grid you’re serving from Python? Maybe you need a quick “Mark as Reviewed” button that pops up when a user right‑clicks a cell, writes a value to the Excel cell, and then saves the updated workbook—all without leaving the web UI.  

W tym samouczku zbudujemy dokładnie to: **custom right‑click menu** powered by GridJs, a server‑side handler that **write(s) value to excel cell**, and a final step that **save(s) updated excel file** on disk. By the end you’ll have a reusable pattern you can drop into any Flask, FastAPI, or Django project.

> **Dlaczego to ważne?**  
> Dodanie własnego menu kontekstowego usprawnia przepływy pracy przeglądu danych, zmniejsza potrzebę ręcznego kopiowania‑wklejania i zapewnia użytkownikom doświadczenie zbliżone do natywnego, bezpośrednio w siatce. Dodatkowo zobaczysz, jak **update cell value python**‑style, co jest kluczową umiejętnością w każdej automatyzacji Excela.

## Wymagania wstępne

- Python 3.9+ (kod działa również na 3.10)  
- `openpyxl` do obsługi plików Excel  
- `gridjs` wrapper Pythona (lub biblioteka JS, jeśli wolisz front‑end)  
- Podstawowy framework webowy (przykład w Flask)  
- Plik skoroszytu o nazwie `sample.xlsx` w folderze projektu  

Jeśli brakuje Ci któregoś z nich, uruchom:

```bash
pip install openpyxl flask gridjs
```

Zanurzmy się.

---

## Krok 1 – Dodaj własne menu kontekstowe: Zainicjalizuj GridJs i powiąż arkusz

Pierwszą rzeczą, którą musisz zrobić, jest uruchomienie instancji `GridJs` i skierowanie jej na arkusz, z którym zamierzasz pracować. To tutaj fraza **add custom context menu** pojawia się po raz pierwszy w naszym kodzie i przygotowuje scenę dla wszystkiego, co nastąpi.

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**Co się dzieje?**  
`grid.set_worksheet(ws)` informuje GridJs, aby używał danych z `ws` jako źródła danych. Od tego momentu wszelkie modyfikacje menu kontekstowego, które dodamy, będą automatycznie skierowane do tego samego arkusza, utrzymując synchronizację UI i pliku.

> **Pro tip:** Trzymaj swój skoroszyt otwarty w trybie odczytu/zapisu tylko raz. Otwieranie go wielokrotnie wewnątrz obsługi żądania może powodować problemy z blokowaniem plików w systemie Windows.

## Krok 2 – Zapisz wartość do komórki Excel: Zdefiniuj akcję dla elementu menu

Teraz, gdy siatka jest gotowa, musimy **write value to excel cell**, gdy użytkownik wybierze naszą własną komendę. Dodamy pozycję menu o nazwie „Mark as Reviewed” i nadamy jej identyfikator `markReviewed`. Identyfikator jest tym, co JavaScript po stronie klienta wyśle z powrotem do serwera.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Dlaczego używać własnego identyfikatora?**  
Identyfikator oddziela tekst UI od logiki serwera, pozwalając zmienić etykietę bez modyfikacji kodu backendu. Dzięki temu operacja **create right‑click menu** staje się wyraźna i wielokrotnego użytku.

## Krok 3 – Utwórz menu prawoklikowe: Zarejestruj obsługę po stronie serwera

Z elementem menu na miejscu, musimy powiedzieć GridJs, co zrobić, gdy użytkownik w niego kliknie. To tutaj wprowadzamy funkcjonalność **create right‑click menu**, która faktycznie wysyła żądanie z powrotem do Pythona.

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

Kilka rzeczy do zauważenia:

1. **`ws[cell_address] = "Reviewed"`** jest najprostszym sposobem na **update cell value python**. W tle `openpyxl` tłumaczy adres w stylu A1 na indeksy wiersza/kolumny.
2. Obsługa zwraca mały ładunek JSON. GridJs oczekuje wskaźnika statusu; możesz go rozbudować o komunikaty o błędach, jeśli zajdzie taka potrzeba.

Teraz wiążemy identyfikator z obsługą:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**Co jeśli komórka jest pusta lub chroniona?**  
- Puste komórki są w porządku — `openpyxl` utworzy je w locie.  
- W przypadku chronionych arkuszy, najpierw musisz je odchronić (`ws.protection.sheet = False`) lub przechwycić `PermissionError`.

## Krok 4 – Aktualizuj wartość komórki w Pythonie: Zapisz zmianę, zapisując skoroszyt

Zapisanie wartości to dopiero połowa historii; musisz **save updated excel file**, aby zmiana przetrwała poza bieżącą sesją. To tutaj kończymy pełny cykl od UI do dysku.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Dlaczego osobny folder?**  
Zapisywanie w katalogu `output/` pozostawia oryginalny szablon nietknięty, co jest przydatne przy ścieżkach audytu. Dostosuj ścieżkę do swojego środowiska wdrożeniowego.

> **Uwaga:** Jeśli obsługujesz wielu jednoczesnych użytkowników, rozważ użycie blokady wątkowo‑bezpiecznej (`threading.Lock`) wokół `wb.save()`, aby uniknąć warunków wyścigu.

## Krok 5 – Wygeneruj JSON konfiguracji klienta i połącz wszystko razem

Na koniec musimy wygenerować JSON, który będzie konsumował front‑end GridJs. Ten JSON zawiera dane arkusza **i** definicję własnego menu.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

Gdy osadzisz `config_json` w swojej stronie HTML, GridJs wyrenderuje siatkę z pozycją „Mark as Reviewed” dostępną po kliknięciu prawym przyciskiem myszy w każdej komórce.

### Pełny przykład Flask

Poniżej znajduje się minimalna aplikacja Flask, która łączy wszystkie elementy. Uruchom ją, otwórz `http://localhost:5000` i kliknij prawym przyciskiem myszy dowolną komórkę, aby zobaczyć własne menu w działaniu.

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**Oczekiwany rezultat:**  
- Kliknij prawym przyciskiem myszy dowolną komórkę → pojawi się „Mark as Reviewed”.  
- Kliknij ją → zawartość komórki zmieni się na „Reviewed”.  
- Skoroszyt `output/sample-updated.xlsx` teraz zawiera nową wartość.

## Częste pytania i przypadki brzegowe

| Question | Answer |
|----------|--------|
| *Co jeśli potrzebuję wielu własnych akcji?* | Po prostu dodaj więcej obiektów do `grid.settings.context_menu.custom_items` i zarejestruj każdy z własnym identyfikatorem. |
| *Czy mogę przekazać dodatkowe dane (np. ID wiersza) do obsługi?* | Tak. Dołącz dodatkowe klucze w ładunku JSON po stronie klienta, a następnie odczytaj je z `request` w `on_custom_command`. |
| *Czy to podejście jest kompatybilne z frameworkami async?* | Zdecydowanie — wystarczy, że `on_custom_command` będzie funkcją async i użyjesz `await wb.save(...)`, jeśli przejdziesz na `aiofiles` lub podobny. |
| *Jak stylizować ikonę menu?* | Podaj dowolną nazwę z Material‑Icons (`"icon": "edit"`). Front‑end automatycznie ładuje czcionkę ikon. |
| *Co z dużymi skoroszytami?* | Ładuj tylko potrzebny arkusz i rozważ strumieniowanie wierszy przy pomocy `openpyxl.iter_rows()`, aby ograniczyć zużycie pamięci. |

## Co powinieneś nauczyć się dalej?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Preserve Single Quote Prefix of Cell Value or Range in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}