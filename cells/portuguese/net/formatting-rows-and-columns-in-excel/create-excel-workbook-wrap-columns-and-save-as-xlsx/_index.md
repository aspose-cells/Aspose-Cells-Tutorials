---
category: general
date: 2026-04-07
description: Criar pasta de trabalho Excel, ajustar colunas no Excel, calcular fórmulas
  e salvar a pasta de trabalho como XLSX com código C# passo a passo.
draft: false
keywords:
- create excel workbook
- wrap columns in excel
- save workbook as xlsx
- how to calculate formulas
- how to save excel
language: pt
og_description: Crie uma pasta de trabalho do Excel, ajuste a quebra de texto nas
  colunas, calcule fórmulas e salve a pasta de trabalho como XLSX. Aprenda todo o
  processo com código executável.
og_title: Criar Pasta de Trabalho do Excel – Guia Completo de C#
tags:
- csharp
- aspnet
- excel
- automation
title: Criar Pasta de Trabalho do Excel – Ajustar Texto nas Colunas e Salvar como
  XLSX
url: /pt/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pasta de Trabalho Excel – Envolver Colunas e Salvar como XLSX

Já precisou **criar pasta de trabalho Excel** programaticamente e se perguntou como fazer os dados se ajustarem bem a um layout de múltiplas colunas? Você não está sozinho. Neste tutorial vamos percorrer a criação da pasta de trabalho, aplicar a fórmula `WRAPCOLS` para **envelopar colunas no Excel**, forçar o motor a calcular o resultado e, finalmente, **salvar a pasta de trabalho como XLSX** para que você possa abri‑la em qualquer programa de planilha.

Também responderemos às inevitáveis perguntas subsequentes: *Como calculo fórmulas em tempo real?* *E se eu precisar mudar o número de colunas?* e *Existe uma maneira rápida de persistir o arquivo?* Ao final, você terá um trecho de código C# autônomo, pronto‑para‑executar, que faz tudo isso e algumas dicas extras que você pode copiar para seus próprios projetos.

## Pré-requisitos

- .NET 6.0 ou posterior (o código funciona também no .NET Framework 4.6+)
- A biblioteca **Aspose.Cells** (ou qualquer outro pacote de processamento Excel que suporte `WRAPCOLS`; o exemplo usa Aspose.Cells porque expõe um método simples `CalculateFormula`)
- Um nível razoável de experiência em C# – se você consegue escrever `Console.WriteLine`, está pronto para prosseguir

> **Dica profissional:** Se ainda não tem uma licença para Aspose.Cells, pode solicitar uma chave de avaliação gratuita no site deles; a avaliação funciona perfeitamente para fins de aprendizado.

## Etapa 1: Criar Pasta de Trabalho Excel

A primeira coisa que você precisa é um objeto de pasta de trabalho vazio que representa o arquivo Excel na memória. Isso é o núcleo da operação de **criar pasta de trabalho Excel**.

```csharp
using Aspose.Cells;

// Step 1: Instantiate a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet – it’s already there by default
Worksheet worksheet = workbook.Worksheets[0];
```

*Por que isso importa:* A classe `Workbook` é o ponto de entrada para qualquer manipulação de Excel. Ao criá‑la primeiro, você configura uma tela limpa onde ações subsequentes—como envolver colunas—podem ser aplicadas sem efeitos colaterais.

## Etapa 2: Popular Dados de Exemplo (Opcional, mas Útil)

Antes de envolver colunas, vamos inserir um pequeno conjunto de dados no intervalo `A1:D10`. Isso reflete um cenário real onde você tem uma tabela bruta que precisa ser remodelada.

```csharp
// Fill A1:D10 with sample numbers for demonstration
for (int row = 0; row < 10; row++)
{
    for (int col = 0; col < 4; col++)
    {
        worksheet.Cells[row, col].PutValue(row * 4 + col + 1);
    }
}
```

Você pode pular este bloco se já possuir dados na planilha; a lógica de envolvimento funciona em qualquer intervalo existente.

## Etapa 3: Envolver Colunas no Excel

Agora vem a estrela do espetáculo: a função `WRAPCOLS`. Ela recebe um intervalo de origem e um número de colunas, então distribui os dados pelo novo layout. Veja como aplicá‑la à célula **A1** para que o resultado ocupe três colunas.

```csharp
// Apply WRAPCOLS to A1 – the result will spill into a 3‑column layout
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,3)";
```

**O que está acontecendo nos bastidores?**  
`WRAPCOLS(A1:D10,3)` instrui o Excel a ler as 40 células em `A1:D10` e então escrevê‑las linha a linha em três colunas, criando automaticamente tantas linhas quanto necessário. Isso é perfeito para transformar uma lista longa em uma visualização mais compacta, estilo jornal.

## Etapa 4: Como Calcular Fórmulas

Definir uma fórmula é apenas metade da batalha; o Excel não calculará o resultado até que você acione uma passagem de cálculo. No Aspose.Cells você faz isso com `CalculateFormula()`.

```csharp
// Force the workbook to evaluate all pending formulas
workbook.CalculateFormula();
```

> **Por que você precisa disso:** Sem chamar `CalculateFormula`, a célula `A1` conterá apenas a string da fórmula ao abrir o arquivo, e o layout envolvido não aparecerá até que o usuário recalcule manualmente.

## Etapa 5: Salvar Pasta de Trabalho como XLSX

Finalmente, persista a pasta de trabalho no disco. O método `Save` infere automaticamente o formato a partir da extensão do arquivo, portanto usar **.xlsx** garante que você obtenha o formato Open XML moderno.

```csharp
// Choose a folder you have write access to and save the file
string outputPath = @"C:\Temp\output.xlsx";
workbook.Save(outputPath);
```

Ao abrir `output.xlsx` no Excel, você verá os dados originais elegantemente envolvidos em três colunas, começando na célula **A1**. O restante da planilha permanece intocado, o que é útil se precisar manter a tabela de origem como referência.

### Captura de Tela do Resultado Esperado

<img src="images/wrapcols-result.png" alt="create excel workbook example" />

A imagem acima ilustra o layout final: os números de `A1:D10` agora são exibidos em três colunas, com linhas geradas automaticamente para acomodar todos os valores.

## Variações Comuns & Casos Limite

### Alterando o Número de Colunas

Se precisar de uma contagem de colunas diferente, basta ajustar o segundo argumento de `WRAPCOLS`:

```csharp
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,5)"; // five‑column layout
```

Lembre‑se de executar novamente `CalculateFormula()` após qualquer alteração.

### Envolvendo Intervalos Não Contíguos

`WRAPCOLS` funciona apenas com intervalos contíguos. Se seus dados de origem estiverem divididos em várias áreas, consolide‑os primeiro (por exemplo, usando `UNION` em uma coluna auxiliar) antes de envolver.

### Conjuntos de Dados Grandes

Para tabelas muito grandes, o cálculo pode levar alguns segundos. Você pode melhorar o desempenho desativando o cálculo automático antes de definir a fórmula e reativando‑o depois:

```csharp
workbook.Settings.CalcMode = CalcMode.Manual;
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D1000,4)";
workbook.CalculateFormula();
workbook.Settings.CalcMode = CalcMode.Automatic;
```

### Salvando em um Stream

Se você está construindo uma API web e deseja retornar o arquivo diretamente ao cliente, pode escrever em um `MemoryStream` em vez de um arquivo físico:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // reset for reading
// return ms as a FileResult in ASP.NET Core, for example
```

## Exemplo Completo Funcional

Juntando tudo, aqui está o programa completo, pronto para copiar e colar:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Fill A1:D10 with sample data (optional)
        for (int row = 0; row < 10; row++)
        {
            for (int col = 0; col < 4; col++)
            {
                worksheet.Cells[row, col].PutValue(row * 4 + col + 1);
            }
        }

        // 3️⃣ Apply WRAPCOLS to produce a 3‑column layout
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,3)";

        // 4️⃣ Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // 5️⃣ Save the workbook as XLSX
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Execute este programa, abra o `output.xlsx` gerado, e você verá os dados envolvidos exatamente como descrito.

## Conclusão

Agora você sabe **como criar objetos de pasta de trabalho Excel** em C#, aplicar a poderosa função `WRAPCOLS` para **envolver colunas no Excel**, **calcular fórmulas** sob demanda e **salvar a pasta de trabalho como XLSX** para consumo posterior. Esse fluxo de ponta a ponta cobre os cenários mais comuns, desde demonstrações simples até automação de nível de produção.

### O Que Vem a Seguir?

- Experimente outras funções de matriz dinâmica como `FILTER`, `SORT` ou `UNIQUE`.
- Combine `WRAPCOLS` com formatação condicional para destacar linhas específicas.
- Integre essa lógica em um endpoint ASP.NET Core para que os usuários possam baixar um relatório personalizado com um único clique.

Sinta‑se à vontade para ajustar a contagem de colunas, o intervalo de origem ou o caminho de saída para atender às necessidades do seu projeto. Se encontrar algum problema, deixe um comentário abaixo—bom código!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}