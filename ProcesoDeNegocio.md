## 1. En este KPI mostramos la ultima fecha de pedido que gestiono cada empleado:
```sql
SELECT max(FechaPedido) as ultimoPedido,  /*Aqui seleccionamos la ultima(maxima) fecha de pedido*/
    (SELECT codEmpleado 
    FROM Empleados AS E1           									
	WHERE E1.codEmpleado = P1.codRepresentante) as codigoEmpleado  /*Con esto indicamos que el codEmpleado es igual al codRepresentante para que solo me salgan empleados que sean representantes*/
	FROM Pedidos AS P1
group by codigoEmpleado;  /* Aqui agrupo a los empleados para que no me aparezcan nulos.*/
```

## 2. En este mostramos las oﬁcinas cuyo objetivo es superior al 50% de la suma de los salarios de sus empleados:
```sql
SELECT CodOficina, Ciudad, Objetivo  /*Aqui seleccionamos el codigo de oficina la ciudad y objetivo*/
FROM Oficinas  
 WHERE Objetivo > (SELECT sum(Sueldo)*0.50 AS S1  /*Aqui digo que me liste cuyo el 50% del sueldo sea mayor que el objetivo*/
 FROM Empleados 
 WHERE Empleados.Oficina = Oficinas.CodOficina);
```

## 3. En este mostramos los empleados cuyo sueldo es mayor a la media de todos los empleados:
```sql
SELECT Codempleado, Nombre, Sueldo, categoria /*Aqui seleccionamos el codigo de empleado, el nombre,el sueldo y su categoria*/
FROM Empleados AS E1
WHERE Sueldo >= (SELECT Avg(Sueldo) FROM Empleados /*Me devuelve los empleados cuyo sueldo es mayor a la media de todos los empleados*/
)
ORDER BY sueldo; /*Aqui le digo que me ordene los sueldos en orden ascendente*/
```

## 4. En este mostramos los empleados cuyas oficinas sus ventas no han podido llegar a su objetivo:
```sql
SELECT codEmpleado,nombre /*Aqui seleccionamos el codigo de empleado y el nombre*/
FROM empleados
WHERE oficina IN ( SELECT oficina FROM oficinas WHERE objetivo > ventas); /*Lista los vendedores que trabajan en oﬁcinas que tienen el objetivo superior a sus ventas).*/
```

**Trabajo hecho por : Pablo Sobral**