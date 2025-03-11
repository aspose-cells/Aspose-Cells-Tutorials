---
title: Personalización de formatos de visualización con números definidos por el usuario
linktitle: Personalización de formatos de visualización con números definidos por el usuario
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a personalizar los formatos de visualización con Aspose.Cells para .NET. Formatee fechas, porcentajes y monedas con esta guía paso a paso.
weight: 11
url: /es/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Personalización de formatos de visualización con números definidos por el usuario

## Introducción
Trabajar con archivos de Excel a menudo requiere un formato personalizado de las celdas para presentar los datos de una manera más significativa y fácil de usar. Imagina que estás creando un archivo de Excel para un informe. No solo quieres números sin formato. Quieres que las fechas, los porcentajes y las monedas se vean elegantes y profesionales, ¿verdad? Ahí es donde entran en juego los formatos de visualización personalizados. En este tutorial, profundizaremos en Aspose.Cells para .NET para mostrarte cómo personalizar el formato de visualización de números mediante configuraciones definidas por el usuario.
## Prerrequisitos
Antes de comenzar, asegúrate de tener todo listo para seguir este tutorial. Esto es lo que necesitarás:
-  Aspose.Cells para .NET instalado.[Descargalo aquí](https://releases.aspose.com/cells/net/).
- Conocimientos básicos de C# y .NET framework.
-  Una licencia válida para Aspose.Cells. Si no tienes una, consigue una[prueba gratis](https://releases.aspose.com/) o solicitar una[licencia temporal](https://purchase.aspose.com/temporary-license/).
- Un IDE como Visual Studio.
- .NET Framework 4.0 o superior.
 Si te falta algo, no te preocupes. Siempre puedes volver a visitar estos enlaces para descargar los archivos necesarios o buscar ayuda en el sitio web.[Foro de soporte de Aspose](https://forum.aspose.com/c/cells/9).
## Importar espacios de nombres
Antes de saltar al código, debe importar los espacios de nombres necesarios para acceder a todas las funcionalidades necesarias de Aspose.Cells.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Estos dos espacios de nombres serán las herramientas principales de este tutorial. Ahora, pasemos a la parte divertida:
## Paso 1: Configuración del directorio del proyecto
Primero, necesitas un lugar para almacenar tus archivos, ¿cierto? Vamos a crear un directorio para guardar el archivo de Excel resultante. En este paso, también nos aseguraremos de que el directorio exista antes de guardar nada.
```csharp
// La ruta al directorio de documentos.
string dataDir = "Your Document Directory";
// Crear directorio si aún no está presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
-  Estamos definiendo una`dataDir` variable para almacenar la ruta donde irá el archivo de salida Excel.
-  Luego verificamos si el directorio existe usando`System.IO.Directory.Exists()`.
-  Si el directorio no existe, se creará utilizando`System.IO.Directory.CreateDirectory()`.
## Paso 2: Crear un nuevo libro de trabajo y agregar una hoja de trabajo
Ahora que tenemos nuestro directorio, creemos un nuevo libro de Excel y agreguemos una hoja de cálculo.
```csharp
// Creación de una instancia de un objeto Workbook
Workbook workbook = new Workbook();
// Agregar una nueva hoja de cálculo al objeto de Excel
int i = workbook.Worksheets.Add();
// Obtener la referencia de la hoja de trabajo recién agregada pasando su índice de hoja
Worksheet worksheet = workbook.Worksheets[i];
```
-  Primero, creamos un nuevo`Workbook` objeto. Piense en esto como su archivo de Excel.
-  Agregamos una nueva hoja de trabajo a este libro de trabajo usando el`Add()`método y almacenar el índice en variable`i`.
-  Hacemos referencia a esta hoja de trabajo utilizando el`workbook.Worksheets[i]`.
## Paso 3: Agregar fecha a una celda y personalizar su formato
 Ahora, insertemos la fecha actual en una celda y formatéela para que se muestre de una manera personalizada. En lugar del formato de fecha predeterminado, estableceremos un formato personalizado como`d-mmm-yy`.
```csharp
// Agregar la fecha actual del sistema a la celda "A1"
worksheet.Cells["A1"].PutValue(DateTime.Now);
// Obteniendo el estilo de la celda A1
Style style = worksheet.Cells["A1"].GetStyle();
// Establecer el formato de visualización personalizado para mostrar la fecha como "d-mmm-aa"
style.Custom = "d-mmm-yy";
// Aplicar el estilo a la celda A1
worksheet.Cells["A1"].SetStyle(style);
```
-  Agregamos la fecha actual del sistema a la celda`A1` usando`PutValue(DateTime.Now)`.
-  Recuperamos el estilo actual de celda.`A1` usando`GetStyle()`.
-  Modificamos el estilo de la celda estableciendo`style.Custom = "d-mmm-yy"`, que formatea la fecha para mostrar el día, el mes abreviado y el año.
-  Finalmente, aplicamos el nuevo estilo a la celda con`SetStyle()`.
## Paso 4: Dar formato a una celda como porcentaje
 A continuación, trabajemos con números. Agregaremos un valor numérico a otra celda, por ejemplo`A2`y formatéelo como porcentaje.
```csharp
//Agregar un valor numérico a la celda "A2"
worksheet.Cells["A2"].PutValue(20);
// Obteniendo el estilo de la celda A2
style = worksheet.Cells["A2"].GetStyle();
// Configuración del formato de visualización personalizado para mostrar el valor como porcentaje
style.Custom = "0.0%";
// Aplicar el estilo a la celda A2
worksheet.Cells["A2"].SetStyle(style);
```
-  Nosotros agregamos el valor`20` A la celda`A2`.
-  Recuperamos el estilo de celda`A2` y configure el formato personalizado en`0.0%` para mostrar el valor como un porcentaje (es decir, 20%).
-  Por último, aplicamos el estilo a la celda usando`SetStyle()`.
## Paso 5: Dar formato a una celda como moneda
 Agreguemos otro valor, digamos a la celda`A3`y formatearlo para que se muestre como moneda. Para que las cosas sean más interesantes, usaremos un formato que muestre los valores positivos como moneda en libras y los valores negativos como dólares.
```csharp
// Agregar un valor numérico a la celda "A3"
worksheet.Cells["A3"].PutValue(2546);
// Obtener el estilo de una celda A3
style = worksheet.Cells["A3"].GetStyle();
// Configuración del formato de visualización personalizado para mostrar el valor como moneda
style.Custom = "£#,##0;[Red]$-#,##0";
// Aplicar el estilo a una celda A3
worksheet.Cells["A3"].SetStyle(style);
```
-  Nosotros agregamos el valor`2546` A la celda`A3`.
-  Establecemos un formato personalizado`£#,##0;[Red]$-#,##0`, que muestra los valores positivos con un signo de libra y los valores negativos en rojo con un signo de dólar.
- Aplicamos el estilo a la celda usando`SetStyle()`.
## Paso 6: Guardar el libro de trabajo
El paso final es guardar el libro de trabajo como archivo de Excel. Para este tutorial, utilizaremos el formato Excel 97-2003.
```csharp
// Guardando el archivo Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
-  El`Save()` El método guarda el libro de trabajo en el directorio especificado.
-  Nosotros elegimos`SaveFormat.Excel97To2003` para garantizar la compatibilidad con versiones anteriores de Excel.
## Conclusión
¡Y listo! Acabamos de crear un archivo de Excel, agregamos formatos personalizados de fecha, porcentaje y moneda a celdas específicas usando Aspose.Cells para .NET y guardamos el archivo. El formato personalizado hace que sus archivos de Excel sean mucho más legibles y profesionales. No olvide explorar otras opciones de formato en Aspose.Cells, como el formato condicional, para tener aún más control sobre el aspecto de sus datos.
## Preguntas frecuentes
### ¿Cómo puedo aplicar opciones de formato más complejas en Aspose.Cells?
Puede combinar diferentes estilos de formato, como color de fuente, bordes y colores de fondo, con formatos de números personalizados.
### ¿Puedo aplicar un formato de número personalizado a un rango de celdas?
Sí, Aspose.Cells le permite aplicar un estilo a un rango de celdas utilizando el`Range.SetStyle()` método.
### ¿En qué otros formatos de archivo puedo guardar el libro de trabajo?
 Aspose.Cells admite muchos formatos, incluidos XLSX, CSV y PDF. Simplemente cambie el`SaveFormat` en el`Save()` método.
### ¿Puedo formatear números negativos de forma diferente?
¡Por supuesto! Puedes usar formatos de números personalizados para mostrar números negativos con diferentes colores o símbolos.
### ¿Aspose.Cells para .NET es gratuito?
 Aspose.Cells ofrece una prueba gratuita, pero para disfrutar de todas sus funciones, necesitará una licencia válida. Puede obtener una[Licencia temporal aquí](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
