---
category: general
date: 2026-02-15
description: como copiar fonte e aplicar estilo de célula em C# com um exemplo simples.
  aprenda como obter o estilo da célula e usar a formatação de célula para definir
  o tamanho da fonte da caixa de texto.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: pt
og_description: como copiar a fonte de uma célula da planilha e aplicar o estilo da
  célula a uma caixa de texto. este guia mostra como obter o estilo da célula, usar
  a formatação da célula e definir o tamanho da fonte da caixa de texto.
og_title: como copiar a fonte de uma célula do Excel – tutorial completo de C#
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: como copiar a fonte de uma célula do Excel para uma caixa de texto – guia passo
  a passo
url: /pt/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como copiar fonte de uma célula do Excel para um TextBox – Tutorial Completo em C#

Já precisou **copiar fonte** de uma célula de planilha e fazer um TextBox da UI ficar exatamente igual? Você não está sozinho. Em muitas ferramentas de relatório ou painéis personalizados, você acaba extraindo dados do Excel e tentando manter a fidelidade visual — família da fonte, tamanho e cor — intactas.  

A boa notícia é que, com apenas algumas linhas de C#, você pode **obter estilo da célula**, ler suas propriedades de fonte e **aplicar estilo da célula** a qualquer controle de text‑box. Neste tutorial, percorreremos um exemplo completo e executável que mostra como **usar formatação de célula** e até **definir tamanho da fonte do textbox** programaticamente.

---

## O que você aprenderá

- Como recuperar um objeto `TextBox` de um componente de grade (`gridJs` em nosso exemplo)
- Como ler a família da fonte, tamanho e cor de uma célula específica do Excel (`B2`)
- Como copiar esses atributos de fonte para o textbox de modo que a UI reflita a planilha
- Armadilhas comuns (por exemplo, conversão de cor) e algumas **dicas avançadas** para manter seu código robusto
- Um trecho de código pronto‑para‑executar que você pode inserir em um aplicativo console ou projeto WinForms

**Pré-requisitos**  
Você deve ter:

1. .NET 6+ (ou .NET Framework 4.8) instalado  
2. O pacote NuGet EPPlus (para manipulação de Excel)  
3. Um controle de grade que expõe um dicionário `TextBoxes` (o exemplo usa um `gridJs` fictício, mas a ideia funciona com qualquer biblioteca UI)

Agora, vamos colocar a mão na massa.

---

## Etapa 1: Configurar o Projeto e Carregar a Planilha

Primeiro, crie um novo projeto console ou WinForms e adicione o EPPlus:

```bash
dotnet add package EPPlus --version 6.*
```

Em seguida, carregue a pasta de trabalho e obtenha a célula cujo estilo você deseja copiar.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Por que isso importa:** EPPlus fornece acesso direto ao objeto `Style`, que contém o sub‑objeto `Font`. A partir dele, você pode ler `Name`, `Size` e `Color`. Este é o núcleo da operação de **obter estilo da célula**.

---

## Etapa 2: Obter o TextBox de Destino da sua Grade

Assumindo que sua grade UI (`gridJs`) armazena text boxes em um dicionário indexado pelo nome da coluna, você pode recuperar o que deseja da seguinte forma:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

Se você estiver usando WinForms, `notesTextBox` pode ser um controle `TextBox`; para WPF pode ser um elemento `TextBox`, e para uma grade baseada na web pode ser um objeto de interop JavaScript. O ponto principal é que você tem uma referência que pode manipular.

---

## Etapa 3: Transferir a Família da Fonte

Agora que temos tanto o estilo de origem quanto o controle de destino, copie a família da fonte.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Dica avançada:** Nem todas as frameworks UI expõem uma propriedade `FontFamily` que aceita uma string simples. No WinForms você definiria `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. Ajuste conforme necessário.

---

## Etapa 4: Transferir o Tamanho da Fonte

O tamanho da fonte é armazenado como `float` no EPPlus. Aplique-o diretamente:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

Se o seu controle usa pontos (como a maioria), você pode atribuir o valor sem conversão. Para grades baseadas em CSS, talvez seja necessário acrescentar "pt".

---

## Etapa 5: Transferir a Cor da Fonte

A conversão de cor é a parte mais complicada porque EPPlus armazena cores como inteiros ARGB, enquanto muitas frameworks UI esperam um `System.Drawing.Color` ou uma string hex CSS.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Por que isso funciona:** `GetColor()` resolve cores baseadas em tema e retorna um `System.Drawing.Color` concreto. Se a célula usar a cor padrão (sem definição explícita), usamos preto como padrão para evitar exceções de referência nula.

---

## Exemplo Completo em Funcionamento

Juntando tudo, aqui está um aplicativo console minimalista que lê um arquivo Excel, extrai a fonte de **B2** e a aplica a um textbox simulado.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Saída esperada (supondo que B2 use Arial, 12 pt, azul):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Execute o programa, abra sua UI e você verá que o textbox “Notes” agora reflete exatamente a estilização da fonte da célula **B2**. Nenhum ajuste manual necessário.

---

## Perguntas Frequentes & Casos Limítrofes

### E se a célula usar uma cor de tema em vez de um valor RGB explícito?

O `GetColor()` do EPPlus resolve automaticamente cores de tema para um `System.Drawing.Color` concreto. Contudo, se você estiver usando uma biblioteca mais antiga que só retorna o índice do tema, será necessário mapear esse índice para uma paleta de cores manualmente.

### Posso copiar outros atributos de estilo (por exemplo, negrito, itálico)?

Com certeza. O objeto `ExcelStyle.Font` também expõe `Bold`, `Italic`, `Underline` e `Strike`. Basta definir as propriedades correspondentes no seu controle UI:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### E se o controle de grade não expuser uma propriedade `FontColor`?

A maioria das frameworks UI modernas possui, mas se a sua aceita apenas uma string CSS, converta o `Color` para hex:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### Como lidar com várias células ao mesmo tempo?

Percorra o intervalo desejado, obtenha o estilo de cada célula e aplique-o ao textbox correspondente. Lembre‑se de armazenar em cache os objetos de estilo se estiver processando muitas linhas para evitar perdas de desempenho.

---

## Dicas Avançadas & Armadilhas Comuns

- **Cache o ExcelPackage** – abrir e fechar o arquivo para cada célula é caro. Carregue a pasta de trabalho uma vez e reutilize o objeto `ExcelWorksheet`.
- **Cuidado com cores nulas** – uma célula que herda a cor padrão retorna `null`. Sempre forneça um valor padrão (preto ou o padrão do controle).
- **Atenção ao dimensionamento DPI** – se você estiver mirando monitores de alta DPI, os tamanhos de fonte podem aparecer ligeiramente maiores. Ajuste usando `Graphics.DpiX` se necessário.
- **Segurança de thread** – EPPlus não é thread‑safe. Se você estiver processando várias planilhas em paralelo, crie um `ExcelPackage` separado por thread.

---

## Conclusão

Agora você sabe **como copiar fonte** de uma célula do Excel e **aplicar estilo da célula** a qualquer controle de text‑box usando C#. Ao recuperar o `Style` da célula, extrair suas propriedades `Font` e atribuí‑las ao elemento UI, você mantém a consistência visual sem cópia manual.

A solução completa — carregar a pasta de trabalho, obter o estilo da célula e definir a família, tamanho e cor da fonte do textbox — cobre o núcleo de **usar formatação de célula** e demonstra como **definir tamanho da fonte do textbox** corretamente.

Em seguida, tente estender o exemplo para copiar cores de fundo, bordas ou até mesmo o conteúdo completo das células. Se você estiver trabalhando com uma biblioteca de data‑grid que suporte renderização rica de células, agora pode alimentá‑la com as mesmas informações de estilo extraídas do Excel, mantendo sua UI e relatórios perfeitamente sincronizados.

Tem mais perguntas? Deixe um comentário ou explore tópicos relacionados como “binding dinâmico Excel‑para‑UI” e “conversão de cor consciente de tema”. Feliz codificação!

---

![exemplo de como copiar fonte](placeholder-image.jpg "como copiar fonte de célula do Excel para TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}