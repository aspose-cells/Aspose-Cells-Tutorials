---
category: general
date: 2026-03-30
description: Aprenda a formatar números com separador usando Aspose.Cells em C#. Inclui
  definir formato numérico personalizado, adicionar separador de milhares, formatar
  casas decimais e como formatar a célula.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: pt
og_description: Formatar número com separador em C#. Este guia mostra como definir
  formato numérico personalizado, adicionar separador de milhares, formatar casas
  decimais e como formatar célula usando Aspose.Cells.
og_title: Formatar número com separador em C# – Tutorial Aspose.Cells
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Formatar número com separador em C# – Guia completo do Aspose.Cells
url: /pt/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formatar Número com Separador em C# – Guia Completo do Aspose.Cells

Já precisou **formatar número com separador** em uma planilha, mas não sabia qual chamada de API usar? Você não está sozinho—os desenvolvedores constantemente lidam com separadores de milhar, casas decimais e padrões personalizados ao exportar dados.  

Boa notícia: o Aspose.Cells torna isso muito fácil. Neste tutorial, percorreremos um exemplo do mundo real que **define um formato numérico personalizado**, **adiciona um separador de milhar**, **formata casas decimais**, e mostra **como formatar célula** para saída como string. Ao final, você terá um trecho pronto‑para‑executar que pode inserir em qualquer projeto .NET.

## O Que Este Guia Abrange

* O pacote NuGet exato que você precisa e como instalá‑lo.  
* Código passo a passo que cria uma workbook, grava um valor numérico e aplica um formato personalizado.  
* Por que `ExportTableOptions.ExportAsString` é a forma preferida de obter um valor formatado.  
* Armadilhas comuns—como esquecer de habilitar `ExportAsString` ou usar a máscara de formato errada.  
* Como ajustar a máscara de formato se precisar de um número diferente de casas decimais ou de um estilo de separador diferente.

Nenhum link de documentação externa é necessário; tudo que você precisa está aqui. Vamos mergulhar.

---

## Pré‑requisitos

| Requisito | Motivo |
|-------------|--------|
| .NET 6.0 ou superior | Aspose.Cells 23.10+ tem como alvo .NET Standard 2.0+, portanto .NET 6 é seguro e atual. |
| Visual Studio 2022 (ou qualquer IDE C#) | Facilita a depuração e o gerenciamento de pacotes. |
| Aspose.Cells for .NET NuGet package | Fornece as classes `Workbook`, `Worksheet` e `ExportTableOptions` que usaremos. |

Você pode instalar o pacote via o Console do Gerenciador de Pacotes:

```powershell
Install-Package Aspose.Cells
```

É isso—nenhum DLL extra, sem interop COM, apenas uma única referência NuGet.

---

## Etapa 1: Inicializar uma Nova Workbook (Como formatar célula)

A primeira coisa que fazemos é criar uma nova instância de `Workbook`. Pense nela como um arquivo Excel vazio pronto para receber dados.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Por que isso importa:** `Workbook` é o ponto de entrada para todas as operações no Aspose.Cells. Ao obter a primeira planilha (`Worksheets[0]`) temos uma tela limpa sem precisar nomear uma planilha.

---

## Etapa 2: Gravar um Valor Numérico na Célula Alvo

Em seguida, inserimos um número bruto na célula **A1**. O valor ainda não está formatado—é apenas um double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Dica profissional:** Use `PutValue` em vez de `PutString` quando pretender aplicar formatação numérica posteriormente. Isso preserva o tipo de dado subjacente, permitindo cálculos compatíveis com Excel.

---

## Etapa 3: Definir Formato Numérico Personalizado (Adicionar Separador de Milhares & Formatar Casas Decimais)

Agora vem o coração do tutorial: definir uma máscara de formato que indica ao Aspose.Cells como exibir o número. A máscara `#,##0.00` faz três coisas:

1. **`#,##0`** – adiciona um separador de milhares (vírgula por padrão).  
2. **`.00`** – força exatamente duas casas decimais.  

Se precisar de um número diferente de casas decimais, basta mudar a quantidade de `0`s após o ponto decimal.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Por que usamos `ExportAsString`**: Por padrão, `ExportString` retorna o valor bruto. Definir `ExportAsString = true` força a API a aplicar a máscara `NumberFormat` antes de converter para texto. Isso é essencial quando você precisa da representação exata em string para relatórios, payloads JSON ou exibição na UI.

---

## Etapa 4: Exportar o Texto Formatado (Como formatar célula)

Com as opções prontas, chamamos `ExportString` na mesma célula. O método respeita a máscara que definimos e devolve uma string bem formatada.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

Executar o programa imprime **`12,345.68`** no console—exatamente o formato que solicitamos.

> **Caso limite:** Se o número de origem tiver mais de duas casas decimais, a máscara o arredonda. Se precisar de truncamento em vez de arredondamento, será necessário pré‑processar o valor com `Math.Truncate` antes de chamar `PutValue`.

---

## Etapa 5: Ajustando o Formato – Variações Comuns

### 5.1 Alterar Precisão Decimal

Quer três casas decimais? Basta substituir a máscara:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Usar um Separador de Milhares Diferente

Algumas localidades preferem um espaço ou um ponto. Você pode inserir o caractere diretamente:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Ou confiar nas configurações de cultura da workbook:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Prefixo ou Sufixo (Moeda, Percentual)

Adicione um símbolo de dólar ou de percentual diretamente na máscara:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Observação:** A máscara diferencia maiúsculas de minúsculas. `$` e `%` são símbolos literais; eles não afetam o valor numérico subjacente.

---

## Etapa 6: Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo que você pode copiar para um novo aplicativo console. Ele inclui todas as etapas, comentários e a verificação da saída final.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Execute o programa (`dotnet run` no terminal ou pressione F5 no Visual Studio) e você verá o número formatado impresso exatamente como mostrado.

---

## Perguntas Frequentes (FAQ)

**Q: Isso funciona com versões mais antigas do Excel?**  
A: Sim. A máscara de formato segue a sintaxe nativa de formatação numérica do Excel, portanto qualquer versão que reconheça `#,##0.00` renderizará a mesma string.

**Q: E se eu precisar formatar um intervalo de células?**  
A: Percorra o intervalo desejado e aplique o mesmo `ExportTableOptions` a cada célula, ou defina a propriedade `Style.Custom` no intervalo e então chame `ExportString` em uma única célula.

**Q: Posso exportar diretamente para CSV com esses formatos aplicados?**  
A: Absolutamente. Use `Workbook.Save("output.csv", SaveFormat.CSV);` após definir o formato em cada célula. O Aspose.Cells respeita o `Style` da célula ao gerar o CSV.

---

## Conclusão

Acabamos de mostrar como **formatar número com separador** em C# usando Aspose.Cells, cobrindo tudo desde **definir formato numérico personalizado** até **adicionar separador de milhares**, **formatar casas decimais**, e o essencial **como formatar célula** para exportação como string. O código é totalmente autocontido, funciona com .NET 6+ e pode ser adaptado para qualquer localidade ou requisito de precisão.

Em seguida, você pode explorar:

* Aplicar a mesma técnica a datas e horas (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Automatizar exportações em massa onde cada coluna precisa de uma máscara diferente.  
* Integrar as strings formatadas em relatórios PDF com Aspose.Words.

Experimente isso, e você rapidamente se tornará a pessoa de referência para formatação de planilhas em sua equipe. Feliz codificação! (Imagem: ![Captura de tela mostrando número formatado com separador no Aspose.Cells](image-placeholder.png){alt="Número formatado com separador exibido na saída do Aspose.Cells"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}