---
category: general
date: 2026-05-04
description: Criar Excel a partir de um modelo e mapear JSON para Excel com nomeação
  dinâmica de planilhas. Aprenda como preencher o Excel a partir de JSON e gerar Excel
  usando JSON em minutos.
draft: false
keywords:
- create excel from template
- map json to excel
- populate excel from json
- dynamic worksheet naming excel
- generate excel using json
language: pt
og_description: Crie Excel a partir de um modelo rapidamente. Este guia mostra como
  mapear JSON para Excel, preencher Excel a partir de JSON, usar nomes de planilhas
  dinâmicos e gerar Excel usando JSON.
og_title: Criar Excel a partir de Modelo – Tutorial Completo de .NET
tags:
- C#
- Aspose.Cells
- SmartMarker
- JSON
title: Criar Excel a partir de um modelo – Guia passo a passo para desenvolvedores
  .NET
url: /pt/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Excel a partir de Modelo – Tutorial Completo .NET

Já precisou **criar Excel a partir de um modelo** mas se sentiu preso tentando lidar com dados JSON e nomes de planilhas? Você não está sozinho. Em muitos projetos de relatórios, o modelo contém o layout enquanto a carga JSON fornece os valores reais, e fazer com que eles conversem pode ser uma dor de cabeça.  

A boa notícia? Com algumas linhas de C# e o motor SmartMarker do Aspose Cells você pode **preencher Excel a partir de JSON**, renomear planilhas de detalhe em tempo real e, finalmente, **gerar Excel usando JSON** sem nunca tocar na interface.  

Neste tutorial vamos percorrer todo o pipeline: carregar um modelo, mapear JSON para Excel, configurar a nomeação dinâmica de planilhas e salvar a pasta de trabalho final. Ao final você terá um trecho reutilizável que pode inserir em qualquer serviço .NET. Sem ferramentas externas, apenas código puro.

---

## O que você precisará

- **Aspose.Cells for .NET** (v24.10 ou posterior) – a biblioteca que alimenta o SmartMarker.  
- Um arquivo **template.xlsx** que contém tags SmartMarker como `{Master:Name}` e `{Detail:Item}`.  
- Um arquivo **data.json** que corresponde à estrutura mestre‑detalhe.  
- Visual Studio 2022 (ou qualquer IDE de sua preferência) direcionado ao .NET 6 ou posterior.  

É só isso. Se você já tem esses itens, está pronto para começar.

---

## Criar Excel a partir de Modelo – Visão Geral

A ideia central é simples: trate o arquivo Excel como um *modelo* e deixe o SmartMarker substituir os marcadores pelos valores do seu JSON. A biblioteca também permite renomear a planilha de detalhe com base em um campo mestre, que é onde **dynamic worksheet naming excel** brilha.

Abaixo está o código completo, pronto‑para‑executar. Sinta‑se à vontade para copiar‑colar em um aplicativo console e apontar os caminhos para seus próprios arquivos.

```csharp
// ------------------------------------------------------------
// Full example: create Excel from template using JSON data
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains SmartMarker tags
            //    (e.g., {Master:Name} in the master sheet and {Detail:Item} in the detail sheet)
            string templatePath = @"C:\MyProject\Templates\template.xlsx";
            Workbook wb = new Workbook(templatePath);

            // 2️⃣ Read the JSON data that will populate the markers
            //    The JSON should match the structure expected by the template.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // 3️⃣ Configure the SmartMarker processor to rename the detail sheet
            //    dynamically based on the master record’s Name field.
            //    This demonstrates dynamic worksheet naming excel.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // 4️⃣ Execute the SmartMarker processing using the JSON data.
            //    This step maps JSON to Excel and populates every marker.
            wb.SmartMarkerProcessor.Execute(json);

            // 5️⃣ Save the processed workbook – now it’s a brand‑new file.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Excel file generated successfully at: " + outputPath);
        }
    }
}
```

> **Resultado esperado:**  
> - A planilha mestre exibirá o nome de `Master.Name`.  
> - A planilha de detalhe será renomeada para algo como `Detail_JohnDoe`.  
> - Todas as linhas `{Detail:Item}` serão preenchidas com o array de itens do JSON.

---

## Mapear JSON para Excel – Carregando Dados

Antes que o motor SmartMarker possa fazer sua mágica, o JSON deve estar **bem‑formado** e refletir a hierarquia usada no modelo. Um JSON típico mestre‑detalhe se parece com isto:

```json
{
  "Master": {
    "Name": "John Doe",
    "Date": "2026-05-04"
  },
  "Detail": [
    { "Item": "Widget A", "Qty": 10, "Price": 2.5 },
    { "Item": "Widget B", "Qty": 5,  "Price": 5.0 }
  ]
}
```

**Por que isso importa:**  
- As chaves `Master` e `Detail` correspondem diretamente às tags `{Master:…}` e `{Detail:…}`.  
- Se a estrutura do JSON divergir, o SmartMarker não encontrará correspondência e as células permanecerão vazias.  

**Dica:** Valide seu JSON com um validador online rápido ou `System.Text.Json.JsonDocument.Parse(json)` para capturar erros de sintaxe cedo.

---

## Preencher Excel a partir de JSON – Configuração do SmartMarker

O SmartMarker funciona escaneando a pasta de trabalho em busca de tags e, em seguida, injetando os dados. A etapa **populate excel from json** é essencialmente a chamada `Execute` que vimos antes, mas há algumas configurações opcionais que valem a pena mencionar:

| Configuração | O que faz | Quando usar |
|--------------|-----------|-------------|
| `Options.CaseSensitive` | Trata os nomes das tags como sensíveis a maiúsculas/minúsculas. | Se seu modelo mistura casos e você precisa de correspondência estrita. |
| `Options.RemoveEmptyRows` | Exclui linhas que não receberam dados. | Para manter a planilha final organizada quando alguns itens de detalhe são opcionais. |
| `Options.EnableHyperlink` | Permite que hyperlinks dentro do JSON se tornem clicáveis. | Quando você precisa de URLs clicáveis no relatório. |

Você pode encadeá‑las assim:

```csharp
wb.SmartMarkerProcessor.Options.CaseSensitive = true;
wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;
```

---

## Nomeação Dinâmica de Planilhas Excel – Configurar Nome da Planilha de Detalhe

Um dos requisitos mais complicados que muitos projetos têm é **dynamic worksheet naming excel**. Em vez de uma planilha “Detail” estática, você pode querer que cada relatório carregue o nome do cliente ou um número de pedido.

A linha:

```csharp
wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";
```

faz exatamente isso. O placeholder `{Master.Name}` é substituído *depois* que o JSON é processado, de modo que o novo nome da planilha se torna `Detail_JohnDoe`.  

**Caso limite:** Se o nome contiver caracteres ilegais em nomes de planilhas (`:`, `\`, `/`, `?`, `*`, `[`, `]`), o Aspose os sanitiza automaticamente, mas você pode limpar a string no JSON se precisar de um formato específico.

---

## Gerar Excel usando JSON – Executar e Salvar

As duas linhas finais do código (`Execute` e `Save`) são onde a magia do **generate excel using json** acontece. Nos bastidores, o Aspose analisa o JSON em uma tabela de dados, itera sobre o modelo e grava o arquivo de saída.

Se precisar gerar várias pastas de trabalho em um loop (por exemplo, uma por cliente), basta mover a instanciação de `Workbook` para dentro do loop e alterar o nome do arquivo de saída conforme necessário:

```csharp
foreach (var customerJson in customers)
{
    Workbook wb = new Workbook(templatePath);
    wb.SmartMarkerProcessor.Options.DetailSheetNewName = $"Detail_{customerJson.Master.Name}";
    wb.SmartMarkerProcessor.Execute(customerJson);
    wb.Save($@"C:\Reports\Report_{customerJson.Master.Name}.xlsx");
}
```

Esse padrão é comum em serviços de relatórios em lote.

---

## Erros Comuns e Dicas Profissionais

- **Missing tags:** Se uma célula ainda mostra `{Master:Name}`, a tag não foi reconhecida. Verifique a ortografia e se a tag está dentro de uma célula, não em um comentário.  
- **Large JSON payloads:** Para conjuntos de dados massivos, considere fazer streaming do JSON ou usar `DataTable` em vez de uma string bruta para reduzir a pressão de memória.  
- **Thread safety:** Instâncias de `Workbook` não são seguras para uso simultâneo. Crie uma nova instância por thread se estiver executando tarefas paralelas.  
- **File locks:** Garanta que o modelo não esteja aberto no Excel enquanto seu código roda; caso contrário, você encontrará um `IOException`.  

> **Dica profissional:** Mantenha uma cópia do modelo original em uma pasta somente‑leitura. Isso evita sobrescritas acidentais durante a depuração.

---

## Recapitulação do Exemplo Completo em Funcionamento

Aqui está o programa inteiro novamente, desta vez com comentários inline para cada linha não óbvia:

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Path to the Excel template that contains SmartMarker tags.
            string templatePath = @"C:\MyProject\Templates\template.xlsx";

            // Load the workbook – this is the "create excel from template" step.
            Workbook wb = new Workbook(templatePath);

            // Read JSON data that maps directly to the template's tags.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // OPTIONAL: tweak SmartMarker behavior (case‑sensitivity, empty rows, etc.).
            wb.SmartMarkerProcessor.Options.CaseSensitive = false;
            wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;

            // Set up dynamic worksheet naming based on the master record's Name field.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // Run the SmartMarker engine – this is where we "populate excel from json".
            wb.SmartMarkerProcessor.Execute(json);

            // Save the newly generated workbook – the final "generate excel using json" step.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Workbook created at: " + outputPath);
        }
    }
}
```

Executar este aplicativo console produzirá `output.xlsx` com a planilha de detalhe renomeada e todos os dados preenchidos.

---

## Próximos Passos e Tópicos Relacionados

- **Export to PDF:** Após gerar a pasta de trabalho, você pode chamar `wb.Save("report.pdf", SaveFormat.Pdf);` para entregar uma versão em PDF.  
- **Chart population:** O SmartMarker também suporta fontes de dados de gráficos; basta vincular o array JSON ao intervalo de séries do gráfico.  
- **Conditional formatting:** Use as regras internas do Excel no modelo; elas permanecerão após a substituição do SmartMarker.  
- **Performance tuning:** Para cenários de alto volume, reutilize uma única instância de `Workbook` com `Clone` para evitar I/O de arquivo repetido.  

Sinta‑se à vontade para experimentar diferentes estruturas JSON, padrões de renomeação ou até combinar múltiplos modelos em uma única execução. A flexibilidade de **create excel from template** usando Aspose.Cells permite adaptar a solução a faturas, dashboards ou qualquer necessidade de relatório.

---

## Resumo Visual

![Fluxo de criação de Excel a partir de modelo mostrando JSON → SmartMarker → Nomeação Dinâmica de Planilha](/images/create-excel-from-template-workflow.png "Diagrama do fluxo de criação de Excel a partir de modelo")

*(O texto alternativo inclui a palavra‑chave principal para SEO)*

---

### Conclusão

Cobremos tudo o que você precisa para **create excel from template**, **map JSON to Excel**, **populate Excel from JSON**, usar **dynamic worksheet naming excel** e, finalmente, **generate Excel using JSON**. O código está completo, as explicações mostram *por que* cada linha importa, e agora você tem uma base sólida para construir pipelines de relatório maiores.

Tem alguma variação que está tentando implementar? Deixe um comentário abaixo e vamos solucionar juntos. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}