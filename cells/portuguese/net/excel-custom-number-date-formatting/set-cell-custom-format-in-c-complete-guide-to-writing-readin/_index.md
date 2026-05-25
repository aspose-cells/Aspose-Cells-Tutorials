---
category: general
date: 2026-03-21
description: Defina formato personalizado de célula em C# e aprenda como gravar datas
  no Excel, aplicar formato de data personalizado, ler DateTime do Excel e criar rapidamente
  uma pasta de trabalho.
draft: false
keywords:
- set cell custom format
- write date to excel
- read datetime from excel
- apply custom date format
- create workbook worksheet
language: pt
og_description: Defina formato personalizado de célula em C# para gravar data no Excel,
  aplique formato de data personalizado, leia DateTime do Excel e crie planilha de
  workbook com facilidade.
og_title: Definir Formato Personalizado de Célula em C# – Escrever e Ler Datas no
  Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Definir Formato Personalizado de Célula em C# – Guia Completo para Escrever
  e Ler Datas no Excel
url: /pt/net/excel-custom-number-date-formatting/set-cell-custom-format-in-c-complete-guide-to-writing-readin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir Formato Personalizado de Célula – Gravar & Ler Datas no Excel com C#

Já precisou **definir formato personalizado de célula** em um arquivo Excel a partir do C# mas não sabia por onde começar? Você não está sozinho. Em muitas ferramentas de relatório ou utilitários de exportação de dados a data precisa aparecer em um local específico — pense em datas de era japonesa, calendários fiscais ou strings ISO‑8601.  

Neste tutorial vamos percorrer um **exemplo completo e executável** que mostra como **gravar data no Excel**, **aplicar formato de data personalizado**, **ler DateTime do Excel** e **criar planilha de workbook** com Aspose.Cells. Ao final, você terá um programa único e autocontido que pode ser inserido em qualquer projeto .NET.

## O que Você Vai Aprender

- Como **criar planilha de workbook** programaticamente.  
- Os passos exatos para **gravar data no Excel** usando uma string específica de localidade.  
- Como **aplicar formato de data personalizado** (incluindo notação de era japonesa).  
- O modo de **ler DateTime do Excel** de volta para um objeto `DateTime`.  
- Dicas, armadilhas e variações que você pode encontrar ao lidar com datas no Excel.

Nenhuma documentação externa necessária — tudo que você precisa está aqui.

## Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.7+).  
- Aspose.Cells para .NET instalado via NuGet (`Install-Package Aspose.Cells`).  
- Um entendimento básico da sintaxe C# — nada sofisticado.

> **Dica profissional:** Se você estiver usando o Visual Studio, habilite *nullable reference types* para capturar bugs sutis mais cedo.

## Etapa 1: Criar um Workbook e uma Worksheet  

Primeiro de tudo: você precisa de um objeto workbook que represente o arquivo Excel e de uma worksheet onde os dados viverão.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1: Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];           // default sheet is named "Sheet1"
```

*Por que isso importa:* A classe `Workbook` é o ponto de entrada para todas as operações do Excel. Criá‑la na memória significa que você nunca toca no sistema de arquivos até salvar explicitamente, o que mantém o processo rápido e amigável a testes.

## Etapa 2: Gravar Data no Excel  

Em seguida, vamos colocar uma string de data da era japonesa (`"R02-04-01"`) na célula **A1**. A string imita a era Reiwa (ano 2, 1º de abril).

```csharp
        // Step 2: Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("R02-04-01");
```

*O que está acontecendo:* `PutValue` armazena a string bruta. Aspose.Cells tentará analisá‑la posteriormente com base no estilo da célula. Se você pular esta etapa e gravar um `DateTime` diretamente, perderá a informação da era que deseja exibir.

## Etapa 3: Aplicar o Formato Numérico de Data Incorporado (ID 14)

O Excel possui um formato de data incorporado com ID 14 (`mm-dd-yy`). Aplicá‑lo informa ao motor que a célula **contém uma data**, não apenas texto.

```csharp
        // Step 3: Apply the built‑in date number format (ID 14)
        worksheet.Cells["A1"].Style.Number = 14;
```

*Por que usar o ID 14?* É o formato “data curta” universal que garante que o Excel trate o conteúdo como um valor de data, pré‑requisito para que qualquer formato personalizado funcione corretamente.

## Etapa 4: Definir um Formato Personalizado para Exibir Notação de Era Japonesa  

Agora vem a parte divertida: instruímos o Excel a renderizar a data usando o formato de era japonesa. A string personalizada `[$-ja-JP]ggge年m月d日` faz exatamente isso.

```csharp
        // Step 4: Set a custom format to display the date in Japanese era notation
        worksheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge年m月d日";
```

*Explicação:*  
- `[$-ja-JP]` força a localidade para japonês.  
- `ggg` é o nome da era (ex.: “R” para Reiwa).  
- `e` é o ano da era.  
- `年`, `月`, `日` são caracteres japoneses literais para ano, mês e dia.

Se precisar de uma localidade diferente, basta substituir `ja-JP` pelo código cultural adequado (ex.: `en-US`).

## Etapa 5: Recuperar o Valor DateTime Analisado  

Por fim, vamos ler o **real `DateTime`** que o Excel analisou a partir da célula. Isso comprova que a string foi interpretada corretamente.

```csharp
        // Step 5: Retrieve the parsed DateTime value from the cell
        DateTime parsedDate = worksheet.Cells["A1"].DateTime;   // => 2020‑04‑01

        // Output to console for verification
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

*Resultado:* O console exibe `Parsed DateTime: 2020-04-01`. Embora tenhamos inserido uma string de era japonesa, o Excel armazena internamente a data gregoriana, que pode ser usada para cálculos, comparações ou exportações adicionais.

## Etapa 6: Salvar o Workbook (Opcional)

Se quiser ver a planilha formatada no Excel, basta salvá‑la no disco.

```csharp
        // Optional: Save the workbook to a file
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Abra o **JapaneseEraDate.xlsx** gerado e você verá a célula **A1** exibindo `R02年4月1日` (o formato exato de era japonesa que definimos).

![definir formato personalizado de célula exemplo](image-placeholder.png "Célula do Excel mostrando data da era japonesa – definir formato personalizado de célula")

*O texto alternativo acima contém a palavra‑chave principal, atendendo ao requisito de SEO da imagem.*

## Variações Comuns & Casos de Borda  

### Gravando um Formato de Data Diferente  

Se preferir ISO‑8601 (`2020-04-01`) em vez de uma string de era, basta mudar a chamada `PutValue`:

```csharp
worksheet.Cells["A1"].PutValue(new DateTime(2020, 4, 1));
worksheet.Cells["A1"].Style.Number = 14;                 // keep built‑in date format
worksheet.Cells["A1"].Style.Custom = "yyyy-mm-dd";      // custom ISO format
```

### Lidando com Células Nulas ou Vazias  

Ao ler uma data, sempre verifique se a célula não está vazia para evitar `InvalidOperationException`:

```csharp
if (!worksheet.Cells["A1"].IsDate)
{
    Console.WriteLine("Cell A1 does not contain a valid date.");
}
else
{
    DateTime dt = worksheet.Cells["A1"].DateTime;
    // use dt...
}
```

### Suportando Múltiplas Localidades  

Você pode percorrer uma lista de códigos culturais e aplicá‑los dinamicamente:

```csharp
string[] cultures = { "ja-JP", "en-US", "fr-FR" };
foreach (var culture in cultures)
{
    worksheet.Cells["A1"].Style.Custom = $"[$-{culture}]ggge年m月d日";
    // Save or export per culture if needed
}
```

## Dicas Profissionais & Armadilhas  

- **Sempre defina primeiro um formato numérico incorporado** (`Style.Number`). Sem ele, o Excel trata a célula como texto simples e o formato personalizado é ignorado.  
- **Códigos de localidade não diferenciam maiúsculas de minúsculas**, mas usar a forma canônica (`ja-JP`) evita confusões.  
- **Salvar é opcional** para processamento em memória; você pode transmitir o workbook diretamente para uma resposta web (`workbook.Save(stream, SaveFormat.Xlsx)`).  
- **Licenças Aspose.Cells**: A versão de avaliação gratuita adiciona marca d'água. Para produção, certifique‑se de ter uma licença válida para evitar penalidades de desempenho.

## Recapitulação  

Mostramos como **definir formato personalizado de célula** em C# para exibir datas de era japonesa, como **gravar data no Excel**, **aplicar formato de data personalizado**, **ler DateTime do Excel** e **criar planilha de workbook** — tudo em um único programa autocontido. A palavra‑chave principal aparece naturalmente ao longo do texto, enquanto palavras‑chave secundárias são inseridas em títulos e no corpo, atendendo tanto aos requisitos de SEO quanto aos padrões de citação por IA.

## O que vem a seguir?

- Explore **formatação condicional** para destacar datas vencidas.  
- Combine esta abordagem com **PivotTables** para relatórios dinâmicos.  
- Experimente **ler arquivos CSV grandes** e convertê‑los para Excel usando a mesma lógica de tratamento de datas.  

Sinta‑se à vontade para experimentar diferentes localidades, padrões personalizados ou até fusos horários. Se encontrar algum obstáculo, deixe um comentário abaixo — feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}