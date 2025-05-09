---
"description": "Aprenda a cambiar los datos de origen de la tabla dinámica mediante programación usando Aspose.Cells para .NET con nuestro completo tutorial paso a paso."
"linktitle": "Cambiar los datos de origen de una tabla dinámica mediante programación en .NET"
"second_title": "API de procesamiento de Excel Aspose.Cells .NET"
"title": "Cambiar los datos de origen de una tabla dinámica mediante programación en .NET"
"url": "/es/net/creating-and-configuring-pivot-tables/changing-source-data/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cambiar los datos de origen de una tabla dinámica mediante programación en .NET

## Introducción
En el mundo del análisis de datos, pocas herramientas brillan tanto como Microsoft Excel. Diariamente, innumerables usuarios dependen de Excel para gestionar y analizar datos, pero en realidad, es mucho más complejo que simplemente hacer clic y arrastrar. Si alguna vez has querido manipular archivos de Excel mediante programación, en concreto, cambiar los datos de origen de una tabla dinámica, ¡estás en el lugar correcto! En esta guía, exploraremos cómo lograrlo con Aspose.Cells para .NET. Tanto si eres un desarrollador experimentado como si apenas estás incursionando en la programación, este tutorial te ofrecerá información valiosa y fácil de seguir.
## Prerrequisitos
Antes de comenzar nuestro viaje para cambiar los datos de origen de una tabla dinámica, asegurémonos de que tenga todo configurado y listo para comenzar:
1. Visual Studio: asegúrese de tener una copia de Microsoft Visual Studio instalada, ya que escribiremos nuestro código aquí.
2. Biblioteca Aspose.Cells: Necesitará tener la biblioteca Aspose.Cells descargada y referenciada en su proyecto. Puede descargarla. [aquí](https://releases.aspose.com/cells/net/).
3. Conocimientos básicos de C#: si bien este tutorial está simplificado, tener una comprensión de C# lo ayudará a comprender mejor el código.
4. Archivo Excel: debe tener un archivo Excel de muestra (como "Book1.xlsx") que contenga una tabla dinámica que podamos manipular.
Muy bien, con estos prerrequisitos en regla, ¡podemos proceder a importar los paquetes necesarios y comenzar a codificar!
## Importar paquetes
Primero lo primero: importemos los paquetes que necesitaremos. Abra su proyecto de C# en Visual Studio y agregue las siguientes directivas using al principio de su archivo de código:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Estos espacios de nombres le darán acceso a las clases esenciales necesarias para trabajar con archivos de Excel y manipular su contenido utilizando Aspose.Cells.

Ahora, desglosemos el proceso en pasos fáciles de seguir. Explicaremos cómo abrir un archivo de Excel, modificar la hoja de cálculo, cambiar la fuente de datos de la tabla dinámica y guardar los resultados.
## Paso 1: Defina su directorio de documentos
Primero, debe especificar dónde se encuentra su archivo de Excel. Modifique el `dataDir` variable para apuntar a la carpeta que contiene su "Book1.xlsx".
```csharp
// La ruta al directorio de documentos.
string dataDir = "Your Document Directory";
```
Esta línea configura el directorio donde se almacena su archivo de Excel, lo que facilita su acceso más adelante.
## Paso 2: Especifique la ruta de entrada
A continuación, creemos una cadena para especificar la ruta completa a su archivo Excel de entrada:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Esto ayuda a agilizar el acceso a sus archivos; no tendrá que escribir la misma ruta varias veces en su código.
## Paso 3: Crear un flujo de archivos
Ahora es el momento de abrir el archivo de Excel. Crearemos un `FileStream` que le permite leer el contenido del archivo Excel:
```csharp
// Creación de un flujo de archivos que contiene el archivo de Excel que se abrirá
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Esta línea abre el archivo en modo lectura, permitiéndonos acceder a sus datos.
## Paso 4: Cargar el libro de trabajo
Con el flujo de archivos en su lugar, el siguiente paso es cargar el libro de trabajo:
```csharp
// Abrir el archivo de Excel a través del flujo de archivos
Workbook workbook = new Workbook(fstream);
```
Este comando toma su archivo de Excel y lo carga en un `Workbook` objeto. Una vez cargado, puede manipular el archivo según sea necesario.
## Paso 5: Acceda a la hoja de trabajo
Es hora de profundizar en los detalles. Accederemos a la primera hoja de cálculo del libro:
```csharp
// Acceder a la primera hoja de cálculo del archivo Excel
Worksheet worksheet = workbook.Worksheets[0];
```
Esto le brinda acceso directo a los datos dentro de la primera hoja de trabajo, lo que facilita su modificación.
## Paso 6: Completar nuevos datos
A continuación, queremos insertar nuevos datos en las celdas. En este ejemplo, agregaremos algunos datos de muestra:
```csharp
// Completar nuevos datos en las celdas de la hoja de cálculo
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
Aquí, ponemos los valores "Golf", "Qtr4" y `7000` en celdas específicas. Puedes cambiar estos valores según tus necesidades.
## Paso 7: Cambiar el rango nombrado
Ahora, cambiaremos el rango con nombre al que hace referencia la tabla dinámica. Esto implica crear o actualizar un rango:
```csharp
// Cambiar el rango con nombre "DataSource"
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Al definir un nuevo rango, nos aseguramos de que la tabla dinámica utilice estos nuevos datos cuando se actualice.
## Paso 8: Guarde el archivo de Excel modificado
Después de todos los cambios, ¡es crucial guardar el trabajo! Guardemos el libro modificado:
```csharp
// Guardar el archivo Excel modificado
workbook.Save(dataDir + "output.xls");
```
Este comando guarda el libro de trabajo en un nuevo archivo, por lo que no sobrescribe el archivo original a menos que lo desee.
## Paso 9: Cerrar el flujo de archivos
Por último, es esencial cerrar el flujo de archivos para liberar cualquier recurso que estés utilizando:
```csharp
// Cerrar el flujo de archivos para liberar todos los recursos
fstream.Close();
```
Este paso garantiza que su aplicación no pierda memoria y se mantenga eficiente.
## Conclusión
¡Felicitaciones! Acaba de cambiar correctamente los datos de origen de una tabla dinámica mediante programación en .NET con Aspose.Cells. Esta funcionalidad abre muchas posibilidades para automatizar tareas de Excel y mejorar su flujo de trabajo. Ya sea que esté actualizando informes financieros, haciendo seguimiento de datos de ventas o simplemente experimentando con conjuntos de datos, poder hacerlo mediante programación le ahorrará mucho tiempo y reducirá el riesgo de errores.

## Preguntas frecuentes
### ¿Qué es Aspose.Cells?
Aspose.Cells es una potente biblioteca .NET para trabajar con archivos de Excel, que permite a los usuarios crear, modificar y manipular documentos de Excel mediante programación.
### ¿Puedo cambiar los datos de origen de las tablas dinámicas existentes utilizando este método?
¡Por supuesto! Este método permite actualizar la fuente de datos de las tablas dinámicas existentes en el libro de Excel.
### ¿Necesito tener Office instalado para utilizar Aspose.Cells?
¡No! Aspose.Cells es una biblioteca independiente, lo que significa que no necesitas tener Microsoft Office instalado para trabajar con archivos de Excel.
### ¿Aspose.Cells es de uso gratuito?
Aspose.Cells ofrece una versión de prueba gratuita, pero para disfrutar de todas sus funciones, deberá adquirir una licencia. Puede encontrar más información. [aquí](https://purchase.aspose.com/buy).
### ¿Dónde puedo encontrar más ejemplos y apoyo?
Para obtener más ejemplos y ayuda, consulte el [Documentación de Aspose.Cells](https://reference.aspose.com/cells/net/) y su foro comunitario [aquí](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}