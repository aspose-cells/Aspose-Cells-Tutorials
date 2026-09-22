---
category: general
date: 2026-03-25
description: Crie uma pasta de trabalho Excel a partir de JSON e salve a pasta de
  trabalho como xlsx. Aprenda como exportar JSON para xlsx, gerar Excel a partir de
  JSON e preencher Excel a partir de JSON em minutos.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: pt
og_description: Crie uma pasta de trabalho Excel a partir de JSON instantaneamente.
  Este guia mostra como exportar JSON para XLSX, gerar Excel a partir de JSON e preencher
  Excel a partir de JSON com Aspose.Cells.
og_title: Criar Pasta de Trabalho Excel a partir de JSON – Tutorial Completo de C#
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Criar Pasta de Trabalho do Excel a partir de JSON – Guia passo a passo
url: /pt/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pasta de Trabalho Excel a partir de JSON – Tutorial Completo em C#

Já precisou **criar excel workbook** a partir de um payload JSON mas não sabia por onde começar? Você não está sozinho; muitos desenvolvedores se deparam com esse obstáculo ao tentar transformar dados de API em uma planilha organizada. A boa notícia? Com algumas linhas de C# e Aspose.Cells você pode **export json to xlsx**, **generate excel from json**, e **populate excel from json** sem lidar com conversores de terceiros.

Neste guia vamos percorrer todo o processo — começando a partir de uma string JSON bruta, inserindo-a em um SmartMarker, e finalmente **save workbook as xlsx** no disco. Ao final você terá um arquivo Excel pronto‑para‑usar que se parece com isto:

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Pro tip:** Se você já está usando Aspose.Cells em outra parte do seu projeto, pode reutilizar a mesma instância `Workbook` para múltiplas importações de JSON — ótimo para processamento em lote.

## O que você precisará

- **.NET 6+** (ou qualquer .NET Framework recente que suporte C# 10)
- **Aspose.Cells for .NET** – instale via NuGet: `dotnet add package Aspose.Cells`
- Um entendimento básico da sintaxe C# (não é necessário conhecimento aprofundado de Excel)

É isso. Sem serviços externos, sem interop COM, apenas código gerenciado puro.

## Etapa 1: Inicializar uma Nova Pasta de Trabalho Excel

A primeira coisa que fazemos é criar um novo objeto workbook. Pense nele como abrir um arquivo Excel em branco onde inseriremos nossos dados mais tarde.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

Por que começar com um novo workbook? Ele garante uma página limpa, impede estilos residuais de execuções anteriores e mantém o tamanho do arquivo mínimo — perfeito para pipelines automatizados.

## Etapa 2: Preparar os Dados JSON que Você Deseja Importar

Para demonstração usaremos um pequeno array JSON, mas você pode substituir isso por qualquer JSON válido que receba de um serviço web, de um arquivo ou de uma consulta ao banco de dados.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

Observe as aspas duplamente escapadas (`\"`) — isso é apenas a sintaxe de literal de string em C#. Em um cenário real você provavelmente leria isso de um arquivo:

```csharp
// string jsonData = File.ReadAllText("data.json");
```

## Etapa 3: Instruir o SmartMarker a Tratar o Array Inteiro como um Único Registro

O mecanismo SmartMarker do Aspose.Cells pode iterar sobre coleções automaticamente. Ao habilitar **ArrayAsSingle**, tratamos todo o array JSON como um único registro, que é exatamente o que precisamos para uma tabela plana.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

Se você esquecer essa flag, o SmartMarker tentará criar uma planilha separada para cada elemento — definitivamente não é o que você quer ao gerar uma tabela simples.

## Etapa 4: Inserir um Token SmartMarker na Planilha

Tokens SmartMarker se parecem com `${jsonArray}`. Quando o processador executa, ele substitui o token pelos dados da fonte JSON. Colocaremos o token na célula **A1** para que a saída comece no canto superior‑esquerdo.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

Você também pode pré‑formatar a linha de cabeçalho antes do processamento. Por exemplo, definir fonte em negrito na primeira linha:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

## Etapa 5: Executar o Processador SmartMarker

Agora a mágica acontece. O processador lê o JSON, mapeia cada propriedade para uma coluna e escreve as linhas abaixo do token.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

Nos bastidores, o Aspose.Cells:

1. Analisa o JSON em um objeto .NET.
2. Corresponde os nomes das propriedades (`Name`, `Score`) aos cabeçalhos das colunas.
3. Escreve cada elemento do array como uma nova linha.

Se seu JSON contém objetos aninhados, você pode referenciá‑los usando notação de ponto (`${parent.child}`) — um recurso útil para relatórios mais complexos.

## Etapa 6: Salvar a Pasta de Trabalho como um Arquivo XLSX

Finalmente, persista o workbook no disco. A extensão de arquivo `.xlsx` indica ao Excel (e à maioria dos outros aplicativos de planilha) que este é um workbook OpenXML.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Você pode, claro, transmitir o workbook diretamente para uma resposta HTTP se estiver construindo uma API web:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

## Exemplo Completo Funcional

Abaixo está o programa completo, pronto‑para‑executar, que incorpora todas as etapas acima. Copie‑e‑cole em um novo projeto de console e pressione **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Resultado esperado:** Abrir `json-single.xlsx` mostra duas linhas sob o cabeçalho em negrito — `John` com pontuação `90` e `Anna` com `85`. Os nomes das colunas são inferidos automaticamente a partir dos nomes das propriedades JSON.

## Perguntas Frequentes & Casos Limites

### E se minhas chaves JSON contiverem espaços ou caracteres especiais?

SmartMarker espera nomes de identificadores válidos. Substitua espaços por underscores ou use um mapeamento customizado:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### Como exportar um grande array JSON (milhares de linhas)?

O processador transmite dados internamente, então o uso de memória permanece modesto. No entanto, você pode querer:

- Aumentar o limite `MaxRows` da planilha (`worksheet.Cells.MaxRow = 1_048_576;` – o máximo do Excel).
- Desativar as linhas de grade para desempenho (`worksheet.IsGridlinesVisible = false;`).

### Posso adicionar várias tabelas JSON na mesma pasta de trabalho?

Claro. Basta colocar diferentes tokens SmartMarker em intervalos separados (por exemplo, `${orders}` em `A10`, `${customers}` em `D1`) e chamar `Process` uma vez por token ou uma única vez com um objeto JSON composto contendo ambos os arrays.

## Bônus: Adicionando um Gráfico Simples (Opcional)

Se você quiser visualizar as pontuações, adicione um gráfico de colunas rápido após os dados serem preenchidos:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

## Conclusão

Agora você sabe **como criar excel workbook** a partir de uma string JSON, **export json to xlsx**, **generate excel from json**, e **populate excel from json** usando o recurso SmartMarker do Aspose.Cells. A solução completa — inicializando um workbook, configurando o SmartMarker, processando JSON e salvando o arquivo — cabe em algumas linhas, mas escala para conjuntos de dados massivos.

Próximos passos? Experimente substituir o JSON estático por uma chamada de API, adicionar formatação condicional baseada nas pontuações, ou gerar múltiplas planilhas para diferentes domínios de dados. O mesmo padrão funciona para CSV, XML ou até mesmo conjuntos de resultados de banco de dados — basta mudar a string de origem e ajustar o token SmartMarker.

Feliz codificação, e que suas planilhas estejam sempre organizadas!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}