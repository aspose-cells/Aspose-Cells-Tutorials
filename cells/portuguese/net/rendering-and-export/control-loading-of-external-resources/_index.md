---
"description": "Descubra como controlar recursos externos na conversão do Excel para PDF usando o Aspose.Cells para .NET com nosso guia fácil de seguir."
"linktitle": "Controle de recursos externos do Excel para PDF no Aspose.Cells"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Controle de recursos externos do Excel para PDF no Aspose.Cells"
"url": "/pt/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Controle de recursos externos do Excel para PDF no Aspose.Cells

## Introdução
Na era digital atual, converter planilhas do Excel em documentos PDF é uma tarefa comum. Seja para preparar relatórios, dados financeiros ou materiais de apresentação, você precisa garantir que seus PDFs tenham exatamente a aparência desejada. O Aspose.Cells para .NET é uma biblioteca robusta que permite controlar esse processo de conversão nos mínimos detalhes, especialmente ao lidar com recursos externos, como imagens que acompanham seus arquivos do Excel. Neste guia, vamos nos aprofundar em como controlar recursos externos durante o processo de conversão do Excel para PDF usando o Aspose.Cells. Então, pegue sua bebida favorita e vamos começar!
## Pré-requisitos
Antes de entrarmos em detalhes, vamos garantir que você tenha tudo o que precisa para começar. Aqui está uma lista de verificação rápida:
1. Visual Studio ou qualquer IDE compatível com .NET: você precisará de um ambiente para escrever e testar seu código.
2. Aspose.Cells para .NET: Se você ainda não o instalou, vá para o [Downloads do Aspose](https://releases.aspose.com/cells/net/) página e baixe a versão mais recente.
3. Conhecimento básico de C#: Familiaridade com a linguagem de programação C# será útil. Se tiver dúvidas sobre algum conceito, não hesite em consultá-lo.
4. Um arquivo Excel de exemplo: prepare um arquivo Excel com os recursos externos que você deseja converter. Você pode usar o arquivo de exemplo fornecido "samplePdfSaveOptions_StreamProvider.xlsx".
5. Um arquivo de imagem para teste: será usado como um recurso externo durante a conversão. O arquivo de imagem "newPdfSaveOptions_StreamProvider.png" é um bom espaço reservado.
## Pacotes de importação
Para começar, você precisará importar os namespaces necessários da biblioteca Aspose.Cells. Isso é crucial para acessar suas funcionalidades. Certifique-se de adicionar as seguintes diretivas "using" no início do seu arquivo:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Esses pacotes fornecerão todas as classes e métodos essenciais que você precisa para executar suas tarefas.
## Etapa 1: Crie sua classe de provedor de fluxo
A primeira tarefa é criar uma classe de provedor de fluxo que implemente o `IStreamProvider` interface. Esta classe permitirá que você controle como os recursos externos são carregados.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // Leia a nova imagem em um fluxo de memória e atribua-a à propriedade Stream
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
Nesta aula:
- CloseStream: Este método será chamado quando o fluxo for fechado. Por enquanto, estamos apenas escrevendo uma mensagem de depuração para rastreamento.
- InitStream: É aqui que a mágica começa. Aqui, você lerá sua imagem externa como uma matriz de bytes, a converterá em um fluxo de memória e a atribuirá ao `options.Stream` propriedade.
## Etapa 2: Configurar diretórios de origem e saída
Agora que seu provedor de transmissão está pronto, é hora de estabelecer onde seu arquivo Excel está localizado e onde você deseja salvar seu PDF.
```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
// Diretório de saída
string outputDir = "Your Document Directory";
```
Simplesmente substitua `"Your Document Directory"` com o caminho real no seu computador onde seus arquivos estão armazenados. Manter seus arquivos organizados é fundamental!
## Etapa 3: carregue seu arquivo Excel
Em seguida, você carregará o arquivo Excel a partir do qual deseja criar o PDF.
```csharp
// Carregar arquivo Excel de origem contendo imagens externas
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
Estamos usando o `Workbook` classe de Aspose.Cells, que representa seu arquivo Excel. O arquivo pode incluir vários recursos externos, como imagens, que você deseja controlar durante a conversão.
## Etapa 4: definir opções de salvamento de PDF
Antes de salvar a pasta de trabalho como PDF, vamos especificar como você deseja salvá-la. Você pode ajustar essas opções conforme suas necessidades.
```csharp
// Especificar opções de salvamento de PDF - Provedor de fluxo
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Salve cada folha em uma nova página
```
Aqui, estamos criando uma nova instância de `PdfSaveOptions`que permite personalizar a formatação do seu PDF. O `OnePagePerSheet` opção é útil para garantir que cada planilha do Excel tenha sua própria página no PDF final.
## Etapa 5: Atribua seu provedor de transmissão
Com suas opções de PDF definidas, você precisa dizer ao Aspose para usar seu provedor de fluxo personalizado para recursos externos.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
Esta linha conecta seu `Workbook` instância com o `MyStreamProvider` classe que você criou anteriormente. Isso significa que sempre que recursos externos forem encontrados durante a conversão, seu provedor os tratará conforme especificado.
## Etapa 6: Salve a pasta de trabalho como PDF
Com tudo pronto, finalmente é hora de salvar sua pasta de trabalho do Excel como PDF.
```csharp
// Salvar a pasta de trabalho em PDF
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
Ao chamar o `Save` método no objeto de pasta de trabalho e passando seu diretório de saída junto com as opções de PDF, você está convertendo o arquivo do Excel em um PDF lindamente formatado.
## Etapa 7: Confirmar a execução bem-sucedida
Para finalizar, é sempre bom confirmar que seu processo foi bem-sucedido!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Exibir uma mensagem de sucesso no console ajuda a mantê-lo informado sobre o status da sua operação. É um bom hábito incluir essas pequenas confirmações no seu código.
## Conclusão
Pronto! Seguindo estes passos simples, você pode controlar com maestria como os recursos externos são tratados durante conversões de Excel para PDF usando o Aspose.Cells. Isso significa que seus documentos agora podem incluir imagens e outros elementos externos com precisão, garantindo um produto final impecável sempre.
## Perguntas frequentes
### O que é Aspose.Cells?  
Aspose.Cells é uma biblioteca poderosa para desenvolvedores .NET que permite criar, manipular, converter e renderizar arquivos do Excel em vários formatos.
### Como faço para baixar o Aspose.Cells?  
Você pode baixar a versão mais recente do Aspose.Cells em [Link para download](https://releases.aspose.com/cells/net/).
### Posso testar o Aspose.Cells gratuitamente?  
Sim! Você pode obter um teste gratuito visitando o [Página de teste gratuito](https://releases.aspose.com/).
### Onde posso encontrar suporte para o Aspose.Cells?  
Para qualquer dúvida relacionada ao suporte, você pode visitar o [Fórum de suporte Aspose](https://forum.aspose.com/c/cells/9).
### Como posso obter uma licença temporária para o Aspose.Cells?  
Você pode solicitar uma licença temporária [aqui](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}