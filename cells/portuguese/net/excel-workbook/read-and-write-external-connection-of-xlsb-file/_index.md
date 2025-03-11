---
title: Ler e escrever conexão externa do arquivo XLSB
linktitle: Ler e escrever conexão externa do arquivo XLSB
second_title: Referência da API Aspose.Cells para .NET
description: Aprenda a gerenciar conexões externas em arquivos XLSB usando o Aspose.Cells para .NET neste tutorial abrangente.
weight: 130
url: /pt/net/excel-workbook/read-and-write-external-connection-of-xlsb-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ler e escrever conexão externa do arquivo XLSB

## Introdução

Olá, entusiastas do Excel! Vocês estão prontos para mergulhar no fascinante mundo dos arquivos XLSB e conexões externas? Se você já trabalhou com o Excel, sabe o quão poderoso e versátil ele pode ser, mas às vezes ele vem com suas peculiaridades — especialmente ao lidar com conexões com bancos de dados externos. É aí que o Aspose.Cells para .NET vem para o resgate! Esta biblioteca bacana permite que você manipule arquivos do Excel de forma direta. Neste artigo, nós o guiaremos por um guia passo a passo sobre como ler e escrever conexões externas em um arquivo XLSB.

## Pré-requisitos

Antes de começar, aqui estão algumas coisas que você precisará:

1. Conhecimento básico de C#: Conhecer a linguagem de programação C# ajudará imensamente. Se você se sente confortável escrevendo código C#, está pronto para começar!
2.  Aspose.Cells para .NET: Você precisará ter esta biblioteca instalada em seu ambiente de desenvolvimento. Se você ainda não fez isso, você pode facilmente baixá-la[aqui](https://releases.aspose.com/cells/net/). 
3. Um IDE: você precisará de um editor de código ou de um Ambiente de Desenvolvimento Integrado (IDE), como o Visual Studio. 
4. Arquivo XLSB de exemplo: Trabalharemos com um arquivo XLSB de exemplo que contém conexões externas. Você pode criar o seu próprio ou baixar amostras online. 

Depois de cumprir todos esses pré-requisitos, estamos prontos para começar a codificar!

## Pacotes de importação

Para começar, vamos importar os pacotes necessários em nosso projeto. Certifique-se de ter adicionado uma referência a Aspose.Cells em seu projeto. Aqui está como você pode fazer isso em C#:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Essas importações dão acesso à funcionalidade necessária para manipular arquivos do Excel e suas conexões.

## Etapa 1: Configurar diretórios

Antes de trabalhar com seu arquivo XLSB, você precisa configurar seus diretórios de origem e saída. Esta etapa é essencial para manter seus arquivos organizados.

```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
// Diretório de saída
string outputDir = "Your Output Directory";
```

 Neste trecho de código,`"Your Document Directory"` e`"Your Document Directory"` são assumidos para buscar os respectivos caminhos para onde seus arquivos de entrada e saída residirão. Você pode substituir esses métodos por caminhos codificados se preferir.

## Etapa 2: Carregue o arquivo XLSB

Agora é hora de carregar seu arquivo Excel em um objeto Workbook. Isso lhe dá a habilidade de manipular os dados dentro.

```csharp
// Carregue o arquivo Xlsb de origem do Excel
Workbook wb = new Workbook(sourceDir + "sampleExternalConnection_XLSB.xlsb");
```

 Apenas certifique-se de que seu arquivo XLSB esteja localizado no local especificado`sourceDir`. Se o caminho estiver correto, sua pasta de trabalho estará pronta para manipulação!

## Etapa 3: Acessar conexões externas

Com a pasta de trabalho carregada, você pode acessar suas conexões externas. No nosso caso, recuperaremos a primeira conexão do banco de dados.

```csharp
// Leia a primeira conexão externa que na verdade é uma conexão DB
Aspose.Cells.ExternalConnections.DBConnection dbCon = wb.DataConnections[0] as Aspose.Cells.ExternalConnections.DBConnection;
```

 Aqui,`DataConnections[0]` refere-se à primeira conexão na pasta de trabalho. Estamos convertendo-a como uma`DBConnection` digite para manipulação posterior.

## Etapa 4: Extrair informações de conexão

Agora que você tem acesso à conexão do banco de dados, vamos extrair e imprimir seus detalhes no console. Isso nos ajudará a ver exatamente com o que estamos trabalhando.

```csharp
// Imprima o nome, comando e informações de conexão da conexão DB
Console.WriteLine("Connection Name: " + dbCon.Name);
Console.WriteLine("Command: " + dbCon.Command);
Console.WriteLine("Connection Info: " + dbCon.ConnectionInfo);
```

Esta etapa permite que você verifique o estado atual da sua conexão externa. Você verá o nome da conexão, o comando usado e as informações da conexão impressas no console.

## Etapa 5: Modifique a conexão

Às vezes, uma mudança de nome é tudo o que é necessário para tornar as coisas mais claras ou para corresponder às novas convenções de nomenclatura. Vamos mudar o nome da conexão existente para algo mais relevante.

```csharp
// Modificar o nome da conexão
dbCon.Name = "NewCust";
```

Esta linha de código efetivamente renomeia sua conexão de seu nome original para "NewCust". É uma mudança simples, mas impactante!

## Etapa 6: Salve suas alterações

Após fazer as modificações, você vai querer salvar suas alterações de volta no arquivo XLSB. Veja como fazer isso:

```csharp
// Salvar o arquivo Excel Xlsb
wb.Save(outputDir + "outputExternalConnection_XLSB.xlsb");
```

Esta linha de código salva sua pasta de trabalho atualizada, mantendo todas as suas alterações, incluindo o novo nome da conexão.

## Etapa 7: Confirmar execução

Por fim, vamos confirmar que tudo funcionou bem. Uma mensagem simples no final deixará isso claro.

```csharp
Console.WriteLine("ReadAndWriteExternalConnectionOfXLSBFile executed successfully.\r\n");
```

Esta mensagem garantirá que seu código foi executado com sucesso e que todas as alterações foram salvas conforme o esperado.

## Conclusão

E aí está! Você aprendeu com sucesso como ler e escrever conexões externas em arquivos XLSB usando o Aspose.Cells para .NET. Seguindo essas etapas, você pode gerenciar efetivamente suas conexões de dados do Excel, tornando seu trabalho com o Excel muito mais simplificado e menos frustrante. Lembre-se, não importa se você está lidando com conjuntos de dados extensos ou simplesmente organizando suas informações, o Aspose.Cells tem as ferramentas de que você precisa.

## Perguntas frequentes

### O que é um arquivo XLSB?  
Um arquivo XLSB é um formato de arquivo binário do Excel que armazena dados de planilhas em um formato binário, tornando-os mais compactos e rápidos de abrir.

### Como instalo o Aspose.Cells para .NET?  
 Você pode baixá-lo facilmente no site da Aspose[aqui](https://releases.aspose.com/cells/net/).

### Posso usar o Aspose.Cells gratuitamente?  
 Sim! Você pode começar com um teste gratuito, que está disponível[aqui](https://releases.aspose.com/).

### O Aspose.Cells suporta outros formatos de arquivo?  
Absolutamente! O Aspose.Cells suporta uma variedade de formatos de arquivo, incluindo XLSX, CSV e mais.

### Onde posso procurar ajuda se tiver problemas?  
Você pode obter suporte nos fóruns do Aspose[aqui](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
