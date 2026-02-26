---
category: general
date: 2026-02-23
description: Crie uma nova pasta de trabalho programaticamente em C# e adicione uma
  fórmula a uma célula. Aprenda a usar o EXPAND e, em seguida, salve a pasta de trabalho
  do Excel sem esforço.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: pt
og_description: Crie uma nova pasta de trabalho programaticamente em C#. Adicione
  uma fórmula a uma célula, aprenda a usar o EXPAND e salve a pasta de trabalho do
  Excel em segundos.
og_title: Criar nova pasta de trabalho em C# – adicionar fórmula e salvar arquivo
  Excel
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Criar Nova Pasta de Trabalho em C# – Adicionar Fórmula e Salvar Arquivo Excel
url: /pt/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Nova Pasta de Trabalho em C# – Adicionar Fórmula e Salvar Arquivo Excel

Já se perguntou como **create new workbook** objetos a partir do código sem nunca abrir o Excel? Você não está sozinho. Muitos desenvolvedores esbarram em um obstáculo quando precisam gerar uma planilha na hora — talvez para um relatório, uma exportação ou um despejo rápido de dados.  

A boa notícia? Neste guia você verá exatamente como **create new workbook**, inserir um **add formula to cell**, e então **save excel workbook** com apenas algumas linhas de C#. Também vamos explorar **how to use expand** para que você possa gerar arrays dinâmicos sem copiar manualmente. Ao final, você será capaz de **create excel file programmatically** e enviá‑lo para usuários ou serviços downstream.

## Pré‑requisitos

- .NET 6.0 ou posterior (qualquer runtime .NET recente funciona)  
- Aspose.Cells para .NET (versão de avaliação ou licenciada) – esta biblioteca fornece as classes `Workbook` e `Worksheet` usadas abaixo.  
- Noções básicas de sintaxe C# — não é necessário conhecimento avançado de Excel.  

Se já tem tudo isso, ótimo! Caso contrário, obtenha o Aspose.Cells via NuGet (`Install-Package Aspose.Cells`) e você estará pronto para começar.

---

## Etapa 1: Create New Workbook – A Base

Para iniciar, precisamos instanciar um novo objeto workbook. Pense nisso como abrir um arquivo Excel totalmente novo e vazio.

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Por que isso importa:** A classe `Workbook` é o ponto de entrada para qualquer manipulação de Excel. Ao criar uma nova instância, alocamos memória para planilhas, estilos e fórmulas — tudo sem tocar no sistema de arquivos.

---

## Etapa 2: Acessar a Primeira Worksheet

Todo workbook novo vem com uma worksheet padrão (nomeada *Sheet1*). Vamos obtê‑la para que possamos inserir dados e fórmulas.

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Dica de especialista:** Se precisar de várias planilhas, basta chamar `workbook.Worksheets.Add("MySheet")` e trabalhar com o objeto `Worksheet` retornado.

---

## Etapa 3: Add Formula to Cell – Usando EXPAND

Agora vem a parte divertida: inserir uma fórmula. A função `EXPAND` é perfeita quando você quer transformar um array estático em um intervalo maior e preenchido automaticamente.

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### Como a Fórmula EXPAND Funciona

| Argumento | Significado |
|-----------|-------------|
| `{1,2,3}` | O array de origem (uma lista horizontal de três números) |
| `5`       | Número desejado de linhas no resultado |
| `1`       | Número desejado de colunas (mantenha 1 para ficar vertical) |

Quando o Excel avalia isso, ele produz uma lista **vertical**:

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **Por que usar EXPAND?** Ela elimina a necessidade de cópias manuais ou loops VBA. A função remodela os dados dinamicamente, tornando suas planilhas mais robustas e fáceis de manter.

---

## Etapa 4: Save Excel Workbook – Persistir o Resultado

Com a fórmula no lugar, o passo final é gravar o workbook no disco. Você pode escolher qualquer pasta onde tenha permissão de escrita.

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **O que você verá:** Abra `ExpandFormula.xlsx` no Excel, e a célula `A1` exibirá o array expandido. A própria fórmula permanece na célula, de modo que, se você editar o array de origem, o resultado será atualizado automaticamente.

---

## Opcional: Verificar a Saída Programaticamente

Se preferir não abrir o Excel manualmente, você pode ler de volta os valores para confirmar que correspondem ao esperado.

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

Executar o código acima imprimirá:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## Perguntas Frequentes & Casos de Borda

| Pergunta | Resposta |
|----------|----------|
| **Can I use EXPAND with a larger source array?** | Absolutamente. Basta mudar `{1,2,3}` para qualquer constante ou intervalo de células, por exemplo, `EXPAND(A1:C1,10,1)`. |
| **What if I need a horizontal result?** | Troque os argumentos de linha/coluna: `EXPAND({1,2,3},1,5)` produzirá uma extensão de 1 linha por 5 colunas. |
| **Will this work on older Excel versions?** | `EXPAND` está disponível a partir do Excel 365/2021. Para versões mais antigas, seria necessário simular o array com `INDEX`/`SEQUENCE`. |
| **Do I need to call `workbook.CalculateFormula()`?** | Não. O Aspose.Cells avalia automaticamente as fórmulas ao salvar, de modo que os valores aparecem imediatamente. |
| **How to add more than one sheet before saving?** | Chame `workbook.Worksheets.Add("SecondSheet")` e repita as etapas de manipulação de células na nova worksheet. |

---

## Exemplo Completo

A seguir está o programa completo, pronto para ser executado. Copie‑e cole em um aplicativo console, ajuste o caminho de saída e pressione **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Saída esperada no console:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

Abra o arquivo gerado e você verá os mesmos números preenchidos na coluna **A**.

---

## Resumo Visual

![Exemplo de criação de nova pasta de trabalho](create-new-workbook.png "Captura de tela mostrando uma nova pasta de trabalho criada com create new workbook em C#")

*A imagem ilustra a pasta de trabalho recém‑gerada com o resultado do EXPAND.*

---

## Conclusão

Agora você sabe como **create new workbook**, **add formula to cell** e **save excel workbook** usando C#. Ao dominar **how to use expand**, pode gerar arrays dinâmicos sem esforço manual, e todo o processo permite que você **create excel file programmatically** para qualquer cenário de automação.

Qual o próximo passo? Experimente trocar o array constante por uma referência de intervalo, teste diferentes dimensões do `EXPAND` ou encadeie múltiplas fórmulas entre planilhas. O mesmo padrão funciona para gráficos, estilos e até tabelas dinâmicas — continue explorando.

Se encontrou algum problema, deixe um comentário abaixo. Feliz codificação e aproveite o poder do Excel programático!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}