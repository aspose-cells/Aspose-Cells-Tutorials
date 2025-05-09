---
"description": "Aprenda a ajustar os níveis de compactação de arquivos do Excel usando o Aspose.Cells para .NET. Otimize o tamanho dos seus arquivos com eficiência com este guia passo a passo."
"linktitle": "Ajustar nível de compressão"
"second_title": "Referência da API Aspose.Cells para .NET"
"title": "Ajustar nível de compressão"
"url": "/pt/net/excel-workbook/adjust-compression-level/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajustar nível de compressão

## Introdução

Ao lidar com arquivos grandes do Excel, o armazenamento eficiente é fundamental. Seja você um desenvolvedor que busca otimizar o tamanho dos arquivos ou um analista de dados que deseja acelerar as transferências de arquivos, entender como ajustar os níveis de compactação no Aspose.Cells para .NET pode ser decisivo. Neste guia, mostraremos as etapas para ajustar os níveis de compactação ao salvar arquivos do Excel, garantindo que você mantenha o desempenho sem comprometer a qualidade.

## Pré-requisitos

Antes de mergulhar nos detalhes dos níveis de compressão, vamos garantir que você tenha tudo o que precisa para começar:

1. Conhecimento básico de C#: Um conhecimento básico de programação em C# é essencial. Se você se sente confortável com variáveis, loops e operações básicas de arquivo, está pronto para começar!
2. Biblioteca Aspose.Cells para .NET: Certifique-se de ter a biblioteca Aspose.Cells instalada. Você pode baixá-la do site [site](https://releases.aspose.com/cells/net/). Se você está apenas começando, considere obter uma avaliação gratuita [aqui](https://releases.aspose.com/).
3. Ambiente de desenvolvimento: configure seu ambiente de desenvolvimento, de preferência o Visual Studio, para escrever e executar seu código C#. 
4. Exemplo de arquivo do Excel: Tenha um arquivo grande do Excel pronto para teste. Você pode criar um ou usar qualquer arquivo existente, mas certifique-se de que ele seja grande o suficiente para ver os efeitos da compactação.

Com esses pré-requisitos em vigor, vamos começar!

## Pacotes de importação

Antes de podermos manipular arquivos do Excel, precisamos importar os namespaces necessários. Esta é uma etapa crucial que nos permite acessar as classes e métodos fornecidos por Aspose.Cells.

### Importe o namespace Aspose.Cells

```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```

Este trecho de código importa o `Aspose.Cells` namespace, que contém todas as classes necessárias para trabalhar com arquivos do Excel. O `Aspose.Cells.Xlsb` namespace é específico para manipular formatos de arquivo XLSB.

Agora que configuramos tudo, vamos dividir o processo de ajuste dos níveis de compressão em etapas gerenciáveis. Salvaremos uma pasta de trabalho com diferentes níveis de compressão e mediremos o tempo gasto em cada operação. 

## Etapa 1: Configure seus diretórios

Antes de mais nada, precisamos definir onde nossos arquivos serão armazenados. Isso envolve especificar o diretório de origem para o arquivo de entrada e o diretório de saída para os arquivos compactados.

```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```

## Etapa 2: Carregar a pasta de trabalho

Em seguida, carregaremos a pasta de trabalho do Excel que queremos compactar. É aqui que você apontará para o seu arquivo grande do Excel.

```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```

Esta linha inicializa uma nova `Workbook` objeto com o arquivo especificado. Certifique-se de que o caminho do arquivo esteja correto; caso contrário, você encontrará erros.

## Etapa 3: Criar opções de salvamento para XLSB

Agora, criaremos uma instância de `XlsbSaveOptions`, que nos permite especificar como queremos salvar nossa pasta de trabalho, incluindo o nível de compactação.

```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```

Esta linha prepara as opções que usaremos para salvar nossa pasta de trabalho no formato XLSB.

## Etapa 4: definir e medir os níveis de compressão

Agora vem a parte divertida! Salvaremos a pasta de trabalho usando diferentes níveis de compactação e mediremos o tempo gasto em cada operação. 

### Compressão de nível 1

Vamos começar com o nível de compressão mais baixo:

```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```

Neste snippet, definimos o tipo de compactação como Nível 1, salvamos a pasta de trabalho e registramos o tempo gasto. 

### Compressão de nível 6

Em seguida, tentaremos um nível de compressão médio:

```csharp
options.CompressionType = OoxmlCompressionType.Level6;
watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```

Desta vez, definimos o tipo de compressão para Nível 6 e repetimos a operação de salvamento.

### Compressão de nível 9

Por fim, vamos salvar usando o nível de compressão mais alto:

```csharp
options.CompressionType = OoxmlCompressionType.Level9;
watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```

Nesta etapa, definimos o tipo de compactação como Nível 9, que deve resultar no menor tamanho de arquivo, mas pode levar mais tempo para salvar.

## Etapa 5: Resultado final

Depois de executar todos os passos acima, você verá os tempos decorridos para cada nível de compressão impressos no console. 

```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```

Esta linha confirma que todo o processo foi concluído sem problemas.

## Conclusão

Ajustar os níveis de compactação ao salvar arquivos do Excel com o Aspose.Cells para .NET é uma técnica simples, porém poderosa. Seguindo os passos descritos neste guia, você poderá manipular facilmente o tamanho dos arquivos, tornando-os mais fáceis de armazenar e transferir. Seja para acessar dados rapidamente ou otimizar o desempenho do seu aplicativo, dominar essas técnicas certamente aprimorará suas habilidades como desenvolvedor.

## Perguntas frequentes

### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca .NET que permite aos desenvolvedores criar, manipular e converter arquivos do Excel programaticamente.

### Como faço para baixar o Aspose.Cells?
Você pode baixar a biblioteca Aspose.Cells do [site](https://releases.aspose.com/cells/net/).

### Posso usar o Aspose.Cells gratuitamente?
Sim, o Aspose oferece uma versão de teste gratuita que você pode acessar [aqui](https://releases.aspose.com/).

### Quais são os diferentes níveis de compressão disponíveis?
Aspose.Cells suporta vários níveis de compactação, que vão do Nível 1 (menor compactação) ao Nível 9 (máxima compactação).

### Onde posso encontrar suporte para o Aspose.Cells?
Você pode obter suporte e fazer perguntas sobre [Fórum Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}