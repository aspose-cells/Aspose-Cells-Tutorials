---
category: general
date: 2026-06-30
description: Crie uma instância do GridJs em Python com configurações personalizadas
  de modal. Aprenda como vincular uma planilha, configurar o modal e gerar JSON para
  o cliente.
draft: false
keywords:
- create gridjs instance
- gridjs custom modal
- gridjs worksheet integration
- gridjs client configuration
- gridjs python api
language: pt
og_description: Crie uma instância do GridJs em Python com configurações personalizadas
  de modal. Instruções passo a passo para integração de planilha e configuração do
  cliente.
og_title: Criar Instância GridJs – Guia Completo de Python
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create GridJs instance in Python with custom modal settings. Learn
    how to bind a worksheet, configure the modal, and output client JSON.
  headline: Create GridJs Instance – Complete Python Guide
  type: TechArticle
tags:
- gridjs
- python
- web‑ui
- data‑grid
title: Criar Instância GridJs – Guia Completo de Python
url: /pt/python/integration-and-interoperability/create-gridjs-instance-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Instância GridJs – Guia Completo em Python

Já se perguntou como **create gridjs instance** a partir do Python sem perder a cabeça? Você não está sozinho. Seja construindo um painel de administração, um catálogo de produtos ou uma planilha de visualização rápida, colocar o GridJs em funcionamento é o primeiro obstáculo.  

Neste tutorial, vamos percorrer um exemplo real: vincular uma planilha, ativar um modal personalizado que aparece ao dar duplo clique e, finalmente, obter o JSON de configuração do lado do cliente para que você possa enviá‑lo ao front‑end. Ao final, você terá uma configuração GridJs funcional que pode ser inserida em qualquer projeto Flask ou Django.

## Pré‑requisitos

- Python 3.8+ instalado localmente  
- Familiaridade básica com OOP em Python  
- Uma classe `Worksheet` mínima (iremos simular uma para a demonstração)  

Não existe um pacote externo do GridJs para Python, então simularemos a API que espelha a biblioteca JavaScript. Os conceitos se traduzem diretamente para o uso real do GridJs em JavaScript.

## Etapa 1: Definir uma Classe Mock GridJs (API GridJs Python)

Antes de podermos **create gridjs instance**, precisamos de um wrapper leve que imite a biblioteca real. Isso mantém o exemplo executável e foca no fluxo de configuração.

```python
# gridjs_mock.py
import json

class Settings:
    """Container for all GridJs settings."""
    def __init__(self):
        self.custom_modal = CustomModal()

class CustomModal:
    """Settings for the double‑click custom modal."""
    def __init__(self):
        self.enabled = False
        self.title = ""
        self.width = "400px"
        self.height = "300px"
        self.url = ""

class GridJs:
    """A lightweight Python representation of a GridJs grid."""
    def __init__(self):
        self._worksheet = None
        self.settings = Settings()

    def set_worksheet(self, worksheet):
        """Bind a Worksheet object to the grid."""
        self._worksheet = worksheet

    def get_client_config(self):
        """Serialize the grid configuration for the front‑end."""
        config = {
            "worksheet": getattr(self._worksheet, "name", "undefined"),
            "custom_modal": {
                "enabled": self.settings.custom_modal.enabled,
                "title": self.settings.custom_modal.title,
                "width": self.settings.custom_modal.width,
                "height": self.settings.custom_modal.height,
                "url": self.settings.custom_modal.url,
            },
        }
        return json.dumps(config, indent=2)
```

> **Dica de especialista:** Mantenha o wrapper Python leve — apenas o suficiente para gerar o JSON que você entregará ao lado JavaScript. Over‑engineering da ponte adiciona sobrecarga de manutenção.

## Etapa 2: Criar um Objeto Worksheet Simples (Integração Worksheet GridJs)

Nossa **gridjs worksheet integration** pode ser tão simples quanto uma classe com um atributo `name`. Em um aplicativo real, você obteria dados de um banco de dados ou de um arquivo CSV.

```python
# worksheet.py
class Worksheet:
    """Mock worksheet holding tabular data."""
    def __init__(self, name):
        self.name = name
        # Imagine self.rows = [...] here
```

Agora você tem um placeholder que pode ser passado para a grade.

## Etapa 3: Montar a Grade – A Lógica Central de “Create GridJs Instance”

Com as classes mock prontas, finalmente podemos **create gridjs instance** e configurá‑la passo a passo.

```python
# main.py
from gridjs_mock import GridJs
from worksheet import Worksheet

# 1️⃣ Create a GridJs instance
grid = GridJs()

# 2️⃣ Associate the worksheet you want to display
worksheet = Worksheet(name="Products")
grid.set_worksheet(worksheet)

# 3️⃣ Enable the custom modal that appears on double‑click
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Product"
grid.settings.custom_modal.width = "600px"
grid.settings.custom_modal.height = "400px"

# 4️⃣ Point the modal to an external HTML editor page
grid.settings.custom_modal.url = "/product-editor.html"

# 5️⃣ Retrieve the client‑side configuration JSON and output it
config_json = grid.get_client_config()
print(config_json)
```

### Saída Esperada (Configuração do Cliente GridJs)

Executar `python main.py` gera um blob JSON formatado de forma agradável:

```json
{
  "worksheet": "Products",
  "custom_modal": {
    "enabled": true,
    "title": "Edit Product",
    "width": "600px",
    "height": "400px",
    "url": "/product-editor.html"
  }
}
```

Esse JSON é exatamente o que você enviaria ao construtor GridJs do front‑end:

```javascript
new Grid({
  data: [],               // will be filled from the worksheet
  customModal: {/* … */} // values from the JSON above
});
```

## Etapa 4: Conectar o JSON a uma Página Front‑End (Juntando Tudo)

A **gridjs client configuration** que você acabou de imprimir pode ser incorporada em uma rota Flask:

```python
# app.py (Flask snippet)
from flask import Flask, render_template_string, jsonify
from main import config_json  # reuse the same grid setup

app = Flask(__name__)

@app.route("/grid-config")
def grid_config():
    return jsonify(json.loads(config_json))

# Simple HTML page loading GridJs from CDN
HTML = """
<!doctype html>
<html>
<head>
  <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
  <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
</head>
<body>
  <div id="wrapper"></div>
  <script>
    fetch('/grid-config')
      .then(r => r.json())
      .then(config => {
        new gridjs.Grid({
          columns: ['ID', 'Name', 'Price'],
          data: [], // fetch actual rows based on config.worksheet
          customModal: config.custom_modal
        }).render(document.getElementById('wrapper'));
      });
  </script>
</body>
</html>
"""
@app.route("/")
def index():
    return render_template_string(HTML)

if __name__ == "__main__":
    app.run(debug=True)
```

> **Por que isso funciona:** O back‑end fornece um payload JSON que espelha as configurações que você definiu em Python. O front‑end lê o mesmo payload, garantindo que o **gridjs custom modal** se comporte exatamente como configurado.

## Armadilhas Comuns e Casos de Borda (GridJs Custom Modal)

| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| Modal nunca abre ao dar duplo clique | `custom_modal.enabled` deixado como `False` | Certifique‑se de definir `grid.settings.custom_modal.enabled = True` |
| Dimensões do modal parecem estranhas no celular | Valores fixos em pixels (`600px`) não escalam | Use unidades CSS relativas (`80%`, `vh`) ou media queries |
| URL retorna 404 | O caminho `/product-editor.html` não está sendo servido | Adicione uma rota estática no Flask/Django ou hospede o arquivo em um CDN |
| Nome da Worksheet ausente no JSON | Objeto `Worksheet` não possui atributo `name` | Forneça um `name` significativo ou estenda o mock para incluir metadados |

Abordar esses problemas cedo economiza horas de depuração posteriormente.

## Extendendo o Exemplo (Próximos Passos)

- **Load real data**: Substitua o mock `Worksheet` por um pandas DataFrame e serialize as linhas para JSON.  
- **Secure the modal**: Adicione verificações de autenticação antes de servir `/product-editor.html`.  
- **Dynamic column mapping**: Obtenha os cabeçalhos das colunas do esquema da worksheet em vez de codificá‑los manualmente.  
- **Internationalization**: Armazene os títulos do modal em um arquivo de idioma e injete‑os via o payload JSON.  

Todas essas melhorias se baseiam na mesma fundação de **create gridjs instance** que você acabou de dominar.

## Conclusão

Cobrimos tudo o que você precisa para **create gridjs instance** em Python, desde conectar uma worksheet até ativar um modal personalizado e, finalmente, expor um JSON de configuração limpo do lado do cliente. O padrão é simples, reutilizável e se encaixa perfeitamente em qualquer framework web moderno.

Experimente, ajuste as dimensões do modal, troque a worksheet por uma consulta real ao banco de dados, e você terá uma integração GridJs pronta para produção em pouco tempo. Tem dúvidas? Deixe um comentário, e feliz codificação!

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Criar e Configurar Pastas de Trabalho Excel com Aspose.Cells .NET: Um Guia Passo a Passo](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Criar um PDF de Gráfico de Tamanho Personalizado com Aspose.Cells .NET: Guia Passo a Passo](/cells/english/net/charts-graphs/create-custom-size-chart-pdf-aspose-cells-net/)
- [Como Criar uma Função de Valor Estático Personalizada no Aspose.Cells Java](/cells/english/java/formulas-functions/aspose-cells-java-custom-static-value-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}