---
layout: post
title: "Tip 1: IEnumerable vs IQueryable vs ICollection"
---

# IEnumerable vs IQueryable vs ICollection

✅ La interfaz IEnumerable&lt;T&gt; se utiliza para iterar sobre una colección de un tipo especificado. Proporciona un único método, GetEnumerator(), que devuelve un enumerador que puede recorrer la colección.

𝐏𝐮𝐧𝐭𝐨𝐬 𝐜𝐥𝐚𝐯𝐞:<br /> 
  1️⃣ IEnumerable&lt;T&gt; es adecuada para iteraciones en una sola dirección sobre una colección. <br />
  2️⃣ Es de solo lectura, lo que significa que no se pueden agregar ni eliminar elementos de la colección.<br />
<br />

✅ La interfaz IQueryable&lt;T&gt; extiende IEnumerable&lt;T&gt; y proporciona funcionalidad para consultar datos desde una fuente de datos. Se utiliza principalmente en LINQ to SQL y LINQ to Entities. Las consultas se construyen, pero no se ejecutan hasta que los datos son enumerados.

𝐏𝐮𝐧𝐭𝐨𝐬 𝐜𝐥𝐚𝐯𝐞: <br />
  1️⃣ Adecuada para consultar datos desde una fuente remota, como una base de datos. <br />
  2️⃣ Soporta la ejecución diferida y puede optimizar las consultas.<br />
<br />

✅ La interfaz ICollection&lt;T&gt; extiende IEnumerable&lt;T&gt; e IEnumerable. Define métodos para agregar, eliminar y verificar la presencia de elementos (búsquedas). También proporciona propiedades para acceder al número de elementos y determinar si la colección es de solo lectura.

𝐏𝐮𝐧𝐭𝐨𝐬 𝐜𝐥𝐚𝐯𝐞: <br />
  1️⃣ Soporta operaciones como agregar, eliminar y verificar elementos. <br />
  2️⃣ Proporciona la propiedad Count para obtener el número de elementos en la colección.<br />
