---
category: general
date: 2026-02-21
description: Salve o Excel como txt com controle preciso sobre os dígitos significativos.
  Exporte o Excel para txt em C# e defina os dígitos significativos facilmente.
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: pt
og_description: Salve o Excel como txt rapidamente. Aprenda como exportar Excel para
  txt, definir casas decimais significativas e controlar a saída de texto usando C#.
og_title: Salvar Excel como txt – Exportar números com dígitos significativos em C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Salvar Excel como txt – Guia completo em C# para exportar números com dígitos
  significativos
url: /pt/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

tutorial we’ll show you a straight‑forward way to **export Excel to txt** while **setting significant digits** so the output looks exactly how you want it. By the end you’ll have a ready‑to‑run C# snippet that saves a workbook as text, exports numbers to txt, and gives you full control over the numeric format."

Translate.

Proceed similarly for all sections.

Make sure to keep markdown formatting.

Also keep blockquote > Pro tip.

Translate.

Now code block placeholders remain unchanged.

List items translate.

Edge-case etc.

Let's write final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salvar Excel como txt – Guia Completo em C# para Exportar Números com Dígitos Significativos

Já precisou **salvar Excel como txt** mas temia que os números perdessem a precisão? Você não está sozinho. Muitos desenvolvedores se deparam com um obstáculo ao tentar exportar Excel para txt e acabam com casas decimais demais ou um resultado arredondado.  

Neste tutorial vamos mostrar uma maneira direta de **exportar Excel para txt** enquanto **define dígitos significativos** para que a saída fique exatamente como você deseja. Ao final, você terá um trecho de código C# pronto‑para‑executar que salva uma pasta de trabalho como texto, exporta números para txt e oferece controle total sobre o formato numérico.

## O que você vai aprender

- Como criar uma nova pasta de trabalho e gravar dados numéricos.  
- A forma correta de **definir dígitos significativos** usando `TxtSaveOptions`.  
- Como **salvar a pasta de trabalho como texto** e verificar o resultado.  
- Tratamento de casos extremos (números grandes, valores negativos, questões de localidade).  
- Dicas rápidas para ajustar ainda mais a saída (alteração de delimitador, codificação).

### Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.6+).  
- O pacote NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).  
- Noções básicas de sintaxe C# — não é necessário conhecimento profundo de interop Excel.

> **Dica profissional:** Se você estiver usando o Visual Studio, habilite *nullable reference types* (`<Nullable>enable</Nullable>`) para capturar possíveis bugs de null antecipadamente.

---

## Etapa 1: Inicializar a Workbook e gravar um número

Primeiro, precisamos de um objeto workbook. Pense nele como a representação em memória de um arquivo Excel.  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**Por que isso importa:**  
Criar a workbook programaticamente evita a sobrecarga do interop COM, e `PutValue` detecta automaticamente o tipo de dado, garantindo que a célula seja tratada como número — não como string.

---

## Etapa 2: Configurar TxtSaveOptions para controlar os dígitos significativos

A classe `TxtSaveOptions` é onde a mágica acontece. Ao definir `SignificantDigits`, você informa ao Aspose.Cells quantos dígitos relevantes manter quando o arquivo for gravado.

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**Por que você deve definir isso:**  
Ao **exportar números para txt**, muitas vezes é necessário uma representação concisa (por exemplo, para sistemas de relatórios que aceitam apenas certa precisão). A propriedade `SignificantDigits` garante arredondamento consistente independentemente do tamanho original do número.

---

## Etapa 3: Salvar a Workbook como arquivo de texto

Agora gravamos a workbook no disco usando as opções que acabamos de definir.

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**O que você verá:**  
Abra `Numbers.txt` e você obterá uma única linha:

```
12350
```

O valor original `12345.6789` foi arredondado para **quatro dígitos significativos**, exatamente como solicitado.

---

## Etapa 4: Verificar a saída (Opcional, mas recomendado)

Testes automatizados são um ótimo hábito. Aqui está uma verificação rápida que você pode executar logo após salvar:

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

Executar este bloco imprimirá uma marca de seleção verde se tudo estiver correto, dando confiança de que a operação **save excel as txt** funcionou como esperado.

---

## Variações comuns e casos extremos

### Exportar múltiplas células ou intervalos

Se precisar **exportar excel para txt** de um intervalo inteiro, basta preencher mais células antes de salvar:

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

As mesmas `TxtSaveOptions` aplicarão a regra de 4 dígitos a cada valor, produzindo:

```
12350
0.0001235
-98800
```

### Alterar o delimitador

Alguns sistemas downstream esperam valores separados por tabulação. Ajuste o delimitador assim:

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

Agora cada célula em uma linha aparece separada por uma tabulação.

### Lidar com separadores decimais específicos de localidade

Se seu público usa vírgulas para decimais, defina a cultura:

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

A saída respeitará a localidade, transformando `12350` em `12 350` (espaço como separador de milhares em francês).

---

## Exemplo completo (pronto para copiar e colar)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**Conteúdo esperado de `Numbers.txt` (delimitador padrão, 4 dígitos significativos):**

```
12350	0.0001235	-98800
```

A tabulação (`\t`) aparece porque deixamos o delimitador no padrão (tab) no exemplo; altere para vírgula se preferir CSV.

---

## Conclusão

Agora você sabe exatamente **como salvar Excel como txt** controlando o número de dígitos significativos. Os passos — criar a workbook, definir `TxtSaveOptions.SignificantDigits` e salvar — são tudo que você precisa para **exportar excel para txt** de forma confiável.  

A partir daqui você pode:

- **Exportar números para txt** em conjuntos de dados maiores.  
- Ajustar delimitadores, codificação ou configurações de cultura para atender a qualquer sistema downstream.  
- Combinar esta abordagem com outros recursos do Aspose.Cells (estilos, fórmulas) antes da exportação.

Experimente, ajuste o `SignificantDigits` para 2 ou 6 e veja como a saída muda. A flexibilidade de **save workbook as text** a torna uma ferramenta útil em qualquer pipeline de troca de dados.

---

### Tópicos relacionados que você pode explorar a seguir

- **Export Excel to CSV** com ordenação personalizada de colunas.  
- **Read txt files back into a workbook** (`Workbook.Load` com `LoadOptions`).  
- **Batch processing** de múltiplas planilhas e consolidação em um único arquivo txt.  
- **Performance tuning** para exportações em larga escala (streaming vs. in‑memory).

Sinta‑se à vontade para deixar um comentário se encontrar algum obstáculo, ou compartilhar como você personalizou a exportação nos seus próprios projetos. Boa codificação!  

---  

*Imagem: Uma captura de tela do arquivo `Numbers.txt` gerado mostrando valores arredondados.*  
*Texto alternativo: “Arquivo Numbers.txt exibindo 12350, 0,0001235 e -98800 após salvar Excel como txt com 4 dígitos significativos.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}