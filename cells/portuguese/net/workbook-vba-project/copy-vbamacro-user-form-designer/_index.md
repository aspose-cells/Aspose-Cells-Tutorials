---
"description": "Aprenda a copiar com eficiência o Designer de Formulários de Usuário de Macros VBA no Aspose.Cells para .NET com nosso tutorial passo a passo completo! Libere todo o potencial do Excel."
"linktitle": "Copiar o armazenamento do VBAMacro User Form Designer para a pasta de trabalho usando Aspose.Cells"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Copiar o armazenamento do VBAMacro User Form Designer para a pasta de trabalho usando Aspose.Cells"
"url": "/pt/net/workbook-vba-project/copy-vbamacro-user-form-designer/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Copiar o armazenamento do VBAMacro User Form Designer para a pasta de trabalho usando Aspose.Cells

## Introdução
Bem-vindo! Se você busca aprimorar sua experiência no Excel com macros VBA e formulários de usuário, está no lugar certo! Neste guia, vamos nos aprofundar em como copiar facilmente um Designer de Formulário de Usuário de Macros VBA de uma pasta de trabalho para outra usando o Aspose.Cells para .NET. Seja você um desenvolvedor experiente ou iniciante, nós o guiaremos por cada etapa crucial. Considere este guia o seu guia para dominar a arte de manipular arquivos do Excel programaticamente. Pronto para começar? Vamos lá!
## Pré-requisitos
Antes de começarmos a trabalhar nos detalhes da codificação, vamos garantir que você tenha tudo o que precisa:
1. Ambiente de desenvolvimento em C#: você deve ter um ambiente de trabalho pronto para desenvolvimento em C#. O Visual Studio é altamente recomendado.
2. Biblioteca Aspose.Cells para .NET: Certifique-se de ter a biblioteca Aspose.Cells integrada ao seu projeto. Você pode facilmente [baixe aqui](https://releases.aspose.com/cells/net/).
3. Conhecimento básico de VBA e macros do Excel: um bom entendimento do VBA e de como as macros do Excel funcionam ajudará você a navegar por este tutorial com facilidade.
4. Um arquivo Excel com um formulário de usuário: para experimentar, criar ou obter uma pasta de trabalho do Excel que contenha um formulário de usuário, de preferência com macros habilitadas (como `.xlsm` arquivos).
## Pacotes de importação
No seu projeto C#, você precisará importar determinados namespaces no topo do arquivo para utilizar as funcionalidades do Aspose.Cells. Veja como fazer isso:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
Incluir esses namespaces permite que você acesse todas as ferramentas poderosas incorporadas na biblioteca Aspose.Cells. 
Agora que cobrimos nossos pré-requisitos e pacotes, é hora de passar para a parte divertida: a codificação! Vamos detalhar passo a passo.
## Etapa 1: Defina seus diretórios de origem e saída
Primeiro, você precisa estabelecer onde seus arquivos estão localizados:
```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
// Diretório de saída
string outputDir = "Your Document Directory";
```
Aqui, substitua `"Your Document Directory"` com o caminho real onde seus arquivos estão armazenados. É aqui que nossa pasta de trabalho de origem (com o UserForm) será obtida e onde a nova pasta de trabalho será salva.
## Etapa 2: Criar uma pasta de trabalho de destino vazia
Em seguida, vamos criar nossa pasta de trabalho de destino, onde copiaremos nosso formulário de usuário e macros:
```csharp
// Criar pasta de trabalho de destino vazia
Workbook target = new Workbook();
```
Esta linha de código inicializa uma nova pasta de trabalho vazia para preenchermos com dados. Pense nela como uma tela em branco para sua obra-prima!
## Etapa 3: Carregue sua pasta de trabalho de modelo
Precisamos carregar a pasta de trabalho que contém seu formulário de usuário e macros:
```csharp
// Carregue o arquivo Excel contendo o formulário de usuário do VBA-Macro Designer
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
Certifique-se de mudar `"sampleDesignerForm.xlsm"` ao nome do seu arquivo. Esta pasta de trabalho é como um livro de receitas — é de onde extrairemos os ingredientes!
## Etapa 4: Copiar planilhas para a pasta de trabalho de destino
Agora, vamos começar a copiar planilhas do nosso modelo para a pasta de trabalho de destino:
```csharp
// Copie todas as planilhas de modelo para a pasta de trabalho de destino
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // Coloque a mensagem na célula A2 da planilha de destino
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
Nesta etapa, percorremos cada planilha do modelo e as copiamos para a nossa pasta de trabalho de destino. Se você pensar bem, é como transferir suas melhores receitas de um livro de receitas para outro!
## Etapa 5: Copie as macros VBA do modelo
Em seguida, copiaremos as macros do VBA, incluindo os módulos do UserForm Designer, para nossa nova pasta de trabalho:
```csharp
// Copie o VBA-Macro Designer UserForm do modelo para o destino
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // Copiar código do módulo ThisWorkbook
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // Copie o código e os dados de outros módulos
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            // Obter os dados do formulário do usuário, ou seja, armazenamento do designer
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // Adicione o armazenamento do designer ao projeto Vba de destino
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
Este pedaço robusto de código verifica cada módulo VBA no arquivo de modelo. Estamos copiando o design do UserForm e seus códigos associados. É como garantir que você não só receberá a famosa receita de torta da vovó, mas também suas técnicas exatas de cozimento!
## Etapa 6: Salve a pasta de trabalho de destino
Depois de conseguirmos todas as nossas cópias, é hora de salvar nosso trabalho duro:
```csharp
// Salvar a pasta de trabalho de destino
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
Certifique-se de modificar o nome do arquivo de saída conforme necessário. Depois de salvá-lo, você estará efetivamente criando sua própria versão personalizada da pasta de trabalho, repleta de macros e formulários de usuário. Que empolgante!
## Etapa 7: Confirme o sucesso
Por fim, vamos imprimir uma mensagem de sucesso no console:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
Esta pequena linha garante que seu processo ocorreu sem problemas. É a cereja do bolo da sua programação!
## Conclusão
Parabéns! Você concluiu o guia passo a passo para copiar um Designer de Formulários de Usuário de Macro VBA de uma pasta de trabalho para outra usando o Aspose.Cells para .NET. Pode parecer um pouco complicado no início, mas com a prática, você lidará com as manipulações de pastas de trabalho como um profissional. Lembre-se: programar é uma questão de prática, então não hesite em experimentar coisas diferentes em seus arquivos do Excel. Se tiver alguma dúvida ou encontrar algum problema, sinta-se à vontade para consultar os fóruns ou a documentação do Aspose para obter suporte!
## Perguntas frequentes
### Quais versões do Excel o Aspose.Cells suporta?
O Aspose.Cells suporta uma ampla variedade de formatos do Excel, incluindo XLSX, XLSM, CSV e muito mais.
### Posso usar o Aspose.Cells gratuitamente?
Sim! Você pode começar com um teste gratuito, que lhe permite avaliar a biblioteca: [Teste grátis](https://releases.aspose.com/).
### Preciso do Visual Studio para executar este código?
Embora seja altamente recomendado por seus recursos fáceis de usar, qualquer IDE C# serve, desde que suporte desenvolvimento .NET.
### Onde posso encontrar mais exemplos e documentação?
Você pode explorar o [Documentação do Aspose.Cells](https://reference.aspose.com/cells/net/) para mais exemplos e explicações mais detalhadas.
### Como resolvo problemas ao usar o Aspose.Cells?
Você deve visitar o [Fórum de Suporte Aspose](https://forum.aspose.com/c/cells/9) para obter ajuda da comunidade e da equipe de suporte da Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}