---
layout: post
title: "Tip 5: Use of var or explicit type"
---

# Use of var or explicit type

🔥 La palabra clave <strong>var</strong> fue introducida en C# 3.0 y permite que el compilador infiera el tipo de una variable basado en el valor asignado. Mejora la legibilidad del código y puede reducir la redundancia. Sin embargo, es fundamental usar <strong>var</strong> de manera efectiva para mantener la claridad del código. 

<strong>1️⃣ Uso de var para mejorar la legibilidad <br /><br />
Cuando usar var puede hacer el código más claro:</strong><br /><br />
✅ Cuando el tipo es obvio en la asignación. <br />Si el tipo de la variable es evidente en el contexto de la asignación, usar <b>var</b> puede hacer que el código sea más fácil de leer al reducir el ruido visual.
<br />
![image](https://github.com/user-attachments/assets/b5cc3898-42e1-4c29-80f8-5c415a948544)
<br />
✅ Para tipos complejos o anónimos. <br />En casos donde el tipo es largo o complejo, <b>var</b> puede hacer que el código sea más legible sin sacrificar la claridad, especialmente cuando se trabaja con tipos de LINQ o clases anónimas.
<br />
![image](https://github.com/user-attachments/assets/90e48e11-19a2-4049-9a24-28b61b35cc7d)
<br />
Aquí, el tipo del objeto es anónimo (no tiene un nombre explícito), por lo que <b>var</b> es la única opción. <br /><br />
✅ Con LINQ y otros casos de tipos inferidos. <br />Al trabajar con LINQ, <b>var</b> es útil para variables que contienen resultados de consultas donde el tipo puede ser complicado. <br />
![image](https://github.com/user-attachments/assets/cc265032-a5e8-4734-8946-03e17a9aa681)
<br />
En este caso, el tipo de resultado es IEnumerable<Persona>, lo cual puede ser un poco más largo y menos intuitivo de escribir que simplemente <b>var</b>.<br /><br />
<strong>2️⃣ Uso del tipo explícito para mayor claridad<br /><br />
Cuándo es preferible declarar el tipo explícitamente:</strong><br /><br />
✅ Cuando el tipo no es obvio. Si el tipo de la variable no es inmediatamente claro a partir de la asignación, es mejor declararlo explícitamente para evitar confusión.<br />
![382681896-a6af583b-9b57-418c-a6da-8ceb31233107](https://github.com/user-attachments/assets/dfd8f4fe-b027-4a5b-b680-b69669611cad)
<br />
Aquí, aunque <b>var</b> podría inferir el tipo de ObtenerContador(), declarar int explícitamente aclara la intención al lector.<br />
✅ Para mejorar la comprensión de intenciones. Al usar tipos primitivos o bien conocidos, el tipo explícito puede ser más claro. Esto es particularmente útil en casos donde una simple asignación puede ser ambigua. <br />
![image](382682781-82eb7e68-aa1d-49b8-8b9e-ea6d04c34d10.png)
<br />
Si se usa <b>var mensaje = "Hola, mundo!";</b> se entenderá que <b>mensaje</b> es una cadena, pero usar <b>string</b> explícitamente puede hacer más claro al lector que la variable <b>mensaje</b> se espera que sea una cadena de texto.<br />
✅ Para evitar inferencias incorrectas. A veces <b>var</b> puede hacer inferencias inesperadas. Por ejemplo:
![image](382684102-e8d8015e-864c-47ce-8e86-69f433407fef.png)
<br />
Si realmente querías que <b>numero</b> fuera un tipo decimal, es preferible especificarlo:
<br />
![image](382684939-2665acf8-b21c-4aef-95b8-c6954aacbf87.png)
<br /><br />
<strong>🚀 Ejemplo práctico de combinación</strong><br />
A continuación, un ejemplo que combina <b>var</b> y tipos explícitos para hacer el código claro y fácil de leer:<br />
![image](382686801-cc1b1bca-b0b9-4a24-8dc8-3c34c140dbe5.png)
<br />
En este ejemplo, <b>mayoresADos</b> es inferido como <b>IEnumerable&lt;int&gt;</b>, que es lo que esperamos, y <b>total</b> es explícitamente <b>int</b>, lo cual puede ayudar a identificar un posible error si <b>Sum()</b> devuelviera otro tipo de dato. <br /><br />
<strong>🔥 Recomendación general</strong><br /><br />
✅ Usa <i>var</i> <b>cuando el tipo es obvio o el tipo es complejo</b> y su uso no disminuye la claridad.<br />
✅ Usa el <b>tipo explícito</b> cuando el tipo no es evidente o para hacer que el código sea más claro en términos de intención y legibilidad.<br /><br />
👉 Cada uno tiene su momento adecuado, y una combinación de ambos generalmente lleva a un código más limpio y comprensible.
