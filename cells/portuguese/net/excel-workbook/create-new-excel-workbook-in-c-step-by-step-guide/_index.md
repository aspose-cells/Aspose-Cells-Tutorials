---
category: general
date: 2026-02-15
description: Criar uma nova pasta de trabalho do Excel e aprender a usar EXPAND, expandir
  uma sequência e calcular a cotangente. Também veja como salvar a pasta de trabalho
  em um arquivo.
draft: false
keywords:
- create new excel workbook
- save workbook to file
- how to use expand
- how to expand sequence
- how to calculate cotangent
language: pt
og_description: Crie uma nova pasta de trabalho do Excel com C#. Aprenda a usar EXPAND,
  expandir uma sequência, calcular a cotangente e salvar a pasta de trabalho em um
  arquivo.
og_title: Criar nova pasta de trabalho do Excel em C# – Guia completo de programação
tags:
- C#
- Aspose.Cells
- Excel automation
title: Criar nova pasta de trabalho Excel em C# – Guia passo a passo
url: /pt/net/excel-workbook/create-new-excel-workbook-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar nova pasta de trabalho Excel em C# – Guia de Programação Completo

Já precisou **criar nova pasta de trabalho Excel** a partir do código e não sabia por onde começar? Você não está sozinho; muitos desenvolvedores encontram essa barreira ao automatizar relatórios ou construir pipelines de dados. Neste tutorial vamos mostrar exatamente como criar nova pasta de trabalho Excel, escrever algumas fórmulas interessantes e então **salvar a pasta de trabalho em arquivo** para inspeção posterior.  

Também vamos nos aprofundar nos detalhes da função `EXPAND`, demonstrar **como usar expand** para transformar uma sequência pequena em um grande bloco, explicar **como expandir sequência** na prática e, por fim, revelar **como calcular cotangente** diretamente dentro do Excel. Ao final, você terá um programa C# executável que pode ser inserido em qualquer projeto .NET.

## O que você precisará

- **Aspose.Cells for .NET** (versão de avaliação gratuita ou licenciada) – a biblioteca que nos permite manipular Excel sem precisar do Office instalado.  
- **.NET 6+** (ou .NET Framework 4.6+).  
- Um IDE modesto, como Visual Studio 2022, VS Code ou Rider.  

Nenhum pacote NuGet adicional é necessário além do `Aspose.Cells`. Se ainda não o tem, execute:

```bash
dotnet add package Aspose.Cells
```

É só isso—não há mais nada a configurar.

## Etapa 1: Criar uma nova pasta de trabalho Excel

A primeira coisa que fazemos é instanciar um objeto `Workbook`. Pense nele como a tela em branco onde todas as planilhas, células e fórmulas viverão.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // default sheet is named "Sheet1"
```

> **Por que isso importa:** Criar a pasta de trabalho na memória significa que nunca tocamos o disco até decidirmos explicitamente **salvar a pasta de trabalho em arquivo**. Isso mantém a operação rápida e permite encadear modificações adicionais sem overhead de I/O.

## Etapa 2: Como usar EXPAND para expandir uma sequência

`EXPAND` é uma função mais recente do Excel que recebe um array menor e o estica para um tamanho definido. No nosso exemplo começamos com uma sequência vertical de três linhas e a transformamos em um bloco 5 × 5.

```csharp
        // Step 2: Write a formula that expands a 3‑row sequence into a 5×5 block
        // The formula lives in A1 and will spill over to E5
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3),5,5)";
```

> **Explicação:** `SEQUENCE(3)` produz `{1;2;3}` (um array vertical). `EXPAND(...,5,5)` indica ao Excel para repetir esse array até preencher um retângulo de 5 linhas por 5 colunas, começando em A1. O resultado é uma matriz onde cada coluna repete os três números originais, e as duas últimas linhas ficam vazias porque a fonte tem apenas três linhas.

### Saída esperada

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 1 |
| 2 | 2 | 2 | 2 | 2 |
| 3 | 3 | 3 | 3 | 3 |
|   |   |   |   |   |
|   |   |   |   |   |

Você verá o mesmo padrão se espalhando pela faixa assim que a pasta de trabalho for aberta no Excel.

## Etapa 3: Como calcular cotangente no Excel

A maioria das pessoas está familiarizada com `SIN`, `COS` e `TAN`, mas `COT` é um atalho útil para o recíproco da tangente. Aqui está como obter a cotangente de 45° (que equivale a 1) usando radianos.

```csharp
        // Step 3: Write a formula that returns the cotangent of 45° (π/4 radians)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

> **Por que usar COT?** Chamar diretamente `COT` evita a divisão extra que seria necessária com `1/TAN(...)`, tornando a fórmula mais clara e ligeiramente mais rápida em planilhas grandes.

## Etapa 4: Avaliar todas as fórmulas

Aspose.Cells não calcula fórmulas automaticamente a menos que você solicite. O método `CalculateFormula` força uma avaliação completa para que os valores resultantes sejam armazenados nas células.

```csharp
        // Step 4: Evaluate all formulas so the results are stored in the cells
        workbook.CalculateFormula();
```

> **Dica:** Se você tem muitas fórmulas custosas, pode passar um objeto `CalculationOptions` para ajustar o desempenho (por exemplo, habilitar multithreading).

## Etapa 5: Salvar a pasta de trabalho em arquivo

Agora que tudo está pronto, finalmente **salvamos a pasta de trabalho em arquivo**. Escolha uma pasta onde você tenha permissão de escrita e dê ao arquivo um nome significativo.

```csharp
        // Step 5: Save the workbook to a file for inspection
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **O que acontece no disco?** A chamada `Save` grava um pacote `.xlsx` totalmente formado, completo com o array expandido de `EXPAND` e o valor de cotangente calculado. Abra o arquivo no Excel e você verá o bloco 5 × 5 começando em A1 e o número `1` em B1.

![Excel output showing expanded sequence and cotangent value](excel-output.png "create new excel workbook example output")

*Image alt text: create new excel workbook example output*

### Verificação rápida

1. Abra `output.xlsx`.  
2. Verifique se as células **A1:E5** contêm o padrão repetido 1‑2‑3.  
3. Observe **B1** – deve exibir `1`.  

Se tudo corresponder, parabéns—você automatizou o Excel com sucesso!

## Como expandir sequência em outros cenários

Embora o exemplo acima use um `SEQUENCE(3)` estático, você pode substituí‑lo facilmente por um intervalo dinâmico ou outra fórmula:

```csharp
// Expand a dynamic range from D1:D10 to a 4×4 block
worksheet.Cells["F1"].Formula = "=EXPAND(D1:D10,4,4)";
```

**Quando usar?**  
- Gerar tabelas placeholder para modelos.  
- Replicar rapidamente uma linha de cabeçalho em várias colunas.  
- Construir grades de mapa de calor sem copiar‑colar manual.

## Armadilhas comuns e como evitá‑las

| Armadilha | Por que acontece | Solução |
|----------|------------------|---------|
| `#VALUE!` após `EXPAND` | O array de origem não é um intervalo adequado (ex.: contém erros) | Limpe os dados de origem ou envolva‑os em `IFERROR`. |
| Cotangente retorna `#DIV/0!` para 0° | `COT(0)` é matematicamente infinito | Proteja com `IF(PI()/4=0,0,COT(...))`. |
| Pasta de trabalho não salva | Caminho inválido ou falta permissão de escrita | Use `Path.GetFullPath` e verifique se a pasta existe. |
| Fórmulas não calculadas | `CalculateFormula` omitido | Sempre chame antes de `Save`. |

## Bônus: Adicionando estilo (opcional)

Se quiser que a saída fique mais agradável, pode aplicar um estilo simples após os cálculos:

```csharp
        // Apply a light gray background to the expanded block
        Style style = workbook.CreateStyle();
        style.Pattern = BackgroundType.Solid;
        style.ForegroundColor = System.Drawing.Color.LightGray;
        StyleFlag flag = new StyleFlag { CellShading = true };
        worksheet.Cells.CreateRange("A1:E5").ApplyStyle(style, flag);
```

Este trecho é opcional, mas ilustra como combinar a lógica de **criar nova pasta de trabalho Excel** com formatação em uma única passagem.

## Recapitulação

Percorremos todo o processo:

1. **Criar nova pasta de trabalho Excel** com Aspose.Cells.  
2. Usar **como usar expand** para transformar um pequeno `SEQUENCE` em uma matriz 5 × 5.  
3. Mostrar **como calcular cotangente** diretamente em uma célula.  
4. Forçar o cálculo com `CalculateFormula`.  
5. **Salvar a pasta de trabalho em arquivo** e verificar o resultado.

Tudo isso é autocontido, roda em qualquer runtime .NET recente e requer apenas um pacote NuGet.

## O que vem a seguir?

- **Fontes de dados dinâmicas:** Buscar dados de um banco e alimentá‑los em `EXPAND`.  
- **Múltiplas planilhas:** Percorrer uma coleção de sheets para gerar um livro de relatório completo.  
- **Fórmulas avançadas:** Explorar `LET`, `LAMBDA` ou lógica condicional baseada em arrays para planilhas mais inteligentes.  

Sinta‑se à vontade para experimentar—troque o argumento de `SEQUENCE`, teste ângulos diferentes para `COT` ou combine com geração de gráficos. O céu é o limite quando você pode **criar nova pasta de trabalho Excel** programaticamente.

---

*Feliz codificação! Se encontrou algum problema, deixe um comentário abaixo ou me chame no Twitter @YourHandle. Ficarei feliz em ajudar.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}