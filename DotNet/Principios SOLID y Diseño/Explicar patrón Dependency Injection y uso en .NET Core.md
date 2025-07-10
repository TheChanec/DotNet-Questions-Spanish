Excelente, esta es una de las preguntas **más comunes en entrevistas senior de .NET Core**. Vamos a explicarlo de forma clara, completa y al nivel que EPAM o cualquier empresa esperaría:

---

## ✅ ¿Qué es el patrón **Dependency Injection (DI)**?

Es un patrón de diseño que consiste en **inyectar las dependencias** (servicios, clases, etc.) de una clase **desde el exterior**, en lugar de que la clase las cree por sí misma.

🔧 Se basa en el principio SOLID de **Inversión de Dependencias (D)**: las clases deben depender de **abstracciones**, no de implementaciones concretas.

---

## 🔍 ¿Por qué usarlo?

- ✅ **Desacopla** las clases
    
- ✅ Facilita los **tests unitarios** (mocking)
    
- ✅ Permite la **sustitución fácil** de implementaciones
    
- ✅ Centraliza la configuración de dependencias
    

---

## 💡 Ejemplo antes de usar DI (acoplamiento):

```csharp
public class PedidoService
{
    private readonly EmailService _email = new EmailService();

    public void Procesar() => _email.EnviarConfirmacion();
}
```

❌ Está acoplado: no se puede reemplazar `EmailService` fácilmente, ni testear sin enviar correos reales.

---

## ✅ Con Dependency Injection:

```csharp
public interface IEmailService
{
    void EnviarConfirmacion();
}

public class EmailService : IEmailService
{
    public void EnviarConfirmacion() => Console.WriteLine("Correo enviado");
}

public class PedidoService
{
    private readonly IEmailService _email;

    public PedidoService(IEmailService email)
    {
        _email = email;
    }

    public void Procesar() => _email.EnviarConfirmacion();
}
```

Ahora puedes inyectar cualquier implementación de `IEmailService`, por ejemplo, un mock en tests.

---

## 🚀 ¿Cómo se usa en .NET Core?

ASP.NET Core tiene un **contenedor de inyección de dependencias incorporado** (IoC container).

### 1. Registras los servicios en `Program.cs`:

```csharp
builder.Services.AddScoped<IEmailService, EmailService>();
builder.Services.AddScoped<PedidoService>();
```

### 2. Se resuelven automáticamente:

- En controladores:
    

```csharp
public class PedidoController : ControllerBase
{
    private readonly PedidoService _service;

    public PedidoController(PedidoService service)
    {
        _service = service;
    }
}
```

- O desde cualquier clase registrada:
    

```csharp
var servicio = scope.ServiceProvider.GetRequiredService<PedidoService>();
```

---

## 🧠 Tipos de vida útil (lifetime):

|Tipo|Descripción|Ejemplo de uso|
|---|---|---|
|`Singleton`|Una sola instancia para toda la app|Configuración, logging|
|`Scoped`|Una instancia por request HTTP|Servicios de negocio|
|`Transient`|Una nueva instancia cada vez que se pide|Servicios livianos|

```csharp
services.AddSingleton<IMiServicio, MiServicio>();
services.AddScoped<IMiServicio, MiServicio>();
services.AddTransient<IMiServicio, MiServicio>();
```

---

## 🎯 Resumen para entrevista:

> “Dependency Injection es un patrón que permite inyectar las dependencias de una clase desde el exterior, reduciendo el acoplamiento. ASP.NET Core lo soporta de forma nativa con un contenedor IoC donde se registran los servicios. Esto mejora la mantenibilidad, facilita las pruebas unitarias y promueve el principio de inversión de dependencias del modelo SOLID.”

---

¿Quieres que te dé un ejemplo con testing (`Moq`) usando DI o una pregunta de práctica tipo entrevista?