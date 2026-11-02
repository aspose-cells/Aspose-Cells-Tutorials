---
category: general
date: 2026-03-01
description: Como criar uma planilha em C# rapidamente—aprenda a escrever valores
  em células, definir o formato numérico da célula e formatar números da célula com
  passos simples.
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: pt
og_description: Como criar uma planilha em C#? Este guia mostra como escrever um valor
  em uma célula, definir o formato numérico da célula e formatar o número da célula
  em apenas algumas linhas de código.
og_title: Como criar uma pasta de trabalho em C# – Escrever valor e formatar número
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Como criar uma pasta de trabalho em C# – escrever valor e formatar número
url: /pt/net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Criar Workbook em C# – Gravar Valor e Formatizar Número

Criar um workbook em C# é uma tarefa comum quando você precisa gerar arquivos Excel dinamicamente. Neste guia vamos mostrar como gravar um valor em uma célula e formatar o número da célula para que a planilha final fique bem apresentável.

Se você já ficou olhando para uma planilha em branco e se perguntou por que os números continuam exibindo muitas casas decimais, não está sozinho. Vamos cobrir tudo, desde a inicialização do objeto workbook até a definição de um formato numérico personalizado, e ainda daremos algumas dicas para casos extremos que você pode encontrar mais tarde.

## O Que Você Vai Aprender

- **Inicializar** uma nova instância de `Workbook`.  
- **Gravar valor em célula** usando o método `PutValue`.  
- **Definir formato numérico da célula** com um objeto `Style`, obtendo uma exibição limpa com duas casas decimais.  
- Verificar o resultado lendo a célula novamente ou abrindo o arquivo no Excel.  

Nenhuma biblioteca externa além do Aspose.Cells padrão (ou qualquer API similar) é necessária, e o código funciona em .NET 6+ sem configuração extra.

---

## Como Criar Workbook – Inicializar o Objeto

Primeiro de tudo: você precisa de um objeto workbook para conter suas planilhas. Pense no `Workbook` como o arquivo Excel completo, enquanto cada `Worksheet` é uma aba única.

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*Por que isso importa:* Criar o workbook aloca as estruturas internas que mais tarde armazenarão linhas, colunas e formatações. Sem esse objeto, não há onde gravar um valor em uma célula.

> **Dica profissional:** Se você pretende trabalhar com um arquivo existente, substitua `new Workbook()` por `new Workbook("template.xlsx")` para carregar um modelo e preservar seus estilos.

## Gravar Valor em Célula

Agora que temos um workbook, vamos inserir um número na célula **A1** da primeira planilha.

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*Por que usamos `PutValue`*: Esse método detecta automaticamente o tipo de dado, então você não precisa fazer cast ou conversão manualmente. Ele também respeita o estilo existente da célula, o que é útil quando você posteriormente **definir o formato numérico da célula**.

### Verificação Rápida

Se você ler a célula novamente, verá o valor bruto:

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

Esse é o número antes de qualquer formatação ser aplicada.

## Definir Formato Numérico da Célula

Exibir um double bruto com muitas casas decimais nem sempre é amigável ao usuário. Vamos limitá-lo a duas casas decimais significativas.

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

A propriedade `Number` corresponde aos IDs de formatos numéricos internos do Excel. `2` significa “Número com duas casas decimais”. Se precisar de um formato diferente — por exemplo, moeda ou data — você usaria outro ID ou uma string de formato personalizada.

### Alternativa: String de Formato Personalizado

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*Por que escolher um estilo personalizado?* Ele oferece controle total, especialmente quando os IDs internos não cobrem as configurações regionais que você precisa.

## Verificar Saída (Opcional, mas Recomendado)

Depois de aplicar o estilo, você pode salvar o workbook e abri‑lo no Excel para confirmar a aparência.

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

Você deverá ver **123.46** na célula A1 — exatamente duas casas decimais, graças ao formato que definimos.

---

### Exemplo Completo Funcional

Juntando tudo, aqui está um programa autocontido que você pode copiar‑colar em um aplicativo console.

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**Saída esperada ao executar o programa:**

```
Cell A1 shows: 123.46
```

Abra `FormattedWorkbook.xlsx` no Excel e você verá o mesmo valor formatado.

---

## Variações Comuns & Casos de Borda

### 1. Diferentes Formatos Numéricos

| Objetivo | ID do Formato | Trecho de Código |
|----------|---------------|------------------|
| Moeda (duas casas decimais) | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| Percentual (sem casas decimais) | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| Notação científica | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

Se nenhum dos IDs internos atender, recorra a uma string personalizada como mostrada anteriormente.

### 2. Separadores Decimais Específicos de Cultura

Algumas localidades usam vírgulas como separador decimal. Você pode impor um formato sensível à cultura:

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. Gravar Texto ao Invés de Números

Quando precisar **como gravar célula** com uma string, basta passar a string para `PutValue`:

```csharp
cellA1.PutValue("Total Revenue");
```

Nenhum formato numérico é necessário, mas você ainda pode aplicar estilos de fonte.

### 4. Grandes Conjuntos de Dados

Se estiver preenchendo milhares de linhas, a inserção em lote (`Cells.ImportArray`) é mais rápida que iterar com `PutValue`. A abordagem de formatação permanece a mesma; você apenas aplica o estilo a um intervalo:

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## Perguntas Frequentes

**P: Isso funciona com .NET Core?**  
R: Absolutamente. Aspose.Cells suporta .NET Standard 2.0 e posteriores, então você pode direcionar .NET 5, .NET 6 ou .NET 7 sem alterações.

**P: E se eu precisar de mais de duas casas decimais?**  
R: Altere a propriedade `Number` para o ID interno apropriado (por exemplo, `3` para três casas decimais) ou ajuste a string de formato personalizada (`"#,##0.000"`).

**P: Posso aplicar o formato a uma coluna inteira de uma vez?**  
R: Sim. Use `Cells["A:A"]` para obter a coluna inteira e então `SetStyle`.

---

## Conclusão

Agora você sabe **como criar objetos workbook** em C#, **gravar valor em célula** e **definir o formato numérico da célula** para que os números apareçam exatamente como você deseja. Ao dominar esses fundamentos, você estará preparado para gerar relatórios Excel, faturas ou exportações de dados com aparência profissional e esforço mínimo.

Em seguida, você pode explorar **formatar número de célula** para datas, percentuais ou formatação condicional — cada um se baseia nos mesmos princípios que abordamos. Mergulhe na documentação do Aspose.Cells para opções de estilo mais avançadas, ou experimente combinar várias planilhas em um único workbook para relatórios mais ricos.

Boa codificação, e lembre‑se: uma planilha bem formatada é apenas

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}