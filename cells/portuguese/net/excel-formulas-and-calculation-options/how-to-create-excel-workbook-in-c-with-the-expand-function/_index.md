---
category: general
date: 2026-10-04
description: Aprenda a criar uma pasta de trabalho Excel em C# e usar EXPAND, forçar
  o cálculo de fórmulas e salvar a pasta de trabalho como XLSX enquanto preenche uma
  coluna com números.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- how to use expand
- force formula calculation
- save workbook as xlsx
- populate column with numbers
language: pt
lastmod: 2026-10-04
og_description: Criar uma pasta de trabalho Excel em C# usando Aspose.Cells. Este
  tutorial mostra como usar EXPAND, forçar o cálculo de fórmulas e salvar a pasta
  de trabalho como XLSX enquanto preenche uma coluna com números.
og_image_alt: Screenshot of a C# program that creates an Excel workbook and applies
  the EXPAND function
og_title: Criar pasta de trabalho Excel em C# – guia completo com EXPAND e salvamento
  em XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to create Excel workbook in C# and use EXPAND, force formula
    calculation, and save workbook as XLSX while populating a column with numbers.
  headline: How to create Excel workbook in C# with the EXPAND function
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Como criar uma pasta de trabalho do Excel em C# com a função EXPAND
url: /pt/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-with-the-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar uma pasta de trabalho Excel em C# com a função EXPAND

Se você precisa **criar uma pasta de trabalho Excel** programaticamente, este guia mostra uma solução completa, pronta‑para‑executar. Você verá como **preencher uma coluna com números**, aplicar a função **EXPAND** para espalhar dados horizontalmente, **forçar o cálculo da fórmula** e, finalmente, **salvar a pasta de trabalho como XLSX**.  

Este tutorial cobre todas as etapas necessárias, desde a inicialização da pasta de trabalho até a verificação do resultado. Nenhuma documentação externa é necessária—basta copiar o código, executá‑lo e você terá um arquivo Excel totalmente funcional.

## Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona com .NET Framework 4.6+)
- Pacote NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Familiaridade básica com a sintaxe C#
- Uma IDE como Visual Studio ou VS Code

## Etapa 1: Criar a pasta de trabalho Excel e acessar a primeira planilha

A primeira ação é **criar a pasta de trabalho Excel** e obter uma referência à sua planilha padrão. O Aspose.Cells adiciona automaticamente uma planilha no índice 0, então você pode trabalhar com ela imediatamente.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();          // create Excel workbook
        Worksheet sheet = workbook.Worksheets[0];   // first (default) worksheet
```

*Por que isso importa:* Instanciar `Workbook` aloca a estrutura interna do arquivo, e recuperar `Worksheets[0]` fornece um objeto `Worksheet` concreto para manipular linhas, colunas e células.

## Etapa 2: Preencher coluna com números

Em seguida, preencha uma lista vertical na coluna A. Isso demonstra **preencher coluna com números** e fornece o intervalo de origem para a função EXPAND.

```csharp
        // Step 2: Fill a vertical list of values in column A
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);
```

*Dica profissional:* Use `PutValue` para números, strings, datas ou qualquer primitivo .NET. O método determina automaticamente o tipo da célula.

## Etapa 3: Como usar EXPAND – espalhar a lista horizontalmente

A parte **como usar expand** é o núcleo deste tutorial. A função `EXPAND` expande um intervalo de origem para uma nova forma. Aqui expandimos o intervalo vertical `A1:A3` para uma única linha que ocupa três colunas, começando em `B1`.

```csharp
        // Step 3: Apply the EXPAND function to spill the list horizontally starting at B1
        // The formula expands the range A1:A3 into 1 row and 3 columns (B1:D1)
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";
```

*Explicação:*  
- O primeiro argumento (`A1:A3`) é o intervalo de origem.  
- O segundo argumento (`1`) força o resultado a ter **1** linha.  
- O terceiro argumento (`3`) força o resultado a ter **3** colunas.  

Quando a pasta de trabalho recalcula, as células `B1`, `C1` e `D1` conterão `1`, `2` e `3`, respectivamente.

## Etapa 4: Forçar o cálculo da fórmula

O Aspose.Cells não avalia automaticamente as fórmulas após você defini‑las, portanto é necessário **forçar o cálculo da fórmula** antes de salvar. Isso garante que o resultado do EXPAND seja materializado no arquivo.

```csharp
        // Step 4: Force calculation of all formulas in the workbook
        workbook.CalculateFormula();   // triggers calculation engine
```

*Por que você precisa disso:* Sem chamar `CalculateFormula`, o arquivo salvo conterá a string da fórmula bruta, e o Excel só recalculará ao abrir o arquivo. Para pipelines automatizados, geralmente você quer que os valores sejam gravados imediatamente.

## Etapa 5: Salvar a pasta de trabalho como XLSX

Agora que a pasta de trabalho está totalmente preparada, **salve a pasta de trabalho como XLSX** em um local de sua escolha. A extensão do arquivo determina o formato de saída; `.xlsx` cria uma pasta de trabalho Office Open XML.

```csharp
        // Step 5: Save the workbook to a file
        string outputPath = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(outputPath);   // save workbook as XLSX
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

*Dica:* Se precisar de um formato diferente (CSV, PDF, etc.), basta mudar a extensão do arquivo ou usar `workbook.Save(outputPath, SaveFormat.Xls)` para versões mais antigas do Excel.

## Exemplo completo, executável

Juntando todas as peças, você obtém um programa autocontido que **cria pasta de trabalho Excel**, preenche uma coluna, usa **EXPAND**, força o cálculo e **salva a pasta de trabalho como XLSX**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create Excel workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2. Populate column with numbers
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // 3. How to use EXPAND – spill horizontally
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";

        // 4. Force formula calculation
        workbook.CalculateFormula();

        // 5. Save workbook as XLSX
        string path = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(path);
        System.Console.WriteLine($"Workbook saved to {path}");
    }
}
```

### Saída esperada

Após executar o programa, abra `ExpandFunction.xlsx` no Excel. Você deverá ver:

| A | B | C | D |
|---|---|---|---|
| 1 | 1 | 2 | 3 |
| 2 |   |   |   |
| 3 |   |   |   |

Os valores `1`, `2`, `3` nas células `B1:D1` confirmam que a função **EXPAND** funcionou e que a etapa **forçar o cálculo da fórmula** materializou os resultados com sucesso.

## Variações comuns e casos de borda

| Cenário | Ajuste |
|----------|------------|
| **Intervalo de origem dinâmico** | Use `=EXPAND(A1:INDEX(A:A, COUNTA(A:A)), 1, 0)` para expandir quantas linhas estiverem preenchidas. |
| **Dimensões de saída diferentes** | Altere os segundo e terceiro argumentos do `EXPAND` para controlar linhas e colunas. |
| **Múltiplas planilhas** | Percorra `workbook.Worksheets` e aplique a mesma lógica a cada planilha. |
| **Conjuntos de dados grandes** | Chame `workbook.CalculateFormula()` uma única vez após definir todas as fórmulas para evitar recalculações repetidas. |
| **Salvar em stream de memória** | Substitua `workbook.Save(path)` por `workbook.Save(stream, SaveFormat.Xlsx)` quando precisar do arquivo em uma resposta de API web. |

## Lista de verificação de solução de problemas

- **Fórmula não está expandindo:** Verifique se `CalculateFormula()` é chamado *depois* de definir a fórmula.  
- **Arquivo não encontrado ao salvar:** Certifique‑se de que o diretório de destino existe e que o processo tem permissão de gravação.  
- **Tipo de dado incorreto:** Use `PutValue` para números; para datas, use `PutValue(DateTime.Now)` ou `PutDateTime`.  
- **Incompatibilidade de versão:** A função EXPAND requer motor de cálculo compatível com Excel 365; Aspose.Cells 23.9+ oferece suporte.

## Conclusão

Agora você sabe como **criar uma pasta de trabalho Excel** em C#, **preencher coluna com números**, aplicar a função **EXPAND**, **forçar o cálculo da fórmula** e **salvar a pasta de trabalho como XLSX**. Este exemplo de ponta a ponta pode ser adaptado para relatórios, transformação de dados ou qualquer cenário de automação que exija saída dinâmica em Excel.

### Próximos passos

- Explore outras funções de matriz dinâmica como `FILTER`, `SORT` e `UNIQUE`.  
- Integre a geração da pasta de trabalho em uma API ASP.NET Core para entregar arquivos Excel sob demanda.  
- Substitua os números fixos por dados lidos de um banco de dados ou arquivo CSV para relatórios do mundo real.

Sinta‑se à vontade para experimentar diferentes intervalos, nomes de planilhas e formatos de saída. Boa codificação!


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Calculate Cotangent in Excel with C# – Create Workbook, Use EXPAND,](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}