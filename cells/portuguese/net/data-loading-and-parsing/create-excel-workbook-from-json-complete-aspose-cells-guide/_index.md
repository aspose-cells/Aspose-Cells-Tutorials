---
category: general
date: 2026-02-14
description: Crie uma pasta de trabalho Excel usando Aspose.Cells e aprenda como processar
  JSON, converter JSON para Excel e carregar JSON no Excel em alguns passos simples.
draft: false
keywords:
- create excel workbook
- how to process json
- convert json to excel
- load json into excel
- aspose cells json
language: pt
og_description: Crie uma pasta de trabalho Excel com Aspose.Cells, aprenda a processar
  JSON, converta JSON para Excel e carregue JSON no Excel de forma rápida e confiável.
og_title: Criar pasta de trabalho Excel a partir de JSON – Tutorial passo a passo
  do Aspose.Cells
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Criar pasta de trabalho do Excel a partir de JSON – Guia completo do Aspose.Cells
url: /pt/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pasta de Trabalho Excel a partir de JSON – Guia Completo do Aspose.Cells

Já precisou **criar uma pasta de trabalho Excel** a partir de um trecho de JSON, mas não sabia por onde começar? Você não está sozinho. Muitos desenvolvedores enfrentam o mesmo obstáculo quando têm um payload JSON e precisam de uma planilha organizada para relatórios ou troca de dados.  

A boa notícia? Com **Aspose.Cells** você pode transformar esse JSON em um arquivo Excel totalmente funcional em apenas algumas linhas. Neste tutorial vamos percorrer **como processar JSON**, **converter JSON para Excel** e **carregar JSON no Excel** usando o poderoso `SmartMarkerProcessor`. Ao final, você terá uma pasta de trabalho pronta‑para‑salvar e uma visão clara das opções que pode ajustar.

## O que você vai aprender

- Como configurar um projeto Aspose.Cells para manipular JSON.  
- O código exato necessário para **criar pasta de trabalho Excel** a partir de um array JSON.  
- Por que a opção `ArrayAsSingle` é importante e quando você pode querer alterá‑la.  
- Dicas para lidar com estruturas JSON maiores, tratamento de erros e salvamento do arquivo.  

> **Pré‑requisitos:** .NET 6+ (ou .NET Framework 4.6+), pacote NuGet Aspose.Cells for .NET e conhecimento básico de C#. Nenhuma outra biblioteca é necessária.

---

## Etapa 1: Instalar Aspose.Cells e adicionar o namespace necessário

Antes de qualquer código ser executado, você precisa referenciar a biblioteca Aspose.Cells no seu projeto.

```bash
dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;   // Core namespace for workbook manipulation
```

> **Dica de especialista:** Se você estiver usando o Visual Studio, o Gerenciador de Pacotes NuGet faz o mesmo trabalho — basta procurar por *Aspose.Cells* e clicar em Instalar.

---

## Etapa 2: Preparar os dados JSON que você deseja converter

O `SmartMarkerProcessor` funciona com qualquer string JSON, mas você precisa decidir como a biblioteca deve interpretar arrays. Neste exemplo trataremos um array numérico simples como um **registro único**, o que é útil quando você só precisa de uma lista plana de valores.

```csharp
// Step 2: Define the JSON payload – an array of three numbers
string jsonData = "[1,2,3]";   // You could also load this from a file or API response
```

> **Por que isso importa:** Por padrão, Aspose.Cells trata cada elemento do array como um registro separado. Definir `ArrayAsSingle = true` colapsa todo o array em um único registro, o que corresponde a muitos cenários de relatório.

---

## Etapa 3: Criar uma nova instância de Workbook

Agora realmente **criamos a pasta de trabalho Excel** na memória. Nenhum arquivo é escrito ainda; estamos apenas preparando o contêiner.

```csharp
// Step 3: Initialise a fresh workbook – starts with a single empty worksheet
Workbook workbook = new Workbook();
```

Neste ponto `workbook.Worksheets[0]` é uma planilha em branco chamada *Sheet1*. Você pode renomeá‑la depois, se desejar.

---

## Etapa 4: Configurar as opções SmartMarker para o processamento de JSON

A classe `SmartMarkerOptions` oferece controle granular sobre como o JSON é interpretado. A flag chave para o nosso cenário é `ArrayAsSingle`.

```csharp
// Step 4: Set SmartMarker options – treat the JSON array as a single record
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // Important when your JSON is a simple list
};
```

> **Quando mudar isso:** Se o seu JSON representa uma coleção de linhas (por exemplo, um array de objetos), deixe `ArrayAsSingle` como `false`. Cada objeto se tornará uma nova linha automaticamente.

---

## Etapa 5: Executar o processamento Smart Marker na planilha

Com a pasta de trabalho e as opções prontas, alimentamos o JSON ao processador. O processador varre a planilha em busca de smart markers (marcadores) e os substitui pelos dados do JSON. Como não temos marcadores explícitos, o processador simplesmente cria um layout padrão.

```csharp
// Step 5: Execute Smart Marker processing on the first worksheet
workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);
```

Se quiser controlar a célula exata onde os dados começam, adicione um marcador como `"${Array}"` à célula **A1** antes de executar o processador. Para este tutorial, usamos o comportamento padrão, que grava os valores do array em células consecutivas a partir de **A1**.

---

## Etapa 6: Salvar a pasta de trabalho em disco (ou em stream)

A etapa final é persistir a pasta de trabalho. Você pode salvar em um arquivo, em um `MemoryStream` ou até retorná‑la diretamente de uma API web.

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

Executar o programa completo gera um arquivo Excel com os números **1**, **2** e **3** posicionados nas células **A1**, **A2** e **A3**, respectivamente.

---

## Exemplo completo em funcionamento

Abaixo está o aplicativo console completo, pronto‑para‑executar, que reúne todas as etapas. Copie‑e‑cole em um novo projeto console C# e pressione **F5**.

```csharp
// ---------------------------------------------------------------
// Complete example: Create Excel workbook from JSON using Aspose.Cells
// ---------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare JSON data
        string jsonData = "[1,2,3]";

        // 2️⃣ Create a new workbook (empty Excel file)
        Workbook workbook = new Workbook();

        // 3️⃣ Configure SmartMarker options – treat the array as a single record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Process the JSON on the first worksheet
        workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);

        // 5️⃣ Optionally, add a header for clarity
        workbook.Worksheets[0].Cells["A1"].PutValue("Numbers");
        // Shift data down one row so the header stays on top
        workbook.Worksheets[0].Cells.InsertRows(1, 1);

        // 6️⃣ Save the workbook
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Excel workbook created at: {outputPath}");
    }
}
```

**Saída esperada no Excel**

| Numbers |
|---------|
| 1       |
| 2       |
| 3       |

A linha de cabeçalho (“Numbers”) é opcional, mas demonstra como você pode combinar edições manuais de células com o processamento de smart‑marker.

---

## Perguntas frequentes & casos de borda

### E se o meu JSON for um objeto, não um array?

```json
{
  "Name": "Alice",
  "Age": 30,
  "Country": "USA"
}
```

Você ainda pode usar `SmartMarkerProcessor`. Coloque marcadores como `${Name}`, `${Age}`, `${Country}` na planilha e, em seguida, chame `StartSmartMarkerProcessing`. O processador substituirá cada marcador pelo valor correspondente.

### Como lidar com arquivos JSON grandes (megabytes)?

- **Transmitir o JSON**: Em vez de carregar a string inteira, leia o arquivo com um `StreamReader` e passe o texto para `StartSmartMarkerProcessing`.  
- **Aumentar limite de memória**: Defina `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` se encontrar `OutOfMemoryException`.  
- **Processamento em blocos**: Divida o JSON em arrays menores e processe cada bloco em uma nova planilha.

### Posso exportar para CSV em vez de XLSX?

Com certeza. Após o processamento, basta chamar:

```csharp
workbook.Save("output.csv", SaveFormat.Csv);
```

O layout dos dados permanece o mesmo; apenas o formato do arquivo muda.

### E se eu precisar formatar células (fontes, cores) após carregar o JSON?

Você pode aplicar formatação depois da etapa de smart‑marker:

```csharp
Style style = workbook.CreateStyle();
style.Font.IsBold = true;
workbook.Worksheets[0].Cells["A1"].SetStyle(style);
```

Como o processador roda primeiro, qualquer formatação aplicada posteriormente não será sobrescrita.

---

## Dicas & boas práticas

- **Sempre defina `ArrayAsSingle` de forma deliberada** – esquecer essa flag é uma fonte comum de duplicação inesperada de linhas.  
- **Valide o JSON antes do processamento** – uma string malformada lança `JsonParseException`. Envolva a chamada em um bloco `try/catch` para tratamento de erros mais elegante.  
- **Use smart markers nomeados** (`${Orders}`) para melhorar a legibilidade, especialmente ao lidar com objetos JSON aninhados.  
- **Mantenha a pasta de trabalho na memória** se estiver retornando-a de uma API web; enviar um `MemoryStream` evita I/O desnecessário de disco.  
- **Compatibilidade de versão**: O código acima funciona com Aspose.Cells 23.12 ou posterior. Verifique as notas de lançamento se estiver usando uma versão mais antiga.

---

## Conclusão

Acabamos de mostrar como **criar pasta de trabalho Excel** a partir de JSON usando Aspose.Cells, cobrindo tudo, desde a instalação da biblioteca até a gravação do arquivo final. Ao dominar `SmartMarkerProcessor` e suas opções, você pode **carregar JSON no Excel**, **converter JSON para Excel** e ainda personalizar a saída para cenários de relatório complexos.  

Pronto para o próximo passo? Experimente alimentar um array JSON aninhado de objetos, adicionar formatação condicional ou exportar o resultado como PDF — tudo com a mesma API Aspose.Cells. Seus pipelines de dados‑para‑Excel agora estão a apenas algumas linhas de código.

Se tiver dúvidas ou encontrar algum obstáculo, deixe um comentário abaixo. Boa codificação e aproveite transformar JSON em planilhas bonitas! 

![Criar pasta de trabalho Excel com dados JSON](/images/create-excel-workbook-json.png "Ilustração de um array JSON sendo transformado em uma planilha Excel")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}