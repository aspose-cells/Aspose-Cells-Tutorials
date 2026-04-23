---
category: general
date: 2026-03-18
description: Aprenda a gerar Excel a partir de JSON com C#, permitir nomes de planilhas
  duplicados, criar planilha de detalhes e salvar a pasta de trabalho em C# em minutos.
draft: false
keywords:
- generate excel from json
- allow duplicate sheet names
- how to create detail sheet
- save workbook c#
- smartmarker options
- aspnet cells integration
language: pt
og_description: Gerar Excel a partir de JSON usando C#. Este guia mostra como permitir
  nomes de planilhas duplicados, criar uma planilha de detalhes e salvar a pasta de
  trabalho em C# com Aspose.Cells.
og_title: Gerar Excel a partir de JSON em C# – Tutorial Completo
tags:
- C#
- Excel automation
- JSON
- Aspose.Cells
title: Gerar Excel a partir de JSON em C# – Guia passo a passo
url: /pt/net/excel-data-import-export/generate-excel-from-json-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gerar Excel a partir de JSON em C# – Guia passo a passo

Já precisou **gerar Excel a partir de JSON** mas não sabia qual biblioteca poderia fazer o trabalho pesado? Você não está sozinho. Em muitas aplicações corporativas recebemos payloads em JSON e precisamos levar esses dados para planilhas bem formatadas — pense em relatórios de vendas, dumps de inventário ou logs de auditoria. A boa notícia? Com o motor SmartMarker do Aspose.Cells você pode transformar uma string JSON em um arquivo Excel completo em apenas algumas linhas.

Neste tutorial vamos percorrer todo o processo: desde a preparação do payload JSON, configuração do SmartMarker para **permitir nomes de planilha duplicados**, criação de uma **planilha de detalhes**, e finalmente **salvar a workbook em C#**. Ao final você terá um trecho reutilizável que pode ser inserido em qualquer projeto .NET.

> **Resumo rápido:**  
> • Objetivo principal – gerar Excel a partir de JSON.  
> • Objetivos secundários – permitir nomes de planilha duplicados, criar planilha de detalhes, salvar workbook em C#.  

## Pré‑requisitos

Antes de começarmos, certifique‑se de que você tem:

- .NET 6.0 SDK (ou qualquer versão recente do .NET).  
- Visual Studio 2022 ou VS Code com a extensão C#.  
- Uma licença ativa ou um trial gratuito do **Aspose.Cells for .NET** (o pacote NuGet é `Aspose.Cells`).  
- Um arquivo Excel modelo (`template.xlsx`) que já contenha tags SmartMarker como `&=Name` e um placeholder de tabela de detalhes.

Se algum desses itens lhe for desconhecido, não entre em pânico — instalar o pacote NuGet é um único comando, e o modelo pode ser uma planilha simples com algumas células placeholder.

## Visão geral da solução

Em alto nível faremos:

1. Definir uma string JSON que reflita os dados que queremos na planilha.  
2. Configurar `SmartMarkerOptions` para que nomes de planilha duplicados sejam permitidos e uma **planilha de detalhes** receba um nome previsível.  
3. Carregar o modelo Excel que contém as tags SmartMarker.  
4. Executar o processador SmartMarker para mesclar os dados JSON na workbook.  
5. Salvar o arquivo final com `workbook.Save(...)`.

Cada passo é explicado abaixo, com trechos de código completos e a importância de cada etapa.

---

## Etapa 1 – Prepare o payload JSON que será mesclado

A primeira coisa que você precisa é um documento JSON que corresponda às tags SmartMarker dentro do seu modelo. Pense no JSON como a fonte da verdade; cada chave se torna um placeholder no arquivo Excel.

```csharp
// Step 1: Define the JSON data that will be merged into the worksheet
string jsonData = @"{
    ""Name"": ""John"",
    ""Date"": ""2023-01-01"",
    ""Orders"": [
        { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
        { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
    ]
}";
```

**Por que isso importa:**  
SmartMarker lê a hierarquia JSON e expande automaticamente tabelas para coleções como `Orders`. Se a estrutura do seu JSON não estiver alinhada com as tags, a mesclagem produzirá silenciosamente linhas vazias — uma armadilha comum.

---

## Etapa 2 – Configure o SmartMarker para permitir nomes de planilha duplicados e nomeie a planilha de detalhes

Por padrão o Aspose.Cells proíbe nomes de planilha duplicados, o que pode ser um obstáculo quando você gera uma planilha de detalhes para cada registro mestre. A classe `SmartMarkerOptions` permite relaxar essa regra e também especificar um padrão de nomenclatura para as novas planilhas de detalhes.

```csharp
// Step 2: Create SmartMarker options and allow duplicate base names for detail sheets
var smartMarkerOptions = new Aspose.Cells.SmartMarker.SmartMarkerOptions
{
    // When a detail sheet is generated, it will be named "Detail", "Detail (2)", etc.
    DetailSheetNewName = "Detail",

    // This flag tells the engine that duplicate sheet names are acceptable.
    // Useful when you generate multiple detail sheets from a loop.
    AllowDuplicateSheetNames = true
};
```

**Por que isso importa:**  
Se você estiver iterando sobre vários clientes e cada iteração criar uma nova planilha, o motor normalmente lançaria uma exceção. Definir `AllowDuplicateSheetNames` como `true` indica ao Aspose.Cells que ele deve acrescentar automaticamente um sufixo numérico, mantendo o processo fluido.

---

## Etapa 3 – Carregue o modelo Excel que contém as tags SmartMarker

Seu modelo é a tela onde o SmartMarker pintará os dados. Ele pode conter qualquer formatação — cores, fórmulas, gráficos — então você não precisa recriar essa lógica programaticamente.

```csharp
// Step 3: Load the workbook that contains SmartMarker tags
using var workbook = new Aspose.Cells.Workbook(@"C:\MyProjects\ExcelDemo\template.xlsx");
```

**Dica:**  
Mantenha o modelo em uma pasta que faça parte da saída do seu projeto (por exemplo, `Content\Templates`). Assim você pode referenciá‑lo com um caminho relativo e evitar codificar diretórios absolutos.

---

## Etapa 4 – Execute o processador SmartMarker com o JSON e as opções

Agora a mágica acontece. O `SmartMarkerProcessor` lê o JSON, respeita as opções configuradas e preenche a workbook de acordo.

```csharp
// Step 4: Process the SmartMarker tags using the JSON data and the configured options
workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);
```

**O que está acontecendo nos bastidores?**  
- O processador varre cada célula em busca de marcadores como `&=Name` ou `&=Orders.Item`.  
- Substitui marcadores simples por valores escalares (`Name`, `Date`).  
- Para coleções (`Orders`), cria uma nova planilha de detalhes (nomeada “Detail”) e preenche uma linha de tabela para cada item.  
- Como permitimos nomes de planilha duplicados, se o modelo já possuir uma planilha chamada “Detail”, o motor criará “Detail (2)”.

---

## Etapa 5 – Salve a workbook mesclada no disco

Por fim, grave a workbook preenchida em um arquivo. Você pode escolher qualquer formato suportado pelo Aspose.Cells — XLSX, CSV, PDF, etc. Aqui usaremos o moderno XLSX.

```csharp
// Step 5: Save the workbook with the merged data
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

**Por que isso importa:**  
A gravação é onde você realmente **salva a workbook em C#**. Se precisar transmitir o arquivo de volta a um cliente web, pode usar `workbook.Save(Stream, SaveFormat.Xlsx)` em vez disso.

---

## Exemplo completo em funcionamento

Juntando tudo, aqui está um aplicativo console completo e pronto‑para‑executar. Certifique‑se de ter instalado o pacote NuGet `Aspose.Cells` (`dotnet add package Aspose.Cells`) antes de compilar.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace ExcelFromJsonDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Define the JSON payload
            string jsonData = @"{
                ""Name"": ""John"",
                ""Date"": ""2023-01-01"",
                ""Orders"": [
                    { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
                    { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
                ]
            }";

            // 2️⃣ Configure SmartMarker options – allow duplicate sheet names & set detail sheet name
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail",
                AllowDuplicateSheetNames = true
            };

            // 3️⃣ Load the template workbook (ensure the path is correct)
            var workbookPath = @"C:\MyProjects\ExcelDemo\template.xlsx";
            using var workbook = new Workbook(workbookPath);

            // 4️⃣ Merge JSON data into the workbook
            workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);

            // 5️⃣ Save the result
            var outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Excel file generated successfully at: {outputPath}");
        }
    }
}
```

### Resultado esperado

- **Sheet 1** (a planilha mestre) exibirá “John” na célula `Name` e “2023‑01‑01” na célula `Date`.  
- Uma nova planilha **Detail** aparecerá, contendo uma tabela com duas linhas: uma para o pedido de Laptop e outra para o pedido de Mouse.  
- Se o modelo já possuir uma planilha chamada “Detail”, a nova planilha será nomeada “Detail (2)”, graças à flag `AllowDuplicateSheetNames`.

![Excel output showing master sheet with name and date, plus a Detail sheet with order rows](excel-output.png "generate excel from json result")

*Texto alternativo da imagem:* **gerar excel a partir de json – exemplo de workbook com planilhas mestre e detalhe**

---

## Perguntas comuns & casos de borda

### E se o meu JSON contiver coleções aninhadas?

SmartMarker pode lidar com arrays aninhados, mas você precisará adicionar planilhas de detalhes adicionais ou usar marcadores hierárquicos. Por exemplo, `&=Orders.SubItems.Product` geraria automaticamente uma planilha de terceiro nível.

### Como personalizo o padrão de nomenclatura para planilhas duplicadas?

Em vez de um `DetailSheetNewName` estático, você pode atribuir um callback via `smartMarkerOptions.DetailSheetNameGenerator`. Isso permite inserir timestamps ou IDs únicos no nome da planilha.

```csharp
smartMarkerOptions.DetailSheetNameGenerator = (baseName, index) =>
    $"{baseName}_{DateTime.Now:yyyyMMdd}_{index}";
```

### Posso gerar CSV em vez de XLSX?

Com certeza. Substitua a chamada final de `Save` por:

```csharp
workbook.Save(outputPath, SaveFormat.Csv);
```

O restante do pipeline permanece idêntico.

### Isso funciona no ASP.NET Core?

Sim. O mesmo código pode ser executado dentro de uma ação de controlador. Basta transmitir a workbook na resposta:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0;
return File(ms, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "report.xlsx");
```

---

## Dicas profissionais & armadilhas

- **Dica profissional:** Mantenha suas tags SmartMarker em uma planilha “Template” separada. Assim você pode proteger a planilha contra edições acidentais enquanto ainda permite que o processador a leia.  
- **Cuidado com:** chaves JSON que contenham espaços ou caracteres especiais. Aspose.Cells espera identificadores JavaScript válidos; renomeie‑as ou use o atributo `JsonProperty` se estiver desserializando de um POCO.  
- **Dica de performance:** Se você estiver processando milhares de linhas, defina `smartMarkerOptions.EnableCache = true` para reutilizar marcadores compilados.  
- **Verificação de versão:** O código acima tem como alvo o Aspose.Cells 23.9+. Versões anteriores podem não suportar `AllowDuplicateSheetNames`.

---

## Conclusão

Agora você tem uma receita completa, de ponta a ponta, para **gerar Excel a partir de JSON** em C#. Ao configurar `SmartMarkerOptions` demonstramos como **permitir nomes de planilha duplicados**, controlar a nomenclatura da **planilha de detalhes** e, finalmente, **salvar a workbook em C#**. A abordagem é totalmente autônoma — sem serviços externos, apenas um único pacote NuGet.

Próximos passos? Experimente substituir a fonte JSON por uma API real

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}