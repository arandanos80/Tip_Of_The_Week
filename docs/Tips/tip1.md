---
layout: post
title: "Tip 1: IEnumerable vs IQueryable vs ICollection"
---

✅ La interfaz **IEnumerable<T>** se utiliza para iterar sobre una colección de un tipo especificado. Proporciona un único método, GetEnumerator(), que devuelve un enumerador que puede recorrer la colección.

𝐏𝐮𝐧𝐭𝐨𝐬 𝐜𝐥𝐚𝐯𝐞: 
  1️⃣ **IEnumerable<T>** es adecuada para iteraciones en una sola dirección sobre una colección. 
  2️⃣ Es de solo lectura, lo que significa que no se pueden agregar ni eliminar elementos de la colección.


✅ La interfaz **IQueryable<T>** extiende **IEnumerable<T>** y proporciona funcionalidad para consultar datos desde una fuente de datos. Se utiliza principalmente en LINQ to SQL y LINQ to Entities. Las consultas se construyen, pero no se ejecutan hasta que los datos son enumerados.
𝐏𝐮𝐧𝐭𝐨𝐬 𝐜𝐥𝐚𝐯𝐞: 
  1️⃣ Adecuada para consultar datos desde una fuente remota, como una base de datos. 
  2️⃣ Soporta la ejecución diferida y puede optimizar las consultas.


✅ La interfaz **ICollection<T>** extiende **IEnumerable<T>** e **IEnumerable**. Define métodos para agregar, eliminar y verificar la presencia de elementos (búsquedas). También proporciona propiedades para acceder al número de elementos y determinar si la colección es de solo lectura.

𝐏𝐮𝐧𝐭𝐨𝐬 𝐜𝐥𝐚𝐯𝐞: 
  1️⃣ Soporta operaciones como agregar, eliminar y verificar elementos. 
  2️⃣ Proporciona la propiedad Count para obtener el número de elementos en la colección.
