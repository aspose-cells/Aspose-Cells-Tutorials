---
"description": "Aprenda como exportar valores de string HTML de células do Excel para uma DataTable usando o Aspose.Cells para .NET em um tutorial passo a passo simples."
"linktitle": "Exportar valor de string HTML de células para DataTable no Excel"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Exportar valor de string HTML de células para DataTable no Excel"
"url": "/pt/net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Exportar valor de string HTML de células para DataTable no Excel

## Introdução

Ao trabalhar com arquivos do Excel em um ambiente .NET, você pode precisar extrair informações de células, não apenas como texto simples, mas também como strings HTML. Isso pode ser bastante útil ao lidar com dados em rich text ou quando você deseja manter a formatação. Neste guia, mostrarei como exportar o valor da string HTML de células para uma DataTable usando o Aspose.Cells para .NET. 

## Pré-requisitos

Antes de mergulhar no código, vamos garantir que você tenha tudo o que precisa. Aqui está uma lista de verificação rápida:

1. Conhecimento básico de C# e .NET: antes de começar a codificar, certifique-se de estar familiarizado com a programação em C# e com os conceitos básicos do .NET framework.
2. Aspose.Cells para .NET: Se ainda não o fez, você precisa instalar o Aspose.Cells para .NET. Você pode baixar uma versão de avaliação gratuita em [aqui](https://releases.aspose.com/).
3. Visual Studio ou IDE de sua escolha: configure seu ambiente para escrever código em C#. O Visual Studio é recomendado por sua ampla gama de recursos e facilidade de uso.
4. Arquivo Excel de exemplo: Você precisará de um arquivo Excel de exemplo (`sampleExportTableAsHtmlString.xlsx`) para trabalhar. Certifique-se de que ele esteja localizado em um diretório acessível.
5. Gerenciador de Pacotes NuGet: certifique-se de ter acesso ao Gerenciador de Pacotes NuGet no seu projeto para adicionar facilmente a biblioteca Aspose.Cells.

Com esses pré-requisitos verificados, vamos colocar a mão na massa e codificar!

## Pacotes de importação

Antes de começarmos a trabalhar com o Aspose.Cells, precisamos importar os pacotes necessários. Isso geralmente envolve adicionar o pacote NuGet do Aspose.Cells ao seu projeto. Veja como fazer isso:

### Abra o Gerenciador de Pacotes NuGet

No Visual Studio, clique com o botão direito do mouse no seu projeto no Solution Explorer e selecione Gerenciar Pacotes NuGet.

### Pesquisar por Aspose.Cells

No Gerenciador de Pacotes NuGet, digite `Aspose.Cells` na barra de pesquisa.

### Instalar o pacote

Após encontrar o Aspose.Cells, clique no botão Instalar. Isso adicionará a biblioteca ao seu projeto e permitirá que você a importe no seu código.

### Importar o namespace

Adicione a seguinte diretiva using no início do seu arquivo de código:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

Agora que configuramos tudo, vamos mergulhar no processo passo a passo de exportação de valores de string HTML de um arquivo Excel para um DataTable. 

## Etapa 1: definir o diretório de origem

Você começará definindo o diretório onde seu arquivo de exemplo do Excel está armazenado. Isso é crucial, pois informa ao seu aplicativo onde encontrar o arquivo. Aqui está o código para isso:

```csharp
string sourceDir = "Your Document Directory";
```

Certifique-se de substituir `"Your Document Directory"` com o caminho real para seu arquivo Excel.

## Etapa 2: Carregue o arquivo Excel de exemplo

O próximo passo é carregar a pasta de trabalho do Excel. Você usará o `Workbook` classe de Aspose.Cells para fazer isso. Veja como você pode carregar o arquivo:

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

Esta linha simples de código inicializa a pasta de trabalho e carrega o arquivo Excel especificado.

## Etapa 3: Acesse a primeira planilha

Depois que a pasta de trabalho for carregada, você precisará acessar a planilha específica que contém os dados de seu interesse. Geralmente, você começará com a primeira planilha:

```csharp
Worksheet ws = wb.Worksheets[0];
```

Aqui, estamos trabalhando com a primeira planilha (índice 0). Certifique-se de que seus dados estejam na planilha correta.

## Etapa 4: especificar opções de tabela de exportação

Para controlar como os dados são exportados, você precisa configurar `ExportTableOptions`Nesse caso, você quer garantir que os nomes das colunas não sejam exportados e quer que os dados das células sejam exportados como strings HTML:

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

Esta configuração permite que você mantenha a formatação avançada dos dados da sua célula ao exportar.

## Etapa 5: Exportar células para DataTable

Agora vem a parte crucial onde você realmente exporta os dados. Usando o `ExportDataTable` método, você pode extrair os dados da planilha para um `DataTable`. Veja como fazer isso:

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

Este código exporta um intervalo especificado de células (da linha 0, coluna 0 até a linha 3, coluna 3) para uma DataTable usando as opções especificadas anteriormente.

## Etapa 6: Imprimir o valor da string HTML

Por fim, vamos imprimir o valor da string HTML de uma célula específica na DataTable para ver o que conseguimos exportar. Por exemplo, se você quiser imprimir o valor da terceira linha e da segunda coluna, faça o seguinte:

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

Esta linha imprime a string HTML desejada do DataTable no console. 

## Conclusão 

pronto! Você exportou com sucesso valores de string HTML de células de um arquivo Excel para uma DataTable usando o Aspose.Cells para .NET. Esse recurso não só enriquece suas habilidades de manipulação de dados, como também amplia suas opções ao lidar com conteúdo formatado diretamente de arquivos Excel. 

## Perguntas frequentes

### Posso usar o Aspose.Cells para outros formatos de arquivo além do Excel?  
Sim, o Aspose.Cells é principalmente para Excel, mas o Aspose oferece outras bibliotecas para diferentes formatos.

### Preciso de uma licença para o Aspose.Cells?  
Sim, é necessária uma licença válida para uso em produção. Você pode obter uma licença temporária [aqui](https://purchase.aspose.com/temporary-license/).

### E se meu arquivo do Excel contiver fórmulas? Elas serão exportadas corretamente?  
Sim, o Aspose.Cells pode manipular fórmulas e, ao exportar, elas serão avaliadas com base nos valores resultantes.

### É possível alterar as opções de exportação?  
Com certeza! Você pode personalizar `ExportTableOptions` para atender às suas necessidades específicas.

### Onde posso encontrar documentação mais detalhada para Aspose.Cells?  
Você pode encontrar ampla documentação [aqui](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}