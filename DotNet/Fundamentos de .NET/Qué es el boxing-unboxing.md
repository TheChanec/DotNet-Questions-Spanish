**Boxing** y **unboxing** son procesos de conversión entre tipos de valor (value types) y referencias (reference types) en .NET:

---

### 🎁 Boxing

- **¿Qué es?**  
    Convertir un tipo de valor (por ejemplo, `int`, `bool`, `struct`) en un objeto de tipo referencia (`object` o una interfaz que implemente).
    
- **¿Cómo funciona?**  
    Se reserva un bloque de memoria en el _heap_, se copia el valor ahí y se devuelve la referencia.
    
- **Ejemplo**:
    
    ```csharp
    int x = 123;
    object obj = x;   // Boxing: x se “empaqueta” en un objeto
    ```
    
- **Costo**:
    
    - **Asignación en heap**
        
    - **Copia de datos**
        
    - Puede generar **presión de GC** si ocurre muy frecuentemente
        

---

### 📦 Unboxing

- **¿Qué es?**  
    Extraer el valor de un objeto que fue previamente “boxeado”. Convierte de nuevo la referencia a un tipo de valor.
    
- **¿Cómo funciona?**  
    Verifica en tiempo de ejecución que el objeto contenga el tipo de valor correcto y copia el contenido de vuelta a la variable de tipo valor.
    
- **Ejemplo**:
    
    ```csharp
    object obj = 123;      // Boxing
    int y = (int)obj;      // Unboxing: se verifica y se copia el valor a y
    ```
    
- **Costo**:
    
    - **Verificación de tipo en tiempo de ejecución**
        
    - **Copia de datos**
        

---

### 🤔 ¿Por qué importa?

- **Rendimiento**:  
    El boxing/unboxing frecuente puede degradar el rendimiento debido a asignaciones en el heap y trabajo extra en el GC.
    
- **Buenas prácticas**:
    
    - Evitar pasar tipos de valor a APIs que usen `object` o `IList<object>` si necesitas performance.
        
    - Usar genéricos (`List<int>`, `IEnumerable<T>`) para evitar boxing automático.
        

---

> **Respuesta corta para entrevista:**  
> “Boxing es convertir un tipo de valor a una referencia (`object`), creando un nuevo objeto en el heap; unboxing es extraer ese valor de vuelta. Ambos implican copia de datos y, en el caso de boxing, asignación en el heap, por lo que hay un costo de rendimiento. El uso de genéricos en .NET ayuda a evitarlos.”

---
