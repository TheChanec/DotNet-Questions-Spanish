- **Qué es**: Interfaz que permite iterar una colección.
- **Dónde se usa**: Ideal para recorrer colecciones en memoria.
- **Ejecución**: **Ejecución diferida** (lazy).
- **Limitación**: No tiene capacidad de construir consultas ni traducirlas (solo `foreach`, LINQ en memoria).

📌 Ejemplo: `IEnumerable<T>` no puede traducir expresiones a SQL en EF Core. Todo se ejecuta en memoria.