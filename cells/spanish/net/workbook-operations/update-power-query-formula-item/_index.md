---
title: Actualizar el elemento de fórmula de Power Query en el libro de trabajo
linktitle: Actualizar el elemento de fórmula de Power Query en el libro de trabajo
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a actualizar fórmulas de Power Query en Excel con Aspose.Cells para .NET en esta completa guía paso a paso.
weight: 27
url: /es/net/workbook-operations/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Actualizar el elemento de fórmula de Power Query en el libro de trabajo

## Introducción
Comprender cómo administrar datos de manera eficiente con Power Query en Excel es fundamental para cualquier analista de datos o entusiasta de Excel. Si alguna vez necesitó actualizar los elementos de fórmula en su libro de Power Query, está en el lugar correcto. Esta guía está diseñada para ayudarlo a aprender a usar Aspose.Cells para .NET para actualizar sin problemas las fórmulas de Power Query en un libro de Excel. Con unos pocos pasos simples, podrá manipular y optimizar sus datos, lo que garantizará que sus libros de trabajo permanezcan dinámicos y centralizados.
## Prerrequisitos
Antes de comenzar a profundizar en el código de ejemplo y los pasos, repasemos lo que necesitará:
1. Comprensión básica de C# y .NET: la familiaridad con los conceptos de programación en C# será beneficiosa ya que escribiremos algo de código.
2.  Instalar Aspose.Cells para .NET: Debe tener la biblioteca Aspose.Cells integrada en su proyecto .NET. Puede descargarla[aquí](https://releases.aspose.com/cells/net/).
3. Un archivo de Excel listo para modificar: asegúrese de tener un archivo de Excel que contenga una consulta de Power Query que desee actualizar. Debe tener un libro de trabajo de muestra como`SamplePowerQueryFormula.xlsx` A su disposición.
## Importar paquetes
Para comenzar, asegúrese de tener los siguientes espacios de nombres incluidos en su archivo C#:
```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```
Esto le permitirá acceder a las funcionalidades proporcionadas por la biblioteca Aspose.Cells, particularmente para trabajar con libros de trabajo y datos de Power Query.
## Paso 1: Configura tus directorios de trabajo
Lo primero es lo primero: debes definir dónde se encuentran los archivos de origen y de salida. 
```csharp
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
```
 En este paso, se especifican las rutas de directorio. Reemplazar`"Your Document Directory"` con la ruta real donde se guardan los archivos de Excel. Esto le indica al programa dónde buscar el archivo de origen y dónde guardar el archivo actualizado.
## Paso 2: Cargue el libro de trabajo
Ahora que ya tiene configurados sus directorios de trabajo, el siguiente paso es cargar su archivo Excel en el programa.
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 Aquí creas un`Workbook` objeto que carga el archivo Excel especificado.`Workbook`La clase es parte de la biblioteca Aspose.Cells y es esencial para cualquier operación que realice en ese archivo de Excel.
## Paso 3: Acceda a los datos de Power Query
Una vez cargado el libro de trabajo, es momento de acceder a las fórmulas de Power Query almacenadas en él.
```csharp
DataMashup mashupData = workbook.DataMashup;
```
 En esta línea, la`DataMashup` La propiedad ayuda a acceder a las estructuras de datos de Power Query dentro del libro de trabajo. Esta propiedad le brinda la capacidad de interactuar con varios aspectos de los datos de Power Query contenidos en su archivo de Excel.
## Paso 4: Recorrer las fórmulas de Power Query
Con los datos de Power Query accesibles, el siguiente paso es iterar a través de cada una de las fórmulas presentes.
```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```
 Aquí es donde ocurre la magia. Recorremos cada uno de los pasos.`PowerQueryFormula` y luego a través de cada uno`PowerQueryFormulaItem` . El`if` La declaración busca el elemento de fórmula denominado "Fuente" y actualiza su valor para que sea la ruta del archivo de origen al que desea que Power Query haga referencia. Esto le permite cambiar dinámicamente de qué archivo extrae datos Power Query.
## Paso 5: Guardar el libro de trabajo actualizado
Después de actualizar los elementos de fórmula necesarios, el paso final es guardar el libro de trabajo.
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
Esta línea guarda el libro de trabajo modificado en un nuevo archivo, preservando así el original y permitiéndole trabajar con la versión actualizada.
## Paso 6: Mensaje de confirmación
Por último, es una buena práctica comprobar si el código se ha ejecutado correctamente.
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
Este simple mensaje le confirmará en la consola que su operación fue exitosa, proporcionándole un final tranquilizador al proceso.
## Conclusión
¡Y ya está! La actualización de los elementos de fórmula de Power Query en Excel con Aspose.Cells para .NET se puede realizar en tan solo unos sencillos pasos. Si sigue esta guía, podrá administrar de manera eficiente sus conexiones de datos de Excel y mantener sus libros de trabajo funcionando sin problemas. Ya sea que sea un profesional experimentado o recién esté comenzando con la manipulación de datos, Aspose.Cells ofrece una forma poderosa de automatizar y mejorar los flujos de trabajo de Excel. 
## Preguntas frecuentes
### ¿Puedo usar Aspose.Cells con cualquier versión de .NET?
Aspose.Cells es compatible con múltiples versiones de .NET, incluidos .NET Framework y .NET Core.
### ¿Aspose.Cells es de uso gratuito?
 Aspose.Cells ofrece una prueba gratuita, pero para un uso continuo se requiere una licencia. Puede obtener una licencia temporal[aquí](https://purchase.aspose.com/temporary-license/).
### ¿Qué pasa si mi archivo de Excel existente no tiene Power Query?
El proceso descrito se centra en actualizar los elementos de Power Query, por lo que si su archivo no los tiene, primero deberá incorporar Power Queries.
### ¿Dónde puedo encontrar más información sobre Aspose.Cells?
 Consulte la documentación para obtener instrucciones y ejemplos completos. Visite el sitio[documentación](https://reference.aspose.com/cells/net/).
### ¿Cómo puedo informar errores o problemas con Aspose.Cells?
Puede comunicarse con su foro de soporte para obtener ayuda sobre cualquier problema que encuentre.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
