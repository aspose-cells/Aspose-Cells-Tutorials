---
category: general
date: 2026-02-28
description: Como criar um array no Excel usando C#. Aprenda a gerar números, avaliar
  fórmulas, criar uma pasta de trabalho do Excel e salvar o arquivo Excel em minutos.
draft: false
keywords:
- how to create array
- create excel workbook
- save excel file
- how to evaluate formula
- how to generate numbers
language: pt
og_description: Como criar um array no Excel usando C#. Este tutorial mostra como
  gerar números, avaliar uma fórmula, criar uma pasta de trabalho e salvar o arquivo.
og_title: Como criar um array no Excel com C# – Guia completo
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Como criar uma matriz no Excel com C# – Guia passo a passo
url: /pt/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Criar Array no Excel com C# – Tutorial de Programação Completo

Já se perguntou **como criar array** no Excel programaticamente com C#? Você não é o único—desenvolvedores perguntam constantemente por uma maneira rápida de gerar um bloco de números sem digitá‑los manualmente. Neste guia, percorreremos os passos exatos para **criar workbook do Excel**, inserir uma fórmula que **gera números**, **avaliar a fórmula**, e finalmente **salvar arquivo Excel** para que você possa abri‑lo no Excel e ver o resultado.

Usaremos a biblioteca Aspose.Cells porque ela nos dá controle total sobre fórmulas e cálculos sem precisar do Excel instalado. Se você preferir outra biblioteca, os conceitos permanecem os mesmos—basta trocar as chamadas da API.

## O que este Tutorial Cobre

- Configurar um projeto C# com o pacote NuGet necessário.  
- Criar um novo workbook (essa é a parte de *criar workbook do Excel*).  
- Escrever uma fórmula que constrói um array de 4 linhas × 3 colunas usando `SEQUENCE` e `WRAPCOLS`.  
- Forçar o mecanismo a **avaliar a fórmula** para que o array se materialize.  
- Salvar o workbook no disco (**salvar arquivo Excel**) e verificar a saída.  

Ao final, você terá um programa executável que produz uma planilha Excel com a seguinte aparência:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |
| 7 | 8 | 9 |
|10 |11 |12 |

![Como criar array no Excel – planilha resultante após executar o código C#](image.png)

*(O texto alternativo da imagem inclui a palavra‑chave principal “how to create array” para SEO.)*

---

## Pré‑requisitos

- .NET 6.0 SDK ou posterior (o código funciona também no .NET Framework 4.6+).  
- Visual Studio 2022 ou qualquer editor de sua preferência.  
- Pacote NuGet **Aspose.Cells** (versão de avaliação gratuita disponível).  

Nenhuma instalação extra do Excel é necessária porque o Aspose.Cells possui o motor de cálculo internamente.

## Etapa 1: Configurar o Projeto e Importar Aspose.Cells

Para começar, crie um aplicativo console e adicione a biblioteca:

```bash
dotnet new console -n ExcelArrayDemo
cd ExcelArrayDemo
dotnet add package Aspose.Cells
```

Agora abra **Program.cs** e adicione o namespace:

```csharp
using Aspose.Cells;
```

*Por que isso importa*: Importar `Aspose.Cells` nos fornece as classes `Workbook`, `Worksheet` e de cálculo que precisaremos para **criar workbook do Excel** e trabalhar com fórmulas.

## Etapa 2: Criar o Workbook e a Planilha de Destino

Precisamos de um novo objeto workbook; a primeira planilha (`Worksheets[0]`) hospedará nosso array.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = workbook.Worksheets[0];            // reference to Sheet1
```

*Explicação*: A classe `Workbook` representa o arquivo Excel completo. Por padrão, contém uma planilha, o que é perfeito para uma demonstração simples. Se precisar de mais planilhas, pode chamar `workbook.Worksheets.Add()` posteriormente.

## Etapa 3: Escrever uma Fórmula que **Gera Números** e Forma um Array

As funções de array dinâmico do Excel (`SEQUENCE` e `WRAPCOLS`) nos permitem produzir um bloco de valores com uma única fórmula. Aqui está a string exata que atribuíremos:

```csharp
// Step 3: Assign a formula that creates a 4‑row × 3‑col array
// SEQUENCE(12,1,1,1) generates numbers 1‑12; WRAPCOLS wraps them into 3 columns
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
```

*Por que isso funciona*:  
- `SEQUENCE(12,1,1,1)` retorna uma lista vertical dos números 1‑12.  
- `WRAPCOLS(...,3)` pega essa lista e a preenche em três colunas, derramando automaticamente nas linhas seguintes.  

Se você abrir o workbook no Excel **sem** avaliar a fórmula primeiro, verá apenas o texto da fórmula em `A1`. A próxima etapa força o cálculo.

## Etapa 4: **Avaliar a Fórmula** Para que o Array se Materialize

O Aspose.Cells não recalcula automaticamente as fórmulas ao gravar, portanto invocamos explicitamente o motor de cálculo:

```csharp
// Step 4: Evaluate the formula so the array is materialised in the sheet
workbook.Calculate();   // runs all pending formulas
```

*O que está acontecendo*: `Calculate()` percorre cada célula que contém uma fórmula, calcula seu resultado e grava os valores de volta. Esta é a parte **como avaliar fórmula** do nosso tutorial. Após esta chamada, as células A1:C4 contêm os números 1‑12, exatamente como um spill nativo do Excel.

## Etapa 5: **Salvar Arquivo Excel** e Verificar o Resultado

Finalmente, persistimos o workbook no disco:

```csharp
// Step 5: Save the workbook to view the result
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Abra `output.xlsx` no Excel e você verá o array 4 × 3 que geramos. Se estiver usando uma versão do Excel anterior a 365/2019, as funções de array dinâmico não serão reconhecidas—o Aspose.Cells ainda gravará os valores avaliados, portanto o arquivo continuará utilizável.

*Dica profissional*: Use `SaveFormat.Xlsx` se precisar forçar um formato específico, por exemplo, `workbook.Save(outputPath, SaveFormat.Xlsx);`.

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo. Cole‑o em **Program.cs**, execute `dotnet run`, e você obterá `output.xlsx` na pasta do projeto.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelArrayDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and grab the first worksheet
            Workbook workbook = new Workbook();               // in‑memory workbook
            Worksheet ws = workbook.Worksheets[0];            // default sheet (Sheet1)

            // 2️⃣ Drop the formula that builds a 4‑row × 3‑col array
            // SEQUENCE creates numbers 1‑12; WRAPCOLS arranges them into 3 columns
            ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";

            // 3️⃣ Force the calculation engine to evaluate the formula
            workbook.Calculate();   // now the array is "spilled" into A1:C4

            // 4️⃣ Save the file so you can open it in Excel
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);
            Console.WriteLine($"✅ Workbook saved to {outputPath}");
        }
    }
}
```

**Saída esperada** (console):

```
✅ Workbook saved to C:\Path\To\ExcelArrayDemo\output.xlsx
```

Abra o arquivo e você verá os números 1‑12 dispostos exatamente como mostrado anteriormente.

## Variações & Casos de Borda

### 1. Versões Antigas do Excel Sem Arrays Dinâmicos  
Se seu público usa Excel 2016 ou anterior, `SEQUENCE` e `WRAPCOLS` não existirão. Uma solução rápida é gerar os números em C# e escrevê‑los diretamente:

```csharp
int value = 1;
for (int row = 0; row < 4; row++)
{
    for (int col = 0; col < 3; col++)
    {
        ws.Cells[row, col].PutValue(value++);
    }
}
```

### 2. Alterando o Tamanho do Array  
Quer uma grade 5 × 5 de números 1‑25? Basta ajustar os argumentos de `SEQUENCE` e a contagem de colunas de `WRAPCOLS`:

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(25,1,1,1),5)";
```

### 3. Usando Intervalos Nomeados para Reutilização  
Você pode atribuir o intervalo derramado a um nome para fórmulas posteriores:

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
workbook.Calculate(); // ensure the range exists
int lastRow = ws.Cells.GetLastDataRow(); // should be 3 (zero‑based)
int lastCol = ws.Cells.GetLastDataColumn(); // should be 2
string address = $"A1:{CellIndexToName(lastRow, lastCol)}";
ws.Workbook.Names.Add("MyArray", ws, address);
```

## Armadilhas Comuns & Como Evitá‑las

| Armadilha | Por que Acontece | Solução |
|---|---|---|
| **Fórmula não derramando** | `Calculate()` omitido ou chamado antes de definir a fórmula. | Sempre chame `workbook.Calculate()` **depois** de atribuir a fórmula. |
| **Arquivo salvo mas vazio** | Usando `SaveFormat.Csv` acidentalmente. | Use `SaveFormat.Xlsx` ou omita o formato para que o Aspose infera. |
| **Dynamic

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}