---
date: '2026-11-16'
description: Aprenda como adicionar a dependência Maven do Aspose.Cells, recuperar,
  listar e gerenciar conexões de dados do Excel e extrair dados SQL para o Excel usando
  Java.
keywords:
- create excel data connections
- pull sql data excel
- manage excel external connections
- Aspose.Cells
- Java Excel integration
lastmod: '2026-11-16'
og_description: Crie conexões de dados do Excel usando Aspose.Cells para Java. Aprenda
  a adicionar a dependência Maven, recuperar conexões, extrair dados SQL para o Excel
  e gerenciar conexões externas de forma eficiente.
og_image_alt: Guide showing how to create excel data connections using Aspose.Cells
  Java API
og_title: Criar conexões de dados do Excel com Aspose.Cells para Java
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to add Aspose.Cells Maven dependency, retrieve, list, and
    manage Excel data connections, and pull SQL data into Excel using Java.
  headline: Create excel data connections with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to add Aspose.Cells Maven dependency, retrieve, list, and
    manage Excel data connections, and pull SQL data into Excel using Java.
  name: Create excel data connections with Aspose.Cells for Java
  steps:
  - name: load your workbook
    text: The `Workbook` class represents an entire Excel file in memory. Loading
      it is the first step before any connection work.
  - name: retrieve connections
    text: '`workbook.getDataConnections()` returns an `ExternalConnectionCollection`
      containing every defined connection.'
  - name: loop through connections
    text: '`DBConnection` is a subclass of `ExternalConnection` that represents a
      database connection and provides properties such as command text, connection
      string, and parameters. Iterate over the collection, cast each entry to `DBConnection`,
      and read its properties.'
  - name: access parameters
    text: Each `DBConnection` exposes a `getParameters()` method that returns a list
      of name/value pairs.
  type: HowTo
- questions:
  - answer: It is the Maven artifact (`com.aspose:aspose-cells`) that provides the
      Java APIs for reading, writing, and managing Excel files, including external
      data connections.
    question: What is Aspose.Cells Maven dependency?
  - answer: Call `workbook.getDataConnections()` and iterate over the returned `ExternalConnectionCollection`.
    question: How can I list excel data connections in my workbook?
  - answer: Cast each connection to `DBConnection` and use methods like `getCommand()`,
      `getConnectionDescription()`, and `getParameters()`.
    question: How do I extract database connection details from a DBConnection object?
  - answer: Yes, use a standard `for` loop over the collection, cast each to the appropriate
      type, and apply changes as needed.
    question: Can I loop through excel connections to modify them?
  - answer: A valid Aspose.Cells license removes evaluation limitations and enables
      full functionality.
    question: Do I need a license to use these features in production?
  type: FAQPage
tags:
- create excel data connections
- Aspose.Cells
- Java Excel data
- external data connections
title: Criar conexões de dados do Excel com Aspose.Cells para Java
url: /pt/java/advanced-features/aspose-cells-java-excel-external-data-connections/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar conexões de dados do Excel com Aspose.Cells para Java

Em aplicações modernas centradas em dados, **criar conexões de dados do Excel** programaticamente para que você possa extrair dados ao vivo de bancos de dados diretamente para as pastas de trabalho. Adicionar a dependência Maven do Aspose.Cells fornece uma API única e bem documentada que lida com tudo, desde listar conexões existentes até extrair strings de conexão completas — tudo sem exigir o Microsoft Office no servidor. Este tutorial orienta você na configuração, recuperação e uso prático, para que possa integrar o Excel ao seu back‑end SQL com confiança.

## Respostas rápidas
- **Qual é a maneira principal de adicionar Aspose.Cells a um projeto Java?** Inclua o artefato Maven `com.aspose:aspose-cells` no seu `pom.xml`.  
- **Posso listar todas as conexões de dados do Excel?** Sim — chame `workbook.getDataConnections()` e itere sobre a coleção retornada.  
- **Como extraio detalhes da conexão de banco de dados?** Converta cada `ExternalConnection` para `DBConnection` e leia suas propriedades, como texto do comando e string de conexão.  
- **É possível percorrer as conexões do Excel?** Absolutamente — use um loop `for` padrão sobre o `ExternalConnectionCollection`.  
- **Preciso de uma licença para uso em produção?** Uma licença válida do Aspose.Cells remove as limitações de avaliação e desbloqueia a funcionalidade completa.

## O que você aprenderá
- Como **criar conexões de dados do Excel** e recuperá‑las de uma pasta de trabalho existente usando Aspose.Cells para Java.  
- Como extrair informações detalhadas sobre cada conexão, incluindo detalhes do banco de dados e parâmetros.  
- Cenários reais para extrair dados SQL para o Excel e automatizar a geração de relatórios.  
- Dicas para otimizar o desempenho ao manipular pastas de trabalho grandes em Java.

## Por que adicionar a dependência Maven do Aspose.Cells? – benefícios e casos de uso
**Você adiciona o artefato Maven para obter controle programático sobre arquivos Excel sem precisar do Office instalado.** Aspose.Cells suporta **mais de 50 formatos de entrada e saída** e pode processar pastas de trabalho com **até 10.000 linhas** mantendo o uso de memória abaixo de 150 MB ao carregar apenas as partes necessárias. Isso o torna ideal para fluxos de trabalho de **extrair dados SQL para Excel**, relatórios automatizados e gerenciamento centralizado de conexões em ambientes corporativos.

## Pré‑requisitos
- **Aspose.Cells for Java** (versão 25.3 ou posterior).  
- Ambiente de construção Maven ou Gradle.  
- Java 8 ou superior instalado.  

### Bibliotecas necessárias
- **Aspose.Cells for Java** – a biblioteca principal que permite a manipulação de arquivos Excel e o gerenciamento de conexões de dados.

### Configuração do ambiente
- Certifique‑se de que sua IDE ou ferramenta de construção suporte Maven ou Gradle.  
- Verifique se o Java 8 ou mais recente está no seu `PATH`.

## Como adicionar a dependência Maven do Aspose Cells
Carregue a biblioteca adicionando uma única linha de dependência ao seu `pom.xml`. Isso lhe dá acesso imediato ao conjunto completo de APIs do Excel.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Se preferir Gradle, a declaração equivalente é:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Etapas de aquisição de licença
- **Teste gratuito** – Explore a biblioteca sem custo.  
- **Licença temporária** – Prolongue seu período de avaliação.  
- **Compra** – Desbloqueie todos os recursos para cargas de trabalho de produção.

## Inicialização e configuração básicas
Depois que a dependência for resolvida, você pode começar a usar o Aspose.Cells no seu código Java:

```java
import com.aspose.cells.Workbook;

// Load an Excel workbook
Workbook workbook = new Workbook("path_to_your_excel_file.xlsx");
```

## Guia de implementação

### Recurso 1: recuperando conexões de dados externas
**O que é?** Este recurso permite que você **liste conexões de dados do Excel** para saber exatamente de quais fontes externas sua pasta de trabalho depende.

#### Etapa 1: carregue sua pasta de trabalho
A classe `Workbook` representa um arquivo Excel completo na memória. Carregá‑lo é o primeiro passo antes de qualquer trabalho com conexões.

```java
String sourceDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(sourceDir + "/sampleRetrievingSQLConnectionData.xlsx");
```

#### Etapa 2: recupere as conexões
`workbook.getDataConnections()` retorna um `ExternalConnectionCollection` contendo todas as conexões definidas.

```java
import com.aspose.cells.ExternalConnectionCollection;

ExternalConnectionCollection connections = workbook.getDataConnections();
int connectionCount = connections.getCount();
```

### Recurso 2: extraindo detalhes da conexão de banco de dados
**Por que usá‑lo?** Para **extrair detalhes da conexão de banco de dados** como comandos, descrições e strings de conexão para auditoria ou modificação dinâmica.

#### Etapa 1: percorrer as conexões
`DBConnection` é uma subclasse de `ExternalConnection` que representa uma conexão de banco de dados e fornece propriedades como texto do comando, string de conexão e parâmetros.  
Itere sobre a coleção, converta cada entrada para `DBConnection` e leia suas propriedades.

```java
import com.aspose.cells.DBConnection;

for (int i = 0; i < connectionCount; i++) {
    Object connection = connections.get(i);
    if (connection instanceof DBConnection) {
        DBConnection dbConn = (DBConnection) connection;
        
        // Display details
        System.out.println("Command: " + dbConn.getCommand());
        System.out.println("Description: " + dbConn.getConnectionDescription());
        // Add more fields as needed...
    }
}
```

### Recurso 3: extraindo detalhes dos parâmetros de conexão
**Como isso ajuda?** Permite que você **integre o Excel ao banco de dados** acessando cada parâmetro necessário para a conexão, como tokens de autenticação ou argumentos de consulta.

#### Etapa 1: acessar os parâmetros
Cada `DBConnection` expõe um método `getParameters()` que retorna uma lista de pares nome/valor.

```java
import com.aspose.cells.ConnectionParameterCollection;
import com.aspose.cells.ConnectionParameter;

for (int i = 0; i < connectionCount; i++) {
    Object connection = connections.get(i);
    if (connection instanceof DBConnection) {
        DBConnection dbConn = (DBConnection) connection;
        ConnectionParameterCollection parameters = dbConn.getParameters();
        
        for (int j = 0; j < parameters.getCount(); j++) {
            ConnectionParameter param = parameters.get(j);
            
            // Display parameter details
            System.out.println("Name: " + param.getName());
            System.out.println("Value: " + param.getValue());
            // Continue displaying other properties...
        }
    }
}
```

## Aplicações práticas
1. **Integração de dados** – Sincronize automaticamente os dados do Excel com bancos de dados externos.  
2. **Relatórios automatizados** – Extraia dados ao vivo para relatórios atualizados sem atualizações manuais.  
3. **Monitoramento de sistema** – Acompanhe alterações nas conexões de banco de dados para verificações de integridade.  
4. **Validação de dados** – Valide dados externos antes de importá‑los para a pasta de trabalho.

## Considerações de desempenho
- Carregue pastas de trabalho grandes com moderação para manter o uso de memória baixo.  
- Use loops eficientes (conforme mostrado) e evite a criação desnecessária de objetos.  
- Aproveite o ajuste da coleta de lixo do Java para serviços de longa duração.

## Problemas comuns & solução de problemas
- **Conexões nulas** – Certifique‑se de que a pasta de trabalho realmente contém conexões externas; caso contrário, `getDataConnections()` retorna uma coleção vazia.  
- **Licença não configurada** – Sem uma licença válida, você pode ver avisos de avaliação ou funcionalidade limitada.  
- **Fonte de dados não suportada** – Algumas conexões ODBC legadas podem exigir a instalação de drivers adicionais na máquina host.

## Perguntas frequentes

**Q: O que é a dependência Maven do Aspose.Cells?**  
A: É o artefato Maven (`com.aspose:aspose-cells`) que fornece as APIs Java para ler, escrever e gerenciar arquivos Excel, incluindo conexões de dados externas.

**Q: Como posso listar as conexões de dados do Excel na minha pasta de trabalho?**  
A: Chame `workbook.getDataConnections()` e itere sobre o `ExternalConnectionCollection` retornado.

**Q: Como extraio detalhes da conexão de banco de dados de um objeto DBConnection?**  
A: Converta cada conexão para `DBConnection` e use métodos como `getCommand()`, `getConnectionDescription()` e `getParameters()`.

**Q: Posso percorrer as conexões do Excel para modificá‑las?**  
A: Sim, use um loop `for` padrão sobre a coleção, converta cada uma para o tipo apropriado e aplique as alterações conforme necessário.

**Q: Preciso de uma licença para usar esses recursos em produção?**  
A: Uma licença válida do Aspose.Cells remove as limitações de avaliação e habilita a funcionalidade completa.

## Recursos
- [Documentação](https://reference.aspose.com/cells/java/)
- [Baixar versão mais recente](https://releases.aspose.com/cells/java/)
- [Comprar licença](https://purchase.aspose.com/buy)
- [Acesso ao teste gratuito](https://releases.aspose.com/cells/java/)
- [Informações sobre licença temporária](https://purchase.aspose.com/temporary-license/)
- [Fórum de suporte](https://forum.aspose.com/c/cells/9)

---

**Última atualização:** 2026-11-16  
**Testado com:** Aspose.Cells 25.3 (Java)  
**Autor:** Aspose

## Tutoriais relacionados

- [Extrair URL do Excel com Aspose.Cells para Java – Carregar conexões de dados](/cells/java/advanced-features/aspose-cells-java-excel-data-connections/)
- [Aspose.Cells Java: Dominando conexões de pastas de trabalho Excel para integração e análise de dados](/cells/java/import-export/aspose-cells-java-excel-connections/)
- [Modificar conexões de dados do Excel com Aspose.Cells para Java – Guia passo a passo](/cells/java/advanced-features/master-excel-data-connections-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}