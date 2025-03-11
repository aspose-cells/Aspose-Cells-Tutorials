---
title: Convertendo JSON para CSV programaticamente em .NET
linktitle: Convertendo JSON para CSV programaticamente em .NET
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como converter JSON para CSV programaticamente em .NET usando Aspose.Cells. Siga nosso guia passo a passo para garantir uma transformação de dados perfeita.
weight: 15
url: /pt/net/converting-excel-files-to-other-formats/converting-json-to-csv/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertendo JSON para CSV programaticamente em .NET

## Introdução
No mundo digital de hoje, manipular dados em vários formatos se tornou comum, e JSON (JavaScript Object Notation) é um dos formatos mais amplamente usados para troca de dados. Mas o que acontece quando você precisa transformar esse JSON em um formato mais acessível para análise, como CSV (Comma Separated Values)? Este tutorial o guiará pelo processo de conversão de JSON para CSV programaticamente usando Aspose.Cells para .NET — uma API de manipulação de planilhas fácil de usar, mas poderosa. 
## Pré-requisitos
Antes de mergulharmos no código, é essencial garantir que você tenha todos os componentes necessários e um entendimento básico das ferramentas que usaremos. Vamos descrever o que você precisa:
-  Aspose.Cells para .NET: Esta é a biblioteca primária que usaremos para converter JSON para CSV. Você pode[baixe aqui](https://releases.aspose.com/cells/net/).
- Visual Studio: você precisará de um ambiente de desenvolvimento integrado (IDE) como o Visual Studio para escrever e executar o código .NET.
- .NET Framework: Certifique-se de ter o .NET Framework instalado. Aspose.Cells é compatível com .NET Core e .NET Framework.
- Conhecimento básico de C#: embora este guia explique cada parte do código, será útil se você tiver alguma familiaridade com C#.
## Pacotes de importação
Para usar Aspose.Cells no seu projeto .NET, primeiro você precisa instalar a biblioteca. Você pode fazer isso por meio do NuGet Package Manager:
1. Abra o Visual Studio.
2. Vá para Ferramentas > Gerenciador de Pacotes NuGet > Gerenciar Pacotes NuGet para Solução.
3. Procure por Aspose.Cells e instale a versão mais recente.
Após a instalação, certifique-se de incluir os seguintes namespaces no seu código:
```csharp
using Aspose.Cells.Utility;
using System;
using System.IO;
```
Agora que tudo está configurado, vamos analisar o código passo a passo para que você possa ver como é fácil converter um arquivo JSON em um CSV usando o Aspose.Cells.
## Etapa 1: leia o arquivo JSON
 A primeira coisa que precisamos fazer é ler os dados JSON de um arquivo. Vamos supor que você já tenha um arquivo JSON (vamos chamá-lo de`SampleJson.json`) armazenados em um diretório no seu sistema.
Você pode usar o`File.ReadAllText()` método em C# para ler o conteúdo do arquivo JSON em uma string.
```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
// Ler arquivo JSON
string str = File.ReadAllText(sourceDir + "SampleJson.json");
```

Esta etapa é crucial porque você precisa dos dados JSON brutos para iniciar o processo de conversão. Ao lê-los como uma string, você os prepara para serem processados pelo Aspose.Cells.
## Etapa 2: Crie uma pasta de trabalho vazia
Aspose.Cells opera principalmente em pastas de trabalho (arquivos Excel). Para começar a importar dados JSON, primeiro você precisa criar uma pasta de trabalho em branco onde esses dados serão inseridos.
```csharp
// Criar pasta de trabalho vazia
Workbook workbook = new Workbook();
```
Aqui, você está inicializando uma pasta de trabalho vazia que eventualmente conterá os dados formatados em CSV. Pense nisso como criar uma planilha em branco no Excel que logo será preenchida com seus dados JSON.
## Etapa 3: Acesse as células na pasta de trabalho
 Agora que temos uma pasta de trabalho vazia, precisamos obter acesso às suas células. O`Cells` coleção em Aspose.Cells representa todas as células em uma planilha, onde você colocará seus dados JSON.
```csharp
// Obter células
Cells cells = workbook.Worksheets[0].Cells;
```
Este trecho de código seleciona a primeira planilha (planilha no índice 0) e obtém seu`Cells` coleção. Essas células são como a grade de uma planilha onde os dados serão adicionados.
## Etapa 4: Defina JsonLayoutOptions
 Aspose.Cells fornece várias opções de personalização para como seus dados JSON serão importados. Aqui, definimos`JsonLayoutOptions` para especificar como o Aspose deve manipular matrizes, dados numéricos e títulos de objetos.
```csharp
// Definir JsonLayoutOptions
JsonLayoutOptions importOptions = new JsonLayoutOptions();
importOptions.ConvertNumericOrDate = true;
importOptions.ArrayAsTable = true;
importOptions.IgnoreArrayTitle = true;
importOptions.IgnoreObjectTitle = true;
```

- ConvertNumericOrDate: converte automaticamente valores de string que são numéricos ou de data.
- ArrayAsTable: trata matrizes em JSON como tabelas na pasta de trabalho.
- IgnoreArrayTitle e IgnoreObjectTitle: Essas opções ignoram títulos de matrizes e objetos, garantindo que apenas os dados brutos sejam importados.
## Etapa 5: Importar os dados JSON
 Depois que as opções de layout forem definidas, é hora de trazer os dados JSON. O`JsonUtility.ImportData()` O método faz o trabalho pesado aqui, inserindo os dados JSON nas células da pasta de trabalho.
```csharp
JsonUtility.ImportData(str, cells, 0, 0, importOptions);
```
Este método utiliza vários parâmetros:
- `str`A string JSON que lemos na Etapa 1.
- `cells`: A coleção de células onde os dados serão colocados.
- `0, 0`: Esses são os índices de linha e coluna que indicam onde os dados devem começar (ou seja, no canto superior esquerdo).
- `importOptions`: As opções de layout que definimos na Etapa 4.
## Etapa 6: Salve a pasta de trabalho como CSV
Agora que os dados JSON estão na pasta de trabalho, podemos facilmente salvar a pasta de trabalho como um arquivo CSV. CSV é um formato simples e leve para armazenar dados tabulares, o que o torna perfeito para análise de dados.
```csharp
// Diretório de saída
string outputDir = "Your Document Directory";
// Salvar pasta de trabalho
workbook.Save(outputDir + @"SampleJson_out.csv");
```
Nesta etapa, salvamos a pasta de trabalho como um arquivo CSV. Você especifica o caminho e o nome do arquivo (`SampleJson_out.csv`) onde o CSV será salvo.
## Etapa 7: Confirme o processo
Para garantir que tudo funcionou conforme o esperado, podemos imprimir uma mensagem de confirmação no console.
```csharp
Console.WriteLine("ConvertJsonToCsv executed successfully.");
```
Uma mensagem de sucesso simples ajuda a confirmar que o processo ocorreu sem problemas.
## Conclusão
Converter JSON para CSV usando Aspose.Cells para .NET é um processo simples, mas poderoso. Com apenas algumas linhas de código, você pode transformar dados JSON complexos em um formato CSV mais acessível. Não importa se você está lidando com matrizes, objetos ou dados numéricos, o Aspose.Cells facilita a configuração do processo de conversão para atender às suas necessidades.
## Perguntas frequentes
### O Aspose.Cells pode manipular arquivos JSON grandes?
Sim, o Aspose.Cells foi projetado para lidar com grandes conjuntos de dados de forma eficiente, tornando-o adequado para processar grandes arquivos JSON sem problemas de desempenho.
### Como posso personalizar a saída CSV?
 Você pode personalizar a saída CSV ajustando o`JsonLayoutOptions` ou manipular a formatação da pasta de trabalho antes de salvá-la como CSV.
### Existe uma maneira de excluir determinados dados do JSON durante a conversão?
Sim, ajustando o JSON ou usando lógica de código personalizada antes da importação, você pode excluir ou filtrar campos de dados específicos.
### O Aspose.Cells suporta outros formatos de arquivo além de CSV?
Absolutamente! O Aspose.Cells suporta uma ampla gama de formatos, incluindo Excel (XLS, XLSX), PDF, HTML e muitos outros.
### Como posso testar o Aspose.Cells gratuitamente?
 Você pode[baixe uma versão de teste gratuita aqui](https://releases.aspose.com/) para testar todos os recursos antes de comprar.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
