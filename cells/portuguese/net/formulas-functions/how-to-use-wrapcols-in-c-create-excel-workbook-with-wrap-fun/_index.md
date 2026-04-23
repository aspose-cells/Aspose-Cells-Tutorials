---
category: general
date: 2026-03-30
description: Aprenda a usar WRAPCOLS em C# para criar uma pasta de trabalho do Excel,
  adicionar dados ao Excel e forçar o cálculo de fórmulas, também usando WRAPROWS.
draft: false
keywords:
- how to use wrapcols
- create excel workbook c#
- add data to excel
- force formula calculation
- how to use wraprows
language: pt
og_description: Descubra como usar WRAPCOLS em C# para criar uma pasta de trabalho
  do Excel, adicionar dados, forçar o cálculo de fórmulas e aproveitar o WRAPROWS
  para fórmulas de matriz.
og_title: Como usar WRAPCOLS em C# – Guia completo
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Como usar WRAPCOLS em C# – Criar pasta de trabalho Excel com funções de wrap
url: /pt/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar WRAPCOLS em C# – Criar Pasta de Trabalho Excel com Funções Wrap

Já se perguntou **como usar WRAPCOLS** ao automatizar o Excel com C#? Você não está sozinho—muitos desenvolvedores esbarram em um obstáculo quando precisam transformar um intervalo horizontal em um array vertical sem escrever muito código. A boa notícia é que o Aspose.Cells torna isso muito simples.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra **como usar WRAPCOLS**, como **criar pasta de trabalho Excel em C#**, como **adicionar dados ao Excel**, e até como **forçar o cálculo de fórmulas** para que os resultados apareçam instantaneamente. Também vamos incluir **como usar WRAPROWS** para a transformação inversa. Ao final, você terá um programa pronto‑para‑executar e entenderá claramente por que cada passo é importante.

---

![Como usar WRAPCOLS em C# exemplo](alt="Screenshot showing Excel workbook after using WRAPCOLS in C#")

## O Que Este Guia Cobre

* Configurar uma nova pasta de trabalho com Aspose.Cells.  
* Preencher células programaticamente (**adicionar dados ao Excel**).  
* Aplicar a função `WRAPCOLS` para transformar uma linha em coluna.  
* Usar `WRAPROWS` para transformar uma coluna de volta em linha (**como usar wraprows**).  
* Forçar o motor a avaliar fórmulas imediatamente (**forçar cálculo de fórmula**).  
* Salvar o arquivo e verificar o resultado.

Nenhuma documentação externa necessária—tudo que você precisa está aqui.

---

## Como Usar WRAPCOLS em C# – Implementação Passo a Passo

Abaixo está o arquivo fonte completo. Sinta‑se à vontade para copiá‑e‑colar em um novo projeto de console, adicionar o pacote NuGet Aspose.Cells e pressionar **F5**.

```csharp
// ------------------------------------------------------------
// How to Use WRAPCOLS in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.Cells;

namespace WrapFunctionsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh workbook (this is how we **create excel workbook c#** style)
            Workbook workbook = new Workbook();

            // 2️⃣ Grab the first worksheet – it's created by default
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ **Add data to Excel**: place two numbers side‑by‑side
            sheet.Cells["A1"].PutValue(1);   // first value
            sheet.Cells["B1"].PutValue(2);   // second value

            // 4️⃣ **How to use WRAPCOLS** – turn the horizontal range A1:B1 into a vertical array
            //    The second argument (1) tells WRAPCOLS to create 1 column per element.
            sheet["C1"].Formula = "WRAPCOLS(A1:B1, 1)";

            // 5️⃣ **How to use WRAPROWS** – the opposite; turn the same range into a horizontal array
            //    Here we ask for 2 rows per element, which produces a single row with both values.
            sheet["C2"].Formula = "WRAPROWS(A1:B1, 2)";

            // 6️⃣ **Force formula calculation** so the workbook reflects the results immediately
            workbook.CalculateFormula();

            // 7️⃣ Save the workbook to disk – change the path to a folder you own
            string outputPath = @"WrapFunctions.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
            Console.WriteLine("Check cells C1 and C2 for the WRAPCOLS / WRAPROWS results.");
        }
    }
}
```

### Por Que Cada Linha É Importante

| Etapa | Explicação |
|------|-------------|
| **1️⃣ Criar uma nova pasta de trabalho** | Esta é a base. O Aspose.Cells trata um objeto `Workbook` como todo o arquivo Excel, então você está efetivamente **criando uma pasta de trabalho Excel em C#**. |
| **2️⃣ Obter a primeira planilha** | Uma nova pasta de trabalho sempre contém ao menos uma planilha (`Worksheets[0]`). Acessá‑la logo no início evita surpresas de referência nula. |
| **3️⃣ Adicionar dados ao Excel** | Usando `PutValue` nós **adicionamos dados ao Excel** sem nos preocupar com formatação de célula. Os números `1` e `2` são nossos dados de teste para as funções wrap. |
| **4️⃣ Como usar WRAPCOLS** | `WRAPCOLS(A1:B1, 1)` indica ao Excel que pegue o intervalo `A1:B1` e espalhe seus valores verticalmente, um por linha. O resultado vai para `C1` e se estende para baixo (`C1`, `C2`, …). |
| **5️⃣ Como usar WRAPROWS** | `WRAPROWS(A1:B1, 2)` faz o oposto: cria um espalhamento horizontal, colocando os dois valores em uma única linha a partir de `C2`. |
| **6️⃣ Forçar cálculo de fórmula** | Por padrão, o Aspose.Cells pode adiar o cálculo até que o arquivo seja aberto no Excel. Chamar `CalculateFormula()` **força o cálculo de fórmula** para que você possa ler os resultados imediatamente após salvar. |
| **7️⃣ Salvar a pasta de trabalho** | O passo final grava tudo no disco. Abra o `WrapFunctions.xlsx` resultante para ver o resultado. |

---

## Criar Pasta de Trabalho Excel em C# – Configurando o Ambiente

Antes de executar o código, certifique‑se de que tem as ferramentas corretas:

1. **.NET 6.0+** – A versão LTS mais recente funciona melhor.  
2. **Visual Studio 2022** (ou VS Code com a extensão C#).  
3. **Aspose.Cells for .NET** – Instale via NuGet:  
   ```bash
   dotnet add package Aspose.Cells
   ```  
4. Uma pasta gravável para o arquivo de saída.

Esses pré‑requisitos são mínimos; não é necessário COM interop nem instalação do Office, razão pela qual o Aspose.Cells é uma escolha popular para geração de Excel no lado do servidor.

---

## Adicionar Dados ao Excel – Boas Práticas

Ao **adicionar dados ao Excel** programaticamente, considere estas dicas:

* **Use `PutValue`** para números ou strings brutas; ele detecta automaticamente o tipo de dado.  
* **Evite codificar endereços de célula** em projetos grandes—use loops ou intervalos nomeados para escalabilidade.  
* **Defina estilos de célula com moderação**; cada mudança de estilo gera sobrecarga. Se precisar de formatação, crie um único objeto de estilo e aplique‑o a várias células.

No nosso exemplo pequeno inserimos apenas dois números, mas o mesmo padrão escala para milhares de linhas.

---

## Como Usar WRAPROWS – Exemplo de Array Horizontal

Se precisar do oposto de `WRAPCOLS`, `WRAPROWS` é a sua solução. A sintaxe é:

```
WRAPROWS(source_range, [rows_per_item])
```

* `source_range` – o intervalo que você deseja transformar.  
* `rows_per_item` – opcional; indica ao Excel quantas linhas cada elemento ocupa. No nosso demo usamos `2` para forçar ambos os valores em uma única linha.

Você pode experimentar alterando o segundo argumento:

```csharp
// Example: split each value into its own column, three rows per item
sheet["D1"].Formula = "WRAPROWS(A1:B1, 3)";
```

Abra a pasta de trabalho e verá os valores espalhados por três colunas, cada coluna contendo os números originais repetidos conforme necessário.

---

## Forçar Cálculo de Fórmula – Quando e Por Que

Você pode se perguntar: “Preciso realmente chamar `CalculateFormula()`?” A resposta é **sim**, se:

* Pretende ler valores calculados **programaticamente** após salvar.  
* Quer garantir que o arquivo abra no Excel já exibindo os resultados corretos.  
* Está executando em um **ambiente sem interface** (por exemplo, uma API web) onde nenhum usuário disparará manualmente um recálculo.

Pular este passo não quebra a pasta de trabalho, mas as células mostrarão o texto da fórmula (`=WRAPCOLS(...)`) em vez dos valores computados até que o Excel recalcule.

---

## Saída Esperada – O Que Procurar

Depois de executar o programa e abrir `WrapFunctions.xlsx`:

| Célula | Fórmula | Valor Exibido |
|------|---------|-----------------|
| **C1** | `=WRAPCOLS(A1:B1, 1)` | `1` (em C1) e `2` (em C2) – lista vertical |
| **C2** | `=WRAPROWS(A1:B1, 2)` | `1` em C2 e `2` em D2 – lista horizontal |

Portanto, você verá uma coluna de valores começando em **C1** e uma linha de valores começando em **C2**. Isso confirma que ambas as funções wrap se comportaram como esperado.

---

## Casos de Borda & Variações

| Cenário | O que muda? | Ajuste sugerido |
|----------|---------------|-----------------|
| **Grande intervalo (A1:Z1)** | Mais valores para espalhar verticalmente | Aumente o segundo argumento de `WRAPCOLS` se quiser múltiplas colunas por grupo. |
| **Dados não numéricos** | Strings são tratadas da mesma forma | Nenhuma mudança de código; `PutValue` aceita qualquer objeto. |
| **Intervalo dinâmico** | Você não conhece o tamanho em tempo de compilação | Use `sheet.Cells.MaxDataColumn` e `MaxDataRow` para montar a string de endereço. |
| **Múltiplas planilhas** | Necessidade de aplicar funções wrap em planilhas diferentes | Referencie a planilha correta (`workbook.Worksheets["Sheet2"]`). |

Antecipando essas variações, você pode adaptar o padrão central a quase qualquer cenário de automação.

---

## Dicas de Profissional da Área

* **Dica de pro:** Envolva a criação da pasta de trabalho em um bloco `using` se estiver mirando .NET Core 3.1+ para garantir que todos os recursos sejam liberados rapidamente.  
* **Fique atento a:** Definir a mesma fórmula em um grande intervalo sem chamar `CalculateFormula()` pode causar gargalos de desempenho. Processar fórmulas em lote sempre que possível.  
* **Sugestão:** Se precisar ler de volta os valores calculados no código, chame `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}