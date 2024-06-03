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
```
SELECT Ubicacion
FROM Departamento
WHERE IDDepartamento = 2;
```
__ejercicio 4__
```
SELECT NombreProyecto, Ubicacion, IDDepartamento
FROM Proyecto;
```

__ejercicio 5__
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
```
SELECT HorasTrabajadas,IDempleado AS "IDEmpleados",
       AVG(HorasTrabajadas + COALESCE(IDProyecto, 0)) AS " Total de horas trabajadas"
FROM EmpleadoProyecto
GROUP BY IDEmpleado, IDProyecto;
```


__ejercicio 10__

```
    SELECT E.IDEmpleado, E.NombreEmpleado
    FROM Empleado E
    JOIN EmpleadoProyecto EP on E.IDEmpleado = EP.IDEmpleado
    GROUP BY E.IDEmpleado, E.NombreEmpleado
    HAVING COUNT(EP.IDProyecto)>1;
```

__ejercicio 11__
```
SELECT E.IDEmpleado, E.NombreEmpleado, SUM(EP.HorasTrabajadas) AS totalHorasTrabajadas
FROM Empleado E
JOIN EmpleadoProyecto EP ON E.IDEmpleado = EP.IDEmpleado
WHERE E.IDJefe IS NOT NULL
GROUP BY E.IDEmpleado, E.NombreEmpleado
HAVING  count(EP.IDProyecto) > 1 AND SUM(EP.HorasTrabajadas) > 30;
```

__ejercicio 12__
```
SELECT IDProyecto, coalesce(AVG(HorasTrabajadas),0) AS "Promedio Horas Trabajadas"
FROM EmpleadoProyecto
GROUP BY IDEmpleado,IDProyecto;
```

__ejercicio 13__
```

SELECT E.IDEmpleado, E.NombreEmpleado,E.Salario,E.comision, P.NombreProyecto
FROM Empleado E
JOIN EmpleadoProyecto EP on E.IDEmpleado = EP.IDEmpleado
JOIN Proyecto P ON EP.IDProyecto = P.IDProyecto
WHERE P.Ubicacion = 'CHICAGO' AND  (E.Salario + coalesce(E.Comision,0))> 2000;
```
__ejercicio 14__
```
SELECT E.IDEmpleado, E.NombreEmpleado, SUM(EP.HorasTrabajadas) AS totalHorasTrabajadas
FROM Empleado E
JOIN EmpleadoProyecto EP ON E.IDEmpleado = EP.IDEmpleado
WHERE E.IDJefe IS NOT NULL
GROUP BY E.IDEmpleado, E.NombreEmpleado
HAVING  count(EP.IDProyecto) > 1 AND SUM(EP.HorasTrabajadas) > 15;
```

__ejercicio 15__
```
SELECT E.IDEmpleado, E.NombreEmpleado, D.NombreDepartamento, D.Ubicacion
FROM Empleado E
JOIN Departamento D ON E.IDDepartamento = D.IDDepartamento
WHERE  E.Comision IS NULL AND (D.Ubicacion = 'DALLAS' OR D.Ubicacion = 'NEW YORK ');
```

