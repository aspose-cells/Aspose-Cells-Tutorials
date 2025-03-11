---
title: Copiar dados dentro da pasta de trabalho usando Aspose.Cells
linktitle: Copiar dados dentro da pasta de trabalho usando Aspose.Cells
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a copiar dados com eficiência em uma pasta de trabalho do Excel usando o Aspose.Cells para .NET com um guia passo a passo, exemplos de código e dicas úteis.
weight: 12
url: /pt/net/worksheet-value-operations/copy-data-within-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar dados dentro da pasta de trabalho usando Aspose.Cells

## Introdução
Gerenciar dados dentro de pastas de trabalho do Excel é uma parte essencial de muitos aplicativos. Imagine que você tem um modelo ou uma planilha preenchida com dados essenciais e quer duplicá-los dentro da mesma pasta de trabalho para uso posterior. É aqui que o Aspose.Cells para .NET brilha! Neste guia, vamos orientá-lo na cópia de dados dentro da mesma pasta de trabalho, usando o Aspose.Cells, com um tutorial passo a passo amigável e claro.
## Pré-requisitos
Antes de começarmos a codificar, vamos ter certeza de que temos tudo o que precisamos para concluir esta tarefa:
1.  Biblioteca Aspose.Cells para .NET – Baixe a versão mais recente em[Página de download do Aspose.Cells para .NET](https://releases.aspose.com/cells/net/).
2. Ambiente de desenvolvimento – Você precisará de um IDE compatível com .NET, como o Visual Studio.
3.  Licença – Usando uma avaliação gratuita ou uma licença comprada para Aspose.Cells. Você pode obter uma licença temporária[aqui](https://purchase.aspose.com/temporary-license/) ou explore opções de compra[aqui](https://purchase.aspose.com/buy).
## Pacotes de importação
No seu código, você precisará importar Aspose.Cells para utilizar suas classes e métodos:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Vamos mergulhar no código! Vamos dividir a tarefa de copiar dados dentro de uma pasta de trabalho usando Aspose.Cells for .NET em etapas fáceis de seguir.
## Etapa 1: configure seus caminhos de diretório
Antes de começarmos a lidar com a pasta de trabalho, vamos definir onde nossos arquivos estão localizados e onde queremos salvar a saída. Configurar um caminho de diretório mantém as coisas organizadas.
```csharp
// Defina o caminho do diretório para documentos.
string dataDir = "Your Document Directory";
string inputPath = dataDir + "book1.xls";
```
 Aqui, substitua`"Your Document Directory"` com o caminho real onde sua pasta de trabalho está armazenada. Essa variável de caminho facilitará a referência aos seus arquivos de entrada e saída.
## Etapa 2: Abra o arquivo Excel existente
Para trabalhar com um arquivo Excel, precisamos carregá-lo no objeto workbook em Aspose.Cells. Esta etapa abre o arquivo do qual você deseja copiar os dados.
```csharp
// Abra um arquivo Excel existente.
Workbook wb = new Workbook(inputPath);
```
 Com isso, nosso`Workbook` objeto`wb` agora está pronto para interagir com o conteúdo de`book1.xls`.
## Etapa 3: Acesse a coleção de planilhas
 Agora que a pasta de trabalho está aberta, acessaremos sua coleção de planilhas. O`WorksheetCollection` A classe nos ajuda a trabalhar com várias planilhas dentro da pasta de trabalho.
```csharp
// Crie um objeto Worksheets que faça referência a todas as planilhas na pasta de trabalho.
WorksheetCollection sheets = wb.Worksheets;
```
 Aqui,`sheets` nos permitirá manipular cada planilha na pasta de trabalho, incluindo adicionar uma cópia de uma planilha existente.
## Etapa 4: Copie os dados para uma nova planilha
A parte principal da nossa tarefa é copiar o conteúdo de uma planilha para uma nova planilha dentro da mesma pasta de trabalho. Neste exemplo, copiaremos dados de "Planilha1" para uma nova planilha.
```csharp
// Copie dados da "Planilha1" para uma nova planilha dentro da pasta de trabalho.
sheets.AddCopy("Sheet1");
```
 O`AddCopy` método cria uma cópia exata da planilha especificada, anexando-a à pasta de trabalho. Aqui, estamos duplicando "Sheet1". Você pode especificar o nome de qualquer planilha que queira copiar.
## Etapa 5: Salve a pasta de trabalho com a nova planilha
Depois de copiar a planilha, salve a pasta de trabalho com um novo nome ou em um novo local para preservar as alterações.
```csharp
// Salve a pasta de trabalho com os dados copiados.
wb.Save(dataDir + "CopyWithinWorkbook_out.xls");
```
 Esta linha salva a pasta de trabalho modificada como`CopyWithinWorkbook_out.xls` no diretório especificado.
## Conclusão
E aí está! Copiar dados dentro de uma pasta de trabalho usando o Aspose.Cells para .NET é moleza. O Aspose.Cells simplifica o manuseio de arquivos do Excel e permite que você execute tarefas complexas de gerenciamento de dados com facilidade. Se você precisa duplicar planilhas para uso de modelo, backups ou criar novas versões, as etapas que abordamos ajudarão você a atingir seus objetivos.
 Se você estiver ansioso para explorar mais, confira o[Documentação do Aspose.Cells](https://reference.aspose.com/cells/net/) para recursos e capacidades avançadas.
## Perguntas frequentes
### Posso copiar várias planilhas de uma vez?
Aspose.Cells não oferece suporte à cópia de várias planilhas em uma única chamada, mas você pode percorrer as planilhas que deseja duplicar e copiá-las individualmente.
### Posso renomear a planilha copiada?
 Sim, depois de copiar a planilha, você pode renomeá-la usando`sheets[sheets.Count - 1].Name = "NewSheetName";`.
### O Aspose.Cells é compatível com o .NET Core?
Absolutamente! Aspose.Cells suporta ambientes .NET Framework e .NET Core.
### Como lidar com a formatação ao copiar planilhas?
 O`AddCopy` O método preserva todo o conteúdo e formatação, para que a planilha copiada fique exatamente igual à original.
### E se eu quiser copiar uma planilha para uma pasta de trabalho diferente?
Você pode usar o`Copy` método com uma referência a outra pasta de trabalho, como`sheets.Add().Copy(wb.Worksheets["Sheet1"]);`.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
