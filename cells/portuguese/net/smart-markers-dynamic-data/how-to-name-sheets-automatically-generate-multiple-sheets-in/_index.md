---
category: general
date: 2026-02-09
description: Como nomear planilhas em C# com SmartMarker – aprenda a gerar várias
  planilhas e automatizar a nomeação de planilhas em apenas algumas linhas de código.
draft: false
keywords:
- how to name sheets
- generate multiple sheets
- automate sheet naming
- SmartMarker sheet naming
- workbook automation
language: pt
og_description: Como nomear planilhas em C# usando opções do SmartMarker. Este guia
  mostra como gerar várias planilhas e automatizar a nomeação de planilhas sem esforço.
og_title: Como Nomear Planilhas Automaticamente – Guia Rápido de C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Como nomear planilhas automaticamente – Gerar múltiplas planilhas em C#
url: /pt/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Nomear Planilhas Automaticamente – Gerar Múltiplas Planilhas em C#

Já se perguntou **como nomear planilhas** em uma pasta de trabalho do Excel sem precisar clicar em “Renomear” manualmente toda vez? Você não está sozinho. Em muitos cenários de relatório você acaba com dezenas de planilhas de detalhe que precisam de nomes sistemáticos, e fazer isso à mão é um pesadelo.  

A boa notícia é que, com algumas linhas de C#, você pode **gerar múltiplas planilhas** e **automatizar a nomeação das planilhas** de modo que cada nova planilha de detalhe siga um padrão previsível. Neste tutorial vamos percorrer a solução completa, explicar por que cada parte é importante e fornecer um exemplo de código pronto‑para‑executar.

## O Que Este Guia Cobre

* Configurar uma pasta de trabalho que contém SmartMarkers.  
* Configurar `SmartMarkerOptions` para controlar o nome base das planilhas geradas.  
* Executar `ProcessSmartMarkers` para que a biblioteca crie `Detail`, `Detail_1`, `Detail_2`, … automaticamente.  
* Dicas para lidar com casos de borda, como nomes de planilhas existentes ou convenções de nomenclatura personalizadas.  
* Um exemplo completo, executável, que você pode colar no Visual Studio e ver o resultado imediatamente.

Nenhuma experiência prévia com Aspose.Cells é necessária — apenas uma configuração básica de C# e uma IDE de sua escolha.

## Pré‑requisitos

| Requisito | Por que importa |
|-----------|-----------------|
| .NET 6.0 ou superior | Recursos de linguagem modernos e compatibilidade com a biblioteca |
| Aspose.Cells for .NET (pacote NuGet) | Fornece o processamento de `SmartMarker` e a criação de planilhas |
| Um projeto de console vazio (ou qualquer app .NET) | Nos dá um local para executar o código |

Instale a biblioteca com:

```bash
dotnet add package Aspose.Cells
```

Agora que cobrimos o básico, vamos mergulhar na implementação real.

## Etapa 1: Criar uma Pasta de Trabalho com SmartMarkers

Primeiro precisamos de uma pasta de trabalho que contenha um placeholder SmartMarker. Pense em um SmartMarker como uma tag de modelo que indica ao motor onde injetar dados e, no nosso caso, quando criar uma nova planilha.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣  Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // 2️⃣  Insert a SmartMarker that will trigger sheet creation
        // The marker {{detail}} tells Aspose.Cells to repeat the row for each item in the "detail" collection.
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // 3️⃣  Prepare sample data for the SmartMarker
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };
```

> **Dica profissional:** Mantenha a planilha modelo leve. Apenas as linhas que precisam ser duplicadas devem conter SmartMarkers; todo o resto permanece estático.

## Etapa 2: Configurar Opções do SmartMarker – O Núcleo da Nomeação de Planilhas

Agora vem a mágica. Ao definir `DetailSheetNewName` informamos ao motor qual nome base usar para cada planilha gerada. A biblioteca acrescentará “_1”, “_2”, etc., sempre que o nome base já existir.

```csharp
        // 4️⃣  Define naming options – this is where we answer “how to name sheets”
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // Primary keyword appears here: how to name sheets
            DetailSheetNewName = "Detail"   // Base name for all generated sheets
        };
```

Se precisar de uma convenção diferente (por exemplo, “Report_2023”), basta alterar a string. O motor trata colisões automaticamente, e é por isso que essa abordagem **automatiza a nomeação de planilhas** sem código extra.

## Etapa 3: Processar SmartMarkers e Gerar as Planilhas

Com a pasta de trabalho, os dados e as opções prontos, uma única chamada de método faz o trabalho pesado.

```csharp
        // 5️⃣  Run the SmartMarker processor – this will create Detail, Detail_1, Detail_2…
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // 6️⃣  Save the result so you can open it in Excel
        wb.Save("GeneratedSheets.xlsx");

        // 7️⃣  Let the user know we’re done
        System.Console.WriteLine("Workbook created – check GeneratedSheets.xlsx");
    }
}
```

### Resultado Esperado

Ao abrir *GeneratedSheets.xlsx* você verá:

| Nome da Planilha | Conteúdo |
|------------------|----------|
| Template         | O layout original do marcador (mantido para referência) |
| Detail           | Primeiro conjunto de linhas (Apple, Banana, Cherry) |
| Detail_1         | Segunda cópia – dados idênticos (útil quando há várias coleções) |
| Detail_2         | …e assim por diante, dependendo de quantos grupos de SmartMarker distintos você tem |

O padrão de nomenclatura (`Detail`, `Detail_1`, `Detail_2`) demonstra **como nomear planilhas** programaticamente enquanto também **gera múltiplas planilhas** conforme necessário.

## Casos de Borda & Variações

### 1. Nomes de Planilhas Existentes

Se sua pasta de trabalho já contém uma planilha chamada “Detail”, o motor começará com “Detail_1”. Isso evita sobrescritas acidentais.

### 2. Formatos de Incremento Personalizados

Quer “Detail‑A”, “Detail‑B” em vez de sufixos numéricos? Você pode pós‑processar os nomes após `ProcessSmartMarkers`:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet sh = wb.Worksheets[i];
    if (sh.Name.StartsWith("Detail_"))
    {
        string suffix = ((char)('A' + i - 1)).ToString(); // A, B, C…
        sh.Name = $"Detail-{suffix}";
    }
}
```

### 3. Múltiplos Grupos de SmartMarker

Se sua pasta de trabalho contém mais de um grupo de SmartMarker (por exemplo, `{{invoice}}` e `{{detail}}`), cada grupo gerará seu próprio conjunto de planilhas baseado no mesmo `DetailSheetNewName`. Para dar a cada grupo um prefixo distinto, crie instâncias separadas de `SmartMarkerOptions` e chame `ProcessSmartMarkers` para cada coleção.

## Dicas Práticas do Campo

* **Dica profissional:** Desative `AllowDuplicateNames` em `WorkbookSettings` se quiser que a biblioteca lance uma exceção em vez de renomear planilhas silenciosamente. Isso ajuda a detectar bugs de lógica de nomeação cedo.  
* **Cuidado com:** Nomes base muito longos. O Excel limita nomes de planilhas a 31 caracteres; a biblioteca trunca automaticamente, mas você pode acabar com nomes ambíguos.  
* **Observação de desempenho:** Gerar centenas de planilhas pode consumir memória. Libere a pasta de trabalho (`wb.Dispose()`) assim que terminar, especialmente se estiver rodando dentro de um serviço de longa duração.

## Visão Geral Visual

![how to name sheets diagram](image.png "Diagram showing the flow from SmartMarker template to generated sheets – how to name sheets")

*Texto alternativo inclui a palavra‑chave principal para atender ao SEO.*

## Código‑Fonte Completo (Pronto para Copiar‑Colar)

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and template sheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // SmartMarker layout
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // Sample data
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };

        // Configure naming – this answers how to name sheets
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // Process markers → generates Detail, Detail_1, Detail_2 …
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // Save and finish
        wb.Save("GeneratedSheets.xlsx");
        System.Console.WriteLine("Workbook created – open GeneratedSheets.xlsx to see the result.");
    }
}
```

Execute o programa, abra o arquivo gerado e você verá as planilhas nomeadas automaticamente de acordo com o padrão que definimos.

## Conclusão

Agora você sabe **como nomear planilhas** em uma pasta de trabalho C#, como **gerar múltiplas planilhas** com SmartMarker e como **automatizar a nomeação de planilhas** para nunca mais precisar renomear nada manualmente. A abordagem escala de algumas páginas de detalhe para centenas, e o mesmo padrão funciona para qualquer coleção que você passar ao `ProcessSmartMarkers`.

Qual o próximo passo? Experimente trocar a fonte de dados por uma consulta ao banco de dados, teste formatos de sufixo personalizados ou encadeie múltiplos grupos de SmartMarker para um motor de relatório completo. O céu é o limite quando você deixa a biblioteca cuidar do trabalho repetitivo de nomeação.

Se este guia foi útil, dê uma estrela no GitHub, compartilhe com a equipe ou deixe um comentário abaixo com seus próprios truques de nomeação. Boa codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}