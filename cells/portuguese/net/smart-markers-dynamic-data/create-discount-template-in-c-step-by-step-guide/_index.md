---
category: general
date: 2026-02-14
description: Crie rapidamente um modelo de desconto e aprenda como aplicar desconto
  em planilha, injetar dados no modelo e definir um prefixo variável para marcadores
  inteligentes.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: pt
og_description: Crie um modelo de desconto com C#. Aprenda a aplicar descontos em
  planilhas, injetar dados no modelo e definir um prefixo de variável para marcadores
  inteligentes.
og_title: Criar Modelo de Desconto – Guia Completo em C#
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Criar Modelo de Desconto em C# – Guia Passo a Passo
url: /pt/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Modelo de Desconto – Guia Completo em C#

Já precisou **criar modelo de desconto** para um relatório de vendas, mas não sabia como inserir os números em uma planilha automaticamente? Você não está sozinho. Neste tutorial vamos mostrar exatamente como **criar modelo de desconto**, então **aplicar desconto na planilha** nas células, **injetar dados no modelo**, e ainda **definir prefixo de variável** para seus marcadores inteligentes — tudo com código C# limpo.

Começaremos delineando o problema, depois passaremos direto para uma solução funcional que você pode copiar‑colar. Ao final, você terá um padrão reutilizável que funciona tanto para gerar faturas, listas de preços ou qualquer planilha que precise de descontos dinâmicos.

---

## O que você aprenderá

- Como projetar um modelo de planilha que reconheça descontos.
- Como configurar um `VariablePrefix` / `VariableSuffix` personalizado para que os marcadores sejam fáceis de identificar.
- Como passar um objeto anônimo (`discountData`) para o `SmartMarkerProcessor`.
- Como a fórmula resultante (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) calcula automaticamente o preço final.
- Dicas para lidar com casos extremos, como linhas sem desconto ou múltiplos níveis de desconto.

**Pré-requisitos** – um runtime .NET recente (≥ .NET 6), uma referência à biblioteca `Aspose.Cells` (ou similar) que fornece `SmartMarkerProcessor`, e um entendimento básico da sintaxe C#. Nada exótico.

---

## Etapa 1: Criar um Modelo de Desconto na sua Planilha

Primeiro, abra uma nova pasta de trabalho (ou use uma existente) e coloque um marcador de posição onde o desconto será aplicado. Pense no modelo como um arquivo Excel simples com “smart markers” que o processador substituirá.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Por que isso importa:** Ao inserir `#Discount#` dentro da fórmula, informamos ao processador exatamente onde o valor do desconto deve ficar. O `SmartMarkerProcessor` substituirá `#Discount#` pelo número que você fornecer posteriormente, deixando o restante da fórmula intacto.

---

## Etapa 2: Definir Prefixo de Variável para Smart Markers

Pronto para uso, muitas bibliotecas procuram por `${Variable}` ou `{{Variable}}`. No nosso caso queremos um marcador limpo e legível, então **definimos explicitamente o prefixo e sufixo da variável**.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Dica profissional:** Usar `#` mantém os marcadores curtos e fáceis de localizar na barra de fórmulas do Excel. Se precisar evitar conflitos com funções existentes do Excel, escolha outro par (por exemplo, `[[` e `]]`).

---

## Etapa 3: Injetar Dados no Modelo usando SmartMarkerProcessor

Agora inserimos o valor real do desconto. O processador varrerá a planilha, encontrará cada `#Discount#` e o substituirá pelo valor do objeto anônimo que passamos.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

After this call, the formula in `B2` becomes:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

When the workbook calculates, `B2` shows **90**, i.e., a 10 % discount applied to the original price of 100.

**Por que funciona:** `StartSmartMarkerProcessing` percorre cada célula, procura o token `#Discount#` e substitui pelo valor numérico. Como o token está dentro de uma instrução `IF`, a planilha ainda lida com casos em que o desconto pode ser zero.

---

## Etapa 4: Aplicar Desconto na Planilha – Verificar o Resultado

Vamos disparar o cálculo e exibir o preço final no console. Esta etapa comprova que o fluxo de **aplicar desconto na planilha** foi bem-sucedido.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Expected output**

```
Original: 100
Discounted (10%): 90
```

Se você mudar `discountData.Discount` para `0.25` e executar o processador novamente, a saída refletirá automaticamente um desconto de 25 % — sem código adicional necessário.

---

## Etapa 5: Lidando com Casos Limites & Múltiplos Descontos

### Linhas com Desconto Zero

Às vezes um produto não está em promoção. Para manter a fórmula robusta, o `IF` que você colocou anteriormente já cobre esse cenário: quando `#Discount#` é `0`, o preço original passa sem alterações.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Colunas de Desconto Múltiplas

Se precisar de descontos separados por linha, dê a cada linha seu próprio marcador, por exemplo, `#Discount1#`, `#Discount2#`, e passe uma coleção:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

O processador combina os marcadores sequencialmente, de modo que cada linha recebe o valor correto.

---

## Exemplo Completo em Funcionamento

Abaixo está o programa completo, pronto para copiar, que incorpora todas as etapas acima. Salve como `Program.cs`, adicione uma referência ao `Aspose.Cells` e execute.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

Executar isso imprime os números esperados e gera um arquivo `DiscountedPricing.xlsx` que você pode abrir no Excel para ver a fórmula já resolvida.

---

## Conclusão

Agora você sabe como **criar modelo de desconto**, **aplicar desconto na planilha**, **injetar dados no modelo**, e **definir prefixo de variável** para smart markers — tudo com algumas linhas concisas de C#. O padrão escala — basta mudar o objeto anônimo ou fornecer uma coleção para atualizações em massa, e o mesmo modelo lidará com qualquer cenário de desconto que você apresentar.

Pronto para o próximo nível? Experimente:

- Adicionar cálculos de impostos junto aos descontos.
- Buscar percentuais de desconto de um banco de dados em vez de codificá‑los diretamente.
- Usar formatação condicional para destacar linhas com descontos altos.

Essas extensões mantêm a ideia central intacta enquanto ampliam a utilidade do seu modelo de desconto.

Tem perguntas ou um caso de uso interessante? Deixe um comentário abaixo, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}