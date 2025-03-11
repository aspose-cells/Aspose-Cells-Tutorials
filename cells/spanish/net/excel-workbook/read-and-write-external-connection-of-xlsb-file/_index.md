---
title: Leer y escribir una conexión externa de un archivo XLSB
linktitle: Leer y escribir una conexión externa de un archivo XLSB
second_title: Referencia de API de Aspose.Cells para .NET
description: Aprenda a administrar conexiones externas en archivos XLSB usando Aspose.Cells para .NET en este completo tutorial.
weight: 130
url: /es/net/excel-workbook/read-and-write-external-connection-of-xlsb-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Leer y escribir una conexión externa de un archivo XLSB

## Introducción

¡Hola, entusiastas de Excel! ¿Están listos para sumergirse en el fascinante mundo de los archivos XLSB y las conexiones externas? Si alguna vez trabajó con Excel, sabe lo poderoso y versátil que puede ser, pero a veces tiene sus peculiaridades, especialmente cuando se trata de conexiones a bases de datos externas. ¡Ahí es donde Aspose.Cells para .NET viene al rescate! Esta ingeniosa biblioteca le permite manipular archivos de Excel de una manera sencilla. En este artículo, lo guiaremos a través de una guía paso a paso sobre cómo leer y escribir conexiones externas en un archivo XLSB.

## Prerrequisitos

Antes de comenzar, aquí hay algunas cosas que necesitarás:

1. Conocimientos básicos de C#: conocer el lenguaje de programación C# será de gran ayuda. Si te sientes cómodo escribiendo código C#, ¡estás listo para empezar!
2.  Aspose.Cells para .NET: Necesitará tener esta biblioteca instalada en su entorno de desarrollo. Si aún no lo ha hecho, puede descargarla fácilmente[aquí](https://releases.aspose.com/cells/net/). 
3. Un IDE: necesitará un editor de código o un entorno de desarrollo integrado (IDE) como Visual Studio. 
4. Archivo XLSB de muestra: trabajaremos con un archivo XLSB de muestra que contiene conexiones externas. Puede crear su propio archivo o descargar muestras en línea. 

¡Una vez que tengamos todos estos requisitos previos en su lugar, estaremos listos para comenzar a codificar!

## Importar paquetes

Para comenzar, importemos los paquetes necesarios en nuestro proyecto. Asegúrese de haber agregado una referencia a Aspose.Cells en su proyecto. A continuación, le indicamos cómo hacerlo en C#:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Estas importaciones le brindan acceso a la funcionalidad que necesitará para manipular archivos de Excel y sus conexiones.

## Paso 1: Configurar directorios

Antes de trabajar con el archivo XLSB, debe configurar los directorios de origen y salida. Este paso es esencial para mantener los archivos organizados.

```csharp
// Directorio de fuentes
string sourceDir = "Your Document Directory";
// Directorio de salida
string outputDir = "Your Output Directory";
```

 En este fragmento de código,`"Your Document Directory"` y`"Your Document Directory"` Se supone que obtienen las rutas respectivas donde se ubicarán los archivos de entrada y salida. Puede reemplazar estos métodos con rutas codificadas si lo prefiere.

## Paso 2: Cargue el archivo XLSB

Ahora es el momento de cargar el archivo de Excel en un objeto de libro de trabajo. Esto le permite manipular los datos que contiene.

```csharp
// Cargar el archivo fuente Excel Xlsb
Workbook wb = new Workbook(sourceDir + "sampleExternalConnection_XLSB.xlsb");
```

 Sólo asegúrese de que su archivo XLSB esté ubicado en el lugar especificado.`sourceDir`¡Si la ruta es correcta, su libro de trabajo estará listo para ser manipulado!

## Paso 3: Acceder a las conexiones externas

Con el libro de trabajo cargado, puedes acceder a sus conexiones externas. En nuestro caso, recuperaremos la primera conexión a la base de datos.

```csharp
// Lea la primera conexión externa que en realidad es una conexión DB
Aspose.Cells.ExternalConnections.DBConnection dbCon = wb.DataConnections[0] as Aspose.Cells.ExternalConnections.DBConnection;
```

 Aquí,`DataConnections[0]` Se refiere a la primera conexión en el libro de trabajo. Lo estamos convirtiendo en un`DBConnection` tipo para una mayor manipulación.

## Paso 4: Extraer información de conexión

Ahora que tienes acceso a la conexión de la base de datos, extraigamos e imprimamos sus detalles en la consola. Esto nos ayudará a ver exactamente con qué estamos trabajando.

```csharp
// Imprima el nombre, el comando y la información de conexión de la conexión a la base de datos
Console.WriteLine("Connection Name: " + dbCon.Name);
Console.WriteLine("Command: " + dbCon.Command);
Console.WriteLine("Connection Info: " + dbCon.ConnectionInfo);
```

Este paso le permite verificar el estado actual de su conexión externa. Verá el nombre de la conexión, el comando utilizado y la información de conexión impresa en la consola.

## Paso 5: Modificar la conexión

A veces, un cambio de nombre es todo lo que se necesita para que todo quede más claro o para que coincida con las nuevas convenciones de nomenclatura. Cambiemos el nombre de la conexión existente por algo más relevante.

```csharp
// Modificar el nombre de la conexión
dbCon.Name = "NewCust";
```

Esta línea de código cambia el nombre original de la conexión a "NewCust". ¡Es un cambio simple pero impactante!

## Paso 6: Guarda los cambios

Después de realizar modificaciones, deberá guardar los cambios en el archivo XLSB. A continuación, le indicamos cómo hacerlo:

```csharp
// Guardar el archivo Excel Xlsb
wb.Save(outputDir + "outputExternalConnection_XLSB.xlsb");
```

Esta línea de código guarda el libro de trabajo actualizado y conserva todos los cambios, incluido el nuevo nombre de conexión.

## Paso 7: Confirmar la ejecución

Finalmente, confirmemos que todo ha funcionado sin problemas. Un mensaje sencillo al final lo dejará claro.

```csharp
Console.WriteLine("ReadAndWriteExternalConnectionOfXLSBFile executed successfully.\r\n");
```

Este mensaje le asegurará que su código se ejecutó correctamente y que todos los cambios se guardaron como se esperaba.

## Conclusión

¡Y ya está! Aprendió a leer y escribir conexiones externas en archivos XLSB con Aspose.Cells para .NET. Si sigue estos pasos, podrá administrar de manera eficaz las conexiones de datos de Excel, lo que hará que su trabajo con Excel sea mucho más ágil y menos frustrante. Recuerde que, ya sea que esté manejando conjuntos de datos extensos o simplemente organizando su información, Aspose.Cells tiene las herramientas que necesita.

## Preguntas frecuentes

### ¿Qué es un archivo XLSB?  
Un archivo XLSB es un formato de archivo binario de Excel que almacena datos de hojas de cálculo en formato binario, lo que las hace más compactas y más rápidas de abrir.

### ¿Cómo instalo Aspose.Cells para .NET?  
 Puedes descargarlo fácilmente desde el sitio web de Aspose[aquí](https://releases.aspose.com/cells/net/).

### ¿Puedo utilizar Aspose.Cells gratis?  
 ¡Sí! Puedes empezar con una prueba gratuita, que está disponible[aquí](https://releases.aspose.com/).

### ¿Aspose.Cells admite otros formatos de archivo?  
¡Por supuesto! Aspose.Cells admite una variedad de formatos de archivo, incluidos XLSX, CSV y más.

### ¿Dónde puedo buscar ayuda si tengo problemas?  
Puede obtener ayuda en los foros de Aspose[aquí](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
