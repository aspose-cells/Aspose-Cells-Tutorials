---
category: general
date: 2026-03-25
description: Como exportar gráficos do Word usando Aspose.Words C# – aprenda a incluir
  gráficos e exportar gráficos do Word em minutos.
draft: false
keywords:
- how to export charts
- how to include charts
- export charts from word
- Aspose.Words export
- C# document automation
language: pt
og_description: Como exportar gráficos do Word usando Aspose.Words C#. Este guia mostra
  como incluir gráficos e exportar gráficos do Word rapidamente.
og_title: Como Exportar Gráficos do Word – Guia Completo de C#
tags:
- C#
- Aspose.Words
- Word Automation
- Charts
title: Como Exportar Gráficos do Word – Guia Completo de C#
url: /pt/net/chart-rendering-and-conversion/how-to-export-charts-from-word-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Exportar Gráficos do Word – Guia Completo em C#

Já precisou **de como exportar gráficos** de um documento Word mas não sabia por onde começar? Você não está sozinho; muitos desenvolvedores encontram esse obstáculo ao automatizar relatórios. Neste tutorial vamos percorrer uma solução prática, de ponta a ponta, que não só mostra **como exportar gráficos**, mas também explica **como incluir gráficos** no arquivo exportado. Ao final, você será capaz de exportar gráficos do Word com apenas algumas linhas de C#.

Usaremos a popular biblioteca **Aspose.Words for .NET**, pois ela lida com objetos de gráfico nativamente e funciona com .docx, .doc e até formatos mais antigos. Nada de mexer com Office Interop, sem pesadelos COM. As etapas abaixo assumem que você tem um projeto C# básico e o pacote NuGet Aspose.Words instalado. Se você é novo na biblioteca, não se preocupe—cobriremos os pré‑requisitos rapidamente.

## Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.7+)
- Visual Studio 2022 ou qualquer IDE de sua preferência
- Aspose.Words for .NET (instale via `dotnet add package Aspose.Words`)

> **Dica de especialista:** Mantenha sua versão do Aspose.Words atualizada; a versão mais recente (a partir de março 2026) adiciona melhor manipulação de gráficos e melhorias de desempenho.

## Etapa 1: Carregar o Documento Word de Origem

A primeira coisa que você precisa fazer é abrir o arquivo `.docx` que contém os gráficos que deseja extrair. Aspose.Words torna isso uma única linha.

```csharp
using Aspose.Words;

// Load the source document (replace with your actual path)
Document document = new Document(@"C:\Docs\input.docx");
```

*Por que isso importa:* Carregar o documento cria uma representação em memória de cada elemento—parágrafos, tabelas e, crucialmente, os objetos de gráfico. Sem essa etapa você não pode acessar ou manipular os gráficos.

## Etapa 2: Configurar Opções de Salvamento para Preservar Gráficos

Por padrão, um simples `document.Save("output.docx")` mantém tudo, mas se você alguma vez ativar `ExportImages` ou flags semelhantes pode acabar perdendo os gráficos incorporados. Para ser explícito—e responder à parte “**como incluir gráficos**” da pergunta—definimos `DocxSaveOptions` com `ExportCharts = true`.

```csharp
// Create save options that ensure charts are included
DocxSaveOptions saveOptions = new DocxSaveOptions
{
    ExportCharts = true          // Guarantees charts are part of the saved file
};
```

*Explicação:* `ExportCharts` indica ao motor que ele deve serializar cada gráfico como uma parte nativa de Office Open XML. Isso é essencial quando você abrir o arquivo posteriormente no Word ou em outros editores; os gráficos aparecerão exatamente como estavam no documento original.

## Etapa 3: Salvar o Documento com as Opções Configuradas

Agora gravamos o documento de volta ao disco, usando as opções que acabamos de definir. O arquivo de saída conterá todo o conteúdo original **e** os gráficos.

```csharp
// Save the document with charts preserved
document.Save(@"C:\Docs\charts.docx", saveOptions);
```

Neste ponto você tem um novo arquivo Word (`charts.docx`) que é uma cópia fiel do original, completo com todos os gráficos. Abra‑o no Microsoft Word para verificar—seus gráficos devem estar totalmente funcionais, editáveis e com a mesma aparência de antes.

## Exemplo Completo Funcionando

Abaixo está o programa completo, pronto para ser executado. Copie‑o para um aplicativo console, ajuste os caminhos e pressione **F5**.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Saving;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document containing charts
            string inputPath = @"C:\Docs\input.docx";
            Document document = new Document(inputPath);
            Console.WriteLine($"Loaded document: {inputPath}");

            // 2️⃣ Set save options to explicitly include charts
            DocxSaveOptions saveOptions = new DocxSaveOptions
            {
                ExportCharts = true   // This ensures charts are not stripped out
            };
            Console.WriteLine("Configured DocxSaveOptions to export charts.");

            // 3️⃣ Save the new file
            string outputPath = @"C:\Docs\charts.docx";
            document.Save(outputPath, saveOptions);
            Console.WriteLine($"Document saved with charts at: {outputPath}");

            // Verification hint
            Console.WriteLine("Open the output file in Word to confirm charts are present.");
        }
    }
}
```

**Resultado esperado:** Ao abrir `charts.docx` no Microsoft Word, cada gráfico de `input.docx` aparece inalterado. Nenhuma imagem faltando, nenhuma referência quebrada.

## Tratamento de Casos de Borda Comuns

| Situação | O que observar | Correção recomendada |
|-----------|-------------------|-----------------|
| **Documento contém planilhas Excel incorporadas** | Os gráficos podem estar vinculados a dados externos do Excel. | Use `DocxSaveOptions.ExportEmbeddedExcelData = true` (disponível em versões mais recentes) para manter os dados intactos. |
| **Documentos grandes (> 100 MB)** | O uso de memória aumenta durante o carregamento. | Defina `LoadOptions.LoadFormat = LoadFormat.Docx` e considere streaming com `DocumentBuilder` para processamento incremental. |
| **Você precisa apenas de gráficos específicos** | Exportar o arquivo inteiro é excessivo. | Percorra `document.GetChildNodes(NodeType.Shape, true)` e filtre por `Shape.IsChart`. Em seguida, clone essas shapes para um novo `Document` antes de salvar. |
| **Formato de destino é PDF** | Os gráficos podem ser renderizados de forma diferente. | Use `PdfSaveOptions` com `ExportCharts = true` (a flag funciona para PDF também). |

Essas variações respondem à consulta “**exportar gráficos do Word**” em diferentes contextos, garantindo que você esteja coberto tanto ao salvar como DOCX quanto ao converter para outro formato.

## Perguntas Frequentes

**P: Isso funciona com arquivos `.doc` mais antigos?**  
R: Sim. Aspose.Words converte automaticamente o formato binário legado para a estrutura moderna Open XML em memória, portanto `ExportCharts` ainda se aplica.

**P: E se eu quiser exportar apenas as imagens dos gráficos, não o documento inteiro?**  
R: Você pode extrair cada gráfico como imagem usando `ChartRenderer`. Exemplo: `chartRenderer.Save("chart.png", ImageFormat.Png);` Isso atende a uma necessidade mais restrita de “como exportar gráficos”.

**P: Existe alguma preocupação de licenciamento?**  
R: Aspose.Words é uma biblioteca comercial. Para avaliação você pode usar uma licença temporária; para produção será necessário adquirir uma licença adequada para evitar a marca d'água de avaliação.

## Visão Geral Visual

Abaixo está um esquema rápido do fluxo—note a palavra‑chave principal no texto alternativo.

![How to export charts example – diagram showing load → configure → save steps](https://example.com/images/export-charts-diagram.png)

*Texto alternativo:* **diagrama de como exportar gráficos ilustrando as etapas de carregamento, configuração e salvamento**

## Conclusão

Acabamos de cobrir **como exportar gráficos** de um documento Word usando Aspose.Words, demonstrado **como incluir gráficos** ao salvar, e abordado vários cenários para **exportar gráficos do Word** em diferentes formatos. O padrão de três etapas—carregar, configurar, salvar—é simples, confiável e escalável, desde pequenos relatórios até documentos corporativos massivos.

Qual o próximo passo? Tente extrair apenas gráficos selecionados, convertê‑los para PNG para uso na web, ou automatizar um processo em lote que percorra uma pasta de arquivos Word e exporte seus gráficos de uma só vez. Cada uma dessas extensões se baseia na técnica central que você acabou de dominar.

Sinta‑se à vontade para deixar um comentário se encontrar algum obstáculo, ou compartilhar como adaptou esse padrão nos seus próprios projetos. Boa codificação, e que seus gráficos estejam sempre renderizados perfeitamente!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}