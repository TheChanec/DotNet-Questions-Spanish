El **Garbage Collector** (GC) es un componente del CLR (Common Language Runtime) que se encarga de **administrar automáticamente la memoria**. Libera los objetos que **ya no son accesibles** para evitar fugas de memoria (memory leaks).

---

### 🧠 ¿Cómo funciona?

1. **Asignación de objetos**  
    Cuando creas un objeto con `new`, se asigna memoria en el **heap administrado**.
    
2. **Alcance del objeto**  
    El GC rastrea si un objeto aún tiene **referencias activas**. Si no hay referencias, se considera **"inaccesible"**.
    
3. **Recolección de basura**  
    El GC se activa **automáticamente** (cuando hay presión de memoria) o **manualmente** (`GC.Collect()`), y limpia los objetos **no referenciados**.
    
4. **Compactación**  
    Después de liberar memoria, el GC **compacta** el heap moviendo objetos para evitar fragmentación.
    

---

### 🧩 Generaciones del GC

Para optimizar el rendimiento, el GC clasifica los objetos por su tiempo de vida:

|Generación|Descripción|
|---|---|
|**Gen 0**|Objetos recién creados. Recolección rápida y frecuente.|
|**Gen 1**|Objetos que sobrevivieron a una recolección Gen 0.|
|**Gen 2**|Objetos longevos (ej: singletons, cachés). Limpieza menos frecuente.|

➡️ Esto mejora la eficiencia: en vez de escanear todo el heap, escanea solo las generaciones más jóvenes.

---

### ✅ ¿Cuándo se activa el GC?

- Cuando hay **presión de memoria**
    
- Cuando el sistema operativo lo requiere
    
- Cuando llamas manualmente `GC.Collect()` (⚠️ Evitar esto salvo casos extremos)
    

---

### 🔒 ¿Qué no hace el GC?

- **No maneja recursos no administrados** (sockets, archivos, conexiones)
    
- Por eso existen los patrones como **`IDisposable` + `using`**
    

---

### 🎯 Respuesta corta para entrevista:

> “El Garbage Collector de .NET administra la memoria automáticamente, liberando objetos que ya no tienen referencias activas. Funciona en base a un modelo de generaciones (0, 1, 2) para optimizar la performance, recolectando con más frecuencia los objetos más jóvenes. Aunque es muy eficiente, no limpia recursos no administrados, por lo que se recomienda usar `IDisposable` y `using` cuando sea necesario.”