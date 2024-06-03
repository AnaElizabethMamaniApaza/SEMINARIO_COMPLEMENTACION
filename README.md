# TAREA 11

**EJERCICIOS PROPUESTOS**

__ejercicio 1__
>¿Cuáles son los identificadores y nombres de todos los proyectos existentes en la empresa?
```
SELECT IDDepartamento,NombreDepartamento
FROM Departamento;
SELECT IDEmpleado,NombreEmpleado
FROM Empleado;
SELECT IDProyecto,NombreProyecto
FROM Proyecto;
SELECT IDEmpleado,IDProyecto
FROM EmpleadoProyecto;
```
__ejercicio 2__
>¿Cuáles son los proyectos que se desarrollan en 'CHICAGO'?
```
SELECT DISTINCT IDDepartamento AS "CHICAGO"
FROM Proyecto
WHERE IDDepartamento IS NOT NULL;
```
__ejercicio 3__
>¿Cuáles son los proyectos que pertenecen al departamento con identificador 2?
```
SELECT Ubicacion
FROM Departamento
WHERE IDDepartamento = 2;
```
__ejercicio 4__
>¿Cuáles son los nombres y ubicaciones de los proyectos junto con los nombres de sus departamentos asociados?
```
SELECT NombreProyecto, Ubicacion, IDDepartamento
FROM Proyecto;
```

__ejercicio 5__
>
```
SELECT *
FROM Empleado
WHERE IDJefe IS NOT NULL AND
(Salario + COALESCE(Comision, 0) > 4 OR Salario > 4);
```
__ejercicio 6__
```
SELECT *
FROM Proyecto
WHERE IDDepartamento IS NOT NULL AND
(NombreProyecto + COALESCE(Ubicacion, 0) > 4 OR NombreProyecto > 4);
```

__ejercicio 7__
>
```
SELECT SUM(Horastrabajadas)
FROM EmpleadoProyecto
WHERE  IDProyecto =2;
```

__ejercicio 8__
```
SELECT E.IDEmpleado, E.NombreEmpleado
FROM Empleado E
Join EmpleadoProyecto EP on E.IDEmpleado = EP.IDEmpleado
where EP.IDProyecto = 2 AND EP.HorasTrabajadas >10;
```

__ejercicio 9__
>
```
SELECT HorasTrabajadas,IDempleado AS "IDEmpleados",
       AVG(HorasTrabajadas + COALESCE(IDProyecto, 0)) AS " Total de horas trabajadas"
FROM EmpleadoProyecto
GROUP BY IDEmpleado, IDProyecto;
```


__ejercicio 10__
>

```
    SELECT E.IDEmpleado, E.NombreEmpleado
    FROM Empleado E
    JOIN EmpleadoProyecto EP on E.IDEmpleado = EP.IDEmpleado
    GROUP BY E.IDEmpleado, E.NombreEmpleado
    HAVING COUNT(EP.IDProyecto)>1;
```

__ejercicio 11__
>¿Cuáles son los empleados que trabajan en más de un proyecto?
```
SELECT E.IDEmpleado, E.NombreEmpleado, SUM(EP.HorasTrabajadas) AS totalHorasTrabajadas
FROM Empleado E
JOIN EmpleadoProyecto EP ON E.IDEmpleado = EP.IDEmpleado
WHERE E.IDJefe IS NOT NULL
GROUP BY E.IDEmpleado, E.NombreEmpleado
HAVING  count(EP.IDProyecto) > 1 AND SUM(EP.HorasTrabajadas) > 30;
```

__ejercicio 12__
>¿Cuál es el promedio de horas trabajadas por proyecto?
```
SELECT IDProyecto, coalesce(AVG(HorasTrabajadas),0) AS "Promedio Horas Trabajadas"
FROM EmpleadoProyecto
GROUP BY IDEmpleado,IDProyecto;
```

__ejercicio 13__
>¿Cuáles son los empleados que trabajan en proyectos ubicados en 'CHICAGO' y que tienen un salario (con o sin comisión) superior a 2000?
```

SELECT E.IDEmpleado, E.NombreEmpleado,E.Salario,E.comision, P.NombreProyecto
FROM Empleado E
JOIN EmpleadoProyecto EP on E.IDEmpleado = EP.IDEmpleado
JOIN Proyecto P ON EP.IDProyecto = P.IDProyecto
WHERE P.Ubicacion = 'CHICAGO' AND  (E.Salario + coalesce(E.Comision,0))> 2000;
```
__ejercicio 14__
>¿Cuáles son los empleados que tienen un jefe, están asignados a más de un proyecto, y han trabajado más de 15 horas en total en todos los proyectos combinados?
```
SELECT E.IDEmpleado, E.NombreEmpleado, SUM(EP.HorasTrabajadas) AS totalHorasTrabajadas
FROM Empleado E
JOIN EmpleadoProyecto EP ON E.IDEmpleado = EP.IDEmpleado
WHERE E.IDJefe IS NOT NULL
GROUP BY E.IDEmpleado, E.NombreEmpleado
HAVING  count(EP.IDProyecto) > 1 AND SUM(EP.HorasTrabajadas) > 15;
```

__ejercicio 15__
>¿Cuáles son los empleados que no reciben comisión y trabajan en departamentos ubicados en 'DALLAS' o 'NEW YORK'?
```
SELECT E.IDEmpleado, E.NombreEmpleado, D.NombreDepartamento, D.Ubicacion
FROM Empleado E
JOIN Departamento D ON E.IDDepartamento = D.IDDepartamento
WHERE  E.Comision IS NULL AND (D.Ubicacion = 'DALLAS' OR D.Ubicacion = 'NEW YORK ');
```

