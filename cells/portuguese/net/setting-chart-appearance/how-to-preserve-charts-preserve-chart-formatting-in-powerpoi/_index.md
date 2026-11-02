---
category: general
date: 2026-07-03
description: como preservar gráficos mantendo a formatação dos gráficos usando Aspose.Slides
  em C#. Siga este guia passo a passo.
draft: false
keywords:
- how to preserve charts
- preserve chart formatting
language: pt
og_description: Como preservar gráficos e a formatação de gráficos com Aspose.Slides
  em C#. Guia completo com código.
og_title: como preservar gráficos – preservar a formatação de gráficos no PowerPoint
  (C#)
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  headline: how to preserve charts – preserve chart formatting in PowerPoint C#
  type: TechArticle
- description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  name: how to preserve charts – preserve chart formatting in PowerPoint C#
  steps:
  - name: Open `EditableCharts.pptx` in PowerPoint.
    text: Open `EditableCharts.pptx` in PowerPoint.
  - name: Click any chart → “Edit Data”.
    text: Click any chart → “Edit Data”.
  - name: The Excel‑like data sheet should appear, letting you modify series values.
    text: The Excel‑like data sheet should appear, letting you modify series values.
  type: HowTo
- questions:
  - answer: Directly no—`ExportEditableObjects` only applies to the PPTX format. Convert
      first, then export.
    question: Does this work with PowerPoint 2003 (PPT) files?
  - answer: Absolutely. The same `ExportEditableObjects` flag keeps SmartArt, tables,
      and diagrams editable.
    question: Can I preserve other objects like SmartArt?
  - answer: 'The slide size is stored in the presentation metadata and isn’t affected
      by these options. No extra code needed. --- ## Next steps – keep the momentum
      Now that you’ve nailed **how to preserve charts**, try exploring: - **preserve
      chart formatting** for specific chart types (e.g., stacked bar vs. rad'
    question: What if I need to keep the original slide size?
  type: FAQPage
tags:
- Aspose.Slides
- C#
- PowerPoint
- chart automation
title: Como preservar gráficos – preservar a formatação de gráficos no PowerPoint
  C#
url: /pt/net/setting-chart-appearance/how-to-preserve-charts-preserve-chart-formatting-in-powerpoi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como preservar gráficos – preservar formatação de gráficos no PowerPoint C#

Já se perguntou **como preservar gráficos** quando você precisa exportar ou manipular um arquivo PowerPoint programaticamente? Talvez você tenha tentado um salvamento rápido e o gráfico tenha se transformado em uma imagem estática, quebrando a editabilidade que você esperava.  

Neste tutorial, mostraremos **como preservar gráficos** **e** manter sua **preservação da formatação de gráficos** intacta usando Aspose.Slides for .NET. Ao final, você terá um trecho de código C# pronto‑para‑executar que produz um PPTX onde cada gráfico permanece um objeto OOXML editável — nada de imagens achatadas.

## O que você aprenderá

- Os passos exatos para carregar uma apresentação, configurar opções de exportação e salvar mantendo **a formatação de gráficos preservada**.  
- Por que a flag `ExportEditableObjects` é importante e como ela impede que os gráficos sejam rasterizados.  
- Armadilhas comuns (por exemplo, formatos PPT antigos, fontes ausentes) e correções rápidas.  

Nenhuma experiência prévia com Aspose é necessária; apenas uma configuração básica de C# e um arquivo PowerPoint que você deseja manter amigável a gráficos.

## Pré-requisitos

- .NET 6.0 ou superior (o código também funciona com .NET Framework 4.7+).  
- Pacote NuGet Aspose.Slides for .NET (`Install-Package Aspose.Slides.NET`).  
- Um exemplo `input.pptx` que contenha ao menos um gráfico.  
- Visual Studio, Rider ou qualquer editor de sua preferência.

---

## Etapa 1: Instalar Aspose.Slides e criar um novo projeto console

Para começar, crie um novo aplicativo console e inclua a biblioteca:

```bash
dotnet new console -n PreserveChartsDemo
cd PreserveChartsDemo
dotnet add package Aspose.Slides.NET
```

> **Dica profissional:** Se você estiver atrás de um proxy corporativo, adicione a flag `--no-restore` e restaure depois com as configurações do seu proxy.

## Etapa 2: Carregar a apresentação de origem – o primeiro lugar para aplicar **como preservar gráficos**

Abra seu arquivo PPTX usando a classe `Presentation`. É aqui que a jornada para **como preservar gráficos** realmente começa.

```csharp
using Aspose.Slides;
using Aspose.Slides.Export;

namespace PreserveChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Load the source presentation
            // Replace the path with the location of your PPTX that contains charts.
            Presentation pres = new Presentation(@"YOUR_DIRECTORY\input.pptx");
```

Observe que ainda não manipulamos nenhum objeto de gráfico — isso é intencional. Carregar o arquivo como está garante que mantenhamos a estrutura XML original, o que é crucial para **preservar a formatação de gráficos** posteriormente.

## Etapa 3: Configurar opções de exportação – o coração de **como preservar gráficos**

Aspose.Slides oferece a classe `PresentationExportOptions`. Definir `ExportEditableObjects` como `true` indica ao mecanismo que mantenha gráficos, tabelas e SmartArt como partes OOXML nativas em vez de achatá‑los.

```csharp
            // Step 3: Configure export options to keep objects editable
            PresentationExportOptions exportOptions = new PresentationExportOptions
            {
                // This flag is the key to how to preserve charts.
                ExportEditableObjects = true
            };
```

Por que isso funciona? Quando `ExportEditableObjects` está `false` (padrão), a biblioteca rasteriza objetos complexos para compatibilidade, o que destrói **a preservação da formatação de gráficos**. Ativá‑la preserva o XML original do gráfico, permitindo que os usuários finais abram o PPTX e ainda editem os dados do gráfico.

## Etapa 4: Salvar a apresentação usando as opções configuradas

Agora gravamos o arquivo de saída. A mesma sobrecarga `Save` que aceita `SaveFormat` e `exportOptions` garante que o gráfico permaneça editável.

```csharp
            // Step 4: Save the presentation with the configured options
            pres.Save(@"YOUR_DIRECTORY\EditableCharts.pptx", SaveFormat.Pptx, exportOptions);

            // Optional: Inform the user
            Console.WriteLine("Presentation saved with editable charts at: YOUR_DIRECTORY\\EditableCharts.pptx");
        }
    }
}
```

Executar este programa produz `EditableCharts.pptx`. Abra‑o no PowerPoint, clique com o botão direito em um gráfico e você verá a opção usual “Edit Data” — prova de que dominamos com sucesso **como preservar gráficos** e **preservar a formatação de gráficos**.

## Etapa 5: Verificar o resultado e solucionar problemas comuns

### Verificar

1. Abra `EditableCharts.pptx` no PowerPoint.  
2. Clique em qualquer gráfico → “Edit Data”.  
3. A planilha de dados semelhante ao Excel deve aparecer, permitindo que você modifique os valores das séries.

Se você vir apenas uma imagem estática, verifique novamente que:

- Você está usando uma versão recente do Aspose.Slides (versões antigas tinham bugs com `ExportEditableObjects`).  
- O PPTX de origem realmente contém objetos de gráfico (não imagens de gráficos).  
- Nenhum tema personalizado ou substituição de fonte está fazendo com que o gráfico seja renderizado como imagem.

### Casos Limite

- **Arquivos PPT (binários) antigos:** Converta‑os para PPTX primeiro (`pres.Save("temp.pptx", SaveFormat.Pptx)`) antes de aplicar as opções de exportação.  
- **Apresentações grandes:** O uso de memória pode disparar; considere o padrão `Dispose` de `Presentation` ou APIs de streaming para arquivos massivos.  
- **Fontes incorporadas:** Se o ambiente de destino não possuir as fontes originais, o PowerPoint pode fazer fallback e renderizar o gráfico como imagem. Incorpore as fontes no arquivo de origem ou envie‑as com sua aplicação.

---

## Perguntas Frequentes (FAQ)

**Q: Isso funciona com arquivos PowerPoint 2003 (PPT)?**  
A: Não diretamente — `ExportEditableObjects` só se aplica ao formato PPTX. Converta primeiro, depois exporte.

**Q: Posso preservar outros objetos como SmartArt?**  
A: Absolutamente. A mesma flag `ExportEditableObjects` mantém SmartArt, tabelas e diagramas editáveis.

**Q: E se eu precisar manter o tamanho original do slide?**  
A: O tamanho do slide está armazenado nos metadados da apresentação e não é afetado por essas opções. Nenhum código extra é necessário.

## Próximos passos – mantenha o ritmo

Agora que você dominou **como preservar gráficos**, experimente explorar:

- **preservar a formatação de gráficos** para tipos específicos de gráfico (por exemplo, barras empilhadas vs. radar).  
- Usar a API `Chart` para modificar programaticamente os dados antes de salvar.  
- Exportar para outros formatos (PDF, HTML) mantendo os gráficos editáveis na PPTX de origem.  

Cada um desses se baseia no mesmo princípio: manter o OOXML subjacente intacto.

## Conclusão

Caminhamos por **como preservar gráficos** em um arquivo PowerPoint usando Aspose.Slides for .NET, e demonstramos as etapas exatas de **preservar a formatação de gráficos** necessárias para manter esses gráficos totalmente editáveis. O trecho de código completo acima está pronto para ser inserido em qualquer projeto C#, e as explicações cobrem o *porquê* de cada linha — então você não apenas copiará e colará, mas entenderá.

Experimente, ajuste as opções de exportação, e em breve você estará automatizando atualizações de apresentações sem jamais perder a capacidade de ajustar os dados dos gráficos. Feliz codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Exportar Gráficos do Excel para PDF Usando Aspose.Cells para .NET&#58; Um Guia Passo a Passo](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Como Converter Gráficos do Excel para SVG Usando Aspose.Cells para .NET (Guia Passo a Passo)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Como Criar Gráficos no Excel Usando Aspose.Cells para .NET&#58; Guia do Desenvolvedor](/cells/english/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}