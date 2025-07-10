Excelente. Estos patrones son muy comunes en entrevistas senior .NET, especialmente cuando se habla de **acceso a datos desacoplado** y **mantenible**. Aquí te explico el **patrón Repository y Unit of Work** con ejemplos claros y nivel de entrevista:

---

## ✅ Patrón Repository

### 📌 ¿Qué es?

El **Repository** es un patrón que actúa como una **abstracción sobre el acceso a datos**, permitiéndote trabajar con entidades del dominio sin preocuparte por los detalles de la base de datos.

### 🎯 Objetivo:

- Centralizar lógica de acceso a datos
    
- Separar el dominio de la infraestructura (SRP de SOLID)
    
- Facilitar pruebas unitarias (mocking)
    

---

### 🧱 Ejemplo básico:

```csharp
public interface IProductoRepository
{
    Producto GetById(int id);
    IEnumerable<Producto> GetAll();
    void Add(Producto producto);
    void Delete(Producto producto);
}
```

```csharp
public class ProductoRepository : IProductoRepository
{
    private readonly DbContext _context;

    public ProductoRepository(DbContext context)
    {
        _context = context;
    }

    public Producto GetById(int id) => _context.Set<Producto>().Find(id);
    public IEnumerable<Producto> GetAll() => _context.Set<Producto>().ToList();
    public void Add(Producto producto) => _context.Set<Producto>().Add(producto);
    public void Delete(Producto producto) => _context.Set<Producto>().Remove(producto);
}
```

---

## ✅ Patrón Unit of Work

### 📌 ¿Qué es?

**Unit of Work (UoW)** es un patrón que agrupa varias operaciones sobre repositorios en una **única transacción**.

### 🎯 Objetivo:

- Controlar la consistencia y persistencia de múltiples repositorios
    
- Garantizar que todas las operaciones de una unidad lógica se guarden juntas (o se reviertan juntas)
    

---

### 🧱 Ejemplo:

```csharp
public interface IUnitOfWork : IDisposable
{
    IProductoRepository Productos { get; }
    IClienteRepository Clientes { get; }
    int Complete(); // Commit
}
```

```csharp
public class UnitOfWork : IUnitOfWork
{
    private readonly AppDbContext _context;

    public UnitOfWork(AppDbContext context)
    {
        _context = context;
        Productos = new ProductoRepository(_context);
        Clientes = new ClienteRepository(_context);
    }

    public IProductoRepository Productos { get; private set; }
    public IClienteRepository Clientes { get; private set; }

    public int Complete() => _context.SaveChanges();
    public void Dispose() => _context.Dispose();
}
```

---

### 🧠 Ventajas combinadas:

|Repository|Unit of Work|
|---|---|
|Encapsula operaciones sobre una entidad|Agrupa operaciones de varios repos|
|Mejora la reutilización y pruebas|Garantiza consistencia (transacción única)|
|Se puede usar con EF, Dapper, ADO.NET|Compatible con múltiples ORMs|

---

### 🎯 Resumen para entrevista:

> “Repository abstrae el acceso a datos por entidad, permitiendo desacoplar el dominio de la persistencia. Unit of Work agrupa varios repositorios para garantizar que sus operaciones se ejecuten como una sola transacción, mejorando la consistencia y manteniendo el principio de responsabilidad única.”

---

¿Quieres un ejemplo con EF Core real y Unit Tests simulados? ¿O cómo implementar estos patrones con Dapper o CQRS?