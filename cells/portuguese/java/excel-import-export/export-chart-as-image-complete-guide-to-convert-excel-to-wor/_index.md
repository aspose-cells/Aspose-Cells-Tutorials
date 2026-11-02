---
category: general
date: 2026-06-30
description: Exporte o gráfico como imagem e aprenda como exportar o gráfico, salvar
  Excel como Word, converter Excel para Word e converter XLSX para DOCX em alguns
  passos fáceis.
draft: false
keywords:
- export chart as image
- how to export chart
- save excel as word
- convert excel to word
- convert xlsx to docx
language: pt
og_description: Exporte o gráfico como imagem e converta rapidamente o Excel para
  Word. Siga este guia para salvar o Excel como Word, exportar gráficos e converter
  XLSX para DOCX.
og_title: Exportar Gráfico como Imagem – Conversão Passo a Passo do Excel para Word
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  headline: Export Chart as Image – Complete Guide to Convert Excel to Word
  type: TechArticle
- description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  name: Export Chart as Image – Complete Guide to Convert Excel to Word
  steps:
  - name: What if my workbook has multiple charts?
    text: You don’t need to change anything—setting `setExportChartAsImage(true)`
      applies to **all** charts in the workbook. If you only want specific charts
      as images, you’ll have to export them manually using `chart.toImage()` and then
      insert them into the Word file yourself.
  - name: Can I control the image format (PNG vs JPEG)?
    text: 'Aspose.Cells uses PNG by default for chart‑as‑image exports. To switch
      to JPEG, you can adjust the `ImageOrPrintOptions` before saving:'
  - name: Does this work with older Excel files (.xls)?
    text: Absolutely. The same code works for both `.xls` and `.xlsx`. Aspose.Cells
      auto‑detects the format, so you can **save Excel as Word** regardless of the
      source version.
  - name: How does this differ from “convert Excel to Word” with native Office interop?
    text: Native interop often requires a Windows machine with Office installed, and
      charts may lose fidelity. Using Aspose.Cells is platform‑agnostic, works on
      Linux/macOS, and preserves chart quality by rasterizing them.
  type: HowTo
tags:
- Excel
- Word
- Chart
- Java
- Aspose.Cells
title: Exportar Gráfico como Imagem – Guia Completo para Converter Excel em Word
url: /pt/java/excel-import-export/export-chart-as-image-complete-guide-to-convert-excel-to-wor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar Gráfico como Imagem – Guia Completo para Converter Excel em Word

Já se perguntou como exportar um gráfico como imagem de uma pasta de trabalho do Excel e inseri‑lo diretamente em um documento Word? Você não está sozinho—desenvolvedores perguntam constantemente: “Como exportar um gráfico de XLSX e incorporá‑lo em DOCX sem perder qualidade?”  

A boa notícia é que, com algumas linhas de código Java, você pode **exportar gráfico como imagem**, então **salvar Excel como Word** em um fluxo contínuo. Neste tutorial, percorreremos todo o processo, cobrindo tudo, desde o carregamento da pasta de trabalho até a configuração das opções de salvamento que transformam seus gráficos em PNGs nítidos dentro de um arquivo DOCX.  

Também abordaremos tarefas relacionadas como **convert Excel to Word**, **save Excel as Word** e **convert XLSX to DOCX**—tudo mantendo o código claro e executável. Sem enrolação, apenas uma solução prática que você pode copiar‑colar hoje.

---

## O que você precisará

- **Java Development Kit (JDK) 8+** – o código roda em qualquer JDK moderno.  
- **Aspose.Cells for Java** library (versão 23.10 ou mais recente). Você pode obtê‑la no Maven Central ou baixar o JAR diretamente.  
- Um **arquivo Excel** (`charts.xlsx`) que contenha ao menos um gráfico que você deseja exportar.  
- Uma **IDE Java** (IntelliJ IDEA, Eclipse ou VS Code) – qualquer uma serve.  
- Familiaridade básica com Java e Maven/Gradle (opcional, mas útil).  

É isso. Sem plugins extras, sem interop COM, apenas Java puro.

---

## Etapa 1: Carregar a Pasta de Trabalho Excel e Localizar o Gráfico

A primeira coisa que precisamos fazer é abrir a pasta de trabalho que contém o gráfico. Aspose.Cells torna isso simples—basta apontá‑la para o caminho do arquivo.

```java
// Step 1: Load the Excel workbook that contains the chart
Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

// Grab the first worksheet (index 0) and its first chart (index 0)
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
```

> **Por que isso importa:** Carregar a pasta de trabalho nos dá acesso ao objeto de gráfico, que mais tarde instruiremos o Aspose a renderizar como imagem. Se a pasta de trabalho contém várias planilhas ou gráficos, você pode ajustar os índices ou percorrê‑los em loop.

---

## Etapa 2: Configurar as Opções de Salvamento DOCX para Exportar Gráficos como Imagens

Aspose.Cells fornece a classe `DocxSaveOptions` que permite controlar como a conversão se comporta. Definir `setExportChartAsImage(true)` indica à biblioteca rasterizar cada gráfico em uma imagem antes de inseri‑lo no arquivo Word.

```java
// Step 2: Create DOCX save options and enable chart‑as‑image export
DocxSaveOptions saveOptions = new DocxSaveOptions();
saveOptions.setExportChartAsImage(true); // This is the key line
```

> **Dica profissional:** Se você prefere gráficos vetoriais (EMF/WMF) pode deixar essa flag desativada, mas imagens rasterizadas geralmente são renderizadas de forma mais consistente entre versões do Word.

---

## Etapa 3: Salvar a Pasta de Trabalho como Arquivo DOCX

Agora que as opções estão definidas, simplesmente salvamos a pasta de trabalho. A biblioteca cuida da conversão de todas as planilhas, tabelas e—graças à flag que definimos—gráficos como imagens.

```java
// Step 3: Save the workbook as a DOCX file, applying the chart‑export option
workbook.save("YOUR_DIRECTORY/charts.docx", saveOptions);
```

> **O que você obtém:** Um arquivo `charts.docx` onde o gráfico original do Excel aparece como um PNG de alta resolução (ou JPEG, dependendo das suas configurações) dentro do documento Word. Abra‑o no Microsoft Word para ver o resultado.

---

## Etapa 4: Verificar a Saída (Opcional, mas Recomendado)

É sempre uma boa ideia verificar programaticamente se a conversão foi bem‑sucedida, especialmente ao automatizar processos em lote.

```java
// Optional: Verify that the DOCX file exists and is not empty
File docxFile = new File("YOUR_DIRECTORY/charts.docx");
if (docxFile.exists() && docxFile.length() > 0) {
    System.out.println("Success! DOCX created with chart as image.");
} else {
    System.err.println("Conversion failed – check the source file and options.");
}
```

Se você executar o trecho e vir a mensagem de sucesso, você efetivamente **convert XLSX to DOCX** preservando os visuais dos gráficos como imagens.

---

## Exemplo Completo em Funcionamento

Abaixo está o programa Java completo, pronto‑para‑executar, que reúne todas as etapas. Basta substituir `YOUR_DIRECTORY` pelo caminho real na sua máquina.

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportChartAsImageDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook containing the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

        // Access the first worksheet and its first chart
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        if (chart == null) {
            System.err.println("No chart found in the first worksheet.");
            return;
        }

        // Configure DOCX save options to export charts as images
        DocxSaveOptions saveOptions = new DocxSaveOptions();
        saveOptions.setExportChartAsImage(true);   // Export chart as image

        // Save as DOCX
        String outputPath = "YOUR_DIRECTORY/charts.docx";
        workbook.save(outputPath, saveOptions);

        // Verify the output file
        File outFile = new File(outputPath);
        if (outFile.exists() && outFile.length() > 0) {
            System.out.println("File saved successfully: " + outputPath);
        } else {
            System.err.println("Failed to create the DOCX file.");
        }
    }
}
```

**Saída esperada ao executar o programa:**

```
File saved successfully: YOUR_DIRECTORY/charts.docx
```

Abra `charts.docx` no Microsoft Word e você verá o gráfico renderizado como uma imagem limpa, perfeitamente posicionada onde o gráfico original do Excel estaria.

---

## Perguntas Frequentes & Casos Limite

### E se minha pasta de trabalho tiver vários gráficos?

Você não precisa mudar nada—definir `setExportChartAsImage(true)` se aplica a **todos** os gráficos na pasta de trabalho. Se você quiser apenas gráficos específicos como imagens, terá que exportá‑los manualmente usando `chart.toImage()` e então inseri‑los no arquivo Word você mesmo.

### Posso controlar o formato da imagem (PNG vs JPEG)?

Aspose.Cells usa PNG por padrão para exportações de gráfico‑como‑imagem. Para mudar para JPEG, você pode ajustar o `ImageOrPrintOptions` antes de salvar:

```java
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.getJpeg());
saveOptions.setImageOrPrintOptions(imgOptions);
```

### Isso funciona com arquivos Excel mais antigos (.xls)?

Absolutamente. O mesmo código funciona tanto para `.xls` quanto para `.xlsx`. Aspose.Cells detecta automaticamente o formato, então você pode **save Excel as Word** independentemente da versão de origem.

### Como isso difere de “convert Excel to Word” com interop nativo do Office?

Interop nativo geralmente requer uma máquina Windows com Office instalado, e os gráficos podem perder fidelidade. Usar Aspose.Cells é independente de plataforma, funciona em Linux/macOS, e preserva a qualidade dos gráficos rasterizando‑os.

---

## Dicas para Implementações Prontas para Produção

- **Processamento em lote:** Percorra um diretório de arquivos XLSX, aplicando o mesmo `DocxSaveOptions`. Envolva a conversão em um bloco try‑catch para lidar graciosamente com arquivos corrompidos.  
- **Gerenciamento de memória:** Para pastas de trabalho muito grandes, chame `workbook.dispose()` após salvar para liberar recursos nativos.  
- **Personalização:** Você também pode definir `saveOptions.setPreserveCellFormatting(true)` se precisar manter o estilo das células intacto durante a conversão.  
- **Logging:** Integre um framework de logging (SLF4J, Log4j) para capturar estatísticas de conversão—útil para trilhas de auditoria.  

---

## Conclusão

Agora você tem uma solução sólida, de ponta a ponta, que **export chart as image**, **save Excel as Word**, e **convert XLSX to DOCX** com apenas algumas instruções Java. O ponto principal é que o `DocxSaveOptions` da Aspose.Cells torna o manuseio de gráficos simples—sem extração manual de imagens, sem interop COM, e com suporte total multiplataforma.  

Sinta‑se à vontade para experimentar: tente exportar várias planilhas, ajuste as resoluções das imagens, ou combine esta abordagem com outras bibliotecas Aspose (como Aspose.Words) para documentos Word ainda mais ricos. O céu é o limite quando você sabe como exportar gráficos corretamente.  

Tem mais perguntas sobre converter arquivos Excel, incorporar imagens ou otimizar desempenho? Deixe um comentário abaixo, e feliz codificação!

---

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Converter Gráfico Excel para Imagem com Aspose.Cells .NET](/cells/english/net/charts-graphs/convert-excel-chart-image-aspose-cells-dotnet/)
- [Como Criar Gráfico Excel com Linha de Tendência e Exportar para Imagem usando Aspose.Cells para Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Converter Gráfico de Pizza Excel para Imagem Usando Aspose.Cells .NET: Um Guia Passo a Passo](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}