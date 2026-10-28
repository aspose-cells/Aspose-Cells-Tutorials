---
category: general
date: 2026-03-25
description: Crie uma nova planilha em C# e aprenda a usar EXPAND, calcular a cotangente
  e salvar a planilha em um arquivo com código passo a passo.
draft: false
keywords:
- create new workbook
- save workbook to file
- how to use expand
- how to calculate cotangent
- how to save excel
language: pt
og_description: Crie uma nova planilha em C# e veja instantaneamente como usar EXPAND,
  calcular a cotangente e salvar a planilha em um arquivo.
og_title: Criar nova pasta de trabalho em C# – Guia completo de programação
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Criar nova pasta de trabalho em C# – Guia completo de programação
url: /pt/net/workbook-operations/create-new-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar nova pasta de trabalho em C# – Guia de Programação Completo

Já precisou **criar nova pasta de trabalho** em C# mas não sabia por onde começar? Você não está sozinho. Seja automatizando um pipeline de relatórios ou apenas brincando com fórmulas do Excel em código, a capacidade de gerar uma pasta de trabalho, inserir fórmulas como `EXPAND` ou `COT`, e então **salvar a pasta de trabalho em um arquivo** é uma habilidade essencial para qualquer desenvolvedor .NET.

Neste tutorial vamos percorrer um exemplo do mundo real que faz exatamente isso: vamos instanciar uma nova pasta de trabalho, usar a função `EXPAND` para transformar um array estático em uma coluna dinâmica, calcular a cotangente com a função `COT` e, finalmente, **salvar a pasta de trabalho em um arquivo** como `.xlsx`. Ao final, você terá um trecho pronto para executar, entenderá *por que* cada chamada é importante e verá algumas variações úteis para casos extremos.

> **Dica profissional:** Todo o código abaixo funciona com a versão mais recente do Aspose.Cells para .NET (a partir de março 2026). Se você estiver usando uma versão mais antiga, a superfície da API é praticamente a mesma, mas verifique novamente as importações de namespace.

## O que você precisará

- .NET 6.0 ou posterior (o exemplo tem como alvo .NET 6, mas .NET 5 também funciona)  
- Aspose.Cells para .NET instalado via NuGet (`Install-Package Aspose.Cells`)  
- Um conhecimento razoável de C# (você tem isso)  

É isso—nenhum DLL extra, sem interop COM, e certamente sem Excel instalado na máquina. Pronto? Vamos mergulhar.

![Screenshot showing how to create new workbook in C#](assets/create-new-workbook.png){alt="Captura de tela mostrando como criar nova pasta de trabalho em C#"}

## Etapa 1: Criar uma nova pasta de trabalho

A primeira coisa que você deve fazer é instanciar a classe `Workbook`. Pense nisso como abrir um arquivo Excel em branco na memória. Esse objeto contém uma coleção de planilhas, estilos e tudo o mais que você precisará depois.

```csharp
using Aspose.Cells;

class ExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // <-- creates an empty .xlsx structure
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

Por que obter a primeira planilha imediatamente? A maioria dos exemplos rápidos trabalha com uma única planilha, e o acessador `Worksheets[0]` é a maneira mais rápida de obter uma referência sem percorrer. Se precisar de várias planilhas depois, pode adicioná‑las com `workbook.Worksheets.Add()`.

## Etapa 2: Como usar EXPAND para gerar intervalos dinâmicos

`EXPAND` é uma função mais recente do Excel que recebe um array e o preenche até um tamanho especificado. No nosso código, vamos expandir o array literal `{1,2,3}` em uma **coluna de 5 linhas** começando na célula `A1`. A sintaxe dentro da string é exatamente o que você digitária no Excel, então você pode copiar‑colar diretamente em uma célula depois, se desejar.

```csharp
        // Step 2: Apply EXPAND to turn {1,2,3} into a 5‑row vertical range
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // rows=5, cols=1
```

### O que está acontecendo nos bastidores?

- `{1,2,3}` é um literal de array horizontal.  
- O segundo argumento (`5`) indica ao Excel para expandir o array para **5 linhas**.  
- O terceiro argumento (`1`) força uma saída de **uma única coluna**.  

Se você omitir o terceiro argumento, o Excel tentará preservar a forma original, o que pode gerar um bloco 5×3 em vez de uma única coluna. Essa é uma armadilha comum quando se experimenta `EXPAND` pela primeira vez.

#### Variações que você pode precisar

| Forma desejada | Exemplo de fórmula |
|---------------|-----------------|
| bloco de 3 linhas, 2 colunas | `=EXPAND({1,2,3},3,2)` |
| Preencher apenas para baixo (mesma coluna) | `=EXPAND({10,20},10,1)` |
| Expandir para um número maior de colunas | `=EXPAND({5},5,4)` |

Sinta‑se à vontade para trocar os literais ou as dimensões para combinar com a lógica de geração de dados.

## Etapa 3: Como calcular a cotangente com a função COT

A função `COT` retorna a cotangente de um ângulo expresso em radianos. No nosso exemplo calculamos a cotangente de 45° (π/4 radianos). O resultado, `1`, aparece na célula `B1`.

```csharp
        // Step 3: Use COT to calculate cotangent of 45 degrees (π/4 radians)
        ws.Cells["B1"].Formula = "=COT(PI()/4)"; // PI() returns π, divided by 4 = 45°
```

### Por que usar COT em vez de calcular manualmente?

O Excel já sabe como lidar com a conversão trigonométrica, então você evita erros de arredondamento de ponto flutuante que podem surgir se você tentar `1 / TAN(angle)`. Além disso, a fórmula permanece legível para quem revisar a planilha depois.

#### Caso extremo: ângulos além de 0‑360°

Se você fornecer um ângulo maior que `2*PI()` (ou um negativo), o Excel o envolverá automaticamente, mas o resultado pode ser surpreendente. Para garantir, talvez você queira normalizar o ângulo primeiro:

```csharp
        // Normalize angle to 0‑2π range before applying COT
        ws.Cells["C1"].Formula = "=COT(MOD(PI()*3, 2*PI()))";
```

Esse trecho demonstra como combinar `MOD` com `COT` para cálculos robustos.

## Etapa 4: Como salvar a pasta de trabalho em um arquivo (Excel)

Agora que as fórmulas estão no lugar, o passo final é **salvar a pasta de trabalho em um arquivo**. Você pode escolher qualquer caminho que desejar—apenas certifique-se de que o diretório exista e que você tenha permissões de gravação.

```csharp
        // Step 4 (optional): Save the workbook so you can inspect the results
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### O que realmente é salvo?

Quando você abrir `output.xlsx` no Excel, verá:

| A | B |
|---|---|
| 1 | 1 |
| 2 |   |
| 3 |   |
|   |   |
|   |   |

- A coluna **A** contém o array expandido `{1,2,3}` seguido de duas células vazias (porque solicitamos 5 linhas).  
- A célula **B1** mostra `1`, a cotangente de 45°.

Se você atualizar a pasta de trabalho (pressionar `F9` ou habilitar cálculo automático), o Excel avaliará as fórmulas e exibirá os resultados. O Aspose.Cells também oferece o método `CalculateFormula` caso você precise dos valores sem abrir o Excel:

```csharp
        workbook.CalculateFormula();
        double cotResult = ws.Cells["B1"].DoubleValue; // should be 1.0
```

## Perguntas Frequentes & Armadilhas

| Pergunta | Resposta |
|----------|----------|
| **Preciso habilitar o cálculo manualmente?** | Não. Por padrão o Aspose.Cells salva as fórmulas como‑estão; o Excel as calculará ao abrir. Use `workbook.CalculateFormula()` para pré‑cálculo. |
| **Posso escrever fórmulas em várias células de uma vez?** | Com certeza. Use `ws.Cells["D1:D5"].Formula = "=RAND()"` para preencher um intervalo com números aleatórios. |
| **E se a pasta de destino não existir?** | Crie-a primeiro: `Directory.CreateDirectory(Path.GetDirectoryName(outputPath));` |
| **O `EXPAND` é suportado em versões mais antigas do Excel?** | `EXPAND` chegou com o Excel 365/2019. Se precisar de compatibilidade com arquivos mais antigos, considere usar combinações de `INDEX`/`SEQUENCE`. |
| **Como ocultar a visualização da fórmula?** | Defina `ws.Cells["A1"].FormulaHidden = true;` e proteja a planilha se não quiser que os usuários vejam a fórmula subjacente. |

## Conclusão

Agora você sabe **como criar novos objetos de pasta de trabalho** em C#, aproveitar o poder da função `EXPAND` para gerar arrays dinâmicos, calcular a cotangente com `COT` e **salvar a pasta de trabalho em um arquivo** como um documento Excel organizado. O exemplo completo e executável está nos trechos de código acima—copie‑o para um aplicativo console, pressione `F5` e abra o `output.xlsx` resultante para ver a mágica.

### O que vem a seguir?

- **Explore outras funções de array dinâmico** como `SEQUENCE`, `FILTER` e `SORT`.  
- **Automatize a criação de gráficos** com a rica API de gráficos do Aspose.Cells.  
- **Integre com fontes de dados** (SQL, CSV) e alimente esses valores nas fórmulas programaticamente.  
- **Aprenda a salvar o Excel como PDF** ou outros formatos—perfeito para pipelines de relatórios.  

Sinta‑se à vontade para experimentar: altere os valores do array, ajuste o ângulo ou escreva o resultado em outra planilha. O céu é o limite quando você combina C# com o motor de fórmulas moderno do Excel.

Feliz codificação, e que suas planilhas sempre calculem corretamente!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}