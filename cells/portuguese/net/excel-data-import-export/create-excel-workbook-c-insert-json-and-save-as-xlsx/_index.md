---
category: general
date: 2026-03-30
description: Crie rapidamente uma planilha Excel em C# inserindo dados JSON e salvando-a
  como XLSX. Aprenda como gerar Excel a partir de JSON, escrever JSON no Excel e inserir
  JSON no Excel.
draft: false
keywords:
- create excel workbook c#
- save workbook as xlsx
- generate excel from json
- write json to excel
- insert json into excel
language: pt
og_description: Crie rapidamente uma planilha Excel em C# inserindo dados JSON e salvando-a
  como XLSX. Siga este guia passo a passo para gerar Excel a partir de JSON.
og_title: Criar Pasta de Trabalho Excel C# – Inserir JSON e Salvar como XLSX
tags:
- Aspose.Cells
- C#
- Excel automation
title: Criar Pasta de Trabalho Excel C# – Inserir JSON e Salvar como XLSX
url: /pt/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pasta de Trabalho Excel C# – Inserir JSON e Salvar como XLSX

Já precisou **criar pasta de trabalho Excel C#** e despejar algum JSON diretamente em uma célula? Você não é o único—os desenvolvedores frequentemente enfrentam o mesmo desafio quando têm payloads de API ou arquivos de configuração que precisam chegar a uma planilha para relatórios ou compartilhamento.  

A boa notícia é que com Aspose.Cells você pode fazer isso em poucas linhas, **salvar pasta de trabalho como XLSX**, e manter todo o processo tipado. Neste tutorial, vamos **gerar Excel a partir de JSON**, **escrever JSON no Excel**, e mostrar os passos exatos para **inserir JSON no Excel** sem concatenações de strings complicadas.

## O que este guia cobre

Vamos percorrer:

1. Configurar uma nova workbook.
2. Adicionar um Smart Marker que espera JSON.
3. Alimentar um array JSON ao marcador.
4. Ajustar `SmartMarkerOptions` para que o JSON permaneça em uma única célula.
5. Salvar o arquivo como uma workbook XLSX.

Ao final, você terá um arquivo `JsonSingleCell.xlsx` pronto para uso e um padrão sólido que pode reutilizar para qualquer cenário JSON‑para‑Excel. Sem serviços externos, apenas C# puro e a biblioteca Aspose.Cells.

**Pré-requisitos**

- .NET 6+ (ou .NET Framework 4.6+).  
- Visual Studio 2022 ou qualquer IDE compatível com C#.  
- Pacote NuGet `Aspose.Cells` (versão de avaliação gratuita ou licenciada).  

Se você tem tudo isso, vamos mergulhar — sem necessidade de configuração extra.

---

## Etapa 1: Criar uma Nova Workbook em C#

A primeira coisa que você precisa é um objeto workbook em branco. Pense nele como um novo arquivo Excel aguardando dados.

```csharp
using Aspose.Cells;

// Initialize a new workbook – this is your empty Excel file
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

**Por que isso importa:**  
`Workbook` é o ponto de entrada para todas as operações do Excel. Ao criá-lo primeiro, você garante que a chamada subsequente de **salvar workbook como xlsx** tenha um objeto concreto para serializar.

> **Dica profissional:** Se você planeja trabalhar com várias planilhas, pode adicioná‑las agora com `workbook.Worksheets.Add()`.

---

## Etapa 2: Colocar um Smart Marker que Espera JSON

Smart Markers são marcadores de posição que o Aspose.Cells substitui em tempo de execução. Aqui indicamos que ele procure por uma string JSON chamada `data`.

```csharp
// Put a Smart Marker in cell A1 – {{data:json}} tells Aspose to expect JSON
worksheet.Cells["A1"].PutValue("{{data:json}}");
```

**Por que isso importa:**  
O sufixo `:json` informa ao motor que o valor recebido é JSON, não texto simples. Isso é a chave para **escrever json no excel** sem análise manual.

---

## Etapa 3: Definir o Array JSON

Agora criamos o JSON que queremos inserir. Para demonstração, usaremos uma lista simples de pessoas.

```csharp
// Sample JSON array – could come from an API, file, or DB
string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Jane\",\"Age\":28}]";
```

**Caso de borda:**  
Se o seu JSON contém aspas duplas, certifique‑se de que elas estejam escapadas (como mostrado) ou use uma string literal (`@"..."`) para evitar erros de compilação.

---

## Etapa 4: Configurar Opções do Smart Marker – Manter o Array Inteiro

Por padrão, o Aspose tentaria expandir o array ao longo das linhas. Queremos que a string JSON inteira permaneça dentro de uma única célula, o que é perfeito para cenários de **inserir json no excel** onde o consumidor analisará o JSON posteriormente.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Treat the whole array as a single cell value
    ArrayAsSingle = true
};
```

**Por que isso importa:**  
`ArrayAsSingle = true` impede a expansão de linhas, fornecendo um blob JSON limpo em uma única célula. Isso é essencial quando a planilha é um formato de transporte e não um relatório.

---

## Etapa 5: Processar o Smart Marker com os Dados JSON

Agora vinculamos o JSON ao marcador e deixamos o Aspose fazer o trabalho pesado.

```csharp
// Process the marker – the anonymous object maps "data" to our JSON string
worksheet.SmartMarkers.Process(new { data = jsonData }, smartMarkerOptions);
```

**O que acontece nos bastidores:**  
O Aspose avalia o marcador `{{data:json}}`, serializa a string `jsonData` e a grava na célula A1 respeitando as opções que definimos.

---

## Etapa 6: Salvar a Workbook como Arquivo XLSX

Finalmente, gravamos a workbook no disco. É aqui que **salvar workbook como xlsx** entra em ação.

```csharp
// Save the workbook – the extension determines the format (XLSX here)
workbook.Save("JsonSingleCell.xlsx");
```

**Resultado:**  
Abra `JsonSingleCell.xlsx` no Excel, e você verá o array JSON exatamente como o definimos, sentado ordenadamente na célula A1.

---

## Exemplo Completo e Executável

Abaixo está o programa completo que você pode copiar‑colar em um aplicativo console. Ele inclui todas as etapas acima e funciona pronto para uso (desde que o pacote NuGet Aspose.Cells esteja instalado).

```csharp
using System;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Add a Smart Marker that expects JSON
            worksheet.Cells["A1"].PutValue("{{data:json}}");

            // 3️⃣ Define the JSON array
            string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Jane\",\"Age\":28}]";

            // 4️⃣ Configure options – keep array as a single cell value
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 5️⃣ Process the marker with the JSON payload
            worksheet.SmartMarkers.Process(new { data = jsonData }, smartMarkerOptions);

            // 6️⃣ Save the workbook as XLSX
            workbook.Save("JsonSingleCell.xlsx");

            Console.WriteLine("Excel file created successfully! Check JsonSingleCell.xlsx.");
        }
    }
}
```

**Saída esperada no Excel**

| A |
|---|
| `[{"Name":"John","Age":30},{"Name":"Jane","Age":28}]` |

Essa única célula agora contém um array JSON perfeitamente válido, pronto para processamento posterior.

---

## Perguntas Frequentes & Casos de Borda

### E se eu precisar que o JSON seja distribuído em linhas?

Defina `ArrayAsSingle = false` (o padrão). O Aspose criará uma linha para cada elemento do array, mapeando as propriedades do objeto para colunas. Isso é útil quando você deseja uma visualização tabular em vez de uma string JSON bruta.

### Posso usar um arquivo JSON em vez de uma string codificada?

Com certeza. Leia o arquivo em uma string:

```csharp
string jsonData = File.ReadAllText("people.json");
```

Então passe `jsonData` para a mesma chamada `Process`. O resto do pipeline permanece inalterado.

### Isso funciona com payloads JSON grandes?

Sim, mas fique de olho no uso de memória. Para arrays massivos, considere transmitir os dados ou escrever diretamente nas linhas (`ArrayAsSingle = false`) para evitar uma única célula gigantesca que o Excel pode ter dificuldade em lidar.

### O XLSX gerado é compatível com versões antigas do Excel?

O formato `.xlsx` baseia‑se no Office Open XML e funciona a partir do Excel 2007. Se precisar do formato legado `.xls`, altere a chamada de salvamento:

```csharp
workbook.Save("JsonSingleCell.xls", SaveFormat.Excel97To2003);
```

---

## Dicas Profissionais para Trabalhar com JSON e Excel

- **Valide o JSON primeiro** – use `System.Text.Json.JsonDocument.Parse(jsonData)` para detectar entradas malformadas cedo.  
- **Escape caracteres especiais** – se o seu JSON contém quebras de linha, elas aparecerão como `\n` literal na célula; você pode substituí‑las por `Environment.NewLine` antes do processamento.  
- **Reutilize Smart Markers** – você pode colocar múltiplos marcadores na mesma planilha, cada um apontando para uma propriedade JSON diferente.  
- **Combine com fórmulas** – uma vez que o JSON está em uma célula, você pode usar `FILTERXML` do Excel (em versões mais recentes) para analisá‑lo em tempo real.

---

## Conclusão

Agora você sabe como **criar excel workbook c#**, incorporar um payload JSON e **salvar workbook como xlsx** usando Aspose.Cells. Esse padrão permite que você **gere excel a partir de json**, **escreva json no excel**, e **insira json no excel** com apenas algumas linhas de código, facilitando a troca de dados entre serviços e analistas.

Pronto para o próximo passo? Tente converter o array JSON em uma tabela adequada (defina `ArrayAsSingle = false`) ou explore estilizar a planilha após a inserção. A mesma abordagem funciona para CSV, XML ou até objetos personalizados — basta ajustar o tipo de Smart Marker.

Feliz codificação, e sinta‑se à vontade para experimentar! Se encontrar algum problema, deixe um comentário abaixo ou consulte a documentação oficial da Aspose para aprofundar nos Smart Markers.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}