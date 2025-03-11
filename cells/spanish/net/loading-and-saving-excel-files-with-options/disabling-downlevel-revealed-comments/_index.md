---
title: Deshabilitar comentarios revelados de nivel inferior al guardar en HTML
linktitle: Deshabilitar comentarios revelados de nivel inferior al guardar en HTML
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda cómo deshabilitar los comentarios revelados de nivel inferior al guardar un libro de Excel en HTML usando Aspose.Cells para .NET con esta guía detallada paso a paso.
weight: 11
url: /es/net/loading-and-saving-excel-files-with-options/disabling-downlevel-revealed-comments/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Deshabilitar comentarios revelados de nivel inferior al guardar en HTML

## Introducción
¿Alguna vez ha tenido que convertir un libro de Excel a HTML y ha querido asegurarse de que no se revelen comentarios innecesarios ni contenido oculto durante el proceso? En este caso, resulta útil desactivar los comentarios revelados de nivel inferior. Si utiliza Aspose.Cells para .NET, tiene control total sobre cómo se representan sus libros de Excel como archivos HTML. En este tutorial, le guiaremos a través de una sencilla guía paso a paso para ayudarle a desactivar los comentarios revelados de nivel inferior al guardar un libro de Excel en HTML. 
Al final de este artículo, comprenderá claramente cómo utilizar esta función y se asegurará de que su salida HTML esté limpia y sin comentarios.
## Prerrequisitos
Antes de sumergirnos en la guía paso a paso, cubramos algunas cosas que necesitará tener en cuenta para seguirla sin problemas:
1. Aspose.Cells para .NET: Necesitará tener instalada la biblioteca Aspose.Cells. Si aún no la ha instalado, puede descargarla[aquí](https://releases.aspose.com/cells/net/).
2. IDE: Un entorno de desarrollo como Visual Studio para escribir y ejecutar su código C#.
3. Conocimientos básicos de C#: la familiaridad con la sintaxis de C# y la programación orientada a objetos le ayudará a seguir el código.
4.  Versión temporal o con licencia: puede utilizar la versión de prueba gratuita o solicitar una licencia temporal desde[aquí](https://purchase.aspose.com/temporary-license/)Esto garantiza que la biblioteca funcione sin limitaciones.
¡Ahora que estás listo, comencemos!
## Importar espacios de nombres
Antes de comenzar con los ejemplos de código, es fundamental incluir los espacios de nombres necesarios para Aspose.Cells. Sin ellos, el código no podrá acceder a los métodos y propiedades necesarios para manipular archivos de Excel.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Asegúrese de colocar esta línea en la parte superior de su archivo C# para importar el espacio de nombres Aspose.Cells.
## Paso 1: Configurar las rutas del directorio
Antes de nada, debemos configurar el directorio de origen (donde se almacena el archivo de Excel) y el directorio de salida (donde se guardará el archivo HTML). Esto es crucial porque Aspose.Cells requiere las rutas de archivo exactas para acceder a los archivos y guardarlos.
```csharp
// Directorio de origen donde se encuentra su archivo Excel
string sourceDir = "Your Document Directory";
// Directorio de salida donde se guardará el archivo HTML resultante
string outputDir = "Your Document Directory";
```
 En este paso, reemplace`"Your Document Directory"` con las rutas de archivo actuales en su sistema. También puede crear directorios personalizados para organizar mejor sus archivos de entrada y salida.
## Paso 2: Cargue el libro de trabajo de Excel
 En este paso, cargaremos el libro de Excel en la memoria para poder manipularlo. Para fines de demostración, utilizaremos un archivo de muestra llamado`"sampleDisableDownlevelRevealedComments.xlsx"`Puedes utilizar cualquier libro de trabajo que prefieras.
```csharp
// Cargue el libro de trabajo de muestra desde el directorio de origen
Workbook wb = new Workbook(sourceDir + "sampleDisableDownlevelRevealedComments.xlsx");
```
Esto crea un objeto de libro de trabajo que contiene todos los datos y la estructura de su archivo de Excel. Desde aquí, puede modificarlo, aplicarle configuraciones y, por último, guardarlo en un formato diferente.
## Paso 3: Configurar las opciones de guardado de HTML
Ahora, debemos configurar el objeto HtmlSaveOptions para desactivar los comentarios revelados de nivel inferior. Esta opción garantiza que ningún comentario o contenido oculto se revele en el archivo HTML resultante.
```csharp
// Cree un nuevo objeto HtmlSaveOptions para configurar las opciones de guardado
HtmlSaveOptions opts = new HtmlSaveOptions();
// Deshabilitar los comentarios revelados de nivel inferior
opts.DisableDownlevelRevealedComments = true;
```
 Mediante la configuración`DisableDownlevelRevealedComments` a`true`, te aseguras de que cuando guardes el libro como un archivo HTML, se deshabilitarán todos los comentarios de nivel inferior.
## Paso 4: Guardar el libro de trabajo como HTML
Una vez configurado el objeto HtmlSaveOptions, el siguiente paso es guardar el libro de trabajo en formato HTML utilizando las opciones especificadas. Aquí es donde se produce la conversión del archivo propiamente dicha.
```csharp
// Guarde el libro de trabajo como un archivo HTML con las opciones de guardado especificadas
wb.Save(outputDir + "outputDisableDownlevelRevealedComments_true.html", opts);
```
En esta línea de código, guardamos el libro de trabajo en el directorio de salida que especificó anteriormente y aplicamos la configuración DisableDownlevelRevealedComments. El resultado será un archivo HTML limpio sin comentarios no deseados.
## Paso 5: Verificar y ejecutar
Por último, para garantizar que todo funcionó como se esperaba, puedes enviar un mensaje de éxito a la consola.
```csharp
// Enviar un mensaje de éxito a la consola
Console.WriteLine("DisableDownlevelRevealedCommentsWhileSavingToHTML executed successfully.");
```
Esto le permite saber que la operación se completó sin errores.
## Conclusión
¡Y ya está! Aprendió a desactivar los comentarios revelados de nivel inferior al guardar un libro de Excel en formato HTML con Aspose.Cells para .NET. Con esta función, ahora puede controlar cómo se representan sus libros de trabajo en formato HTML y evitar revelar contenido innecesario. Ya sea que esté desarrollando una aplicación web o simplemente necesite una salida HTML limpia, este método garantiza que las conversiones de sus libros de trabajo sean precisas y seguras.
Si este tutorial le resultó útil, considere explorar otras características de Aspose.Cells para mejorar aún más sus capacidades de procesamiento de Excel.
## Preguntas frecuentes
### ¿Qué son los comentarios revelados de nivel inferior?
Los comentarios revelados de nivel inferior se utilizan normalmente en el desarrollo web para proporcionar información adicional a los navegadores más antiguos que no admiten determinadas funciones HTML. En las conversiones de Excel a HTML, a veces pueden revelar contenido o comentarios ocultos, por lo que deshabilitarlos puede resultar útil.
### ¿Puedo habilitar comentarios de nivel inferior si los necesito?
 Sí, simplemente configure el`DisableDownlevelRevealedComments` propiedad a`false` Si desea habilitar comentarios de nivel inferior al guardar su libro de trabajo como HTML.
### ¿Cómo obtengo una licencia temporal para Aspose.Cells?
 Puede solicitar fácilmente una licencia temporal visitando el sitio[Sitio web de Aspose](https://purchase.aspose.com/temporary-license/).
### ¿Deshabilitar los comentarios de nivel inferior afecta la apariencia del HTML?
No, deshabilitar los comentarios revelados de nivel inferior no afecta la apariencia visual de la salida HTML. Solo evita la exposición de información adicional destinada a navegadores más antiguos.
### ¿Puedo guardar el libro de trabajo en otros formatos además de HTML?
 Sí, Aspose.Cells admite una variedad de formatos de salida, como PDF, CSV y TXT. Puede explorar más opciones en la[documentación](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
