---
category: general
date: 2026-06-05
description: Crie uma pasta de trabalho do Excel em C# rapidamente e aprenda a definir
  o formato numérico da célula, exportar a célula do Excel e converter o valor da
  célula para string com precisão de duas casas decimais.
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: pt
og_description: Criar uma pasta de trabalho do Excel em C# e dominar a configuração
  do formato numérico das células, exportar a célula do Excel como string e formatar
  números com duas casas decimais.
og_title: Criar Pasta de Trabalho Excel em C# – Guia Completo Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Criar Pasta de Trabalho do Excel em C# – Guia Completo de Programação
url: /pt/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pasta de Trabalho Excel em C# – Guia Completo de Programação

Já se perguntou como **criar pasta de trabalho Excel** em C# sem lutar com COM interop ou truques bagunçados de CSV? Você não está sozinho. Muitos desenvolvedores precisam de uma maneira limpa, nativa do .NET, para gerar um arquivo .xlsx, inserir um número em uma célula e, em seguida, exportar esse valor como uma string formatada adequadamente.  

Neste tutorial vamos percorrer exatamente isso — começando de uma pasta de trabalho vazia, definindo o formato numérico da célula, formatando o número com duas casas decimais e, por fim, aprendendo **como exportar célula Excel** como string. Ao final, você também verá como **converter valor da célula para string** sem perder precisão.

> **Pro tip:** A abordagem abaixo usa a biblioteca **Aspose.Cells for .NET**, que é uma API testada em produção e de nível comercial. Se você procura uma alternativa gratuita, EPPlus ou ClosedXML funcionam de forma semelhante, mas os trechos de código serão ligeiramente diferentes.

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- .NET 6.0 SDK (ou qualquer versão recente do .NET) instalado.
- Visual Studio 2022 ou VS Code com a extensão C#.
- O pacote NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).

Nenhuma outra dependência é necessária — todo o resto está dentro da biblioteca.

## Etapa 1: Instalar Aspose.Cells e Configurar o Projeto

Abra seu terminal (ou o Package Manager Console) e execute:

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

Isso cria um novo aplicativo console chamado `ExcelDemo` e adiciona o assembly `Aspose.Cells`.  

Por que essa etapa importa: sem a biblioteca, você não pode **criar pasta de trabalho Excel** nem manipular células de forma segura e tipada.

## Etapa 2: Criar a Pasta de Trabalho e Obter a Primeira Planilha

Agora abra `Program.cs` e substitua o código padrão pelo trecho abaixo. Ele mostra a primeira coisa que você faz ao **criar pasta de trabalho Excel** — instanciar a classe `Workbook` e obter uma referência à planilha padrão.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **Por quê?** O objeto `Workbook` é a representação em memória de um arquivo Excel. Por padrão ele contém uma planilha, que acessamos via índice zero‑based.

## Etapa 3: Inserir um Valor Numérico em uma Célula Específica

Vamos direcionar a linha 5, coluna 2 (índices zero‑based) e inserir um número decimal. Isso demonstra **formatar número com duas casas decimais** mais adiante.

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

O método `PutValue` armazena o double bruto. Neste ponto, o Excel exibiria a precisão total, a menos que apliquemos um formato.

## Etapa 4: Definir o Formato Numérico da Célula (Duas Casas Decimais)

Aqui é onde **definimos o formato numérico da célula**. Usaremos o objeto `Style` para definir um formato numérico personalizado `"0.00"` — exatamente duas casas decimais.

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

Por que usar um estilo ao invés de conversão para string? Manter a célula como tipo numérico preserva sua natureza calculável (você ainda pode somar, fazer média etc.) enquanto exibe exatamente o que precisa.

## Etapa 5: Exportar o Valor da Célula como String Formatada

Às vezes você precisa do **como exportar célula excel** como texto simples — talvez para gravar em um arquivo de log ou enviá‑lo por uma API web. Aspose.Cells permite anexar opções de exportação a uma célula, instruindo a biblioteca a renderizar o valor como string usando o mesmo formato numérico.

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

Agora, ao ler o valor da célula através da API de exportação, receberemos uma string que já respeita a regra de duas casas decimais.

## Etapa 6: Recuperar a String Formatada (Converter Valor da Célula para String)

Vamos realmente executar a exportação e ver o resultado. O método `ExportString` devolve o conteúdo da célula como string, aplicando quaisquer `ExportTableOptions` que anexamos.

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

Ao executar o programa, o console exibe:

```
Formatted cell value: 12345.68
```

Observe o arredondamento de `12345.6789` para `12345.68` — esse é o efeito de **formatar número com duas casas decimais**.

## Etapa 7: (Opcional) Salvar a Pasta de Trabalho no Disco

Se também quiser ver o resultado dentro de um arquivo `.xlsx` real, basta chamar `Save`:

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

Abrindo `DemoWorkbook.xlsx` mostra o mesmo número na célula **C6**, formatado com duas casas decimais.

## Casos Limite & Perguntas Frequentes

### E se a célula já possuir um estilo?

O método `GetStyle` devolve uma cópia do estilo existente, de modo que qualquer formatação anterior (fonte, cor, etc.) é mantida. Você sobrescreve apenas a propriedade `Custom`, deixando todo o resto intacto.

### Como a cultura afeta o separador decimal?

Aspose.Cells respeita o `CultureInfo` da thread. Se precisar de vírgula ao invés de ponto, defina:

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

O mesmo formato `"0.00"` agora será renderizado como `12 345,68`.

### Posso exportar um intervalo de células de uma só vez?

Sim — use `Worksheet.ExportDataTable` ou `Worksheet.ExportString` com um endereço de intervalo. As `ExportTableOptions` definidas para uma única célula podem ser reutilizadas para todo o intervalo.

### E se eu não quiser que o valor seja arredondado, mas truncado?

Altere o formato personalizado para `"0.00"` com modo de arredondamento, ou trunque manualmente antes de inserir o valor:

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## Exemplo Completo (Pronto para Copiar‑Colar)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**Saída esperada no console**

```
Formatted cell value: 12345.68
```

Abra `DemoWorkbook.xlsx` → vá para a célula **C6** → você verá o mesmo número com duas casas decimais.

## Conclusão

Acabamos de cobrir tudo o que você precisa para **criar pasta de trabalho Excel** em C#, **definir formato numérico da célula**, **formatar número com duas casas decimais**, entender **como exportar célula Excel** e **converter valor da célula para string** para processamento posterior.  

Os principais aprendizados são:

1. Use `Workbook` e `Worksheet` para gerar um arquivo Excel em memória.  
2. Aplique um estilo personalizado (`"0.00"`) para impor exibição com duas casas decimais.  
3. Anexe `ExportTableOptions` a uma célula quando precisar de uma representação em string que respeite o mesmo formato.  

A partir daqui você pode experimentar — adicionar mais células, aplicar formatação condicional ou até gerar gráficos. Se estiver curioso sobre estilizar fontes ou adicionar fórmulas, consulte a documentação do Aspose.Cells sobre **cell styling** e **formula evaluation**.

Tem mais dúvidas sobre automação Excel em C#? Deixe um comentário, e feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Master Workbook Operations in Aspose.Cells .NET&#58; Load Excel Files and Trace Cell Precedents Effectively](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Master Aspose.Cells for .NET&#58; Advanced Excel Workbook and Cell Management](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}