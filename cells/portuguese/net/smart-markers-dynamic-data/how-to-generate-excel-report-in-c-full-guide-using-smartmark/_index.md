---
category: general
date: 2026-03-22
description: Como gerar relatório Excel em C# com um modelo mestre‑detalhe. Aprenda
  a preencher rapidamente um modelo Excel em C#, usando SmartMarker para planilhas
  repetíveis.
draft: false
keywords:
- how to generate excel report
- populate excel template c#
- excel smartmarker c#
- master detail excel c#
- c# excel automation
language: pt
og_description: Como gerar relatório Excel em C# usando um modelo reutilizável. Este
  guia passo a passo mostra como preencher o modelo Excel em C# com dados mestre‑detalhe.
og_title: Como gerar relatório Excel em C# – Tutorial completo do SmartMarker
tags:
- Excel
- C#
- SmartMarker
- Reporting
title: Como gerar relatório Excel em C# – Guia completo usando SmartMarker
url: /pt/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Gerar Relatório Excel em C# – Guia Completo Usando SmartMarker

Já se perguntou **como gerar relatório Excel** em C# sem escrever código célula‑por‑célula interminável? Você não está sozinho. A maioria dos desenvolvedores bate em um muro quando precisa de um relatório polido, com várias planilhas, que reflita relacionamentos mestre‑detalhe — pense em pedidos e itens — mas não quer reinventar a roda a cada vez.

A boa notícia? Com um modelo Excel pronto e o motor **SmartMarker** do Aspose.Cells, você pode **populate Excel template C#** em apenas algumas linhas. Neste tutorial vamos percorrer um cenário real, explicar por que cada passo importa e fornecer um exemplo completo e executável que você pode copiar‑colar hoje.

> **O que você receberá:** um relatório Excel mestre‑detalhe onde cada pedido gera sua própria planilha, tudo impulsionado por objetos C# simples. Sem loops manuais sobre células, sem fórmulas frágeis — apenas código limpo e mantível.

---

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- **.NET 6.0** (ou superior) instalado – o código tem alvo .NET 6 mas funciona também no .NET Framework 4.7+.
- **Aspose.Cells for .NET** pacote NuGet (`Install-Package Aspose.Cells`) – fornece as classes `Workbook`, `SmartMarkerProcessor` e relacionadas.
- Um arquivo Excel chamado **MasterDetailTemplate.xlsx** colocado em `YOUR_DIRECTORY`. Ele deve conter um bloco SmartMarker como `{{Orders.OrderId}}` na primeira planilha e um bloco aninhado `{{Orders.Items.Prod}}` para os itens de linha.
- Um entendimento básico de tipos anônimos C# – usaremos eles para modelar pedidos e itens.

Se algum desses itens lhe for desconhecido, não se preocupe. Mencionaremos alternativas (por exemplo, usando EPPlus) mais adiante, mas o conceito central permanece o mesmo.

---

## Etapa 1: Carregar o Modelo Excel que Contém Blocos SmartMarker

A primeira coisa que fazemos é abrir o arquivo de modelo. Pense no modelo como um esqueleto; o SmartMarker preencherá depois com dados reais.

```csharp
using Aspose.Cells;

// Load the template containing SmartMarker tags
var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Por que isso importa:** Ao separar o layout (o modelo) dos dados (os objetos C#), você mantém designers e desenvolvedores felizes. Designers podem ajustar fontes, cores ou fórmulas sem tocar no código.

---

## Etapa 2: Construir a Fonte de Dados Mestre‑Detalhe

Em seguida, criamos os dados que irão popular o modelo. Para um relatório típico de pedidos, você tem uma coleção de pedidos, cada um com sua própria coleção de itens.

```csharp
// Master‑detail data: a list of orders, each with a list of items
var masterDetailData = new
{
    Orders = new[]
    {
        new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Prod = "A", Qty = 2 },
                new { Prod = "B", Qty = 1 }
            }
        },
        new
        {
            OrderId = 2,
            Items = new[]
            {
                new { Prod = "C", Qty = 5 }
            }
        }
    }
};
```

> **Dica profissional:** Use classes fortemente tipadas em vez de tipos anônimos se precisar reutilizar em vários relatórios. A abordagem anônima mantém o exemplo conciso.

**Por que isso importa:** O SmartMarker funciona combinando nomes de propriedades (`Orders`, `OrderId`, `Items`, `Prod`, `Qty`) com os marcadores no modelo. A hierarquia deve coincidir exatamente, caso contrário o motor ignorará essas seções.

---

## Etapa 3: Instruir o SmartMarker a Criar uma Nova Planilha para Cada Registro Mestre

Por padrão o SmartMarker grava todas as linhas em uma única planilha. Queremos cada pedido em sua própria planilha, o que é perfeito para impressão ou envio de PDFs por pedido posteriormente.

```csharp
// Enable a separate sheet for each master (order) record
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableRepeatingSheet = true // each Order gets its own sheet
};
```

**Por que isso importa:** `EnableRepeatingSheet` elimina a necessidade de clonagem manual de planilhas. O motor copia a planilha original, injeta os dados do pedido e renomeia a planilha automaticamente (geralmente usando o valor da primeira coluna).

---

## Etapa 4: Processar o Modelo com Seus Dados

Agora juntamos tudo. O `SmartMarkerProcessor` percorre a pasta de trabalho, substitui as tags e cria novas planilhas conforme instruído.

```csharp
// Apply the data to the workbook
workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);
```

**Por que isso importa:** Esta única linha faz o trabalho pesado — analisar o modelo, iterar sobre coleções e lidar com tabelas aninhadas. É o coração de **populate Excel template C#** sem loops manuais.

---

## Etapa 5: Salvar o Relatório Finalizado

Por fim, gravamos a pasta de trabalho preenchida no disco. Você também pode transmiti‑la diretamente para uma resposta HTTP em aplicações web.

```csharp
// Save the generated report
workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");
```

**Por que isso importa:** Salvar em um arquivo fornece um artefato tangível que você pode abrir no Excel, compartilhar com stakeholders ou alimentar em processos subsequentes como conversão para PDF.

---

## Exemplo Completo Funcionando (Pronto para Copiar‑Colar)

Abaixo está o programa completo, incluindo diretivas `using` e um método `Main`. Cole em um aplicativo console, ajuste os caminhos dos arquivos e execute.

```csharp
using System;
using Aspose.Cells;

namespace ExcelReportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template
            var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

            // 2️⃣ Build master‑detail data
            var masterDetailData = new
            {
                Orders = new[]
                {
                    new
                    {
                        OrderId = 1,
                        Items = new[]
                        {
                            new { Prod = "A", Qty = 2 },
                            new { Prod = "B", Qty = 1 }
                        }
                    },
                    new
                    {
                        OrderId = 2,
                        Items = new[]
                        {
                            new { Prod = "C", Qty = 5 }
                        }
                    }
                }
            };

            // 3️⃣ Enable a new sheet per order
            var smartMarkerOptions = new SmartMarkerOptions
            {
                EnableRepeatingSheet = true
            };

            // 4️⃣ Process the template with data
            workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);

            // 5️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");

            Console.WriteLine("Excel report generated successfully!");
        }
    }
}
```

### Saída Esperada

Ao abrir `MasterDetailResult.xlsx` você verá:

- **Planilha “Order_1”** – contém o cabeçalho do Pedido 1 e duas linhas para os produtos A e B.
- **Planilha “Order_2”** – contém o cabeçalho do Pedido 2 e uma única linha para o produto C.
- Todas as fórmulas, formatações e gráficos do modelo original são preservados.

![Relatório Excel com planilhas separadas para cada pedido – exemplo de pasta de trabalho preenchida](/images/excel-report-example.png "Relatório Excel gerado com dados mestre‑detalhe")

*Texto alternativo da imagem: relatório Excel gerado com planilhas separadas para cada pedido, mostrando como gerar relatório Excel usando C# e SmartMarker.*

---

## Perguntas Frequentes & Casos de Borda

### E se eu precisar de uma planilha estática (por exemplo, um resumo) ao lado das planilhas repetidas?

Defina `EnableRepeatingSheet = true` **apenas** na planilha que contém o bloco mestre. As demais planilhas permanecerão intactas, permitindo que você mantenha uma página de resumo no modelo original.

### Posso usar um DataTable em vez de objetos anônimos?

Com certeza. O SmartMarker funciona com qualquer objeto que implemente `IEnumerable`. Basta substituir o tipo anônimo por um `DataTable` e garantir que os nomes das colunas correspondam às tags.

```csharp
DataTable ordersTable = GetOrdersFromDatabase();
var data = new { Orders = ordersTable };
```

### Como altero a convenção de nomenclatura das planilhas geradas?

Implemente a interface personalizada `ISmartMarkerSheetNaming` (ou manipule `workbook.Worksheets` após o processamento). A maioria dos desenvolvedores simplesmente renomeia as planilhas com base no valor de uma célula:

```csharp
foreach (var sheet in workbook.Worksheets)
{
    sheet.Name = $"Order_{sheet.Cells["A1"].StringValue}";
}
```

### E se meu modelo usar uma sintaxe de placeholder diferente?

O SmartMarker permite delimitadores personalizados via `SmartMarkerOptions`. Por exemplo, para usar `<< >>` em vez de `{{ }}`:

```csharp
smartMarkerOptions.StartTag = "<<";
smartMarkerOptions.EndTag = ">>";
```

---

## Dicas para Escalar Essa Abordagem

- **Cache o modelo** na memória se você gerar muitos relatórios por requisição; carregar do disco a cada vez adiciona latência.
- **Combine com conversão para PDF** (`workbook.Save("report.pdf", SaveFormat.Pdf)`) para saídas amigáveis a e‑mail.
- **Parametrize os caminhos dos arquivos** usando arquivos de configuração ou variáveis de ambiente para tornar a solução portátil entre dev, teste e produção.
- **Teste unitariamente a camada de dados** separadamente; o SmartMarker é determinístico, então você só precisa verificar se os dados fornecidos correspondem ao esquema esperado.

---

## Conclusão

Cobremos **como gerar relatório Excel** em C# de ponta a ponta, desde o carregamento de um modelo habilitado para SmartMarker até a gravação de uma pasta de trabalho multi‑planilha que reflete relacionamentos mestre‑detalhe. Ao **populate Excel template C#** com apenas algumas linhas de código, você evita lógica frágil célula‑por‑célula e dá liberdade aos designers para moldar o visual final.

A seguir, você pode explorar:

- Usar **populate Excel template C#** com gráficos que atualizam automaticamente por planilha.
- Integrar **excel smartmarker c#** com ASP.NET Core para transmitir relatórios diretamente aos navegadores.
- Automatizar pipelines de **c# excel automation** que extraem dados de APIs ou bancos de dados.

Experimente, ajuste o modelo e veja como rapidamente você pode transformar dados brutos em um relatório Excel refinado. Tem dúvidas ou um caso de uso interessante? Deixe um comentário abaixo — feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}