---
category: general
date: 2026-02-21
description: Crie estilo de célula em C# rapidamente. Aprenda como aplicar estilo
  a uma célula, centralizar texto na célula, definir o alinhamento da célula e dominar
  a formatação de células.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: pt
og_description: Crie estilo de célula em C# e aprenda como aplicar o estilo a uma
  célula, centralizar o texto na célula e definir o alinhamento da célula com um guia
  claro, passo a passo.
og_title: Criar estilo de célula em C# – Aplicar estilo a uma célula e centralizar
  o texto
tags:
- C#
- Aspose.Cells
- Excel automation
title: Criar estilo de célula em C# – Como aplicar estilo a uma célula e centralizar
  o texto
url: /pt/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar estilo de célula em C# – Guia completo para aplicar estilos e centralizar texto

Já precisou **criar estilo de célula** em uma planilha Excel, mas não sabia por onde começar? Você não está sozinho. Em muitos projetos de automação, a capacidade de **aplicar estilo a célula** é a diferença entre uma planilha sem graça e um relatório bem elaborado.  

Neste tutorial vamos percorrer um exemplo completo e executável que mostra **como centralizar texto** dentro de uma célula, definir o alinhamento e adicionar uma borda fina — tudo em apenas algumas linhas de C#. Ao final, você entenderá exatamente por que cada parte é importante e como ajustá‑la para seus próprios cenários.

## O que você vai aprender

- Uma compreensão clara do fluxo **create cell style** usando Aspose.Cells (ou qualquer biblioteca similar).
- O código exato que você pode copiar‑colar em um aplicativo console para **apply style to cell**.
- Visão sobre **center text in cell**, **set cell alignment** e como lidar com casos especiais como células mescladas ou formatos numéricos personalizados.
- Dicas para estender o estilo — diferentes fontes, cores de fundo ou formatação condicional.

> **Pré‑requisito:** Visual Studio 2022 (ou qualquer IDE C#) e o pacote NuGet Aspose.Cells for .NET. Nenhuma outra dependência é necessária.

---

## Etapa 1: Configurar seu projeto e importar namespaces

Antes de podermos **create cell style**, precisamos de um projeto que faça referência à biblioteca Excel.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Por que isso importa:* Importar `Aspose.Cells` nos dá acesso às classes `Workbook`, `Worksheet`, `Style` e `Border`. Se você estiver usando outra biblioteca (por exemplo, EPPlus), os nomes das classes mudam, mas o conceito permanece o mesmo.

---

## Etapa 2: Criar uma Workbook e obter a primeira célula

Agora **create cell style** obtendo primeiro uma referência à célula que queremos formatar.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Observe que usamos `Cell` em vez do genérico `var` — tipagem explícita deixa o código mais claro para iniciantes. A chamada a `PutValue` grava uma string para que possamos ver o efeito do estilo mais tarde.

---

## Etapa 3: Definir o estilo – centralizar texto, adicionar borda fina

Aqui está o coração da operação **create cell style**. Definiremos o alinhamento horizontal, uma borda fina e alguns detalhes opcionais.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Por que fazemos isso:*  
- **HorizontalAlignment** e **VerticalAlignment** juntos respondem à pergunta “**como centralizar texto** em uma célula?”.  
- Adicionar as quatro bordas garante que a célula pareça um rótulo em caixa, útil para cabeçalhos.  
- A cor de fundo não é obrigatória, mas demonstra como você pode estender o estilo posteriormente.

---

## Etapa 4: Aplicar o estilo definido à célula selecionada

Agora que o estilo existe, **apply style to cell** com uma única chamada de método.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

É isso — Aspose.Cells cuida de copiar o estilo para a coleção interna de estilos da célula. Se precisar da mesma formatação em um intervalo, pode usar `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`.

---

## Etapa 5: Salvar a Workbook e verificar o resultado

Um salvamento rápido permite abrir o arquivo no Excel e confirmar que o texto está realmente centralizado e que a borda aparece.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Saída esperada:* Ao abrir **StyledCell.xlsx**, a célula **A1** contém “Hello, styled world!” centralizado horizontal e verticalmente, cercado por uma borda cinza fina e com fundo cinza‑claro.

---

## Variações comuns & casos de borda

### 1. Centralizar texto em uma região mesclada

Se você mesclar as células **A1:C1** e ainda quiser o texto centralizado, deve aplicar o estilo à célula superior‑esquerda **após** a mesclagem:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Usando um formato numérico

Às vezes você precisa **set cell alignment** *e* exibir números com um formato específico:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

O alinhamento permanece centralizado enquanto o número aparece como `12,345.68`.

### 3. Reutilizando estilos de forma eficiente

Criar um novo `Style` para cada célula pode prejudicar o desempenho. Em vez disso, crie um objeto de estilo único e reutilize‑o em várias células ou intervalos. A classe `StyleFlag` permite aplicar somente as partes que interessam, economizando memória.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Dicas avançadas & armadilhas a observar

- **Não esqueça o alinhamento vertical** — centralizar apenas horizontalmente costuma ficar estranho, especialmente em linhas mais altas.
- **Tipos de borda**: `CellBorderType.Thin` funciona na maioria dos relatórios, mas você pode mudar para `Medium` ou `Dashed` para criar hierarquia visual.
- **Manipulação de cores**: Ao direcionar .NET Core, use `System.Drawing.Color` do pacote `System.Drawing.Common`; caso contrário, você encontrará um erro em tempo de execução.
- **Formato de salvamento**: Se precisar de compatibilidade com versões antigas do Excel, altere `SaveFormat.Xlsx` para `SaveFormat.Xls`.

---

![Exemplo de criação de estilo de célula](https://example.com/images/create-cell-style.png "Criar estilo de célula em C#")

*Texto alternativo: captura de tela mostrando uma célula com texto centralizado e borda fina criada pelo tutorial de criar estilo de célula.*

---

## Exemplo completo (pronto para copiar‑colar)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Execute este programa, abra **StyledCell.xlsx** e você verá exatamente o resultado descrito anteriormente. Sinta‑se à vontade para mudar o texto, o estilo da borda ou a cor de fundo para combinar com sua identidade visual.

---

## Conclusão

Acabamos de **create cell style** do zero, **apply style to cell**, e demonstramos **como centralizar texto** tanto horizontal quanto verticalmente. Ao dominar esses blocos de construção, você pode formatar cabeçalhos, destacar totais ou criar templates de relatórios completos sem nunca sair do C#.  

Se quiser avançar, experimente:

- **Aplicar o mesmo estilo a uma linha inteira** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).
- **Adicionar formatação condicional** para mudar o fundo com base nos valores das células.
- **Exportar para PDF** mantendo o estilo.

Lembre‑se, estilizar é tanto sobre legibilidade quanto sobre estética. Experimente, itere, e em breve suas planilhas parecerão tão profissionais quanto seu código.

*Feliz codificação!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}