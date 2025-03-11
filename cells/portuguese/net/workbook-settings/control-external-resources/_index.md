---
title: Controle recursos externos usando a configuração da pasta de trabalho
linktitle: Controle recursos externos usando a configuração da pasta de trabalho
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como controlar recursos externos no Excel usando o Aspose.Cells para .NET com nosso tutorial passo a passo abrangente.
weight: 10
url: /pt/net/workbook-settings/control-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Controle recursos externos usando a configuração da pasta de trabalho

## Introdução
No reino da manipulação e apresentação de dados, lidar com recursos externos de forma eficiente pode ser um divisor de águas. Se você está trabalhando com arquivos do Excel e quer gerenciar recursos externos perfeitamente usando o Aspose.Cells para .NET, você chegou ao lugar certo! Neste artigo, vamos nos aprofundar no controle de recursos externos ao trabalhar com pastas de trabalho do Excel. Ao final deste guia, você será capaz de implementar uma solução personalizada para carregar imagens e dados de fontes externas sem esforço.
## Pré-requisitos
Antes de pularmos para os detalhes da codificação, há alguns pré-requisitos que você precisa ter em vigor. Certifique-se de:
1. Tenha o Visual Studio: Você precisará de um IDE para escrever e testar seus aplicativos .NET. O Visual Studio é a opção mais recomendada devido ao seu amplo suporte e facilidade de uso.
2.  Baixe Aspose.Cells para .NET: Se ainda não o fez, pegue a biblioteca Aspose.Cells do[link para download](https://releases.aspose.com/cells/net/). 
3. Noções básicas de C#: A familiaridade com os conceitos do C# e do .NET framework tornará o processo mais tranquilo para você.
4. Configure seu ambiente: certifique-se de que seu projeto faça referência à biblioteca Aspose.Cells. Você pode fazer isso por meio do NuGet Package Manager no Visual Studio.
5. Arquivos de amostra: Tenha um arquivo Excel de amostra pronto que inclua um recurso externo, como uma imagem vinculada. Este arquivo ajudará a demonstrar as funcionalidades que discutimos.
Depois de configurar tudo isso, você estará pronto para se aprofundar no controle de recursos externos com o Aspose.Cells.
## Pacotes de importação
Para começar a codificar, você precisará importar os pacotes necessários no seu arquivo C#. Aqui está o que você precisa:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
Esses namespaces fornecem acesso às funcionalidades necessárias para manipular arquivos do Excel e manipular imagens.
 Vamos dividir isso em etapas gerenciáveis para ajudar você a controlar recursos externos usando`Workbook Settings`. Vamos percorrer a criação de um provedor de fluxo personalizado, carregar um arquivo Excel e renderizar uma planilha para uma imagem. Sinta-se à vontade para acompanhar!
## Etapa 1: Definir diretórios de origem e saída
Para começar, precisamos especificar os diretórios de onde leremos nossos arquivos e onde salvaremos nossa saída. É essencial definir os caminhos corretos para evitar erros de arquivo não encontrado.
```csharp
// Diretório de origem
static string sourceDir = "Your Document Directory";
// Diretório de saída
static string outputDir = "Your Document Directory";
```
 Substituir`"Your Document Directory"` com o caminho real onde seus arquivos estão localizados.
## Etapa 2: Implementar a interface IStreamProvider
 Em seguida, criaremos uma classe personalizada que implementa o`IStreamProvider` interface. Esta classe gerenciará como recursos externos (como imagens) são acessados.
```csharp
class SP : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        // Limpe todos os recursos, se necessário
    }
    public void InitStream(StreamProviderOptions options)
    {
        // Abra o fluxo de arquivos do recurso externo
        FileStream fi = new FileStream(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.png", FileMode.OpenOrCreate, FileAccess.Read);
        options.Stream = fi;
    }
}
```
 No`InitStream` método, abrimos o arquivo que atua como nosso recurso externo e o atribuímos ao`Stream`propriedade. Isso permite que a pasta de trabalho acesse o recurso ao renderizar.
## Etapa 3: Carregue o arquivo Excel
Agora que temos nosso provedor de fluxo pronto, vamos carregar a pasta de trabalho do Excel que contém o recurso externo.
```csharp
public static void Run()
{
    // Carregar arquivo Excel de exemplo
    Workbook wb = new Workbook(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.xlsx");
    
    // Forneça sua implementação do IStreamProvider
    wb.Settings.StreamProvider = new SP();
```
 Neste snippet, carregamos nosso arquivo Excel e atribuímos nosso personalizado`StreamProvider` implementação para lidar com recursos externos.
## Etapa 4: Acesse a planilha
Após carregar a pasta de trabalho, podemos acessar facilmente a planilha desejada. Vamos pegar a primeira.
```csharp
    // Acesse a primeira planilha
    Worksheet ws = wb.Worksheets[0];
```
É simples, não é? Você pode acessar qualquer planilha especificando seu índice.
## Etapa 5: Configurar opções de imagem ou impressão
Agora definiremos como queremos que a imagem de saída fique. Configuraremos opções como garantir que haja uma página para cada planilha e especificar o tipo de imagem de saída.
```csharp
    // Especificar opções de imagem ou impressão
    ImageOrPrintOptions opts = new ImageOrPrintOptions();
    opts.OnePagePerSheet = true;
    opts.ImageType = Drawing.ImageType.Png;
```
Escolher PNG como formato de saída garante que a qualidade permaneça nítida e clara!
## Etapa 6: renderizar a planilha em uma imagem
Com tudo configurado, vamos renderizar nossa planilha escolhida para um arquivo de imagem! Esta é a parte emocionante; você verá sua planilha do Excel transformada em uma bela imagem.
```csharp
    // Crie uma renderização de folha passando os parâmetros necessários
    SheetRender sr = new SheetRender(ws, opts);
    // Converta toda a sua planilha em imagem png
    sr.ToImage(0, outputDir + "outputControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
    
    Console.WriteLine("ControlExternalResourcesUsingWorkbookSetting_StreamProvider executed successfully.");
}
```
 O`ToImage` A função faz todo o trabalho pesado, convertendo a planilha em uma imagem. Quando essa etapa for concluída, você encontrará a imagem salva no seu diretório de saída.
## Conclusão
E aí está! Agora você possui o know-how para controlar recursos externos ao trabalhar com arquivos do Excel usando Aspose.Cells no .NET. Isso não apenas aprimora os recursos do seu aplicativo, mas também torna o manuseio de conjuntos de dados e apresentações uma caminhada na praia. Seguindo as etapas fornecidas, você pode facilmente replicar e adaptar essa funcionalidade para atender às necessidades específicas do seu projeto.
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca poderosa projetada para desenvolvedores C# e .NET criarem, manipularem e gerenciarem arquivos do Excel sem precisar instalar o Microsoft Excel.
### Como posso baixar o Aspose.Cells para .NET?
 Você pode baixá-lo do[Site Aspose](https://releases.aspose.com/cells/net/).
### Existe um teste gratuito disponível?
 Sim! Você pode acessar uma avaliação gratuita do Aspose.Cells em seu[página de lançamento](https://releases.aspose.com/).
### Que tipos de arquivos o Aspose.Cells suporta?
O Aspose.Cells suporta vários formatos do Excel, incluindo XLS, XLSX, CSV e muito mais.
### Onde posso encontrar suporte para o Aspose.Cells?
 Você pode visitar o fórum de suporte do Aspose em[Fórum Aspose](https://forum.aspose.com/c/cells/9) para obter assistência.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
