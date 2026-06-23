---
category: general
date: 2026-03-25
description: Como criar um modelo usando Smart Markers e aprender a repetir linhas,
  vincular dados, gerar relatórios e criar modelos sem esforço.
draft: false
keywords:
- how to write template
- how to repeat rows
- how to bind data
- how to generate report
- how to create template
language: pt
og_description: Como escrever um modelo usando Smart Markers. Descubra como repetir
  linhas, vincular dados, gerar relatório e criar modelo em C#.
og_title: Como escrever um modelo com marcadores inteligentes – Guia completo
tags:
- Aspose.Cells
- C#
- SmartMarkers
title: Como escrever um modelo com marcadores inteligentes – Guia passo a passo
url: /pt/net/smart-markers-dynamic-data/how-to-write-template-with-smart-markers-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como escrever modelo com Marcadores Inteligentes – Tutorial completo  

Já se perguntou **como escrever modelo** que se expanda automaticamente com base nos seus dados? Você não está sozinho—muitos desenvolvedores encontram um obstáculo quando precisam de um relatório Excel dinâmico, mas não sabem qual recurso da API usar. A boa notícia? Com os Marcadores Inteligentes do Aspose.Cells você pode criar um modelo de célula única, vincular dados hierárquicos e deixar a biblioteca repetir linhas por você. Neste guia também abordaremos **como repetir linhas**, **como vincular dados** e até **como gerar relatório** sem percorrer manualmente as planilhas.

Ao final deste tutorial você terá um exemplo completo e executável que mostra **como criar modelo** para cenários mestre‑detalhe, além de dicas para casos extremos e truques de desempenho. Nenhuma documentação externa é necessária—tudo que você precisa está aqui.

---

## O que você vai construir

Vamos gerar uma pasta de trabalho Excel que lista pedidos (o mestre) e seus itens de linha (o detalhe). O modelo fica na célula **A1**, e os Marcadores Inteligentes o expandirão em uma tabela bem formatada. A planilha final ficará assim:

```
Order1
   A
   B
Order2
   C
```

Esse é um cenário clássico de “como gerar relatório”, e o código funciona com .NET 6+ e Aspose.Cells 23.x (ou posterior).

---

## Pré‑requisitos

- .NET 6 SDK (ou qualquer versão recente do .NET)  
- Visual Studio 2022 ou VS Code  
- Aspose.Cells para .NET (instale via NuGet: `Install-Package Aspose.Cells`)  

Se você tem isso, está pronto para começar.

---

## Etapa 1: Configurar o Projeto e Adicionar Aspose.Cells  

```csharp
// Create a new console app (run this in a terminal)
// dotnet new console -n SmartMarkerDemo
// cd SmartMarkerDemo
// dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new workbook with a single worksheet
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];
```

*Por que isso importa*: Começar com um `Workbook` novo garante uma tela limpa. O objeto `Worksheet` é onde colocaremos nosso modelo.

---

## Etapa 2: Escrever o Modelo de Marcador Inteligente  

O modelo usa `${Master.Name}` para o título do pedido e `${Detail:Repeat}` para iterar sobre cada item de linha.

```csharp
            // Step 2: Define a Smart Marker template that repeats detail rows for each master record
            string smartMarkerTemplate = @"${Master.Name}
${Detail:Repeat}
   ${Detail.Item}
${/Detail}";
            
            // Write the template into cell A1
            worksheet.Cells["A1"].PutValue(smartMarkerTemplate);
```

> **Dica profissional**: Mantenha o modelo em uma única célula; os Marcadores Inteligentes o expandirão automaticamente nas linhas.  

*Como isso resolve o problema*: Ao incorporar o bloco de repetição diretamente na célula, você evita inserções manuais de linhas—Aspose cuida disso para você.

---

## Etapa 3: Construir Dados Hierárquicos que Correspondam ao Modelo  

Nossos dados devem espelhar a estrutura do modelo: uma coleção `Master`, cada uma contendo um array `Detail`.

```csharp
            // Step 3: Create hierarchical data matching the template structure
            var orderData = new
            {
                Master = new[]
                {
                    new
                    {
                        Name = "Order1",
                        Detail = new[]
                        {
                            new { Item = "A" },
                            new { Item = "B" }
                        }
                    },
                    new
                    {
                        Name = "Order2",
                        Detail = new[]
                        {
                            new { Item = "C" }
                        }
                    }
                }
            };
```

*Por que vinculamos os dados desta forma*: Os Marcadores Inteligentes usam vinculação ao estilo de reflexão, portanto os nomes das propriedades devem coincidir exatamente com os marcadores. Isso é o núcleo de **como vincular dados** para relatórios dinâmicos.

---

## Etapa 4: Processar o Modelo – Deixe os Marcadores Inteligentes Fazem o Trabalho Pesado  

```csharp
            // Step 4: Process the Smart Markers – the template will be expanded using the data above
            worksheet.SmartMarkerProcessor.Process(orderData);
```

Após o processamento, a planilha conterá as linhas expandidas. Sem loops, sem gravações manuais de células.

---

## Etapa 5: Salvar a Pasta de Trabalho  

```csharp
            // Save the result to an XLSX file
            workbook.Save("SmartMarkerReport.xlsx", SaveFormat.Xlsx);
            System.Console.WriteLine("Report generated: SmartMarkerReport.xlsx");
        }
    }
}
```

Abra o arquivo gerado e você verá o layout mestre‑detalhe exatamente como descrito anteriormente. Isso é **como gerar relatório** com uma única linha de código de processamento.

---

## Visão Geral Visual  

![Excel report generated by Smart Markers – how to write template](/images/smart-marker-report.png "how to write template")

*Texto alternativo*: "how to write template" – captura de tela do arquivo Excel final mostrando linhas repetidas para cada pedido.

---

## Análise Detalhada: Por que os Marcadores Inteligentes São um Divisor de Águas  

### Como Repetir Linhas Sem um Loop  

A automação tradicional do Excel obriga você a calcular a última linha, inserir novas linhas e copiar estilos—todas tarefas propensas a erros. Os Marcadores Inteligentes substituem isso por um bloco declarativo `${Detail:Repeat}`. O mecanismo analisa o bloco, clona a linha para cada elemento da coleção e injeta os valores. Essa abordagem é **como repetir linhas** de forma eficiente.

### Vinculando Objetos Complexos  

Você pode vincular objetos aninhados, coleções ou até DataTables. Desde que os nomes das propriedades estejam alinhados, o processador percorrerá o grafo de objetos. Essa é a essência de **como vincular dados**: você fornece ao processador um objeto CLR simples (ou um tipo anônimo, como fizemos) e deixa que ele faça o mapeamento automaticamente.

### Gerando Diferentes Formatos  

Embora nosso exemplo salve em XLSX, você pode trocar `SaveFormat.Pdf` ou `SaveFormat.Csv` com uma única linha de alteração. Esse é um caminho rápido para **como gerar relatório** em vários formatos sem tocar no modelo.

### Reutilizando o Modelo  

Se você precisar **como criar modelo** para outras planilhas, basta copiar o conteúdo da célula para outra aba ou armazená-lo em um recurso de string. A mesma chamada ao processador funciona em todos os lugares, tornando seu código DRY e fácil de manter.

---

## Perguntas Frequentes & Casos Limite  

| Pergunta | Resposta |
|----------|----------|
| *E se um mestre não tiver linhas de detalhe?* | O bloco `${Detail:Repeat}` será ignorado, deixando apenas o nome do mestre. Nenhuma linha vazia será criada. |
| *Posso estilizar as linhas repetidas?* | Sim—aplique formatação à linha modelo (fonte, bordas, etc.) antes do processamento. O estilo é copiado para cada linha gerada. |
| *Preciso descartar o workbook?* | O `Workbook` implementa `IDisposable`. Envolva‑o em um bloco `using` para código de produção, mas para uma demonstração rápida de console é opcional. |
| *Quão grande podem ser os dados?* | Os Marcadores Inteligentes são eficientes em memória, mas coleções extremamente grandes (centenas de milhares) podem exigir paginação ou streaming. |
| *Posso usar um arquivo JSON em vez de um objeto?* | Com certeza—deserializar JSON em um POCO que corresponda ao modelo, e então passá‑lo para `Process`. |

---

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

```csharp
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize workbook
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];

            // Define template
            string smartMarkerTemplate = @"${Master.Name}
${Detail:Repeat}
   ${Detail.Item}
${/Detail}";

            worksheet.Cells["A1"].PutValue(smartMarkerTemplate);

            // Prepare data
            var orderData = new
            {
                Master = new[]
                {
                    new
                    {
                        Name = "Order1",
                        Detail = new[]
                        {
                            new { Item = "A" },
                            new { Item = "B" }
                        }
                    },
                    new
                    {
                        Name = "Order2",
                        Detail = new[]
                        {
                            new { Item = "C" }
                        }
                    }
                }
            };

            // Process template
            worksheet.SmartMarkerProcessor.Process(orderData);

            // Save file
            workbook.Save("SmartMarkerReport.xlsx", SaveFormat.Xlsx);
            System.Console.WriteLine("Report generated: SmartMarkerReport.xlsx");
        }
    }
}
```

Execute o programa (`dotnet run`) e abra *SmartMarkerReport.xlsx* – você verá as linhas mestre‑detalhe organizadas de forma limpa.

---

## Recapitulação  

Respondemos **como escrever modelo** usando os Marcadores Inteligentes do Aspose.Cells, demonstramos **como repetir linhas**, mostramos **como vincular dados** com objetos hierárquicos e ilustramos **como gerar relatório** em XLSX (ou qualquer outro formato suportado). O mesmo padrão permite que você **como criar modelo** para faturas, inventários ou qualquer layout mestre‑detalhe que imaginar.

---

## O que vem a seguir?  

- **Estilizar a saída**: aplique estilos de célula à linha modelo antes do processamento.  
- **Exportar para PDF**: altere `SaveFormat.Xlsx` para `SaveFormat.Pdf` para um relatório imprimível.  
- **Cabeçalhos dinâmicos**: adicione marcadores `${Headers}` para gerar títulos de colunas dinamicamente.  
- **Múltiplas planilhas**: repita o processo em planilhas adicionais para relatórios de múltiplas seções.  

Sinta-se à vontade para experimentar—troque a fonte de dados, adicione mais níveis aninhados ou combine com fórmulas. A flexibilidade dos Marcadores Inteligentes significa que você gasta menos tempo codificando loops e mais tempo entregando valor.

*Feliz codificação! Se você encontrou algum problema, deixe um comentário abaixo ou me chame no Stack Overflow com a tag `aspose-cells`. Vamos manter a conversa em andamento.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}