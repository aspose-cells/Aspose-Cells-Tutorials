---
title: Lendo números de planilhas programaticamente em .NET
linktitle: Lendo números de planilhas programaticamente em .NET
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a ler planilhas do Numbers e convertê-las em PDF usando o Aspose.Cells para .NET neste tutorial detalhado.
weight: 18
url: /pt/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lendo números de planilhas programaticamente em .NET

## Introdução
No mundo digital de hoje, o gerenciamento de dados é uma habilidade vital, e as planilhas estão na vanguarda da organização de dados. Mas e se você precisar trabalhar com uma planilha do Numbers — aqueles arquivos criados pelo aplicativo Numbers da Apple — usando .NET? Não se preocupe; você não está sozinho! Neste tutorial, mostraremos o processo de leitura de uma planilha do Numbers programaticamente com o Aspose.Cells para .NET. Você aprenderá como carregar um arquivo do Numbers e convertê-lo em PDF.
## Pré-requisitos
Antes de começar, há algumas coisas que você precisa ter em mãos:
1. Aspose.Cells para .NET: Certifique-se de ter a biblioteca Aspose.Cells instalada. Você pode baixá-la[aqui](https://releases.aspose.com/cells/net/).
2. Visual Studio: É recomendável ter o Visual Studio (ou qualquer outro IDE compatível com .NET) instalado em sua máquina.
3. Conhecimento básico de C#: Um pouco de familiaridade com a programação em C# ajudará você a acompanhar sem problemas.
4. Seu diretório de documentos: você precisará de um diretório onde seu arquivo do Numbers esteja armazenado, juntamente com um local para salvar o PDF convertido.
Depois de atender a esses pré-requisitos, você estará pronto para começar!
## Pacotes de importação
Para começar, precisamos importar os pacotes necessários para o nosso projeto C#. Este é um passo crucial porque nos permite alavancar as funcionalidades fornecidas pela biblioteca Aspose.Cells.
1. Abra seu projeto C# no Visual Studio.
2. Adicione uma referência à biblioteca Aspose.Cells:
   - Se você estiver usando o NuGet, basta executar o seguinte comando no Console do Gerenciador de Pacotes:
```
 Install-Package Aspose.Cells
 ```
3. Importe os namespaces necessários no seu código:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Agora que importamos os pacotes necessários, vamos passar para o guia passo a passo para ler uma planilha do Numbers.
## Etapa 1: especifique os diretórios de origem e saída
Nesta etapa, configuraremos os diretórios onde seu arquivo de origem do Numbers está localizado e onde você deseja salvar o PDF de saída.
```csharp
// Diretório de origem
string sourceDir = "Your Document Directory"; // Atualize isso para seu diretório atual
// Diretório de saída
string outputDir = "Your Document Directory"; // Atualize isso para seu diretório atual
```
 Aqui, estamos definindo duas variáveis de string,`sourceDir` e`outputDir` , para especificar os locais dos arquivos de entrada e saída. Certifique-se de substituir`"Your Document Directory"` com os caminhos reais no seu sistema.
## Etapa 2: Configurar opções de carga para formato de números
Em seguida, especificaremos as opções de carga para ler uma planilha do Numbers. Esta etapa é essencial, pois informa ao Aspose como interpretar o arquivo do Numbers.
```csharp
// Especifique as opções de carga; queremos carregar a planilha Numbers
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
 Nós criamos um`LoadOptions` objeto e especifique o formato como`LoadFormat.Numbers`. Isso informa à biblioteca Aspose.Cells que estamos trabalhando com um arquivo Numbers. 
## Etapa 3: Carregue a planilha Numbers em uma pasta de trabalho
Agora, é hora de carregar a planilha Numbers real em um`Workbook` objeto.
```csharp
// Carregue a planilha Numbers na pasta de trabalho com as opções de carregamento acima
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
 Nós instanciamos um`Workbook` objeto e passe o caminho do arquivo do arquivo Numbers junto com nossas opções de carregamento. Certifique-se de que o nome do arquivo (`sampleNumbersByAppleInc.numbers`) corresponde ao nome real do seu arquivo Numbers.
## Etapa 4: Salve a pasta de trabalho como PDF
Depois que o arquivo Numbers for carregado com sucesso, o próximo passo é salvá-lo em um formato diferente, especificamente, PDF.
```csharp
// Salvar a pasta de trabalho em formato PDF
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
 Aqui, chamamos de`Save` método sobre o`Workbook` objeto, especificando o caminho do arquivo de saída e o formato em que queremos salvá-lo. Neste caso, estamos salvando-o como um PDF. Certifique-se de que o nome do arquivo de saída (`outputNumbersByAppleInc.pdf`) é único e não substitui nenhum arquivo existente.
## Etapa 5: Confirme o sucesso
Por fim, vamos adicionar uma mensagem para confirmar que nossa operação foi bem-sucedida.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
Esta linha de código imprimirá uma mensagem de sucesso no console quando tudo estiver pronto. É sempre bom ter feedback, certo?
## Conclusão
E aí está! Você leu com sucesso uma planilha do Numbers e a converteu para PDF usando o Aspose.Cells para .NET. Esta biblioteca poderosa permite que você manipule planilhas sem esforço, tornando suas tarefas de gerenciamento de dados muito fáceis. Não importa se você está desenvolvendo aplicativos ou apenas precisa lidar com planilhas de forma mais eficiente, o Aspose.Cells é uma ferramenta fantástica para ter em seu kit de ferramentas.
## Perguntas frequentes
### Que tipos de arquivos o Aspose.Cells pode ler?  
O Aspose.Cells pode ler uma variedade de formatos de arquivo, incluindo arquivos XLS, XLSX, CSV e Numbers. 
### Posso editar arquivos do Numbers usando o Aspose.Cells?  
Sim, você pode ler, manipular e salvar arquivos do Numbers com o Aspose.Cells.
### O Aspose.Cells é gratuito?  
 Aspose.Cells oferece um teste gratuito, mas você precisará de uma licença para uso estendido. Verifique o preço[aqui](https://purchase.aspose.com/buy).
### que devo fazer se encontrar um erro ao carregar um arquivo do Numbers?  
 Certifique-se de que você está usando as opções de carregamento corretas e que o caminho do arquivo está correto. Para obter mais suporte, visite o[Fórum de suporte Aspose](https://forum.aspose.com/c/cells/9).
### Como posso obter uma licença temporária para o Aspose.Cells?  
 Você pode solicitar uma licença temporária[aqui](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
