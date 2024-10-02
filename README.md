## **Contexto del proyecto individual**
Para este proyecto se ha creado un dashboard de ventas que permita responder las siguientes preguntas realizadas por el cliente:
•	Determinar las ventas (Total venta y cantidad).
•	Determinar el total de ventas por mes y su correspondiente variación porcentual.
•	Determinar el total de ventas por departamento del cliente.
•	Determinar el total de ventas por categoría de producto.
•	Determinar el total de ventas por género.

**Pasos para construir el Dashboard**

Paso 1: comprensión de las fuentes de datos y su contenido.
Paso 2: realización de la conexión a los datos por medio de Power BI.
Paso 3:  Proceso de limpieza a los datos.
Se realizó la transformación de datos en power query de la siguiente manera:
•	Modificación de los nombres de los archivos Excel correspondientes a las ventas de minoristas, transformándolos completamente a letras mayúsculas.
•	Se aplicó una condición de filtro a las filas de la tabla diciendo que se va a conservar las filas con extensión xslx.
•	Se aplicó un filtro para la nomenclatura de aquellos archivos que comiencen con VENTA MINORISTAS, ya que puede haber otro archivo que no necesariamente correspondan a las ventas.
•	Conservó las filas en el que el nombre no comienza por este carácter (~)
•	Se quito otras columnas y solo se conservó la columna Content
•	Se creo otra columna Datos y ahí se le asigno Content, para eso se usó la fórmula de columna personalizada   Datos = Excel.workbook([Content])
•	Se filtró las columnas de tipo Table.
•	Me percate de que no hayga filas vacías.
•	Se expandió las tablas de los dos archivos de ventas de los años 2022 y 2023 en un solo archivo
•	Le di el tipo de dato adecuado a cada columna
•	Creo una nueva consulta en lenguaje M, llamada calendario indicando que la fecha empezara con la primera venta y como última fecha con la última venta, para que a posterior cuando se agregue otras ventas se cree una fecha de acuerdo a la venta agregada.
Paso 4: creación del modelo de datos.
