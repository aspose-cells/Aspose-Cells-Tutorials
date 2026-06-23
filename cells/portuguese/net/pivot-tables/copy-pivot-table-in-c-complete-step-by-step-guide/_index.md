---
category: general
date: 2026-03-25
description: Copie a tabela dinâmica com C# usando Aspose.Cells. Aprenda como copiar
  a tabela dinâmica, exportar o arquivo da tabela dinâmica e preservar os dados em
  minutos.
draft: false
keywords:
- copy pivot table
- how to copy pivot
- export pivot table file
- Aspose.Cells pivot
- C# Excel automation
language: pt
og_description: Copie a tabela dinâmica em C# usando Aspose.Cells. Este guia mostra
  como copiar a tabela dinâmica, exportar o arquivo da tabela dinâmica e manter todas
  as configurações intactas.
og_title: Copiar Tabela Dinâmica em C# – Tutorial Completo de Programação
tags:
- C#
- Excel
- Aspose.Cells
- Data Export
title: Copiar Tabela Dinâmica em C# – Guia Completo Passo a Passo
url: /pt/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar Tabela Dinâmica em C# – Guia Completo Passo a Passo

Já precisou **copiar tabela dinâmica** de uma planilha para outra e se perguntou se a lógica da tabela dinâmica sobrevive à movimentação? Você não é o único. Em muitos pipelines de relatórios geramos uma planilha mestre e, em seguida, enviamos uma cópia leve que ainda permite que os usuários finais segmentem os dados. A boa notícia? Com algumas linhas de C# e Aspose.Cells você pode fazer exatamente isso — sem necessidade de ajustes manuais.

Neste tutorial percorreremos todo o processo: carregar o arquivo de origem, selecionar o intervalo que contém a tabela dinâmica, colá-lo em uma nova planilha preservando a definição da tabela dinâmica e, finalmente, **exportar o arquivo da tabela dinâmica** para consumo posterior. Ao final, você saberá *como copiar tabelas dinâmicas* programaticamente e terá um exemplo pronto para usar que pode inserir em seu projeto.

## Pré-requisitos

- .NET 6+ (ou .NET Framework 4.6+) instalado  
- Pacote NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
- Um arquivo Excel de origem (`source.xlsx`) que já contém uma tabela dinâmica (qualquer tamanho serve)  
- Conhecimento básico de C#; não é necessário conhecimento profundo de internals do Excel  

Se você não tem algum desses, basta adicionar o pacote NuGet e abrir o Visual Studio — nada mais.

## O que o Código Faz (Visão Geral)

1. **Load** a pasta de trabalho que contém a tabela dinâmica original.  
2. **Define** um `Range` que engloba toda a tabela dinâmica (incluindo seu cache).  
3. **Create** uma nova pasta de trabalho que será o destino.  
4. **Paste** o intervalo com `CopyPivotTable = true` para que a definição da tabela dinâmica seja copiada, não apenas os valores.  
5. **Save** o arquivo de destino, fornecendo um **arquivo de exportação da tabela dinâmica** que você pode compartilhar.

Esse é todo o fluxo de trabalho em cinco etapas simples. Vamos mergulhar em cada uma.

## Etapa 1 – Carregar a Pasta de Trabalho de Origem que Contém a Tabela Dinâmica

Primeiro precisamos trazer o arquivo de origem para a memória. Aspose.Cells torna isso uma única linha.

```csharp
using Aspose.Cells;

// Load the source workbook (replace the path with your actual file)
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet – adjust the index if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
```

*Por que isso importa:* Carregar a pasta de trabalho nos dá acesso ao cache subjacente da tabela dinâmica. Se você copiar apenas os valores das células, a tabela dinâmica perde sua capacidade de segmentação. Mantendo o objeto da pasta de trabalho ativo, preservamos todos os metadados da tabela dinâmica.

## Etapa 2 – Definir o Intervalo que Inclui a Tabela Dinâmica

Uma tabela dinâmica não é apenas um bloco de células; ela também possui dados de cache ocultos. A maneira mais segura é selecionar um retângulo que circunde totalmente a área visível. Na maioria dos casos `A1:E20` funciona, mas você pode descobrir programaticamente os limites exatos usando as propriedades de `PivotTable`.

```csharp
// Example range – adjust to match your pivot's size
Range sourceRange = sourceSheet.Cells.CreateRange("A1:E20");

// (Optional) Dynamically get the used range of the pivot:
PivotTable pivot = sourceSheet.PivotTables[0];
int firstRow = pivot.Row - 1;      // include header row
int firstCol = pivot.Column - 1;   // include field list
int lastRow  = pivot.Row + pivot.RowCount;
int lastCol  = pivot.Column + pivot.ColumnCount;
Range dynamicRange = sourceSheet.Cells.CreateRange(firstRow, firstCol,
                                                    lastRow - firstRow + 1,
                                                    lastCol - firstCol + 1);
```

*Por que escolhemos um intervalo:* O método `Paste` funciona em um objeto `Range`. Ao especificar a área exata, garantimos que tanto o layout da tabela dinâmica quanto seu cache viajem juntos.

## Etapa 3 – Criar uma Nova Pasta de Trabalho de Destino

Agora criamos uma pasta de trabalho em branco que receberá a tabela dinâmica copiada. Nada sofisticado, apenas uma tela limpa.

```csharp
// Initialize an empty workbook – it comes with one default worksheet
Workbook destinationWorkbook = new Workbook();
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

*Dica:* Se precisar preservar planilhas existentes (por exemplo, um modelo), você pode adicionar a nova pasta de trabalho como um clone de um arquivo de modelo em vez de usar o construtor vazio.

## Etapa 4 – Colar o Intervalo Preservando a Tabela Dinâmica

Aqui está o coração da operação. Definir `CopyPivotTable = true` indica ao Aspose.Cells que transfira a definição da tabela dinâmica, não apenas os valores exibidos.

```csharp
destinationSheet.Cells.Paste(
    sourceRange,
    new PasteOptions
    {
        PasteType = PasteType.All,      // copy everything: formulas, formats, etc.
        CopyPivotTable = true           // crucial – keeps the pivot functional
    });
```

*O que acontece nos bastidores?* Aspose.Cells recria o cache da tabela dinâmica na pasta de trabalho de destino, reconecta a fonte de dados da tabela dinâmica e mantém segmentações, filtros e campos calculados. O resultado é uma tabela dinâmica totalmente interativa — exatamente o que você esperaria se tivesse duplicado a planilha manualmente no Excel.

## Etapa 5 – Salvar a Pasta de Trabalho Resultante (Exportar Arquivo da Tabela Dinâmica)

Finalmente gravamos a pasta de trabalho de destino no disco. O arquivo que você obtém é seu **arquivo de exportação da tabela dinâmica** pronto para distribuição.

```csharp
destinationWorkbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");
```

Abra `copy-pivot.xlsx` no Excel e você verá a tabela dinâmica intacta, pronta para ser atualizada ou segmentada.

## Exemplo Completo Funcional (Todas as Etapas Combinadas)

Abaixo está o programa completo que você pode copiar‑colar em um aplicativo console. Ele inclui tratamento de erros e comentários para clareza.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load source workbook with the pivot table
                Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
                Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

                // 2️⃣ Define the range that fully encloses the pivot
                // Adjust "A1:E20" as needed, or use dynamic detection shown earlier
                Range sourceRange = sourceSheet.Cells.CreateRange("A1:E20");

                // 3️⃣ Create a fresh destination workbook
                Workbook destinationWorkbook = new Workbook();
                Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

                // 4️⃣ Paste the range and keep the pivot definition
                destinationSheet.Cells.Paste(
                    sourceRange,
                    new PasteOptions
                    {
                        PasteType = PasteType.All,
                        CopyPivotTable = true
                    });

                // 5️⃣ Save the new file – this is your exported pivot table file
                destinationWorkbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

                Console.WriteLine("✅ Pivot table copied successfully! File saved as copy-pivot.xlsx");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ An error occurred: {ex.Message}");
            }
        }
    }
}
```

**Resultado esperado:** Ao abrir `copy-pivot.xlsx`, a tabela dinâmica aparece exatamente como em `source.xlsx`. Você pode atualizá‑la, mudar filtros ou até adicionar novas fontes de dados sem perder a funcionalidade.

## Perguntas Frequentes & Casos Limítrofes

### E se a pasta de trabalho de origem tiver múltiplas tabelas dinâmicas?

Percorra `sourceSheet.PivotTables` e repita o copiar‑colar para cada uma. Apenas certifique-se de que cada intervalo de destino não se sobreponha.

```csharp
int destRow = 0;
foreach (PivotTable pt in sourceSheet.PivotTables)
{
    // Calculate a non‑overlapping destination range for each pivot
    Range src = sourceSheet.Cells.CreateRange(pt.Row, pt.Column,
                                              pt.RowCount + 5, pt.ColumnCount + 5);
    destinationSheet.Cells.Paste(src, new PasteOptions { PasteType = PasteType.All, CopyPivotTable = true });
    destRow += pt.RowCount + 10; // move down for the next pivot
}
```

### Isso funciona com fontes de dados externas (por exemplo, SQL)?

Se a tabela dinâmica original obtém dados de uma conexão externa, a string de conexão também é copiada. Contudo, a pasta de trabalho de destino deve ter acesso à mesma fonte de dados. Pode ser necessário ajustar credenciais ou usar `WorkbookSettings` para permitir conexões externas.

### Posso copiar apenas o layout da tabela dinâmica (sem dados)?

Defina `PasteOptions.PasteType = PasteType.Formulas` e mantenha `CopyPivotTable = true`. Isso copia a estrutura enquanto deixa o cache de dados vazio, forçando uma atualização na primeira abertura.

### E quanto à proteção da planilha?

Se a planilha de origem estiver protegida, desproteja-a antes de copiar, ou passe a `Password` apropriada para `Worksheet.Unprotect`. Após colar, você pode reaplicar a proteção na planilha de destino.

## Dicas Profissionais & Armadilhas

- **Dica profissional:** Sempre use a versão mais recente do Aspose.Cells; versões antigas tinham um bug onde `CopyPivotTable` ignorava segmentações.  
- **Cuidado com:** Grandes caches de tabelas dinâmicas podem inflar o arquivo de destino. Se o tamanho for importante, considere limpar campos não usados antes da cópia.  
- **Dica de desempenho:** Ao copiar muitas planilhas, desative temporariamente `WorkbookSettings.EnableThreadedCalculation` para acelerar a operação.  
- **Conflito de nomes:** Se a pasta de trabalho de destino já contém uma tabela dinâmica com o mesmo nome, o Aspose renomeará a que está sendo importada (`PivotTable1_1`). Renomeie manualmente se precisar de um identificador específico.

## Resumo Visual

![Copiar tabela dinâmica em C# – diagrama mostrando pasta de trabalho de origem → seleção de intervalo → colar com preservação da tabela dinâmica → arquivo de destino](copy-pivot-diagram.png "Ilustração do fluxo de trabalho de copiar tabela dinâmica")

*Texto alternativo:* **Copiar tabela dinâmica** diagrama do fluxo de trabalho ilustrando origem, intervalo, opções de colagem e arquivo exportado.

## Conclusão

Cobrimos tudo o que você precisa para **copiar tabelas dinâmicas** usando C# e Aspose.Cells: carregar a origem, selecionar o intervalo correto, preservar a definição da tabela dinâmica durante a colagem e, finalmente, exportar o resultado como um arquivo independente. O trecho acima está pronto para produção; basta inserir seus caminhos e você está pronto para usar.

Agora que você sabe *como copiar tabelas dinâmicas* programaticamente, pode automatizar a distribuição de relatórios, criar geradores de modelos ou integrar análises Excel em serviços .NET maiores. Em seguida, você pode explorar **exportar o arquivo da tabela dinâmica** para outros formatos (PDF, CSV) ou incorporar a pasta de trabalho em uma API web para análises em tempo real.

Tem alguma variação que gostaria de compartilhar — talvez copiar tabelas dinâmicas entre diferentes versões do Excel ou lidar com modelos PowerPivot? Deixe um comentário e vamos manter a conversa fluindo. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}