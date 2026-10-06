---
category: general
date: 2026-03-25
description: Aprenda a exportar Excel para DataTable em C# rapidamente. Este tutorial
  aborda a exportação de Excel com nomes de colunas e a exportação de dados do Excel
  como string para um manuseio de dados confiável.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: pt
og_description: Exporte Excel para DataTable em C# com nomes de colunas e conversão
  de string. Siga este tutorial conciso para uma solução pronta‑para‑usar.
og_title: Exportar Excel para DataTable em C# – Guia Completo
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: Exportar Excel para DataTable em C# – Guia passo a passo
url: /pt/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar Excel para DataTable em C# – Guia Passo a Passo

Já precisou **exportar Excel para DataTable** mas não sabia quais opções ativar? Você não está sozinho — muitos desenvolvedores encontram a mesma dificuldade ao tentar trazer dados de planilhas para um `DataTable`.  

A boa notícia? Em apenas algumas linhas de código você pode **exportar Excel com nomes de colunas** e ainda **exportar dados do Excel como string** para evitar dores de cabeça com incompatibilidade de tipos. Abaixo você encontrará um exemplo completo e executável, além do “porquê” de cada configuração, para que possa adaptá‑lo a qualquer projeto sem adivinhações.

## O que este tutorial cobre

* Como criar uma workbook na memória (sem necessidade de arquivo físico).  
* Preencher algumas linhas de exemplo para que você veja o resultado imediatamente.  
* Configurar `ExportTableOptions` para que cada célula seja tratada como string.  
* Exportar um intervalo retangular para um `DataTable` preservando a primeira linha como cabeçalhos de coluna.  
* Verificar a saída e imprimir a primeira linha no console.  

Nenhum link externo de documentação é necessário — tudo que você precisa está aqui. Se já possuir um arquivo Excel no disco, basta substituir a linha de criação da workbook por `new Workbook("path/to/file.xlsx")` e pronto.

---

## Etapa 1: Configurar o Projeto e Adicionar o Pacote NuGet Aspose.Cells

Antes de escrever qualquer código, certifique‑se de que seu projeto referencia **Aspose.Cells for .NET** (a biblioteca que fornece a classe `Workbook`). Você pode adicioná‑la via NuGet Package Manager:

```bash
dotnet add package Aspose.Cells
```

> **Dica de especialista:** Use a versão estável mais recente (em março 2026, é 22.12) para obter as correções de bugs e melhorias de desempenho mais recentes.

---

## Etapa 2: Criar uma Workbook e Preenchê‑la com Dados de Exemplo

Começaremos com uma `Workbook` novinha em folha e escreveremos algumas linhas para que você veja a exportação em ação. Esta etapa também demonstra **como exportar excel para datatable** quando os dados de origem vivem apenas na memória.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*Por que isso importa:* Ao inserir a linha de cabeçalho primeiro (`A1` & `B1`), podemos posteriormente instruir o exportador a tratar a primeira linha como nomes de coluna — exatamente o que **export excel with column names** significa.

---

## Etapa 3: Instruir o Aspose.Cells a Tratar Cada Célula como String

Ao exportar células numéricas ou de data, o Aspose tenta inferir o tipo .NET. Isso pode causar bugs sutis se seu código posterior esperar strings. A flag `ExportTableOptions.ExportAsString` força uma conversão uniforme para string.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*Por que usar isso?* Imagine uma coluna que às vezes contém números e às vezes texto (ex.: “00123” vs. “ABC”). Exportando tudo como string, você evita perder zeros à esquerda ou disparar exceções de conversão de tipo.

---

## Etapa 4: Exportar o Intervalo Desejado para um DataTable

Agora realmente **exportamos excel para datatable**. O método `ExportDataTable` recebe a linha/coluna inicial, o número de linhas/colunas, uma flag para extração de nomes de coluna e as opções que acabamos de criar.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*O que está acontecendo nos bastidores?*  
- `startRow: 0` aponta para a primeira linha do Excel (a linha de cabeçalho).  
- `exportColumnNames: true` indica ao Aspose que ele deve elevar “Name” e “Age” para a coleção de colunas do `DataTable`.  
- `totalRows`/`totalColumns` podem ser maiores que os dados reais; células excedentes tornam‑se strings vazias por causa de `ExportAsString`.

---

## Etapa 5: Verificar o Resultado – Imprimir a Primeira Linha

Um rápido dump no console prova que a conversão funcionou e que os nomes das colunas permanecem intactos.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Saída esperada**

```
First row: Alice, 30
```

Se você alterar os dados de exemplo, o console refletirá essas mudanças automaticamente — sem código extra necessário.

---

## Perguntas Frequentes & Casos de Borda

| Pergunta | Resposta |
|----------|----------|
| **Posso exportar uma planilha que já existe no disco?** | Sim — substitua `new Workbook()` por `new Workbook("myFile.xlsx")`. O restante das etapas permanece idêntico. |
| **E se meu arquivo Excel contiver células mescladas?** | Células mescladas são descompactadas; o valor da célula superior‑esquerda é usado para todo o intervalo mesclado. |
| **Preciso me preocupar com formatos numéricos específicos de cultura?** | Não quando `ExportAsString = true`; tudo chega como a string bruta exibida no Excel. |
| **Quantas linhas posso exportar de uma vez?** | Aspose.Cells pode lidar com milhões de linhas, mas o consumo de memória cresce com o tamanho do `DataTable`. Considere paginação se atingir limites. |
| **E colunas ocultas?** | Colunas ocultas são exportadas a menos que você defina `ExportHiddenColumns = false` em `ExportTableOptions`. |

---

## Bônus: Exportando para CSV ao Invés de DataTable

Às vezes você pode preferir um arquivo plano. As mesmas `ExportTableOptions` podem ser reutilizadas com `ExportDataTableToCSV`:

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

Essa única linha gera um CSV pronto para importação enquanto ainda **exporta dados do Excel como string**.

---

## Exemplo Completo (Pronto para Copiar‑Colar)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

Execute o programa (`dotnet run`) e você verá o resultado do **export excel to datatable** impresso no console. Troque os dados de exemplo, altere `totalRows`/`totalColumns` ou aponte a workbook para um arquivo real — tudo escala.

---

## Conclusão

Agora você tem uma **solução completa e autocontida para exportar Excel para DataTable** em C#. Ao configurar `ExportTableOptions.ExportAsString` você garante que **export excel data as string**, e ao definir `exportColumnNames: true` obtém os cabeçalhos de coluna familiares que espera ao **exportar excel com nomes de colunas**.  

A partir daqui você pode:

* Alimentar o `DataTable` no Entity Framework ou Dapper para inserções em lote.  
* Passá‑lo para um motor de relatórios como **FastReport** ou **RDLC**.  
* Convertê‑lo para JSON em uma resposta de API (`JsonConvert.SerializeObject(table)`).

Sinta‑se à vontade para experimentar — talvez tente exportar uma planilha maior, ou combinar isso com **como exportar excel para datatable** a partir de um compartilhamento de rede. O padrão permanece o mesmo, e o código está pronto para produção.

---

![Diagrama do fluxo de conversão Excel → DataTable – export excel to datatable](https://example.com/placeholder.png "diagrama export excel to datatable")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}