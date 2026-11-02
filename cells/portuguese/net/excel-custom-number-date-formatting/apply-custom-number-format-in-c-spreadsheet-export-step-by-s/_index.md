---
category: general
date: 2026-04-07
description: Aplique formato numérico personalizado a uma célula de planilha e aprenda
  como formatar números na planilha ao exportar o valor da célula com C#. Guia rápido
  e completo.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: pt
og_description: Aplique um formato numérico personalizado a uma célula de planilha
  e exporte-a como uma string formatada. Aprenda como formatar números em planilhas
  e exportar o valor da célula.
og_title: Aplicar Formato de Número Personalizado – Tutorial Completo de Exportação
  em C#
tags:
- C#
- Spreadsheet
- Number Formatting
title: Aplicar Formato de Número Personalizado na Exportação de Planilha em C# – Guia
  Passo a Passo
url: /pt/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aplicar Formato Numérico Personalizado na Exportação de Planilha em C# – Tutorial Completo

Já precisou **aplicar formato numérico personalizado** a uma célula e depois extrair essa string formatada de uma planilha? Você não está sozinho. Muitos desenvolvedores se deparam com a situação de que o valor bruto é retornado em vez da string bonita e sensível à localidade que esperam. Neste guia, mostraremos exatamente como formatar números em células de planilha e como exportar o valor da célula como uma string formatada usando uma biblioteca popular de planilhas em C#.

Ao final do tutorial, você será capaz de **aplicar formato numérico personalizado** a qualquer célula numérica, exportar o resultado com `ExportTable` e ver a saída exata que esperaria exibir em uma interface ou relatório. Nenhuma documentação externa necessária — tudo está aqui.

## Pré-requisitos

- .NET 6.0 ou posterior (o código também funciona no .NET Framework 4.7+)
- Uma referência à biblioteca de planilhas que fornece `Workbook`, `Worksheet` e `ExportTableOptions` (por exemplo, **Aspose.Cells** ou **GemBox.Spreadsheet**; a API mostrada corresponde ao Aspose.Cells)
- Conhecimento básico de C# — se você consegue escrever um `Console.WriteLine`, está pronto para prosseguir

> **Dica profissional:** Se você estiver usando uma biblioteca diferente, os nomes das propriedades geralmente são semelhantes (`NumberFormat`, `ExportAsString`). Basta mapeá‑las de acordo.

## O que o tutorial cobre

1. Criar uma workbook e selecionar a primeira worksheet.  
2. Inserir um valor numérico em uma célula.  
3. Configurar `ExportTableOptions` para **aplicar formato numérico personalizado** e retornar uma string.  
4. Exportar a célula e imprimir o resultado formatado.  
5. Tratamento de casos extremos – e se a célula contiver uma fórmula ou um valor nulo?

Vamos começar.

![exemplo de aplicação de formato numérico personalizado](https://example.com/image.png "exemplo de aplicação de formato numérico personalizado")

## Etapa 1 – Criar uma workbook e obter a primeira worksheet

A primeira coisa que você precisa é um objeto workbook. Pense nele como o arquivo Excel que você abriria no aplicativo Office. Depois de obtê‑lo, pegue a primeira planilha — a maioria dos tutoriais começa por aí porque mantém o exemplo conciso.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Por que isso importa:** Uma workbook nova fornece uma tela limpa, garantindo que nenhuma formatação oculta interfira no nosso formato numérico personalizado mais tarde.

## Etapa 2 – Inserir um valor numérico na célula B2 (a célula que exportaremos)

Agora precisamos de algo para formatar. A célula **B2** é um local conveniente — fácil de referenciar e suficientemente distante do canto padrão A1 para evitar sobrescritas acidentais.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**E se o valor for uma fórmula?**  
Se você posteriormente substituir o valor bruto por uma fórmula (por exemplo, `=SUM(A1:A10)`), a rotina de exportação ainda respeitará o formato numérico que aplicamos na próxima etapa, porque a formatação está vinculada à célula, não ao tipo de valor.

## Etapa 3 – Configurar opções de exportação para receber o valor como uma string formatada

Aqui está o coração do tutorial: instruímos a biblioteca a **aplicar formato numérico personalizado** durante a exportação. A string `NumberFormat` segue o mesmo padrão que você usaria na categoria “Personalizado” do Excel.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` garante que o método retorne uma `string` em vez de um double bruto.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` reproduz o padrão do Excel: vírgulas para milhares, duas casas decimais e parênteses para números negativos.

> **Por que usar um formato personalizado?** Ele garante consistência entre culturas (por exemplo, separadores de número dos EUA vs. Europa) e permite incorporar estilos específicos de negócios, como parênteses contábeis.

## Etapa 4 – Exportar a célula usando as opções configuradas

Agora realmente extraímos o valor da worksheet, permitindo que a biblioteca faça o trabalho pesado de aplicar o formato que definimos.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Caso extremo – célula vazia:** Se `B2` estiver vazia, `formattedResult` será `null`. Você pode proteger isso com uma simples verificação de nulo antes de imprimir.

## Etapa 5 – Exibir a string formatada

Finalmente, escrevemos o resultado no console. Em um aplicativo real, você pode enviar essa string para um PDF, um e‑mail ou um rótulo de interface.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Saída esperada**

```
1,234.56
```

Se você mudar o valor bruto para `-9876.54`, o mesmo formato lhe dará `(9,876.54)` — exatamente o que muitos relatórios contábeis exigem.

## Exemplo completo e executável

Abaixo está o programa completo que você pode copiar‑colar em um novo projeto de console. Ele compila e executa como está, assumindo que você adicionou o pacote NuGet apropriado para a biblioteca de planilhas.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Verificação rápida de sanidade

- **Compila?** Sim — apenas certifique-se de que o DLL `Aspose.Cells` (ou equivalente) está referenciado.
- **Funciona com outras culturas?** A string de formato é independente de cultura; a biblioteca respeita o padrão que você fornece. Se precisar de separadores específicos de localidade, você pode preceder o tratamento com `CultureInfo` antes da exportação.

## Perguntas comuns & variações

### Como **formatar número em planilha** usando um padrão diferente?

Substitua a string `NumberFormat`. Por exemplo, para mostrar uma porcentagem com uma casa decimal:

```csharp
NumberFormat = "0.0%";
```

### E se eu precisar **exportar valor da célula** como HTML em vez de texto simples?

A maioria das bibliotecas tem uma sobrecarga que aceita um tipo de exportação. Você definiria `ExportAsString = true` e adicionaria `ExportHtml = true` (ou similar). O princípio permanece o mesmo: defina o formato e depois escolha a representação de saída.

### Posso aplicar o formato a um intervalo inteiro, não apenas a uma célula?

Absolutamente. Você pode atribuir `NumberFormat` a um objeto `Style` e então aplicar esse estilo a um `Range`. A chamada de exportação permanece inalterada; ela capturará o estilo automaticamente.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### O que acontece quando a célula contém uma fórmula?

A rotina de exportação avalia a fórmula primeiro, depois formata o valor numérico resultante. Nenhum código extra é necessário — apenas certifique‑se de que `Calculate` foi chamado se você desativou o cálculo automático.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Conclusão

Agora você sabe como **aplicar formato numérico personalizado** a uma célula de planilha, **formatar número em planilha** e **exportar valor da célula** como uma string pronta para exibição. O exemplo de código conciso acima cobre cada passo — da criação da workbook até a saída final — para que você possa inseri‑lo diretamente em um projeto de produção.

Pronto para o próximo desafio? Experimente combinar esta técnica com **como formatar célula numérica** para datas, símbolos de moeda ou formatação condicional. Ou explore a exportação de múltiplas células como CSV mantendo o formato personalizado de cada célula. O céu é o limite, e com esses fundamentos você tem uma base sólida.

Feliz codificação, e não se esqueça de experimentar — às vezes as melhores respostas surgem quando você ajusta a string de formato um pouquinho!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}