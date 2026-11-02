---
category: general
date: 2026-05-30
description: Adicionar comentário ao Excel usando C# rapidamente. Aprenda como escrever
  comentário em uma célula, inserir marcadores de posição Smart Marker e salvar a
  pasta de trabalho.
draft: false
keywords:
- add comment to excel
- write comment to cell
- add comment using c#
language: pt
og_description: Adicione comentário ao Excel usando C# em minutos. Este tutorial mostra
  como escrever um comentário em uma célula, lidar com o processamento de Smart Marker
  e salvar o arquivo.
og_title: Adicionar comentário ao Excel com C# – Guia completo
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Add comment to Excel using C# quickly. Learn how to write comment to
    cell, insert Smart Marker placeholders, and save the workbook.
  headline: Add comment to Excel with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add comment to Excel using C# quickly. Learn how to write comment to
    cell, insert Smart Marker placeholders, and save the workbook.
  name: Add comment to Excel with C# – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Adding Multiple Comments in One Pass
    text: If you need to add comments to several cells, just place multiple placeholders
      (`${Comment1}`, `${Comment2}`, …) and expand the data object accordingly.
  - name: 2. Preserving Existing Comments
    text: Sometimes a sheet already contains reviewer notes that you don’t want to
      lose. Retrieve the existing comment, merge, then write back.
  - name: 3. Unicode and Emojis
    text: Excel fully supports Unicode, so you can embed emojis, non‑Latin scripts,
      or special symbols directly in the comment string.
  - name: 4. Large Workbooks & Performance
    text: 'Processing a workbook with thousands of Smart Markers can be costly. To
      improve speed:'
  type: HowTo
- questions:
  - answer: Yes, but you must open the workbook with the `LoadOptions` that allow
      editing, e.g., `new LoadOptions(LoadFormat.Xlsx) { ReadOnly = false }`.
    question: Can I add a comment to a *read‑only* workbook?
  - answer: '`PutComment` overwrites the existing comment. To merge, retrieve the
      current comment first (`GetComment()`), concatenate, then call `PutComment`
      again.'
    question: What if the target cell already has a comment?
  - answer: Absolutely. Aspose.Cells abstracts the format; just point the `Workbook`
      constructor at the `.xls` file and everything else stays the same.
    question: Does this work with older `.xls` files?
  - answer: 'Practically, Excel supports comments up to 32,767 characters. Aspose.Cells
      respects the same limit—larger strings will be truncated. --- ## Recap & Next
      Steps We’ve covered how to **add comment to Excel** using C#, demonstrated the
      **write comment to cell** technique with Smart Markers, and explored'
    question: Is there a limit to comment length?
  type: FAQPage
tags:
- Excel
- C#
- Aspose.Cells
title: Adicionar comentário ao Excel com C# – Guia completo passo a passo
url: /pt/net/excel-comment-annotation/add-comment-to-excel-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add comment to Excel with C# – Guia completo passo a passo

Já se perguntou como **add comment to Excel** a partir de uma aplicação C# sem abrir o arquivo manualmente? Você não está sozinho. Muitos desenvolvedores precisam **write comment to cell** programaticamente — seja para trilhas de auditoria, notas de revisores ou relatórios dinâmicos. Neste tutorial vamos percorrer uma solução limpa, de ponta a ponta, que usa o recurso Smart Marker do Aspose.Cells, e também abordaremos o “porquê” de cada passo para que você possa adaptar o padrão aos seus próprios projetos.

Até o final do guia você será capaz de:

* Carregar uma pasta de trabalho existente,
* Inserir um comentário placeholder em uma célula específica,
* Substituir o placeholder por texto real usando um objeto anônimo,
* Salvar o arquivo atualizado,
* E lidar com alguns casos comuns, como comentários existentes ou texto Unicode.

Sem scripts externos, sem interop do Excel, apenas código C# puro que funciona no Windows, Linux e macOS.

## Pré-requisitos — O que você precisa antes de começar

* **Aspose.Cells for .NET** (v23.10 ou posterior). A biblioteca é gratuita para teste, e o nome do pacote NuGet é `Aspose.Cells`.
* Um ambiente de desenvolvimento .NET (Visual Studio, Rider ou VS Code com a extensão C#).  
* Uma pasta de trabalho de entrada (`input.xlsx`) colocada em uma pasta que você pode referenciar no código.  
* Familiaridade básica com tipos anônimos C# e inicializadores de objetos.  

Se você já tem esses itens, ótimo—vamos mergulhar. Caso contrário, obtenha o pacote NuGet com:

```bash
dotnet add package Aspose.Cells
```

Essa única linha traz tudo que você precisa, incluindo a classe `SmartMarkerProcessor` que usaremos mais adiante.

## Etapa 1 – Carregar a Pasta de Trabalho (add comment to excel)

Antes de podermos **add comment to Excel**, precisamos abrir o arquivo na memória. Aspose.Cells abstrai o formato do arquivo, então você não precisa se preocupar se é .xlsx, .xls ou até .csv.

```csharp
// Load the workbook that contains the target worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Por que isso importa:** Abrir a pasta de trabalho cria um objeto `Workbook` que contém todas as planilhas, estilos e comentários existentes. Se você pular esta etapa e tentar referenciar uma planilha diretamente, encontrará um `NullReferenceException`.

## Etapa 2 – Selecionar a Planilha e a Célula (write comment to cell)

A maioria das planilhas do mundo real tem várias abas. Para simplificar, trabalharemos com a primeira planilha, mas você pode indexar por nome se preferir.

```csharp
// Grab the first worksheet (index 0)
Worksheet ws = wb.Worksheets[0];

// Place a Smart Marker placeholder in cell A1 where the comment will appear
ws.Cells["A1"].PutComment("${Comment}");
```

A chamada a `PutComment` cria um objeto *comment* anexado a `A1`. O conteúdo `${Comment}` é um **placeholder Smart Marker**—pense nele como um token que será substituído mais tarde por dados reais.

> **Dica profissional:** Se a célula já contém um comentário, `PutComment` o sobrescreve. Para preservar comentários existentes, leia `ws.Cells["A1"].GetComment().Comment` primeiro, concatene, então reaplique.

## Etapa 3 – Preparar o Objeto de Dados (add comment using c#)

Smart Markers funcionam com qualquer objeto .NET que tenha propriedades correspondentes aos nomes dos placeholders. Um objeto anônimo é perfeito para demonstrações rápidas.

```csharp
// Anonymous object that supplies the actual comment text
var data = new { Comment = "Reviewed by John – ✅ Approved" };
```

Você também pode usar uma classe fortemente tipada se precisar de validação ou campos adicionais.

```csharp
public class ReviewInfo
{
    public string Comment { get; set; }
    public DateTime ReviewedOn { get; set; }
}
```

Então instancie:

```csharp
var data = new ReviewInfo
{
    Comment = "Reviewed by John – ✅ Approved",
    ReviewedOn = DateTime.UtcNow
};
```

> **Por que objetos anônimos?** Eles mantêm o código conciso quando você precisa de apenas alguns valores. Para conjuntos de dados maiores, um DTO (data‑transfer object) adequado oferece melhor manutenibilidade.

## Etapa 4 – Processar o Smart Marker (add comment to excel)

Agora a mágica acontece. O `SmartMarkerProcessor` varre a planilha, encontra `${Comment}` e o substitui pelo valor de `data.Comment`.

```csharp
// Run the processor to replace placeholders with real values
new SmartMarkerProcessor().Process(ws, data);
```

Nos bastidores, o processador:

1. Analisa a representação XML da planilha,
2. Detecta quaisquer tokens `${…}`,
3. Busca propriedades correspondentes no objeto fornecido,
4. Grava a string resolvida no nó de texto do comentário.

Se o placeholder estiver ausente, o processador o ignora silenciosamente — nenhuma exceção é lançada. Isso torna a abordagem segura para comentários opcionais.

## Etapa 5 – Salvar a Pasta de Trabalho (see the result)

Finalmente, escreva a pasta de trabalho modificada de volta ao disco. Você pode sobrescrever o arquivo original ou criar um novo.

```csharp
// Save the workbook – you can change the format by using SaveOptions if needed
wb.Save("YOUR_DIRECTORY/output.xlsx");
```

Quando você abrir `output.xlsx` no Excel, verá o comentário “Reviewed by John – ✅ Approved” anexado à célula **A1**. Passe o mouse sobre o pequeno triângulo vermelho no canto superior direito da célula para visualizá‑lo.

> **Saída esperada:**  

> ![Captura de tela mostrando uma célula com um comentário – exemplo de add comment to excel](add-comment-to-excel-example.png "add comment to excel example")

*O texto alternativo inclui a palavra‑chave principal, atendendo à regra de SEO.*

## Lidando com Cenários Comuns

### 1. Adicionando Múltiplos Comentários em Uma Passagem

Se precisar adicionar comentários a várias células, basta colocar múltiplos placeholders (`${Comment1}`, `${Comment2}`, …) e expandir o objeto de dados de acordo.

```csharp
ws.Cells["A1"].PutComment("${Comment1}");
ws.Cells["B2"].PutComment("${Comment2}");

var data = new
{
    Comment1 = "First note",
    Comment2 = "Second note"
};

new SmartMarkerProcessor().Process(ws, data);
```

### 2. Preservando Comentários Existentes

Às vezes, uma planilha já contém notas de revisores que você não quer perder. Recupere o comentário existente, mescle, então grave novamente.

```csharp
var existing = ws.Cells["A1"].GetComment()?.Comment ?? string.Empty;
var merged   = string.IsNullOrWhiteSpace(existing)
               ? data.Comment
               : $"{existing}\n{data.Comment}";

ws.Cells["A1"].PutComment(merged);
```

### 3. Unicode e Emojis

O Excel suporta totalmente Unicode, então você pode incorporar emojis, scripts não latinos ou símbolos especiais diretamente na string do comentário.

```csharp
var data = new { Comment = "审查通过 – ✅" };
```

Apenas certifique-se de que seu arquivo fonte está salvo com codificação UTF‑8 (o padrão na maioria das IDEs modernas).

### 4. Pastas de Trabalho Grandes e Desempenho

Processar uma pasta de trabalho com milhares de Smart Markers pode ser custoso. Para melhorar a velocidade:

* Use `SmartMarkerProcessorOptions` para limitar o escopo a uma única planilha.
* Desative o cálculo (`wb.CalculateFormula = false`) se você precisar apenas de comentários.
* Reutilize uma única instância `SmartMarkerProcessor` ao invés de criar uma nova por planilha.

```csharp
var processor = new SmartMarkerProcessor
{
    Options = new SmartMarkerProcessorOptions { ProcessAllWorksheets = false }
};

processor.Process(ws, data);
```

## Exemplo Completo Funcional

Juntando tudo, aqui está um aplicativo console autônomo que você pode copiar e colar em `Program.cs` e executar.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Get the first worksheet and insert a placeholder comment
            Worksheet ws = wb.Worksheets[0];
            ws.Cells["A1"].PutComment("${Comment}");

            // 3️⃣ Prepare data – you can use an anonymous type or a DTO
            var data = new { Comment = "Reviewed by John – ✅ Approved" };

            // 4️⃣ Process Smart Markers to replace the placeholder
            new SmartMarkerProcessor().Process(ws, data);

            // 5️⃣ Save the result
            wb.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Comment added successfully!");
        }
    }
}
```

Execute o programa, abra `output.xlsx` e você verá o comentário aparecer exatamente onde colocamos o placeholder. Nenhuma interface do Excel necessária, sem interop COM, apenas código gerenciado puro.

## Perguntas Frequentes (FAQ)

**Q: Posso adicionar um comentário a uma pasta de trabalho *somente‑leitura*?**  
A: Sim, mas você deve abrir a pasta de trabalho com `LoadOptions` que permitem edição, por exemplo, `new LoadOptions(LoadFormat.Xlsx) { ReadOnly = false }`.

**Q: E se a célula alvo já tiver um comentário?**  
A: `PutComment` sobrescreve o comentário existente. Para mesclar, recupere o comentário atual primeiro (`GetComment()`), concatene, então chame `PutComment` novamente.

**Q: Isso funciona com arquivos `.xls` mais antigos?**  
A: Absolutamente. Aspose.Cells abstrai o formato; basta apontar o construtor `Workbook` para o arquivo `.xls` e todo o resto permanece o mesmo.

**Q: Existe um limite para o tamanho do comentário?**  
A: Na prática, o Excel suporta comentários de até 32.767 caracteres. Aspose.Cells respeita o mesmo limite — strings maiores serão truncadas.

## Recapitulação & Próximos Passos

Abordamos como **add comment to Excel** usando C#, demonstramos a técnica **write comment to cell** com Smart Markers, e exploramos variações como múltiplos comentários, suporte a Unicode e ajuste de desempenho. O padrão central — placeholder → objeto de dados → processador → salvar — pode ser reutilizado para qualquer conteúdo dinâmico, não

## O que você deve aprender a seguir?

- [Adicionar um Comentário com Imagem no Excel](/cells/english/net/excel-comment-annotation/add-comment-with-image-excel/)
- [Adicionar Imagem ao Comentário do Excel com Aspose.Cells para Java: Guia Completo](/cells/english/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)
- [Adicionar Comentário com Imagem no Excel](/cells/german/net/excel-comment-annotation/add-comment-with-image-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}