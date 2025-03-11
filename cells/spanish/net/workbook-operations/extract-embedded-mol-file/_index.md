---
title: Extraer archivo Mol integrado del libro de trabajo
linktitle: Extraer archivo Mol integrado del libro de trabajo
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a extraer archivos MOL incrustados de libros de Excel usando Aspose.Cells para .NET en este detallado tutorial paso a paso.
weight: 18
url: /es/net/workbook-operations/extract-embedded-mol-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraer archivo Mol integrado del libro de trabajo

## Introducción
Cuando se trata de administrar datos dentro de los libros de Excel, a veces se encuentran varios objetos incrustados que no están en un formato estándar. Uno de esos formatos es el MOL (Archivo de Estructura Molecular), que se usa comúnmente en química para representar información molecular. Si está buscando extraer estos archivos MOL de un libro de Excel con Aspose.Cells para .NET, ha llegado a la guía correcta. En este artículo, lo guiaremos a través del proceso paso a paso, desmitificando cada parte a lo largo del camino.
## Prerrequisitos
Antes de sumergirse en el código, es fundamental asegurarse de que se tienen las habilidades y herramientas necesarias. Esto es lo que se necesita:
1. Comprensión básica de la programación .NET: debe estar familiarizado con C# y el marco .NET.
2.  Aspose.Cells para .NET: Asegúrese de tener la biblioteca Aspose.Cells. Puede[Descárgalo aquí](https://releases.aspose.com/cells/net/).
3. Un IDE: puede utilizar Visual Studio o cualquier otro IDE compatible con .NET.
4. Libro de trabajo de Excel con archivos MOL integrados: para este tutorial, necesita un archivo de Excel que contenga objetos MOL. Puede crear uno propio o usar cualquier archivo de muestra.
## Importar paquetes
Para comenzar, deberá importar los espacios de nombres necesarios en su proyecto. Esto es fundamental para acceder a las funcionalidades de Aspose.Cells. A continuación, le indicamos cómo hacerlo:

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

Estos espacios de nombres le permitirán manipular libros de trabajo, acceder a hojas de trabajo y trabajar con archivos en general.
Ahora que hemos resuelto nuestros requisitos previos, profundicemos en el código y comprendamos cada paso involucrado en la extracción de archivos MOL integrados de un libro de Excel. 
## Paso 1: Configuración de sus directorios
El primer paso es definir dónde se encuentra el documento de origen y dónde desea guardar los archivos MOL extraídos. Vamos a configurar esos directorios.
```csharp
string SourceDir = "Your Document Directory"; // Reemplazar con la ruta de su directorio
string outputDir = "Your Document Directory"; // Reemplazar con su ruta de salida
```
 Aquí, reemplaza`"Your Document Directory"`con la ruta a los directorios actuales. Es importante que tanto los directorios de origen como los de salida sean accesibles para la aplicación.
## Paso 2: Cargar el libro de trabajo
Una vez que hayas configurado los directorios, la siguiente tarea es cargar el libro de Excel. Hagámoslo ahora.

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

 Estamos creando una instancia de la`Workbook` clase y pasar la ruta a nuestro archivo Excel llamado`EmbeddedMolSample.xlsx`Este paso inicializa el libro de trabajo y le permite acceder a su contenido.
## Paso 3: Iteración sobre las hojas de trabajo
Ahora que el libro de trabajo está cargado, debe recorrer cada hoja de trabajo dentro del libro de trabajo. Esto le permite examinar cada hoja en busca de objetos incrustados.

```csharp
var index = 1; // Se utiliza para nombrar archivos MOL extraídos
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // Aquí va más lógica de extracción
}
```

 Aquí estás usando un`foreach` para navegar por las hojas de trabajo. Para cada hoja de trabajo, se accede a la`OleObjects` colección, que contiene todos los objetos incrustados.
## Paso 4: Extracción de archivos MOL
Ahora viene la parte crítica: extraer los archivos MOL de los objetos OLE. Para ello es necesario ejecutar otro bucle dentro del bucle de la hoja de cálculo.

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

 Para cada objeto OLE que haya encontrado, está creando un nuevo archivo en el directorio de salida.`ObjectData` propiedad de la`OleObject` contiene los datos del objeto incrustado, que escribe en un archivo recién creado mediante un`FileStream`El archivo se nombra secuencialmente (`OleObject1.mol`, `OleObject2.mol` , etc.) basado en el`index` variable.
## Paso 5: Confirmación de finalización del proceso
Finalmente, una vez que se hayan extraído todos los archivos MOL, es una buena práctica informar al usuario que el proceso se ha completado con éxito.

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

Esta línea simplemente imprime un mensaje en la consola para informarle que la extracción se realizó correctamente. Es un buen detalle para recibir comentarios de los usuarios.
## Conclusión
¡Y ya está! Ha extraído con éxito archivos MOL incrustados de un libro de Excel con Aspose.Cells para .NET. Este proceso integra algunos pasos básicos, lo que garantiza un enfoque estructurado para manejar objetos incrustados. Ya sea que trabaje en investigación científica, análisis químicos o simplemente trabaje con conjuntos de datos complejos, poder extraer y manipular estos tipos de archivos puede marcar una diferencia significativa en la forma en que administra su información. 
## Preguntas frecuentes
### ¿Puedo extraer otros tipos de archivos además de MOL de Excel?
Sí, puedes extraer varios otros tipos de archivos incrustados con técnicas similares.
### ¿Aspose.Cells es de uso gratuito?
 Aspose.Cells es una biblioteca comercial, pero puedes[Pruébelo gratis por un período limitado](https://releases.aspose.com/).
### ¿Este método funciona con todas las versiones de Excel?
Sí, siempre que el formato de archivo sea compatible con Aspose.Cells.
### ¿Puedo automatizar este proceso de extracción?
¡Por supuesto! Puedes automatizar este proceso colocando el código en una tarea programada o en un script.
### ¿Dónde puedo encontrar más documentación sobre Aspose.Cells?
 Puedes consultar el[Documentación de Aspose.Cells](https://reference.aspose.com/cells/net/) para más detalles y ejemplos.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
