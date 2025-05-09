---
"description": "Aprenda a especificar propriedades de documento como versão, autor e título em um arquivo Excel programaticamente usando o Aspose.Cells para .NET com instruções passo a passo."
"linktitle": "Especificando a versão do documento do arquivo Excel programaticamente no .NET"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Especificando a versão do documento do arquivo Excel programaticamente no .NET"
"url": "/pt/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Especificando a versão do documento do arquivo Excel programaticamente no .NET

## Introdução
O Aspose.Cells para .NET é uma biblioteca poderosa que permite aos desenvolvedores manipular arquivos do Excel programaticamente com facilidade. Seja para criar arquivos do Excel do zero ou modificar arquivos existentes, o Aspose.Cells oferece uma API abrangente para atingir seus objetivos. Um desses recursos é a especificação de propriedades do documento, como versão, autor ou título. Este tutorial mostrará como especificar a versão do documento de um arquivo do Excel programaticamente usando o Aspose.Cells para .NET.
## Pré-requisitos
Antes de entrarmos em detalhes, vamos garantir que você tenha tudo o que precisa para seguir este tutorial:
1. Aspose.Cells para .NET: Você pode baixar a versão mais recente [aqui](https://releases.aspose.com/cells/net/). Se você ainda não adquiriu uma licença, você pode optar por uma [licença temporária](https://purchase.aspose.com/temporary-license/) para explorar os recursos.
2. Ambiente de desenvolvimento .NET: você pode usar o Visual Studio ou qualquer IDE compatível com .NET.
3. Conhecimento básico de C#: entender a programação em C# tornará mais fácil acompanhar.
## Pacotes de importação
Antes de começar a programar, você precisa importar os namespaces necessários da biblioteca Aspose.Cells. Isso lhe dará acesso às classes e métodos necessários para a manipulação de arquivos do Excel.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Esses dois namespaces serão essenciais para interagir com a pasta de trabalho e suas propriedades de documento integradas.
Agora, vamos detalhar o processo de especificação de propriedades de documento em um arquivo Excel, incluindo versão, título e autor.
## Etapa 1: inicializar o objeto da pasta de trabalho
primeiro passo é criar uma nova instância do `Workbook` objeto. Este objeto representa todo o arquivo Excel com o qual você trabalhará.
```csharp
Workbook wb = new Workbook();
```
O `Workbook` A classe fornece uma representação de um arquivo do Excel. Ao instanciá-la, criamos uma pasta de trabalho do Excel em branco que podemos manipular.
## Etapa 2: acessar as propriedades do documento integradas
O Aspose.Cells oferece propriedades de documento integradas, que incluem campos como título, autor e versão do documento. Você pode acessar essas propriedades por meio do `BuiltInDocumentProperties` coleção.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
O `BuiltInDocumentPropertyCollection` A classe fornece acesso a uma coleção de propriedades de documentos integradas, como título, autor e outros metadados normalmente associados ao documento.
## Etapa 3: Defina o título do documento do Excel
Em seguida, definiremos o título do documento do Excel. Esses metadados ajudam a identificar e gerenciar o arquivo posteriormente.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
Definir o título é importante para a organização do documento. Esses metadados podem ser vistos nas propriedades do arquivo e podem ser usados por sistemas externos para catalogar ou identificar o documento com mais eficácia.
## Etapa 4: especifique o autor
O autor do documento também pode ser especificado para refletir quem criou ou modificou o arquivo.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
Esta etapa ajuda a atribuir o documento ao seu criador, fornecendo metadados adicionais para gerenciamento de documentos ou cenários de colaboração.
## Etapa 5: especifique a versão do documento
Uma das propriedades mais cruciais que abordaremos neste tutorial é a versão do documento. Esta etapa permite especificar a versão do documento, o que é útil ao trabalhar em ambientes que exigem controle de versão.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
Definir a versão do documento esclarece qual versão do documento ou biblioteca foi usada para criar o arquivo. Isso é particularmente importante em ambientes que precisam rastrear revisões de arquivos ou compatibilidade com diferentes versões de bibliotecas.
## Etapa 6: Salve o arquivo do Excel
Por fim, você pode salvar o arquivo do Excel com todas as propriedades que acabou de definir. O Aspose.Cells permite salvar o arquivo em vários formatos, mas, para este exemplo, vamos usar o `.xlsx` formatar.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
O `Save` O método é usado para salvar o arquivo no diretório especificado. Aqui, estamos salvando-o como um arquivo Excel no `.xlsx` formato. Se necessário, Aspose.Cells também suporta formatos como `.xls`, `.csv`, e `.pdf`, proporcionando flexibilidade com base nas necessidades do seu projeto.
## Conclusão
Neste tutorial, explicamos como especificar propriedades de um documento, especialmente a versão do documento, em um arquivo Excel usando o Aspose.Cells para .NET. O Aspose.Cells é uma ferramenta extremamente flexível e poderosa que permite manipular arquivos do Excel programaticamente, tornando-se um ótimo recurso para qualquer desenvolvedor .NET que trabalhe com planilhas.
## Perguntas frequentes
### Posso modificar outras propriedades internas usando Aspose.Cells?  
Sim, você pode modificar outras propriedades internas, como assunto, palavras-chave e comentários, entre outras.
### Quais formatos de arquivo são suportados pelo Aspose.Cells?  
Aspose.Cells suporta uma grande variedade de formatos, incluindo `.xls`, `.xlsx`, `.csv`, `.pdf`, e muito mais.
### Preciso de uma licença para usar o Aspose.Cells para .NET?  
Você pode explorar Aspose.Cells com um [teste gratuito](https://releases.aspose.com/) ou solicitar um [licença temporária](https://purchase.aspose.com/temporary-license/) para testes estendidos.
### Posso usar o Aspose.Cells em um aplicativo web?  
Sim, o Aspose.Cells pode ser usado tanto em aplicativos desktop quanto web. É altamente versátil e se integra bem com frameworks web .NET.
### Onde posso obter suporte para o Aspose.Cells?  
Você pode acessar a comunidade e o suporte por meio do [Fórum de suporte do Aspose.Cells](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}