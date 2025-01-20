---
layout: post
title: "Tip 13: Eficiencia con AsParallel en LINQ"
---
# Eficiencia con AsParallel en LINQ  

### 🔍 ¿Qué es ```AsParallel()```?  
```AsParallel()``` es una extensión del espacio de nombres ```System.Linq``` que permite ejecutar consultas LINQ de manera paralela utilizando **Parallel LINQ (PLINQ)**, lo cual puede mejorar significativamente el rendimiento en tareas de cálculo intensivo o en operaciones que pueden ejecutarse en paralelo.  


### 🔧 ¿Cuándo usar ```AsParallel()```?
- Cuando trabajas con **grandes cantidades de datos.**
- Si las operaciones dentro de la consulta **no tienen dependencias entre sí.**
- En escenarios donde las consultas sean **CPU-bound** (es decir, tareas intensivas de CPU).

### 🔷 Ejemplo: Procesamiento de Datos Sin Paralelismo
```c#
var numbers = Enumerable.Range(1, 10_000_000);
var evenNumbers = numbers
    .Where(n => n % 2 == 0)
    .Select(n => n * n)
    .ToList();
```
🔸 **Problema:** Aunque funcional, este enfoque procesa los datos de forma secuencial, utilizando solo un núcleo de la CPU.  

### 🔷 Ejemplo: Procesamiento Paralelo con ```AsParallel()```
```c#
var numbers = Enumerable.Range(1, 10_000_000);
var evenNumbers = numbers
    .AsParallel()
    .Where(n => n % 2 == 0)
    .Select(n => n * n)
    .ToList();
```
🔹 **Ventaja:** Esta versión utiliza todos los núcleos de la CPU disponibles, acelerando la operación en hardware multinúcleo.  

### 🔷 Comparativa
<table>
  <thead>
    <tr style="background-color: #e5e5e5">
      <th>Método</th>
      <th>Ventaja</th>
      <th>Desventaja</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Secuencial (sin PLINQ)</td>
      <td>Fácil de leer y predecible</td>
      <td>Más lento en escenarios intensivos</td>
    <tr>
      <td>Paralelo (con PLINQ)</td>
      <td>Mejor rendimiento en hardware multinúcleo.</td>
      <td>Sobrecarga por manejo de hilos y no siempre es más rápido para colecciones pequeñas.</td>
  </tbody>
</table>

### ⚠ Precauciones al usar ```AsParallel()```
- **No lo uses en operaciones I/O-bound:** PLINQ no es eficiente para operaciones que esperan datos externos (como consultas a bases de datos o servicios web).
- **Ordenación:** Si necesitas mantener el orden original, usa ```.AsParallel().AsOrdered()```.
- **Evita bloqueos compartidos:** Asegúrate de que las operaciones dentro de ```AsParallel()``` no manipulen recursos compartidos para evitar **race conditions**.

### 💡 Conclusión
Utiliza ```AsParallel()``` para aprovechar múltiples núcleos en tu CPU, pero ten cuidado con los escenarios en los que lo aplicas. Evalúa siempre el impacto en la legibilidad del código y en la eficiencia de las operaciones.
