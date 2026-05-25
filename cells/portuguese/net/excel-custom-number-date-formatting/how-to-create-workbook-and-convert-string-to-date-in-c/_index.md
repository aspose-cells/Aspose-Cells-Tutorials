---
category: general
date: 2026-02-15
description: Como criar uma pasta de trabalho, converter string para data e formatar
  a célula como data com Aspose.Cells. Aprenda a definir o formato numérico da célula
  e ler a data do Excel facilmente.
draft: false
keywords:
- how to create workbook
- convert string to date
- format cell as date
- set cell number format
- read excel date
language: pt
og_description: Como criar uma planilha, converter string para data e formatar a célula
  como data. Guia completo passo a passo para ler datas do Excel.
og_title: Como criar uma planilha e converter string para data em C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Como criar uma pasta de trabalho e converter string para data em C#
url: /pt/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar workbook e converter string para data em C#

Já se perguntou **como criar workbook** que transforma um texto simples como `"R3-04-01"` em um valor real de `DateTime`? Você não é o único — muitos desenvolvedores enfrentam esse problema ao extrair dados de sistemas legados ou entrada de usuário. A boa notícia? Com algumas linhas de C# e Aspose.Cells você pode fazer isso rapidamente, sem necessidade de análise manual.

Neste tutorial vamos percorrer todo o processo: criar um workbook, inserir uma string de data, aplicar um **format cell as date** adequado, forçar o mecanismo a **set cell number format**, e finalmente **read excel date** de volta como um `DateTime`. Ao final, você terá um trecho de código executável que pode ser inserido em qualquer projeto .NET.

## Pré-requisitos

- .NET 6+ (ou .NET Framework 4.7.2+)
- Pacote NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`)
- Um entendimento básico da sintaxe C#
- Uma IDE como Visual Studio ou VS Code (qualquer uma serve)

Nenhuma configuração extra é necessária — Aspose.Cells cuida de todo o trabalho pesado internamente.

## Etapa 1: Como criar workbook – inicializar o arquivo Excel

Primeiro, precisamos de um objeto workbook novo. Pense nele como um caderno em branco onde cada planilha é uma página.

```csharp
using Aspose.Cells;

 // Step 1: Create a new workbook
 var workbook = new Workbook();          // Empty workbook with one default sheet
```

*Por que isso importa:* Criar o workbook nos fornece um contêiner para células, estilos e fórmulas. Sem ele, não há onde colocar a string de data.

## Etapa 2: Converter string para data – inserir o texto bruto

Agora inserimos a string de data bruta na célula **A1** da primeira planilha. A string usa um formato personalizado (`R3-04-01`) que o Excel não reconhece imediatamente.

```csharp
 // Step 2: Insert a date string into cell A1 of the first worksheet
 var targetCell = workbook.Worksheets[0].Cells["A1"];
 targetCell.PutValue("R3-04-01");        // Raw text, not yet a date
```

*Por que fazemos isso:* `PutValue` armazena o texto literal. Se tentássemos definir um `DateTime` diretamente, o formato personalizado seria perdido. Mantê‑lo como texto nos permite aplicar posteriormente um **set cell number format** que indica ao Excel como interpretá‑lo.

## Etapa 3: Format cell as date – aplicar estilo número 14

O estilo de data interno do Excel 14 corresponde a `mm-dd-yy`. Ao atribuir esse estilo, informamos ao mecanismo: “Trate o conteúdo desta célula como uma data.”

```csharp
 // Step 3: Apply a date number format (style number 14) to the cell
 targetCell.SetStyle(new Style { Number = 14 });
```

*O que acontece nos bastidores:* A propriedade `Number` mapeia para os IDs de formato numérico internos do Excel. Quando o workbook recalcula, o Excel tentará converter o texto em uma data serial usando o formato fornecido.

## Etapa 4: Set cell number format – forçar recalculação

O Excel não converterá magicamente o texto até que solicitemos a avaliação de fórmulas (ou, neste caso, a reinterpretação da célula). Chamar `CalculateFormula` dispara essa conversão.

```csharp
 // Step 4: Recalculate any formulas so the cell value is interpreted as a date
 workbook.CalculateFormula();
```

*Dica:* Se você estiver trabalhando com muitas células, pode chamar `CalculateFormula` uma única vez após concluir toda a formatação — isso economiza alguns milissegundos.

## Etapa 5: Read Excel date – obter o valor DateTime

Finalmente, extraímos a representação `DateTime` da célula. Aspose.Cells a expõe via `DateTimeValue`.

```csharp
 // Step 5: Retrieve the DateTime representation and display it
 Console.WriteLine(targetCell.DateTimeValue);
```

**Saída esperada (assumindo o calendário gregoriano padrão):**

```
2023-04-01 00:00:00
```

Observe como o prefixo `"R3-"` é ignorado porque o analisador de datas do Excel foca na parte numérica quando o estilo é de data. Se suas strings contiverem outros prefixos, pode ser necessário pré‑processá‑las, mas para muitos formatos legados essa abordagem funciona perfeitamente.

## Exemplo Completo Funcional

Juntando tudo, aqui está o programa completo, pronto‑para‑executar:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook
        var workbook = new Workbook();

        // Step 2: Insert a date string into cell A1 of the first worksheet
        var targetCell = workbook.Worksheets[0].Cells["A1"];
        targetCell.PutValue("R3-04-01");

        // Step 3: Apply a date number format (style number 14) to the cell
        targetCell.SetStyle(new Style { Number = 14 });

        // Step 4: Recalculate any formulas so the cell value is interpreted as a date
        workbook.CalculateFormula();

        // Step 5: Retrieve the DateTime representation and display it
        Console.WriteLine(targetCell.DateTimeValue);
    }
}
```

Salve isso como `Program.cs`, restaure o pacote Aspose.Cells e execute `dotnet run`. Você deverá ver o `DateTime` formatado impresso no console.

## Variações Comuns & Casos Limite

### Diferentes strings de data

Se seus dados de origem se parecem com `"2023/04/01"` ou `"01‑Apr‑2023"`, você ainda pode usar o mesmo fluxo de trabalho — basta alterar a propriedade **Number** para um formato que corresponda ao padrão (por exemplo, `Number = 15` para `d-mmm-yy`).  

### Formatos específicos de localidade

O Excel respeita as configurações de localidade do workbook. Para forçar a análise no estilo dos EUA, defina a cultura do workbook:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

### Quando a string não é reconhecida

Às vezes o Excel não consegue inferir uma data (ex.: `"R3-13-40"`). Nesses casos, pré‑procese a string:

```csharp
string raw = "R3-04-01";
string cleaned = raw.Replace("R3-", "");   // Remove the prefix
targetCell.PutValue(cleaned);
```

Em seguida, aplique o mesmo formato numérico.

## Dicas Profissionais & Armadilhas

- **Dica profissional:** Use `StyleFlag` para modificar apenas o formato numérico, deixando os demais atributos de estilo intactos.  
  ```csharp
  var style = targetCell.GetStyle();
  style.Number = 14;
  var flag = new StyleFlag { Number = true };
  targetCell.SetStyle(style, flag);
  ```
- **Cuidado:** Sobrescrever estilos existentes em uma célula que já possui bordas ou fontes. A abordagem `StyleFlag` evita isso.
- **Nota de desempenho:** Se você estiver processando milhares de linhas, agrupe a chamada `CalculateFormula` após concluir todas as atualizações; chamá‑la por linha adiciona sobrecarga desnecessária.

## Conclusão

Agora você sabe **como criar workbook**, **converter string para data**, **format cell as date**, **set cell number format**, e finalmente **read excel date** de volta para um `DateTime`. O padrão é simples: inserir texto bruto, aplicar um estilo de data, forçar a recalculação e então ler o valor.  

A partir daqui, você pode estender a lógica para colunas inteiras, importar dados CSV ou até gerar relatórios que traduzam automaticamente strings de data legadas em datas corretas do Excel.  

Pronto para avançar? Experimente aplicar um formato numérico personalizado (`Number = 22`) para exibir datas como `yyyy-mm-dd`, ou explore as utilidades `DateTimeConversion` do Aspose.Cells para cenários mais complexos.

Feliz codificação! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}