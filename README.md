## **Contexto del proyecto individual**
Para este proyecto se ha creado un dashboard de ventas que permita responder las siguientes preguntas realizadas por el cliente:

+ Determinar las ventas (Total venta y cantidad).

+ Determinar el total de ventas por mes y su correspondiente variación porcentual.

+ Determinar el total de ventas por departamento del cliente.

+ Determinar el total de ventas por categoría de producto.

+ Determinar el total de ventas por género.

## **Pasos para construir el Dashboard**

  + `Paso 1:` Comprensión de las fuentes de datos y su contenido.

  + `Paso 2:` Realización de la conexión a los datos por medio de Power BI.

  + `Paso 3:` Proceso de limpieza de datos en power query.

      *• Modificación de los nombres de los archivos Excel correspondientes a las ventas de minoristas, transformándolos completamente a letras mayúsculas.*
    
      *• Se aplicó una condición de filtro a las filas de la tabla diciendo que se va a conservar las filas con extensión xslx.*
    
      *•	Se aplicó un filtro para la nomenclatura de aquellos archivos que comiencen con VENTA MINORISTAS, ya que puede haber otro archivo que no necesariamente correspondan a las ventas.*
    
      *•	Conservó las filas en el que el nombre no comienza por este carácter (~)*
    
      *•	Se quitó otras columnas y solo se conservó la columna Content*
    
      *•	Se creo otra columna Datos y ahí se le asigno Content, para eso se usó la fórmula de columna personalizada*

         Datos = Excel.workbook([Content])
    
      *•	Se filtró las columnas de tipo Table.*
    
      *•	Me percate de que no hayga filas vacías.*
    
      *•	Se expandió las tablas de los dos archivos de ventas de los años 2022 y 2023 en un solo archivo.*
    
      *•	Le di el tipo de dato adecuado a cada columna.*
    
      *•	Creo una nueva consulta en lenguaje M, llamada calendario indicando que la fecha empezara con la primera venta y como última fecha con la última venta, para que a posterior cuando se agregue otras ventas se cree una fecha de acuerdo a la venta agregada.*
    

  + `Paso 4:` Creación del modelo de datos.
<img src="https://github.com/Elizabeth02fh/Dashboard_Ventas_Minoristas/blob/8dbfc848ccee8cb35c633323b24bcaba7b66d9bf/MODELO_DATOS.PNG" alt="MODELO_DATOS" width="700">

  + `Paso 5:` Creación de los cálculos necesarios para el reporte.
    
Se realizaron las siguientes Medidas DAX:

     Total Ventas = SUMX( Ventas_Minoristas, Ventas_Minoristas[Precio Unitario]*Ventas_Minoristas[Cantidad])
*

      Total Unidades = SUM( Ventas_Minoristas[Cantidad] )


*

      % Var Mensual Ventas = 
      VAR Ventas_PM = CALCULATE ( [Total Ventas], DATEADD ( Calendario[Fecha], -1, MONTH) ) 
      VAR Variacion = DIVIDE ( [Total Ventas] - Ventas_PM, Ventas_PM, 0 ) 
      RETURN
      IF ( ISBLANK ( Ventas_PM ), 0, Variacion )
*

      Maximo Eje Y Ventas = 
      VAR Tabla = ALLSELECTED ( Calendario[Mes Abreviado], Calendario[Nombre del mes] ) 
      VAR Maximo = MAXX ( Tabla, [Total Ventas] ) 
      VAR Incremento = 1.5
      RETURN
      Maximo * Incremento
*

      Formato dinámico
      """"&FORMAT ([% Var Mensual Ventas], "+0.0%; -0.0%;0.0%")&""""

  + `Paso 5:` Diseño y visualización de los datos.
![DASHBOARD VENTAS MINORISTAS](https://github.com/Elizabeth02fh/Dashboard_Ventas_Minoristas/blob/96b4e5f12ae1ab8f0f3df35c60db1da5dffa1c9e/DASHBOARD%20VENTAS%20MINORISTAS.PNG)

    Interpretación del grafico de TOTAL VENTAS POR MES
    
    *•	Las mayores ventas se otorgaron en el mes de mayo, y las ventas más bajas fueron en el mes de setiembre, y se terminó el año con unas ventas de $43.852 lo que significa un 27.9 % de una variación positiva con respecto al mes de noviembre.*
    
**Technological tools:**

+ `Power Query:` EDA + transformations + Preprocessing 
+	`Dax:` Medidas Dax, calculos
+	`Power BI:` database, Entity Relationship Diagram, Dashboard


