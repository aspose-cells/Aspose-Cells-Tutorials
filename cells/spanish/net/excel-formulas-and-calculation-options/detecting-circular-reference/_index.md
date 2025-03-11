---
title: Detección de referencias circulares en Excel mediante programación
linktitle: Detección de referencias circulares en Excel mediante programación
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Detecte fácilmente referencias circulares en Excel con Aspose.Cells para .NET. Siga nuestra guía paso a paso para garantizar cálculos precisos en sus hojas de cálculo.
weight: 13
url: /es/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Detección de referencias circulares en Excel mediante programación

## Introducción
Cuando se trata de trabajar con archivos de Excel, uno de los problemas más frustrantes que puede encontrar es una referencia circular. Esto sucede cuando una fórmula hace referencia a su propia celda, ya sea directa o indirectamente, creando un bucle que puede confundir al motor de cálculo de Excel. ¡Pero no tema! Con Aspose.Cells para .NET, puede detectar programáticamente estas molestas referencias circulares, lo que garantiza que sus hojas de cálculo sigan siendo funcionales y precisas. En esta guía, lo guiaremos a través del proceso paso a paso, haciéndolo muy fácil.
## Prerrequisitos
Antes de sumergirnos en los detalles de la detección de referencias circulares, asegurémonos de que tienes todo lo que necesitas para comenzar:
1. Visual Studio: Asegúrate de tener Visual Studio instalado en tu equipo. Este será tu entorno de desarrollo.
2. .NET Framework: asegúrese de estar utilizando una versión compatible de .NET Framework (al menos .NET Framework 4.0).
3.  Biblioteca Aspose.Cells: Necesita tener la biblioteca Aspose.Cells. Puede descargarla desde[Sitio web de Aspose](https://releases.aspose.com/cells/net/).
4. Conocimientos básicos de C#: será beneficioso estar familiarizado con la programación en C#, ya que escribiremos código en este lenguaje.
5. Archivo de Excel: tenga listo un archivo de Excel que contenga referencias circulares para realizar pruebas. Puede crear uno simple o descargar una muestra.
Ahora que tenemos nuestros requisitos previos establecidos, ¡pasemos a la parte divertida!
## Importar paquetes
Antes de comenzar a codificar, debes importar los paquetes necesarios. A continuación, te indicamos cómo hacerlo:
### Crear un nuevo proyecto
- Abra Visual Studio y cree un nuevo proyecto de aplicación de consola C#.
### Añadir referencia de Aspose.Cells
- Haga clic derecho en su proyecto en el Explorador de soluciones.
- Seleccione "Administrar paquetes NuGet".
- Busque “Aspose.Cells” e instale la última versión.
### Importar espacios de nombres requeridos
 En la parte superior de tu`Program.cs` archivo, importe los espacios de nombres necesarios:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ahora que tenemos todo configurado, profundicemos en el código para detectar referencias circulares en un archivo Excel.
## Paso 1: Definir el directorio de entrada
Primero, debes especificar el directorio donde se encuentra tu archivo de Excel. Aquí es donde cargarás tu archivo de Excel.
```csharp
// Directorio de entrada
string sourceDir = "Your Document Directory";
```
 Reemplazar`"Your Document Directory"` con la ruta real a su archivo Excel.
## Paso 2: Cargue el libro de trabajo con LoadOptions
A continuación, cargará su libro de Excel. ¡Aquí es donde comienza la magia!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
 Aquí, estamos creando una nueva instancia de`LoadOptions` y cargar el libro de trabajo desde la ruta especificada. ¡Asegúrese de que el nombre del archivo de Excel coincida!
## Paso 3: Habilitar la configuración de iteración
Para permitir referencias circulares, debe habilitar la configuración de iteración en el libro de trabajo.
```csharp
objWB.Settings.Iteration = true;
```
Esto le dice a Aspose.Cells que permita referencias circulares durante el cálculo.
## Paso 4: Crear opciones de cálculo y monitor circular
Ahora, vamos a crear las opciones de cálculo y nuestro monitor circular personalizado.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
 Aquí, estamos creando una instancia de`CalculationOptions` y una costumbre`CircularMonitor`Este monitor ayudará a rastrear cualquier referencia circular encontrada durante los cálculos.
## Paso 5: Calcular las fórmulas
Ahora es el momento de calcular las fórmulas en tu libro de trabajo.
```csharp
objWB.CalculateFormula(copts);
```
Esta línea ejecuta el cálculo y verifica si hay referencias circulares.
## Paso 6: Contar las referencias circulares
Después del cálculo, puedes contar cuántas referencias circulares se encontraron.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Esto generará el número de referencias circulares detectadas en su archivo Excel.
## Paso 7: Mostrar resultados
Finalmente, mostremos los resultados y confirmemos que nuestro método se ejecutó correctamente.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Paso 8: Implementar la clase CircularMonitor
 Para completar el proceso, deberá implementar el`CircularMonitor` Clase. Esta clase heredará de`AbstractCalculationMonitor` y manejar la detección de referencias circulares.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
Esta clase captura los detalles de cada referencia circular encontrada, incluido el nombre de la hoja de trabajo y el índice de celda.
## Conclusión
Detectar referencias circulares en Excel con Aspose.Cells para .NET es un proceso sencillo una vez que lo divide en pasos manejables. Si sigue esta guía, podrá identificar y manejar fácilmente las referencias circulares en sus hojas de cálculo, lo que garantizará que sus cálculos sigan siendo precisos y confiables. Ya sea que sea un desarrollador experimentado o recién esté comenzando, Aspose.Cells le brinda herramientas poderosas para mejorar sus capacidades de manipulación de Excel. 
## Preguntas frecuentes
### ¿Qué es una referencia circular en Excel?
Una referencia circular ocurre cuando una fórmula hace referencia a su propia celda, lo que provoca un bucle infinito en los cálculos.
### ¿Cómo puedo detectar referencias circulares mediante programación?
Puede utilizar la biblioteca Aspose.Cells en .NET para detectar programáticamente referencias circulares implementando un monitor de cálculo personalizado.
### ¿Cuáles son los requisitos previos para utilizar Aspose.Cells?
Necesita tener instalados Visual Studio, .NET Framework y la biblioteca Aspose.Cells.
### ¿Puedo utilizar Aspose.Cells gratis?
Sí, Aspose.Cells ofrece una prueba gratuita que puedes usar para explorar sus funciones.
### ¿Dónde puedo encontrar más información sobre Aspose.Cells?
 Puedes visitar el[Documentación de Aspose.Cells](https://reference.aspose.com/cells/net/) para obtener información detallada y ejemplos.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
