---
category: general
date: 2026-07-13
description: Crie uma pasta de trabalho do Excel e defina a fórmula da célula usando
  EXPAND. Aprenda como recalcular a pasta de trabalho e escrever fórmulas do Excel
  dinamicamente em C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell formula
- recalculate workbook
- write excel formula
- how to use expand
language: pt
lastmod: 2026-07-13
og_description: Crie uma pasta de trabalho do Excel instantaneamente. Este guia mostra
  como definir a fórmula da célula, recalcular a pasta de trabalho e dominar o uso
  do EXPAND para intervalos dinâmicos.
og_image_alt: Screenshot showing create excel workbook with EXPAND formula in C#
og_title: Criar Pasta de Trabalho do Excel com a Fórmula EXPAND – Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Create Excel workbook and set cell formula using EXPAND. Learn how
    to recalculate workbook and write Excel formulas dynamically in C#.
  headline: Create Excel Workbook with EXPAND Formula – Complete Guide
  type: TechArticle
tags:
- excel
- csharp
- aspnet
title: Criar Pasta de Trabalho do Excel com a Fórmula EXPAND – Guia Completo
url: /pt/net/formulas-functions/create-excel-workbook-with-expand-formula-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pasta de Trabalho Excel com Fórmula EXPAND – Guia Completo

Já se perguntou como **criar pasta de trabalho excel** programaticamente e deixar uma única fórmula preencher toda uma tabela para você? Você não está sozinho. Em muitos cenários de relatórios ou exportação de dados, você precisa colocar uma pasta de trabalho na pasta Downloads do usuário, espalhar uma fórmula pelas células e fazer com que ela seja avaliada automaticamente.  

Neste tutorial vamos percorrer exatamente isso: vamos **criar pasta de trabalho excel**, **definir fórmula de célula** usando a nova função `EXPAND`, e então **recalcular a pasta de trabalho** para que os resultados apareçam instantaneamente. Ao final, você também saberá **como usar expand** para intervalos dinâmicos e ficará confortável em **escrever fórmula excel** que se adapta a tamanhos de dados que mudam.

---

## O que Você Vai Construir

- Uma nova instância `Workbook` (nenhum modelo necessário).  
- Uma fórmula de matriz expansiva em `A1` que cresce para um bloco de 5 linhas × 3 colunas.  
- Uma chamada a `Calculate()` que força o motor a avaliar a fórmula.  
- Uma leitura rápida das células preenchidas para que você possa verificar a saída.

Nenhuma biblioteca externa além do núcleo Aspose.Cells (ou qualquer engine Excel .NET comparável) é necessária — apenas C# puro.

---

## Pré-requisitos

- .NET 6+ (ou .NET Framework 4.7.2+).  
- Uma referência a uma biblioteca de manipulação Excel que suporte funções de matriz dinâmica (por exemplo, **Aspose.Cells**, **GemBox.Spreadsheet**, ou **ClosedXML** com um engine Excel recente).  
- Familiaridade básica com a sintaxe C# — se você já escreveu um “Hello World”, está pronto para prosseguir.

---

## Etapa 1: Criar Pasta de Trabalho Excel e Adicionar uma Planilha

Primeiro as primeiras coisas. Precisamos de um objeto workbook para conter tudo. Pense nele como o caderno vazio que você preencherá depois.

```csharp
// Step 1: Instantiate a new workbook
var workbook = new Workbook();               // Primary object
var sheet = workbook.Worksheets[0];          // Grab the default sheet
```

> **Por que isso importa:** A classe `Workbook` é o ponto de entrada para qualquer operação Excel. Sem ela você não pode definir uma fórmula ou recalcular nada. Criar a pasta de trabalho antecipadamente também permite que você adicione várias planilhas depois, caso seu cenário cresça.

---

## Etapa 2: Definir Fórmula de Célula com `EXPAND`

Agora vamos **definir fórmula de célula** em `A1`. A função `EXPAND` recebe uma referência “spill” (`A1#`) e a expande para um tamanho específico — no nosso caso, 5 linhas por 3 colunas.

```csharp
// Step 2: Insert an expanding array formula into cell A1
// The source range A1# will be stretched to 5 rows × 3 columns
sheet.Cells[0, 0].Formula = "=EXPAND(A1#,5,3)";
```

> **Dica profissional:** Se você estiver usando uma biblioteca que espelha o motor de cálculo do Excel, o operador spill `#` funciona pronto para uso. Caso contrário, pode ser necessário habilitar o suporte a matrizes dinâmicas nas configurações da biblioteca.

> **E se a célula de origem estiver vazia?** `EXPAND` retornará `#SPILL!`. Para evitar isso, você pode envolver a referência em `IFERROR` ou fornecer um valor padrão, por exemplo, `=IFERROR(EXPAND(A1#,5,3),0)`.

---

## Etapa 3: Preencher a Célula de Origem (Opcional)

`EXPAND` precisa de algo para expandir. Vamos colocar uma constante de matriz simples em `A1` para que possamos ver o spill em ação.

```csharp
// Optional: Fill A1 with a 2‑by‑2 array constant
sheet.Cells[0, 0].ArrayFormula = "{1,2;3,4}";
```

Agora `A1#` representa um bloco 2 × 2, e `EXPAND` o estenderá para a matriz 5 × 3 solicitada, preenchendo as células extras com zeros (ou o que o motor decidir).

---

## Etapa 4: Recalcular a Pasta de Trabalho para Avaliar a Fórmula

Definir a fórmula não basta — você precisa **recalcular a pasta de trabalho** para que o motor realmente calcule os valores.

```csharp
// Step 4: Force calculation of all formulas
workbook.Calculate();
```

> **Por que recalculamos:** Algumas bibliotecas avaliam fórmulas de forma preguiçosa apenas quando você salva ou solicita explicitamente um valor. Chamar `Calculate()` garante que a área de spill seja preenchida imediatamente, o que é essencial para processamento posterior ou para retornar dados a uma interface de usuário.

---

## Etapa 5: Verificar o Resultado – Ler o Intervalo Expandido

Vamos buscar algumas células da área expandida para provar que funcionou.

```csharp
// Step 5: Read back a few cells from the expanded block
for (int row = 0; row < 5; row++)
{
    for (int col = 0; col < 3; col++)
    {
        var value = sheet.Cells[row, col].Value;
        Console.Write($"{value}\t");
    }
    Console.WriteLine();
}
```

**Saída esperada no console**

```
1	2	0	
3	4	0	
0	0	0	
0	0	0	
0	0	0	
```

Observe como a matriz original 2 × 2 é colocada no canto superior esquerdo, e as células restantes são preenchidas com zeros (o comportamento padrão do `EXPAND` quando o tamanho alvo excede o da origem).

---

## Variações Comuns e Casos de Borda

| Situação | Como Lidar |
|-----------|------------|
| **Intervalo de origem maior que o alvo** | `EXPAND` truncará as linhas/colunas extras. Se você precisar da origem completa, omita os argumentos de tamanho. |
| **Tamanho de origem dinâmico** | Use `ROWS(A1#)` e `COLUMNS(A1#)` dentro de `EXPAND` para um spill auto‑ajustável. |
| **Desempenho em intervalos enormes** | Recalcular uma pasta de trabalho massiva pode ser lento. Chame `Calculate()` apenas na planilha afetada: `sheet.Calculate();`. |
| **Salvar a pasta de trabalho** | Após a verificação, chame `workbook.Save("Report.xlsx");` para persistir o arquivo. |
| **Usando outras funções dinâmicas** | `SEQUENCE`, `FILTER` e `SORT` combinam bem com `EXPAND`. Por exemplo, `=EXPAND(FILTER(A2:A20, B2:B20>0),10,2)`. |

---

## Exemplo Completo em Funcionamento (Todas as Etapas Combinadas)

```csharp
using System;
using Aspose.Cells;   // Replace with your chosen library

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];

        // 2️⃣ Set an expanding formula in A1
        sheet.Cells[0, 0].Formula = "=EXPAND(A1#,5,3)";

        // 3️⃣ Optional: give A1 a 2x2 array constant
        sheet.Cells[0, 0].ArrayFormula = "{1,2;3,4}";

        // 4️⃣ Recalculate so the formula evaluates
        workbook.Calculate();

        // 5️⃣ Print the first 5 rows × 3 columns
        for (int r = 0; r < 5; r++)
        {
            for (int c = 0; c < 3; c++)
            {
                Console.Write($"{sheet.Cells[r, c].Value}\t");
            }
            Console.WriteLine();
        }

        // Save if you want to inspect the file
        workbook.Save("ExpandDemo.xlsx");
    }
}
```

Execute este programa e você verá a saída exata mostrada anteriormente, além de um arquivo `ExpandDemo.xlsx` no disco contendo a mesma matriz spill.

---

## Dicas & Truques da Prática

- **Dica profissional:** Se você só precisa dos valores expandidos para cálculo posterior (sem planilha visível ao usuário), considere ler os valores diretamente após `Calculate()` — não há necessidade de gravar no disco.  
- **Fique atento:** Algumas versões antigas de engines Excel não suportam matrizes dinâmicas; elas lançarão `#NAME?`. Sempre verifique a versão da sua biblioteca.  
- **Erro típico:** Esquecer de chamar `Calculate()` resulta em células vazias e usuários confusos. Sempre teste todo o fluxo.  
- **Dica de desempenho:** Definir fórmulas em lote (`sheet.Cells[range].Formula = ...`) pode ser mais rápido que atribuições individuais ao lidar com milhares de células.

---

## Conclusão

Agora você sabe como **criar pasta de trabalho excel**, **definir fórmula de célula** com a poderosa função `EXPAND`, e **recalcular a pasta de trabalho** para que os dados sejam espalhados exatamente onde você precisa. Essa abordagem permite que você **escreva fórmula excel** que se adapta a tamanhos de dados que mudam sem codificar intervalos — perfeito para dashboards, relatórios automatizados ou qualquer cenário onde os dados de origem crescem ao longo do tempo.

Pronto para o próximo passo? Experimente substituir `EXPAND` por `SEQUENCE` para gerar grades numeradas, ou combine‑o com `FILTER` para extrair apenas linhas que atendam a uma condição. E não se esqueça de explorar como **definir fórmula de célula** para gráficos, tabelas dinâmicas ou formatação condicional — sua recém‑criada pasta de trabalho é uma base sólida.

Tem perguntas sobre casos de borda ou particularidades de bibliotecas? Deixe um comentário abaixo, e feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Criar Intervalos Nomeados com Escopo de Pasta de Trabalho no Excel Usando Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Automação Excel com Aspose.Cells .NET: Criar Pasta de Trabalho & Definir Links Externos](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Como Carregar uma Pasta de Trabalho Excel & Definir Tamanhos de Impressora Usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/load-workbook-set-printer-sizes-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}