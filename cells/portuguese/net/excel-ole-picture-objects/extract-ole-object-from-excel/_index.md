---
title: Extrair objeto OLE do Excel
linktitle: Extrair objeto OLE do Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a extrair objetos OLE de arquivos do Excel usando o Aspose.Cells para .NET. Guia passo a passo para extração fácil.
weight: 10
url: /pt/net/excel-ole-picture-objects/extract-ole-object-from-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair objeto OLE do Excel

## Introdução
No mundo tecnológico de hoje, lidar com arquivos do Excel é uma tarefa comum, especialmente para aqueles em análise de dados, finanças e gerenciamento de projetos. Um aspecto frequentemente esquecido é o manuseio de objetos OLE (Object Linking and Embedding) em planilhas do Excel. Eles podem ser documentos incorporados, imagens ou até mesmo tipos de dados complexos que desempenham um papel crucial no aprimoramento da funcionalidade e riqueza de seus arquivos do Excel. Se você é um usuário do Aspose.Cells procurando extrair esses objetos OLE programaticamente usando .NET, você está no lugar certo! Este guia o guiará pelo processo passo a passo, garantindo que você entenda não apenas como fazê-lo, mas também por que cada parte do processo é significativa.
## Pré-requisitos
Antes de nos aprofundarmos nos detalhes essenciais da extração de objetos OLE, há algumas coisas que você precisa ter em mente:
1. Conhecimento básico de C#: Se você está familiarizado com C#, você já está no caminho certo. Se não, não se preocupe! Nós manteremos as coisas simples.
2. Aspose.Cells instalado: Você precisará da biblioteca Aspose.Cells. Você pode baixá-la do site[aqui](https://releases.aspose.com/cells/net/).
3. Um ambiente de desenvolvimento compatível: certifique-se de ter um ambiente de desenvolvimento .NET configurado, como o Visual Studio, pronto para uso.
4. Um arquivo Excel de exemplo: você precisará de um arquivo Excel com objetos OLE incorporados para testes. 
Depois de atender a esses pré-requisitos, podemos começar nossa jornada no mundo da extração de objetos OLE.
## Pacotes de importação
Primeiro, vamos importar os pacotes necessários que usaremos em nosso tutorial. No seu projeto C#, você precisará incluir o namespace Aspose.Cells. Veja como você pode fazer isso:
```csharp
using System.IO;
using Aspose.Cells;
```
## Etapa 1: Defina o diretório de documentos
Nesta etapa, definiremos o caminho onde nosso arquivo Excel está localizado. Você pode se perguntar por que isso é importante. É como preparar o cenário para uma apresentação — ajuda o script a saber onde encontrar os atores (no nosso caso, o arquivo Excel).
```csharp
string dataDir = "Your Document Directory";
```
 Substituir`"Your Document Directory"` com o caminho real onde seu arquivo Excel (`book1.xls`) é armazenado.
## Etapa 2: Abra o arquivo Excel
Agora que configuramos nosso diretório de documentos, o próximo passo é abrir o arquivo Excel. Pense nisso como abrir um livro antes de começar a ler — é essencial ver o que tem dentro.
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
## Etapa 3: Acesse a coleção de objetos OLE
Cada planilha em uma pasta de trabalho do Excel pode conter vários objetos, incluindo objetos OLE. Aqui, estamos acessando a coleção de objetos OLE da primeira planilha. É semelhante a selecionar uma página para verificar imagens e documentos incorporados.
```csharp
Aspose.Cells.Drawing.OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```
## Etapa 4: Faça um loop pelos objetos OLE
Agora vem a parte divertida — percorrer todos os objetos OLE em nossa coleção. Esta etapa é crucial, pois nos permite lidar com vários objetos OLE de forma eficiente. Imagine vasculhar um baú de tesouro para encontrar itens valiosos!
```csharp
for (int i = 0; i < oles.Count; i++)
{
    Aspose.Cells.Drawing.OleObject ole = oles[i];
    // Mais lógica para lidar com cada objeto
}
```
## Etapa 5: especifique o nome do arquivo de saída
À medida que nos aprofundamos em cada objeto OLE, precisamos criar um nome de arquivo para os objetos extraídos. Por quê? Porque, uma vez que os extraímos, queremos manter tudo organizado para que possamos encontrar facilmente nossos tesouros mais tarde.
```csharp
string fileName = dataDir + "ole_" + i + ".";
```
## Etapa 6: Determine o tipo de formato de arquivo
Cada objeto OLE pode ser de tipos diferentes (por exemplo, documentos, planilhas, imagens). É crucial determinar o tipo de formato para que você possa extraí-lo corretamente. É como saber a receita de um prato — você precisa saber os ingredientes!
```csharp
switch (ole.FileFormatType)
{
    case FileFormatType.Doc:
        fileName += "doc";
        break;
    case FileFormatType.Xlsx:
        fileName += "xlsx";
        break;
    case FileFormatType.Ppt:
        fileName += "ppt";
        break;
    case FileFormatType.Pdf:
        fileName += "pdf";
        break;
    case FileFormatType.Unknown:
        fileName += "jpg";
        break;
    default:
        // Lidar com outros formatos de arquivo
        break;
}
```
## Etapa 7: Salve o objeto OLE
 Agora, vamos prosseguir para salvar o objeto OLE. Se o objeto for um arquivo Excel, nós o salvaremos usando um`MemoryStream` que nos permite manipular os dados na memória antes de escrevê-los. Este passo é semelhante a empacotar seu tesouro antes de enviá-lo a um amigo.
```csharp
if (ole.FileFormatType == FileFormatType.Xlsx)
{
    MemoryStream ms = new MemoryStream();
    ms.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    Workbook oleBook = new Workbook(ms);
    oleBook.Settings.IsHidden = false;
    oleBook.Save(dataDir + "Excel_File" + i + ".out.xlsx");
}
```
 Para outros tipos de arquivos, usaremos um`FileStream` para criar o arquivo no disco.
```csharp
else
{
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
}
```

## Conclusão
assim, você navegou com sucesso nas águas da extração de objetos OLE com o Aspose.Cells para .NET! Seguindo essas etapas, você pode facilmente extrair e gerenciar objetos incorporados de seus arquivos Excel. Lembre-se, como qualquer habilidade valiosa, a prática leva à perfeição. Então, aproveite seu tempo experimentando diferentes arquivos Excel, e logo você se tornará um profissional em extração OLE!
## Perguntas frequentes
### O que são objetos OLE no Excel?
Objetos OLE são tecnologias que permitem incorporar e vincular documentos e dados em outros aplicativos dentro de uma planilha do Excel.
### Por que eu precisaria extrair objetos OLE?
Extrair objetos OLE permite que você acesse e manipule documentos ou imagens incorporados independentemente do arquivo original do Excel.
### O Aspose.Cells pode manipular todos os tipos de arquivos incorporados?
Sim, o Aspose.Cells pode gerenciar vários objetos OLE, incluindo documentos do Word, planilhas do Excel, apresentações do PowerPoint e imagens.
### Como instalo o Aspose.Cells para .NET?
 Você pode instalar o Aspose.Cells baixando-o do site deles[página de lançamento](https://releases.aspose.com/cells/net/).
### Onde posso encontrar suporte para o Aspose.Cells?
Você pode obter suporte para Aspose.Cells em seu[fórum de suporte](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
