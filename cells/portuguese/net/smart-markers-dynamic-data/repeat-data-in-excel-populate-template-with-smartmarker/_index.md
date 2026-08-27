---
category: general
date: 2026-02-21
description: Repita dados no Excel rapidamente usando SmartMarker — aprenda a preencher
  o modelo do Excel e repetir linhas sem esforço.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: pt
og_description: Repita dados no Excel usando SmartMarker. Aprenda como preencher um
  modelo do Excel, repetir linhas e automatizar suas planilhas.
og_title: repetir dados no Excel – Preencher modelo com SmartMarker
tags:
- excel
- csharp
- smartmarker
- automation
title: repetir dados no Excel – Preencher modelo com SmartMarker
url: /pt/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# repetir dados no excel – Preencher modelo com SmartMarker

Já precisou **repetir dados no Excel** mas não sabia como evitar copiar‑colar manualmente? Você não está sozinho. Em muitos cenários de relatórios você tem uma lista de itens que deve se expandir em linhas automaticamente, e fazer isso manualmente é uma receita para erros.

A questão é que—usar o SmartMarkerProcessor da biblioteca **GemBox.Spreadsheet** permite que você **preencha um modelo Excel** com uma única linha de C# e faça as linhas se repetirem para cada item da sua coleção. Neste guia vamos percorrer os passos exatos, mostrar o código completo e explicar por que cada parte importa, para que você possa repetir linhas no Excel com confiança e sem esforço.

## O que você aprenderá

* Como definir a estrutura de dados que controla a operação de repetição.  
* Como conectar um `SmartMarkerProcessor` a uma pasta de trabalho que contém uma planilha de modelo oculta.  
* Como o marcador `${Repeat:Item}` se expande em várias linhas automaticamente.  
* Dicas para lidar com casos extremos, como coleções vazias ou formatação personalizada.  

Até o final deste tutorial você será capaz de **preencher excel a partir de dados** de forma escalável, fácil de manter e que funciona com qualquer projeto .NET.

---

## Pré‑requisitos

* .NET 6.0 ou superior (o código usa recursos modernos de C#).  
* O pacote NuGet **GemBox.Spreadsheet** (a versão gratuita funciona para até 150 linhas).  
* Um arquivo de modelo Excel básico (`Template.xlsx`) com uma planilha oculta chamada `HiddenTemplate`.  
* Familiaridade com objetos C# e LINQ é útil, mas não obrigatória.

---

## Etapa 1 – Definir a estrutura de dados de repetição

Primeiro, você precisa de uma fonte de dados que o mecanismo SmartMarker possa iterar. Na maioria das aplicações reais isso virá de um banco de dados, uma API ou um arquivo CSV. Para fins de clareza, usaremos um tipo anônimo com uma única propriedade chamada `Item` que contém um array de strings.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Por que isso importa:** O marcador `${Repeat:Item}` dentro do modelo Excel procura uma propriedade chamada `Item`. Se você renomear a propriedade, atualize o marcador de forma correspondente. Esse acoplamento apertado garante que o modelo permaneça sincronizado com seu código, facilitando **preencher modelo excel** sem adivinhar nomes de colunas.

### Variações comuns

* **Objetos complexos:** Em vez de um simples array de strings, você pode fornecer uma lista de objetos (`new[] { new { Name = "A", Qty = 10 } }`). O marcador repetirá linhas e você pode referenciar `${Item.Name}` e `${Item.Qty}` na planilha.  
* **Coleções vazias:** Se `Item` estiver vazio, o SmartMarker simplesmente remove o bloco de repetição, deixando o modelo intacto—ótimo para seções opcionais.

---

## Etapa 2 – Criar o SmartMarkerProcessor para a planilha de modelo oculta

Em seguida, carregue sua pasta de trabalho e instancie um `SmartMarkerProcessor`. Aponte-o para a pasta de trabalho que contém a planilha de modelo oculta; o SmartMarker copiará essa planilha para uma visível e expandirá os marcadores de repetição.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Dica profissional:** Se você tem múltiplos modelos no mesmo arquivo, pode especificar o nome da planilha de origem ao chamar `processor.Process`. Isso ajuda quando você precisa **repetir linhas no excel** para diferentes seções de um relatório.

### Tratamento de casos extremos

* **Planilha de modelo ausente:** Envolva o carregamento em um try/catch e registre um erro claro—isso impede falhas silenciosas quando o caminho do arquivo está errado.  
* **Conjuntos de dados grandes:** Para milhares de linhas, considere transmitir a saída para um arquivo (`processor.Save`) em vez de manter tudo na memória.

---

## Etapa 3 – Aplicar os dados e expandir o marcador `${Repeat:Item}`

Agora vem a linha mágica que realmente repete as linhas. Passe o objeto criado na Etapa 1 para `processor.Process`. O SmartMarker localizará cada marcador `${Repeat:Item}`, duplicará a linha para cada elemento e substituirá os marcadores de posição pelos valores reais.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### O que você deve ver

Ao abrir `Result.xlsx`, a planilha de modelo oculta foi copiada para uma nova planilha visível (por padrão chamada `Sheet1`). A linha que continha `${Repeat:Item}` agora aparece três vezes, com as células exibindo **A**, **B** e **C** respectivamente.

| Item |
|------|
| A    |
| B    |
| C    |

Se você adicionou mais colunas como `${Item.Price}`, elas seriam preenchidas automaticamente a partir da fonte de dados.

---

## Como repetir linhas no Excel sem SmartMarker (comparação rápida)

| Abordagem                | Complexidade do Código | Manutenção | Desempenho |
|--------------------------|------------------------|------------|------------|
| Copiar‑colar manual      | Alta                   | Baixa      | Ruim       |
| Macro VBA                | Média                  | Média      | Boa        |
| **SmartMarkerProcessor** | Baixa                  | Alta       | Excelente  |

Como pode ver, usar o SmartMarker para **repetir dados no excel** oferece a separação mais limpa entre o design do modelo e a lógica de negócios. Também é independente de linguagem—conceitos semelhantes existem em bibliotecas Java, Python e JavaScript.

---

## Dicas avançadas & armadilhas comuns

### 1. Formatar as linhas repetidas

O SmartMarker copia a linha inteira—incluindo estilos de célula, bordas e formatação condicional. Se precisar de um estilo diferente para a primeira ou última linha, adicione marcadores extras como `${If:Item.IsFirst}` e use fórmulas condicionais dentro do Excel.

### 2. Lidar com grandes volumes de dados

Ao trabalhar com > 10 000 linhas, desative o cálculo automático do Excel antes do processamento:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

Reative-o após salvar para manter o desempenho ágil.

### 3. Preencher Excel a partir de dados em um banco real

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

Em seguida, use `${Repeat:Order}` no modelo para listar cada pedido. Esse padrão demonstra como é fácil **preencher excel a partir de dados** diretamente do Entity Framework.

### 4. Usar múltiplos blocos de repetição

Você pode ter vários marcadores `${Repeat:...}` na mesma planilha ou em planilhas diferentes. O SmartMarker os processa sequencialmente, portanto a ordem só importa se um bloco depender da saída de outro.

---

## Exemplo completo executável

Abaixo está um aplicativo console autônomo que você pode colar no Visual Studio e executar imediatamente. Ele demonstra as três etapas mais a gravação do arquivo.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**Saída esperada:** `Result.xlsx` contém uma planilha onde a linha com `${Repeat:Item}` aparece três vezes, mostrando A, B e C. Nenhum ajuste manual necessário.

---

## Conclusão

Agora você sabe como **repetir dados no excel** de forma eficiente usando o SmartMarkerProcessor. Definindo um objeto de dados simples, carregando um modelo de pasta de trabalho e chamando `Process`, você pode **preencher modelo excel**, **repetir linhas no excel**, e geralmente **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}