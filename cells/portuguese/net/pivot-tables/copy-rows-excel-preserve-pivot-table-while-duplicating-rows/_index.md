---
category: general
date: 2026-02-14
description: Copiar linhas do Excel e preservar a tabela dinâmica de uma só vez. Aprenda
  como copiar linhas, copiar intervalo para a planilha e duplicar linhas com a tabela
  dinâmica usando Aspose.Cells.
draft: false
keywords:
- copy rows excel
- preserve pivot table
- how to copy rows
- copy range to sheet
- duplicate rows with pivot
language: pt
og_description: Copiar linhas do Excel e preservar a tabela dinâmica de uma só vez.
  Siga este guia passo a passo para duplicar linhas com a tabela dinâmica usando C#.
og_title: Copiar linhas Excel – Preservar Tabela Dinâmica ao Duplicar Linhas
tags:
- Aspose.Cells
- C#
- Excel automation
title: Copiar linhas no Excel – Preservar Tabela Dinâmica ao Duplicar Linhas
url: /pt/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/
---

complete, runnable solution that shows you **how to copy rows**, keep the **preserve pivot table** behavior alive, ...". Need translate but keep bold parts maybe keep English inside bold? The bold text includes "copy rows excel", "how to copy rows", "preserve pivot table". Should we keep them English? Technical terms maybe keep English. So we keep bold as is. Translate rest.

Let's produce translation.

Will keep code block placeholders unchanged.

Also need to translate table rows.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# copiar rows excel – Preservar Tabela Dinâmica ao Duplicar Linhas

Já precisou **copy rows excel** mantendo a tabela dinâmica intacta? Neste tutorial vamos percorrer uma solução completa e executável que mostra **how to copy rows**, mantém o comportamento **preserve pivot table** ativo e ainda **duplicate rows with pivot** entre planilhas usando Aspose.Cells para .NET.

Imagine que você está construindo um relatório mensal de vendas que puxa dados de uma planilha mestre, gera uma tabela dinâmica e, em seguida, precisa enviar uma versão reduzida para um parceiro. Copiar o intervalo manualmente é trabalhoso e você corre o risco de quebrar a tabela dinâmica. A boa notícia? Algumas linhas de C# podem fazer o trabalho pesado para você — sem cliques de mouse.

> **O que você receberá:** um exemplo completo de código, explicações passo a passo, dicas para casos de borda e um rápido sanity‑check para verificar se a tabela dinâmica sobreviveu à cópia.

---

## O que você precisará

- **Aspose.Cells para .NET** (o pacote NuGet gratuito funciona bem para esta demonstração).  
- Um runtime **.NET recente** (4.7+ ou .NET 6/7).  
- Um arquivo Excel (`source.xlsx`) que contém uma tabela dinâmica na primeira planilha.  
- Visual Studio, Rider ou qualquer editor C# de sua preferência.

Nenhuma biblioteca adicional, sem interop COM e sem instalação do Excel no servidor. Por isso essa abordagem é tanto **copy range to sheet** amigável quanto segura para servidores.

---

## Etapa 1 – Carregar a Pasta de Trabalho (copy rows excel)

A primeira coisa a fazer é abrir a pasta de trabalho de origem. Usar Aspose.Cells nos fornece um modelo de objeto limpo que funciona da mesma forma no Windows, Linux ou Azure.

```csharp
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Por que isso importa:** ao carregar a pasta de trabalho criamos uma representação em memória de cada planilha, incluindo objetos ocultos como caches de tabelas dinâmicas. Assim que o arquivo está na memória, podemos manipular linhas sem nunca tocar na UI.

---

## Etapa 2 – Identificar a Planilha de Destino (copy range to sheet)

Queremos que as linhas copiadas sejam inseridas em outra planilha — `Sheet2` neste exemplo. Se a planilha não existir, Aspose a criará para você.

```csharp
        // Get (or create) the destination worksheet where the rows will be placed
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");
```

> **Dica profissional:** sempre verifique `Worksheets.Contains` antes de adicionar uma planilha; caso contrário você acabará com nomes duplicados e uma exceção em tempo de execução.

---

## Etapa 3 – Copiar Linhas Preservando a Tabela Dinâmica

Agora vem o ponto central: copiar as linhas **A1:E20** (que incluem a tabela dinâmica) da primeira planilha para `Sheet2`. O método `CopyRows` copia as células brutas *e* o cache subjacente da tabela dinâmica, de modo que a tabela permanece funcional.

```csharp
        // Define the source range: rows 0‑19 (A1:E20) on the first worksheet
        Worksheet sourceWorksheet = sourceWorkbook.Worksheets[0];

        // Copy rows 0‑19 from source to destination, starting at row 0 on the destination sheet
        sourceWorksheet.Cells.CopyRows(
            sourceWorksheet.Cells,   // source cells collection
            0,                       // source start row (0‑based, i.e., row 1)
            0,                       // destination start row on the same sheet (adjust if needed)
            20);                     // total number of rows to copy
```

> **Por que funciona:** `CopyRows` respeita o cache interno da tabela dinâmica, então a tabela dinâmica na planilha de destino é uma cópia *viva*, não uma captura estática. Isso satisfaz o requisito **preserve pivot table** sem código extra.

Se precisar que as linhas comecem em um deslocamento diferente na planilha de destino — por exemplo, na linha 10 — basta alterar o terceiro argumento para `9`.

---

## Etapa 4 – Salvar a Pasta de Trabalho (duplicate rows with pivot)

Por fim, grave a pasta de trabalho modificada no disco. A tabela dinâmica estará totalmente funcional no novo arquivo.

```csharp
        // Save the workbook; the copied pivot remains active automatically
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

> **Verificação de resultado:** abra `copyWithPivot.xlsx` no Excel, vá para *Sheet2* e atualize a tabela dinâmica. Você deverá ver o mesmo layout de campos e cálculos da original — nada quebrado.

---

## Verificando a Cópia – Quick sanity check

```csharp
// Optional: programmatically confirm the pivot exists on the destination sheet
Worksheet dest = sourceWorkbook.Worksheets["Sheet2"];
bool pivotExists = dest.PivotTables.Count > 0;
Console.WriteLine($"Pivot table copied? {pivotExists}");
```

Se o console imprimir `True`, você duplicou **duplicate rows with pivot** com sucesso e manteve o motor de análise de dados ativo.

---

## Casos de Borda Comuns & Como Lidar com Eles

| Situação | O que observar | Ajuste sugerido |
|-----------|-------------------|-----------------|
| **O intervalo de origem inclui células mescladas** | Células mescladas podem causar desalinhamento ao copiar. | Use `CopyRows` como mostrado; ele preserva mesclagens automaticamente. |
| **A planilha de destino já contém dados** | Novas linhas podem sobrescrever conteúdo existente. | Altere a linha inicial de destino (terceiro argumento) para a primeira linha vazia: `destWorksheet.Cells.MaxDataRow + 1`. |
| **A tabela dinâmica usa fonte de dados externa** | Conexões externas não são copiadas. | Garanta que a pasta de trabalho de origem contenha o conjunto completo de dados; caso contrário, reconecte a fonte após a cópia. |
| **Pasta de trabalho grande (100k+ linhas)** | O uso de memória aumenta. | Considere copiar em blocos (ex.: 5.000 linhas por vez) para manter o GC satisfeito. |

---

## Exemplo Completo (Todas as Etapas Juntas)

Abaixo está o programa inteiro que você pode colar em um aplicativo console e executar imediatamente.

```csharp
using System;
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");

        // 2️⃣ Get (or create) the destination worksheet
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");

        // 3️⃣ Copy rows A1:E20 (includes pivot) from the first sheet
        Worksheet sourceWorksheet = sourceWorkbook.Worksheets[0];
        sourceWorksheet.Cells.CopyRows(
            sourceWorksheet.Cells, // source cells
            0,                     // start at row 0 (A1)
            0,                     // destination start row (adjust as needed)
            20);                   // copy 20 rows

        // 4️⃣ Save the workbook – pivot stays alive
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");

        // Optional verification
        bool pivotExists = destinationWorksheet.PivotTables.Count > 0;
        Console.WriteLine($"Pivot table copied? {pivotExists}");
    }
}
```

Execute o programa, abra o `copyWithPivot.xlsx` gerado e você verá que a tabela dinâmica em **Sheet2** funciona exatamente como a original. Nenhuma recriação manual necessária.

---

## Perguntas Frequentes

**Q: Isso funciona com arquivos `.xls` compatíveis com Excel 2003?**  
A: Sim. Aspose.Cells abstrai o formato do arquivo, então o mesmo código funciona para `.xls`, `.xlsx` e até `.xlsb`.

**Q: E se eu precisar copiar *colunas* em vez de linhas?**  
A: Use `CopyColumns` de forma semelhante; basta trocar os parâmetros de linha pelos índices de coluna.

**Q: Posso copiar vários intervalos não contíguos de uma vez?**  
A: Não diretamente com `CopyRows`. Percorra cada intervalo ou crie uma planilha temporária que consolide os intervalos antes de copiar.

---

## Conclusão

Acabamos de demonstrar um padrão limpo de **copy rows excel** que mantém a integridade da **preserve pivot table**, permite **how to copy rows** de forma eficiente e mostra como **copy range to sheet** sem perder nenhuma funcionalidade da tabela dinâmica. Ao final deste guia você deverá estar confiante para **duplicate rows with pivot** em qualquer pipeline de automação — seja gerando relatórios diários ou construindo um serviço de exportação de dados em larga escala.

Pronto para o próximo desafio? Experimente estender o código para:

- Exportar a planilha duplicada como PDF.  
- Atualizar a tabela dinâmica programaticamente após a cópia.  
- Percorrer uma lista de arquivos de origem e processá‑los em lote.

Se encontrar algum obstáculo, deixe um comentário abaixo ou me chame no GitHub. Boa codificação e aproveite o tempo que você economizou ao não arrastar o Excel manualmente!  

<img src="copy-rows-excel.png" alt="copy rows excel diagram" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}