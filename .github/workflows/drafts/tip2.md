---
layout: post
title: "Tip 2: Uso de AsSpan en lugar de Substring"
---

# Uso de AsSpan en lugar de Substring

🔥 Usar 𝙎𝙪𝙗𝙨𝙩𝙧𝙞𝙣𝙜 asigna un nuevo objeto 𝙨𝙩𝙧𝙞𝙣𝙜 en la pila (heap) e implica una copia completa del texto extraído. La manipulación de cadenas puede convertirse en un cuello de botella para el rendimiento, especialmente cuando se trata con muchas cadenas pequeñas y de corta duración. Esto puede afectar el rendimiento debido a la asignación de memoria y el garbage collection.

El problema se vuelve más notable al trabajar con subcadenas grandes. Para abordar esto, C# introdujo los tipos `𝙎𝙥𝙖𝙣<𝙏>` y `𝙍𝙚𝙖𝙙𝙤𝙣𝙡𝙮𝙎𝙥𝙖𝙣<𝙏>`. Esto permite una manipulación más eficiente de datos de caracteres sin copias innecesarias.

✅ Cuando las APIs ofrezcan sobrecargas que acepten 𝙍𝙚𝙖𝙙𝙤𝙣𝙡𝙮𝙎𝙥𝙖𝙣<𝙘𝙝𝙖𝙧>, considera usar 𝘼𝙨𝙎𝙥𝙖𝙣 en lugar de 𝙎𝙪𝙗𝙨𝙩𝙧𝙞𝙣𝙜 para mejorar el rendimiento.

📜 Rule ID: 𝗖𝗔𝟭𝟴𝟰𝟲 (Prefer AsSpan over Substring)

❓ ¿Has usado 𝘼𝙨𝙎𝙥𝙖𝙣 en lugar de 𝙎𝙪𝙗𝙨𝙩𝙧𝙞𝙣𝙜?