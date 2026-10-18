---
category: general
date: 2026-03-21
description: Criar uma pasta de trabalho do Excel e importar a tabela de dados para
  o Excel definindo o estilo da coluna, exportar os dados para o Excel e formatar
  a data das células do Excel em minutos.
draft: false
keywords:
- create excel workbook
- import datatable to excel
- set column style
- export data to excel
- format excel cells date
language: pt
og_description: Crie rapidamente uma pasta de trabalho do Excel. Aprenda a importar
  datatable para o Excel, definir o estilo das colunas, exportar dados para o Excel
  e formatar datas nas células do Excel em um único guia.
og_title: Criar Pasta de Trabalho Excel – Tutorial Completo de Estilização e Exportação
tags:
- C#
- Aspose.Cells
- Excel automation
title: Criar Pasta de Trabalho do Excel com Tabela Estilizada – Guia Passo a Passo
url: /pt/net/excel-workbook/create-excel-workbook-with-styled-table-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pasta de Trabalho Excel – Tutorial de Programação Completo

Já precisou **create excel workbook** que pareça polido direto do código? Talvez você esteja extraindo dados de um banco de dados e queira que as datas apareçam no formato correto sem ter que mexer no Excel depois. Esse é um ponto de dor comum—especialmente quando o resultado chega na caixa de entrada de um cliente e ele espera que tudo esteja pronto para uso.

Neste guia vamos percorrer uma solução única e autocontida que **imports datatable to excel**, aplica um **set column style** e, finalmente, **export data to excel** como um arquivo bem formatado. Você verá exatamente como **format excel cells date** para que a planilha se pareça com um relatório profissional, e receberá um exemplo completo e executável ao final. Sem peças faltando, sem atalhos “veja a documentação”—apenas código puro que você pode inserir no seu projeto hoje.

---

## O que você aprenderá

- Como **create excel workbook** usando a biblioteca Aspose.Cells (ou qualquer API compatível).
- A maneira mais rápida de **import datatable to excel** sem loops manuais célula por célula.
- Técnicas para **set column style**, incluindo a aplicação de um formato de data a uma coluna específica.
- Como **export data to excel** com uma única chamada `Save`.
- Armadilhas comuns ao tentar **format excel cells date** e como evitá‑las.

### Pré‑requisitos

- .NET 6+ (ou .NET Framework 4.6+).  
- Aspose.Cells for .NET instalado (`Install-Package Aspose.Cells`).  
- Um `DataTable` pronto para ser exportado—sua fonte de dados pode ser SQL, CSV ou qualquer coisa que possa ser convertida em um `DataTable`.

Se você já está confortável com C# e tem esses itens em mãos, está pronto para começar. Caso contrário, a seção “Pré‑requisitos” acima fornece uma lista rápida para você conferir.

---

## Etapa 1 – Criar a Instância da Pasta de Trabalho Excel

A primeira coisa que você faz quando quer **create excel workbook** programaticamente é instanciar o objeto workbook. Pense nisso como abrir um caderno em branco onde você escreverá seus dados mais tarde.

```csharp
using Aspose.Cells;
using System.Data;

// Step 1: Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();
```

> **Por que isso importa:**  
> A classe `Workbook` é o ponto de entrada para toda operação no Aspose.Cells. Criá‑la antecipadamente fornece uma tela limpa, e você pode carregar um arquivo existente depois, se precisar acrescentar dados em vez de começar do zero.

---

## Etapa 2 – Preparar o DataTable para Importar

Antes de podermos **import datatable to excel**, precisamos de um `DataTable`. Em projetos reais isso costuma vir de `SqlDataAdapter.Fill` ou `DataTable.Load`. Para fins de clareza, vamos criar um método que devolve uma tabela pronta.

```csharp
// Step 2: Obtain the data to be written – a DataTable with three columns
DataTable dataTable = GetData();   // assume GetData() returns the required table

// Example implementation (you can replace this with your own data source)
DataTable GetData()
{
    DataTable dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Quantity", typeof(int));

    dt.Rows.Add(DateTime.Today.AddDays(-2), "Apples", 120);
    dt.Rows.Add(DateTime.Today.AddDays(-1), "Bananas", 85);
    dt.Rows.Add(DateTime.Today, "Cherries", 60);
    return dt;
}
```

> **Dica:** Se suas datas estiverem armazenadas como strings, converta‑as para `DateTime` primeiro—caso contrário a etapa **format excel cells date** não funcionará como esperado.

---

## Etapa 3 – Definir Estilos para Cada Coluna (Set Column Style)

Agora vem a parte em que **set column style**. Criaremos um array de objetos `Style`—um por coluna. A primeira coluna recebe um formato de data embutido (código 14), enquanto as demais permanecem com o formato geral (código 0).

```csharp
// Step 3: Define a style for each column; apply a date format to the first column
Style[] columnStyles = new Style[3];
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = workbook.CreateStyle();
    columnStyles[i].Number = (i == 0) ? 14 : 0;   // 14 = date format, 0 = general
}
```

> **Por que usar objetos de estilo?**  
> Aplicar um estilo uma única vez e reutilizá‑lo é muito mais eficiente do que definir o formato em cada célula individualmente. Também garante que toda a coluna siga a mesma regra **format excel cells date**, o que é essencial para consistência quando o arquivo for aberto em diferentes localidades.

---

## Etapa 4 – Importar o DataTable com Estilos na Worksheet

Com o workbook pronto e os estilos definidos, agora **import datatable to excel**. O método `ImportDataTable` faz o trabalho pesado: grava os cabeçalhos das colunas, as linhas e aplica os estilos que passamos.

```csharp
// Step 4: Access the first worksheet and import the DataTable using the styles
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

> **O que está acontecendo nos bastidores?**  
> - `true` indica ao Aspose.Cells que inclua os nomes das colunas na primeira linha.  
> - `0, 0` são os índices de linha e coluna iniciais (canto superior esquerdo).  
> - `columnStyles` alinha cada coluna ao estilo que preparamos, garantindo que a regra **format excel cells date** seja aplicada à coluna de data.

---

## Etapa 5 – Salvar (Exportar) o Workbook para um Arquivo Físico

Finalmente, **export data to excel** salvando o workbook no disco. Você pode mudar o caminho para qualquer pasta que desejar, ou até mesmo transmitir o arquivo diretamente como resposta HTTP em uma API web.

```csharp
// Step 5: Save the workbook with the styled table
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

> **Pro dica:** Use `workbook.Save(Stream, SaveFormat.Xlsx)` quando precisar enviar o arquivo pela rede sem gravá‑lo no disco.

---

## Exemplo Completo Funcionando (Todas as Etapas Combinadas)

Abaixo está o programa completo, pronto‑para‑executar. Copie‑e‑cole em um aplicativo console, ajuste o caminho de saída e você terá um arquivo Excel bem formatado em segundos.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Get the data (replace GetData with your own source if needed)
        DataTable dataTable = GetData();

        // 3️⃣ Prepare column styles – date format for the first column
        Style[] columnStyles = new Style[3];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            columnStyles[i] = workbook.CreateStyle();
            columnStyles[i].Number = (i == 0) ? 14 : 0;   // 14 = date, 0 = general
        }

        // 4️⃣ Import the DataTable with the styles
        Worksheet worksheet = workbook.Worksheets[0];
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 5️⃣ Save the file
        workbook.Save("StyledTable.xlsx");

        Console.WriteLine("Excel workbook created successfully!");
    }

    // Sample data generator – replace with real data source
    static DataTable GetData()
    {
        DataTable dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(DateTime.Today.AddDays(-2), "Apples", 120);
        dt.Rows.Add(DateTime.Today.AddDays(-1), "Bananas", 85);
        dt.Rows.Add(DateTime.Today, "Cherries", 60);
        return dt;
    }
}
```

**Saída esperada:**  
Ao abrir `StyledTable.xlsx`, a coluna A mostra datas como `03/19/2026` (dependendo da sua localidade), enquanto as colunas B e C exibem os nomes dos produtos e quantidades como texto/números simples. Nenhum passo extra de formatação é necessário—seu processo **create excel workbook** está concluído.

---

## Perguntas Frequentes & Casos de Borda

### 1️⃣ E se meu DataTable tiver mais de três colunas?
Adicione mais objetos `Style` ao array `columnStyles` e ajuste a propriedade `Number` para qualquer coluna que precise de um formato especial (por exemplo, moeda, porcentagem). O método `ImportDataTable` combinará cada estilo pela posição.

### 2️⃣ Posso aplicar um formato de data personalizado em vez do embutido 14?
Com certeza. Substitua `columnStyles[i].Number = 14;` por:

```csharp
columnStyles[i].Number = 22;               // built‑in custom format ID
columnStyles[i].Custom = "dd‑MMM‑yyyy";    // or any .NET date pattern you like
```

### 3️⃣ Como **export data to excel** em uma API web sem gravar no disco?
Use um `MemoryStream`:

```csharp
using (var ms = new MemoryStream())
{
    workbook.Save(ms, SaveFormat.Xlsx);
    ms.Position = 0;
    // return File(ms.ToArray(), "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "Report.xlsx");
}
```

### 4️⃣ E se a localidade do usuário esperar um separador de data diferente?
O formato de data embutido (ID 14) respeita as configurações de localidade do workbook. Se precisar de um formato fixo independente da localidade, use a propriedade `Custom` como mostrado acima.

### 5️⃣ Isso funciona com .NET Core?
Sim—Aspose.Cells suporta .NET Standard 2.0 e posteriores, então o mesmo código roda no .NET 6, .NET 7 ou qualquer runtime compatível.

---

## Dicas de Melhores Práticas (Pro Tips)

- **Reutilize estilos**: Criar um estilo por coluna é barato, mas reutilizar o mesmo objeto de estilo para colunas idênticas economiza memória.
- **Evite loops célula por célula**: `ImportDataTable` é altamente otimizado; loops manuais são mais lentos e propensos a erros.
- **Defina a cultura do workbook cedo** se precisar de separadores consistentes de número/data em todos os ambientes:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

- **Valide o DataTable** antes da importação—datas nulas lançarão exceção quando o estilo de data for aplicado.
- **Ative o cálculo** se você adicionar fórmulas após a importação:

```csharp
workbook.CalculateFormula();
```

---

## Conclusão

Agora você tem uma receita completa, de ponta a ponta, para **create excel workbook**, **import datatable to excel**, **set column style**, **export data to excel** e **format excel cells date**—tudo em menos de uma dúzia de linhas de código C#. A abordagem é rápida, confiável e mantém as preocupações de formatação dentro do código, de modo que a planilha final esteja pronta para os usuários de negócios assim que for aberta.

Pronto para o próximo desafio? Experimente adicionar formatação condicional, inserir gráficos ou converter o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}