---
title: Uso de formatos numéricos integrados en Excel mediante programación
linktitle: Uso de formatos numéricos integrados en Excel mediante programación
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Automatice el formato de números en Excel con Aspose.Cells para .NET. Aprenda a aplicar formatos de fecha, porcentaje y moneda mediante programación.
weight: 10
url: /es/net/number-and-display-formats-in-excel/using-built-in-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uso de formatos numéricos integrados en Excel mediante programación

## Introducción
En este tutorial, le explicaremos cómo usar los formatos de números integrados en Excel con Aspose.Cells para .NET. Cubriremos todo, desde la configuración de su entorno hasta la aplicación de diferentes formatos, como fechas, porcentajes y monedas. Ya sea que sea un profesional experimentado o que recién esté incursionando en el ecosistema .NET, esta guía le permitirá formatear celdas de Excel en un abrir y cerrar de ojos.
## Prerrequisitos
Antes de sumergirte, asegúrate de tener lo siguiente:
-  Se instaló la biblioteca Aspose.Cells para .NET. Puede[Descárgalo aquí](https://releases.aspose.com/cells/net/).
- Un conocimiento práctico de C# y programación básica .NET.
- Visual Studio o cualquier IDE .NET instalado en su máquina.
-  Una licencia Aspose válida o[licencia temporal](https://purchase.aspose.com/temporary-license/).
- .NET framework instalado (versión 4.0 o superior).
  
Si no tienes ninguno de los elementos anteriores, sigue los enlaces que te proporcionamos para configurar todo. ¿Estás listo? ¡Pasemos a la parte divertida!
## Importar paquetes
Antes de comenzar con el tutorial, asegúrese de importar los espacios de nombres necesarios para trabajar con Aspose.Cells para .NET:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Una vez que hayas importado estos datos, ya estarás listo para manipular archivos de Excel mediante programación. ¡Ahora, profundicemos en la guía paso a paso!
## Paso 1: Cree o acceda a su libro de trabajo de Excel
En este paso, creará un nuevo libro de trabajo. Piense en esto como si estuviera abriendo un nuevo archivo de Excel, ¡excepto que lo está haciendo mediante código!
```csharp
// La ruta al directorio de documentos.
string dataDir = "Your Document Directory";
// Crear directorio si aún no está presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Creación de una instancia de un objeto Workbook
Workbook workbook = new Workbook();
```
 Aquí, simplemente estamos instanciando una nueva`Workbook` objeto. Este actúa como su archivo de Excel, listo para la manipulación de datos. También puede cargar un archivo existente proporcionando su ruta.
## Paso 2: Acceda a la hoja de trabajo
Los libros de Excel pueden contener varias hojas de cálculo. En este paso, accederemos a la primera hoja de cálculo de su libro:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Ahora estamos accediendo a la primera hoja de cálculo del libro. Si necesita manipular hojas adicionales, puede hacer referencia a ellas mediante su índice o nombre.
## Paso 3: Agregar datos a las celdas
Comencemos a agregar algunos datos a celdas específicas. Primero, insertaremos la fecha actual del sistema en la celda "A1":
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Esta línea inserta la fecha actual en la celda A1. ¡Genial, verdad? Imagina hacer esto manualmente para cientos de celdas; sería una pesadilla. ¡Ahora, pasaremos al formato!
## Paso 4: Formatear la fecha en la celda "A1"
A continuación, formateemos esa fecha en un formato más legible, como "15-Oct-24". Aquí es donde realmente destaca Aspose.Cells:
1. Recuperar el estilo de la celda:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Aquí, tomamos el estilo de la celda A1. Piense en esto como tomar el "estilo" de la celda antes de hacer cualquier ajuste.
2. Establezca el formato de fecha:
```csharp
style.Number = 15;
```
 Configuración de la`Number` La propiedad 15 aplica el formato de fecha deseado. Este es un código de formato numérico incorporado para mostrar fechas en el formato "d-mmm-aa".
3. Aplicar el estilo a la celda:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Esta línea aplica los cambios de estilo a la celda. Ahora, en lugar de un formato de fecha predeterminado, verá algo mucho más fácil de usar como "15-Oct-24".
## Paso 5: Agregar y dar formato a un porcentaje en la celda "A2"
Pasemos ahora a dar formato a los porcentajes. Imagina que quieres insertar un valor y mostrarlo como porcentaje. En este paso, agregaremos un valor numérico a la celda "A2" y le daremos formato como porcentaje:
1. Insertar valor numérico:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Esto inserta el número 20 en la celda A2. Es posible que estés pensando: "Es solo un número normal, ¿cómo lo convierto en un porcentaje?". Bueno, estamos a punto de llegar a eso.
2. Recupere el estilo y establezca el formato de porcentaje:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Formato como porcentaje
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Aquí, sumamos 2546 a la celda A3. A continuación, formatearemos este número para que aparezca como moneda.
2. Recupere el estilo y establezca el formato de moneda:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Formato como moneda
worksheet.Cells["A3"].SetStyle(style);
```
 Configuración de la`Number` La propiedad 6 aplica el formato de moneda. Ahora, el valor en la celda A3 se mostrará como "2546,00", con comas y dos decimales.
## Paso 7: Guarde el archivo Excel
Ahora que hemos aplicado toda la magia del formato, es hora de guardar el archivo:
```csharp
// Guardando el archivo Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 Esta línea guarda el archivo de Excel en formato Excel 97-2003. Puede cambiar el formato`SaveFormat`para adaptarlo a sus necesidades. ¡Y así, ya habrá creado y formateado un archivo Excel mediante programación!
## Conclusión
¡Felicitaciones! Aprendió a usar Aspose.Cells para .NET para aplicar formatos de números integrados a las celdas de un archivo de Excel. Desde fechas hasta porcentajes y monedas, cubrimos algunas de las necesidades de formato más comunes para el procesamiento de datos de Excel. Ahora, en lugar de formatear las celdas manualmente, puede automatizar todo el proceso, lo que le permitirá ahorrar tiempo y reducir los errores.
## Preguntas frecuentes
### ¿Puedo aplicar formatos de números personalizados usando Aspose.Cells para .NET?
 ¡Sí! Además de los formatos integrados, Aspose.Cells también admite formatos de números personalizados. Puede crear formatos muy específicos utilizando el`Custom` propiedad en el`Style` clase.
### ¿Cómo puedo formatear una celda como moneda con un símbolo específico?
 Para aplicar un símbolo de moneda específico, puede utilizar un formato personalizado configurando el`Style.Custom` propiedad.
### ¿Puedo formatear filas o columnas enteras?
 ¡Por supuesto! Puedes aplicar estilos a filas o columnas enteras usando el`Rows` o`Columns`colecciones en el`Worksheet` objeto.
### ¿Cómo puedo formatear varias celdas a la vez?
Puedes utilizar el`Range` objeto para seleccionar varias celdas y aplicar estilos a todas ellas a la vez.
### ¿Necesito tener instalado Microsoft Excel para utilizar Aspose.Cells?
No, Aspose.Cells funciona independientemente de Microsoft Excel, por lo que no necesita tener Excel instalado en su máquina.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
