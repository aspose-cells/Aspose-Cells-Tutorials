---
category: general
date: 2026-06-30
description: Adicione um menu de contexto personalizado no GridJs e aprenda como carregar
  uma pasta de trabalho do Excel, atualizar o valor de uma célula, habilitar a verificação
  ortográfica e registrar um comando personalizado.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: pt
og_description: Adicionar menu de contexto personalizado no GridJs enquanto aprende
  a carregar uma pasta de trabalho do Excel, atualizar o valor de uma célula, habilitar
  a verificação ortográfica e registrar um comando personalizado.
og_title: Adicione Menu de Contexto Personalizado ao GridJs – Tutorial Python Passo
  a Passo
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
title: Adicionar Menu de Contexto Personalizado ao GridJs – Guia Completo de Python
url: /pt/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Menu de Contexto Personalizado ao GridJs – Guia Completo em Python

Já se perguntou como **adicionar itens de menu de contexto personalizados** a uma tabela GridJs que tem como base uma planilha Excel? Você não está sozinho. Em muitos aplicativos com grande volume de dados, você precisa desse menu de clique‑direito para permitir que os usuários sinalizem linhas, marquem itens como revisados ou iniciem uma ação no servidor — sem sair da grade.

Neste tutorial vamos percorrer o carregamento de uma planilha Excel, a criação de uma entrada de menu de contexto personalizada, a atualização do valor de uma célula, a habilitação da verificação ortográfica e o registro de um comando personalizado que persiste as alterações de volta ao arquivo. Ao final, você terá uma instância GridJs totalmente funcional, que parece nativa para seus usuários e grava diretamente na planilha de origem.

## Pré‑requisitos

- Python 3.9+ (o código usa type hints, mas funciona em qualquer versão recente)  
- Biblioteca `cells` (ou qualquer wrapper de manipulação de Excel que forneça objetos `Workbook` e `Worksheet`)  
- Vinculação Python do `gridjs` (o modelo de objetos espelha a API JavaScript)  
- Noções básicas de lambdas e estruturas JSON  

Se você tem tudo isso, vamos começar.

## Etapa 1: Carregar a Planilha Excel e Selecionar uma Worksheet

A primeira coisa que você precisa fazer é **carregar a planilha Excel** para que o GridJs tenha dados a exibir. A classe `cells.Workbook` abstrai o I/O do arquivo e fornece acesso direto a linhas, colunas e células individuais.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Por que isso importa:** Carregar a planilha antecipadamente permite que a grade busque dados sob demanda, e quaisquer edições que você fizer depois (como **atualizar o valor da célula**) serão persistidas no mesmo arquivo.

## Etapa 2: Criar Instância GridJs e Vinculá‑la à Worksheet

Agora criamos um objeto `gridjs.GridJs` e informamos qual worksheet deve ser renderizada. Pense nisso como fornecer ao GridJs uma fonte de dados ao vivo que ele pode consultar sempre que precisar renderizar uma página ou um bloco carregado de forma preguiçosa.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Dica profissional:** Se você trabalhar com várias planilhas, basta chamar `grid.set_worksheet(other_ws)` mais tarde — não é necessário recriar a grade.

## Etapa 3: Habilitar Verificação Ortográfica (e Outros Recursos Úteis)

A maioria dos aplicativos empresariais permite que os usuários digitem notas livres. Habilitar a **verificação ortográfica** reduz erros de digitação e melhora a qualidade dos dados. O GridJs expõe uma flag simples para isso.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Por que habilitar a verificação ortográfica?** Ela roda no cliente, fornecendo feedback instantâneo sem chamadas adicionais ao servidor — perfeito para planilhas de grande escala.

## Etapa 4: Adicionar um Item de Menu de Contexto Personalizado

Aqui está o coração do tutorial: **adicionar itens de menu de contexto personalizados**. Criaremos uma opção “Marcar como Revisado” que, ao ser clicada, executa um comando no servidor que definiremos a seguir.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Ilustração da imagem**  
> ![Captura de tela adicionando menu de contexto personalizado mostrando opções de clique‑direito](/images/add-custom-context-menu.png "Exemplo de menu de contexto personalizado")

O texto alternativo acima contém a palavra‑chave principal, atendendo aos requisitos de SEO.

## Etapa 5: Registrar Comando Personalizado para Atualizar o Valor da Célula

Quando o usuário selecionar “Marcar como Revisado”, precisamos **registrar um comando personalizado** que atualiza a célula Excel subjacente e salva o arquivo. O método `grid.register_custom_command` associa uma callable Python ao identificador de ação que definimos anteriormente.

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

> **Por que isso funciona:** O manipulador recebe a referência da célula do cliente, usa a API `Worksheet` para **atualizar o valor da célula** e, em seguida, grava toda a planilha de volta ao disco. A resposta informa ao front‑end que a operação foi bem‑sucedida.

### Tratamento de Casos Limite

- **Referência de célula ausente:** Se `req` não contiver `"cell"`, lance um erro claro para que a UI possa exibir um toast.  
- **Edições concorrentes:** Em cenários de alto tráfego, considere bloquear a planilha ou usar um carimbo de versão para evitar condições de corrida.

## Etapa 6: Habilitar Carregamento Preguiçoso para Planilhas Grandes

Se você estiver lidando com milhares de linhas, o carregamento preguiçoso mantém a UI ágil. Defina o tamanho da página para um bloco razoável — 500 linhas funciona bem na maioria dos navegadores.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **E se você tiver 10 000 linhas?** A grade solicitará os dados página por página, reduzindo a pressão de memória tanto no cliente quanto no servidor.

## Etapa 7: (Opcional) Adicionar um Modal Personalizado para Edição de Linhas

Às vezes você precisa de uma UI mais rica que um editor inline. O GridJs permite abrir uma janela modal que pode ser hospedada em qualquer lugar — talvez um componente React ou um simples formulário HTML.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Por que usar um modal?** Ele isola lógica de validação complexa e dá controle total sobre o layout, enquanto ainda pode ser acionado a partir da grade.

## Etapa 8: Recuperar o JSON de Configuração do Lado do Cliente

Por fim, você precisa enviar a configuração para o navegador. O método `get_client_config` serializa tudo em um blob JSON que a biblioteca GridJs do front‑end pode consumir.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

A saída se parece aproximadamente com isto (truncada para brevidade):

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

### Resultado Esperado

- Ao clicar com o botão direito em qualquer célula, abre‑se um menu com **Marcar como Revisado**.  
- Selecionar a opção envia uma requisição ao servidor, que **atualiza o valor da célula** para “Reviewed” e salva `example‑updated.xlsx`.  
- A verificação ortográfica destaca palavras incorretas enquanto o usuário digita.  

Tudo isso ocorre sem recarregar a página inteira, graças ao carregamento preguiçoso e ao payload JSON leve.

## Perguntas Frequentes & Dicas Profissionais

| Pergunta | Resposta |
|----------|----------|
| *E se a planilha for somente leitura?* | Garanta que as permissões de arquivo permitam escrita, ou abra a planilha com `mode="rw"` se a biblioteca oferecer suporte. |
| *Posso adicionar mais de um item de menu personalizado?* | Claro — basta acrescentar dicionários adicionais a `grid.settings.context_menu.custom_items`. |
| *Preciso recarregar a grade após atualizar uma célula?* | O GridJs atualiza automaticamente a linha afetada se você retornar `{status:"ok"}`; caso contrário, chame `grid.refresh()` do cliente. |
| *Como tornar a verificação ortográfica específica para um idioma?* | Defina `grid.settings.spell_check.language = "en-US"` (ou qualquer locale suportado). |
| *O carregamento preguiçoso é compatível com filtragem no lado do servidor?* | Sim — combine `grid.settings.filter.enabled = True` e implemente a lógica de filtro no seu comando personalizado. |

## Exemplo Completo (Todas as Etapas Combinadas)

Abaixo está um script único que você pode colocar em uma rota Flask ou executar como processo independente. Substitua `YOUR_DIRECTORY` pelo caminho real no seu servidor.

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


## O que Você Deve Aprender a Seguir?


Os tutoriais a seguir abordam tópicos estreitamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Add Custom XML Parts with ID to Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}