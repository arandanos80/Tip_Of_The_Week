---
layout: post
title: "Tip 12: Performance impact of Skip-Take order in Queries"
---
# Performance impact of Skip-Take order in Queries  

### 🔍 ¿Hay una diferencia?  
Cuando trabajas con Entity Framework y consultas que incluyen paginación, el orden en el que aplicas los métodos ```.Skip()``` y ```.Take()``` puede afectar el rendimiento. Esto depende de cómo se traduce la consulta LINQ a SQL en la base de datos subyacente.  

### 🔧 Diferencia Clave
- ```.Skip(x).Take(y)```: Es el orden recomendado para implementar paginación. Primero salta los elementos iniciales (x) y luego toma el número requerido (y).
- ```.Take(y).Skip(x)```: Generalmente es menos eficiente en consultas de paginación porque puede requerir que la base de datos recupere más registros de los necesarios, lo que aumenta la carga en memoria y red.

### 🔷 Ejemplo Práctico  
<strong>🛠 Consulta con ```.Skip().Take()```:</strong>
```c#
var results = dbContext.Products
    .OrderBy(p => p.ProductId)
    .Skip(10)
    .Take(5)
    .ToList();
```
<strong>Traducción SQL:</strong>  
```SQL
SELECT TOP(5) * 
FROM (SELECT *, ROW_NUMBER() OVER (ORDER BY ProductId) AS RowNum 
      FROM Products) AS RowResult
WHERE RowResult.RowNum > 10
```

**Eficiencia:** Solo devuelve los registros requeridos (5 elementos) después de saltar los primeros 10.  


<strong>🛠 Consulta con ```.Take().Skip()```:</strong>
```c#
var results = dbContext.Products
    .OrderBy(p => p.ProductId)
    .Take(15)
    .Skip(10)
    .ToList();
```
<strong>Traducción SQL:</strong>  
```SQL
SELECT * 
FROM (SELECT TOP(15) *, ROW_NUMBER() OVER (ORDER BY ProductId) AS RowNum 
      FROM Products) AS RowResult
WHERE RowResult.RowNum > 10
```

**Problema:** La base de datos primero recupera 15 registros, de los cuales solo usa 5, lo que implica un desperdicio de recursos en la red y memoria.  

### 🔷 Comparativa  
<table>
    <thead>
        <tr style="background-color: #e5e5e5">
          <th>Método</th>
          <th>Uso recomendado</th>
          <th>Traducción SQL</th>
          <th>Rendimiento</th>
        </tr>
    </thead>
    <tbody>
        <tr>
          <td>.Skip(x).Take(y)</td>
          <td>✅ Sí</td>
          <td>Recupera solo los registros necesarios.</td>
          <td>Eficiente. Solo consulta los registros requeridos.</td>
        </tr>
        <tr>
          <td>.Take(y).Skip(x)</td>
          <td>❌ No</td>
          <td>Puede recuperar más registros de los necesarios.</td>
          <td>Menos eficiente. Incrementa la carga de datos.</td>
        </tr>
    </tbody>
</table>


### 💡 Extra Tip  
Antes de usar paginación, siempre incluye un método ```OrderBy()``` en tu consulta para garantizar resultados consistentes, ya que sin un orden definido, los resultados pueden ser impredecibles.
