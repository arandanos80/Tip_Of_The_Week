---
layout: post
title: "Tip 6: New Data Annotations en .NET 8"
---

# New Data Annotations en .NET 8

🔥 En .NET 8, se introdujeron nuevas DataAnnotations para validación, permitiendo validar longitudes mínimas y máximas de cadenas, rangos de valores numéricos, especificar valores permitidos y denegados, así como la validación de Base64 strings.

✅ Atributo <b>Length</b>: Este atributo valida la longitud mínima y máxima de cadenas o colecciones.

Ej: [Length(2, 255)]

✅ Atributo <b>Range</b> con Minimun/Maximun Exclusivity: El atributo Range permite especificar si el valor mínimo o máximo es exclusivo.

Ej: [Range(1, 1000, MinimumIsExclusive = true, MaximumIsExclusive = false)]

<b>MinimumIsExclusive</b>: Especifica si la validación falla para valores iguales al mínimo.<br />
<b>MaximumIsExclusive</b>: Especifica si la validación falla para valores iguales al máximo.

✅ Atributo <b>Base64String</b>: Este atributo valida si una cadena es una representación válida en formato Base64.

Ej: [Base64String]

✅ Atributos <b>AllowedValues</b> y <b>DeniedValues</b>: Estos atributos permiten especificar un conjunto de valores permitidos o denegados para una propiedad.

```c#
    public class Producto
    {
        [Length(2, 30)]
        public string Nombre { get; set; }

        [Length(2, 255)]
        public string Descripcion { get; set; }

        [Range(1, 1000, MinimumIsExclusive = true, MaximumIsExclusive = false)]
        public decimal Precio { get; set; }

        [AllowedValues("S", "M", "L", "XL", "XXL")]
        public string Talla { get; set; }

        [DeniedValues("Electronica", "Ordenadores")]
        public string Categoria { get; set; }

        [Base64String]
        public string Imagen { get; set; }
    }

```

❓ ¿Qué piensas de las Data Annotations en .NET 8?