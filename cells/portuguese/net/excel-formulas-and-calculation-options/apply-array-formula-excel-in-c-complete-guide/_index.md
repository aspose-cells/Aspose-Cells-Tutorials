---
category: general
date: 2026-06-24
description: Aplicar fórmula de matriz no Excel usando C#. Aprenda como salvar arquivo
  Excel em C# e criar uma pasta de trabalho Excel em C# com a função Expand e gerar
  arquivo Excel com fórmulas.
draft: false
keywords:
- apply array formula excel
- save excel file c#
- create excel workbook c#
- use expand function excel
- generate excel file with formulas
language: pt
og_description: Aplique fórmulas de matriz do Excel em C# e aprenda a salvar arquivos
  do Excel em C# rapidamente. Este guia mostra como criar uma pasta de trabalho do
  Excel em C# e usar a função expand do Excel.
og_title: Aplicar Fórmula de Matriz do Excel em C# – Guia Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Apply array formula excel using C#. Learn how to save excel file c#
    and create excel workbook c# with the Expand function and generate excel file
    with formulas.
  headline: Apply Array Formula Excel in C# – Complete Guide
  type: TechArticle
- description: Apply array formula excel using C#. Learn how to save excel file c#
    and create excel workbook c# with the Expand function and generate excel file
    with formulas.
  name: Apply Array Formula Excel in C# – Complete Guide
  steps:
  - name: What if the target folder doesn’t exist?
    text: '`Workbook.Save` will throw a `DirectoryNotFoundException`. A quick fix
      is to ensure the directory exists before calling `Save`:'
  - name: Can I apply the array formula to a range other than A1?
    text: 'Absolutely. Just change the cell address:'
  - name: Does the calculation engine respect Excel’s precision settings?
    text: Aspose.Cells follows IEEE‑754 double‑precision arithmetic, which matches
      Excel’s default. If you need custom precision, you can tweak the `CalculationOptions`
      object before calling `CalculateFormula`.
  - name: What about older Excel versions that don’t support `EXPAND`?
    text: 'If you need backward compatibility, replace `EXPAND` with a combination
      of `INDEX` and `SEQUENCE` or simply write the values directly via C# loops.
      The library also lets you write values without formulas:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Aplicar Fórmula de Matriz do Excel em C# – Guia Completo
url: /pt/net/excel-formulas-and-calculation-options/apply-array-formula-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aplicar Fórmula de Matriz no Excel em C# – Tutorial Completo de Programação

Já precisou **aplicar fórmula de matriz excel** mas não sabia como fazer isso a partir do código C#? Você não está sozinho. Muitos desenvolvedores se deparam com dificuldades ao tentar gerar uma planilha que contém fórmulas de matriz dinâmicas como `EXPAND` ou `COT`.  

Neste tutorial vamos percorrer um exemplo prático que **cria uma pasta de trabalho excel c#**, insere uma fórmula de matriz, usa a função `EXPAND` e, finalmente, **salva arquivo excel c#** para que você possa abri‑lo no Excel e ver os resultados. Ao final, você também saberá como **gerar arquivo excel com fórmulas** de forma pronta para produção.

> **Dica de especialista:** A abordagem mostrada aqui funciona nas versões mais recentes do Excel que suportam funções de matriz dinâmica (Office 365, Excel 2021+). Se precisar de compatibilidade retroativa, será necessário recorrer a técnicas de fórmula mais antigas.

![Screenshot of Excel showing the array formula result – apply array formula excel](apply-array-formula-excel.png)

*(Texto alternativo da imagem: aplicar fórmula de matriz excel – captura de tela da pasta de trabalho Excel com fórmula de matriz dinâmica)*

## O que você vai precisar

- **.NET 6+** (ou qualquer runtime .NET recente) – o código compila tanto com .NET Core quanto com .NET Framework.  
- **Aspose.Cells for .NET** (versão de avaliação gratuita ou licenciada). Esta biblioteca permite manipular arquivos Excel sem precisar do Excel instalado.  
- Uma IDE favorita (Visual Studio, Rider, VS Code).  
- Conhecimento básico de C# – nada sofisticado, apenas o suficiente para acompanhar o código.

Se já tem tudo isso, ótimo – vamos começar.

---

## Etapa 1 – Aplicar Fórmula de Matriz Excel: Criar a Pasta de Trabalho

A primeira coisa que fazemos é **criar pasta de trabalho excel c#** usando Aspose.Cells. Isso nos fornece um objeto de workbook limpo que podemos preencher posteriormente com fórmulas.

```csharp
using System;
using Aspose.Cells;

namespace ExcelArrayFormulaDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a new workbook
            Workbook workbook = new Workbook();

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

> **Por que isso importa:** Instanciar um objeto `Workbook` é o ponto de entrada para qualquer automação do Excel. Ele representa o arquivo inteiro, e a primeira planilha é um local conveniente para começar a testar fórmulas.

---

## Etapa 2 – Usar Função Expand Excel para Popular uma Matriz

Agora nós **usamos a função expand excel** para transformar uma matriz estática simples `{1,2,3}` em um derramamento vertical de cinco linhas. A função `EXPAND` faz parte do motor de matrizes dinâmicas do Excel e preenche o intervalo automaticamente.

```csharp
            // Set a formula that expands an array into 5 rows, 1 column
            // The formula will spill into A1:A5
            worksheet.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";
```

> **Explicação:**  
> - `{1,2,3}` é uma constante de matriz literal.  
> - `5` indica ao Excel que deve retornar cinco linhas, enquanto `1` mantém em uma única coluna.  
> - Quando você abrir o arquivo, as células de A1 a A5 mostrarão `1, 2, 3, 0, 0` (as linhas extras são preenchidas com zeros).

---

## Etapa 3 – Adicionar uma Fórmula Matemática Clássica (Cotangente)

Matrizes dinâmicas não são as únicas fórmulas que você pode incorporar. Vamos também **gerar arquivo excel com fórmulas** que calculam a cotangente de π/4. Isso demonstra que fórmulas regulares funcionam lado a lado com as dinâmicas.

```csharp
            // Set a formula that calculates the cotangent of π/4 (≈1)
            worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

> **Por que incluir isso?** Mostra que você pode misturar funções legadas e novas sem nenhuma configuração extra. A função `COT` está disponível em todas as versões modernas do Excel.

---

## Etapa 4 – Recalcular Todas as Fórmulas na Pasta de Trabalho

Aspose.Cells não avalia automaticamente as fórmulas quando você as define. É preciso instruir o motor a **recalcular** antes de salvar, caso contrário o arquivo conterá apenas as fórmulas brutas.

```csharp
            // Force calculation of all formulas
            workbook.CalculateFormula();
```

> **O que acontece nos bastidores?** A biblioteca analisa cada fórmula, constrói uma árvore de expressão e a avalia usando seu próprio motor de cálculo. Essa etapa é crucial se você quiser que o arquivo gerado mostre os valores imediatamente ao ser aberto.

---

## Etapa 5 – Salvar Arquivo Excel C# – Persistir os Resultados

Por fim, nós **salvamos arquivo excel c#** no disco. Você pode escolher qualquer pasta; apenas certifique‑se de que a aplicação tenha permissão de escrita.

```csharp
            // Define the output path (adjust as needed)
            string outputPath = @"C:\Temp\output.xlsx";

            // Save the workbook – this writes the calculated values into the file
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Ao abrir `output.xlsx` no Excel você deverá ver:

| A   | B |
|-----|---|
| 1   | 1 |
| 2   |   |
| 3   |   |
| 0   |   |
| 0   |   |

- A coluna **A** mostra a matriz derramada produzida por `EXPAND`.  
- A célula **B1** exibe `1`, o resultado de `COT(π/4)`.

Esse é o fluxo completo de **gerar arquivo excel com fórmulas**.

---

## Perguntas Frequentes & Casos de Borda

### E se a pasta de destino não existir?

`Workbook.Save` lançará uma `DirectoryNotFoundException`. Uma solução rápida é garantir que o diretório exista antes de chamar `Save`:

```csharp
if (!System.IO.Directory.Exists(System.IO.Path.GetDirectoryName(outputPath)))
{
    System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath));
}
```

### Posso aplicar a fórmula de matriz a um intervalo diferente de A1?

Com certeza. Basta mudar o endereço da célula:

```csharp
worksheet.Cells["D4"].Formula = "=EXPAND({10,20,30},3,1)";
```

O derramamento começará em D4 e preencherá D4:D6.

### O motor de cálculo respeita as configurações de precisão do Excel?

Aspose.Cells segue a aritmética de ponto flutuante de dupla precisão IEEE‑754, que corresponde ao padrão do Excel. Se precisar de precisão personalizada, ajuste o objeto `CalculationOptions` antes de chamar `CalculateFormula`.

```csharp
var options = new CalculationOptions { PrecisionAsDisplayed = true };
workbook.CalculateFormula(options);
```

### E quanto às versões antigas do Excel que não suportam `EXPAND`?

Se precisar de compatibilidade retroativa, substitua `EXPAND` por uma combinação de `INDEX` e `SEQUENCE` ou simplesmente escreva os valores diretamente via loops C#. A biblioteca também permite gravar valores sem fórmulas:

```csharp
object[] values = { 1, 2, 3, 0, 0 };
for (int i = 0; i < values.Length; i++)
{
    worksheet.Cells[i, 0].PutValue(values[i]); // Column A
}
```

---

## Dicas de Especialista para Trabalhar com Fórmulas em C#

- **Cálculos em lote:** Se estiver inserindo centenas de fórmulas, chame `CalculateFormula` uma única vez após todas as inserções. Isso reduz a sobrecarga de CPU.  
- **Evite funções voláteis:** Funções como `NOW()` recalculam a cada abertura, o que pode deixar pastas de trabalho grandes mais lentas.  
- **Use intervalos nomeados:** Eles tornam as fórmulas mais fáceis de ler e manter, especialmente quando você as gera programaticamente.  
- **Mantenha a biblioteca atualizada:** As versões mais recentes do Aspose.Cells costumam incluir otimizações de desempenho e suporte a novas funções do Excel (por exemplo, `XLOOKUP`, `FILTER`).  

---

## Recapitulação – O que Cobremos

Começamos **aplicando fórmula de matriz excel** a uma workbook nova, depois **usamos a função expand excel** para derramar uma matriz estática em cinco linhas. Em seguida, adicionamos um cálculo clássico `COT`, forçamos a recalculação completa e, por fim, **salvamos arquivo excel c#** no disco. O resultado é uma planilha pronta para abrir que demonstra tanto o comportamento de matrizes dinâmicas quanto a avaliação de fórmulas regulares – uma base sólida para qualquer projeto de **gerar arquivo excel com fórmulas**.

---

## Próximos Passos

- **Estilizar a saída:** Aplique fontes, bordas ou formatação condicional via Aspose.Cells para deixar a planilha mais polida.  
- **Adicionar gráficos:** Use a API de gráficos da biblioteca para visualizar os dados da matriz automaticamente.  
- **Exportar para outros formatos:** A mesma workbook pode ser salva como CSV, PDF ou HTML com uma única chamada (`workbook.Save("output.pdf")`).  
- **Integrar ao ASP.NET:** Sirva o arquivo gerado diretamente aos usuários através de um endpoint de API web.

Sinta‑se à vontade para experimentar – troque `EXPAND` por `SEQUENCE`, teste derramamentos multi‑coluna ou gere dashboards completos programaticamente. O céu é o limite quando você sabe como **aplicar fórmula de matriz excel** a partir do C#.

Boa codificação! 🚀


## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Create Save Excel File Aspose Cells Dotnet](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [How to Save Specific Pages of an Excel File as PDF Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}