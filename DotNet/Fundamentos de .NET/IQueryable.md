- **Qué es**: Extiende `IEnumerable`, pero permite construir consultas **expresadas como árboles de expresión**.
- **Dónde se usa**: Ideal para providers como Entity Framework o LINQ to SQL.
- **Ejecución**: Diferida también, pero permite ser **traducida a SQL u otro lenguaje**.
- **Ventaja**: Optimiza consultas; solo ejecuta lo necesario en el origen de datos.

📌 Ejemplo: `.Where(x => x.Id == 1)` se traduce a SQL y se ejecuta en el servidor.