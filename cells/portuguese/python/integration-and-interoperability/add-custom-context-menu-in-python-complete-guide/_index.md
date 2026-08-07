---
category: general
date: 2026-06-30
description: Adicione um menu de contexto personalizado a uma grade Excel em Python
  e escreva um valor na célula do Excel ao salvar o arquivo atualizado. Aprenda a
  criar um menu de clique‑direito e atualizar o valor da célula ao estilo Python.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: pt
og_description: Adicione um menu de contexto personalizado em Python para escrever
  um valor em uma célula do Excel e salvar o arquivo Excel atualizado. Este guia orienta
  você na criação de um menu de clique direito com o GridJs.
og_title: Adicionar Menu de Contexto Personalizado em Python – Tutorial Passo a Passo
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
title: Adicionar menu de contexto personalizado em Python – Guia completo
url: /pt/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Menu de Contexto Personalizado em Python – Guia Completo

Já se perguntou como **add custom context menu** itens em uma grade de planilha que você está servindo a partir do Python? Talvez você precise de um botão rápido “Mark as Reviewed” que aparece quando um usuário clica com o botão direito em uma célula, grava um valor na célula do Excel e, em seguida, salva a pasta de trabalho atualizada — tudo sem sair da interface web.  

Neste tutorial vamos construir exatamente isso: um **custom right‑click menu** alimentado pelo GridJs, um manipulador do lado do servidor que **write(s) value to excel cell**, e um passo final que **save(s) updated excel file** no disco. Ao final, você terá um padrão reutilizável que pode ser inserido em qualquer projeto Flask, FastAPI ou Django.

> **Por que se importar?**  
> Adicionar um custom context menu simplifica fluxos de trabalho de revisão de dados, reduz a cópia‑colagem manual e oferece aos usuários finais uma experiência de sensação nativa diretamente dentro da grade. Além disso, você verá como **update cell value python**‑style, que é uma habilidade essencial para qualquer tarefa de automação do Excel.

## Pré-requisitos

- Python 3.9+ (o código funciona também em 3.10)  
- `openpyxl` para manipulação de arquivos Excel  
- `gridjs` wrapper Python (ou a biblioteca JS se preferir o front‑end)  
- Um framework web básico (exemplo com Flask mostrado)  
- Um arquivo de workbook chamado `sample.xlsx` na pasta do seu projeto  

Se estiver faltando algum desses, execute:

```bash
pip install openpyxl flask gridjs
```

Agora vamos mergulhar.

---

## Etapa 1 – Add Custom Context Menu: Initialize GridJs and Bind Worksheet

A primeira coisa que você precisa fazer é iniciar uma instância `GridJs` e apontá‑la para a planilha com a qual você pretende trabalhar. É aqui que a frase **add custom context menu** aparece pela primeira vez em nosso código, e ela prepara o cenário para todo o resto.

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

**O que está acontecendo?**  
`grid.set_worksheet(ws)` informa ao GridJs para usar os dados de `ws` como sua fonte de dados. A partir de agora, quaisquer modificações de context‑menu que adicionarmos irão automaticamente direcionar a mesma planilha, mantendo a UI e o arquivo sincronizados.

> **Pro tip:** Mantenha sua workbook aberta em modo leitura/escrita apenas uma vez. Abrí‑la repetidamente dentro de um manipulador de requisição pode causar problemas de bloqueio de arquivos no Windows.

## Etapa 2 – Write Value to Excel Cell: Define the Action for the Menu Item

Agora que a grade está pronta, precisamos **write value to excel cell** quando o usuário seleciona nosso comando personalizado. Vamos adicionar uma entrada de menu chamada “Mark as Reviewed” e atribuir a ela um identificador `markReviewed`. O identificador é o que o JavaScript do lado do cliente enviará de volta ao servidor.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Por que usar um identificador personalizado?**  
O identificador desacopla o texto da UI da lógica do servidor, permitindo que você altere o rótulo sem tocar no código backend. Ele também torna a operação **create right‑click menu** explícita e reutilizável.

## Etapa 3 – Create Right‑Click Menu: Register the Server‑Side Handler

Com o item de menu em vigor, precisamos dizer ao GridJs o que fazer quando o usuário clicar nele. É aqui que implementamos a funcionalidade **create right‑click menu** que realmente dispara uma requisição de volta ao Python.

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

Algumas coisas a observar:

1. **`ws[cell_address] = "Reviewed"`** é a maneira mais direta de **update cell value python**. Nos bastidores, `openpyxl` traduz o endereço no estilo A1 para índices de linha/coluna.
2. O manipulador retorna um pequeno payload JSON. O GridJs espera um indicador de status; você pode expandir isso para incluir mensagens de erro, se necessário.

Agora vinculamos o identificador ao manipulador:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**E se a célula estiver vazia ou protegida?**  
- Células vazias não são problema — `openpyxl` as criará automaticamente.  
- Para planilhas protegidas, será necessário desproteger primeiro (`ws.protection.sheet = False`) ou capturar um `PermissionError`.

## Etapa 4 – Update Cell Value Python: Persist the Change by Saving the Workbook

Gravar um valor é apenas metade da história; você deve **save updated excel file** para que a alteração persista além da sessão atual. É aqui que concluímos o ciclo de ida e volta da UI para o disco.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Por que uma pasta separada?**  
Salvar em um diretório `output/` mantém o modelo original intacto, o que é útil para trilhas de auditoria. Ajuste o caminho para corresponder ao seu ambiente de implantação.

> **Cuidado:** Se você estiver atendendo a muitos usuários simultâneos, considere usar um lock thread‑safe (`threading.Lock`) ao redor de `wb.save()` para evitar condições de corrida.

## Etapa 5 – Generate Client Configuration JSON and Wire It All Together

Finalmente, precisamos gerar o JSON que a instância GridJs do front‑end consumirá. Esse JSON contém os dados da planilha **and** a definição do menu personalizado.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

Quando você incorporar `config_json` em sua página HTML, o GridJs renderizará a grade com a entrada “Mark as Reviewed” clicável com o botão direito em cada célula.

### Exemplo Completo em Flask

Abaixo está um aplicativo Flask minimalista que reúne todas as peças. Execute‑o, abra `http://localhost:5000` e clique com o botão direito em qualquer célula para ver o menu personalizado em ação.

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

**Resultado esperado:**  
- Clique com o botão direito em qualquer célula → “Mark as Reviewed” aparece.  
- Clique nele → o conteúdo da célula muda para “Reviewed”.  
- A workbook `output/sample-updated.xlsx` agora contém o novo valor.

## Perguntas Frequentes & Casos Limite

| Pergunta | Resposta |
|----------|----------|
| *E se eu precisar de múltiplas ações personalizadas?* | Basta adicionar mais objetos a `grid.settings.context_menu.custom_items` e registrar cada um com seu próprio identificador. |
| *Posso passar dados extras (ex., row ID) para o manipulador?* | Sim. Inclua chaves extras no payload JSON no lado do cliente, e então leia‑as de `request` em `on_custom_command`. |
| *Essa abordagem é compatível com frameworks assíncronos?* | Absolutamente — basta tornar `on_custom_command` uma função async e usar `await wb.save(...)` se você mudar para `aiofiles` ou similar. |
| *Como estilizar o ícone do menu?* | Forneça qualquer nome de Material‑Icons (`"icon": "edit"`). O front‑end carrega automaticamente a fonte do ícone. |
| *E quanto a workbooks grandes?* | Carregue apenas a planilha necessária e considere fazer streaming das linhas com `openpyxl.iter_rows()` para manter o uso de memória baixo |

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Preservar Prefixo de Aspas Simples do Valor da Célula ou Intervalo no Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preservar Prefixo de Aspas Simples do Valor da Célula ou Intervalo no Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preservar Prefixo de Aspas Simples do Valor da Célula ou Intervalo no Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}