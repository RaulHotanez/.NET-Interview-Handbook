# Delegates
________________________________________
Un delegate es un tipo que puede almacenar una referencia a uno o varios métodos que tengan la misma firma (mismos parámetros y tipo de retorno).

Piensa en él como un puntero a función, pero de forma segura en C#.
________________________________________
#### Definición para entrevista:

"Un delegate es un tipo seguro que permite almacenar y ejecutar referencias a métodos con la misma firma. Se utiliza para desacoplar el código, implementar callbacks, eventos y expresiones lambda."
________________________________________
#### Ejemplo sencillo

Supongamos este método:

```csharp title="C#"
public static void Saludar()
{
    Console.WriteLine("Hola");
}
```

Creamos un delegate:

```csharp title="C#"
delegate void MiDelegate();
```

Ahora lo usamos:
```csharp title="C#"
MiDelegate delegado = Saludar;

delegado();
```

Salida:

```csharp title="C#"
Hola
```

En realidad estás llamando al método mediante el delegate.

Otro ejemplo
```csharp title="C#"
delegate int Operacion(int a, int b);

public static int Sumar(int a, int b)
{
    return a + b;
}

Operacion op = Sumar;

Console.WriteLine(op(5, 3));
```

Salida:
```csharp title="C#"
8
```
________________________________________
### ¿Para qué sirven?

#### 1. Ejecutar diferentes métodos dinámicamente
```csharp title="C#"
delegate int Operacion(int a, int b);
int Sumar(int a, int b) => a + b;
int Restar(int a, int b) => a - b;

Operacion op;
op = Sumar;
Console.WriteLine(op(5,3));
op = Restar;
Console.WriteLine(op(5,3));
```

El mismo delegate puede apuntar a distintos métodos.

#### 2. Callbacks

Imagina un método que recibe "qué hacer" cuando termine.

```csharp title="C#"
public void Procesar(Action accion)
{
    Console.WriteLine("Procesando...");

    accion();
}
```

Uso:

```csharp title="C#"
Procesar(() =>
{
    Console.WriteLine("Proceso terminado");
});
```
#### 3. Eventos

Todos los eventos en C# están basados en delegates.

```csharp title="C#"
button.Click += MiMetodo;
```

Internamente:

```csharp title="C#"
Evento

↓

Delegate

↓

Método
```
#### 4. LINQ

Cuando haces esto:

```csharp title="C#"
var mayores = personas.Where(x => x.Edad > 18);
```
La expresión:
```csharp title="C#"
x => x.Edad > 18
```
Es una lambda que se convierte en un delegate (o en una expresión, según el contexto).

Delegates incorporados

Hoy en día casi nunca defines tus propios delegates porque .NET ya trae varios.

Action

No devuelve nada.

```csharp title="C#"
Action<string> saludar =
    nombre => Console.WriteLine($"Hola {nombre}");

saludar("Raúl");
```

Devuelve un valor.

```csharp title="C#"
Func<int, int, int> suma = (a, b) => a + b;

Console.WriteLine(suma(3,4));
```

Resultado:

```csharp title="C#"
7
```
________________________________________
#### Predicate

Siempre devuelve un bool.

```csharp title="C#"
Predicate<int> esPar = x => x % 2 == 0;

Console.WriteLine(esPar(10));
```

Resultado:
```csharp title="C#"
True
```
________________________________________
#### Delegate vs Lambda

Muchos creen que son lo mismo.

No.

La lambda:

```csharp title="C#"
x => x > 10
```

No es un delegate.

Es una forma corta de escribir un método anónimo.

Luego el compilador la convierte en un delegate (o en un árbol de expresiones, dependiendo del contexto).
________________________________________
#### Delegate vs Evento

Un delegate puede invocarse directamente:

```csharp title="C#"
delegado();
```

Un evento (event) solo puede invocarse desde la clase que lo declara.

Por eso los eventos son más seguros.

¿Cuándo usar un delegate?
• Cuando un método necesita recibir otro método como parámetro.
• Para implementar callbacks.
• Para trabajar con eventos.
• En expresiones lambda.
• En consultas LINQ.
• En programación asíncrona y paralela.

________________________________________
#### Ejemplo del mundo real

Supón que tienes un método para registrar acciones:

```csharp title="C#"
public void Ejecutar(Action accion)
{
    Console.WriteLine("Iniciando...");

    accion();

    Console.WriteLine("Finalizado.");
}
```

Puedes reutilizarlo para distintas tareas:

```csharp title="C#"
Ejecutar(() =>
{
    Console.WriteLine("Guardando usuario...");
});

Ejecutar(() =>
{
    Console.WriteLine("Enviando correo...");
});
```

El método Ejecutar no sabe qué acción realizará; simplemente ejecuta el delegate que recibe.

Respuesta ideal para una entrevista

"Un delegate es un tipo seguro que almacena referencias a métodos con la misma firma. Permite pasar métodos como parámetros, implementar callbacks y desacoplar componentes. En C# se usa ampliamente como base de los eventos (event), las expresiones lambda y LINQ. En la práctica, hoy es común utilizar los delegates genéricos Action, Func y Predicate en lugar de definir delegates personalizados."

