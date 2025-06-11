---
"description": "Aprenda a ajustar o nível de compactação de pastas de trabalho do Excel usando o Aspose.Cells para .NET com este guia passo a passo. Otimize seu gerenciamento de arquivos."
"linktitle": "Ajustar o nível de compressão na pasta de trabalho"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Ajustar o nível de compressão na pasta de trabalho"
"url": "/pt/net/workbook-operations/adjust-compression-level/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajustar o nível de compressão na pasta de trabalho

## Introdução
Quando se trata de gerenciar arquivos grandes do Excel, a compactação é um divisor de águas. Ela não só economiza espaço de armazenamento, como também torna as transferências de arquivos mais rápidas e eficientes. Se você estiver trabalhando com o Aspose.Cells para .NET, poderá ajustar facilmente o nível de compactação das suas pastas de trabalho. Neste guia, mostraremos o processo passo a passo, garantindo que você entenda cada parte do código e como ele funciona.
## Pré-requisitos
Antes de mergulhar no código, há alguns pré-requisitos que você precisa ter em mente:
1. Conhecimento básico de C#: a familiaridade com a programação em C# ajudará você a entender melhor os trechos de código.
2. Biblioteca Aspose.Cells: Você precisa ter a biblioteca Aspose.Cells instalada. Você pode baixá-la em [aqui](https://releases.aspose.com/cells/net/).
3. Visual Studio: Um ambiente de desenvolvimento como o Visual Studio será necessário para executar o código.
4. .NET Framework: certifique-se de que seu projeto esteja configurado com uma versão compatível do .NET Framework.
## Pacotes de importação
Para começar, você precisa importar os pacotes necessários para o seu projeto C#. Veja como fazer isso:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
Esses pacotes são essenciais para trabalhar com arquivos Excel usando a biblioteca Aspose.Cells. `Aspose.Cells` namespace contém todas as classes que você precisa para manipular arquivos do Excel, enquanto `Aspose.Cells.Xlsb` fornece opções para salvar arquivos no formato XLSB.
Agora, vamos dividir o processo de ajuste do nível de compactação em uma pasta de trabalho em etapas gerenciáveis.
## Etapa 1: definir diretórios de origem e saída
Primeiro, você precisa especificar onde seus arquivos de origem estão localizados e onde deseja salvar os arquivos de saída. Isso é crucial para garantir que seu programa saiba onde encontrar os arquivos com os quais precisa trabalhar.
```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
Substituir `"Your Document Directory"` com o caminho real para seus diretórios. Isso ajudará o programa a localizar os arquivos que você deseja compactar.
## Etapa 2: Carregar a pasta de trabalho
Em seguida, você carregará a pasta de trabalho que deseja compactar. É aqui que a mágica começa!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
Nesta linha, criamos uma nova instância do `Workbook` class e carregue um arquivo Excel existente. Certifique-se de que o nome do arquivo corresponda ao que você tem no diretório de origem.
## Etapa 3: Configurar opções de salvamento
Agora é hora de configurar as opções de salvamento. Definiremos o tipo de compactação do arquivo de saída. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
O `XlsbSaveOptions` A classe permite que você especifique várias opções ao salvar sua pasta de trabalho no formato XLSB, incluindo níveis de compactação.
## Etapa 4: Medir o tempo de compressão para o nível 1
Vamos começar com o primeiro nível de compactação. Mediremos quanto tempo leva para salvar a pasta de trabalho com esse nível de compactação.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
Aqui, definimos o tipo de compactação como Nível 1, salvamos a pasta de trabalho e medimos o tempo decorrido. Isso nos dá uma ideia de quanto tempo o processo leva.
## Etapa 5: Medir o tempo de compressão para o nível 6
Em seguida, vamos ver o desempenho da compressão de Nível 6.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
Esta etapa é semelhante à anterior, mas alteramos o nível de compactação para o Nível 6. Você notará que o tempo necessário pode variar de acordo com a complexidade da pasta de trabalho.
## Etapa 6: Medir o tempo de compressão para o nível 9
Por fim, vamos verificar o desempenho com o maior nível de compressão.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
Nesta etapa, definimos o nível de compactação como Nível 9. É aqui que você normalmente verá a redução mais significativa no tamanho do arquivo, mas pode levar mais tempo para processar.
## Etapa 7: Resultado final
Depois de executar todos os níveis de compactação, você pode exibir uma mensagem indicando que o processo foi concluído com sucesso.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
Esta linha simples de código confirma que seu programa terminou de ser executado sem problemas.
## Conclusão
Ajustar o nível de compactação das suas pastas de trabalho usando o Aspose.Cells para .NET é um processo simples que pode gerar benefícios significativos em termos de tamanho e desempenho do arquivo. Seguindo os passos descritos neste guia, você pode implementar facilmente a compactação em seus aplicativos e melhorar a eficiência do gerenciamento de arquivos do Excel.
## Perguntas frequentes
### O que é Aspose.Cells?  
Aspose.Cells é uma biblioteca poderosa para .NET que permite aos desenvolvedores criar, manipular e converter arquivos do Excel sem a necessidade do Microsoft Excel.
### Como instalo o Aspose.Cells?  
Você pode baixar e instalar o Aspose.Cells do [Site Aspose](https://releases.aspose.com/cells/net/).
### Quais níveis de compressão estão disponíveis?  
O Aspose.Cells suporta vários níveis de compactação que variam do Nível 1 (menor compactação) ao Nível 9 (maior compactação).
### Posso testar o Aspose.Cells gratuitamente?  
Sim! Você pode obter uma avaliação gratuita do Aspose.Cells [aqui](https://releases.aspose.com/).
### Onde posso encontrar suporte para o Aspose.Cells?  
Para qualquer dúvida ou suporte, você pode visitar o fórum de suporte do Aspose [aqui](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}