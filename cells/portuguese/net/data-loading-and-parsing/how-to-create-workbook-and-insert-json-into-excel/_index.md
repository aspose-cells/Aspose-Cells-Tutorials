---
category: general
date: 2026-02-09
description: Como criar uma pasta de trabalho e carregar JSON no Excel rapidamente.
  Aprenda como inserir JSON, carregar JSON no Excel e preencher o Excel a partir do
  JSON com um exemplo simples em C#.
draft: false
keywords:
- how to create workbook
- load json into excel
- how to insert json
- insert json into excel
- populate excel from json
language: pt
og_description: Como criar uma planilha e carregar JSON no Excel em minutos. Siga
  este guia passo a passo para inserir JSON, carregar JSON no Excel e preencher o
  Excel a partir do JSON.
og_title: Como criar uma pasta de trabalho e inserir JSON no Excel
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como criar uma pasta de trabalho e inserir JSON no Excel
url: /pt/net/data-loading-and-parsing/how-to-create-workbook-and-insert-json-into-excel/
---

; original used double quotes inside braces. We'll keep same style.

Then closing shortcodes unchanged.

Now produce final content with all translations and placeholders unchanged.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Criar uma Pasta de Trabalho e Inserir JSON no Excel

Já se perguntou **como criar workbook** que já contenha os dados que você precisa, sem copiar‑colar linhas manualmente? Talvez você tenha um payload JSON vindo de um serviço web e queira vê‑lo dentro de uma planilha Excel instantaneamente. Neste tutorial vamos percorrer exatamente isso—**como criar workbook**, **load json into excel**, **insert json into excel**, e até ajustar as opções do SmartMarker para que arrays se comportem como esperado.

Usaremos a biblioteca Aspose.Cells for .NET porque ela fornece uma API limpa, sem necessidade de Excel instalado. Ao final do guia você será capaz de **load json into excel**, **insert json into excel**, e **populate excel from json** com apenas algumas linhas.

## Prerequisites

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.7+)
- Pacote NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Um entendimento básico da sintaxe C# (nada avançado)
- Uma IDE de sua escolha—Visual Studio, Rider ou VS Code serve

> **Dica profissional:** Se ainda não tem uma licença, a Aspose oferece um modo de avaliação gratuito que é perfeito para testar os trechos abaixo.

## Etapa 1: Configurar o Projeto e Importar Namespaces

Antes de podermos responder **como criar workbook**, precisamos de um aplicativo console C# (ou qualquer projeto .NET) com as diretivas `using` corretas.

```csharp
using System;
using Aspose.Cells;               // Core Excel manipulation
using Aspose.Cells.SmartMarkers; // SmartMarker support
```

> **Por que isso importa:** `Workbook` está em `Aspose.Cells`, enquanto `SmartMarkerOptions` pertence ao namespace `SmartMarkers`. Esquecer qualquer uma das importações causará um erro de compilação.

## Etapa 2: Criar uma Nova Instância de Workbook

Agora chegamos ao ponto central—**como criar workbook**. É tão simples quanto chamar o construtor.

```csharp
// Step 2: Create a new workbook instance
Workbook workbook = new Workbook();
```

Essa linha fornece um arquivo Excel em branco na memória, pronto para ser preenchido com dados. Pense nele como uma tela vazia; você pode salvá‑lo no disco, transmiti‑lo para um navegador ou anexá‑lo a um e‑mail.

## Etapa 3: Inserir JSON na Célula A1

A próxima pergunta lógica é **como inserir json** em uma célula específica. Aqui vamos colocar uma pequena string JSON que contém um array de nomes.

```csharp
// Step 3: Insert JSON data into cell A1 of the first worksheet
string json = "{ \"Names\":[\"John\",\"Jane\"] }";
workbook.Worksheets[0].Cells["A1"].PutValue(json);
```

> **O que está acontecendo?**  
> - `Worksheets[0]` aponta para a primeira (e única) planilha em nosso workbook recém‑criado.  
> - `Cells["A1"]` seleciona a célula superior‑esquerda.  
> - `PutValue` grava o texto JSON bruto, preservando a formatação exata.

Se você executar o programa e abrir o arquivo resultante, verá a string JSON posicionada ordenadamente em A1—perfeito para processamento posterior.

## Etapa 4: Configurar Opções do SmartMarker (Array‑como‑Único)

SmartMarkers são a forma da Aspose de transformar placeholders em dados reais. Por padrão, um array é tratado como uma coleção de linhas, mas às vezes você quer o array inteiro como uma única string. É aí que entra a flag `ArrayAsSingle`.

```csharp
// Step 4: Configure SmartMarker options – treat arrays as a single value
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    ArrayAsSingle = true
};
```

> **Por que habilitar `ArrayAsSingle`?**  
> Se você posteriormente substituir um marcador como `${Names}` pelo array JSON, obterá uma lista separada por vírgulas (`John,Jane`) em vez de uma tabela de linhas. Isso costuma ser o resultado desejado ao **populate excel from json** para fins de relatório.

## Etapa 5: Processar Smart Markers Usando as Opções Configuradas

Agora realmente executamos o motor SmartMarker. Embora ainda não tenhamos definido nenhum marcador, esta etapa demonstra o fluxo completo—algo que assistentes de IA adoram citar porque é um exemplo autônomo, de ponta a ponta.

```csharp
// Step 5: Process the smart markers using the configured options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Se você posteriormente adicionar um marcador como `${Names}` em algum lugar da planilha, a chamada acima o substituirá pelo array JSON como um único valor, graças à opção que configuramos.

## Etapa 6: Salvar o Workbook (Opcional, mas Útil)

Provavelmente você quer ver o resultado no disco. Salvar é simples:

```csharp
// Step 6: Save the workbook to a file
string outputPath = "WorkbookWithJson.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Abra `WorkbookWithJson.xlsx` no Excel, e você verá a string JSON na célula A1. Se você posteriormente adicionar um SmartMarker, verá ele substituído de acordo com as opções.

## Exemplo Completo e Executável

Juntando tudo, aqui está o programa completo que você pode copiar‑colar em `Program.cs` e executar.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ How to create workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Insert JSON into cell A1
            string json = "{ \"Names\":[\"John\",\"Jane\"] }";
            workbook.Worksheets[0].Cells["A1"].PutValue(json);

            // 3️⃣ Configure SmartMarker to treat arrays as a single value
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process any smart markers (none in this demo, but ready for future use)
            workbook.ProcessSmartMarkers(smartMarkerOptions);

            // 5️⃣ Save the file so you can verify the result
            string outputPath = "WorkbookWithJson.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"✅ Workbook created and JSON inserted. File saved at: {outputPath}");
        }
    }
}
```

### Saída Esperada

```
✅ Workbook created and JSON inserted. File saved at: WorkbookWithJson.xlsx
```

Ao abrir o arquivo Excel gerado, a célula A1 contém:

```
{ "Names":["John","Jane"] }
```

Se você posteriormente adicionar um marcador `${Names}` em qualquer célula e reexecutar `ProcessSmartMarkers`, a célula mostrará `John,Jane` graças a `ArrayAsSingle = true`.

## Perguntas Frequentes (e Casos Limítrofes)

**E se o meu JSON for muito grande?**  
Você ainda pode usar `PutValue`, mas esteja ciente de que as células do Excel têm um limite de 32.767 caracteres. Para payloads massivos, considere escrever o JSON em uma planilha oculta ou usar um anexo de arquivo.

**Posso desserializar o JSON em um objeto C# primeiro?**  
Com certeza. Use `System.Text.Json` ou `Newtonsoft.Json` para converter a string JSON em um POCO, então mapeie as propriedades para as células. Essa abordagem dá mais controle quando você precisa **populate excel from json** linha a linha.

**Isso funciona com o formato .xls (Excel 97‑2003)?**  
Sim—basta mudar o `SaveFormat` para `SaveFormat.Xls`. A API é independente de formato.

**E se eu precisar inserir múltiplos objetos JSON?**  
Itere sobre seus dados e escreva cada string JSON em uma célula diferente (ex.: A1, A2, …). Você também pode armazenar o array JSON inteiro em uma única célula e deixar os SmartMarkers expandi‑lo em linhas se definir `ArrayAsSingle = false`.

**O SmartMarker é a única forma de lidar com JSON?**  
Não. Você também pode analisar o JSON manualmente e escrever os valores diretamente. SmartMarkers são convenientes quando você já tem um modelo com placeholders.

## Dicas Profissionais & Armadilhas Comuns

- **Dica profissional:** Ative `Workbook.Settings.EnableFormulaCalculation` se planeja adicionar fórmulas que dependam dos valores derivados do JSON.
- **Cuidado com:** espaços finais em strings JSON; o Excel os trata como parte do texto, o que pode quebrar a análise posterior.
- **Dica:** Use `worksheet.AutoFitColumns()` após inserir os dados para garantir que tudo esteja visível sem redimensionamento manual.

## Conclusão

Agora você sabe **como criar workbook**, **load json into excel**, **insert json into excel**, e até como **populate excel from json** usando o motor SmartMarker do Aspose.Cells. O exemplo completo e executável mostra cada passo—from inicializar o workbook até salvar o arquivo final—para que você possa copiar o código, ajustá‑lo e inseri‑lo em seus próprios projetos.

Pronto para o próximo desafio? Tente obter JSON de um endpoint REST ao vivo, desserializá‑lo em objetos e preencher automaticamente várias linhas. Ou experimente outros recursos do SmartMarker, como formatação condicional baseada em valores JSON. O céu é o limite quando você combina C# com Aspose.Cells.

Tem perguntas ou um caso de uso interessante que gostaria de compartilhar? Deixe um comentário abaixo, e vamos continuar a conversa. Feliz codificação!  

![ilustração de como criar workbook](workbook-json.png){alt="exemplo de como criar workbook"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}