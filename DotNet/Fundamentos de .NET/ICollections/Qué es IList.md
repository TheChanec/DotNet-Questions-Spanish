`IList<T>` es una **interfaz genérica** de .NET que **hereda de `ICollection<T>` y `IEnumerable<T>`**, y representa una **colección indexada** de objetos que puedes **leer, modificar, insertar o eliminar**.

---

### 🧠 Características clave:

|Propiedad|Descripción|
|---|---|
|**Indexada**|Puedes acceder a los elementos por su posición (`myList[0]`)|
|**Mutable**|Permite agregar, eliminar, insertar y modificar elementos|
|**Ordenada**|Mantiene el orden de inserción|
|**Herencia**|Hereda de `IEnumerable<T>` → se puede recorrer con `foreach`|

---

### ✅ Métodos y propiedades comunes:

csharp

CopiarEditar

`IList<string> nombres = new List<string>();  nombres.Add("Juan");            // Agrega nombres.Insert(0, "Ana");       // Inserta en posición nombres.Remove("Juan");         // Elimina por valor nombres.RemoveAt(0);            // Elimina por índice var segundo = nombres[1];       // Accede por índice nombres[1] = "Pedro";           // Modifica`

---

### ✅ Implementaciones comunes:

- `List<T>` (más común)
    
- `BindingList<T>` (útil para UI)
    
- `Collection<T>`
    

---

### 🚀 ¿Cuándo usar `IList<T>`?

- Cuando necesitas una **colección modificable e indexada**
    
- Cuando quieres trabajar contra una interfaz (buenas prácticas) en vez de una implementación concreta como `List<T>`
    
- Útil en **inyección de dependencias**, tests, y desacoplar componentes
    

---

### ⚠️ ¿En qué se diferencia de `List<T>`?

- `List<T>` es una **clase concreta**.
    
- `IList<T>` es una **interfaz**, así que no puedes instanciarla directamente.
    
- Te da flexibilidad para cambiar la implementación sin romper el contrato.
    

---

Si te preguntan en entrevista:

> “¿Por qué usarías `IList<T>` en vez de `List<T>`?”

Puedes decir:

> “Porque trabajar con la interfaz `IList<T>` me permite desacoplar la lógica de negocio de la implementación concreta, facilitando pruebas unitarias y aplicando principios como programación orientada a interfaces y el principio de inversión de dependencias (D de SOLID).”