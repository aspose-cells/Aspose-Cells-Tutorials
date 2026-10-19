---
category: general
date: 2026-05-23
description: Como usar marcadores com Aspose.Cells para alcançar a nomeação dinâmica
  de planilhas na automação do Excel. Aprenda marcadores inteligentes, vinculação
  de dados JSON e criação de planilhas em minutos.
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: pt
og_description: Como usar marcadores no Aspose.Cells para gerar arquivos Excel com
  nomeação dinâmica de planilhas. Guia completo passo a passo com exemplo completo
  em C#.
og_title: Como usar marcadores – Nomeação dinâmica de planilhas no Excel com Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como usar marcadores no Aspose.Cells para nomeação dinâmica de planilhas no
  Excel
url: /pt/net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar Marcadores no Aspose.Cells para Nomeação Dinâmica de Planilhas no Excel

Já se perguntou **como usar marcadores** para transformar um modelo estático do Excel em uma planilha mestre‑detalhe completa? Você não está sozinho. Muitos desenvolvedores encontram dificuldades quando precisam de recursos de *nomeação dinâmica de planilhas excel*, especialmente quando os nomes das planilhas devem refletir valores de dados provenientes de JSON ou de um banco de dados.  

Neste tutorial, percorreremos um exemplo completo, pronto‑para‑executar em C# que mostra **como usar marcadores** com os smart markers do **Aspose.Cells**, vincular dados JSON e permitir que o processador crie planilhas cujos nomes mudam dinamicamente. Sem enrolação, apenas o código exato que você pode inserir no Visual Studio e ver os resultados instantaneamente.

## O que Você Vai Aprender

- O conceito de **smart markers** e por que eles são perfeitos para cenários mestre‑detalhe.  
- Como inserir tags de marcador em uma pasta de trabalho que serão substituídas posteriormente pelos nomes reais das planilhas.  
- Configurar **dynamic sheet naming excel** usando a opção `DetailSheetNewName`.  
- Executar o `SmartMarkerProcessor` com dados JSON para gerar várias planilhas automaticamente.  
- Verificar a saída e algumas dicas úteis para evitar armadilhas comuns.

> **Pré‑requisitos** – Você precisa de um runtime .NET recente (≥ .NET 6 é suficiente), da biblioteca Aspose.Cells para .NET (você pode obter uma avaliação gratuita da Aspose) e de familiaridade básica com C#.  

---

![exemplo de como usar marcadores no Aspose.Cells](example.png "exemplo de como usar marcadores no Aspose.Cells")

## Como Usar Marcadores para Criar Nomeação Dinâmica de Planilhas (Passo 1)

A primeira coisa que precisamos é de uma pasta de trabalho em branco que atuará como nosso modelo. Em um projeto real, você provavelmente começaria a partir de um arquivo `.xlsx` existente que já contém layout, formatação e células de espaço reservado. Para fins de clareza, criaremos tudo programaticamente.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*Por que isso importa*: O objeto `Worksheet` é onde inseriremos nossas tags de **smart marker**. Pense nas tags como pequenos espaços reservados que o processador substituirá posteriormente por valores reais do JSON.  

## Inserir Tags de Smart Marker (Passo 2)

Agora colocamos as tags de marcador diretamente nas células. A sintaxe `${...}` indica ao Aspose.Cells “isto é um marcador”. No nosso exemplo, precisamos de dois marcadores: um para o nome da planilha mestre e outro para o nome da planilha de detalhe.

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **Dica profissional** – Mantenha os nomes dos marcadores curtos e significativos; eles se tornam as chaves que você usará na carga JSON.  

## Preparar os Dados JSON (Passo 3)

O processador funciona com qualquer fonte de dados que possa ser representada como JSON, um `DataSet` ou até mesmo um objeto simples. Aqui está uma string JSON mínima que contém uma coleção mestre‑detalhe. Observe que cada pedido contém tanto um `MasterSheetName` quanto um `DetailSheetName`.

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*Por que JSON?* É leve, legível por humanos e funciona muito bem com APIs web. Você poderia facilmente obter esses dados de uma consulta SQL e serializá‑los com `Newtonsoft.Json`.

## Inicializar o SmartMarkerProcessor (Passo 4)

O `SmartMarkerProcessor` é o mecanismo que analisa a pasta de trabalho, encontra marcadores e realiza a vinculação de dados. Instanciá‑lo é uma única linha.

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## Definir Nomeação Dinâmica de Planilhas (Passo 5)

É aqui que **dynamic sheet naming excel** realmente brilha. Ao definir `DetailSheetNewName`, informamos ao processador para criar uma nova planilha de detalhe para cada pedido e nomeá‑la com base no `OrderId`. O placeholder `${OrderId}` é resolvido a partir do registro atual durante o processamento.

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **Atenção** – Se você esquecer de incluir a sintaxe `${}`, a planilha será literalmente nomeada “Detail_${OrderId}” em vez de “Detail_1”, “Detail_2”, etc.

## Aplicar JSON e Gerar Planilhas (Passo 6)

Agora deixamos o processador fazer o trabalho pesado. Ele lerá o JSON, substituirá os marcadores e criará novas planilhas conforme necessário.

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### O Que Acontece Por Trás dos Panos?

1. O processador lê o array `Orders`.  
2. Para cada pedido ele cria uma **planilha mestre** (usando `${Orders.MasterSheetName}`) e uma **planilha de detalhe** (usando o padrão `DetailSheetNewName`).  
3. Os valores das células são substituídos pelos campos JSON correspondentes, de modo que a primeira célula da planilha mestre passa a conter “Master_1”, “Master_2”, etc.  

## Salvar e Verificar o Resultado (Opcional)

Finalmente, grave a pasta de trabalho no disco. Abra o arquivo no Excel e você deverá ver duas planilhas mestre (`Master_1`, `Master_2`) e duas planilhas de detalhe nomeadas dinamicamente (`Detail_1`, `Detail_2`).  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**Saída esperada** – Após abrir `output.xlsx` você verá:

- Planilha **Master_1** com a célula A1 = “Master_1”.  
- Planilha **Detail_1** com a célula A1 = “Detail_1”.  
- Planilha **Master_2** com a célula A1 = “Master_2”.  
- Planilha **Detail_2** com a célula A1 = “Detail_2”.  

Esse é o ciclo completo de **como usar marcadores** para alcançar **dynamic sheet naming excel** com **smart markers do Aspose.Cells**.

---

## Perguntas Frequentes & Casos Limite

### E se eu precisar de mais de dois níveis de hierarquia?

Você pode aninhar marcadores dentro das planilhas de detalhe recém‑criadas. Basta colocar tags `${...}` adicionais na planilha modelo antes do processamento. O processador percorrerá cada nível automaticamente.

### Posso usar um DataTable em vez de JSON?

Com certeza. `SmartMarkerProcessor` tem sobrecargas para `DataSet`, `DataTable` e até objetos personalizados. A única mudança é a chamada para `ApplyJson` – você usaria `ApplyDataSet(myDataSet)` em vez disso.

### Como controlo a ordem de criação das planilhas?

A ordem segue a sequência da coleção de origem. Se precisar de uma ordenação personalizada, basta ordenar o array JSON (ou DataTable) antes de passá‑lo ao processador.

### Existe uma maneira de ocultar a planilha modelo após o processamento?

Sim. Defina `sm.Options.RemoveTemplateSheets = true;` antes de chamar `ApplyJson`. A planilha original (índice 0) será removida da pasta de trabalho final.

## Exemplo Completo Funcional (Todos os Passos Combinados)

Abaixo está o programa completo que você pode copiar‑colar em um novo projeto de console C#. Certifique‑se de que referenciou o pacote NuGet `Aspose.Cells`.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

Execute o programa, abra `output.xlsx` e você verá as planilhas dinâmicas exatamente como descrito anteriormente.

---

## Conclusão

Acabamos de cobrir **como usar marcadores** no Aspose.Cells para transformar uma pasta de trabalho simples em uma solução mestre‑detalhe com **dynamic sheet naming excel**. Os principais pontos são:

1. Insira marcadores smart `${...}` onde deseja que os dados apareçam.  
2. Alimente JSON (ou qualquer fonte de dados suportada) ao `SmartMarkerProcessor`.  
3. Use `DetailSheetNewName` para permitir que o processador nomeie novas planilhas dinamicamente.  

A partir daqui, você pode explorar cenários mais avançados — adicionando tabelas, estilizando células ou até incorporando gráficos — tudo impulsionado

## Tutoriais Relacionados

- [Como Implementar Smart Markers do Aspose.Cells em C# para Relatórios Dinâmicos no Excel](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Gerar Relatórios Dinâmicos no Excel Usando Smart Markers do Aspose.Cells .NET](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Dominar Aspose.Cells .NET: Implementar Smart Markers e Rótulos Personalizados para Relatórios Dinâmicos no Excel](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}