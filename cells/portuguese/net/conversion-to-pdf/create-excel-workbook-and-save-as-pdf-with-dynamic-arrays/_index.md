---
category: general
date: 2026-09-15
description: Crie uma pasta de trabalho do Excel em C# e aprenda a salvar a pasta
  de trabalho como PDF enquanto espalha arrays dinâmicos usando a função EXPAND.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: pt
lastmod: 2026-09-15
og_description: Crie uma pasta de trabalho do Excel em C# e salve rapidamente a pasta
  de trabalho como PDF usando a função EXPAND para gerar um array dinâmico.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: Criar pasta de trabalho do Excel e salvar como PDF com arrays dinâmicos
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Criar pasta de trabalho do Excel e salvar como PDF com arrays dinâmicos
url: /pt/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar pasta de trabalho Excel e salvar como PDF com arrays dinâmicos

Se você precisa **criar pasta de trabalho Excel** programaticamente e então **salvar a pasta de trabalho como PDF**, este guia mostra uma solução completa, de ponta a ponta, em C#. Você também verá como **despejar resultados de array dinâmico** usando a **função EXPAND**, que é a maneira moderna de gerar arrays sem VBA.  

Seja construindo um serviço de relatórios, um recurso de exportação para um sistema ERP ou um painel orientado a dados, os passos abaixo permitem gerar uma pasta de trabalho, preenchê‑la com dados de smart‑marker e produzir um PDF que preserva recursos avançados de fontes.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou posterior (o código também funciona com .NET Framework 4.8)
* Uma versão recente do **Aspose.Cells for .NET** (v25.8 ou mais nova) – ele fornece `Workbook`, `PdfSaveOptions` e `SmartMarkerProcessor`.
* Uma IDE como Visual Studio 2022 (qualquer editor que compile C# funciona).

Adicione o pacote NuGet ao seu projeto:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Etapa 1: Criar pasta de trabalho Excel e configurar a primeira planilha

A primeira tarefa é **criar pasta de trabalho Excel** e obter uma referência à planilha padrão. Esta planilha hospedará o array dinâmico e o modelo Smart Marker.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Por que isso importa*: Instanciar `Workbook` aloca a estrutura interna da pasta de trabalho, enquanto acessar `Worksheets[0]` fornece uma planilha pronta para uso sem precisar adicioná‑la manualmente.

## Etapa 2: Despejar array dinâmico usando a função EXPAND

A **função EXPAND** do Excel pode transformar um literal de array estático em um intervalo de spill de qualquer tamanho. Aqui pedimos ao Excel para expandir `{1,2,3}` em um intervalo de 5 linhas × 1 coluna começando em `A1`.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Por que isso importa*: Usar `EXPAND` evita loops manuais em C#. O motor calcula o intervalo de spill e armazena os valores diretamente na planilha, que depois aparecem no PDF.

## Etapa 3: Salvar pasta de trabalho como PDF preservando seletores de variação de fonte

Quando precisar **salvar a pasta de trabalho como PDF**, você também pode habilitar recursos tipográficos avançados, como seletores de variação de fonte (disponíveis a partir do Aspose.Cells v25.8). Isso garante que PDFs renderizem scripts complexos corretamente.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Por que isso importa*: Definir `FontVariationSelectors` como `true` é essencial para idiomas que dependem de variação de glifos (por exemplo, chinês, japonês, emoji). O PDF produzido reflete a visualização do Excel na tela.

## Etapa 4: Inserir um modelo Smart Marker que referencia uma fonte de dados aninhada

Smart Markers permitem incorporar marcadores de posição diretamente na planilha. O modelo abaixo gerará uma lista de pedidos e seus itens.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Por que isso importa*: Ao colocar o modelo em `A1`, você indica ao Aspose.Cells onde começar a expandir os dados. A sintaxe `:` (`Items:ItemName`) indica ao processador que deve iterar sobre uma coleção aninhada.

## Etapa 5: Definir a fonte de dados aninhada (pedidos contendo itens)

Criamos um array anônimo de pedidos, cada um contendo sua própria coleção de objetos item. Isso reflete um cenário típico mestre‑detalhe.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Por que isso importa*: A estrutura aninhada demonstra **como criar array dinâmico no Excel** através de Smart Markers, sem escrever VBA ou loops manuais de células.

## Etapa 6: Processar os Smart Markers e salvar o arquivo Excel final

Agora entregamos a pasta de trabalho e a fonte de dados ao `SmartMarkerProcessor`. Após o processamento, os marcadores são substituídos por linhas reais, e salvamos o resultado como um arquivo `.xlsx` comum.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Por que isso importa*: `SmartMarkerProcessor` expande automaticamente o modelo, cria as linhas necessárias e preenche‑as com dados. A pasta de trabalho final pode ser aberta no Excel para verificar se cada pedido e seus itens aparecem corretamente.

## Saída esperada

* **VarSelector.pdf** – um arquivo PDF que mostra os números 1‑3 se espalhando por cinco linhas, renderizado com quaisquer variações OpenType de fonte que você habilitou.
* **NestedSmartMarker.xlsx** – um arquivo Excel com as seguintes linhas (começando em `A1`):

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

A versão PDF mantém o mesmo spill numérico porque o estado da planilha foi salvo antes do processamento do Smart Marker; você pode repetir a gravação em PDF após o processamento se precisar dos dados finais também em PDF.

## Dicas profissionais e armadilhas comuns

| Dica | Explicação |
|------|------------|
| **Reutilizar o mesmo `PdfSaveOptions`** | Criar o objeto de opções uma única vez e reutilizá‑lo evita diferenças sutis na renderização (por exemplo, seletores de variação ausentes). |
| **Chamar `ws.Calculate()` após definir fórmulas** | Sem um cálculo explícito, o intervalo de spill pode permanecer vazio ao inspecionar a pasta de trabalho programaticamente. |
| **Colocar modelos Smart Marker em uma planilha limpa** | Misturar modelos com dados existentes pode causar inserções de linhas inesperadas. Use uma planilha dedicada, se possível. |
| **Ficar atento aos caminhos de arquivo** | Use `Path.Combine(Environment.CurrentDirectory, "output.pdf")` para evitar diretórios codificados em diferentes máquinas. |
| **Verificar a versão** | `FontVariationSelectors` está disponível apenas a partir da versão 25.8; versões anteriores ignorarão a propriedade sem lançar erro. |

## Próximos passos

Agora que você sabe como **criar pasta de trabalho Excel**, **despejar array dinâmico** e **salvar a pasta de trabalho como PDF**, pode explorar:

* Adicionar gráficos ou imagens antes da conversão para PDF.
* Exportar a mesma pasta de trabalho para outros formatos (por exemplo, HTML, CSV) usando sobrecargas do `Save`.
* Usar **expressões Smart Marker** (`${Orders.Total:SUM(Items.Price)}`) para calcular agregados em tempo real.
* Integrar este código em uma API ASP.NET Core para que os usuários baixem o PDF gerado diretamente de um endpoint web.

---

**Resumo** – Este tutorial mostrou como **criar pasta de trabalho Excel**, usar a **função EXPAND** para **despejar array dinâmico**, incorporar um **Smart Marker** que trabalha com uma fonte de dados aninhada e, finalmente, **salvar a pasta de trabalho como PDF** preservando recursos avançados de fontes. O exemplo completo e executável pode ser copiado para qualquer projeto C# e adaptado às suas próprias estruturas de dados. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}