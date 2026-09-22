---
category: general
date: 2026-02-15
description: Crie uma nova pasta de trabalho e exporte o Excel para TXT definindo
  a precisão numérica. Aprenda a definir dígitos significativos e limitar dígitos
  significativos em C#.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: pt
og_description: Crie uma nova planilha e exporte o Excel para TXT, definindo dígitos
  significativos para a precisão numérica. Um guia passo a passo em C#.
og_title: Criar Nova Pasta de Trabalho – Exportar Excel para TXT com Precisão
tags:
- C#
- Aspose.Cells
- Excel automation
title: Criar Nova Pasta de Trabalho e Exportar Excel para TXT com Precisão
url: /pt/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Nova Pasta de Trabalho – Exportar Excel para TXT com Formatação Numérica Precisa

Já se perguntou como **criar novos objetos workbook** em C# e exportá‑los instantaneamente para um arquivo de texto simples? Você não está sozinho. Em muitos cenários de pipelines de dados precisamos **exportar Excel para TXT** mantendo os números legíveis, o que significa limitar a quantidade de dígitos que aparecem após o ponto decimal.

Neste tutorial vamos percorrer todo o processo: desde a criação de uma nova pasta de trabalho, até a configuração da exportação para **definir dígitos significativos** (ou limitar dígitos significativos) e, por fim, gravar o arquivo no disco. Ao final você terá um trecho pronto‑para‑executar que respeita seus requisitos de **precisão numérica** — sem bibliotecas extras, sem mágica.

> **Dica profissional:** Se você já usa Aspose.Cells, as classes mostradas abaixo fazem parte dessa biblioteca. Se estiver em outra plataforma, os conceitos ainda se aplicam; basta trocar as chamadas de API.

---

## O que Você Precisa

- .NET 6+ (o código compila tanto no .NET Core quanto no .NET Framework)  
- Aspose.Cells para .NET (versão de avaliação ou licenciada) – instale via NuGet: `dotnet add package Aspose.Cells`  
- Qualquer IDE de sua preferência (Visual Studio, Rider, VS Code)  

É só isso. Sem arquivos de configuração adicionais, sem etapas ocultas.

---

## Etapa 1: Criar uma Nova Pasta de Trabalho

A primeira coisa a fazer é **criar nova workbook**. Pense na classe `Workbook` como um arquivo Excel vazio aguardando planilhas, células e dados.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Por que isso importa:** Ao iniciar com uma workbook limpa você evita formatações ocultas que poderiam interferir nas configurações de precisão mais adiante.

---

## Etapa 2: Configurar Opções de Salvamento de Texto – Definir Dígitos Significativos

Agora informamos ao Aspose.Cells quantos **dígitos significativos** queremos ao gravar um arquivo `.txt`. A classe `TxtSaveOptions` expõe a propriedade `SignificantDigits` que faz exatamente isso.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Explicação:** `SignificantDigits = 5` significa que o exportador manterá os cinco dígitos mais importantes de qualquer número, independentemente de onde o ponto decimal esteja. É uma forma prática de **definir precisão numérica** sem formatar manualmente cada célula.

---

## Etapa 3: Salvar a Pasta de Trabalho como Arquivo de Texto Simples

Com a workbook e as opções prontas, finalmente **exportamos Excel para txt**. O método `Save` recebe o caminho do arquivo e o objeto de opções que configuramos.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

Executar o programa gera um arquivo que se parece com isto:

```
12346
0.00012346
3.1416
```

Observe como cada número respeita a regra de **limitar dígitos significativos** que definimos anteriormente.

---

## Etapa 4: Verificar o Resultado (Opcional, mas Recomendado)

É fácil abrir o `numbers.txt` gerado em qualquer editor, mas você pode querer automatizar a verificação, especialmente em pipelines de CI.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

Se o console mostrar as três linhas acima, você definiu **dígitos significativos** com sucesso e a exportação funciona como esperado.

---

## Armadilhas Comuns & Como Evitá‑las

| Problema | Por que Acontece | Solução |
|----------|------------------|---------|
| Números aparecem com muitas casas decimais | `SignificantDigits` ficou no padrão (0) | Defina explicitamente `SignificantDigits` com a contagem desejada |
| Arquivo vazio é criado | Workbook nunca recebeu dados antes de salvar | Preencha as células **antes** de chamar `Save` |
| Caminho do arquivo lança `UnauthorizedAccessException` | Tentativa de gravar em pasta protegida | Use uma pasta onde você tenha permissão de escrita (ex.: `C:\Temp` ou `%USERPROFILE%\Documents`) |
| Precisão parece errada para números muito pequenos | A contagem de dígitos significativos inclui zeros à esquerda após o decimal | Lembre‑se que “significativo” ignora zeros iniciais; 0.000123456 com 5 dígitos torna‑se `0.00012346` |

---

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

A seguir está o programa completo e autocontido. Cole em um novo projeto de console e execute **Run**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Saída esperada no console**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

E o arquivo `numbers.txt` conterá as três linhas mostradas acima.

---

## Próximos Passos: Indo Além do Básico

- **Exportar outros formatos** – Aspose.Cells também suporta CSV, HTML e PDF. Troque `TxtSaveOptions` por `CsvSaveOptions` ou `PdfSaveOptions` conforme necessário.  
- **Precisão dinâmica** – você pode calcular `SignificantDigits` em tempo de execução com base na entrada do usuário ou em arquivos de configuração.  
- **Múltiplas planilhas** – itere sobre `workbook.Worksheets` e exporte cada uma para seu próprio arquivo `.txt`.  
- **Localização** – controle o separador decimal (`.` vs `,`) via `CultureInfo` se precisar adequar às configurações regionais.  

Todas essas extensões ainda se baseiam na ideia central que abordamos: **criar nova workbook**, configurar a exportação e **definir precisão numérica** para atender aos requisitos de relatório.

---

## Resumo

Pegamos uma instância fresca de **criar nova workbook**, preenchemos com dados e demonstramos como **exportar Excel para TXT** enquanto **definimos dígitos significativos** para limitar a precisão da saída. O exemplo completo funciona imediatamente, e a explicação cobriu o *porquê* de cada linha para que você possa adaptá‑lo aos seus próprios projetos.

Sinta‑se à vontade para experimentar — altere o valor de `SignificantDigits`, adicione mais planilhas ou troque o formato de saída. Se encontrar algum obstáculo, consulte a documentação do Aspose.Cells ou deixe um comentário abaixo. Boa codificação!

---

![Criar novo exemplo de workbook](/images/create-new-workbook.png "Captura de tela mostrando um IDE C# com o código de criar nova workbook")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}