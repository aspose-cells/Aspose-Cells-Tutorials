---
"description": "Substitua facilmente o texto em caixas de texto em suas planilhas do Excel usando o Aspose.Cells para .NET. Um guia passo a passo para automação do Excel."
"linktitle": "Substituir tag por texto em TextBox no Excel"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Substituir tag por texto em TextBox no Excel"
"url": "/pt/net/excel-shape-text-modifications/replace-tag-text-textbox-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Substituir tag por texto em TextBox no Excel

## Introdução
Neste artigo, vamos nos aprofundar em uma tarefa específica: substituir tags por texto dentro de caixas de texto em uma planilha do Excel usando o Aspose.Cells. Guiaremos você por todo o processo passo a passo, garantindo que você entenda cada detalhe. Ao final deste tutorial, você não apenas aprimorará sua compreensão do Aspose.Cells, como também otimizará suas tarefas relacionadas ao Excel!
## Pré-requisitos
Antes de começar, você precisará de algumas coisas prontas:
1. Visual Studio: Certifique-se de ter o Visual Studio instalado. É um IDE flexível que facilita a programação em C#.
2. Biblioteca Aspose.Cells: Se você ainda não fez isso, baixe a biblioteca Aspose.Cells para .NET do site [página](https://releases.aspose.com/cells/net/). Você também pode obter uma versão de teste gratuita para verificar seus recursos.
3. Conhecimento básico de C#: um conhecimento básico de programação em C# ajudará muito você a seguir este guia facilmente.
Agora que você está pronto, vamos para a parte divertida: escrever o código!
## Pacotes de importação
Vamos começar com o mais importante: vamos importar os pacotes necessários. Isso é crucial porque, sem as importações corretas, seu código não reconhecerá as classes e métodos que usaremos.
## Inicie seu projeto C#
Abra o Visual Studio e crie um novo projeto em C#, de preferência um aplicativo de console, pois ele permitirá que você veja a saída facilmente.
## Adicionar referência Aspose.Cells
- Clique com o botão direito do mouse no seu projeto no Solution Explorer.
- Selecione “Adicionar” > “Referência”.
- Navegue até o local onde você baixou a biblioteca Aspose.Cells e inclua-a no seu projeto.
## Importe os namespaces necessários
Depois de adicionar a referência, adicione o seguinte `using` diretiva no topo do seu arquivo principal:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Isso lhe dá acesso às classes dentro do namespace Aspose.Cells.
Agora que configuramos nosso ambiente, vamos à parte mais importante: a codificação! Nosso objetivo é encontrar tags específicas em caixas de texto dentro de um arquivo Excel e substituí-las pelo texto fornecido.
## Etapa 1: definir o diretório de origem e saída
Primeiro, precisamos especificar onde nosso arquivo de origem do Excel está localizado e onde queremos salvar a versão modificada.
```csharp
// Diretório de origem e saída
string sourceDir = "Your Document Directory"; // Alterar para seu diretório
string outputDir = "Your Document Directory"; // Alterar para seu diretório
```
## Etapa 2: Carregar a pasta de trabalho
É aqui que carregaremos nossa pasta de trabalho do Excel. Se o arquivo não existir, será gerado um erro. Portanto, certifique-se de que o caminho do arquivo esteja correto!
```csharp
Workbook wb = new Workbook(sourceDir + "sampleReplaceTagWithText.xlsx");
```
Aqui, estamos carregando um arquivo Excel existente chamado `sampleReplaceTagWithText.xlsx`.
## Etapa 3: definir tags e texto de substituição
Em seguida, precisamos definir as tags que estamos procurando e o que queremos usar para substituí-las.
```csharp
string tag = "TAG_2$TAG_1";
string replace = "1$ys";
```
Neste exemplo, as tags são divididas usando `$`Você pode substituir isso por qualquer delimitador que preferir.
## Etapa 4: faça um loop sobre as tags e substitua
Criaremos um loop para percorrer cada tag que queremos substituir. É aqui que a mágica acontece!
```csharp
for (int i = 0; i < tag.Split('$').Length; i++)
{
    sheetReplace(wb, "<" + tag.Split('$')[i] + ">", replace.Split('$')[i]);
}
```
## Etapa 5: Salve a pasta de trabalho
Agora que fizemos as substituições, é hora de salvar a pasta de trabalho modificada no formato desejado. Veja como convertê-la para PDF.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
wb.Save(outputDir + "outputReplaceTagWithText.pdf", opts);
```
Você também pode salvá-lo em vários outros formatos, incluindo XLSX.
## Etapa 6: Implementar a lógica de substituição
É aqui que reside o coração da nossa funcionalidade. `sheetReplace` O método tratará da substituição real nas planilhas do Excel.
```csharp
public static void sheetReplace(Workbook workbook, string sFind, string sReplace)
{
    string finding = sFind;
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sheet.Replace(finding, sReplace);
        for (int j = 0; j < 3; j++)
        {
            if (sheet.PageSetup.GetHeader(j) != null)
                sheet.PageSetup.SetHeader(j, sheet.PageSetup.GetHeader(j).Replace(finding, sReplace));
                
            if (sheet.PageSetup.GetFooter(j) != null)
                sheet.PageSetup.SetFooter(j, sheet.PageSetup.GetFooter(j).Replace(finding, sReplace));
        }
    }
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sFind = sFind.Replace("<", "&lt;");
        sFind = sFind.Replace(">", "&gt;");
        foreach (Aspose.Cells.Drawing.TextBox mytextbox in sheet.TextBoxes)
        {
            if (mytextbox.HtmlText != null)
            {
                if (mytextbox.HtmlText.IndexOf(sFind) >= 0)
                {
                    mytextbox.HtmlText = mytextbox.HtmlText.Replace(sFind, sReplace);
                }
            }
        }
    }
}
```
- Primeiro, percorremos cada planilha da pasta de trabalho.
- Substituímos a tag principal não apenas no conteúdo da célula, mas também nos cabeçalhos e rodapés (se existirem).
- Por fim, verificamos cada caixa de texto na planilha e substituímos o texto dentro delas, com base na tag que estamos procurando.
## Conclusão
pronto! Agora você aprendeu a substituir tags por texto em caixas de texto em seus documentos do Excel usando o Aspose.Cells para .NET. Isso pode economizar muito tempo, especialmente ao lidar com tarefas repetitivas em planilhas.
## Perguntas frequentes
### Posso substituir tags em vários arquivos do Excel de uma só vez?
Sim, ao executar um loop em uma lista de arquivos, você pode aplicar a mesma lógica a vários arquivos do Excel.
### Preciso de uma licença paga para usar o Aspose.Cells?
Você pode começar com um teste gratuito, mas para obter a funcionalidade completa, precisará adquirir uma licença. Confira [Opções de compra da Aspose](https://purchase.aspose.com/buy).
### Posso substituir imagens em caixas de texto usando Aspose.Cells?
O Aspose.Cells lida principalmente com texto. No entanto, você pode manipular imagens separadamente, se necessário.
### Em quais formatos posso salvar meu arquivo Excel modificado?
Você pode salvá-lo em vários formatos, incluindo XLSX, PDF, CSV, etc.
### Onde posso encontrar suporte para o Aspose.Cells?
Você pode encontrar suporte e fazer perguntas no [Fórum Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}