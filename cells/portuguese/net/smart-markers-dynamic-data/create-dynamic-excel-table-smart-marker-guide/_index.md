---
category: general
date: 2026-05-23
description: Crie uma tabela dinâmica no Excel usando um modelo e dados JSON. Aprenda
  como carregar o modelo do Excel, automatizar o relatório do Excel e preencher o
  Excel a partir de JSON rapidamente.
draft: false
keywords:
- create dynamic excel table
- load excel template
- automate excel report
- populate excel from json
- generate excel report json
language: pt
og_description: Crie tabelas dinâmicas no Excel em minutos com um modelo e JSON. Este
  tutorial mostra como carregar o modelo do Excel, automatizar o relatório do Excel
  e preencher o Excel a partir de JSON.
og_title: Crie Tabela Dinâmica no Excel – Guia do Marcador Inteligente
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create dynamic excel table using a template and JSON data. Learn how
    to load excel template, automate excel report, and populate excel from json quickly.
  headline: Create Dynamic Excel Table – Smart Marker Guide
  type: TechArticle
tags:
- Excel
- Smart Markers
- JSON
- .NET
title: Criar Tabela Dinâmica no Excel – Guia de Marcador Inteligente
url: /pt/net/smart-markers-dynamic-data/create-dynamic-excel-table-smart-marker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Tabela Dinâmica do Excel – Guia de Smart Marker

Já precisou **criar tabela dinâmica do excel** que se expanda automaticamente para cada registro no seu conjunto de dados? Você não está sozinho. Seja construindo um painel de vendas mensal ou um pacote de faturas por cliente, a capacidade de **preencher excel a partir de json** sem escrever loops intermináveis pode economizar horas.

Neste tutorial, percorreremos uma solução completa e prática que mostra como **carregar modelo excel**, incorporar um Smart Marker, alimentá‑lo com JSON e, finalmente, **automatizar a geração de relatórios excel**. Ao final, você terá um projeto .NET pronto‑para‑executar que produz uma planilha Excel polida a partir de um único payload JSON.

---

## O que você precisará

- **Aspose.Cells for .NET** (ou qualquer biblioteca que suporte Smart Markers). O exemplo usa a versão 24.5, mas qualquer versão recente funciona.
- Visual Studio 2022 (ou sua IDE C# favorita).
- Um arquivo de modelo Excel simples (`template.xlsx`) colocado em uma pasta que você controla.
- Uma string JSON contendo uma coleção chamada `Customers`.

É isso—nenhum serviço extra, nenhuma conexão de banco de dados, apenas código puro.

---

## Etapa 1: Criar uma Pasta de Trabalho Modelo – Carregar Modelo Excel

A primeira coisa que fazemos é **carregar modelo excel** na memória. Pense no modelo como uma tela onde um placeholder especial indica ao processador onde repetir linhas.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook (make sure the path is correct)
Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

// Grab the first worksheet – this is where our Smart Marker lives
Worksheet worksheet = workbook.Worksheets[0];
```

> **Por que isso importa:** Carregar o modelo uma única vez mantém o I/O de arquivo mínimo e permite reutilizar o mesmo layout para vários relatórios. Também isola a lógica do Smart Marker do restante do seu código, proporcionando uma separação limpa de responsabilidades.

---

## Etapa 2: Inserir um Smart Marker – Criar Tabela Dinâmica do Excel

Agora incorporamos um **Smart Marker** que repetirá uma tabela para cada entrada na coleção `Customers`. A sintaxe `${Customers.RepeatWorksheet}` indica ao Aspose.Cells para clonar a planilha inteira para cada cliente.

```csharp
// Place the Smart Marker in cell A1 (top‑left corner)
worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");
```

> **Dica profissional:** Se você precisar repetir apenas linhas em vez de planilhas inteiras, use `${Customers.Repeat}` na primeira linha da tabela. A repetição ao nível de planilha é útil quando cada cliente recebe sua própria aba.

---

## Etapa 3: Preparar o SmartMarkerProcessor – Automatizar Relatório Excel

Com o marcador no lugar, criamos um `SmartMarkerProcessor`. Este objeto orquestra o vínculo de dados entre o JSON e o modelo Excel.

```csharp
// Initialize the processor with the workbook that contains the marker
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

O processador é leve; você pode reutilizá‑lo para múltiplos payloads JSON, se desejar.

---

## Etapa 4: Alimentar Dados JSON – Preencher Excel a partir de JSON

É aqui que a mágica acontece. Alimentamos uma string JSON que contém um array de clientes. Cada cliente pode ter campos como `Name`, `Email` e `Total`.

```csharp
// Sample JSON data – in a real scenario you might read this from a file or API
string customersJson = @"
{
  ""Customers"": [
    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
  ]
}";

// Apply the JSON to the processor – this populates the workbook
processor.ApplyJson(customersJson);
```

> **Por que JSON?** JSON é independente de linguagem e fácil de gerar a partir de APIs, bancos de dados ou até mesmo entrada manual. Usar `ApplyJson` significa que você não precisa mapear objetos manualmente; o processador faz o trabalho pesado.

---

## Etapa 5: Salvar o Resultado – Gerar Relatório Excel JSON

Finalmente, gravamos a pasta de trabalho preenchida no disco. O arquivo de saída agora contém uma planilha separada para cada cliente, cada uma preenchida com os dados do nosso JSON.

```csharp
// Save the filled workbook – choose a path that makes sense for your app
workbook.Save(@"C:\Reports\output.xlsx");
```

### Saída Esperada

- **output.xlsx** terá três planilhas nomeadas `Sheet1`, `Sheet2`, `Sheet3` (ou qualquer convenção de nomenclatura que seu modelo use).
- Cada planilha exibirá os valores `Name`, `Email` e `Total` de um único cliente.
- O layout que você projetou em `template.xlsx` (cabeçalhos, estilos, fórmulas) é preservado em todas as planilhas geradas.

---

## Exemplo Completo em Funcionamento

Abaixo está o programa completo, pronto‑para‑executar. Copie‑e‑cole em um aplicativo console, ajuste os caminhos dos arquivos e pressione **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace DynamicExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            string templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert the Smart Marker that repeats the worksheet per customer
            worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");

            // 3️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // 4️⃣ JSON data containing a collection of customers
            string customersJson = @"
            {
                ""Customers"": [
                    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
                    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
                    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
                ]
            }";

            // Apply the JSON – this populates the workbook dynamically
            processor.ApplyJson(customersJson);

            // 5️⃣ Save the generated report
            string outputPath = @"C:\Reports\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Dynamic Excel report generated at: {outputPath}");
        }
    }
}
```

Execute o programa, abra `output.xlsx` e você verá uma **criar tabela dinâmica do excel** em ação—cada cliente recebe sua própria planilha, totalmente formatada como você projetou.

---

## Perguntas Frequentes & Casos Limite

| Pergunta | Resposta |
|----------|----------|
| *E se meu JSON tiver objetos aninhados?* | Smart Markers suportam notação de ponto (`${Customers.Address.City}`) desde que a hierarquia JSON corresponda. |
| *Posso nomear as planilhas geradas com o nome do cliente?* | Sim—adicione um marcador como `${Customers.Name}` na célula de nome da planilha ou use `processor.ApplyJson(customersJson, "Customers")` com um padrão de nomenclatura. |
| *E quanto a grandes conjuntos de dados (10 k+ linhas)?* | O processador transmite dados de forma eficiente, mas fique atento à memória. Considere dividir o relatório em vários arquivos se atingir limites de desempenho. |
| *Preciso de licença para Aspose.Cells?* | Uma avaliação gratuita funciona para testes, mas uma versão licenciada remove marcas d'água de avaliação e concede todos os recursos. |
| *Posso usar esta abordagem com .NET Core?* | Com certeza—Aspose.Cells suporta .NET 6/7/8. Basta referenciar o pacote NuGet e o código permanece o mesmo. |

---

## Dicas para Implementações Prontas para Produção

- **Validar JSON** antes de alimentá‑lo ao `ApplyJson`. Um payload malformado lançará uma `JsonParseException`.
- **Cachear o modelo** se você gerar muitos relatórios em pouco tempo; carregar do disco repetidamente gera I/O desnecessário.
- **Bloquear a pasta de trabalho** durante o processamento se você executar isso em um serviço web multithread para evitar condições de corrida.
- **Adicionar tratamento de erros** ao redor de `workbook.Save` para lidar graciosamente com problemas de permissão ou arquivos bloqueados.
- **Personalizar estilos** no modelo (formatação condicional, fórmulas) para que as planilhas geradas mantenham a lógica de negócios sem código extra.

---

## Conclusão

Agora você tem um padrão sólido, de ponta a ponta, de como **criar tabela dinâmica do excel** usando um modelo, Smart Markers e dados JSON. Ao **carregar modelo excel**, inserir um marcador de repetição e **preencher excel a partir de json**, você pode **automatizar a geração de relatórios excel** com apenas algumas linhas de C#.

Próximos passos? Experimente adicionar gráficos que referenciem as tabelas dinâmicas, ou exportar o mesmo JSON para PDF usando Aspose.Words. Você também pode experimentar **gerar relatório excel json** a partir de uma consulta ao banco de dados para fechar o ciclo.

## Tutoriais Relacionados

- [Criar uma Tabela Dinâmica no Excel Usando Aspose.Cells para .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Criar Gráficos de Linha Dinâmicos no Excel Usando Aspose.Cells para .NET: Um Guia Passo a Passo](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Como Criar Caixas de Seleção no Excel usando Aspose.Cells para .NET | Tutorial de Validação de Dados](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}