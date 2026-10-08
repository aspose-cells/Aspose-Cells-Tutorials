---
category: general
date: 2026-06-08
description: Crie uma pasta de trabalho Excel em C# passo a passo e aprenda a usar
  a função EXPAND no Excel para intervalos dinâmicos. Perfeito para desenvolvedores
  .NET.
draft: false
keywords:
- create excel workbook c#
- use expand function in excel
language: pt
og_description: Crie uma pasta de trabalho do Excel em C# com um exemplo claro e descubra
  como usar a função expand no Excel para gerar arrays dinâmicos.
og_title: Criar Pasta de Trabalho Excel C# – Guia Completo de Programação
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  headline: Create Excel Workbook C# – Full Guide with Expand Function
  type: TechArticle
- description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  name: Create Excel Workbook C# – Full Guide with Expand Function
  steps:
  - name: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
    text: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
  - name: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
    text: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
  - name: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
    text: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
  - name: '**Creates an Excel workbook C#** using Aspose.Cells.'
    text: '**Creates an Excel workbook C#** using Aspose.Cells.'
  - name: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
    text: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
  - name: Adds a cotangent formula (`COT(PI()/4)`).
    text: Adds a cotangent formula (`COT(PI()/4)`).
  - name: Saves the file and optionally auto‑fits columns.
    text: Saves the file and optionally auto‑fits columns.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells targets .NET Standard 2.0, which is compatible
      with both .NET Core and the classic Framework.
    question: Does this work with .NET Framework 4.8?
  - answer: Use `ws.Protect(ProtectionType.All, "yourPassword");` before saving.
    question: What if I need to protect the sheet?
  - answer: 'Yes—`workbook.Save(stream, SaveFormat.Xlsx);` is handy for web APIs that
      return the file as a download. --- ## TL;DR We built a **complete C# console
      app** that: 1. **Creates an Excel workbook C#** using Aspose.Cells. 2. **Uses
      the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.'
    question: Can I write the workbook directly to a `MemoryStream`?
  type: FAQPage
tags:
- csharp
- excel
- aspose-cells
- .net
title: Criar Pasta de Trabalho do Excel em C# – Guia Completo com Função Expand
url: /pt/net/excel-workbook/create-excel-workbook-c-full-guide-with-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pasta de Trabalho Excel C# – Guia Completo com Expand Function

Já se perguntou como **create Excel workbook C#** sem lutar com COM interop ou mexer com XML? Você não é o único. Em muitos projetos .NET precisamos gerar uma planilha, preenchê‑la com fórmulas e entregá‑la a usuários não técnicos. A boa notícia? Com uma biblioteca moderna como **Aspose.Cells** todo o processo é muito fácil.

Neste tutorial vamos percorrer um exemplo completo e executável que **creates an Excel workbook C#**, insere algumas fórmulas — incluindo como **use expand function in Excel** — e salva o arquivo para que você possa abri‑lo no Excel instantaneamente. Ao final você saberá não apenas *o que* digitar, mas *por que* cada linha importa, e terá um modelo que pode copiar para qualquer projeto.

## Pré‑requisitos

- .NET 6 SDK (ou qualquer versão recente do .NET) instalado.
- Uma IDE compatível com NuGet (Visual Studio, VS Code, Rider, etc.).
- O pacote NuGet **Aspose.Cells** – ele fornece as classes `Workbook` e `Worksheet` usadas no código.
- Familiaridade básica com C#; não é necessária experiência específica em Excel.

Tudo pronto? Ótimo—vamos começar.

## Etapa 1: Configurar o Projeto e Adicionar Aspose.Cells

Primeiro, crie um aplicativo console e inclua a biblioteca.

```bash
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

> **Dica profissional:** Se você estiver em uma rede corporativa, pode ser necessário configurar um proxy NuGet. O pacote Aspose.Cells é leve, então a instalação termina em segundos.

Agora abra `Program.cs`. Você verá o método `Main` padrão—substitua‑o pelo esqueleto abaixo.

```csharp
using System;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // All of our Excel logic will go here.
        }
    }
}
```

A linha `using Aspose.Cells;` traz as classes de planilha para o escopo. Se você esquecê‑la, o compilador reclamará que `Workbook` está indefinido—algo que evitaremos mais tarde.

## Etapa 2: Criar Excel Workbook C# e Acessar a Primeira Worksheet

Com o projeto pronto, podemos finalmente **create Excel workbook C#**. O construtor `Workbook` nos fornece uma pasta de trabalho nova e vazia, e o índice `Worksheets[0]` retorna a planilha padrão (nomeada “Sheet1”).

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx file in memory
Worksheet ws = workbook.Worksheets[0];            // reference to the first (default) sheet
```

Por que pegamos a primeira worksheet explicitamente? Porque muitas APIs subsequentes (como definir fórmulas) exigem um objeto `Worksheet`, não apenas o `Workbook`. Isso também torna o código mais claro para quem o ler depois.

## Etapa 3: Usar Expand Function no Excel para Preencher um Intervalo Dinâmico

Agora vem a estrela do show: **use expand function in Excel**. A função `EXPAND` (disponível a partir do Excel 365) recebe um array de origem e o preenche até o tamanho desejado. No nosso exemplo, começaremos com um array vertical de 3 linhas gerado por `SEQUENCE(3)` e o expandiremos para um bloco 5 × 5.

```csharp
// Step 3: Insert the EXPAND formula into cell A1
ws.Cells["A1"].Formula = "EXPAND(SEQUENCE(3),5,5)";
```

O que realmente acontece?

1. `SEQUENCE(3)` produz um array vertical `{1;2;3}`.
2. `EXPAND(...,5,5)` indica ao Excel para ampliar esse array para 5 linhas e 5 colunas.
3. O resultado é uma grade 5 × 5 onde as três primeiras linhas contêm os números 1‑3 repetidos nas colunas, e as duas linhas restantes ficam vazias.

Como estamos escrevendo a fórmula como uma string, o Excel a avalia *quando o arquivo é aberto*, não em tempo de execução. Isso significa que a pasta de trabalho permanece leve, e quaisquer alterações no array de origem se propagam automaticamente.

> **Caso extremo:** Se um usuário abrir a pasta de trabalho em uma versão mais antiga do Excel que não suporte `EXPAND`, a célula exibirá `#NAME?`. Para proteger contra isso, você poderia envolver a fórmula em `IFERROR`, mas em ambientes modernos é seguro confiar na função.

## Etapa 4: Adicionar uma Fórmula de Cotangente para Completar

Vamos acrescentar outra fórmula para demonstrar como é simples adicionar expressões matemáticas. Calcularemos a cotangente de π/4, que é exatamente `1`.

```csharp
// Step 4: Insert a cotangent calculation in cell B1
ws.Cells["B1"].Formula = "COT(PI()/4)";
```

A função `COT` do Excel não é tão usada quanto `SIN` ou `COS`, mas é perfeita para fluxos de trabalho trigonométricos. Quando você abrir a pasta de trabalho, a célula **B1** exibirá `1`.

## Etapa 5: Salvar a Pasta de Trabalho e Verificar o Resultado

Todo esse trabalho seria inútil se não persistíssemos o arquivo. O método `Save` grava a pasta de trabalho em memória no disco. Escolha uma pasta onde você tenha permissão de escrita e dê ao arquivo um nome amigável.

```csharp
// Step 5: Save the workbook to the output folder
string outputPath = @"./output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Execute o programa:

```bash
dotnet run
```

Você deverá ver a mensagem no console confirmando a gravação. Abra `output.xlsx` no Excel e observará:

- As células **A1:E5** preenchidas com a sequência expandida (1,2,3 nas três primeiras linhas, vazias nas linhas 4‑5).
- A célula **B1** exibindo o valor `1` da fórmula de cotangente.

![Captura de tela da pasta de trabalho Excel gerada mostrando o array expandido e o resultado da cotangente](/images/create-excel-workbook-csharp.png "create excel workbook c# example")

*Texto alternativo da imagem: create excel workbook c# – visual da planilha preenchida.*

## Etapa 6: Opcional – Auto‑Ajustar Colunas para um Visual Polido

Se você pretende distribuir o arquivo para usuários finais, um auto‑ajuste rápido deixa‑lo com aparência profissional.

```csharp
// Optional: Auto‑fit all columns in the used range
ws.AutoFitColumns(0, ws.Cells.MaxColumn);
```

Esta linha percorre cada coluna que contém dados e ajusta sua largura para a entrada mais longa. É um detalhe pequeno, mas impede o temido overflow “…###” quando os números são mais largos que a largura padrão da coluna.

## Etapa 7: Conclusão e Próximos Passos

Parabéns—você acabou de dominar como **create excel workbook c#** do zero e aprendeu a **use expand function in excel** para gerar arrays dinâmicos. O código foi intencionalmente minimalista para que você possa copiar‑colar em qualquer projeto, mas os conceitos são escaláveis:

- **Fontes de dados dinâmicas:** Substitua `SEQUENCE(3)` por uma referência a outro intervalo ou a uma tabela nomeada.
- **Formatação condicional:** Use `ws.Cells["A1:E5"].Style` para adicionar cores com base nos valores.
- **Gráficos e imagens:** Aspose.Cells pode incorporar gráficos, imagens e até tabelas dinâmicas.

Sinta‑se à vontade para experimentar—troque as dimensões do `EXPAND`, experimente `FILTER` ou `SORT`, ou encadeie várias fórmulas. A biblioteca lida com tudo isso sem que você precise tocar no formato de baixo nível OpenXML.

---

### Perguntas Frequentes

**Q: Isso funciona com .NET Framework 4.8?**  
A: Absolutamente. Aspose.Cells tem como alvo .NET Standard 2.0, que é compatível tanto com .NET Core quanto com o Framework clássico.

**Q: E se eu precisar proteger a planilha?**  
A: Use `ws.Protect(ProtectionType.All, "yourPassword");` antes de salvar.

**Q: Posso gravar a pasta de trabalho diretamente em um `MemoryStream`?**  
A: Sim—`workbook.Save(stream, SaveFormat.Xlsx);` é útil para APIs web que retornam o arquivo como download.

## TL;DR

Construímos um **aplicativo console C# completo** que:

1. **Creates an Excel workbook C#** usando Aspose.Cells.  
2. **Uses the EXPAND function in Excel** para transformar um array de 3 linhas em um bloco 5 × 5.  
3. Adiciona uma fórmula de cotangente (`COT(PI()/4)`).  
4. Salva o arquivo e, opcionalmente, auto‑ajusta as colunas.

Agora você tem uma base sólida para qualquer tarefa de automação que envolva gerar arquivos Excel a partir do .NET. Boa codificação, e que suas planilhas estejam sempre livres de erros!

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Criar Intervalos Nomeados com Escopo de Pasta de Trabalho no Excel Usando Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Como Criar e Usar Intervalos de União no Excel com Aspose.Cells .NET (Guia C#)](/cells/english/net/range-management/excel-union-range-aspose-cells-net/)
- [Criar Pasta de Trabalho Excel com Gráficos Usando Aspose.Cells .NET | Guia Passo a Passo](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}