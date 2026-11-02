---
category: general
date: 2026-07-03
description: Escreva fórmula de matriz em C# para criar um array de 2 colunas, calcular
  a célula do Excel e distribuir a lista em colunas. Siga este exemplo passo a passo
  usando Aspose.Cells.
draft: false
keywords:
- write array formula
- calculate excel cell
- wrap list into columns
- create 2‑column array
- generate excel array
language: pt
og_description: Escreva uma fórmula de matriz em C# para criar um array de 2 colunas,
  calcular a célula do Excel e organizar a lista em colunas. Aprenda todo o processo
  com código executável.
og_title: Escreva fórmula de matriz em C# – Guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Write array formula in C# to create a 2‑column array, calculate Excel
    cell and wrap list into columns. Follow this step‑by‑step example using Aspose.Cells.
  headline: Write array formula in C# – Complete Programming Guide
  type: TechArticle
- description: Write array formula in C# to create a 2‑column array, calculate Excel
    cell and wrap list into columns. Follow this step‑by‑step example using Aspose.Cells.
  name: Write array formula in C# – Complete Programming Guide
  steps:
  - name: What if I need a dynamic range rather than a hard‑coded list?
    text: 'You can construct the list part of the formula at runtime:'
  - name: Does `WRAPCOLS` work on older Excel versions?
    text: '`WRAPCOLS` is available starting with Excel 365/2019. If you target older
      versions, you’ll need to simulate the behavior with `INDEX` and `MOD` tricks,
      but that quickly becomes messy. Using Aspose.Cells lets you keep the modern
      formula and still produce a compatible file for most users.'
  - name: Can I write the formula to a range instead of a single cell?
    text: 'Yes—assign the same formula to the top‑left cell of the range, then call
      `Calculate()` on the range object:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- automation
title: Escreva fórmula de matriz em C# – Guia completo de programação
url: /pt/net/formulas-functions/write-array-formula-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Escreva fórmula de matriz em C# – Guia de Programação Completo

Já precisou **escrever fórmula de matriz** em C# mas não sabia como fazer o Excel gerar uma lista bem formatada? Você não está sozinho. Muitos desenvolvedores encontram dificuldades ao tentar *gerar matriz Excel* sem abrir a interface. Neste tutorial vamos percorrer um exemplo conciso, de ponta a ponta, que **escreve uma fórmula de matriz**, **calcula célula Excel**, e **organiza lista em colunas** para **criar uma matriz de 2 colunas** que você pode salvar e inspecionar.

Usaremos a popular biblioteca Aspose.Cells porque permite manipular pastas de trabalho inteiramente em código. Ao final, você terá um trecho pronto‑para‑executar, uma explicação clara de cada linha e ideias para expandir o padrão para conjuntos de dados maiores. Sem enrolação — apenas as partes práticas que você pode copiar‑colar hoje.

## O que você precisará

* .NET 6.0 ou posterior (o código também funciona no .NET Core)  
* Uma referência ao **Aspose.Cells** (você pode obtê‑la no NuGet: `Install-Package Aspose.Cells`)  
* Uma pasta onde você possa ler/gravar arquivos Excel – a chamaremos de `YOUR_DIRECTORY` nos exemplos  

É isso. Sem interop adicional do Excel, sem COM, apenas código gerenciado puro.

![Exemplo de escrita de fórmula de matriz em C#](write-array-formula.png "Captura de tela mostrando a matriz de 2 colunas gerada no Excel – escrever fórmula de matriz em C#")

## Etapa 1: Escrever fórmula de matriz com Aspose.Cells

A primeira coisa que devemos fazer é **escrever fórmula de matriz** em uma célula. Na sintaxe do Excel, a função `WRAPCOLS` recebe uma lista plana e a remodela em uma matriz. Veja como fazer isso programaticamente:

```csharp
// Step 1: Load the workbook (or create a new one)
var workbook = new Aspose.Cells.Workbook(); // creates a blank workbook

// Access the first worksheet – this is where we’ll work
var worksheet = workbook.Worksheets[0];

// Write array formula into A1 that wraps {1,2,3,4} into 2 columns
worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";
```

**Por que isso importa:** A propriedade `Formula` armazena a string literal da fórmula do Excel. Ao usar `WRAPCOLS` indicamos ao Excel que pegue a matriz linear `{1,2,3,4}` e a organize em um layout de 2 colunas, efetivamente **criando uma matriz de 2 colunas**. A própria fórmula é uma *fórmula de matriz* — você notará as chaves ao redor dos números.

## Etapa 2: Calcular célula Excel para que a fórmula seja avaliada

Escrever a fórmula não basta; precisamos **calcular célula Excel** para que o motor a avalie. Aspose.Cells não recalcula automaticamente a menos que você solicite:

```csharp
// Step 2: Force calculation of the cell containing the array formula
worksheet.Cells["A1"].Calculate();
```

**Por que esta etapa é crucial:** Sem chamar `Calculate()`, a célula permanece em estado “pendente” e a pasta de trabalho que você salvará conterá a fórmula bruta, não os valores calculados. Ao recalcular explicitamente, garantimos que a matriz de saída seja materializada no arquivo.

## Etapa 3: Organizar lista em colunas – veja o resultado

Neste ponto a planilha contém um bloco de 2 colunas começando em `A1`. Se você abrir o arquivo verá:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |

Essa é a representação visual de **organizar lista em colunas** usando a função `WRAPCOLS`. Se preferir um número diferente de colunas, basta alterar o segundo argumento:

```csharp
worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)"; // creates 3 columns
worksheet.Cells["A1"].Calculate();
```

Agora a matriz fica assim:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

**Dica profissional:** Ao lidar com conjuntos de dados maiores, construa a string da lista dinamicamente (por exemplo, usando `string.Join(",", myNumbers)`) para evitar valores codificados.

## Etapa 4: Salvar a pasta de trabalho e verificar a saída

Finalmente, persistimos a pasta de trabalho no disco para que você possa abri‑la no Excel e confirmar o trabalho de **gerar matriz excel**:

```csharp
// Step 4: Save the workbook – you’ll see the calculated array in Excel
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Abra `output.xlsx` e você verá a matriz de 2 colunas exatamente como descrito. Se você mudar a fórmula e recalcular, o arquivo salvo será atualizado automaticamente — sem necessidade de atualização manual.

## Exemplo Completo e Executável

Juntando tudo, aqui está o programa completo que você pode inserir em um aplicativo console:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load (or create) a workbook
        var workbook = new Workbook(); // blank workbook

        // 2️⃣ Access the first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3️⃣ Write the array formula that wraps a list into 2 columns
        worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";

        // 4️⃣ Calculate the cell so the formula is evaluated
        worksheet.Cells["A1"].Calculate();

        // 5️⃣ (Optional) Save the workbook to view the result
        workbook.Save("YOUR_DIRECTORY/output.xlsx");

        Console.WriteLine("Workbook saved – check output.xlsx to see the 2‑column array.");
    }
}
```

**Saída esperada:** Quando você abrir `output.xlsx`, as células `A1:B2` contêm os números 1‑4 organizados em duas colunas. O console exibe uma confirmação amigável.

## Casos de Borda e Perguntas Frequentes

### E se eu precisar de um intervalo dinâmico em vez de uma lista codificada?

Você pode construir a parte da lista da fórmula em tempo de execução:

```csharp
int[] values = { 10, 20, 30, 40, 50, 60 };
string list = "{" + string.Join(",", values) + "}";
worksheet.Cells["A1"].Formula = $"=WRAPCOLS({list},3)";
worksheet.Cells["A1"].Calculate();
```

Isso ainda **gera matriz excel** de saída, mas agora os dados de origem vêm da lógica da sua aplicação.

### O `WRAPCOLS` funciona em versões mais antigas do Excel?

`WRAPCOLS` está disponível a partir do Excel 365/2019. Se você direcionar versões mais antigas, precisará simular o comportamento com truques `INDEX` e `MOD`, mas isso rapidamente se torna complicado. Usar Aspose.Cells permite manter a fórmula moderna e ainda produzir um arquivo compatível para a maioria dos usuários.

### Posso escrever a fórmula em um intervalo em vez de uma única célula?

Sim — atribua a mesma fórmula à célula superior‑esquerda do intervalo e, em seguida, chame `Calculate()` no objeto de intervalo:

```csharp
var range = worksheet.Cells.CreateRange("A1", 2, 2); // 2x2 block
range.Formula = "=WRAPCOLS({1,2,3,4},2)";
range.Calculate();
```

O resultado é idêntico, mas você tem mais controle sobre onde a matriz reside.

## Considerações de Performance

Quando você **calcula célula Excel** para muitas fórmulas, Aspose.Cells pode agrupar cálculos para ganhar velocidade. Se estiver gerando milhares de matrizes, chame `workbook.CalculateFormula()` uma única vez após todas as fórmulas serem definidas, em vez de `Calculate()` em cada célula. Isso reduz a sobrecarga drasticamente.

## Próximos Passos

Agora que você sabe como **escrever fórmula de matriz**, **calcular célula Excel**, e **organizar lista em colunas** para **criar uma matriz de 2 colunas**, você pode explorar:

* **Gerar matriz Excel** para relatórios de múltiplas planilhas  
* Aplicar estilos (bordas, formatos numéricos) ao intervalo resultante  
* Exportar a pasta de trabalho para PDF ou CSV para processamento posterior  
* Combinar com regras de validação de dados para criar planilhas interativas  

Cada um desses se baseia na técnica central que abordamos, permitindo automatizar fluxos de trabalho complexos do Excel inteiramente a partir do C#.

---

**Em resumo**, este guia mostrou como **escrever fórmula de matriz** em C# usando Aspose.Cells, forçar a etapa de **calcular célula Excel**, e **organizar lista em colunas** para **criar uma matriz de 2 colunas** que você pode **gerar matriz excel** em arquivos. O código está totalmente executável, as explicações cobrem o *porquê* de cada linha, e você tem dicas para escalar e lidar com casos de borda.

Experimente, ajuste a contagem de colunas, insira seus próprios dados e deixe o Excel fazer o trabalho pesado por você. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Domine Fórmulas de Matriz Excel com Aspose.Cells Java: Otimize Cálculos e Formatação](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)
- [Criar Objetos de Lista Excel usando Aspose.Cells .NET: Um Guia Passo a Passo](/cells/english/net/tables-structured-references/create-excel-list-objects-aspose-cells-net/)
- [Importar Matriz Multidimensional Excel Aspose Cells Java](/cells/german/java/import-export/import-multi-dimensional-array-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}